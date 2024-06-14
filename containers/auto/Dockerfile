# hadolint global ignore=DL3059

# Use Bitnami Debian as base image
FROM bitnami/minideb:bookworm

# Build arguments
ARG BINARY_VERSION=11.1.6
ARG TARGETARCH=amd64
ARG TARGETOS=linux

# OCI Labels
LABEL org.opencontainers.image.authors="hello@livewyer.com"
LABEL org.opencontainers.image.url="https://livewyer.io"
LABEL org.opencontainers.image.source="https://github/livewyer-ops"
LABEL org.opencontainers.image.licenses="MIT"
LABEL org.opencontainers.image.version="${BINARY_VERSION}"

# Copy checksum file in the image
COPY checksums.sha512 /checksums.sha512

# Safe scripting
SHELL ["/bin/bash", "-euo", "pipefail", "-c"]

# Install required packages
RUN install_packages \
    ca-certificates \
    git \
    wget

# Download, verify, archive, extract binary and install
RUN wget -q "https://github.com/intuit/auto/releases/download/v${BINARY_VERSION}/auto-${TARGETOS}.gz"; \
    grep "auto-$TARGETOS.gz" checksums.sha512 | sha512sum -c; \
    gunzip "auto-$TARGETOS.gz"; install -o root -g root -m 0755 "auto-$TARGETOS" /usr/local/bin/auto; \
    rm checksums.sha512 "auto-$TARGETOS"

# Create/set user and group
RUN set -eu; \
    groupadd -g 65532 git; \
    useradd -m -g 65532 -u 65532 git
USER 65532
WORKDIR /home/git

# Set bash as default command
CMD [ "/usr/local/bin/auto" ]
