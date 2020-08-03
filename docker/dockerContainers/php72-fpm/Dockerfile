FROM php:7.3.14-fpm

RUN apt-get update > /dev/null && apt-get install -y \
    git \
    unzip \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libxml2-dev \
    libpng-dev \
    zlib1g-dev \
    libicu-dev \
    jpegoptim \
    libzip-dev \
    libpq-dev \
    g++ \
    libxrender1 \
    libfontconfig \
    gnupg2 \
    nano > /dev/null \
    && docker-php-ext-install intl > /dev/null \
    && docker-php-ext-install soap > /dev/null \
    && docker-php-ext-install bcmath > /dev/null \
    && docker-php-ext-configure zip --with-libzip > /dev/null \
    && docker-php-ext-install zip > /dev/null

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer > /dev/null

# Install MySQL and PostgreSQL PDO
RUN docker-php-ext-install pdo pdo_mysql pdo_pgsql > /dev/null

# Install xDebug
ARG INSTALL_XDEBUG=false
RUN if [ ${INSTALL_XDEBUG} = true ]; then \
    # Install XDebug extention PDO
    pecl install xdebug > /dev/null && \
    docker-php-ext-enable xdebug > /dev/null \
;fi

# Install wkhtmltopdf
RUN curl -L#o wk.tar.xz https://downloads.wkhtmltopdf.org/0.12/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz \
    && tar xf wk.tar.xz \
    && cp wkhtmltox/bin/wkhtmltopdf /usr/bin \
    && cp wkhtmltox/bin/wkhtmltoimage /usr/bin \
    && rm wk.tar.xz \
    && rm -r wkhtmltox

# ADD Alias to bin/console
RUN echo 'alias sf="php bin/console"' >> ~/.bashrc

RUN docker-php-ext-install gettext

# Install gd
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

EXPOSE 9000
CMD ["php-fpm", "-F"]

WORKDIR /backend
