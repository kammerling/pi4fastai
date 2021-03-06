# Instruction for installing [fast.ai](https://www.fast.ai) on Raspberry Pi 4 
forked from prakash0228/pi4fastai

- #### Clone this repo to home directory
- #### Set up swap file
```
chmod +x setup_swapfile.sh && ./setup_swapfile.sh
```
- #### Install prerequisites
```
sudo apt install libopenblas-dev libblas-dev m4 cmake cython python3-dev python3-yaml python3-setuptools numpy
```
- #### Install pytorch
  * ##### Method 1: Build from source (This process may take several hours but will work for any ARM boards)
    - Clone pytorch repo
      ```
      mkdir pytorch_install && cd pytorch_install
      git clone --recursive https://github.com/pytorch/pytorch
      cd pytorch
      git checkout v1.1.0
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
  * ##### Method 2: download pytorch wheel from this repo (may only work for Raspberry pi 4)
    ```
    mkdir pytorch && cd pytorch
    mv /home/torch-1.0.0a0+8322165-cp37-cp37m-linux_armv7l.whl /home/pytorch/torch-1.0.0a0+8322165-cp37-cp37m-linux_armv7l.whl
    sudo pip3 install ./torch-1.0.0a0+8322165-cp37-cp37m-linux_armv7l.whl
    ```
- #### Verify pytorch installatiion
  ```
  cd 
  python3
  >>> from __future__ import print_function
  >>> import torch
  >>> a = torch.rand(5,3)
  >>> print (a)
  ```
  Output from about should look like 
  ```
  tensor([[0.3380, 0.3845, 0.3217],
       [0.8337, 0.9050, 0.2650],
       [0.2979, 0.7141, 0.9069],
       [0.1449, 0.1132, 0.1375],
       [0.4675, 0.3947, 0.1426]])
  ```
  Exit python
  ```
  exit()
  ```
- #### Install fastai and dependancies
  ```
  cd
  chmod +x fastai_rpi4.sh && ./fastai_rpi4.sh
  ```
  Above will print #### Done with part1 – now logout, login again and run setup_jupyter.sh
  Restart Pi

- #### Setup jupyter
  ```
  chmod +x setup_jupyter.sh && ./setup_jupyter.sh
  ```
- #### Verify jupyter install
  ```
  jupyter notebook
  ```
