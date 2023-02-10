# Use debian as base system
FROM ubuntu:18.04

ENV LC_ALL en_US.UTF-8
ARG user
ARG group
ARG uid
ARG gid
ARG HOME=/home/${user}
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
	apt-get upgrade --no-install-recommends -y locales tzdata sudo curl git && \
	apt-get install --no-install-recommends -y patch bzip2 git bash-completion doxygen && \
	apt-get install --no-install-recommends -y build-essential libncurses-dev mtd-utils && \
	apt-get install --no-install-recommends -y gcc-multilib g++-multilib && \
	apt-get install --no-install-recommends -y bison flex libboost-system-dev libboost-filesystem-dev && \
        apt-get install --no-install-recommends -y python-pip python3-pip && \
	groupadd -g ${gid} ${group} && \
	useradd --create-home --shell /bin/bash -u ${uid} -g ${gid} ${user} && \
	locale-gen "en_US.UTF-8" && \
	echo "Asia/Taipei" > /etc/timezone && \
	dpkg-reconfigure -f noninteractive tzdata locales

WORKDIR ${HOME}
RUN echo "${user} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/${user} && \
	chmod 0440 /etc/sudoers.d/${user}

# Install Python2
RUN curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py && python2 get-pip.py
RUN pip2 install --upgrade pip
RUN pip install gitpython kconfiglib

# Inatall Python3
RUN pip3 install --upgrade pip
RUN pip3 install gitpython kconfiglib

# Config Python alternative(python2 as default)
RUN update-alternatives --install /usr/bin/python python /usr/bin/python2 30 && update-alternatives --install /usr/bin/python python /usr/bin/python3 20

# Download and install ARM toolchain
RUN curl https://armkeil.blob.core.windows.net/developer/Files/downloads/gnu-rm/10-2020q4/gcc-arm-none-eabi-10-2020-q4-major-x86_64-linux.tar.bz2 --output gcc-arm-none-eabi-10-2020-q4-major-x86_64-linux.tar.bz2
RUN mkdir -p /opt/altair && tar -C /opt/altair -xvf gcc-arm-none-eabi-10-2020-q4-major-x86_64-linux.tar.bz2 && rm gcc-arm-none-eabi-10-2020-q4-major-x86_64-linux.tar.bz2

# Add PATH
USER ${user}:${group}
RUN echo "export PATH=$PATH:~/.local/bin:/opt/altair/gcc-arm-none-eabi-10-2020-q4-major/bin" >> ${HOME}/.bashrc
RUN echo "export TERM=xterm-256color" >> ${HOME}/.bashrc

