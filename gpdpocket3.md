---
layout: default
title: GPD Pocket 3
---

# GPD Pocket 3

![](https://c1.iggcdn.com/indiegogo-media-prod-cld/image/upload/c_limit,w_695/v1634805061/l9clmahpo4mvxw8yc2bm.png)

+ https://wiki.archlinux.org/title/GPD_Pocket
+ https://wiki.archlinux.org/title/GPD_Pocket_3

## Install

系统安装过程参考：[Archlinux](./archlinux)

## Setup

### Screen

![](https://ae01.alicdn.com/kf/S77b97a97086b45dbaf3e15c24073e6b6K/GPD-Pocket-3-Memory-Hard-Disk-16GB-SSD-1TB-Handheld-Portable-Mini-Gaming-Laptop-CPU-Core.jpg)

The Pocket 3's display is designed for portrait devices and is rotated by 90 degrees counter-clockwise by default.  
GPD Pocket 3 的屏幕总成用的是平板电脑的库存屏幕，默认的固件是竖屏模式,可以通过下面的命令修改屏幕的模式。

```shell
~# xrandr --rotate right
```

可以添加到配置文件 `/etc/X11/xorg.conf.d/01-monitor.conf`

```patch
+ Section "Monitor"
+   Identifier "DSI-1"
+   Option "Rotate" "right"
+ EndSection
```

Note: The `Identifier` may be different depending on your display driver of choice (either `DSI-1` for modesetting or `DSI1` for xf86-video-intel)


#### Install intel video drivers

```shell
~# pacman -S xf86-video-intel
```

`/etc/X11/xorg.conf.d/20-intel.conf`

```
Section "Device" 
  Identifier  "Intel Graphics" 
  Driver      "intel" 
  Option      "AccelMethod"     "sna" 
  Option      "TearFree"        "true" 
  Option      "DRI"             "2" 
EndSection
```

安装后 `Identifier` 将 `/etc/X11/xorg.conf.d/01-monitor.conf` 中的 `DSI-1` 改为 `DSI1`

```patch
Section "Monitor"
-   Identifier "DSI-1"
+   Identifier "DSI1"
    Option "Rotate" "right"
EndSection
```

#### 屏幕缩放

由于屏幕分辨率较高，所以 UI 元素较小，需要调整 DPI 来缩放屏幕。

`~/.Xresources`

```
Xft.dpi: 144
```

如果需要支持多显示器可以设置一下：

```
Section "Monitor"
    Identifier  "DSI1"
    Option      "Rotate"        "right"
    Option      "Primary"       "true"
EndSection

Section "Monitor"
    Identifier  "HDMI1"
    Option      "LeftOf"        "DSI1"
    Option      "PreferredMode" "3840x2160"
    Option      "DPI"           "144x144"
EndSection
```

#### Backlight 屏幕背光控制

```shell
~$ pacman -S xorg-xbacklight
```

```shell
~$ xbacklight -set 80
```

### Touch Screen

Install `xf86-input-wacom`

`/etc/X11/xorg.conf.d/99-touchscreen.conf`

```
Section "InputClass"
  Identifier    "calibration"
  Driver        "wacom"
  MatchProduct  "GXTP7380"
  Option        "TransformationMatrix" "0 1 0 -1 0 1 0 0 1"
  Option        "Button2" "3"
EndSection
```

### Sound

```shell
~# pacman -S sof-firmware
```

## Sources Used in this Document

* [arch linux's GPD Pocket device wiki](https://wiki.archlinux.org/index.php/GPD_Pocket)
* [njkli's github repo](https://github.com/njkli/gpd-pocket)
* [nexus511's github repo](https://github.com/nexus511/gpd-ubuntu-packages)
* [cawilliamson's github repo](https://github.com/cawilliamson/ansible-gpdpocket)
* [gilbertw1's original arch linux setup guide](https://gist.github.com/gilbertw1/81ef4b0bcf3ddefa4b18)
* [GPD Pocket Arch Linux Full disk encryption](https://github.com/sigboe/GPD-ArchISO)
* [Arch Linux setup guide for the GPD Pocket](https://github.com/joshskidmore/gpd-pocket-arch-guide)
* <https://github.com/wimpysworld/umpc-ubuntu>
* <https://github.com/defencore/gpd-pocket-3-linux>
* <https://ubuntu-mate.org/download/gpd_pocket_3/>
* <https://www.reddit.com/r/GPDPocket/comments/s9ka7g/my_gpd_pocket_3_linux_setup/>
* [GPD Pocket 快速配置](https://plumz.me/archives/7331/)
* [GPD Pocket 的折腾日记——安装Arch](https://www.jianshu.com/p/aa72af0e4c44)
* [运维掌机 GPD Pocket 3 机房体验实测，做运维的馋哭了。UMPC、掌上电脑](https://post.smzdm.com/p/aevgm75q)
