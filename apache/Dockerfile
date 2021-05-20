ARG DEBIAN_FRONTEND=noninteractive
ARG PHP_VERSION
ARG APACHE_DOCUMENT_ROOT
ARG DOMAIN_HOST_MAIN
ARG DOMAIN_HOST_ALIAS

FROM php:$PHP_VERSION

# Install MCrypt
RUN apt-get update \
    && apt-get install -yq libmcrypt-dev \
    && docker-php-ext-install mcrypt

# Install Mysql
RUN docker-php-ext-install mysqli pdo pdo_mysql

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Install Git
RUN apt-get update \
    && apt-get install -y git

# Install soap
RUN apt-get update \
    && apt-get install -yq libxml2-dev \
    && docker-php-ext-install soap

# Install opcache
RUN docker-php-ext-install opcache

# Install gmp
RUN apt install -y libgmp-dev
RUN docker-php-ext-install gmp

# Install xsl
RUN apt-get update \
    && apt-get install -yq libxslt-dev \
    && docker-php-ext-install xsl

# Enable Apache mod_rewrite
RUN a2enmod rewrite

# Install MySQL CLI Client
RUN apt-get update \
    && apt-get install -y mysql-client

ENV PHP_TIMEZONE America/Argentina/Buenos_Aires

ARG APACHE_DOCUMENT_ROOT
ENV APACHE_DOCUMENT_ROOT=${APACHE_DOCUMENT_ROOT}

ARG DOMAIN_HOST_MAIN
ENV DOMAIN_HOST_MAIN=${DOMAIN_HOST_MAIN}

ARG DOMAIN_HOST_ALIAS
ENV DOMAIN_HOST_ALIAS=${DOMAIN_HOST_ALIAS}

COPY ./apache/conf/000-default.conf /etc/apache2/sites-available/000-default.conf

RUN sed -ri -e 's!APACHE_DOC_ROOT!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/000-default.conf
RUN sed -ri -e 's!DOMAIN_HOST_MAIN!${DOMAIN_HOST_MAIN}!g' /etc/apache2/sites-available/000-default.conf
RUN sed -ri -e 's!DOMAIN_HOST_ALIAS!${DOMAIN_HOST_ALIAS}!g' /etc/apache2/sites-available/000-default.conf
