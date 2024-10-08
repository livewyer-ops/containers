## Stage 1: prepare binary
# Base image
FROM alpine:3 as build

# Build arguments
ARG BINARY_VERSION="1.8.1"
ARG TARGETARCH=amd64
ARG TARGETOS=linux

# Copy checksum file in the image
COPY checksums.sha512 /checksums.sha512

# Safe scripting
SHELL ["/bin/ash", "-eo", "pipefail", "-c"]

# Install required packages
RUN apk add --update --no-cache \
    binutils

# Download binary
RUN wget -q "https://github.com/kubernetes-sigs/cluster-api/releases/download/v$BINARY_VERSION/clusterctl-$TARGETOS-$TARGETARCH"

# Verify binary and install
RUN grep "clusterctl-$TARGETOS-$TARGETARCH" checksums.sha512 | sha512sum -c; \
    install -s -o root -g root -m 0755 "clusterctl-$TARGETOS-$TARGETARCH" /usr/local/bin/clusterctl

## Final stage: prepare image
FROM alpine:3.19 AS clusterctl

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
COPY --from=build /usr/local/bin/clusterctl /usr/local/bin/clusterctl

# Set binary as entrypoint command
ENTRYPOINT [ "clusterctl" ]
