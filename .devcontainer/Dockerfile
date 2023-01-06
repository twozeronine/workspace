ARG UBUNTU_VERSION=jammy-20220428
FROM hexpm/elixir:1.14.0-rc.1-erlang-25.2-ubuntu-${UBUNTU_VERSION}

# Common
ARG COMMON_SCRIPT=common-debian.sh

# GitHub CLI
ARG GITHUB_CLI_VERSION=latest
ARG GITHUB_CLI_SCRIRP=github-debian.sh

# for phx.new
ARG PHOENIX_VERSION="1.6.10"

ARG SCRIPT_SOURCE=https://raw.githubusercontent.com/microsoft/vscode-dev-containers/main/script-library

RUN DEBIAN_FRONTEND=nointeractive \
    && apt-get update \
    && apt-get -y install --no-install-recommends \
    apt-transport-https \
    curl \
    ca-certificates \
    # Common
    && curl -sSL ${SCRIPT_SOURCE}/${COMMON_SCRIPT} -o /tmp/${COMMON_SCRIPT} \
    && /bin/bash /tmp/${COMMON_SCRIPT} \
    # GitHub CLI
    && curl -sSL ${SCRIPT_SOURCE}/${GITHUB_CLI_SCRIRP} -o /tmp/${GITHUB_CLI_SCRIRP} \
    && /bin/bash /tmp/${GITHUB_CLI_SCRIRP} ${GITHUB_CLI_VERSION} \
    # Clean Up
    && apt-get -y autoremove \ 
    && apt-get -y clean \ 
    && rm -rf /var/lib/apt/lists/* /tmp/* \
    # Phoenix
    && mix local.rebar --force \
    && mix local.hex --force \
    && mix archive.install hex phx_new --force ${PHOENIX_VERSION} 