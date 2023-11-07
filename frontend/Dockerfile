# Use an official Node.js image
FROM node

# Atualize o sistema e instale as dependências necessárias
RUN apt-get update -qq && \
    apt-get install -y apt-utils build-essential && \
    rm -rf /var/lib/apt/lists/*

# Instale o Vue.js e o Vue CLI globalmente
RUN npm install -g vue@latest @vue/cli@latest

# Defina o diretório de trabalho para o aplicativo Vue.js
WORKDIR /usr/src/client
