FROM php:7.3.18-apache-stretch

RUN apt-get update -yqq && \
    
    apt-get install -y apt-utils zip unzip && \
    apt-get install -y nano && \
    apt-get install -y libzip-dev libpq-dev && \
    a2enmod rewrite && \
    docker-php-ext-install pdo_pgsql && \
    docker-php-ext-install pgsql && \
    docker-php-ext-configure zip --with-libzip && \
    docker-php-ext-install zip && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/app

#RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer
#COPY composer.lock /var/www/app
#COPY composer.json /var/www/app
#CMD bash -c "composer install"
#RUN composer install  \
#    --ignore-platform-reqs \
#    --no-ansi \
#    --no-autoloader \
#    --no-interaction \
#    --no-scripts

COPY default.conf /etc/apache2/sites-enabled/000-default.conf 
COPY src/ /var/www/app
#COPY .env.example  /var/www/app/.env
#RUN composer dump-autoload --optimize --classmap-authoritative
#RUN chown -R www-data: /var/www/app
#RUN chmod -R 755 /var/www/app/storage
#RUN chmod 600 /var/www/app/.env
#RUN php artisan key:generate
RUN apt-get update && apt-get install -y iputils-ping && apt-get install -y telnet
RUN docker-php-ext-install \
    mysqli \ 
    pdo \
    pdo_mysql 
CMD bash
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

EXPOSE 80
