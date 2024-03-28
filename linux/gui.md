---
layout: default
title: X Window System
parent: Linux
nav_order: 3
---

## X Window System

X 是 Linux 中负责渲染图形界面的广义概念，
X11 是一种 C/S 架构的协议，
X Server 通过 framebuffer 与显卡打交道用来渲染图形，
X Client 用来与 X Server 通信，[Xorg](https://wiki.archlinux.org/index.php/Xorg) 是它的其中一种主流实现，
[Wayland](https://wayland.freedesktop.org) 是另一种比较新的实现。
X 提供了基础的框架，例如渲染和设备输入事件的处理等，但不直接处理窗口管理、提供用户界面等。
窗口上面的标题栏、最大最小化、关闭按钮等修饰是窗口管理器负责绘制的，窗口中的内容是 DE 桌面环境实现的。

### Display Manager

DM：[Display Manager](https://wiki.archlinux.org/title/display_manager)，显示管理器，是 X Window System 的一部分，它启动图形用户界面并管理用户登录。

常见的显示管理器有 

+ GDM（GNOME Display Manager）
+ KDM（KDE Display Manager）
+ [LightDM](lightdm)

### Desktop Environment

DE：Desktop Environment，桌面环境，提供了一个完整的图形用户界面框架。桌面环境包括窗口管理器、面板、桌面图标、文件管理器、工具集（如 GTK+ 和 Qt）等。

常见的桌面环境有 

+ KDE
+ LXDE
+ [Xfce](https://wiki.archlinux.org/index.php/Xfce)
+ [Gnome](https://wiki.archlinux.org/index.php/Gnome)

### Window Manager

WM：Window Manager，窗口管理器，是 X Window System 的一部分，负责管理窗口的布局和外观。窗口管理器控制如何移动、调整大小、隐藏或显示应用程序窗口。

常见的窗口管理器有 

+ Metacity
+ KWin
+ Openbox
+ xmonad
+ [i3wm](i3wm)
+ [bspwm](bspwm)
