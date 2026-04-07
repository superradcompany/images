# Claude Code CLI Docker Image
FROM node:22-slim

# Install git and other useful tools for Claude Code
RUN apt-get update && apt-get install -y \
    git \
    curl \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Install Claude Code CLI globally
RUN npm install -g @anthropic-ai/claude-code

# Create a non-root user for running Claude
RUN useradd -m -s /bin/bash claude
USER claude
WORKDIR /home/claude/workspace

# Set up git config (Claude Code uses git)
RUN git config --global user.name "Claude User" && \
    git config --global user.email "claude@docker.local"

# API keys/tokens must be provided at runtime
# docker run -e ANTHROPIC_API_KEY=your-key ...

# Default command - start Claude
ENTRYPOINT ["claude"]
