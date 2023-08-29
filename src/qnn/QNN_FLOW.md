## Setup Linux Build Environment

Launch Ubuntu 20.04 docker. This has been tested on a Linux host and a Mac host. 
```
docker run -it ubuntu:20.04 bash
```
Install Miniconda
```
apt update
apt install wget -y
wget -c https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
chmod +x Miniconda3-latest-Linux-x86_64.sh
./Miniconda3-latest-Linux-x86_64.sh
```

Activate conda and create a Python3.6 environment
```
bash
export PATH="/root/miniconda3/bin:$PATH"
conda init bash
bash
conda activate
conda create -n py36 python=3.6
conda activate py36
```

Some basic installs
```
apt update
apt install sudo
apt-get install python3-dev python3-matplotlib python3-numpy python3-protobuf python3-scipy python3-skimage python3-sphinx wget zip -y
```

Copy `build-sdk-snpe-2.10.0.4541.zip`[download here](https://amdcloud-my.sharepoint.com/:u:/g/personal/rradjabi_amd_com/ESXFsYjLySpIkNNKN13XCS0ByjipY-QHqNqt94VWlh_gWw?e=qdThxl) to container, extract, install dependencies
```
docker cp build-sdk-snpe-2.10.0.4541.zip <CONTAINER ID>:/root/
unzip sdk.zip
cd sdk/bin
chmod +x dependencies.sh
./dependencies.sh
source check_python_depends.sh
```

Output from `source check_python_depends.sh`
```
  (py36) root@c132adb960d3:~/snpe-2.10.0.4541/bin# source check_python_depends.sh
  Supported version of Python found: 3.6
  Checking for python3-numpy: install ok installed
  WARNING: It appears the python module numpy is installed on this system using the apt-get distribution as well as pip. If you encounter errors, please use only one distribution.
  ===========================================
  Checking for python-sphinx:
  sphinx installed via pip Version: 3.1.2
  ===========================================
  Checking for python3-scipy: install ok installed
  WARNING: It appears the python module scipy is installed on this system using the apt-get distribution as well as pip. If you encounter errors, please use only one distribution.
  ===========================================
  Checking for python3-matplotlib: install ok installed
  WARNING: It appears the python module matplotlib is installed on this system using the apt-get distribution as well as pip. If you encounter errors, please use only one distribution.
  ===========================================
  Checking for python3-skimage: install ok installed
  WARNING: It appears the python module scikit-image is installed on this system using the apt-get distribution as well as pip. If you encounter errors, please use only one distribution.
  ===========================================
  dpkg-query: no packages found matching python-protobuf
  Checking for python-protobuf:
  WARNING: Package(s) not found: protobuf
  ===========================================
  Checking for python3-yaml: install ok installed
  WARNING: It appears the python module pyyaml is installed on this system using the apt-get distribution as well as pip. If you encounter errors, please use only one distribution.
  ===========================================
  dpkg-query: no packages found matching python3-mako
  Checking for python3-mako:
  WARNING: Package(s) not found: mako
  ===========================================
```
NOTE: There are many WARNING messages, but it is okay to ignore these.

Setup for TensorFlow:
```
pip install --upgrade pip
pip install tensorflow
pip show tensorflow
```

Setup for PyTorch
```
pip install --upgrade pip
pip install torch==1.8.1
```

Setup for ONNX
```
pip install --upgrade pip
pip install onnx==1.11.0
pip install onnx-simplifier==0.4.10
pip install packaging
pip install pyyaml
```

## Build Model Binary on Linux

Source envsetup.sh
```
source snpe-xxxx/bin/envsetup.sh -o /root/miniconda3/envs/py36-onnx/lib/python3.6/site-packages
```

