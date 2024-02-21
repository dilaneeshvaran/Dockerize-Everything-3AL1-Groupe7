# Créer un Dockerfile pour cette application en mode production
# utilisation de php-fpm
FROM php:8.3-fpm

# définir le répertoire de travail
WORKDIR /var/www/html

# installer l'extension intl
RUN docker-php-ext-install intl

# installer le composer dans le container
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# copier les fichiers sources dans le répertoire de travail 
COPY . .

# installer les dépendances
RUN composer install --no-dev --optimize-autoloader

# compiler le JS et le CSS (voire README)
RUN php bin/console asset-map:compil

# nettoyer le cache (voire le README)
RUN php bin/console cache:clear --env=prod