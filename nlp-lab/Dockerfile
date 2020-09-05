FROM ubuntu:18.04
MAINTAINER DongWookKim <kdw4521@gmail.com>

# install basic setupss
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul
RUN apt-get update && apt-get install -y \
        bash \
        build-essential \
        ca-certificates \
        python 3.7.* \
        locales \
        sudo \
        vim \
        git \
        curl \
        wget \
        openssl \
        libgl1-mesa-glx \
        libglib2.0-0 \
        libgomp1 \
        libibverbs-dev \
        libsm6\
        libxext6\
        libxrender-dev\
        openjdk-8-jdk-headless\
        zip \
        bzip2 \
        libx11-6 \
        gcc

# Install python3.7 pip
RUN curl https://bootstrap.pypa.io/get-pip.py -o /tmp/get-pip.py
RUN python3.7 /tmp/get-pip.py
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3.7 1
ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8

# pip install
COPY requirements.txt /tmp
WORKDIR /tmp
RUN pip install --upgrade pip
RUN pip uninstall -y enum34
RUN pip install -r requirements.txt

# nodejs
RUN apt-get update && curl -sL https://deb.nodesource.com/setup_12.x | bash - && apt-get install -y nodejs

# pip install requirements.txt
COPY requirements.txt /tmp
WORKDIR /tmp
RUN pip install --upgrade pip
RUN pip uninstall -y enum34
RUN pip install -r requirements.txt

# install git and zsh
RUN apt-get install -y zsh git git-lfs
RUN git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.zsh/zsh-syntax-highlighting
RUN echo "source ~/.zsh/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc
RUN git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
RUN echo "source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc
RUN curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | bash

RUN pip install python-language-server[all]

RUN ldconfig && \
    apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* ~/*

# Language Server for @krassowski/jupyterlab-lsp
COPY server.yml /tmp
CMD ["node","usr/local/share/jupyter/lab/staging/node_modules/jsonrpc-ws-proxy/dist/server.js","--port 3000","--languageServers","/tmp/server.yml"]

WORKDIR /root