---
layout: default
title: Docker-Compose
parent: Dashboard
nav_order: 1
---

# Docker-Compose
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## docker-compose.yml

Here, there's a brief of the services included in the docker-compose

```yml
version: '3'
services:
    mysql:
        image: mysql:latest
    ...
    mysql-workbench:
        image: jdecool/mysql-workbench
```
Docker compose based on docker image:
[jdecool MySQL Workbench image in dockerhub](https://hub.docker.com/r/jdecool/mysql-workbench).

## MySQL

```yml
mysql:
    image: mysql:latest
    container_name: mysql
    volumes:
        - ./.mysql-data/db:/var/lib/mysql
    restart: always
    ports:
        - 3306:3306
    environment:
        - MYSQL_DATABASE=dashboard
        - MYSQL_ROOT_PASSWORD=admin
        
```    

## Running GUI apps into docker container (MySQL-Workbench)

```yml
    mysql-workbench:
        image: jdecool/mysql-workbench
        container_name: mysql-workbench
        volumes:
            - /tmp/.X11-unix:/tmp/.X11-unix
            - ./.mysql-workbench:/root/.mysql/workbench
        network_mode: host
        environment:
            - DISPLAY=unix${DISPLAY}
        
```        
- /tmp.X11-unix ⇢
- /root/.mysql/workbench ⇢
- network_mode: host ⇢
- DISPLAY=UNIX${DISPLAY} ⇢

