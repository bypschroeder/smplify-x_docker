FROM nvidia/cuda:11.6.1-cudnn8-devel-ubuntu20.04

ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /smplify-x
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3-dev \
    python3-pip \
    git \
    unzip \
    build-essential \
    wget \
    libgl1-mesa-glx \
    libglib2.0-0 && \
    apt-get clean

WORKDIR /smplx
RUN pip3 install --no-cache-dir chumpy smplx[all] \
    git+https://github.com/nghorbani/configer 

RUN git clone https://github.com/vchoutas/smplx . && \
    python3 setup.py install
RUN wget -O /smplx/models_smplx_v1_1.zip "https://www.dropbox.com/scl/fi/sq5tzk1stcmjn6e3iadi6/models_smplx_v1_1.zip?rlkey=bjou496ef97zbfc0j0bslxjeg&st=lu588o61&dl=1" && \
    unzip -n /smplx/models_smplx_v1_1.zip -d /smplx
RUN mkdir /vposer && wget -O /vposer/V02_05.zip "https://www.dropbox.com/scl/fi/iikqr1ocfthtptmfo2cjz/V02_05.zip?rlkey=gj0jlwruni7tfaf556n9pieuz&st=b2onbhct&dl=1" && \
    unzip -n /vposer/V02_05.zip -d /vposer

WORKDIR /smplify-x
RUN git clone https://github.com/KyujinHan/Smplify-X-Perfect-Implementation . && \
    pip3 install -r requirements.txt || true

RUN pip3 install --no-cache-dir configargparse omegaconf loguru git+https://github.com/nghorbani/human_body_prior