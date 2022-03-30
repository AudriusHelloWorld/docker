FROM php:8.1.4-fpm-alpine

WORKDIR /var/www

#install
RUN apk update && apk add \
    build-base \
    vim \
    nano \
    git \
    curl \
    bash
RUN docker-php-ext-install pdo_mysql

# set timezone
RUN apk add tzdata
RUN cp /usr/share/zoneinfo/Europe/Vilnius /etc/localtime
RUN echo "Europe/Vilnius" > /etc/timezone

# install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

# install symfony
RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony

RUN addgroup -g 1000 -S www && \
    adduser -u 1000 -S www -G www

USER www

COPY --chown=www:www . /var/www

EXPOSE 9000