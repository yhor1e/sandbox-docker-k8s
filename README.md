# sandbox-docker-k8s

## todo

- [x] 🌟 Introduction to Docker 🌟
- [x] 🌟 Images, Containers, and Ports 🌟
- [ ] 🌟 Volumes 🌟
- [ ] 🌟 Building Images 🌟
- [ ] 🌟 Project: Build an Image for an API 🌟
- [ ] 🌟 Caching and Layers 🌟
- [ ] 🌟 Reducing Image Size 🌟
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

### Introduction to Docker

```
$ docker --version
```

```
$ docker ps
```

### Images, Containers, and Ports

```
$ docker pull nginx
```

```
$ docker images
```

```
docker run nginx:latest
```

```
docker container ls  # is the same as "docker ps"?
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
docker ps -a -q # -q is for displaying only id
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
