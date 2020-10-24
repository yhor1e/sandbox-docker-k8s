# sandbox-docker-k8s

## todo

- [x] 🌟 Introduction to Docker 🌟
- [x] 🌟 Images, Containers, and Ports 🌟
- [x] 🌟 Volumes 🌟
- [x] 🌟 Building Images 🌟
- [x] 🌟 Project: Build an Image for an API 🌟
- [x] 🌟 Caching and Layers 🌟
- [x] 🌟 Reducing Image Size 🌟
- [ ] 🌟 Tags and Versioning 🌟
- [ ] 🌟 Image Registries 🌟
- [ ] 🌟 Debugging Containers 🌟
- [ ] 🌟 Introduction to Kubernetes 🌟
- [ ] 🌟 Kubernetes Architecture & Components 🌟
- [ ] 🌟 Developing Locally 🌟
- [ ] 🌟 Project: MongoDB and Mongo Express 🌟e end 🎉


## ref

* https://www.youtube.com/watch?v=t8GbPocwQW0

## note

### Reducing Image Size

```
$ docker pull node:lts-alpine
```

```
$ docker image ls
```

```
$ docker pull nginx:alpine      
```

### Caching and Layers

`.dockerignore`
```
node_modules
Dockerfile
.git
```

`Dockerfile` **To use cache setting**
```diff
FROM node:latest
WORKDIR /app
+ ADD package*.json ./
+ RUN npm install
ADD . .
- RUN npm install
CMD node index.js
```


### Project: Build an Image for an API

```
FROM node:latest
WORKDIR /app
ADD . .
RUN npm install
CMD node index.js
```

```
$ docker build -t user-service-api:latest .
```

```
$ docker run --name user-api -d -p 3000:3000 user-service-api:latest
```

### Building Images

`Dockerfile`
```
FROM nginx:latest
ADD . /usr/share/nginx/html
```

```
$ docker build --tag website:latest   # . : where Docker file is.
```

```
$ docker run --name website -p 8080:80 -d website:latest 
```

### Volumes

```
$ docker run --name website -v $(pwd):/usr/share/nginx/html:ro  -d -p 8080:80 nginx:latest  # ro -> read only
```

```
$ docker exec -it website bash
```

```
$ docker run --name website -v $(pwd):/usr/share/nginx/html  -d -p 8080:80 nginx:latest
```

```
$ docker run --name website-copy --volumes-from website -d -p 8081:80 nginx:latest
```


### Images, Containers, and Ports

```
$ docker pull nginx
```

```
$ docker images
```

```
$ docker run nginx:latest
```

```
$ docker container ls  # is the same as "docker ps"?
```

```
$ docker run -d nginx:latest  # detach mode
```

```
$ docker stop 5caeec4293f8 # container id
```

```
$ docker run -d -p 8080:80 nginx:latest 
```

```
$ docker run -d -p 8080:80 -p 3000:80 nginx:latest # both port are portforwarded to 80
```

```
$ docker stop agitated_margulis  # container name
```

```
$ docker start priceless_jepsen # ran container name
```

```
$ docker ps -a
```

```
$ docker rm 7d71094bca43 # rm container
```

```
$ docker ps -a -q # -q is for displaying only id
```

```
$ docker rm $(docker ps -aq)  # Remove all container
```

```
$ docker rm -f $(docker ps -aq) # Remove even running containers forcely
```

```
$ docker run --name website -d -p 3000:80 -p 8080:80 nginx:latest  # Specify name
```

### Introduction to Docker

```
$ docker --version
```

```
$ docker ps
```
