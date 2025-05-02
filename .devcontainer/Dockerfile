FROM nvidia/cuda:12.4.0-runtime-ubuntu22.04

COPY --from=ghcr.io/astral-sh/uv:latest --chown=vscode: /uv /uvx /bin/

ARG USERNAME=vscode
ARG UID=1000
ARG GID=1000

RUN apt update && DEBIAN_FRONTEND=noninteractive apt install -y \
  build-essential \
  ccache \
  curl \
  git \
  libffi-dev \
  libomp-dev \
  libopenblas-dev \
  pkg-config \
  sudo \
  wget \
  && apt autoclean \
  echo 'export CCACHE_DIR=/home/vscode/.ccache' >> /etc/profile && \
  echo 'export USE_CCACHE=1' >> /etc/profile && \
  rm -rf /var/lib/apt/lists/*

RUN useradd -m vscode && echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

ENV PATH="/home/vscode/.local/bin:${PATH}"
ENV UV_LINK_MODE=copy

USER vscode
WORKDIR /home/vscode
