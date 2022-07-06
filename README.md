# Jetson Nano
In this branch, we will be using the Jetson Nano as our development platform.


## Installation (Headless mode) (Windows)
To setup the Jetson Nano in headless mode, we will need the following:
1. A microSD card
2. A micro-USB cable
3. Ethernet connection
4. Power supply
5. Jumpers

Quick format the miroSD card using [SD Memory Card Formatter for Windows](https://www.sdcard.org/downloads/formatter_4/eula_windows/) (Leave the volume label empty)

Download and install [Etcher](https://www.balena.io/etcher) and flash the [Jetson Nano Developer Kit SD Card Image](https://developer.nvidia.com/jetson-nano-sd-card-image) into the microSD card (we used 4.6.1 version)

Insert microSD card into Jetson and jumper the J48 pins and connect a DC power supply to J25 power jack. Connect the ethernet cable from Jetson to your router and also connect the micro-USB cable from Jetson to your computer. Allow Jetson to boot up.

Check Device Manager and see which Port it is connected to.

Use Putty to connect to the Jetson Nano using serial connection with a baudrate of 115200.

Configure the initial OS setups and choose eth0 for internet setup so that the router assigns an IP address to the Jetson Nano. Use `ifconfig` to check the IP address.

You can now disconnect the micro-USB cable from the Jetson Nano and use the IP address to start a new session with Putty.

You can also install a lightweight Desktop on Jetson and connect to it with Remote Desktop Connection.

`sudo apt-get install xrdp` on Jetson Nano.

Then, you can connect to the Jetson Nano with Remote Desktop Connection.

You may need a VPN connection to install updates from nvidia (I used a Cisco Anyconnect VPN).

## CUDA Installation
Confirm that the Nvidia CUDA Compiler (nvcc) is installed and the correct path is sourced. The JetPack comes preinstalled with the compiler. Add the appropriate paths to the compiler in the bash file to run the compiler via the command line. The output should mention the current version of the compiler.
```
// Open the ~/.bashrc file
~$ sudo gedit ~/.bashrc
// Append these two lines to the file
export PATH=${PATH}:/usr/local/cuda/bin
export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/cuda/lib64
// Source the file
~$ source ~/.bashrc
// Confirm the compiler version
~$ nvcc --version
```
The output of `nvcc --version` is:
```
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2021 NVIDIA Corporation
Built on Sun_Feb_28_22:34:44_PST_2021
Cuda compilation tools, release 10.2, V10.2.300
Build cuda_10.2_r440.TC440_70.29663091_0
```
## OpenCL Installation
Follow the instructions on [Build and Install OpenCL on Jetson Nano](https://yunusmuhammad007.medium.com/build-and-install-opencl-on-jetson-nano-10bf4a7f0e65) to build PoCL 1.7 with CUDA backend enable on Jetson Nano.