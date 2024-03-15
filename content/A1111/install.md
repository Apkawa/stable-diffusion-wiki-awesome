+++
title = "Install"
insert_anchor_links = "right"
weight = 100
+++

# Check compatibly version
1) a1111 changelog grep torch https://github.com/AUTOMATIC1111/stable-diffusion-webui/releases/
2) pytorch version https://github.com/pytorch/pytorch/blob/main/RELEASE.md#release-compatibility-matrix
3) check cuda and nvidia driver compatibly https://docs.nvidia.com/deploy/cuda-compatibility/

For 3060 i choosed:

* a1111==1.8.0
* pytorch==2.1.2
* CUDA==11.8
* nvidia==550

## Install driver

* If you have previous installation remove it first.
```
sudo apt-get purge nvidia*
sudo apt remove nvidia-*
sudo rm /etc/apt/sources.list.d/cuda*
sudo apt-get autoremove && sudo apt-get autoclean
sudo rm -rf /usr/local/cuda*
```

* system update
```
sudo apt-get update
sudo apt-get upgrade
```

* install other import packages
  `sudo apt-get install g++ freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev`

* first get the PPA repository driver
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
```

* install nvidia driver with dependencies
```
V=550 sudo apt install libnvidia-common-$V libnvidia-gl-$V nvidia-driver-$V
```

## Install CUDA

Add cuda repository
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/3bf863cc.pub
sudo add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/ /"
sudo apt-get update
```
Install
```
export CUDA_VERSION=11.8
sudo apt install cuda-$(echo $CUDA_VERSION|sed 's/\./-/g')

echo "export PATH=/usr/local/cuda-$CUDA_VERSION/bin:\$PATH" >> ~/.bashrc
echo "export LD_LIBRARY_PATH=/usr/local/cuda-$CUDA_VERSION/lib64:\$LD_LIBRARY_PATH" >> ~/.bashrc
source ~/.bashrc
sudo ldconfig
```
## Install cuDNN
Get latest version tarball https://developer.nvidia.com/cudnn-downloads

Or get specific version from https://developer.download.nvidia.com/compute/cudnn/redist/cudnn/linux-x86_64/

I choose 8.9.7.29_cuda11
```
wget -c https://developer.download.nvidia.com/compute/cudnn/redist/cudnn/linux-x86_64/cudnn-linux-x86_64-8.9.7.29_cuda11-archive.tar.xz -O cudnn.tar.xz 
tar -xvf cudnn.tar.xz
cd cudnn-*/
sudo cp -P include/cudnn.h /usr/local/cuda-11.8/include
sudo cp -P lib/libcudnn* /usr/local/cuda-11.8/lib64/
sudo chmod a+r /usr/local/cuda-11.8/lib64/libcudnn*
```

* Check cuda

```
nvidia-smi
nvcc -V
```


https://gist.github.com/Apkawa/2e1cbeced22135b2a8bad9d230f4e70c


# Install A1111

## Pull source code

1. `git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui`
2. `cd stable-diffusion-webui`
3. `git checkout v1.8.0`

## Prepare venv

* Init venv \
  `python3 -m venv ./venv`

* Enter venv
  `source ./venv/bin/activate`
* install 'pip install accelerate`

### Install pytorch and xformers

for a1111==1.8.0 support pytorch version 2.1.2

* get specific version from https://pytorch.org/get-started/previous-versions/
```
pip install torch==2.1.2 torchvision==0.16.2 torchaudio==2.1.2 xformers --index-url https://download.pytorch.org/whl/cu118
```

* check installed xformers version `pip show xformers` and get version
* enable xformers, add to `webui-user.sh` after `COMMANDLINE_ARGS=`
```
XFORMERS_PACKAGE='xformers==0.0.23.post1+cu118'
export  COMMANDLINE_ARGS="$COMMANDLINE_ARGS  --xformers"
```


# FAQ:
Q: nvidia-smi `NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver`\
A: Try reboot. Also, for hybrid video check https://wiki.debian.org/NVIDIA%20Optimus or https://wiki.ubuntu.com/Bumblebee manuals

Q: `RuntimeError: "LayerNormKernelImpl" not implemented for 'Half'`\
A: Edit `webui-user.sh`, uncomment and add to `COMMANDLINE_ARGS`, like:
`export COMMANDLINE_ARGS="--precision full --no-half"`

Q: `AssertionError: Torch is not able to use GPU; add --skip-torch-cuda-test to COMMANDLINE_ARGS variable to disable this check`\
A: `export COMMANDLINE_ARGS="--skip-torch-cuda-test"`

Q: Fail for 6Gb Nvidia videocard \
A: `export COMMANDLINE_ARGS="--medvram"`

Q: How to run as server \
A: `export COMMANDLINE_ARGS="--listen --enable-insecure-extension-access"`

Q: Huge memory leaks \
A: Install `tcmalloc`.  for ubuntu - `apt install libtcmalloc-minimal4`. See https://github.com/AUTOMATIC1111/stable-diffusion-webui/discussions/6722

Q: `./webui.sh: line 292: 18311 Segmentation fault (core dumped)` after load model \
A: Check a1111 supported torch version, pin torch version https://pytorch.org/get-started/previous-versions/

https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Command-Line-Arguments-and-Settings