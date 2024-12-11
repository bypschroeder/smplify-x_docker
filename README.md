# Docker setup for SMPLify-X and OpenPose

A Docker setup for SMPLify-X and OpenPose creating a shared volume and building the images.

## Requirements
- https://docs.nvidia.com/cuda/wsl-user-guide/index.html
- https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html

## Usage

To build:
```bash
docker-compose up --build
```

To run:
```bash
docker-compose up 
```

To run OpenPose or SMPLify-X, navigate to the respective container. For detailed instructions, refer to ```smplify-x/README.md``` and ```openpose/README.md```.