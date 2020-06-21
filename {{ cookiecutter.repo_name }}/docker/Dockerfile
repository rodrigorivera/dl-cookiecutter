ARG IMAGE_DL={{ cookiecutter.base_docker_image  }}
FROM $IMAGE_DL
ADD requirements.txt /build/requirements.txt
WORKDIR /build/
# Install JAX
# alternatives: cp36, cp37, cp38
# alternatives: cuda92, cuda100, cuda101, cuda102
# alternatives: linux_x86_64
# install jax
RUN pip install -r requirements.txt &&\
    PYTHON_VERSION="cp37"   &&\
    CUDA_VERSION="cuda102"  && \
    PLATFORM="linux_x86_64"  && \
    BASE_URL='https://storage.googleapis.com/jax-releases' && \ 
    pip install --upgrade $BASE_URL/$CUDA_VERSION/jaxlib-0.1.48-$PYTHON_VERSION-none-$PLATFORM.whl && \ 
    pip install --upgrade jax  
WORKDIR /mnt/