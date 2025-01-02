FROM debian:11

ARG PHP_VERSION
ENV PHP_VERSION=$PHP_VERSION

LABEL MAINTAINER="Dalibor Menkovic <dalibor.menkovic@gmail.com>"

RUN apt-get update && \
    apt-get install -y \
    locales \
    apt-transport-https \
    lsb-release \
    ca-certificates \
    gpg \
    curl \
    wget \
    apache2 \
    zip \
    unzip \
    locales \
    cron

RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" >> /etc/apt/sources.list.d/php.list

RUN apt-get update && apt-get install -y \
    php$PHP_VERSION \
    php$PHP_VERSION-cli \
    php$PHP_VERSION-mysql \
    php$PHP_VERSION-dev \
    php$PHP_VERSION-gd \
    php$PHP_VERSION-memcached \
    php$PHP_VERSION-xml \
    php$PHP_VERSION-zip \
    php$PHP_VERSION-curl \
    php$PHP_VERSION-imagick \
    php$PHP_VERSION-mbstring \
    php$PHP_VERSION-mongodb \
    php-common \
    php-pear \
    php-intl \
    php-log

#     php$PHP_VERSION-json \


RUN php -r " file_put_contents('cs.php', file_get_contents('https://getcomposer.org/installer')); if (hash_file('SHA384', 'cs.php') !== trim(file_get_contents('https://composer.github.io/installer.sig'))) { echo 'Corupted'.PHP_EOL; unlink('cs.php'); } " && \
    php cs.php --install-dir=/usr/local/bin --filename=composer  && \
    rm cs.php

RUN apt-get install -y libapache2-mod-php$PHP_VERSION 
RUN a2enmod rewrite && \
    a2enmod headers

EXPOSE 80

CMD ["/usr/sbin/apache2ctl", "-DFOREGROUND"]
