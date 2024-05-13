## Stage 1: prepare binary
# Base image
FROM alpine:3 as build

# Maintainers
LABEL org.opencontainers.image.authors="hello@livewyer.com"

# Build arguments
ARG BINARY_VERSION="3.14.2"
ARG TARGETARCH=amd64
ARG TARGETOS=linux
hello
error
# Copy checksum file in the image
COPY checksums.sha512 /checksums.sha512

# Safe scripting
SHELL ["/bin/ash", "-eo", "pipefail", "-c"]

# Download binary archive
RUN wget -q "https://get.helm.sh/helm-v$BINARY_VERSION-$TARGETOS-$TARGETARCH.tar.gz"

# Verify archive, extract binary and install
RUN grep "helm-v$BINARY_VERSION-$TARGETOS-$TARGETARCH.tar.gz" checksums.sha512 | sha512sum -c; \
    tar xzf "helm-v$BINARY_VERSION-$TARGETOS-$TARGETARCH.tar.gz"; \
    install -o root -g root -m 0755 "$TARGETOS-$TARGETARCH/helm" /usr/local/bin/helm

## Final stage: prepare image
FROM alpine:3 AS helm

# OCI labels
LABEL org.opencontainers.image.authors="hello@livewyer.com"
LABEL org.opencontainers.image.url="https://livewyer.io"
LABEL org.opencontainers.image.source="https://github/livewyer-ops"
LABEL org.opencontainers.image.licenses="MIT"
LABEL org.opencontainers.image.version="$BINARY_VERSION"

# Create/set user and group
RUN set -eu; \
    addgroup -g 1000 group; \
    adduser -D -u 1000 -G group user
USER 1000

# Copy clusterctl binary from the build stage
COPY --from=build /usr/local/bin/helm /usr/local/bin/helm

# Set binary as entrypoint command
ENTRYPOINT [ "helm" ]
