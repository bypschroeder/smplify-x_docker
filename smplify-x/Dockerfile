FROM python:3.9.21-slim

WORKDIR /smplify-x
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    unzip \
    build-essential \
    wget && \
    apt-get clean

WORKDIR /smplx
RUN pip install --no-cache-dir chumpy smplx[all] \
    git+https://github.com/nghorbani/configer \
    git+https://github.com/nghorbani/human_body_prior

RUN git clone https://github.com/vchoutas/smplx . && \
    python setup.py install
RUN wget -O /smplx/models_smplx_v1_1.zip "https://www.dropbox.com/scl/fi/sq5tzk1stcmjn6e3iadi6/models_smplx_v1_1.zip?rlkey=bjou496ef97zbfc0j0bslxjeg&st=lu588o61&dl=1" && \
    unzip -n /smplx/models_smplx_v1_1.zip -d /smplx
RUN mkdir /vposer && wget -O /vposer/V02_05.zip "https://www.dropbox.com/scl/fi/iikqr1ocfthtptmfo2cjz/V02_05.zip?rlkey=gj0jlwruni7tfaf556n9pieuz&st=b2onbhct&dl=1" && \
    unzip -n /vposer/V02_05.zip -d /vposer

WORKDIR /smplify-x
RUN git clone https://github.com/KyujinHan/Smplify-X-Perfect-Implementation . && \
    cd Smplify-X-Perfect-Implementation && \
    pip install -r requirements.txt || true

RUN pip install --no-cache-dir configargparse omegaconf loguru