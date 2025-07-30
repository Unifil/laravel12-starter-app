# Use PHP 8.4 CLI com Debian Bullseye
FROM php:8.4-cli-bullseye

# Instalar dependências essenciais, Composer e Laravel installer
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
  && apt-get install -y curl git unzip nodejs npm \
  && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
  && composer global require laravel/installer \
  && apt-get clean && rm -rf /var/lib/apt/lists/*

ENV PATH="$PATH:/root/.composer/vendor/bin"
