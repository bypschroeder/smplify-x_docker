FROM nvidia/cuda:11.6.1-cudnn8-devel-ubuntu20.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    g++ \
    wget \
    make \
    unzip \
    libatlas-base-dev \
    libprotobuf-dev \
    libleveldb-dev \
    libsnappy-dev \
    libhdf5-serial-dev \
    protobuf-compiler \
    libgflags-dev \
    libgoogle-glog-dev \
    liblmdb-dev \
    opencl-headers \
    ocl-icd-opencl-dev \
    libviennacl-dev && \
    apt-get clean

RUN wget https://cmake.org/files/v3.13/cmake-3.13.0-Linux-x86_64.tar.gz && \
    tar -xfz cmake-3.13.0-Linux-x86_64.tar.gz --strip-components=1 -C /usr/local && \
    rm cmake-3.13.0-Linux-x86_64.tar.gz
ENV PATH="/usr/local/cmake-3.16.0-Linux-x86_64/bin:${PATH}"

WORKDIR /openpose
RUN git clone --depth 1 https://github.com/CMU-Perceptual-Computing-Lab/openpose.git .

COPY openpose_models.zip /openpose/models/
RUN unzip -n openpose_models.zip -d /openpose/models/ && \ 
    mv /openpose/models/pose_iter_102000.caffemodel /openpose/models/hand && \
    mv /openpose/models/pose_iter_584000.caffemodel /openpose/models/pose/body_25 && \
    mv /openpose/models/pose_iter_116000.caffemodel /openpose/models/face && \
    rm /openpose/models/openpose_models.zip

RUN sed -i 's/execute_process(COMMAND git checkout master WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}\/3rdparty\/caffe)/execute_process(COMMAND git checkout f019d0dfe86f49d1140961f8c7dec22130c83154 WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}\/3rdparty\/caffe)/g' openpose/CMakeLists.txt

WORKDIR /openpose/build
RUN cmake .. -DUSE_CUDNN=OFF && make -j`nproc`
