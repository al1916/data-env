FROM python:3.11-bookworm

# Variables d'environnement
ENV PYTHONUNBUFFERED=1 \
    DEBIAN_FRONTEND=noninteractive \
    PIP_NO_CACHE_DIR=1

# Installation des outils système essentiels
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    curl \
    wget \
    vim \
    nano \
    build-essential \
    postgresql-client \
    && rm -rf /var/lib/apt/lists/*

# Créer un utilisateur non-root
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Passer à l'utilisateur
USER $USERNAME

# Copier et installer les requirements Python
COPY requirements.txt /tmp/pip-tmp/
RUN pip install --upgrade pip && \
    pip install -r /tmp/pip-tmp/requirements.txt && \
    rm -rf /tmp/pip-tmp

# Définir le répertoire de travail
WORKDIR /workspace

CMD [ "sleep", "infinity" ]
