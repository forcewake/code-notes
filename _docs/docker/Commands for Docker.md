---
title: Commands for Docker
category: Docker
order: 1
---

Here are the commands that I've used for Docker before.

## Run nginx with mapping to port 80 with config from current folder

In `CMD`
``` cmd
docker run -d --restart always --name nginx -p 80:80 -v %cd%/nginx.conf:/etc/nginx/nginx.conf:ro nginx:1.15-alpine
```

In `bash` or `ps`
``` bash
docker run -d --restart always --name nginx -p 80:80 -v ${PWD}/nginx.conf:/etc/nginx/nginx.conf:ro nginx:1.15-alpine
```