FROM php:7.4-apache

# Tizim kutubxonalarini o'rnatish
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libmagickwand-dev \
    libpq-dev \
    libzip-dev \
    openssl \
    && a2enmod ssl \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_pgsql zip \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# mod_rewrite ni faollashtirish
RUN a2enmod rewrite

# Apache konfiguratsiyasini o'rnatish
COPY ./apache-config.conf /etc/apache2/sites-available/000-default.conf

# Apache va cron xizmatlarini ishga tushirish
CMD ["sh", "-c", "apache2-foreground"]
