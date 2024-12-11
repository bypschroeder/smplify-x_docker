# Docker Image for SMPLify-x

A docker build file for SMPLify-x.

## Requirements
- https://docs.nvidia.com/cuda/wsl-user-guide/index.html
- https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html

## Installation

### Build the image using the Dockerfile
```bash
cd ./smplify-x
sudo docker build -t smplify-x .
```

### Start docker env

```bash
sudo docker run --gpus all --name smplifyx -it smplify-x:latest /bin/bash
```

### Example usage

```bash
cd /smplify-x
python3 smplifyx/main.py --config cfg_files/fit_smplx.yaml --data_folder ../shared/data/ --output_folder ../shared/data/smplify-x_results --visualize=False --gender="male" --model_folder ../smplx/models --vposer_ckpt ../vposer/V02_05
```