# Dockerised PHP & apache2 

Repo provides tooling for building images that have baked in [PHP](https://www.php.net/), [composer](https://getcomposer.org/) and [apache2](https://httpd.apache.org/).

Supported versions of PHP:

- **PHP 5.6** 
- **PHP 7.0** 
- **PHP 7.1** 
- **PHP 7.2** 
- **PHP 7.4** 
- **PHP 8.0** 
- **PHP 8.1** 
- **PHP 8.2** 
- **PHP 8.3** 
- **PHP 8.4**

Published images can be found [on docker hub](https://hub.docker.com/repository/docker/dbor91/apache2-php)

## Building

To build different images first you need to set image name that will be used as base.
This is done by setting `IMAGE_REPO` variable and different versions will be appended as tags to this name.

```sh 
# For example base image 'dbor91/apache2-php'

export IMAGE_REPO="dbor91/apache2-php" 
```

### Building All Versions

To build all supported versions you can simply run 

```sh
bin/build-image 
```

This will loop over all supported versions and create images, to list them all 

```sh
docker image ls | grep $IMAGE_REPO
```

### Building Specific Versions

To build specific version you need to specify `IMAGE_VERSION` variable

```sh
# for example 7.4 

export IMAGE_VERSION="7.4"
```

Then just run same script as for building all images 

```sh
bin/build-image 
```

### Publishing 

You can generate publish command for all built images by simply running

```sh
docker image ls | grep $IMAGE_REPO | awk '{ print "docker push "$1":"$2 }'
```


### Debugging 

`bin/build-image` produces `record.log` file which logs which docker commands we run and output of those, can be used to debug if something fails

## Testing

To test different versions you can use `docker compose` to check built images. 
Setting `PHP_VERSION` variable to specify which version you want to run before `docker compose` allows you to switch between different versions.


To just print php version in terminal run

```sh
PHP_VERSION="5.6" docker compose run php php -r 'echo phpversion();'
PHP_VERSION="7.0" docker compose run php php -r 'echo phpversion();'
PHP_VERSION="7.1" docker compose run php php -r 'echo phpversion();'
PHP_VERSION="7.2" docker compose run php php -r 'echo phpversion();'
PHP_VERSION="7.4" docker compose run php php -r 'echo phpversion();'
PHP_VERSION="8.0" docker compose run php php -r 'echo phpversion();'
PHP_VERSION="8.1" docker compose run php php -r 'echo phpversion();'
PHP_VERSION="8.2" docker compose run php php -r 'echo phpversion();'
PHP_VERSION="8.3" docker compose run php php -r 'echo phpversion();'
PHP_VERSION="8.4" docker compose run php php -r 'echo phpversion();'
```

If you want to see php version from apache2 simply run command bellow
targeting correct PHP version and visit [localhost:8080](http://localhost:8080/) in browser

```sh 
PHP_VERSION="5.6" docker compose run --service-ports php
PHP_VERSION="7.0" docker compose run --service-ports php
PHP_VERSION="7.1" docker compose run --service-ports php
PHP_VERSION="7.2" docker compose run --service-ports php
PHP_VERSION="7.4" docker compose run --service-ports php
PHP_VERSION="8.0" docker compose run --service-ports php
PHP_VERSION="8.1" docker compose run --service-ports php
PHP_VERSION="8.2" docker compose run --service-ports php
PHP_VERSION="8.3" docker compose run --service-ports php
PHP_VERSION="8.4" docker compose run --service-ports php
```
