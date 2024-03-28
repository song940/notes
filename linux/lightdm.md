---
layout: default
title: LightDM
parent: Linux
---

# LightDM

LightDM is a lightweight display manager.

## Install

```shell
apt install lightdm
```

## Configuration

```shell
lightdm --show-config
```

默认登录界面用户名输入框，我们可以修改配置将其改为用户下拉选择框：

`/usr/share/lightdm/lightdm.conf.d/01_debian.conf`

```patch
# Debian specific defaults
#
# - use lightdm-greeter session greeter, points to the etc-alternatives managed
# greeter
# - hide users list by default, we don't want to expose them
# - use Debian specific session wrapper, to gain support for
# /etc/X11/Xsession.d scripts

[Seat:*]
greeter-session=lightdm-greeter
- greeter-hide-users=true
session-wrapper=/etc/X11/Xsession
```

### Autologin

`/etc/lightdm/lightdm.conf.d/autologin.conf`

```ini
[Seat:*]
autologin-user=<USERNAME>
autologin-user-timeout=10
```
