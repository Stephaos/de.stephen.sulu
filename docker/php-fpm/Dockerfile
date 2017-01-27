FROM php:7.0-fpm

ENV APP_BASEDIR=/var/www/app

COPY ./docker/php-fpm/php.ini /usr/local/etc/php/conf.d/

# Install selected extensions and other stuff
RUN apt-get update && apt-get install -y \
        git \
        unzip \
        zip \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install pdo_mysql \
    && pecl install xdebug \
    && apt-get clean \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

# copy only composer.json and composer.lock
COPY ./composer.* $APP_BASEDIR/

WORKDIR $APP_BASEDIR/

# without scripts, so it doesn't try to create parameters.yml or autoloader etc.
RUN composer install --no-interaction --no-scripts --no-autoloader

# now copy our actual source code (taking into account .dockerignore)
COPY ./ $APP_BASEDIR/

# again, but this time we have the source code and can generate parameters.yml etc.
RUN rm -rf var/cache/*
RUN composer install --no-interaction