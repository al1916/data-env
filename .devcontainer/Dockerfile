FROM python:3.11-bookworm

ENV PYTHONUNBUFFERED=1 \
    DEBIAN_FRONTEND=noninteractive \
    PIP_NO_CACHE_DIR=1

# Installation des outils systeme
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    curl \
    wget \
    vim \
    nano \
    build-essential \
    postgresql-client \
    sudo \
    && rm -rf /var/lib/apt/lists/*

# Creer utilisateur vscode
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Copier requirements en tant que root
COPY requirements.txt /tmp/requirements.txt

# Installer les packages Python en tant que root
RUN pip install --upgrade pip && \
    pip install -r /tmp/requirements.txt

# Nettoyer (en tant que root, pas de probleme de permission)
RUN rm -f /tmp/requirements.txt

# Creer le repertoire workspace
RUN mkdir -p /workspace && chown -R $USERNAME:$USERNAME /workspace

# Passer a l'utilisateur vscode
USER $USERNAME
WORKDIR /workspace

CMD [ "sleep", "infinity" ]
