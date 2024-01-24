# Docker Nginx & PHP-FPM with Supervisor

![GitHub Workflow Status (branch)](https://img.shields.io/github/actions/workflow/status/breadhub-org/docker-nginx-php-fpm/docker-build.yml?branch=main) ![GitHub](https://img.shields.io/github/license/breadhub-org/docker-nginx-php-fpm)

Based Official PHP image: https://hub.docker.com/_/php with additional packages:

* Nginx
* Supervisor
* [renatomefi/php-fpm-healthcheck](https://github.com/renatomefi/php-fpm-healthcheck)

This repository will automatically update weekly.

## Supported PHP versions

Alpine:

* 8.3: `8.3`, `8`, `latest`
* 8.2: `8.2`,
* 8.1: `8.1`,
* 8: `8.0`,
* 7.4: `7.4`, `7`
* 7.3: `7.3`  # note: lots of vulnerabilities

Debian Buster:

* 8.3: `8.3-debian`, `8-debian`, `latest-debian`
* 8.2: `8.2-debian`,
* 8.1: `8.1-debian`,
* 8: `8.0-debian`

Check from Tags all supported versions and architectures.

## Usage (docker compose)

Run latest version

```sh
curl https://github.com/breadhub-org/docker-nginx-php-fpm/raw/main/docker-compose.yml -o docker-compose.yml
curl https://github.com/breadhub-org/docker-nginx-php-fpm/raw/main/configs/debian-nginx-default.conf -o config/nginx_default.conf
docker compose up -d
```

## Production image

To build image to production create `Dockerfile` to specify your own configuration. 

```Dockerfile
# Use breadhub-org/docker-nginx-php-fpm image
FROM ghcr.io/breadhub-org/docker-nginx-php-fpm:7.4

# Use production php.ini configuration and hide PHP-version
RUN cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini \
    && sed -i -e 's/expose_php = On/expose_php = Off/' /usr/local/etc/php/php.ini

# Do other changes like copy website files to image with COPY: https://docs.docker.com/engine/reference/builder/#copy
```

## License

[MIT](https://github.com/breadhub-org/docker-nginx-php-fpm/blob/main/LICENSE)

## Source origin
Source: https://github.com/olkitu/docker-nginx-php-fpm
