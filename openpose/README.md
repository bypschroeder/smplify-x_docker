# Docker Image for OpenPose

A docker build file for CMU openpose with Python API support.

## Disclaimer
Since the required models aren't hosted anymore on the original location, I uploaded them manually on my dropbox. To use your own link, upload the models to dropbox and paste them like this in the Dockerfile:
```bash
RUN wget -O /openpose/models/hand/pose_iter_102000.caffemodel "{LINK}"
```
Here it is important that the download link has dl=1 at the end, so it directly downloads the file instead of redirecting to a page with a download button.

## Requirements

- https://docs.nvidia.com/cuda/wsl-user-guide/index.html
- https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html

## Installation

### Build the image using the Dockerfile
```bash
cd ./openpose
sudo docker build -t openpose .
```

### Start docker env

```bash
sudo docker run --gpus all --name openpose -it openpose:latest /bin/bash
```

### Example usage

```bash
cd openpose # It is important to be in the root directory
./build/examples/openpose/openpose.bin --image_dir ../shared/data/images/ --write_json ../shared/data/keypoints/ --face --hand --display 0 --write_images ../shared/data/openpose_images/
```