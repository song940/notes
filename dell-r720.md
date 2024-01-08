---
layout: default
title: DELL R720
---

# DELL PowerEdge R720

<img style="width:100%; max-width: 600px;" src="https://www.stalliontek.com/media/catalog/product/r/7/r720_8bay_3.5_1.jpg" />
<br />
<img style="width:100%; max-width: 600px;" src="https://cdn.bargainhardware.co.uk/media/product/c91/dell-poweredge-r720-xd-16x-sff-hot-swap-sas-psu-2u-barebones-server-829.jpg" />

+ CPU: Intel Xeon 2560
+ RAM: 64GB（24slot）
+ HDD: 12TB（3.5inch x 8Ray）
+ NIC: 4 * 1G + iDRAC
+ Power: 750W * 2

我们可以看到服务器的性能是比较强的，如果我们在服务器上安装操作系统那么我们可能就只有一种选择，为了能更好的发挥其作用我选择将其虚拟化，然后再使用上面的资源。

- [VMware Sphere](vmware)
    - [ESXi](vmware/esxi)
    - [vCenter](vmware/vcenter)
- [Proxmox PVE](pve)

如果你使用的是 戴尔、超微、惠普等公司的服务器，我建议你使用 [VMware](vmware)，因为通常有包含驱动的定制版本，稳定性会比较好，而一些非知名品牌的服务器或者干脆是自己组装的服务器 硬件比较特殊我建议使用 [Proxmox PVE](pve) 驱动会好解决一些。

## iDRAC

iDRAC is the Dell Integrated Dell Remote Access Controller.

- https://www.dell.com/support/kbdoc/en-us/000178115/idrac9-versions-and-release-notes
- https://www.dell.com/support/kbdoc/en-us/000135299/idrac7-idrac8-red007-error-when-applying-latest-idrac-firmware-from-out-of-band-interface

## Nvidia P40 GPU

![](https://www.elsa-jp.co.jp/wp-content/uploads/2019/03/nvidia_tesla_p40_3qtr_s.png)

<https://www.nvidia.com/content/dam/en-zz/Solutions/design-visualization/documents/nvidia-p40-datasheet.pdf>

有几个需要注意的地方：

1. *「New Virtual Machine」 -> 「Customize settings」-> 「Boot Options」* 将 Firmware 的模式从 *BIOS* 改到 ***UEFI***，否则在系统中无法识别到 GPU。
2. 在内存选项中选择 Memory - Check All guest memory (All locked)「预留所有内存」，否则会遇到 *Failed - Invalid memory setting: memory reservation (sched.mem.min) should be equal to memsize(16384).*
3. 在 VM Options 的 Advanced 中添加以下配置，否则会遇到 *Failed - Module 'DevicePowerOn' power on failed.*

![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/727f63e968ad40bc8859ae1f6e7154fb~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)
![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ed30afa6a3ea456698b62b6f0c3dda84~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)

```ini
hypervisor.cpuid.v0=FALSE
pciPassthru.use64bitMMIO=TRUE
pciPassthru.64bitMMIOSizeGB=64
```

```shell
apt-get update
apt install make gcc git
```

```shell
apt-get install linux-headers-generic
apt-get install linux-headers-$(uname -r)
```

<https://www.nvidia.com/Download/index.aspx>

```shell
wget https://us.download.nvidia.cn/tesla/515.105.01/NVIDIA-Linux-x86_64-515.105.01.run # CUDA 11
wget https://us.download.nvidia.cn/tesla/535.129.03/NVIDIA-Linux-x86_64-535.129.03.run # CUDA 10
chmod +x NVIDIA-Linux-x86_64-535.129.03.run
./NVIDIA-Linux-x86_64-535.129.03.run
```

**Nouveau kernel driver**

```shell
cat /etc/modprobe.d/blacklist-nvidia-nouveau.conf << EOF
blacklist nouveau
options nouveau modeset=0
EOF
```

<https://askubuntu.com/questions/841876/how-to-disable-nouveau-kernel-driver>

```shell
lspci | grep -i nvidia
```

### CUDA Toolkit

<https://developer.nvidia.com/cuda-downloads>

```shell
wget https://developer.download.nvidia.com/compute/cuda/12.3.1/local_installers/cuda_12.3.1_545.23.08_linux.run
./cuda_12.3.1_545.23.08_linux.run
```

安装完成后运行 `nvidia-smi` 检查是否安装成功 以及 CUDA 版本

## Refs

+ <https://juejin.cn/post/7248072694335799333>

### Q&A: NAS 还是服务器？

群晖是计算机、路由器是计算机、服务器也是，只是他们的用途不一样，所以在硬件配置方面的取舍会有区别。

如果你只是想上个网当然买个现成的路由器就行了，如果你想要搞一些复杂的网络配置，就需要自己搭建性能强劲的软路由系统。

同理，如果你只是想存个文件方便远程访问，群晖就够了。

但是如果你的需求会比较多，我想搭建 Kubernates(k8s)、VM 虚拟化、MediaServer 媒体服务器、Web Server、Database Server 或者你对性能和硬盘空间有要求，消费级的路由器或者 NAS 肯定不够用了，那么你需要服务器。