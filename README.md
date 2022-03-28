# Nerds
Welcome!

## New Stuff

### hcxdumptool

```
hcxdumptool -o capture.pcapng -i [interface] --enable_status=1
```

Hcxdumptool uses PMKID stuff to avoid needing the 4 way handshake for capturing PWs

https://hashcat.net/forum/thread-7717.html

### hcxpcapngtool

```
hcxpcapngtool -o capture_hash.txt [capture file]
```

```
hashcat -m 22000 [captured hash] -a3 ?l?l?l?l?l?l?l?l
```

## Hashcat Benchmarks

So far I've ran these benchmarks on the following GPUs
### WPA2 Benchmark
#### `hashcat -m 2500 -b` (Hashmode: 2500 - WPA-EAPOL-PBKDF2)

### GeForce GTX 1070, 7936/8117 MB, 16MCU
**210.4 kH/s** - (77.64ms) @ Accel:8 Loops: 512 Thr:1024 Vec:1

### NVIDIA RTX A3000 Laptop GPU, 5832/5946 MB, 32MCU
**394.0 kH/s** - (82.99ms) @ Accel:32 Loops:128 Thr:1024 Vec:1

### NVIDIA GeForce RTX 3080, 9538/10015 MB, 68MCU
**912.8 kH/s** - (76.13ms) @ Accel:32 Loops:128 Thr:1024 Vec:1

# Hashcat Driver Stuff

NVIDIA-SMI and the NVIDIA Cuda Toolkit seem to be required to successfully use Hashcat with NVIDIA GPUs. SMI (System Management Interface) is used for monitoring NVIDIA GPUs (I assume for features Hashcat has like watching the GPU Temps in order to shut it off if it gets too hot), while the CUDA Toolkit is what actually enables Hashcat to interface with the GPU to do the cracking.

## How to enable OpenCL on Kali Linux (Debian, Linux Mint, Ubuntu) for hashcat

So after much headache, it appears that the newest version of Parrot doesn't support the newest version of NVIDIA Driver. The Driver was compiled with a newer compiler version than Parrot has, or some such thing. The easiest way I got it working was the following: 

Install Parrot 4.10

Boot into headless mode (add the 3 at the end of the linux boot line)

Install Linux NVIDIA Driver 470.103.01 via CLI ( this is important because if you have the GUI running the Driver has issues installing )

Install Linux NVIDIA Cuda Toolkit ( Comes with newest NVIDIA Driver, do NOT install the driver )

## Enabling OpenCL for NVIDIA

Start with a full system upgrade and then reboot:
```
sudo apt update && sudo apt full-upgrade -y
reboot
```

After we updated the system, we need to check the nouveau kernel modules (Open Source Nvidia drivers that will conflict with NVIDIA Official Drivers)

```
lsmod | grep -i nouveau
```

If the previous command outputs something, for example:
```
nouveau 1499136 1
mxm_wmi 16384 1 nouveau
wmi 16384 2 mxm_wmi,nouveau
video 40960 1 nouveau
```
this means that nouveau is in use. Therefore, you must add them to the blacklist:

```
echo -e "blacklist nouveau\noptions nouveau modeset=0\nalias nouveau off" | sudo tee /etc/modprobe.d/blacklist-nouveau.conf
```

After changing the kernel parameters, we need to update our initramfs and reboot.
```
update-initramfs -u && reboot
```

After rebooting and verifying that the nouveau modules are not loaded, we proceed to install the OpenCL ICD bootloader, drivers, and the CUDA toolkit.
```
sudo apt install -y ocl-icd-libopencl1 nvidia-driver nvidia-cuda-toolkit
```
During driver installation, the system creates new kernel modules, so another reboot is required.

## Checking installed drivers

Now our system should be ready, we need to check that the drivers are loaded correctly. We can quickly verify this by running the nvidia-smi tool.
```
nvidia-smi
```

The output shows that our driver and GPU are fine – we can proceed to crack passwords. Before continuing, let's check again and make sure hashcat and CUDA work together.
```
hashcat -I
```

# More Reading

[NVIDIA-SMI](https://developer.nvidia.com/nvidia-system-management-interface)

[NVIDIA Cuda Toolkit](https://developer.nvidia.com/cuda-toolkit)

Most of the info about driver stuff was stolen (and lovingly modified) [from this post](https://miloserdov.org/?p=4726)
