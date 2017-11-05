---
layout: post
title: Docker-Services
---

- In a distributed application, different pieces of the app are called “services.” Services are really just “containers in production.”

- Scaling a service changes the number of container instances running that piece of software, assigning more computing resources to the service in the process.

- Define, run, and scale services with the Docker platform – just write a `docker-compose.yml`

- Run the new load-balanced app: `docker swarm init`

	Swarm initialized: current node (su2np68tvril4xcjp20odfbyt) is now a manager.

	To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-3tp2gkfp3a4yxp93tf0ozz62isazfbvoldtsusdo06dk725wgq-4eleytibu50vbcnlx8v61b9nq 192.168.65.2:2377

	To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.

- `docker stack deploy -c docker-compose.yml appname` `docker service ls` List the tasks for the service: `docker service ps getstartedlab_web` `docker container ls -q`

- Run `curl -4 http://localhost` or visit that URL in the browser. Either way, the  container ID wil change, demonstrating the load-balancing; with each request, one of the 5 tasks is chosen, in a round-robin fashion, to respond. The container IDs will match your output from the previous command (docker container ls -q).

### Take down the app and the swarm

- Take the app down with `docker stack rm <appName>`
- Take down the swarm `docker swarm leave --force`
