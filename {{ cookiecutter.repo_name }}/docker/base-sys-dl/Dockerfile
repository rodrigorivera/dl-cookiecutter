FROM nvidia/cuda:10.2-cudnn7-devel-ubuntu18.04
# This part below should be same as in orbyter-base-sys/2.x/Dockerfile
WORKDIR /build
ENV LC_ALL=C.UTF-8 \
    LANG=C.UTF-8
RUN apt-get update -qq && \
    DEBIAN_FRONTEND=noninteractive apt-get install -qqy --no-install-recommends \
    gnome-terminal \
    python3.7=3.7.5-2~18.04 \
    python3-pip \
    build-essential \
    nano \
    apt-utils \
    ca-certificates \
    libssl-dev \
    libffi-dev \
    python3.7-dev \
    vim \
    emacs \
    screen \
    git \
    wget \
    curl \
    bzip2 \
    zip \
    unzip \
    libssl-dev \
    libncurses5-dev \
    libncursesw5-dev \
    libopenmpi-dev \
    libopenblas-base \
    libopenblas-dev \
    libomp-dev \
    libjpeg-dev \
    libpng-dev \
    libboost-all-dev \
    libsdl2-dev \
    libcurl4-openssl-dev \
    openssh-client \
    openssh-server \
    swig \
    pkg-config \
    g++ \
    zlib1g-dev \
    protobuf-compiler \
    libosmesa6-dev \
    patchelf \
    xvfb \
    software-properties-common \
    protobuf-compiler \
    libgtk2.0-0 \
    libxtst6 \
    libxss1 \
    libgconf-2-4 \
    libnss3 \
    libasound2 \
    libprotoc-dev \
    libblas-dev \
    libatlas-base-dev \
    libgflags-dev \
    libgoogle-glog-dev \
    libhdf5-serial-dev \
    libleveldb-dev \
    liblmdb-dev \
    libprotobuf-dev \
    libsnappy-dev \
    openmpi-bin \
    libpng-dev \
    libjpeg-dev \
    libtiff-dev \
    cmake \
    libnvinfer6=6.0.1-1+cuda10.2 \
    libnvinfer-dev=6.0.1-1+cuda10.2 \
    libnvinfer-plugin6=6.0.1-1+cuda10.2 \
    htop 
# clean up. Need to change python3 to 3.7 or pip installs get confused
RUN rm -rf /var/lib/apt/lists/* && \
    rm -f /usr/bin/python3 && \
    rm -f /usr/bin/python3.6* && \
    rm -f /usr/bin/python && \
    ln -s /usr/bin/python3.7 /usr/bin/python3 && \
    ln -s /usr/bin/python3.7 /usr/bin/python && \
    ln -s /usr/bin/pip3 /usr/bin/pip && \
    rm -rf ~/.cache
RUN pip install wheel==0.33.6 && \
    pip install setuptools==42.0.2 && \
    pip install -U pip==19.3.1
WORKDIR /
RUN apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* ~/* &&\
    rm -rf /build
