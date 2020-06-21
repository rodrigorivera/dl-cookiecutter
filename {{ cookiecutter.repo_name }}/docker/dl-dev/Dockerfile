ARG IMAGE_BASE=/base-sys-dl:gpu
FROM ${IMAGE_BASE}
COPY . /build
WORKDIR /build
# Separely split pip to avoid pip install main issue
RUN apt-get update &&\
    DEBIAN_FRONTEND=noninteractive apt-get install -y libpq-dev &&\
    pip install -r requirements.txt &&\
    jupyter contrib nbextension install --user &&\
    mkdir -p /home/orca && \
    cd /home/orca && \
    wget https://github.com/plotly/orca/releases/download/v1.2.1/orca-1.2.1-x86_64.AppImage && \
    chmod +x orca-1.2.1-x86_64.AppImage && \
    ./orca-1.2.1-x86_64.AppImage --appimage-extract && \
    printf '#!/bin/bash \nxvfb-run --auto-servernum --server-args "-screen 0 640x480x24" /home/orca/squashfs-root/app/orca "$@"' > /usr/bin/orca && \
    chmod +x /usr/bin/orca
# END ffmpeg install specific lines
# Python installs
ENV PYTHONPATH="/mnt:${PYTHONPATH}"
WORKDIR /mnt
RUN apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* ~/* && \
    rm -rf /build && \
    rm -rf ~/.cache