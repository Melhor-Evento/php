FROM php:7.3

WORKDIR /var/www

RUN rm -rf /var/www/html \
  && apt-get update -y \
  && apt-get install -y \
  autoconf \
  build-essential \
  curl \
  git \
  libicu-dev \
  libmpdec-dev \
  libpq-dev \
  libjpeg-dev \
  libpng-dev \
  libzip-dev \
  supervisor \
  unzip \
  vim \
  wget \
  zip \
  && apt autoremove \
  && apt clean \
  && pecl install decimal \
  && pecl install grpc \
  && pecl install protobuf \
  && pecl install redis \
  && docker-php-ext-configure gd --with-png-dir=/usr/include --with-jpeg-dir=/usr/include \
  && docker-php-ext-install \
  bcmath \
  exif \
  gd \
  intl \
  opcache \
  pcntl \
  pdo_mysql \
  pdo_pgsql \
  pgsql \
  sysvmsg \
  sysvsem \
  sysvshm \
  zip \
  && curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer \
  && composer self-update --clean-backups \
  && composer global require hirak/prestissimo \
  && git clone https://github.com/census-instrumentation/opencensus-php \
  && cd opencensus-php/ext \
  && phpize \
  && ./configure --enable-opencensus \
  && make -j "$(nproc)" \
  && make install \
  && cd ../../ \
  && rm -rf ./opencensus-php \
  && docker-php-ext-enable opencensus
