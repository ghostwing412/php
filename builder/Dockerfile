FROM php:5.6.40-fpm-alpine3.8
ENV PHPIZE_DEPS \
                autoconf \
                dpkg-dev dpkg \
                file \
                g++ \
                gcc \
                libc-dev \
                make \
                pkgconf \
                re2c
RUN apk add --no-cache --virtual .build-deps2 \
                $PHPIZE_DEPS; \
        \
        pecl install redis-4.2.0 \
        && docker-php-ext-enable redis \
        && apk del --no-network .build-deps2; \
        \
        apk add --no-cache freetype-dev \
                libjpeg-turbo-dev \
                libpng-dev; \
        \
        docker-php-ext-install -j$(nproc) iconv \
        && docker-php-ext-configure gd --with-freetype-dir=/usr/inclue/ --with-jpeg-dir=/usr/include/ \
        && docker-php-ext-install -j$(nproc) gd \
		pdo_mysql \
                mysqli \
                mysql; \
