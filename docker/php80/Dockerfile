# FROM php:8.0.21RC1-fpm-alpine3.16
ARG PHP80_VERSION
FROM php:$PHP80_VERSION


# Docker php extension 安裝的輔助腳本
# https://github.com/mlocati/docker-php-extension-installer
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN apk add vim
RUN apk add htop
RUN apk add --no-cache zip libzip-dev
RUN docker-php-ext-configure zip
RUN docker-php-ext-install zip

RUN chmod +x /usr/local/bin/install-php-extensions
RUN install-php-extensions gd 
RUN install-php-extensions xdebug
RUN install-php-extensions @composer-2.0.9 
RUN install-php-extensions @fix_letsencrypt
RUN install-php-extensions zip
RUN install-php-extensions mysqli
RUN install-php-extensions pdo_mysql
RUN install-php-extensions redis
RUN install-php-extensions intl
RUN install-php-extensions imagick
# RUN install-php-extensions mongodb
# RUN install-php-extensions pgsql
# RUN install-php-extensions pdo_pgsql

RUN apk add --update nodejs npm
RUN apk add --update npm
RUN apk add --no-cache supervisor

# USER root

# RUN adduser -D jason -u 1000

# RUN chown -R jason:jason /var/www/html

# USER jason

RUN apk --no-cache add shadow && usermod -u 1000 www-data && groupmod -g 1000 www-data

COPY php.ini /usr/local/etc/php/conf.d/

COPY supervisord.conf /etc/supervisor/supervisord.conf

CMD ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisor/supervisord.conf"]
