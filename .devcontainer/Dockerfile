# .devcontainer/Dockerfile
FROM php:8.4-cli-bullseye
# Usa a imagem oficial PHP 8.4 CLI sobre Debian Bullseye 

# Cria usuário vscode (UID/GID 1000) e habilita sudo
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
  && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
  # Instala dependências básicas
  && apt-get update \
  && apt-get install -y --no-install-recommends sudo curl git unzip \
  # Configura NodeSource para Node.js 20.x
  && curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
  && apt-get install -y nodejs \
  # Instala Composer e Laravel Installer
  && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
  && composer global require laravel/installer \
  # Limpeza de cache
  && apt-get clean && rm -rf /var/lib/apt/lists/*  
# Node.js 20.x e npm instalados via NodeSource :contentReference[oaicite:3]{index=3}

USER $USERNAME
ENV PATH="/home/$USERNAME/.composer/vendor/bin:${PATH}"
# Define usuário não-root conforme padrão DevContainers :contentReference[oaicite:4]{index=4}
