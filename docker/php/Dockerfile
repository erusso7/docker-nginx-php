FROM php:7-fpm-alpine

RUN apk upgrade --update && apk add \
            freetype-dev \
            libjpeg-turbo-dev \
            libpng-dev \
        && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
        && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
        && docker-php-ext-install -j${NPROC} gd \
        && docker-php-ext-install mysqli exif

ADD app/ /var/www

RUN chown -R www-data:www-data /var/www

USER 'www-data'

WORKDIR /var/www