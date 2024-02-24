# Créer un Dockerfile pour cette application en mode production
# utilisation de php-fpm
FROM php:8.3-fpm

# installer l'extension intl
RUN apt-get update && apt-get install -y \
        libicu-dev \
        libzip-dev \
        zip \
        git\
    && docker-php-ext-install intl zip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*


# installer le composer dans le container
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# définir le répertoire de travail
WORKDIR /var/www/html
# copier les fichiers sources dans le répertoire de travail
COPY . .



ENV COMPOSER_ALLOW_SUPERUSER=1
# installer les dépendances
RUN composer install --no-dev --optimize-autoloader

RUN composer require symfony/asset-mapper symfony/asset symfony/twig-pack
# compiler le JS et le CSS (voire README)
RUN php bin/console asset-map:compile

# nettoyer le cache (voire le README)

COPY --chown=www-data:www-data . .

USER www-data
CMD ["php-fpm"]