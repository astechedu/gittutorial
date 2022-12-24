# Docker Images

<a name="top"></a>
Topic: 
  [PHP Docker Images](#php_images)
  
  
  
  
  
[Go To Top](#top)
<a name="php_images"></a>  

    FROM php:7.2-alpine3.8

    RUN apk update
    RUN apk add bash
    RUN apk add curl

    # INSTALL COMPOSER
    RUN curl -s https://getcomposer.org/installer | php
    RUN alias composer='php composer.phar'

    # INSTALL NGINX
    RUN apk add nginx
    
    
    
    
    FROM php:8.0.2-apache
    RUN apt-get update && apt-get upgrade -y
    RUN apt-get install -y mariadb-client libxml2-dev
    RUN apt-get autoremove -y && apt-get autoclean
    RUN docker-php-ext-install mysqli pdo pdo_mysql xml
    COPY --from=composer /usr/bin/composer /usr/bin/composer






    FROM php:7.3-fpm-alpine
    RUN docker-php-ext-install pdo pdo_mysql
    RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

    RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer
    RUN apk update
    RUN apk upgrade
    RUN apk add bash
    RUN alias composer='php /usr/bin/composer'



