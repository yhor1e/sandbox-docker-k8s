# sandbox-docker-k8s

## todo

- [x] 🌟 Introduction to Docker 🌟
- [x] 🌟 Images, Containers, and Ports 🌟
- [x] 🌟 Volumes 🌟
- [x] 🌟 Building Images 🌟
- [x] 🌟 Project: Build an Image for an API 🌟
- [x] 🌟 Caching and Layers 🌟
- [x] 🌟 Reducing Image Size 🌟
- [x] 🌟 Tags and Versioning 🌟
- [x] 🌟 Image Registries 🌟
- [x] 🌟 Debugging Containers 🌟
- [ ] 🌟 Introduction to Kubernetes 🌟
- [ ] 🌟 Kubernetes Architecture & Components 🌟
- [ ] 🌟 Developing Locally 🌟
- [ ] 🌟 Project: MongoDB and Mongo Express 🌟e end 🎉


## ref

* https://www.youtube.com/watch?v=t8GbPocwQW0

## note

### Introduction to Kubernetes

### Debugging Containers

```
$ docker inspect cf1ea1e1a7bf  # or name
```

```
$ docker logs cf1ea1e1a7bf 
```

```
$ docker logs -f cf1ea1e1a7bf  # -f: follow
```

```
$ docker exec -it  2a00473593e7f /bin/sh
```

### Image Registries

* 2FA を有効にしている場合は Access Token が必要。
  - https://docs.docker.com/docker-hub/access-tokens/

```
$ docker push yhor1e/website:1
$ docker push yhor1e/website:2
$ docker push yhor1e/website:latest
```

```
$ docker pull yhor1e/website # download latest
```

```
docker run --name yhor1e-website -p 9000:80 -d yhor1e/website:latest
```

### Tags and Versioning

```diff
+ FROM nginx:1.17.2-alpine
- FROM nginx:alpine
ADD . /usr/share/nginx/html
```

```diff
+ FROM node:12.19.0-alpine
- FROM node:alpine
WORKDIR /app
ADD package*.json ./
RUN npm install
ADD . .
CMD node index.js
```

```diff
$ docker tag amigoscode-website:latest amigoscode-website:1
$ docker image ls
REPOSITORY           TAG                 IMAGE ID            CREATED             SIZE
user-service-api     latest              a1a845b148ba        8 minutes ago       126MB
+ amigoscode-website   1                   758c4646f93c        9 minutes ago       22.5MB
amigoscode-website   latest              758c4646f93c        9 minutes ago       22.5MB
```

```
$ docker run --name amigoscode-latest -p 8080:80 -d amigoscode-website:latest 
cec4c2a68abb00e0b0ca483ce8ddfa4101a0759f7bd14275bb24a013107517b2

$ docker run --name amigoscode-2 -p 8082:80 -d amigoscode-website:2 
e3cf906a7c7165831a103ec7c430b983a80751bdac6f5c9564d042ee9b46a85a

$ docker run --name amigoscode-1 -p 8081:80 -d amigoscode-website:1
e91091f897098766920059dc2cf58c260fc1db33571208433f98c5ae50d20921
```

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
