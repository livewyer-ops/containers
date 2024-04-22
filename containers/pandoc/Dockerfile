FROM ubuntu:22.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt update && \
    apt-get --assume-yes --no-install-recommends install ca-certificates librsvg2-bin wget git texlive texlive-fonts-recommended texlive-fonts-extra pandoc lmodern texlive-latex-extra texlive-xetex && \
    rm -rf /var/lib/apt/lists/*
RUN wget https://github.com/cli/cli/releases/download/v2.48.0/gh_2.48.0_linux_amd64.deb && \
    dpkg -i gh_2.2.0_linux_amd64.deb
RUN wget https://github.com/jgm/pandoc/releases/download/3.1.13/pandoc-3.1.13-1-amd64.deb && \
    dpkg -i pandoc-2.16.2-1-amd64.deb
RUN wget https://github.com/mikefarah/yq/releases/download/v4.43.1/yq_linux_amd64.tar.gz -O /usr/bin/yq && \
    chmod +x /usr/bin/yq
