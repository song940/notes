---
layout: default
title: VMware ESXi
parent: VMware
---

# VMware ESXi

VMware ESXi is the virtualization solution for enterprise environments.
VMWare ESXi 是 Type 1 虚拟化方案，区别于运行在操作系统之上的虚拟化方案，运行效率会高很多。

### VMware Compatibility Guide

+ https://ark.intel.com/content/www/us/en/ark/products/series/78580/intel-xeon-processor-e3-v2-family.html
+ https://ark.intel.com/content/www/us/en/ark/products/65732/intel-xeon-processor-e31230-v2-8m-cache-3-30-ghz.html
+ https://www.intel.com/content/www/us/en/products/sku/65732/intel-xeon-processor-e31230-v2-8m-cache-3-30-ghz/specifications.html
+ https://www.dell.com/support/home/en-us/drivers/driversdetails?driverid=0ghf4&oscode=ws8r2&productcode=poweredge-r720
+ https://www.vmware.com/resources/compatibility/detail.php?scat=cpu&productid=67&deviceCategory=server&details=1&cpuSeries=67&page=1&display_interval=10&sortColumn=Partner&sortOrder=Asc

### VMware ESX Command Line Interface

[ESXi CLI](https://developer.vmware.com/web/tool/7.0/esxcli) 可以用于在不方便使用 Web UI 的场景管理 ESXi 服务器。

https://developer.vmware.com/web/tool/7.0/esxcli

[Download esxcli](https://customerconnect.vmware.com/downloads/get-download?downloadGroup=ESXCLI-700&download=true&fileId=1651b84165c70f7a25b662368a71772c&uuId=47c5bf87-2470-431a-9055-91c243611868) 

### Upgrade

```sh
esxcli software sources profile list -d /vmfs/volumes/storage/VMware-VMvisor-Installer-8.0.0-205
13097.x86_64-Dell_Customized-A00.zip

esxcli software profile update -p DEL-ESXi_800.20513097-A00 -d /vmfs/volumes/storage/VMware-VMvisor-Instal
ler-8.0.0-20513097.x86_64-Dell_Customized-A00.zip
```

### VMware ESXi 与服务器硬件的集成

VMware ESXi 有专门针对服务器做优化的自定义镜像的版本

+ [Dell PowerEdge R720](../dell-r720)
+ [HP ProLiant MicroServer Gen8](../hp-gen8)

### FAQ

***Cannot change host configuration when create datastore***

在安装全新的硬盘后需要在启动时按下 「Ctrl-R」进入阵列卡设置，设置成 RAID-1 后，进入 VMware ESXi 中的 「Datastore」 时会遇到无法创建的情况，
原因是磁盘没有创建分区表，找到磁盘的 `naa.xxxx` 并记录，打开 SSH 输入以下创建分区表：

```sh
partedUtil setptbl /vmfs/devices/disks/naa.55cd2e41241cec36 msdos
```
