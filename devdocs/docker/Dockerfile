FROM php:5.6-apache

RUN a2enmod rewrite

# install modules of apache that will be required for Drupal 7
RUN apt-get update && apt-get install -y libpng-dev libjpeg-dev && \
	rm -rf /var/lib/apt/lists/* && docker-php-ext-configure gd \
	--with-png-dir=/usr --with-jpeg-dir=/usr && docker-php-ext-install gd
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install zip
RUN docker-php-ext-install bcmath

## ImageMagick - Mosaico 2.0.beta2 requirement

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libmagickwand-dev \
    && rm -rf /var/lib/apt/lists/*

RUN pecl install imagick-3.4.1 \
    && docker-php-ext-enable imagick
