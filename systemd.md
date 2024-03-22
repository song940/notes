---
layout: default
parent: Linux
title: systemd
---

# Systemd

Systemd is a system and service manager for Unix-like operating systems.
`systemd` 是大多数现代 Linux 发行版使用的初始化系统和系统管理守护程序。它负责初始化系统组件和服务，管理系统运行过程中的服务，以及在系统启动时按照依赖关系顺序启动服务。

## Quick Start

```shell
systemctl start <service>
systemctl stop <service>
systemctl restart <service>
systemctl status <service>
```

## Targets

在 `systemd` 中，启动目标（targets）类似于传统 `init` 系统中的运行级别（runlevels），但提供了更灵活的依赖关系和更细粒度的控制。启动目标是一组服务和其他单位（units）的集合，这些服务和单位共同定义了系统的一个特定状态或模式。每个目标都可以依赖于其他目标或服务，`systemd` 会确保在进入目标之前启动所有必需的依赖项。

了解 `systemd` 的启动目标对于管理 Linux 系统的启动行为和服务是非常重要的。通过合理设置启动目标，你可以控制系统启动时加载哪些服务，以及系统应该进入的运行状态。对于大多数桌面用户来说，`graphical.target` 提供了一个方便的方式来确保系统启动直接进入图形界面。

### 图形目标（graphical.target）

`graphical.target` 是 `systemd` 管理的一个特殊目标，它代表了系统的图形界面状态。当系统设置为在启动时达到这个目标时，`systemd` 会启动所有必需的服务来启动图形用户界面（GUI），包括显示管理器（如 LightDM）、桌面环境（如 GNOME、KDE、XFCE 等）和其他图形界面相关的服务。

### 为什么要使用图形目标

使用 `graphical.target` 作为默认启动目标的主要原因是，大多数桌面用户需要图形界面来进行日常工作。设置 `graphical.target` 为默认目标，确保用户在开机后直接进入图形登录界面，无需手动启动图形环境。

### 如何查看和设置默认启动目标

- **查看当前默认目标**：

  ```bash
  systemctl get-default
  ```

  这个命令会显示当前系统的默认启动目标。

- **设置默认启动目标**：

  如果你想改变默认启动目标到图形界面，可以使用：

  ```bash
  systemctl set-default graphical.target
  ```

  相反，如果你出于某种原因需要系统默认启动到命令行界面，可以设置为 `multi-user.target`：

  ```bash
  systemctl set-default multi-user.target
  ```


## Systemd Logs

```shell
journalctl -u <service>
```

## Systemd Analyze

```shell
systemd-analyze critical-chain
```
