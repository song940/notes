---
layout: default
title: ssh
parent: Linux
---

# SSH

## Getting started

ssh is a network client and server program for Unix-like operating systems such as Linux, macOS, and Windows.

### Connecting

Connect to a server (default port 22)

```shell
$ ssh root@192.168.1.5
```

Connect on a specific port

```shell
$ ssh root@192.168.1.5 -p 6222
```

Connect via pem file (0400 permissions)

```shell
$ ssh -i /path/file.pem root@192.168.1.5
```

See: [SSH Permissions](chmod/#ssh-permissions)

### Executing

Executes remote command

```shell
$ ssh root@192.168.1.5 'ls -l'
```

Invoke a local script

```shell
$ ssh root@192.168.1.5 bash < script.sh
```

Compresses and downloads from a server

```shell
$ ssh root@192.168.1.5 "tar cvzf - ~/source" > output.tgz
```

### SCP

Copies from remote to local

```shell
$ scp user@server:/dir/file.ext dest/
```

Copies between two servers

```shell
$ scp user@server:/file user@server:/dir
```

Copies from local to remote

```shell
$ scp dest/file.ext user@server:/dir
```

Copies a whole folder

```shell
$ scp -r user@server:/dir dest/
```

Copies all files from a folder

```shell
$ scp user@server:/dir/* dest/
```

Copies from a server folder to the current folder

```shell
$ scp user@server:/dir/* .
```

### Config location

| File Path                | Description          |
| ------------------------ | -------------------- |
| `/etc/ssh/ssh_config`    | System-wide config   |
| `~/.ssh/config`          | User-specific config |
| `~/.ssh/id_{type}`       | Private key          |
| `~/.ssh/id_{type}.pub`   | Public key           |
| `~/.ssh/known_hosts`     | Logged in host       |
| `~/.ssh/authorized_keys` | Authorized login key |

### SCP Options

| Options       | Description                         |
| ------------- | ----------------------------------- |
| scp `-r`      | Recursively copy entire directories |
| scp `-C`      | Compresses data                     |
| scp `-v`      | Prints verbose info                 |
| scp `-P` 8080 | Uses a specific Port                |
| scp `-B`      | Batch mode _(Prevents password)_    |
| scp `-p`      | Preserves times and modes           |

### Config sample

```
Host server1 
    HostName 192.168.1.5
    User root
    Port 22
    IdentityFile ~/.ssh/server1.key
```

Launch by alias

```shell
$ ssh server1
```

See: Full [Config Options](https://linux.die.net/man/5/ssh_config)

### ProxyJump

```shell
$ ssh -J proxy_host1 remote_host2
```

```shell
$ ssh -J user@proxy_host1 user@remote_host2
```

Multiple jumps

```shell
$ ssh -J user@proxy_host1:port1,user@proxy_host2:port2 user@remote_host3
```

### ssh-copy-id

```shell
$ ssh-copy-id user@server
```

Copy to alias server

```shell
$ ssh-copy-id server1
```

Copy specific key

```shell
$ ssh-copy-id -i ~/.ssh/id_rsa.pub user@server
```

## SSH keygen

### ssh-keygen

```shell
$ ssh-keygen -t rsa -b 4096 -C "your@mail.com"
```

| -    | -                              |
| ---- | ------------------------------ |
| `-t` | [Type](ssh.md#key-type) of key |
| `-b` | The number of bits in the key  |
| `-C` | Provides a new comment         |

Generate an RSA 4096 bit key with email as a comment

### Generate

Generate a key interactively

```shell
$ ssh-keygen
```

Specify filename

```shell
$ ssh-keygen -f ~/.ssh/filename
```

Generate public key from private key

```shell
$ ssh-keygen -y -f private.key > public.pub
```

Change comment

```shell
$ ssh-keygen -c -f ~/.ssh/id_rsa
```

Change private key passphrase

```shell
$ ssh-keygen -p -f ~/.ssh/id_rsa
```

### Key type

* rsa
* ed25519
* dsa
* ecdsa

### known_hosts

Search from known_hosts

```shell
$ ssh-keygen -F <ip/hostname>
```

Remove from known_hosts

```shell
$ ssh-keygen -R <ip/hostname>
```

### Key format

* PEM
* PKCS8

## See also

* [OpenSSH Config File Examples](https://www.cyberciti.biz/faq/create-ssh-config-file-on-linux-unix/) _(cyberciti.biz)_
* [ssh_config](https://linux.die.net/man/5/ssh_config) _(linux.die.net)_
