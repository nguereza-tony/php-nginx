# Docker PHP-FPM 8.0 & Nginx 1.26 on Alpine Linux
PHP-FPM 8.0 & Nginx 1.26 container image for Docker, built on [Alpine Linux](https://www.alpinelinux.org/).

Repository: https://github.com/nguereza-tony/php-nginx  
Inspired from `TrafeX/docker-php-nginx`

* Built on the lightweight and secure Alpine Linux distribution
* Multi-platform, supporting AMD4, ARMv6, ARMv7, ARM64
* Very small Docker image size (+/-100MB)
* Uses PHP 8.0 for the best performance, low CPU usage & memory footprint
* Optimized for 100 concurrent users
* Optimized to only use resources when there's traffic (by using PHP-FPM's `on-demand` process manager)
* The services Nginx, PHP-FPM and supervisord run under a non-privileged user (nobody) to make it more secure
* The logs of all the services are redirected to the output of the Docker container (visible with `docker logs -f <container name>`)
* Follows the KISS principle (Keep It Simple, Stupid) to make it easy to understand and adjust the image to your needs

[![Docker Pulls](https://img.shields.io/docker/pulls/nguereza/php-nginx.svg)](https://hub.docker.com/r/nguereza/php-nginx/)
![nginx 1.26](https://img.shields.io/badge/nginx-1.26-brightgreen.svg)
![php 8.0](https://img.shields.io/badge/php-8.0-brightgreen.svg)
![License MIT](https://img.shields.io/badge/license-MIT-blue.svg)

## Goal of this project
The goal of this container image is to provide an example for running Nginx and PHP-FPM in a container which follows
the best practices and is easy to understand and modify to your needs.

## Usage

Start the Docker container:

```bash
    docker run -p 80:8080 nguereza/php-nginx
```

See the PHP info on http://localhost, or the static html page on http://localhost/test.html

Or mount your own code to be served by PHP-FPM & Nginx
```bash
    docker run -p 80:8080 -v ~/my-codebase:/var/www/html nguereza/php-nginx
```
## Versioning
Major or minor changes are always published as a [release](https://github.com/nguereza-tony/php-nginx/releases) with correspondending changelogs.

## Configuration
In [config/](config/) you'll find the default configuration files for Nginx, PHP and PHP-FPM.
If you want to extend or customize that you can do so by mounting a configuration file in the correct folder;

Nginx configuration:
```bash
    docker run -v "`pwd`/nginx-server.conf:/etc/nginx/conf.d/server.conf" nguereza/php-nginx
```
PHP configuration:
```bash
    docker run -v "`pwd`/php-setting.ini:/etc/php80/conf.d/settings.ini" nguereza/php-nginx
```
PHP-FPM configuration:
```bash
    docker run -v "`pwd`/php-fpm-settings.conf:/etc/php80/php-fpm.d/server.conf" nguereza/php-nginx
```
_Note; Because `-v` requires an absolute path I've added `pwd` in the example to return the absolute path to the current directory_