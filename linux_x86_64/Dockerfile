FROM ubuntu:22.10

ENV DEBIAN_FRONTEND=noninteractive

# Perform full update and install common utilities
RUN \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get autoremove && \
    apt-get autoclean && \
    apt-get -y install \
        cmake \
        ca-certificates \
        wget \
        make \
        git \
        nasm \
        curl \
        libasound2-dev \
        python3 \
        python3-pip \
        libssl-dev \
        gnupg \
        pkg-config \
        apt-transport-https \
        gcc-12 \
        g++-12 \
        libgl1-mesa-dev \
            && \
    apt-get autoclean && \
    python3 -m pip install conan

RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 10

RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-12 10
RUN update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-12 10

ADD remotes.txt /
ADD conanfile.txt /

RUN conan config install remotes.txt

ENV CONAN_SYSREQUIRES_SUDO 0
ENV CONAN_SYSREQUIRES_MODE enabled
RUN conan install . -c tools.system.package_manager:mode=install
