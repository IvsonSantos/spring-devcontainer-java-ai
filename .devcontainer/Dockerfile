FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

# 1. Instalar dependências e o repositório oficial do Adoptium (Temurin)
RUN apt-get update && apt-get install -y \
    maven \
    curl \
    wget \
    zstd \
    gnupg \
    lsb-release \
    && mkdir -p /etc/apt/keyrings \
    && wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | tee /etc/apt/keyrings/adoptium.asc \
    && echo "deb [signed-by=/etc/apt/keyrings/adoptium.asc] https://packages.adoptium.net/artifactory/deb $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/adoptium.list \
    && apt-get update \
    && apt-get install -y temurin-25-jdk \
    && rm -rf /var/lib/apt/lists/*

# 2. Criar um link simbólico independente da arquitetura (amd64 ou arm64)
RUN ln -s $(ls -d /usr/lib/jvm/temurin-25-jdk-* | head -n 1) /usr/lib/jvm/java-25

# 3. Configurar as variáveis de ambiente apontando para o link simbólico
ENV JAVA_HOME=/usr/lib/jvm/java-25
ENV PATH="${JAVA_HOME}/bin:${PATH}"