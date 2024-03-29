---
layout: default
title: HP Microserver Gen8
---

# HP Microserver Gen8

![](https://rabbit-note.com/wp-content/uploads/2019/08/MicroServerGen8.jpg)

+ CPU: Xeon E3 1230v2
+ RAM: 16G（2slot）
+ HDD: 4Ray
+ NIC: 2 * 1Gb + iLO
+ Power: 200W

## HP iLO

![](https://www.storagereview.com/wp-content/uploads/2019/05/StorageReview-HP-iLO.jpg)

Integrated Lights-Out, or iLO, is a proprietary embedded server management technology by Hewlett-Packard Enterprise which provides out-of-band management facilities. The physical connection is an Ethernet port that can be found on most ProLiant servers and microservers[1] of the 300 and above series.

iLO has similar functionality to the lights out management (LOM) technology offered by other vendors, for example, Sun/Oracle's LOM port, Dell DRAC, the IBM Remote Supervisor Adapter and Cisco CIMC.

<https://en.wikipedia.org/wiki/HP_Integrated_Lights-Out>

## 硬件升级

1. 更换 CPU
    HP Microserver Gen8 出厂自带的 CPU 是 Intel Celeron G1610T，性能比较弱，而且不支持 VT-d，所以我选择更换 CPU。
    我这里推荐 Intel Xeon E3 1230v2，性能比较强，而且支持 VT-d。

2. 添加内存
    HP Microserver Gen8 出厂自带的内存是 2G，我们添加到 16G ECC。

3. RAID 阵列卡
    HP Gen 8 内置的是软件阵列驱动器,而不是硬盘驱动器。能够支持的 RAID Level 比较有限，只有 RAID 0 和 RAID 1。
    VMWare ESXi 对 Gen8 的软 RAID 驱动性能非常有问题，需要将驱动降级到 ESXi6 才能使硬盘性能表现正常。
    我能找到最新的支持 Gen8 软 RAID 驱动的 ESXi 的版本就只到 ESXi7 了，而 ESXi8 已经不再支持了。
    所以换一个独立的阵列卡是很有必要的。

### HP Smart Array P420

![](https://i.ebayimg.com/images/g/eOoAAOSwUFBjx6FM/s-l1200.webp)

## 安装 [VMware ESXi](vmware/esxi)

### FAQ

***HP MicroServer Gen8, Solving performance issues with ESXi 6***

If you have installed to a newer version of ESXi on your Gen8 Micro Server and are now suffering from very low performance disk speed, try the following steps to downgrade to a former hpvsa-driver (scsi-hpvsa-5.5.0-88).
Just follow these simple steps:

Download the driver https://support.hpe.com/connect/s/softwaredetails?language=en_US&softwareId=MTX_dcfe1ad1b6ae442e8ed665c595

```shell
scp Downloads/scsi-hpvsa-5.5.0-88OEM.550.0.0.1331820.x86_64.vib root@192.168.88.2:/tmp
cp scsi-hpvsa-5.5.0-88OEM.550.0.0.1331820.x86_64.vib /var/log/vmware/
esxcli system maintenanceMode set --enable true
esxcli software vib remove -n scsi-hpvsa -f
esxcli software vib install -v file:scsi-hpvsa-5.5.0-88OEM.550.0.0.1331820.x86_64.vib --force --no-sig-check --maintenance-mode
```

Restart your ESXi, stop the maintenance mode, disable SSH connections and start VMs again Hope that helps for you as well.

+ https://seiler.it/solving-performance-issues-with-esxi-6-gen8/
+ http://h20564.www2.hpe.com/hpsc/swd/public/detail?swItemId=MTX_bfdbb1dfc5314e02bc01b1436b
+ https://kb.vmware.com/s/article/1017530
