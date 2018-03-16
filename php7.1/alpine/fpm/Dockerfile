FROM php:7.1-fpm-alpine3.4

ENV PHALCON_VERSION=3.2
ENV TIME_ZONE = Asia/Shanghai

MAINTAINER sl <ott321@yeah.net>

RUN set -xe \
    && apk --update add --no-cache --virtual build-dependencies \
    autoconf \
    g++ \
    file \
    re2c \
    make \
    git \
    && apk add --no-cache openssl-dev \
    tzdata \
    linux-headers \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update --clean-backups \
    && echo "${TIME_ZONE}" > /etc/timezone \
    && ln -sf /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime \
    && wget https://codeload.github.com/phalcon/cphalcon/tar.gz/v${PHALCON_VERSION} -O phalcon.tar.gz \
    && mkdir -p phalcon \
    && tar -xf phalcon.tar.gz -C phalcon --strip-components=1 \
    && cd phalcon/build \
    && ./install \
    && docker-php-ext-enable phalcon \
    && docker-php-ext-install pdo pdo_mysql \
    && cd ../../ \
    && apk del build-dependencies \
    && rm -rf \
        /phalcon.tar.gz \
        /phalcon \
        /var/cache/apk/* \
        /tmp/* \
        /var/tmp/* \
    && unset PHALCON_VERSION TIME_ZONE

WORKDIR /var/www/html

CMD ["php", "-a"]
