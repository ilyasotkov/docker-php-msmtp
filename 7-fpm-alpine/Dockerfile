FROM php:7-fpm-alpine

RUN apk add --update --no-cache \
        ca-certificates \
        msmtp

COPY php.ini /usr/local/etc/php/php.ini
