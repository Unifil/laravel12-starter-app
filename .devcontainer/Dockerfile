# .devcontainer/Dockerfile
FROM mcr.microsoft.com/devcontainers/php:1‑8.4-bullseye

# Instalar dependências para Laravel e Node.js
RUN apt-get update \
  && export DEBIAN_FRONTEND=noninteractive \
  && apt-get install -y --no-install-recommends curl git unzip nodejs npm \
  && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
  && composer global require laravel/installer

ENV PATH="$PATH:/root/.composer/vendor/bin"
