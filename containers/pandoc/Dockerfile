ARG PANDOC_BINARY_VERSION="3.1.1"
ARG TARGETARCH=amd64 
ARG TARGETOS=linux

# Use Pandoc as base image
FROM pandoc/latex:${PANDOC_BINARY_VERSION}

# OCI Labels
LABEL org.opencontainers.image.authors="hello@livewyer.com"
LABEL org.opencontainers.image.url="https://livewyer.io"
LABEL org.opencontainers.image.source="https://github/livewyer-ops"
LABEL org.opencontainers.image.licenses="MIT"
LABEL org.opencontainers.image.version="$PANDOC_BINARY_VERSION"

# Safe scripting
SHELL ["/bin/ash", "-eo", "pipefail", "-c"]

# Install required packages
RUN apk add --upgrade --update --no-cache \
    bash \
    git \
    yq

# Create/set user and group
RUN set -eu; \
    addgroup -g 1001 group; \
    adduser -D -u 1001 -G group user
USER 1001

# Set bash as entrypoint command
ENTRYPOINT [ "/bin/bash" ]
