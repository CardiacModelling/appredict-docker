FROM debian:bullseye-slim

USER root

RUN echo "deb http://deb.debian.org/debian bullseye main contrib non-free" >> /etc/apt/sources.list

# Install dependencies with recommended, applicable suggested and other useful packages
RUN apt-get update && \
    apt-get install -y g++ cmake && \
    apt-get install -y --no-install-recommends \
    wget \
    git \
    petsc-dev \
    libhdf5-dev \
    libboost-serialization-dev \
    libboost-filesystem-dev \
    libboost-program-options-dev \
    libparmetis-dev \
    xsdcxx \
    libmetis-dev \
    libxerces-c-dev \
    libsundials-dev \
    python3 \
    python3-venv && \
    rm -rf /var/lib/apt/lists/*

ENV HOME=/home/appredict
RUN useradd -ms /bin/bash -d $HOME appredict
USER appredict
