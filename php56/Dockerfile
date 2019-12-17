# alpine
FROM  hub.c.163.com/library/php:5-fpm-alpine
# alpine mirror

RUN echo "http://mirrors.ustc.edu.cn/alpine/latest-stable/main" > /etc/apk/repositories \
    && echo "http://mirrors.ustc.edu.cn/alpine/edge/testing/" >> /etc/apk/repositories \
    && echo "http://mirrors.ustc.edu.cn/alpine/edge/community/" >> /etc/apk/repositories \
    && echo "nameserver 8.8.8.8" >> /etc/resolv.conf \
    && apk add --update freetype-dev \
        libjpeg-turbo-dev \
        libltdl \
        libmcrypt-dev \
        libpng-dev \
        shadow \
    && groupadd -g 1000 vboxsf \
    && usermod -a -G vboxsf www-data \
    && docker-php-ext-install iconv mcrypt bcmath mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install mysqli pdo_mysql

# RUN apk add \
#        pcre-dev \
#        build-base \
#        autoconf \
#        libtool

#RUN pecl install swoole \
#    && docker-php-ext-enable swoole

#Install redis extension
RUN curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/2.2.8.tar.gz \
    && tar zxvf /tmp/redis.tar.gz \
    && rm -r /tmp/redis.tar.gz \
    && mkdir -p /usr/src/php/ext \
    && mv phpredis-2.2.8 /usr/src/php/ext/redis \
    && cd /usr/src/php/ext/redis \
    && docker-php-ext-install redis


CMD ["php-fpm"]