FROM php:apache

MAINTAINER Robert Schneider <shakemedev@gmail.com>

# remove SUID flag
RUN for i in `find / -perm +6000 -type f`; do chmod a-s $i; done

# install dependencies
RUN apt-get update \
    && apt-get install --assume-yes \
        libmemcache-dev \
        libpq-dev \
        zlib1g-dev

# install and enable extensions
RUN docker-php-ext-install \
        mysqli \
        pdo \
        pdo_mysql \
        pdo_pgsql \
    && docker-php-ext-enable \
        mysqli \
        pdo \
        pdo_mysql \
        pdo_pgsql

RUN pecl install \
        memcached \
        redis \
    && docker-php-ext-enable \
        memcached \
        redis

# cleanup
RUN apt-get --assume-yes autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /tmp/*

