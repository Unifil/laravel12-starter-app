# .devcontainer/Dockerfile
FROM php:8.4-cli-bullseye
# Imagem oficial PHP 8.4 CLI sobre Debian Bullseye :contentReference[oaicite:6]{index=6}

# Cria o grupo e o usuário vscode com UID/GID 1000 e habilita sudo sem senha
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
  && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
  && apt-get update \
  && apt-get install -y --no-install-recommends sudo curl git unzip nodejs npm \
  && echo "$USERNAME ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/$USERNAME \
  && chmod 0440 /etc/sudoers.d/$USERNAME \
  && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
  && composer global require laravel/installer \
  && apt-get clean && rm -rf /var/lib/apt/lists/*
# Inclusão de usuário não-root conforme guia oficial :contentReference[oaicite:7]{index=7}  
USER $USERNAME
ENV PATH="/home/$USERNAME/.composer/vendor/bin:${PATH}"
