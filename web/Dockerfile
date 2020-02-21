FROM php:7.2.11-apache

RUN apt-get update && apt-get -y install vim wget tree zsh zip
RUN apt-get -y install lsb-release libicu-dev mysql-client \
   libfreetype6-dev libpng-dev libjpeg62-turbo-dev -qy \
   && apt-get clean \
   && rm -rf /var/lib/apt/lists/ */tmp/* /var/tmp/*

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
   && docker-php-ext-install pdo_mysql mysqli intl gd
RUN ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/rewrite.load
RUN ln -s /etc/apache2/mods-available/vhost_alias.load /etc/apache2/mods-enabled
RUN echo ServerName $HOSTNAME > /etc/apache2/conf-available/fqdn.conf && a2enconf fqdn
RUN a2enmod headers
RUN a2enmod include

COPY ./apache2.conf /etc/apache2/apache2.conf
COPY ./localhost.conf /etc/apache2/sites-available/000-default.conf
COPY ./php.ini /usr/local/etc/php/

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
