# Caffe Compile Tutorial  
##### Author: Nick Zhou  
Environment: Ubuntu16.04  Nvidia GTX 1050  
# Dependencies  
### General Dependencies
`sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler`  
`sudo apt-get install --no-install-recommends libboost-all-dev`
### CUDA  
##### Graphics Card Driver
```
blacklist nouveau
blacklist vga16fb
blacklist rivafb
blacklist rivatv
blacklist nvidiafb
```
`sudo apt-get  -purge remove nvidia-*`  
Restart. And press `Ctrl + Alt + F1`  
`sudo /etc/init.d/lightdm  stop`   
Run Nvidia Driver  
`sudo sh NVIDIA-LINUX-X86_64-361.**.run -k $(uname -r)`  
In Terminal, `nvidia-smi` to test whether you have installed Nividia Driver Successfully.`   
##### Install CUDA  
```
apt-get update
dpkg -i CUDA-***-8.0.deb
apt-get update
apt-get install cuda
```  
set PATH, `vim ~/.bashrc`  
```
export CUDA_HOME=/usr/local/cuda-8.0
export LD_LIBRARY_PATH=${CUDA_HOME}/lib64
PATH=${CUDA_HOME}/bin:${PATH}
export PATH
```
Restart XServer  
```
sudo /etc/init.d/lightdm  start
```
In Terminal, `sudo /etc/init.d/lightdm  start`    
PRIME Profiles -- Select the GPU you would like to use *NVIDIA*   
And then install CUDA as the offical instructions.  
### BLAS  
`sudo apt-get install libatlas-base-dev`  
or ` sudo apt-get install libopenblas-dev` or `MKL` (1 for 3)  
### Python  
`sudo apt-get install the python-dev`  
### CUDNN  
Download from https://developer.nvidia.com/cudn  
choose proper version  (8.0 recommended)
`sudo tar -zxvf ./cudnn-8.0-linux-x64-v5.1.tgz`   
cd its directory
```
cd cuda/include  
sudo cp cudnn.h /usr/local/cuda/include
cd ..  
cd lib64
sudo cp lib* /usr/local/cuda/lib64/   
cd /usr/local/cuda/lib64/
sudo rm -rf libcudnn.so libcudnn.so.5  
sudo ln -s libcudnn.so.5.0.5 libcudnn.so.5  
sudo ln -s libcudnn.so.5 libcudnn.so   
```
# Clone Sources 
`git clone https://github.com/BVLC/caffe.git`  
# Compile  
`cd ./caffe-master`  
`cp Makefile.config.example ./Makefile.cofig`  
`vim Makefile.config`  
Canel Comment for following lines:  
`USE_CUDNN := 1`  
`WITH_PYTHON_LAYER := 1`  
And you should adjust the *python* include/lib path (advise you to use the system python2.7)   
Then you should adjust the *CUDA* path  
In Makefile.config  
change  
`INCLUDE_DIRS:=$(PYTHON_INCLUDE) /usr/local/include`   
to  
`INCLUDE_DIRS:=$(PYTHON_INCLUDE) /usr/local/include/usr/include/hdf5/serial/`  
In Makefile  
change  
`LIBRARIES +=glog gflags protobuf boost_system boost_filesystem m hdf5_hl hdf5`  
to  
`LIBRARIES +=glog gflags protobuf boost_system boost_filesystem m hdf5_serial_hl hdf5_serial`  
`sudo make -j4`    
(**sudo** is necessary)  This procedure takes a while.  
`sudo make pycaffe -j4`   






