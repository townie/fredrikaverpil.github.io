---
layout: post
title: Docker cleanup
tags: [docker]
---

Quick and easy way to remove all containers and all images along with their volumes:

```bash
# Remove containers and their volumes
docker stop $(docker ps -a -q)
docker rm -v $(docker ps -a -q)

# Remove images
docker rmi -f $(docker images -q)
```
