
FROM php:8.5-cli-bookworm

RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    unzip \
    libicu-dev \
    libpq-dev \
    libzip-dev \
    && rm -rf /var/lib/apt/lists/*

# Compiler les extensions séparément pour identifier toute erreur
RUN docker-php-ext-install -j1 intl

RUN docker-php-ext-install -j1 pdo_pgsql

RUN docker-php-ext-install -j1 zip

# Installer Composer
COPY --from=composer:2 /usr/bin/composer /usr/local/bin/composer

WORKDIR /var/www/html

RUN composer --version
