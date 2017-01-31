FROM php:fpm

RUN usermod -u 1000 www-data

ADD php.ini /usr/local/etc/php/conf.d
# ADD www.conf /usr/local/etc/php-fpm.d/

RUN apt-get update

RUN apt-get install -y libpq-dev \
	&& docker-php-ext-install pdo pdo_pgsql pdo_mysql

RUN apt-get install -y \
        libmcrypt-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt

WORKDIR /var/www/

CMD ["php-fpm"]

EXPOSE 9000
