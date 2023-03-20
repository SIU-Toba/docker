FROM alpine:3.16

# Set Environments values for PHP
ENV PHP_MEMORY_LIMIT    256M
ENV PHP_MAX_UPLOAD_SIZE 16M
ENV PHP_MAX_FILE_UPLOAD 200
ENV PHP_MAX_POST        32M
ENV PHP_MAX_INPUT_VARS  1500
ENV PHP_DISPLAY_ERRORS Off
ENV PHP_LOGS_ERRORS  On

# Por defecto se utiliza la timezone de Buenos Aires
ENV TZ=America/Argentina/Buenos_Aires

## Falta agregar  php8-memcached que no esta en el repo aun

RUN apk --no-cache add \
    bash \
    tzdata \
    php81 \
    php81-ctype \
    php81-curl \
    php81-dom \
    php81-exif \
    php81-fileinfo \
    php81-gd \
    php81-gmp \
    php81-iconv \
    php81-json \
    php81-mbstring \
    php81-opcache \
    php81-openssl \
    php81-pcntl \
    php81-pdo_pgsql \
    php81-phar \
    php81-session \
    php81-simplexml \
    php81-sodium \
    php81-tokenizer \
    php81-zip \
    php81-xml \
    php81-xmlwriter \
    php81-xsl \
    libsodium \
    apache2 \
    php81-apache2 \
    php81-pecl-memcached \
    curl \
    && rm -rf /var/cache/apk/* \
    && mkdir -p /run/apache2 \
    && echo "ErrorLog /dev/stderr" >> /etc/apache2/httpd.conf \
    && echo "TransferLog /dev/stdout" >> /etc/apache2/httpd.conf \
    && echo "LoadModule rewrite_module modules/mod_rewrite.so" >> /etc/apache2/httpd.conf \
    && echo "ServerTokens Prod" >> /etc/apache2/httpd.conf \
    && echo "ServerSignature Off" >> /etc/apache2/httpd.conf \
    && echo "TraceEnable off" >> /etc/apache2/httpd.conf \
    && cp /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Set environments variables in config file
COPY setup_php_ini.sh /
RUN /setup_php_ini.sh /etc/php81/php.ini

# https://gitlab.alpinelinux.org/alpine/aports/-/issues/12308
RUN ln -s /usr/bin/php81 /usr/bin/php
    
EXPOSE 80
