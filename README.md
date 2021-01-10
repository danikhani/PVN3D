# PVN3D with conda
This is only a test and no garantie that this instruction will actually work. I have tried the similar thing on a ubuntu 18.04 machine with cuda 10.2 installed.

## Installation
You need to have NVIDIA driver version 440 installed.

 We need **two conda envoirment** for this to work:
* First conda env: In this we compile the build
* Second conda env: In this we actually use the build

cloning the conda branch from git:
  ```shell
  git clone -b torch-1.5_conda https://github.com/danikhani/PVN3D.git
  ```
Installing Tkinter dependencies:
  ```shell
  sudo apt install python3-tk
  sudo apt install libpcl-dev libvtk6-dev
  ```
### 1) Conda env for compiling:
 * making the env and installing the pacakges:
  ```shell
  # create the env
  conda create -n PVN3D_compile python=3.6
  # go into the env to install the packages
  conda activate PVN3D_compile
  cd PVN3D
  # In order to compile the cython packages, cython and numpy need to be installed in home directory
  pip3 install Cython numpy --user
  # install the rest of packages
  pip install -r requirement_compile.txt
  ```
  * Install python-pcl. For Ubtuntu 18.04 from source:
  ```shell
  # you should be in PVN3D folder and use following:
  # clone fork with fix for Ubuntu 18.04
  git clone https://github.com/Tuebel/python-pcl
  cd python-pcl
  python3 setup.py install
  ```
  * Install PointNet++ (refer from Pointnet2_PyTorch): 
  ```shell
  # you should be in PVN3D folder and use following:
  cd ..
  # clone and install
  git clone https://github.com/erikwijmans/Pointnet2_PyTorch
  cd Pointnet2_PyTorch
  pip3 install -r requirements.txt
  # this is the compile file in PVN3D/setup.py
  cd ..
  python3 setup.py build_ext
  ```

### 2) Conda env for running the code:
  * making the env and installing the pacakges:
  ```shell
  # create the env
  conda create -n PVN3D_run python=3.6
  # go into the env to install the packages
  conda activate PVN3D_run
  # Install the pytorch and torchvision with cuda
  conda install pytorch==1.7.1 torchvision==0.8.2 cudatoolkit=10.2 -c pytorch
  # In order to compile the cython packages, cython and numpy need to be installed in home directory
  pip3 install Cython numpy --user
  # install the rest of packages
  pip install -r requirements_run.txt
  # install python-pcl requirements in the new env:
  cd python-pcl
  python3 setup.py install
  # install the PointNet++ requirements in the new env:
  cd Pointnet2_PyTorch
  pip3 install -r requirements.txt
  cd ..
  ```
If none of steps above gave back error, then you are good to go and can enjoy [PVNET](https://github.com/ethnhe/PVN3D).
