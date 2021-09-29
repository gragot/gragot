FROM php:7.4-apache

# Instalación de extensiones
RUN docker-php-ext-install pdo_mysql

# Para usar URLs amigables
RUN a2enmod rewrite

# Para que "docker exec" se abra en la raiz del repositorio y poder ejecutar "php artisan" sin cambiar de directorio
WORKDIR /var/www