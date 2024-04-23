# SRC docker image to pull is ubuntu 22.04
FROM ubuntu:22.04
# Set frontend to noninteractive
ARG DEBIAN_FRONTEND=noninteractive
# Arguments to call later
ARG PANDOC_BINARY_VERSION="3.1.13"
ARG GH_BINARY_VERSION="2.48.0"
ARG YQ_BINARY_VERSION="4.43.1"
ARG TARGETARCH=amd64 
ARG TARGETOS=linux
# OCI Labels
LABEL org.opencontainers.image.authors="hello@livewyer.com"
LABEL org.opencontainers.image.url="https://livewyer.io"
LABEL org.opencontainers.image.source="https://github/livewyer-ops"
LABEL org.opencontainers.image.licenses="MIT"
LABEL org.opencontainers.image.version="$BINARY_VERSION"
# apt-get update && installations of some dependencies
RUN apt-get update && \
    apt-get --assume-yes --no-install-recommends install \
    ca-certificates=20230311ubuntu0.22.04.1 librsvg2-bin=2.52.5+dfsg-3ubuntu0.2 wget=1.21.2-2ubuntu1 git=1:2.34.1-1ubuntu1.10 texlive=2021.20220204-1 texlive-fonts-recommended=2021.20220204-1 texlive-fonts-extra=2021.20220204-1 pandoc=2.9.2.1-3ubuntu2 lmodern=2.004.5-6.1 texlive-latex-extra=2021.20220204-1 texlive-xetex=2021.20220204-1 && \
    rm -rf /var/lib/apt/lists/*
# Install GH CLI utility deb from src
RUN wget -q "https://github.com/cli/cli/releases/download/v${GH_BINARY_VERSION}/gh_${GH_BINARY_VERSION}_${TARGETOS}_${TARGETARCH}.deb" -O gh.deb && \
	  dpkg -i gh.deb
# Install pandoc utility binary from src
RUN wget -q "https://github.com/jgm/pandoc/releases/download/$PANDOC_BINARY_VERSION/pandoc-$PANDOC_BINARY_VERSION-1-$TARGETARCH.deb" -O pandoc.deb && \
    dpkg -i pandoc.deb || apt-get update && apt-get -f install
# Install yq from src
RUN wget -q "https://github.com/mikefarah/yq/releases/download/v$YQ_BINARY_VERSION/yq_${TARGETOS}_${TARGETARCH}.tar.gz" -O /usr/bin/yq && \
    chmod +x /usr/bin/yq
