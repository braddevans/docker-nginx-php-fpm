# Docker Nginx & PHP-FPM with Supervisor

![GitHub Workflow Status (branch)](https://img.shields.io/github/actions/workflow/status/breadhub-org/docker-nginx-php-fpm/docker-build.yml?branch=main) ![GitHub](https://img.shields.io/github/license/breadhub-org/docker-nginx-php-fpm)

Based Official PHP image: https://hub.docker.com/_/php with additional packages:

* Nginx
* Supervisor
* [renatomefi/php-fpm-healthcheck](https://github.com/renatomefi/php-fpm-healthcheck)

This repository will automatically update weekly.

## Supported PHP versions

Alpine:

* 8: `8.0`, `8`, `latest`
* 7.4: `7.4`, `7`
* 7.3: `7.3`

Debian Buster:

* 8: `8.0-buster`, `8-buster`, `latest-buster`
* 7.4: `7.4-buster`, `7-buster`
* 7.3: `7.3-buster`

Check from Tags all supported versions and architechtures.

## Usage (docker run)

Run latest version

```
docker run --name nginx-php-fpm -v /some/content:/var/www/html:ro -d ghcr.io/olkitu/breadhub-org/docker-nginx-php-fpm
```

Run specific version, example 7.4

```
docker run --name nginx-php-fpm -v /some/content:/var/www/html:ro -d ghcr.io/breadhub-org/docker-nginx-php-fpm:7.4
```

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
