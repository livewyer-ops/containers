# Final image
FROM alpine:3 AS git

# Build arguments
ARG GIT_CLI_VERSION="2.45.1-r0"
ARG GH_CLI_VERSION="2.47.0-r2"
ARG GLAB_CLI_VERSOIN="1.40.0-r1"

# OCI Labels
LABEL org.opencontainers.image.authors="hello@livewyer.com"
LABEL org.opencontainers.image.url="https://livewyer.io"
LABEL org.opencontainers.image.source="https://github/livewyer-ops"
LABEL org.opencontainers.image.licenses="MIT"

# Install necessary packages
RUN apk --update --upgrade --no-cache add \
    bash jq \
    git=${GIT_CLI_VERSION} \
    github-cli=${GH_CLI_VERSION} \
    glab=${GLAB_CLI_VERSOIN}

# Create/set user and group
RUN set -eu; \
    addgroup -g 1000 group; \
    adduser -D -u 1000 -G group user
USER 1000

# Set git CLI as CMD command
SHELL [ "bash" ]
