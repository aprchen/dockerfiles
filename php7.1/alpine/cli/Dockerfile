FROM php:7.1-cli-alpine3.4

ENV SWOOLE_VERSION=2.1.0
ENV HIREDIS_VERSION=0.13.3
ENV TIME_ZONE = Asia/Shanghai

MAINTAINER sl <ott321@yeah.net>

RUN set -xe \
    && apk --update add --no-cache --virtual build-dependencies \
    autoconf \
    g++ \
    file \
    re2c \
    make \
    && apk add --no-cache tzdata  \
    openssl-dev \
    linux-headers \
    && echo "${TIME_ZONE}" > /etc/timezone \
    && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime \
    && wget https://github.com/redis/hiredis/archive/v${HIREDIS_VERSION}.tar.gz -O hiredis.tar.gz \
    && mkdir -p hiredis \
    && tar -xf hiredis.tar.gz -C hiredis --strip-components=1 \
    &&  cd hiredis \
    && make -j \
    && make install \
    && cd .. \
    && wget https://github.com/swoole/swoole-src/archive/v${SWOOLE_VERSION}.tar.gz -O swoole.tar.gz \
    && mkdir -p swoole \
    && tar -xf swoole.tar.gz -C swoole --strip-components=1 \
    && cd swoole \
    && phpize \
    && ./configure --enable-async-redis --enable-mysqlnd --enable-coroutine --enable-openssl \
    && make -j \
    && make install \
    && docker-php-ext-enable swoole\
    && cd .. \
    && apk del build-dependencies \
    && rm -rf /hiredis.tar.gz \
        /hiredis \
        /swoole.tar.gz \
        /swoole \
        /var/cache/apk/* \
        /tmp/* \
        /var/tmp/* \
    && unset HIREDIS_VERSION SWOOLE_VERSION TIME_ZONE

WORKDIR /var/www/html

CMD ["php", "-a"]
