# Linux Command Line Pipes and Redirection
#linux #pipe #redirection

## Resource
- [Linux Command Line Pipes and Redirection](https://www.youtube.com/watch?v=mV_8GbzwZMM)
- [Sample Code](https://github.com/engineer-man/youtube/blob/master/102/examples.sh)

## Key Point
## File Descriptor
A file descriptor is a unique, non-negative integer that the operating system assigns to an open file, socket, or other input/output resource for a process to use. It acts as a handle or ticket, allowing a program to interact with that resource through system calls like read() and write(). The three default file descriptors for every process are 0 for standard input, 1 for standard output, and 2 for standard error.  


**Unique identifier**: Each open file or resource gets a unique integer file descriptor within a process, making it easy for the program to distinguish between them. 

**Kernel interface:** The operating system uses the file descriptor to look up its internal data structures and perform operations on the file, such as reading, writing, or seeking. 

**Process-specific:** A process has its own set of file descriptors. When a child process is created, it inherits the file descriptors from the parent, sharing the same open files and their states. 

**Default descriptors**: By default, every new process has three file descriptors already open: 

- 0: Standard input (stdin) 
- 1: Standard output (stdout) 
- 2: Standard error (stderr) 

**Importance of closing:** It is crucial to close file descriptors when they are no longer needed. Failing to do so can lead to resource leakage and hit the system's file descriptor limit, which can cause errors or failures when trying to open new files. 

## Pipeline
### Anonymous Pipeline
Syntax: `|`

```bash
ls -l | grep keywrod | wc -l
```

### Named Pipeline
You need to uderstand `redirection` concept before use named pipeline.

Syntax:
```bash
mkfifo mypipe
program1 > mypipe
program2 < mypipe
```

## Redirection
Redirection and pipes are very similar, except pipes deal primarily with the output of a program whereas redirection deals with the input of files and in the output to files.   
Syntax : 
- `>` to truncate and rewrite
- `>>` to append

```bash
program1 > out.log 2>&1
=> send std-out to out.log file and send std-err to std-out
```


## Full Sample Command

```bash
#!/usr/bin/env bash

# default fds
0 stdin
1 stdout
2 stderr

# run program1, stdout/stderr to terminal (default)
program1

# send stdout from program1 to stdin of program2 with anonymous pipe
program1 | program2

# run program1, stdout to out.log, stderr to terminal
program1 1> out.log
program1 > out.log

# run program1, stdout/stderr to out.log, nothing to terminal
program1 1> out.log 2> out.log
program1 > out.log 2> out.log
program1 > out.log 2>&1

# run program1 with input.txt as input,
# stdout/stderr to terminal
program1 < input.txt
cat input.txt | program1

# run program1 with input.txt to stdin,
# stdout to output.txt, stderr to terminal
program1 < input.txt > output.txt
cat input.txt | program1 > output.txt

# send stdout from program1 to stdin of program2 with named pipe
mkfifo mypipe
program1 > mypipe
program2 < mypipe

# run program1, discard all output
program1 > /dev/null 2>&1

# run ./write, send fd4 to out.log (see write.c)
./write 4> out.log
```