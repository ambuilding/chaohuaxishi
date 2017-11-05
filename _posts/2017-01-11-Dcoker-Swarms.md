---
layout: post
title: Docker-Swarms
---

## Swarms
- A swarm is a group of machines that are running Docker and joined into a cluster. Join multiple machines into a “Dockerized” cluster called a swarm.

- Deploy this app onto a cluster, running it on multiple machines.

## Set up the swarm
 - Create a cluster / two VMs

    ```
	$ docker-machine create --driver virtualbox myvm1
	Running pre-create checks...
	(myvm1) No default Boot2Docker ISO found locally, downloading the latest release...
	(myvm1) Latest release for github.com/boot2docker/boot2docker is v17.10.0-ce
	(myvm1) Downloading /Users/william/.docker/machine/cache/boot2docker.iso from https://github.com/boot2docker/boot2docker/releases/download/v17.10.0-ce/boot2docker.iso...
	(myvm1) 0%....10%....20%....30%....40%....50%....60%....70%....80%....90%....100%
	Creating machine...
	(myvm1) Copying /Users/william/.docker/machine/cache/boot2docker.iso to /Users/william/.docker/machine/machines/myvm1/boot2docker.iso...
	(myvm1) Creating VirtualBox VM...
	(myvm1) Creating SSH key...
	(myvm1) Starting the VM...
	(myvm1) Check network to re-create if needed...
	(myvm1) Found a new host-only adapter: "vboxnet0"
	(myvm1) Waiting for an IP...
	Waiting for machine to be running, this may take a few minutes...
	Detecting operating system of created instance...
	Waiting for SSH to be available...
	Detecting the provisioner...
	Provisioning with boot2docker...
	Copying certs to the local machine directory...
	Copying certs to the remote machine...
	Setting Docker configuration on the remote daemon...
	Checking connection to Docker...
	Docker is up and running!
	To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env myvm1
	```
 - List the VMS and get their IP: `docker-machine ls`
 - Initialize the swarm and add nodes:

    ```
    $ docker-machine ssh myvm1 "docker swarm init --advertise-addr 192.168.99.100"
	Swarm initialized: current node (m5ddcbmwk63e2ao182szg8vfq) is now a manager.

	To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-4qgigh1juhts0mqfn2kgpxxm1cmt4a5ymow4zah4vrhhlb4tot-82oa8jfmzf6v130ow1dsief73 192.168.99.100:2377

	To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
    ```

    ```
    $ docker-machine ssh myvm2 "docker swarm join --token SWMTKN-1-4qgigh1juhts0mqfn2kgpxxm1cmt4a5ymow4zah4vrhhlb4tot-82oa8jfmzf6v130ow1dsief73 192.168.99.100:2377"
    This node joined a swarm as a worker.
    ```
- View the nodes in the first swarm `docker-machine ssh myvm1 "docker node ls"`

## Deploy the app on the swarm cluster

- Configure a `docker-machine` shell to the swarm manager. Run `docker-machine env myvm1` to get the command to configure the shell to talk to myvm1.

    ```
    $ docker-machine env myvm1
	export DOCKER_TLS_VERIFY="1"
	export DOCKER_HOST="tcp://192.168.99.100:2376"
	export DOCKER_CERT_PATH="/Users/william/.docker/machine/machines/myvm1"
	export DOCKER_MACHINE_NAME="myvm1"
	# Run this command to configure your shell:
	# eval $(docker-machine env myvm1)
    ```

## Deploy the app on the swarm manager:
- `docker stack deploy -c docker-compose.yml getstartedlab`
- `$ docker stack ps getstartedlab`

## Accessing the cluster:
-The network we created is shared between them and load-balancing. We can access the app from the IP address of either myvm1 or myvm2.

## Cleanup and reboot

- Tear down the stack `docker stack rm getstartedlab`
- Remove swarm `docker-machine ssh myvm2 "docker swarm leave"` on the worker and `docker-machine ssh myvm1 "docker swarm leave --force"` on the manager.
- Unsetting docker-machine shell variable settings `eval $(docker-machine env -u)`
