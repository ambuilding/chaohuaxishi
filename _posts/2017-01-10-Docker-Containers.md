---
layout: post
title: Docker-Containers
---

- Docker-new development environment: No installation / Dockerfile / Build

- Define a container with a Dockerfile. Dockerfile will define what goes on in the environment inside your container.

### Setup `$ docker run hello-world`


### Get Started

- `$ docker build -t name .` `$ docker images` `$ docker run -p 4000:80 name`
- `$ docker run -p 4000:80 name` `http://localhost:4000 / $ curl http://localhost:4000`
- `docker run -p 80:80 username/repo:tag` `http://localhost/`

- Run the app in the background, in detached mode: `docker run -d -p 4000:80 friendlyhello` See abbreviated container ID: `docker container ls` End th eprocess: `docker container stop <Container ID>`

### Tag / Publish the image
- `docker tag image username/repository:tag` `$ docker images`
- `docker push username/repository:tag`
- From now on, you can use docker run and run your app on any machine with this command: `docker run -p 4000:80 username/repository:tag `

### Git database

- Git tree `~/Library/Containers/com.docker.docker/Data` `com.docker.driver.amd64-linux`

- `$ docker info` `$ docker info | grep Proxy`

- Fuck

	# Set proxy server, replace host:port with values for your servers
	`ENV http_proxy socks5://127.0.0.1:1080`
	`ENV https_proxy socks5://127.0.0.1:1080`
