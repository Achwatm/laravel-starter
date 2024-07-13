FROM php:8.2-fpm-alpine
LABEL MAINTEINER="Mariusz Achwat"

ENV APCU_PECL 5.1.18
ENV MEMCACHED_PECL 3.1.5
ENV REDIS_PECL 5.3.1
ENV MONGO_PECL 1.11.0


RUN apk --no-cache add ca-certificates

RUN apk add -U --no-cache autoconf \
  bash \
  c-client \
  cyrus-sasl-dev \
  freetype \
  freetype-dev \
  g++ \
  git \
  gettext-dev \
  icu-dev \
  icu-libs \
  jq \
  libjpeg-turbo \
  libjpeg-turbo-dev \
  libmemcached-dev \
  libpng \
  libpng-dev \
  libressl \
  libressl-dev \
  librsvg \
  libwebp-dev \
  libxml2-dev \
  libxpm-dev \
  libzip-dev \
  make \
  mysql-client \
  openldap-dev \
  pcre-dev \
  re2c \
  zlib-dev \
  tzdata \
  && pecl install memcached-${MEMCACHED_PECL} APCu-${APCU_PECL} mongodb \
  && printf "no\n" | pecl install redis \
  && docker-php-ext-enable apcu memcached redis \
  && pecl clear-cache \
  && docker-php-ext-configure exif \
  && docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg \
  && docker-php-ext-install -j 4 exif gd opcache pdo pdo_mysql soap zip calendar \
  && docker-php-ext-enable mongodb \
  && curl --silent --show-error https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer \
  && chmod +x /usr/local/bin/composer \
  && apk del --purge autoconf \
    cyrus-sasl-dev \
    freetype-dev \
    g++ \
    icu-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libwebp-dev \
    libxml2-dev \
    make \
    pcre-dev \
    zlib-dev

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

CMD ["php-fpm"]
