# Docker Image for SMPLify-x

A docker build file for SMPLify-x.

## Requirements
- https://docs.nvidia.com/cuda/wsl-user-guide/index.html
- https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html

## Installation

### Build the image using the Dockerfile
```bash
cd ./smplify-x
sudo docker build -t smplifyx .
```

### Start docker env

```bash
sudo docker run --gpus all --name smplifyx -it smplifyx:latest /bin/bash
```

### Example usage

```bash
python3 /smplify-x/smplifyx/main.py --config /smplify-x/cfg_files/fit_smplx.yaml --data_folder /data --output_folder /data/smplify-x_results --visualize=False --gender="male" --model_folder /smplx/models --vposer_ckpt /vposer/V02_05 --part_segm_fn smplx_parts_segm.pkl
```