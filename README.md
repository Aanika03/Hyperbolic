# Hyperbolic
#!/bin/bash

# Hyperbolic Node Setup Script for WSL2
# This script will install dependencies, configure the environment, and run a hyperbolic node

# Check if running as root
if [ "$EUID" -ne 0 ]; then
    echo "Please run this script as root or with sudo"
    exit 1
fi

# Update package lists
echo "Updating package lists..."
apt-get update -y

# Install required dependencies
echo "Installing dependencies..."
apt-get install -y \
    build-essential \
    git \
    curl \
    wget \
    python3 \
    python3-pip \
    python3-venv \
    libssl-dev \
    pkg-config \
    cmake

# Install Rust (required for many hyperbolic implementations)
echo "Installing Rust..."
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
source $HOME/.cargo/env

# Clone hyperbolic node repository (replace with actual repository)
echo "Cloning hyperbolic node repository..."
HYPERBOLIC_REPO="https://github.com/hyperbolic-space/hyperbolic-core.git"
HYPERBOLIC_DIR="/opt/hyperbolic-node"

if [ ! -d "$HYPERBOLIC_DIR" ]; then
    git clone $HYPERBOLIC_REPO $HYPERBOLIC_DIR
else
    echo "Repository
