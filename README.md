# Instruction for installing [fast.ai](https://www.fast.ai) on Raspberry Pi 4

- ### Clone this repo to home directory
- Set up swap file
```
chmod +x setup_swapfile.sh && ./setup_swapfile.sh
```
- Install prerequisites
```
sudo apt install libopenblas-dev libblas-dev m4 cmake cython python3-dev python3-yaml python3-setuptools
```
- Install pytorch
  * Method 1: Build from source (This process may take several hours but will work for any ARM boards)
    - Clone pytorch repo
      ```
      mkdir pytorch_install && cd pytorch_install
      git clone --recursive https://github.com/pytorch/pytorch
      cd pytorch
      git checkout v1.0.1
      git submodule update --init
      git submodule update --remote third_party/protobuf
      ```
    - Set environment variables (RPI dose not support CUDA amd MKLDNN)
      ```
      export NO_CUDA=1
      export NO_DISTRIBUTED=1
      export NO_MKLDNN=1 
      export NO_NNPACK=1
      export NO_QNNPACK=1
      ```
    - Complie
      ```
      python3 setup.py build
      ```
    - Install pytorch
      ```
      sudo -E python3 setup.py install
      ```
  * Method 2: download pytorch wheel from this repo (may only work for Raspberry pi 4)
    ```
    mkdir pytorch
    cd pytorch
    mv /home/torch-1.0.0a0+8322165-cp37-cp37m-linux_armv7l.whl /home/pytorch/torch-1.0.0a0+8322165-cp37-cp37m-linux_armv7l.whl
    sudo pip3 install ./torch-1.0.0a0+8322165-cp37-cp37m-linux_armv7l.whl
    ```
      
