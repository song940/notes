---
layout: default
title: uConsole
---

# Clockwork Pi - uConsole

![](https://liliputing.com/wp-content/uploads/2023/07/uconsole.jpg)

Clockwork Pi uConsole 可以选择不同的核心板

+ CM4
+ A06
+ R01

## 

## Install

我选择的 CM4 版本有两个系统，分别是基于 LXDE 和 XFCE

+ <http://dl.clockworkpi.com/uConsole_CM4_v1.3g_64bit.img.7z>
+ <http://dl.clockworkpi.com/uConsole_CM4_v0.1b_xfce_64bit.img.7z>

我比较喜欢 XFCE 版本的，因为它比较简单。

下载好之后通过 `dd` 将其写入到 SD 卡中

```shell
dd if=uConsole_CM4_v0.1b_xfce_64bit.img of=/dev/mmcblk0 status=progress
```

插入 SD 卡后就可以启动 uConsole 了，首次启动需要一点时间。

进入 XFCE 界面后会有一个欢迎界面，提示我们默认 username: `cpi` password: `cpi`.

我们可以连接网络，然后开启 SSH 服务，然后通过 `ssh cpi@<uconsole_ip>` 进入命令行界面。

## Configuration

进入系统后先设置一下 RPI Configuration

更新软件源

```shell
apt update
apt upgrade -y
```

安装中文字体

```shell
apt install fonts-noto-cjk -y
```

接下来我们开始创建一个自己的用户:

```shell
adduser lsong
usermod -a lsong -G sudo # 添加到 sudoers，允许使用 sudo
```

uConsole OS 里面桌面是通过 `x11-autologin.service` 这个服务启动桌面的 (后面我会修正这个问题)，所以为了能够使用我们新建的用户启动桌面，我们需要修改 `x11-autologin.service` 的配置。

```patch
[Unit]
Description=X11 session for cpi
After=graphical.target systemd-user-sessions.service

[Service]
- User=cpi
+ User=lsong
WorkingDirectory=~

PAMName=login
Environment=XDG_SESSION_TYPE=x11
TTYPath=/dev/tty7
StandardInput=tty
UnsetEnvironment=TERM

UtmpIdentifier=tty7
UtmpMode=user

StandardOutput=journal
ExecStartPre=/usr/bin/chvt 7
ExecStart=/usr/bin/startx -- vt7 -keeptty -verbose 3
Restart=no

[Install]
WantedBy=graphical.target
```

重新启动系统后就会使用新创建的用户登录桌面了，但是我发现屏幕方向有问题。

## Screen

cpi 用户是通过在 `~/.xinitrc` 中 xrandr 设置的:

```shell
xrandr --output DSI-1 --rotate right
```

这种方式需要每个用户都修改一次。

我们创建一个配置文件 `/etc/X11/xorg.conf.d/01-monitor.conf`

```
Section "Monitor"
  Identifier "DSI-1"
  Option "Rotate" "right"
EndSection
```

这样就可以在 X11 层面设置屏幕方向了，对所有用户都生效，而无需单独配置。

/etc/X11/Xresources/x11-dpi

```
Xft: 144
```

## Keyboard

下载 uConsole 的 [Keyboard Flash Tool](https://github.com/clockworkpi/uConsole/raw/master/Bin/uconsole_keyboard_flash.tar.gz)

```shell
wget https://github.com/clockworkpi/uConsole/raw/master/Bin/uconsole_keyboard_flash.tar.gz
tar xzvf uconsole_keyboard_flash.tar.gz
```

然后安装 `dfu-util`

```shell
~# apt install dfu-util
```

下载 [Keyboard Firmware](https://github.com/clockworkpi/uConsole/tree/master/Bin)

```shell
wget https://github.com/clockworkpi/uConsole/blob/master/Bin/uconsole.kbd.0.4_48mhz.bin
```

升级 Keyboard 固件

```shell
./maple_upload ttyACM0 2 1EAF:0003 uconsole.kbd.0.4_48mhz.bin
```

按住 <kbd>Fn</kbd> 然后滚动轨迹球就可以翻页了。

## LightDM

前面我们说到 uConsole OS 里面桌面是通过 `x11-autologin.service` 这个服务启动桌面的，这里我们把它修改为 `lightdm`。

```shell
apt install lightdm -y
```

然后参考 [systemd#targets](../systemd#targets) 的部分来修改启动目标，设置为 `graphical.target` 图形启动目标：

```bash
systemctl set-default graphical.target
```

然后删除掉 `x11-autologin.service` ，重新启动就会启动到 lightdm 了。

详细参考 [lightdm](../linux/lightdm) 的部分。

## Battery

The default charging speed of the uConsole is way too slow. Run this to fixt hat:

```shell
echo 'KERNEL=="axp20x-battery", ATTR{constant_charge_current_max}="2200000", ATTR{constant_charge_current}="2000000"' | sudo tee /etc/udev/rules.d/99-uconsole-charging.rules
```

## Bluetooth

```shell
apt install blueman
```

## IME

```shell
apt install fcitx5 fcitx5-rime
```
