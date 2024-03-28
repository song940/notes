---
layout: default
title: Rclone
---

# Rclone

rclone is a file synchronisation tool for the cloud.

https://rclone.org

## config

```shell
rclone config
rclone authorize "google photos"
```

## google photos

```shell
rclone lsd gphotos:
rclone ls gphotos:media/all
```

## sync vs copy

+ *rclone copy* - Copy files from source to dest, skipping already copied
+ *rclone sync* - Make source and dest identical, modifying destination only.

```shell
rclone sync -v --ptogress gphotos:media/all /data/google-photos
```