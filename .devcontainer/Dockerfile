FROM mcr.microsoft.com/devcontainers/base:ubuntu

# 1. Install system dependencies
RUN apt-get update && apt-get install -y \
    curl ca-certificates bash git build-essential \
    && rm -rf /var/lib/apt/lists/*

# 2. Install 'uv' globally (The cleanest way)
# We copy it from the official image so it lands in /usr/local/bin
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# 3. Setup NVM in a way the 'vscode' user can actually use
ENV NVM_DIR=/usr/local/nvm
RUN mkdir -p $NVM_DIR && chown vscode:vscode $NVM_DIR

# Switch to the vscode user to install NVM/Node
USER vscode
RUN curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash \
    && . $NVM_DIR/nvm.sh \
    && nvm install --lts \
    && nvm alias default 'lts/*'

# 4. Persistence: Ensure NVM is loaded in every terminal session
RUN echo 'export NVM_DIR="/usr/local/nvm"' >> ~/.bashrc \
    && echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.bashrc