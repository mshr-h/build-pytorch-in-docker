FROM nvidia/cuda:12.4.0-runtime-ubuntu22.04

COPY --from=ghcr.io/astral-sh/uv:latest --chown=vscode: /uv /uvx /bin/

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN apt update && DEBIAN_FRONTEND=noninteractive apt install -y \
  build-essential \
  ccache \
  curl \
  git \
  libffi-dev \
  libomp-dev \
  libopenblas-dev \
  pkg-config \
  wget \
  && apt autoclean \
  echo 'export CCACHE_DIR=/home/$USERNAME/.ccache' >> /etc/profile && \
  echo 'export USE_CCACHE=1' >> /etc/profile && \
  echo 'export UV_LINK_MODE=copy' >> /etc/profile && \
  rm -rf /var/lib/apt/lists/*

RUN groupadd --gid $USER_GID $USERNAME \
  && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
  && apt-get update \
  && apt-get install -y sudo \
  && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
  && chmod 0440 /etc/sudoers.d/$USERNAME

USER $USERNAME
WORKDIR /home/$USERNAME
