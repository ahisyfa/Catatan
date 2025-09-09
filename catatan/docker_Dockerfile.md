# DockerFile
![Slide](https://docs.google.com/presentation/d/1bW0-88g_s54-X_rBLaZ-N2EhW3HngAZSN6UInyBlIn8/edit?slide=id.g125a9a30bb3_0_289#slide=id.g125a9a30bb3_0_289)

## From Instruction
- FROM digunakan untuk membuat build stage dari image yang kita tentukan
- Saat kita membuat Docker Image, biasanya perintah pertama adalah melakukan build stage dengan instruksi FROM
- Biasanya, jarang sekali kita akan membuat Docker Image dari scratch (kosongan), biasanya kita akan membuat Docker Image dari Docker Image lain yang sudah ada
- Untuk menggunakan FROM, kita bisa gunakan perintah :

```sh
# Command
FROM image:version

# Content in Dockerfile
FROM alpine:3

# build image
docker build -t ahisyfa/my-simpe-image from
```

## Run Instruction
- RUN adalah sebuah instruksi untuk mengeksekusi perintah di dalam image pada saat build stage. 
- Hasil perintah RUN akan di commit dalam perubahan image tersebut, jadi perintah RUN akan dieksekusi pada saat proses docker build saja, setelah menjadi Docker Image, perintah tersebut tidak akan dijalankan lagi. 
- Jadi ketika kita menjalankan Docker Container dari Image tersebut, maka perintah RUN tidak akan dijalankan lagi.

```Dockerfile
FROM alpine:3

RUN mkdir hello
RUN echo "Hello World" > "hello/world.txt"
RUN cat "hello/world.txt"
```
```sh
# build image
docker build -t ahisyfa/my-image-run run

# Display output
## add --progress=plain

# Disable cache
## --no-cahe

docker build -t ahisyfa/my-image-run run --progress=plain --no-cache

```

## Command Instruction
- CMD atau Command, merupakan instruksi yang digunakan ketika Docker Container berjalan
- CMD tidak akan dijalankan ketika proses build, namun dijalankan ketika Docker Container berjalan
- Dalam Dockerfile, kita tidak bisa menambah lebih dari satu instruksi CMD, jika kita tambahkan lebih dari satu instruksi CMD, maka yang akan digunakan untuk menjalankan Docker Container adalah instruksi CMD yang terakhir


```Dockerfile
FROM alpine:3

RUN mkdir hello
RUN echo "Hello World" > "hello/world.txt"

CMD cat "hello/world.txt"
```

```sh
docker build -t ahisyfa/my-image-command command --progress=plain --no-cache

docker container create --name my-container-command ahisyfa/my-image-command

```

## Label

## ADD Instruction
```Dockerfile
FROM alpine:3

RUN mkdir hello
RUN echo "Hello World" > "hello/world.txt"

CMD cat "hello/world.txt"
```


## COPY Instruction
