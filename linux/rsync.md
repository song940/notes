---
layout: default
title: rsync
parent: Linux
---

# Rsync

## Rsync over SSH

### Copying a file from local to remote

```bash
rsync -avz -e ssh /path/to/local/file user@remotehost:/path/to/remote/file
```

### Copying a file from remote to local

```bash
rsync -avz -e ssh user@remotehost:/path/to/remote/file /path/to/local/file
```

### Exclude a Specific Directory

```shell
rsync -avz -e ssh --exclude 'dir1' --exclude 'dir2' user@remotehost:/path/to/remote/file /path/to/local/file
```