#FROM php:5.6-fpm
#FROM php:5.6.23-fpm
#FROM index.tenxcloud.com/docker_library/php:5.4.45-fpm
#FROM  hub.c.163.com/library/php:5-fpm
FROM daocloud.io/library/php:5.4.45-fpm

ADD debian.sources.list /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev libmemcached-dev \
    && docker-php-ext-install iconv mcrypt bcmath mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install mysql mysqli pdo_mysql

#Install redis extension
#RUN curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/2.2.8.tar.gz \
#    && tar zxvf /tmp/redis.tar.gz \
#    && rm -r /tmp/redis.tar.gz \
#    && mkdir -p /usr/src/php/ext \
#    && mv phpredis-2.2.8 /usr/src/php/ext/redis \
#    && cd /usr/src/php/ext/redis \
#    && docker-php-ext-install redis

RUN pecl install redis \
    && docker-php-ext-enable redis \
    && groupadd -g 1000 vboxsf \
    && usermod -a -G vboxsf www-data
#     && pecl install memcache && docker-php-ext-enable memcache

CMD ["php-fpm"]
