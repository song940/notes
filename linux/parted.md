---
layout: default
title: parted
parent: Linux
---

# parted

parted is a Linux disk partitioning tool

## List all available disks
```shell
parted --list
```

## Print partition layout of a specific disk
```shell
parted /dev/sdX print
```

## Start parted interactive mode for a specific disk
```shell
parted /dev/sdX
```

## Create a new GPT partition table
```shell
parted /dev/sdX mklabel gpt
```

## Create a new MBR partition table
```shell
parted /dev/sdX mklabel msdos
```

## Create a new partition
```shell
# Create a partition starting at 1GB and ending at 5GB
parted /dev/sdX mkpart primary 1GB 5GB
```

## Delete a partition
```shell
# Delete partition number 1
parted /dev/sdX rm 1
```

## Resize a partition
```shell
# Resize partition number 1 to end at 10GB
parted /dev/sdX resizepart 1 10GB
parted /dev/sdX resizepart 1 100%
```

## Set a partition as bootable
```shell
parted /dev/sdX set 1 boot on
```

## Check the disk for errors
```shell
parted /dev/sdX check 1
```

## Move a partition (Warning: Data loss possible)
```shell
# Move partition number 1 to start at 2GB
parted /dev/sdX move 1 2GB 4GB
```

## Quit parted
```shell
# When in interactive mode
(parted) quit
```

## Help in interactive mode
```shell
# When in interactive mode
(parted) help
```

## Other useful commands
```shell
# To align a partition optimally
parted /dev/sdX align-check optimal 1
```

Note: Replace `/dev/sdX` with your actual device name and adjust sizes as necessary.

## Important Notice

Always backup important data before performing disk operations. 
Use the 'print' command in parted to confirm your configurations before applying.
