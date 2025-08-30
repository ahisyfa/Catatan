# Docker

## Architecture
- Docker use Client-Server 

## Docker Image
- Docker Image mirip seperti installler aplikasi

Melihat Docker Image
```
docker image ls
```

Download Docker Image
```
docker pull redis:latest
or
docker image pull redis:latest
```

Delete Docker Image
```
docker image rm redis:latest
```

## Docker Container
Jika Docker Image seperti installer aplikasi, maka docker Container mirip seperti aplikasi hasil installernya.
Satu Docker Image bisa digunakan untuk membuat banyak docker container.
Jika suatu Docker Image sudah dibuat menjadi Docker Container, maka tidak bisa dihapus karena isinya sedang digunakan di docker container.
### Container Status
- Saat container dibuat, tidak langsung dibuat

**Command**
```
# Melihat semua container
docker container ls -a

# Membuat Container
docker container create --name my-redis redis:latest

# Menjalanakan container
docker container start my-redis

# menghentikan container
docker container stop my-redis

# Menghapus container
docker container rm my-redis

```

### Container Log
Untuk melihat log dalam container
```
# Melihat Log
docker container logs my-redis
or
docker container logs -f my-redis
```

### Container Exec
Untuk masuk ke dalam container

```
docker container exec -i -t my-redis /bin/bash
```

### Container Port
```

# Port Forwading
docker container create --name my-nginx --publish 8080:80 nginx:latest
```

### Container Environment Variable
```sh
docker container create --name my-mongo --publish 27017:27017 --env MONGO_INITDB_ROOT_USERNAME=amin --env MONGO_INITDB_ROOT_PASSWORD=amin mongo:latest
```

### Container Stats
```sh
docker container stats 
```


### Container Resource Limit
- Saat membuat container, secara default dia akan menggunakan semua CPU dan Memory yang diberikan ke Docker (Mac dan Windows), dan akan menggunakan semua CPU dan Memory yang tersedia di sistem Host (Linux)
- Jika terjadi kesalahan, misal container terlalu banyak memakan CPU dan Memory, maka bisa berdampak terhadap performa container lain, atau bahkan ke sistem host
- Oleh karena itu, ada baiknya ketika kita membuat container, kita memberikan resource limit terhadap container nya

**Memory**
- Saat membuat container, kita bisa menentukan jumlah memory yang bisa digunakan oleh container ini, dengan menggunakan perintah --memory diikuti dengan angka memory yang diperbolehkan untuk digunakan
- Kita bisa menambahkan ukuran dalam bentu b (bytes), k (kilo bytes), m (mega bytes), atau g (giga bytes), misal 100m artinya 100 mega bytes

**CPU**

```sh
docker container create --name my-small-nginx --publish 8081:80 --memory 100m --cpus 1 nginx:latest 
```
![alt text](../images/container-stats-1.png)


### Bind Mounts
- Bind Mounts merupakan kemampuan melakukan mounting (sharing) file atau folder yang terdapat di sistem host ke container yang terdapat di docker
- Fitur ini sangat berguna ketika misal kita ingin mengirim konfigurasi dari luar container, atau misal menyimpan data yang dibuat di aplikasi di dalam container ke dalam folder di sistem host
- Jika file atau folder tidak ada di sistem host, secara otomatis akan dibuatkan oleh Docker
- Untuk melakukan mounting, kita bisa menggunakan parameter --mount ketika membuat container
- Isi dari parameter --mount memiliki aturan tersendiri

**Parameter Mount**
| Parameter   | Keterangan |
| -------     | ------     |
| type        | Tipe mount, bind atau volume           |
| source      | Lokasi file atau folder di sistem host |
| destination | Lokasi file atau folder di container   |
| readonly    | Jika ada, maka file atau folder hanya bisa dibaca di container, tidak bisa ditulis |


```sh
docker container create --name my-mounted-mongo --mount "type=bind,source=/home/amin/Documents/lab/hello-docker,destination=/data/db" --publish 27018:27017 --env MONGO_INITDB_ROOT_USERNAME=amin --env  MONGO_INITDB_ROOT_PASSWORD=amin1234 mongo:latest
```


### Docker Volume
- Fitur Bind Mounts sudah ada sejak Docker versi awal, di versi terbaru direkomendasikan menggunakan Docker Volume
- Docker Volume mirip dengan Bind Mounts, bedanya adalah terdapat management Volume, dimana kita bisa membuat Volume, melihat daftar Volume, dan menghapus Volume
- Volume sendiri bisa dianggap storage yang digunakan untuk menyimpan data, bedanya dengan Bind Mounts, pada bind mounts, data disimpan pada sistem host, sedangkan pada volume, data di manage oleh Docker

**Melihat Docker Volume**  
- Saat kita membuat container, dimanakah data di dalam container itu disimpan, secara default semua data container disimpan di dalam volume
- Jika kita coba melihat docker volume, kita akan lihat bahwa ada banyak volume yang sudah terbuat, walaupun kita belum pernah membuatnya sama sekali
- Kita bisa gunakan perintah berikut untuk melihat daftar volume :
`docker volume ls`

```sh
# create
docker volume create my-volume

# delete - stop the container that use the volume first
docker volume rm my-volume
```


### Container Volume
```sh
# create volume
docker volume create my-mongo-volume

## Create container with volume
docker container create --name my-volumed-mongo --mount "type=volume,source=my-mongo-volume,destination=/data/db" --publish 27019:27017 --env MONGO_INITDB_ROOT_USERNAME=amin --env  MONGO_INITDB_ROOT_PASSWORD=amin1234 mongo:latest
```


### Backup Volume
- Sayangnya, sampai saat ini, tidak ada cara otomatis melakukan backup volume yang sudah kita buat
- Namun kita bisa memanfaatkan container untuk melakukan backup data yang ada di dalam volume ke dalam archive seperti zip atau tar.gz  

**Tahapan Melakukan Backup**
- Matikan container yang menggunakan volume yang ingin kita backup
- Buat container baru dengan dua mount, volume yang ingin kita backup, dan bind mount folder dari sistem host
- Lakukan backup menggunakan container dengan cara meng-archive isi volume, dan simpan di bind mount folder
- Isi file backup sekarang ada di folder sistem host
- Delete container yang kita gunakan untuk melakukan backup


```sh
docker container stats 
```


### Restore Volume
```sh
docker container stats 
```


### Docker Network
![Docker Networks](../images/docker-network-ls.png)

**Docker Network**   
- Saat kita membuat container di docker, secara default container akan saling terisolasi satu sama lain, jadi jika kita mencoba memanggil antar container, bisa dipastikan bahwa kita tidak akan bisa melakukannya
- Docker memiliki fitur Network yang bisa digunakan untuk membuat jaringan di dalam Docker
- Dengan menggunakan Network, kita bisa mengkoneksikan container dengan container lain dalam satu Network yang sama
- Jika beberapa container terdapat pada satu Network yang sama, maka secara otomatis container tersebut bisa saling berkomunikasi

**Network Driver**
- Saat kita membuat Network di Docker, kita perlu menentukan driver yang ingin kita gunakan, ada banyak driver yang bisa kita gunakan, tapi kadang ada syarat sebuah driver network bisa kita gunakan.
- bridge, yaitu driver yang digunakan untuk membuat network secara virtual yang memungkinkan container yang terkoneksi di bridge network yang sama saling berkomunikasi
- host, yaitu driver yang digunakan untuk membuat network yang sama dengan sistem host. host hanya jalan di Docker Linux, tidak bisa digunakan di Mac atau Windows
- none, yaitu driver untuk membuat network yang tidak bisa berkomunikasi 



```sh
# List network
docker network ls 

## create network
docker network create --driver bridge my-network-1 

## Remove network
docker network rm my-network-1 
```


### Container Network
- Setelah kita membuat Network, kita bisa menambahkan container ke network
- Container yang terdapat di dalam network yang sama bisa saling berkomunikasi (tergantung jenis driver network nya)
- Container bisa mengakses container lain dengan menyebutkan hostname dari container nya, yaitu nama container nya

```sh
# Untuk menambahkan container ke network, kita bisa menambahkan perintah --network ketika membuat container, misal :
docker container create --name namacontainer --network namanetwork image:tag

# 1. Create network  
docker network create --driver bridge my--mongo-network

# 2. Create Container MongoDB
docker container create --name my-networked-mongo --network my--mongo-network --env MONGO_INITDB_ROOT_USERNAME=user_amin --env  MONGO_INITDB_ROOT_PASSWORD=amin1234 mongo:latest

# 3. Create Container Mongo-Express
docker container create --name my-networked-mongo-express --network my--mongo-network --env ME_CONFIG_MONGODB_URL="mongodb://user_amin:amin1234@my-networked-mongo:27017" --publish 8082:8081 mongo-express:latest

# 5. Start the cpntainers
docker container start my-networked-mongo 
docker container start my-networked-mongo-express

# Diconnect container from some network
docker network disconnect my--mongo-network my-networked-mongo

## Attach pre-create container to a network
docker network connect my--mongo-network my-networked-mongo

```


### Inspect
- Setelah kita men-download image, atau membuat network, volume dan container. Kadang kita ingin melihat detail dari tiap hal tersebut
- Misal kita ingin melihat detail dari image, perintah apa yang digunakan oleh image tersebut? Environment variable apa yang digunakan? Atau port apa yang digunakan?
- Misal kita juga ingin melihat detail dari container, Volume apa yang digunakan? Environment variable apa yang digunakan? Port forwarding apa yang digunakan? dan lain-lain
- Docker memiliki fitur bernama inspect, yang bisa digunakan di image, container, volume dan network
- Dengan fitur ini, kita bisa melihat detail dari tiap hal yang ada di Docker

```sh
# Untuk melihat detail dari image, gunakan : 
docker image inspect namaimage

#Untuk melihat detail dari container, gunakan : 
docker container inspect namacontainer

# Untuk melihat detail dari volume, gunakan : 
docker volume inspect namavolume

#Untuk melihat detail dari network, gunakan : 
docker network inspect namanetwork

```


### Prune
- Saat kita menggunakan Docker, kadang ada kalanya kita ingin membersihkan hal-hal yang sudah tidak digunakan lagi di Docker, misal container yang sudah di stop, image yang tidak digunakan oleh container, atau volume yang tidak digunakan oleh container
- Fitur untuk membersihkan secara otomatis di Docker bernama prune
- Hampir di semua perintah di Docker mendukung prune

```sh
# Untuk menghapus semua container yang sudah stop, gunakan : 
docker container prune

# Untuk menghapus semua image yang tidak digunakan container, gunakan : 
docker image prune

# Untuk menghapus semua network yang tidak digunakan container, gunakan : 
docker network prune

# Untuk menghapus semua volume yang tidak digunakan container, gunakan : 
docker volume prune

# Atau kita bisa menggunakan satu perintah untuk menghapus container, network dan image yang sudah tidak digunakan menggunakan perintah :
docker system prune

```


