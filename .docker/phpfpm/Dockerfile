FROM php:7.4-fpm

# Install git and zip
RUN set -ex; \
        apt-get update \
        && apt-get install -y git zip

# Add php extension installer - simplify way of extention installation
ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions /usr/local/bin/

RUN chmod uga+x /usr/local/bin/install-php-extensions && sync && \
    install-php-extensions \
        pdo_mysql \
        xdebug

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Install symfony cli
RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony

RUN apt-get clean && apt-get autoclean && rm -rf /var/lib/apt/lists/*

WORKDIR /code
