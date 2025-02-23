# Docker PHP-FPM 8.2 & Nginx 1.24 on Alpine Linux 3.18

WORK IN PROGRESS. USAGE WILL BE ADDED ONCE EVERYTHING IS SET UP

* Built on the lightweight and secure Alpine Linux distribution
* Very small Docker image size (+/-35MB)
* Uses PHP 8 for better performance, lower CPU usage & memory footprint
* Optimized for 100 concurrent users
* Optimized to only use resources when there's traffic (by using PHP-FPM's on-demand PM)
* The servers Nginx, PHP-FPM and supervisord run under a non-privileged user (nobody) to make it more secure
* The logs of all the services are redirected to the output of the Docker container (visible with `docker logs -f <container name>`)
* Follows the KISS principle (Keep It Simple, Stupid) to make it easy to understand and adjust the image to your needs

![nginx 1.22.0](https://img.shields.io/badge/nginx-1.22-brightgreen.svg)
![php 8](https://img.shields.io/badge/php-8-brightgreen.svg)
![License MIT](https://img.shields.io/badge/license-MIT-blue.svg)

### Includes

* Composer
* WP-CLI
* GD2
* Various other extensions (like SimpleXML)
* MySQL CLI

This image is built on GitHub actions and hosted on the GitHub Docker images repo. It is also available under `khromov/alpine-nginx-php8` on [Docker Hub](https://hub.docker.com/r/khromov/alpine-nginx-php8).

WORK IN PROGRESS. USAGE WILL BE ADDED ONCE EVERYTHING IS SET UP

This is convenient for developing Laravel, WordPress or Drupal sites. It includes MySQL and phpMyAdmin

```
docker-compose up
```

Now you can access your site at http://localhost:8080 and the MySQL database at `db:3306`.

The folder `./src-compose` will be created and you can put your project files there.

The urls are:
* Web: http://localhost:8080
* phpMyAdmin: http://localhost:8081

###### File permission issues

If you copied files into `./src-compose` you need to run:

```
sudo chown -R nobody:nogroup ./src-compose
sudo chmod -R 777 ./src-compose
```

This makes sure that the files have the correct owner inside the container but remain writable outside of it.

#### Quick build / run

```
docker build . -t php8
docker run -p 8080:8080 -t php8
```

Go to:  
http://localhost:8080/

## Configuration
In [config/](config/) you'll find the default configuration files for Nginx, PHP and PHP-FPM.
If you want to extend or customize that you can do so by mounting a configuration file in the correct folder.

## Acknowledgements

Forked from [khromov/alpine-nginx-php8](https://github.com/khromov/alpine-nginx-php8)

Inspired by [TrafeX/docker-php-nginx](https://github.com/TrafeX/docker-php-nginx) and [this subsequent fork](https://github.com/khromov/docker-php-nginx).
