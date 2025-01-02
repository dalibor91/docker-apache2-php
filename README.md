# Dockerised apache2 & php

Repo provides tools that builds docker images for runing php using apache.
It supports multiple versions of php 

```sh
docker login 

export IMAGE_REPO="dbor91/apache2-php" 
export IMAGE_VERSION=7.4

bin/build-image

docker push "$IMAGE_REPO:$IMAGE_VERSION"
```