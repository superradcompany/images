# OpenCode CLI Docker Image
FROM debian:bookworm-slim

# Install dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    ca-certificates \
    ripgrep \
    fzf \
    tini \
    && rm -rf /var/lib/apt/lists/*

# Install OpenCode via official install script
RUN curl -fsSL https://opencode.ai/install | bash \
    && mv /root/.opencode/bin/opencode /usr/local/bin/opencode \
    && rm -rf /root/.opencode

# Create a non-root user for running OpenCode
RUN useradd -m -s /bin/bash opencode
USER opencode
WORKDIR /home/opencode/workspace

# Set up git config (OpenCode uses git)
RUN git config --global user.name "OpenCode User" && \
    git config --global user.email "opencode@docker.local"

# API keys must be provided at runtime
# docker run -e ANTHROPIC_API_KEY=your-key ...

# Default command - start OpenCode with tini for proper signal handling
ENTRYPOINT ["tini", "--", "opencode"]
