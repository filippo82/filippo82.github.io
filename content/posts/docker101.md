+++
draft = true
date = 2021-01-25T22:01:47+01:00
updated = 2021-01-25T22:01:47+01:00
title = "Docker 101"
description = ""
slug = ""
authors = ["Filippo"]
tags = [
    "docker"
]
categories = []
externalLink = ""
series = [
    "Docker"
]
+++

## Build an image

```shell
docker build -t fastapi_simple .
```

## Run an image locally

```shell
docker run -d --name mycontainer -p 80:80 fastapi_simple
```

## Login into DockerHub

```shell
docker login
```

## Tag an image

```shell
docker tag fastapi_simple filippo82/fastapi_simple:0.0.1
```

## Push an image to DockerHub

```shell
docker push filippo82/fastapi_simple:0.0.1
```
