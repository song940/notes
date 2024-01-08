---
layout: default
title: OpenWRT
---

# OpenWRT

OpenWRT is a open source Linux distribution.

## Package Manager

opkg is a package manager for OpenWRT.

```shell
~$ opkg update
```

## Expanding the filesystem

```shell
~$ opkg update
~$ opkg install fdisk resize2fs
```

```shell
~$ fdisk /dev/mmcblk0
```

1. Press `p` to print out the partition table, 记下分区的起始扇区号
2. Press `d` to delete the main partition
3. Press `n` to re-create partition, 起始扇区填写前面打印的起始扇区号，会提示检测到 `ext4` 签名，询问是否移除，选择 「No」。
4. Press `w` to write the partition table
5. Press `q` to quit

这样操作下来原有的分区结束为止就被修改为最大值了，保留分区签名 数据就不会丢失了，现在我们 `reboot` 重启，做 fsck 检查，修复 ext4 数据。

```shell
e2fsck -f /dev/mmcblk0p1
```

```shell
resize2fs /dev/mmcblk0p1
```

然后我们看下系统的磁盘容量

```shell
root at nanopi-r2s in ~
$ df -h
Filesystem                Size      Used Available Use% Mounted on
/dev/root                14.6G     76.3M     14.5G   1% /
tmpfs                   494.1M    100.0K    494.0M   0% /tmp
tmpfs                   512.0K         0    512.0K   0% /dev
```

至此，系统扩容工作已经完成了。

for more information, please refer to <https://openwrt.org/docs/guide-user/installation/installation_methods/sd_card>

## Firewall

*Firewall - Traffic Rules*

+ **Name**: *Allow HTTP*
+ **Protocol**: *TCP | UDP*
+ **Source zone**: *wan*
+ **Source address**: *-- add IP --*
+ **Source port**: *any*
+ **Destination zone**: *Device (input)*
+ **Destination address**: *-- add IP --*
+ **Destination port**: *8888*