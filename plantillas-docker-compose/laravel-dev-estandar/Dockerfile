FROM php:8.0-apache

# Instalación de extensiones php
RUN docker-php-ext-install pdo_mysql

# Para usar URLs amigables
RUN a2enmod rewrite

# Instalamos composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

# Instalamos xdebug
RUN yes | pecl install xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini \

# Para que la web funcione con el protocolo https
RUN a2enmod ssl
RUN openssl req -new -newkey rsa:4096 -days 3650 -nodes -x509 -subj \
    "/C=../ST=...../L=..../O=..../CN=..." \
    -keyout /etc/ssl/certs/ssl.key -out /etc/ssl/certs/ssl.crt

# Para que "docker exec" se abra en la raiz del repositorio y poder ejecutar "php artisan" sin cambiar de directorio
WORKDIR /var/www
