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
Jika Docker Image seperti installer aplikasi, maka docker Cintainer mirip seperti aplikasi hasil installernya.
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
```
docker container create --name my-mongo --publish 27017:27017 --env MONGO_INITDB_ROOT_USERNAME=amin --env MONGO_INITDB_ROOT_PASSWORD=amin mongo:latest
```
