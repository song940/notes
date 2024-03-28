---
layout: default
title: lsof
parent: Linux
---

# lsof

**lsof** meaning **L**i**s**t **O**pen **F**iles is used to find out which files are open by which process

## Basic


```shell
$ lsof 
$ sudo lsof -u root
```
### Port-specific

```shell
$ lsof -i :8080
$ lsof -i :80 -i :22
$ lsof -i TCP:22
$ lsof -i TCP:1-1024
$ lsof -i UDP
$ lsof -i @192.168.1.5
```

## Process-specific

```shell
$ lsof -c mysql 
$ lsof -c java 
$ lsof -c ssh 
$ lsof -c nginx 
$ lsof -c ssh -c httpd
```
### User-specific

```shell
$ lsof -u www-data
$ lsof -u www-data -u ubuntu
$ lsof -i -u ^root # Except certain user
```

## Network-specific

```shell
$ lsof -i 4 \# IPv4 only 
$ lsof -i 6 \# IPv6 only
```
### PID-specific
```shell
$ lsof -p 1753
$ lsof -p ^3  # Except certain pids
```

## Filename-specific

```shell
$ lsof /var/log/messages 
$ lsof /etc/passwd
```
### Directory-specific
```shell
$ lsof +D /var/log # Within a directory
```

## Kill

```shell
$ kill -9
$ lsof -t -u apache
$ kill -9 $(lsof -t -i :8080)
```