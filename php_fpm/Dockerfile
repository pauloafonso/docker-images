FROM php:8.3-fpm-alpine

ENV TZ=Europe/Berlin

RUN apk update && apk upgrade && \
adduser -Du 1000 -s /bin/bash app_user && \
apk add --update autoconf gcc build-base libxml2-dev git linux-headers
RUN pecl channel-update pecl.php.net
RUN pecl install apcu
RUN pecl install timezonedb
RUN pecl install xdebug
RUN pecl install mongodb

RUN docker-php-ext-enable apcu
RUN docker-php-ext-enable xdebug
RUN docker-php-ext-enable timezonedb
RUN docker-php-ext-enable opcache
RUN docker-php-ext-enable mongodb

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

COPY php.ini /usr/local/etc/php_fpm/php.ini
COPY xdebug.ini /usr/local/etc/php_fpm/conf.d/xdebug.ini
COPY php-fpm.conf /usr/local/etc/php-fpm.conf
COPY www.conf /usr/local/etc/php-fpm.d/www.conf

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

RUN chown -R app_user:app_user /usr/local/var/log/

WORKDIR /var/www/html
