FROM --platform=linux/amd64 ubuntu:20.04

LABEL maintainer="ldfandian@hotmail.com"
LABEL version="0.1.0"

# change to use China sources
RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/' /etc/apt/sources.list \
 && sed -i 's/security.ubuntu.com/mirrors.aliyun.com/' /etc/apt/sources.list 

# basic os management tools
ENV LANGUAGE=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LC_ALL=C
RUN apt-get update -y \
  && apt-get install -y apt-utils \
  && apt-get install -y iproute2 procps lsb-release build-essential net-tools iputils-ping file psmisc \
  && apt-get install -y vim wget curl tree jshon

# install basic dev tools
RUN apt-get install -y g++ gcc make autoconf automake
RUN apt-get install -y git

# install python
RUN apt-get autoremove -y && apt-get -y update --fix-missing
RUN apt-get install -y python3 python3-venv python3-pip

# install conda pkg mgmt system
RUN wget -O /tmp/Miniconda3-py38_4.12.0-Linux-x86_64.sh https://repo.anaconda.com/miniconda/Miniconda3-py38_4.12.0-Linux-x86_64.sh \
  && /bin/bash /tmp/Miniconda3-py38_4.12.0-Linux-x86_64.sh -b \
  && rm -f /tmp/Miniconda3-py38_4.12.0-Linux-x86_64.sh
ENV PATH /root/miniconda3/bin/:$PATH
RUN conda init bash

# install GPU extension
RUN DEBIAN_FRONTEND=noninteractive TZ=Asia/Shanghai \
  apt-get install -y libgl1 libglib2.0-dev

# setup global mirror config for the python
RUN pip3 config set global.index-url https://mirrors.aliyun.com/pypi/simple --user
RUN pip3 config set install.trusted-host mirrors.aliyun.com --user


# set working directory 
WORKDIR /mnt/devroot/stable-diffusion-webui-devkit/

# starting app
CMD [ "/bin/bash" ]

