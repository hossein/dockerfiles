FROM php:8.2-apache

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y \
        curl \
        g++ \
        git \
        libbz2-dev \
        libfreetype6-dev \
        libicu-dev \
        libjpeg-dev \
        libmcrypt-dev \
        libpng-dev \
        libreadline-dev \
        libzip-dev \
        unzip \
        zip \
        libpq-dev \
        netcat \
    && rm -rf /var/lib/apt/lists/*

COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

RUN a2enmod rewrite headers \
    && docker-php-ext-install \
        bcmath \
        bz2 \
        calendar \
        iconv \
        intl \
        opcache \
        pdo_mysql \
        zip \
        pcntl \
        exif \
        pdo  \
        pdo_pgsql

RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
    && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1)  \
    && docker-php-ext-install -j${NPROC} gd

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer \
    && chmod +x /usr/bin/composer

EXPOSE 80

# $PHP_INI_DIR is /usr/local/etc/php/
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
COPY php.ini "$PHP_INI_DIR/conf.d/z-00-hosseinaz-overrides.ini"

WORKDIR /var/www/
