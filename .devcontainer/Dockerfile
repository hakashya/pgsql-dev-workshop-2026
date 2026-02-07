# Use the latest Ubuntu LTS distribution
FROM ubuntu:24.04

# Set environment variables to avoid interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Update package list and install C/C++ development tools
RUN apt-get update && apt-get install -y \
    # Essential build tools
    build-essential \
    # GCC and G++ compilers
    gcc \
    g++ \
    # Make utility
    make \
    # CMake build system
    cmake \
    # GDB debugger
    gdb \
    # Git version control
    git \
    # pkg-config for managing compile and link flags
    pkg-config \
    # Additional development tools
    autoconf \
    automake \
    libtool \
    # Utilities
    curl \
    wget \
    vim \
    nano \
    # Clean up to reduce image size
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Set the default shell to bash
SHELL ["/bin/bash", "-c"]

# Create a non-root user for development
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Set the default user
USER $USERNAME

# Set working directory
WORKDIR /workspace
