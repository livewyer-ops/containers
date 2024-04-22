FROM ubuntu:22.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get --assume-yes --no-install-recommends install \
    ca-certificates=20230311ubuntu0.22.04.1 librsvg2-bin=2.52.5+dfsg-3ubuntu0.2 wget=1.21.2-2ubuntu1 git=1:2.34.1-1ubuntu1.10 texlive=2021.20220204-1 texlive-fonts-recommended=2021.20220204-1 texlive-fonts-extra=2021.20220204-1 pandoc=2.9.2.1-3ubuntu2 lmodern=2.004.5-6.1 texlive-latex-extra=2021.20220204-1 texlive-xetex=2021.20220204-1 && \
    rm -rf /var/lib/apt/lists/*
RUN wget -q https://github.com/cli/cli/releases/download/v2.48.0/gh_2.48.0_linux_amd64.deb && \
    dpkg -i gh_2.2.0_linux_amd64.deb
RUN wget -q https://github.com/jgm/pandoc/releases/download/3.1.13/pandoc-3.1.13-1-amd64.deb && \
    dpkg -i pandoc-2.16.2-1-amd64.deb
RUN wget -q https://github.com/mikefarah/yq/releases/download/v4.43.1/yq_linux_amd64.tar.gz -O /usr/bin/yq && \
    chmod +x /usr/bin/yq
