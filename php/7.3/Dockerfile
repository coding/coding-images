FROM php:7.3

RUN curl -sS https://getcomposer.org.mirrors.china-speed.org.cn/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer config -g repo.packagist composer https://mirrors.cloud.tencent.com/composer/

RUN find /etc/apt/ -name '*.list' -print0 | xargs -0 sed -i 's/[a-z]\+.debian.org/mirrors.cloud.tencent.com/g'
RUN apt-get update \
    && apt-get install -y \
    cron \
    git \
    icu-devtools \
    jq \
    libfreetype6-dev libicu-dev libjpeg62-turbo-dev libpng-dev librsvg2-bin libsasl2-dev libssl-dev libwebp-dev libxpm-dev libzip-dev \
    unzip \
    vim \
    zlib1g-dev

RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini \
    && yes '' | pecl install redis \
    && pecl install xdebug \
    && docker-php-ext-configure gd  \
    && docker-php-ext-install gd intl pdo_mysql zip \
    && docker-php-ext-enable opcache redis xdebug

RUN apt-get clean \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
