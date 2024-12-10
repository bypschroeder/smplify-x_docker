FROM nvidia/cuda:11.6.1-cudnn8-devel-ubuntu20.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    g++ \
    wget \
    make \
    libatlas-base-dev \
    libprotobuf-dev \
    libleveldb-dev \
    libsnappy-dev \
    libhdf5-serial-dev \
    protobuf-compiler \
    libgflags-dev \
    libgoogle-glog-dev \
    liblmdb-dev \
    libopencv-dev \
    libboost-all-dev \
    opencl-headers \
    ocl-icd-opencl-dev \
    libviennacl-dev && \
    apt-get clean

RUN wget https://cmake.org/files/v3.13/cmake-3.13.0-Linux-x86_64.tar.gz && \
    tar -xzf cmake-3.13.0-Linux-x86_64.tar.gz --strip-components=1 -C /usr/local && \
    rm cmake-3.13.0-Linux-x86_64.tar.gz
ENV PATH="/usr/local/cmake-3.13.0-Linux-x86_64/bin:${PATH}"

WORKDIR /openpose
RUN git clone --depth 1 https://github.com/CMU-Perceptual-Computing-Lab/openpose.git .

RUN wget -O /openpose/models/hand/pose_iter_102000.caffemodel "https://www.dropbox.com/scl/fi/the6q2tj5m215cxq85mko/pose_iter_102000.caffemodel?rlkey=hiasv5euzdg1gzyda5h7fcwvi&st=96mbr3af&dl=1"  && \
    wget -O /openpose/models/pose/body_25/pose_iter_584000.caffemodel "https://www.dropbox.com/scl/fi/pfl1nonefgd2r3w42e2ij/pose_iter_584000.caffemodel?rlkey=hnj53tdg47d4fzgm9fz967tnb&st=hsgm207a&dl=1" && \
    wget -O /openpose/models/face/pose_iter_116000.caffemodel "https://www.dropbox.com/scl/fi/0i0z2fq8o3d75irw8sube/pose_iter_116000.caffemodel?rlkey=mux887c03dr4xtdjwxg0a5n5i&st=yodcb89a&dl=1"

RUN sed -i 's/execute_process(COMMAND git checkout master WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}\/3rdparty\/caffe)/execute_process(COMMAND git checkout f019d0dfe86f49d1140961f8c7dec22130c83154 WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}\/3rdparty\/caffe)/g' /openpose/CMakeLists.txt

WORKDIR /openpose/build
RUN cmake .. -DUSE_CUDNN=OFF && make -j`nproc`
