# Final image
FROM alpine:3

# OCI Labels
LABEL org.opencontainers.image.authors="hello@livewyer.com"
LABEL org.opencontainers.image.url="https://livewyer.io"
LABEL org.opencontainers.image.source="https://github/livewyer-ops"
LABEL org.opencontainers.image.licenses="MIT"

# Install necessary packages
RUN apk --update --upgrade --no-cache add \
    bash jq git github-cli glab

# Create/set user and group
RUN set -eu; \
    addgroup -g 65532 git; \
    adduser -D -u 65532 -G git git
USER 65532

# Set BASH as a default shell
ENTRYPOINT [ "/bin/bash" ]
