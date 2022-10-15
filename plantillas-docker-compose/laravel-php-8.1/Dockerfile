FROM php:8.1-apache

# Distribución
# Debian GNU/Linux 11 (bullseye)

# Instalación de extensiones php necesarias para ejecutar laravel
RUN docker-php-ext-install pdo_mysql

# Para usar URLs amigables
RUN a2enmod rewrite

# Instalamos composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

# Instalamos xdebug
RUN yes | pecl install xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.mode=develop,debug" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini

# Instalamos zip, necesario para algunas dependencias de composer
RUN apt-get update
RUN apt-get install -y libzip-dev
RUN docker-php-ext-install zip

# Creamos un usuario con el gui del usuario del sitema y permisos de root para que los archivos que se generen
# dentro del contenedor se puedan eliminar desde  windows
RUN useradd -rm -d /home/docker -s /bin/bash -g root -G sudo -u 1000 docker
# Ponemos el nuevo usuario por defecto para hacer login cuando nos conectamos al contendor con "docker exec"
USER docker

# Para que "docker exec" se abra en la raiz del repositorio y poder ejecutar "php artisan" sin cambiar de directorio
WORKDIR /var/www
