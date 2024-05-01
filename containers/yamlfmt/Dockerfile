## Stage 1: prepare binary
# Base image
FROM golang:1-alpine as build

# Build arguments
ARG BINARY_VERSION="0.11.0"
ARG TARGETARCH=amd64
ARG TARGETOS=linux

# Fetch code and dependencies, compile and strip binary
RUN go install -ldflags "-w" "github.com/google/yamlfmt/cmd/yamlfmt@v$BINARY_VERSION"

## Final stage: prepare image
FROM alpine:3 AS yamlfmt

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
COPY --from=build /go/bin/yamlfmt /usr/local/bin/yamlfmt

# Set binary as entrypoint command
ENTRYPOINT [ "yamlfmt" ]
