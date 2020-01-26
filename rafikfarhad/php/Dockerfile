FROM php:7.4-fpm

LABEL AUTHOR="RafikFarhad"

ARG BUILD=PROD
ARG DEBUG_IP=0.0.0.0
ARG DEBUG_PORT=9999
ARG DEBUG_IDE_KEY=ddebug

WORKDIR /var/www
RUN apt-get update && \
    apt-get install -y libzip-dev libonig-dev libpng-dev
RUN apt-get clean && \
    docker-php-ext-install pdo_mysql mbstring zip exif pcntl sockets json bcmath
# RUN docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/
RUN docker-php-ext-install gd
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN if [ "$BUILD" = "DEV" ]; then \
    pecl install xdebug && \
    echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_port=${DEBUG_PORT}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_connect_back=0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.idekey=${DEBUG_IDE_KEY}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini; \
    fi
    
EXPOSE 9000

CMD ["php-fpm"]
