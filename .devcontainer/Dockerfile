# Base: PHP 8.4 CLI (Debian Bullseye)
FROM php:8.4-cli-bullseye

# Arguments para criar usuário não-root 'vscode'
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# 1) Cria grupo e usuário vscode
# 2) Instala sudo, curl, git, unzip
# 3) Configura Node.js 20.x via NodeSource
# 4) Instala Composer e Laravel Installer
RUN groupadd --gid $USER_GID $USERNAME \
  && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
  && apt-get update \
  && apt-get install -y --no-install-recommends sudo curl git unzip \
  && curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
  && apt-get install -y nodejs \
  && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
  && composer global require laravel/installer \
  && apt-get clean && rm -rf /var/lib/apt/lists/*

# Passa a executar como usuário vscode
USER $USERNAME
ENV PATH="/home/$USERNAME/.composer/vendor/bin:${PATH}"
