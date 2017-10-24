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
In Terminal, `nvidia-smi' to test whether you have installed Nividia Driver Successfully.`   
##### Install CUDA  
```apt-get update
dpkg -i CUDA-***-8.0.deb
apt-get update
apt-get install cuda```  
set PATH, `vim ~/.bashrc'  
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

# Clone Sources 
`git clone https://github.com/BVLC/caffe.git`  
# Compile  
`cd ./caffe-master'  

