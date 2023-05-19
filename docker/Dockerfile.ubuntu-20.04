# Dockerfile for self-hosted runner with Ubuntu 20.04

FROM ubuntu:20.04

# Install dependencies
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    sudo \
    unzip \
    iputils-ping \
    && rm -rf /var/lib/apt/lists/*

# Working directory
WORKDIR /runner

# Install GitHub Actions Runner
ARG RUNNER_VERSION="2.304.0"
ARG RUNNER_CHECKSUM="292e8770bdeafca135c2c06cd5426f9dda49a775568f45fcc25cc2b576afc12f"

RUN curl -o actions-runner.tar.gz -L https://github.com/actions/runner/releases/download/v${RUNNER_VERSION}/actions-runner-linux-x64-${RUNNER_VERSION}.tar.gz \
    && echo "292e8770bdeafca135c2c06cd5426f9dda49a775568f45fcc25cc2b576afc12f  actions-runner.tar.gz" | sha256sum -c - \
    && tar xzf ./actions-runner.tar.gz \
    && rm actions-runner.tar.gz

# Copy entrypoint script and make it executable
COPY entrypoint.sh .
RUN chmod +x ./entrypoint.sh

# Configure the runner
ENTRYPOINT ["./entrypoint.sh"]
