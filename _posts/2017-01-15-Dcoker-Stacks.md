---
layout: post
title: Docker-Stacks
---

## Stacks
- A stack is a group of interrelated services that share dependencies, and can be orchestrated and scaled together.

- Add a free visualizer service that lets us look at how the swarm is scheduling containers.

- Persist the data, add a Redis database for storing app data.
  - Add a Redis service.
  - Store data. Create a `./data` directory on the manager: `docker-machine ssh myvm1 "mkdir ./data"`
- Deploy and verify that the three services are running as expected.
