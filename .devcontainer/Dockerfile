# Base: PHP 8.4 CLI (Debian Bullseye)
FROM php:8.4-cli-bullseye

# Argumentos para criar usuário vscode (UID/GID 1000)
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# 1) Cria grupo e usuário vscode
# 2) Instala utilitários, Node.js 20.x via NodeSource, Composer e Laravel Installer
# 3) Habilita e instala a extensão PCNTL
RUN groupadd --gid $USER_GID $USERNAME \
 && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
 && apt-get update \
 && apt-get install -y --no-install-recommends sudo curl git unzip \
 && curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
 && apt-get install -y nodejs \
 && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
 && composer global require laravel/installer \
 \
 # Habilita PCNTL para o Pail  
 && docker-php-ext-configure pcntl --enable-pcntl \
 && docker-php-ext-install pcntl \
 \
 && apt-get clean && rm -rf /var/lib/apt/lists/*

# Passa a executar como vscode
USER $USERNAME
ENV PATH="/home/$USERNAME/.composer/vendor/bin:${PATH}"
