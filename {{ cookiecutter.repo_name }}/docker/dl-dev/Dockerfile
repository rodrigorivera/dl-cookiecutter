FROM ${USER}/base-sys-dl:gpu
COPY . /build
WORKDIR /build
# Separely split pip to avoid pip install main issue
RUN apt-get update &&\
    apt-get install -y libpq-dev &&\
    pip install -r requirements.txt &&\
    jupyter contrib nbextension install --user
# Install JAX
RUN PYTHON_VERSION=cp37  # alternatives: cp36, cp37, cp38 &&\
    CUDA_VERSION=cuda102  # alternatives: cuda92, cuda100, cuda101, cuda102 && \
    PLATFORM=linux_x86_64  # alternatives: linux_x86_64 && \
    BASE_URL='https://storage.googleapis.com/jax-releases' && \ 
    pip install --upgrade $BASE_URL/$CUDA_VERSION/jaxlib-0.1.48-$PYTHON_VERSION-none-$PLATFORM.whl && \ 
    pip install --upgrade jax  # install jax
# Plotly-orca depedencies
RUN apt-get install -y --no-install-recommends \
        xvfb \
        libgtk2.0-0 \
        libxtst6 \
        libxss1 \
        libgconf-2-4 \
        libnss3 \
        libasound2 && \
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
RUN rm -rf /build &&\
    rm -rf ~/.cache