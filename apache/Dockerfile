ARG DEBIAN_FRONTEND=noninteractive
ARG PHP_VERSION

FROM php:$PHP_VERSION

# APT update
RUN apt-get update

# Install Mysql
RUN docker-php-ext-install mysqli pdo pdo_mysql

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Install Git
RUN apt-get install -y git

# Install soap / xml
RUN apt-get install -yq libxml2-dev \
    && docker-php-ext-install soap \
    && docker-php-ext-install xml

# Install opcache
RUN docker-php-ext-install opcache

# Install gmp
RUN apt install -y libgmp-dev
RUN docker-php-ext-install gmp

# Install xsl
RUN apt-get install -yq libxslt-dev \
    && docker-php-ext-install xsl

# Install gd
RUN apt-get install -y \
    libpng-dev \
    libwebp-dev \
    libjpeg62-turbo-dev \
    libxpm-dev \
    libfreetype6-dev

RUN docker-php-ext-install gd

# Install zip
RUN apt-get install -y \
    libzip-dev \
    zip \
  && docker-php-ext-install zip

# Enable Apache mod_rewrite
RUN a2enmod rewrite

ENV PHP_TIMEZONE America/Argentina/Buenos_Aires

COPY ./apache-dev/conf/*.conf /etc/apache2/sites-available/
RUN a2dissite 000-default

RUN a2ensite dev

RUN service apache2 restart
