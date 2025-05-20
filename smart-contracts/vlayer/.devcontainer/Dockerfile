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
RUN curl -SL https://install.vlayer.xyz | bash && \
    vlayerup

# Install bun
RUN curl -fsSL https://bun.sh/install | bash

# Create a default README in the workspace.
WORKDIR /home/vscode/workspace
RUN echo "# vlayer Devcontainer Workspace" > README.md

