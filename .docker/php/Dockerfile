FROM php:fpm

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    curl \
    vim \
    curl \
    debconf \
    git \
    apt-transport-https \
    apt-utils \
    build-essential \
    locales \
    acl \
    mailutils \
    wget \
    zip \
    unzip \
    gnupg \
    gnupg1 \
    gnupg2 \
    nano \
    libzip-dev \
    zlib1g-dev \
    libonig-dev \
    ntp \
    libpq-dev \
    libmpdec-dev \
    && docker-php-ext-install zip pdo_pgsql mbstring bcmath

RUN pecl install decimal && docker-php-ext-enable decimal

COPY php.ini /usr/local/etc/php/php.ini

RUN curl -sSk https://getcomposer.org/installer | php -- && \
   mv composer.phar /usr/local/bin/composer

RUN groupadd docker -g 999
RUN useradd docker -g docker -d /home/docker -m

RUN rm -rf /var/lib/apt/lists/*
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen

USER docker

WORKDIR /PROJECT_NAME/app

EXPOSE 9000
CMD ["php-fpm"]