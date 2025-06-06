
# Use the official Ubuntu base image
FROM ubuntu:22.04

# Avoid prompts from apt
ARG DEBIAN_FRONTEND=noninteractive

# Install basic utilities and dependencies
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    git \
    build-essential \
    zsh \
    sudo \
    openssh-server \
    python3 \
    python3-pip \
    python3-venv \
    && rm -rf /var/lib/apt/lists/*

# Install Pandoc and TeXLive with required packages
RUN apt-get update && apt-get install -y \
    pandoc \
    texlive-full \
    texlive-latex-extra \
    texlive-fonts-extra \
    texlive-xetex \
    lmodern \
    && rm -rf /var/lib/apt/lists/*

# Create a non-root user and add to sudoers
ARG USERNAME=codespace
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Set the default user
USER $USERNAME

# Install Oh My Zsh
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended

# Set default shell to zsh
ENV SHELL /bin/zsh
