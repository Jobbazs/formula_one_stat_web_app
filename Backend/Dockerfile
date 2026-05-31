FROM php:8.3-apache

RUN docker-php-ext-install pdo pdo_mysql

WORKDIR /var/www/html
COPY . .

RUN curl -sS https://getcomposer.org/installer | php && \
    php composer.phar install --no-dev

ENV APACHE_DOCUMENT_ROOT /var/www/html/public
RUN sed -i 's|/var/www/html|/var/www/html/public|g' /etc/apache2/sites-available/000-default.conf
RUN a2enmod rewrite

CMD php artisan optimize:clear && php artisan migrate:fresh --seed --force && apache2-foreground