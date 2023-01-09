#-------------------------------------------------------------------------------------------------------------
# Copyright (c) Microsoft Corporation. All rights reserved.
# Licensed under the MIT License. See https://go.microsoft.com/fwlink/?linkid=2090316 for license information.
#-------------------------------------------------------------------------------------------------------------

FROM ubuntu:latest

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
    && apt-get -y install --no-install-recommends apt-utils 2>&1

# Verify git and needed tools are installed
RUN apt-get install --no-install-recommends -y git procps
RUN apt-get install --no-install-recommends -y ssh

# Install Tex Live
RUN apt-get update
RUN apt-get -y upgrade

RUN apt-get -y install --no-install-recommends \
    texlive-latex-base
RUN apt-get -y install --no-install-recommends \
    texlive-extra-utils
RUN apt-get -y install --no-install-recommends \
    texlive-latex-extra
RUN apt-get -y install --no-install-recommends \
    texlive-science
RUN apt-get -y install --no-install-recommends \
    texlive-lang-polish
RUN apt-get -y install --no-install-recommends \
    biber chktex latexmk make
RUN apt-get -y install --no-install-recommends \
    python3-pygments python3-pkg-resources

# latexindent modules
RUN apt-get install --no-install-recommends -y curl
RUN curl -L http://cpanmin.us | perl - App::cpanminus \
    && cpanm Log::Dispatch::File \
    && cpanm YAML::Tiny \
    && cpanm File::HomeDir \
    && cpanm Unicode::GCString

# Clean up
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*
ENV DEBIAN_FRONTEND=dialog \
    LANG=C.UTF-8 \
    LC_ALL=C.UTF-8