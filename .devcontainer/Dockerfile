FROM mcr.microsoft.com/devcontainers/base:ubuntu

RUN apt-get update && apt-get install -y \
    curl ca-certificates bash git build-essential \
    && rm -rf /var/lib/apt/lists/*

# UV
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# NVM
ENV NVM_DIR=/usr/local/nvm
RUN mkdir -p $NVM_DIR && chown vscode:vscode $NVM_DIR

USER vscode
RUN curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash \
    && . $NVM_DIR/nvm.sh \
    && nvm install --lts \
    && nvm alias default 'lts/*'

RUN echo 'export NVM_DIR="/usr/local/nvm"' >> ~/.bashrc \
    && echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.bashrc