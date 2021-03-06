FROM php:7.1-fpm

MAINTAINER sl <ott321@yeah.net>

ENV PHPREDIS_VERSION=3.1.6
ENV PHALCON_VERSION=3.2.4

RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo 'Asia/Shanghai' > /etc/timezone

RUN apt-get update \
    && apt-get install -y \
        curl \
        wget \
        git \
        vim \
        zip \
        libz-dev \
        libssl-dev \
    && apt-get clean

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update --clean-backups

RUN wget https://codeload.github.com/phalcon/cphalcon/tar.gz/v${PHALCON_VERSION} -O /tmp/phalcon.tar.gz \
    && mkdir -p /tmp/phalcon \
    && tar -xf /tmp/phalcon.tar.gz -C /tmp/phalcon --strip-components=1 \
    && rm /tmp/phalcon.tar.gz \
    && cd /tmp/phalcon/build \
    && ./install \
    && rm -r /tmp/phalcon \
    && docker-php-ext-enable phalcon

RUN pecl install mongodb \
    && docker-php-ext-install pdo pdo_mysql \
    && pecl install redis-${PHPREDIS_VERSION} \
    && docker-php-ext-enable mongodb redis pdo_mysql

CMD ["php-fpm"]
