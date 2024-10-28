FROM php:7.4-apache

RUN apt-get update && apt-get install -y \
    libzip-dev \
    libcurl4-openssl-dev \
    libxml2-dev \
    libxml2 \
    libpng-dev \
    libxslt-dev \
    git \
    libwebp-dev \
    freetype* \
    libjpeg-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libxpm-dev \
    libmagickwand-dev \
    libonig-dev \
    libsodium-dev \
    zip \
    unzip \
    rsync \
    vim \
    nano \
    unzip \
    p7zip-full

RUN docker-php-ext-install mysqli \
    pdo \
    pdo_mysql \
    zip \
    bcmath \
    ctype \
    curl \
    dom \
    fileinfo \
    filter \
    iconv \
    intl \
    mbstring \
    simplexml \
    soap \
    sockets \
    sodium \
    xmlwriter \
    xsl

RUN docker-php-ext-configure gd --with-jpeg --with-freetype && docker-php-ext-install gd
RUN docker-php-ext-configure pcntl --enable-pcntl && docker-php-ext-install pcntl
RUN yes '' | pecl install imagick && docker-php-ext-enable imagick
RUN pecl install xdebug-3.1.6 && docker-php-ext-enable xdebug

RUN echo "memory_limit=8000M" > /usr/local/etc/php/conf.d/memory_limit.ini
RUN echo "max_execution_time=300" > /usr/local/etc/php/conf.d/max_execution_time.ini
RUN echo "upload_max_filesize=100M" > /usr/local/etc/php/conf.d/upload_max_filesize.ini
RUN echo "post_max_size=100M" > /usr/local/etc/php/conf.d/post_max_size.ini

RUN echo "xdebug.mode=debug" > /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.client_host=host.docker.internal" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.client_port=9003" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.discover_client_host=1" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.idekey=PHPSTORM" >> /usr/local/etc/php/conf.d/xdebug.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN a2enmod rewrite

CMD ["sh", "-c", "apache2-foreground"]
