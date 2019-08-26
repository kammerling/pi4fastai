# Instruction for installing [fast.ai](https://www.fast.ai) on Raspberry Pi 4

- Clone this repo to home directory
- Set up swap file
```
chmod +x setup_swapfile.sh && ./setup_swapfile.sh
```
- Install prerequisites
```
sudo apt install libopenblas-dev libblas-dev m4 cmake cython python3-dev python3-yaml python3-setuptools
```
- Install pytorch
