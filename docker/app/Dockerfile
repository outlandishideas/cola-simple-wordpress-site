FROM php:7.2-fpm-alpine as development

RUN apk update
    
# See https://getcomposer.org/doc/faqs/how-to-install-composer-programmatically.md    
RUN wget https://raw.githubusercontent.com/composer/getcomposer.org/1b137f8bf6db3e79a38a5bc45324414a6b1f9df2/web/installer -O - -q | php -- --quiet
RUN mv /var/www/html/composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer

ENV PATH="/var/www/html/vendor/bin:${PATH}"

ENV PHP_GD_DEPS "freetype-dev libjpeg-turbo-dev libpng-dev"

# Set up PHP with modules and ini settings for running WordPress
RUN apk update && \
    apk add --no-cache $PHP_GD_DEPS && \
    docker-php-ext-install gd mysqli pdo && \
    echo "date.timezone=Europe/London" > /usr/local/etc/php/conf.d/zz-custom.ini && \
    echo "session.autostart=0" >> /usr/local/etc/php/conf.d/zz-custom.ini

COPY docker/app/docker-wordpress-entrypoint /usr/local/bin/

ENTRYPOINT ["docker-wordpress-entrypoint"]
CMD ["php-fpm"]

#---------------------------------------------------------------------------

FROM development as production

COPY . /var/www/html

RUN composer install