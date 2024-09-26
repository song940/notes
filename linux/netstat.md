---
layout: default
title: netstat
parent: Linux
---

# netstat

netstat is a network utility for Unix-like operating systems such as Linux, macOS, and Windows.

```shell
netstat -nr
```

## Statistics

All connections on port 80 

```shell
$ netstat -anp | grep :80
```

Netstat Help
```shell
$ netstat -h
```

## Listening

| Option | Example |
| :--- | :--- |
| `netstat -ltunp` | All Listening ports |
| `netstat -ltn` | Listening TCP ports |
| `netstat -lun` | Listening UDP ports |
| `netstat -lx` | Listening Unix ports |

## Connections

| Option | Example |
| :--- | :--- |
| `netstat -a` | All connections |
| `netstat -at` | All TCP connections |
| `netstat -au` | All UDP connections |

## Statistics

| Option | Example |
| :--- | :--- |
| `netstat -s` | Display statistics |
| `netstat -st` | Display TCP statistics |
| `netstat -su` | Display UDP statistics |

## Networks

| Option | Example |
| :--- | :--- |
| `netstat -i` | Show network interfaces |
| `netstat -ie` | Show network interfaces extended info |

## Routing

| Option | Example |
| :--- | :--- |
| `netstat -r` | Show routing table |
| `netstat -rn` | Show routing table, don't resolve hosts |

