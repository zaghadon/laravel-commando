FROM php:7.2-cli-stretch

#
# Packages
#

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    mysql-client \
    git zip unzip

RUN apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

#
# PHP
#

RUN docker-php-ext-install pdo_mysql

# Enable debuging
RUN mv /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

#
# Composer
#

ENV COMPOSER_ALLOW_SUPERUSER=1
ENV COMPOSER_NO_INTERACTION=1
ENV COMPOSER_MEMORY_LIMIT=-1

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer global require hirak/prestissimo --no-plugins --no-scripts

# Set default workdir
WORKDIR /var/www/html

# Keep spinning
CMD ["tail", "-f", "/dev/null"]