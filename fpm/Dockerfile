FROM php:8.1-fpm-bullseye

# Install dependencies
RUN apt-get update && apt-get install -yqq \
    libzip-dev \
    zip \
    unzip \
    wget \
    gnupg \
    git \
    libsodium-dev \
    libsodium23 \
    libcurl4-openssl-dev \
    libxslt1-dev \
    libxslt1.1 \
    libicu67 \
    libicu-dev \
    libpq-dev

RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pdo_pgsql
RUN docker-php-ext-install sodium
RUN docker-php-ext-install xsl
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl
RUN docker-php-ext-install zip
RUN docker-php-ext-install pcntl
RUN docker-php-ext-install pdo_pgsql
RUN docker-php-ext-install exif
RUN docker-php-ext-install soap
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install curl

RUN pecl install xdebug

RUN pecl install -o -f redis \
    && rm -rf /tmp/pear

COPY php.ini /usr/local/etc/php/php.ini

RUN find /usr/local/lib/php -name "xdebug.so" -exec echo 'zend_extension="{}"' >> /usr/local/etc/php/php.ini \;

COPY xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

#ARG OPCACHE_ENABLE
#RUN sed -i "s/;opcache.enable=1/opcache.enable=1/" /usr/local/etc/php/php.ini
#opcache.preload=/path/to/project/var/cache/prod/srcApp_KernelProdContainer.preload.ph

USER 1000:1000

CMD ["php-fpm"]
