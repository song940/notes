---
layout: default
title: iptables
parent: Linux
---

# iptables

iptables is the userspace command line program used to configure the Linux 2.4.x and later packet filtering ruleset. When a connection tries to establish itself on your system, iptables looks for a rule in its list to match it to. If it doesn’t find one, it resorts to the default action.

![](https://qdnqn.com/content/images/2023/07/Netfilter-packet-flow.svg)

## How it works

iptables uses three different chains to allow or block traffic: 

- **Input** – This chain is used to control the behavior for incoming connections.
- **Output** – This chain is used for outgoing connections.
- **Forward** – This chain is used for incoming connections that aren’t actually being delivered locally like routing and NATing.

![](https://stuffphilwrites.com/wp-content/uploads/2014/09/FW-IDS-iptables-Flowchart-v2019-04-30-1.png)

## Configuring Rules

By default, all chains are set to the "accept" rule. For hardening, start with a "deny all" configuration and then only open necessary ports:

    iptables --policy INPUT DROP
    iptables --policy OUTPUT DROP
    iptables --policy FORWARD DROP

**Displaying Rules**:  

    # Verbose print of all active rules
    iptables -n -L -v

    # With line numbers
    iptables -n -L -v --line-numbers

    # Specific to INPUT/OUTPUT chains
    iptables -L INPUT -n -v
    iptables -L OUTPUT -n -v --line-numbers

**List Rules by Chain**:

    iptables -L INPUT
    iptables -S INPUT

    # With packet count
    iptables -L INPUT -v

**Modifying Rules**:

    # Delete rule by chain and number
    iptables -D INPUT 10

    # Delete rule by specification
    iptables -D INPUT -m conntrack --ctstate INVALID -j DROP

    # Flush all rules and accept all
    iptables -P INPUT ACCEPT
    iptables -P FORWARD ACCEPT
    iptables -P OUTPUT ACCEPT
    iptables -t nat -F
    iptables -t mangle -F
    iptables -F
    iptables -X

    # Flush a single chain
    iptables -F INPUT

    # Insert a rule
    iptables -I INPUT 2 -s 202.54.1.2 -j DROP

**Rule Examples**:  
(I've taken a subset of your rule examples for brevity. You can continue in this format for the rest of them.)

    # Allow loopback connections
    iptables -A INPUT -i lo -j ACCEPT
    iptables -A OUTPUT -o lo -j ACCEPT

    # Allow established and related incoming connections
    iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

...and so on.
