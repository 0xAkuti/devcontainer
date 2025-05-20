# syntax=docker/dockerfile:1.8
# check=error=true

FROM ghcr.io/0xakuti/devcontainer/smart-contracts:latest

# The base image should set the user to vscode and configure zsh as the default shell.
# We'll run installations as vscode user.
USER vscode
WORKDIR /home/vscode

# Set shell to zsh with -ic for install scripts that might expect an interactive setup
SHELL ["/usr/bin/zsh", "-ic"]

# Install vLayer
RUN curl -SL https://install.vlayer.xyz | bash
RUN vlayerup

# Install bun
RUN curl -fsSL https://bun.sh/install | bash

USER root
# Backup /etc/os-release and spoof VERSION_CODENAME to bookworm and VERSION_ID to 12
# This is primarily for dev container docker-in-docker feature that officially doesn't support trixie yet
RUN cp /etc/os-release /etc/os-release.bak && \
    sed -i 's/VERSION_CODENAME=trixie/VERSION_CODENAME=bookworm/g' /etc/os-release && \
    sed -i '/^VERSION_ID=/s/=.*/="12"/' /etc/os-release && \
    echo "INFO: Spoofed /etc/os-release to pretend to be bookworm (Debian 12). Original backed up." && \
    echo "INFO: Current /etc/os-release content:" && \
    cat /etc/os-release

USER vscode
# Create a default README in the workspace.
WORKDIR /home/vscode/workspace
RUN echo "# vlayer Devcontainer Workspace" > README.md

