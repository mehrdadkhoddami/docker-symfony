FROM alpine:edge
ARG PROJECT_NAME
ARG ENV=prod

LABEL maintainer="Mehrdad Khoddami <khoddami.me@gmail.com>"

RUN apk add --update --no-cache \
    coreutils \
    php7-fpm \
    php7-apcu \
    php7-ctype \
    php7-curl \
    php7-dom \
    php7-gd \
    php7-iconv \
    php7-imagick \
    php7-json \
    php7-intl \
    php7-mcrypt \
    php7-fileinfo\
    php7-mbstring \
    php7-opcache \
    php7-openssl \
    php7-pdo \
    php7-pdo_mysql \
    php7-mysqli \
    php7-xml \
    php7-zlib \
    php7-phar \
    php7-tokenizer \
    php7-session \
    php7-simplexml \
    php7-xdebug \
    php7-zip \
    php7-xmlwriter \
    php7-bcmath \
    php7-gmp \
    make \
    unzip \
    zip \
    git \
    jpegoptim \
	optipng \
	pngquant \
	gifsicle \
    curl

RUN echo "$(curl -sS https://composer.github.io/installer.sig) -" > composer-setup.php.sig \
        && curl -sS https://getcomposer.org/installer | tee composer-setup.php | sha384sum -c composer-setup.php.sig \
        && php composer-setup.php --install-dir=/usr/local/bin --filename=composer && rm composer-setup.php*

COPY docker/php-fpm/php_docker.ini /etc/php7/conf.d/
COPY docker/php-fpm/php_docker.ini /etc/php7/cli/conf.d/
COPY docker/php-fpm/symfony.pool.conf /etc/php7/php-fpm.d/
		
COPY etc/aliases.sh /etc/profile.d/aliases.sh

RUN mkdir -p /var/lib/php/session
RUN mkdir /var/php_tmp


CMD ["php-fpm7", "-F"]

WORKDIR /var/www/${PROJECT_NAME}

EXPOSE 9001