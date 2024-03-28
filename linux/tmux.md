---
layout: default
title: tmux
parent: Linux
---

# tmux

tmux is a terminal multiplexer

### New session

Start a new session 
```shell
$ tmux
```

Start a new named session
```shell
$ tmux new -s myname
```

Show all sessions 
```shell
$ tmux ls
```

### Attach session
Attach to last session
```shell
$ tmux a
```

Attach to named 
```shell
$ tmux a -t myname
```

### Kill session
Kill a session by name
```shell
$ tmux kill-ses -t myname
```

Kill sessions but the current 
```shell
$ tmux kill-ses -a
```

Kill sessions but 'myname'
```shell
$ tmux kill-ses -a -t myname
```

### Tmux help


```shell
$ tmux info
```

### Config
Reload config

```shell
$ tmux source-file ~/.tmu­x.conf
```

Show config 
```shell
$ tmux show-options -g
```

### Copy Mode  

| Command             | Description                  |
|---------------------|------------------------------|
| `Ctrl+b` `[`        | Enter copy mode           |
| `<Space>`      | Start selection                         |
| `Enter`         | Copy selection                          |
| `q`                 | Quit copy mode               |
| `Ctrl+b` `]`        | Paste contents of buffer_0 |



Mainly works like selecting text in [Vim](/vim#motions)

## Tmux shortcuts 

### Getting started 

| Shortcuts           | Description                  |
|---------------------|------------------------------|
| `Ctrl+b` `?`        | List all shortcuts           |


Show every session, window, pane, etc.

```shell
$ tmux info
```

### Panes (Splits) 

| Shortcuts | Description |
| :--- | :--- |
| `Ctrl+b` `"` _/_ `%` | Split Horiz/Vert |
| `Ctrl+b` `!` | Pane -&gt; Window |
| `Ctrl+b` `x` | Kill pane |
| `Ctrl+b` | Navigate panes |
| `Ctrl+b` | Toggle layouts |
| `Ctrl+b` `{` _/_ `}` | Move to Left/Right |
| `Ctrl+b` `o` | Goto next panes |
| `Ctrl+b` `z` | toggle full-screen |
| `Ctrl+b` `;` | Toggle Last pane |
| `Ctrl+b` `q` | Show numbers |
| `Ctrl+b` `q` `0`...`9` | Goto \# pane |



### Window \(Tabs\) 

| - | - |
| :--- | :--- |
| `Ctrl+b` `c` | Create window |
| `Ctrl+b` `p` _/_ `n` | Previous/Next window |
| `Ctrl+b` `"` _/_ `%` | Split Horiz/Vert |
| `Ctrl+b` `w` | List window |
| `Ctrl+b` `,` | Rename window |
| `Ctrl+b` `f` | Find window |
| `Ctrl+b` `l` | Last window |
| `Ctrl+b` `.` | Move window |
| `Ctrl+b` `&` | Close window |
| `Ctrl+b` `0`...`9` | Goto \# window |



### Session \(Set of Windows\)

| - | - |
| :--- | :--- |
| `Ctrl+b` `d` | Detach from session |
| `Ctrl+b` `s` | Show all sessions |
| `Ctrl+b` `$` | Rename session |
| `Ctrl+b` `(` _/_ `)` | Previous/Next session |



## Command Mode 

### Usage 

| Command | Description |
| :--- | :--- |
| `Ctrl+b` `:` | Enter command mode |



### Resizing

| Command | Description |
| :--- | :--- |
| `resize-pane -D 20` | Resize down |
| `resize-pane -U 20` | Resize up |
| `resize-pane -L 20` | Resize left |
| `resize-pane -R 20` | Resize right |

### Listing

| Command | Description |
| :--- | :--- |
| `list-keys` | All commands |
| `list-panes` | All panes |
| `list-windows` | All Windows |

### Copying

| Command | Description |
| :--- | :--- |
| `list-buffers` | List all buffers |
| `show-buffer` | Show \#0 contents |
| `capture-pane` | Copy of pane |
| `choose-buffer` | Show and paste |
| `save-buffer a.txt` | Save to file |
| `delete-buffer -b 1` | Delete buffer 1 |

### Setting

| Command | Description |
| :--- | :--- |
| `set -g OPTION`           | Set for all sessions  |
| `setw -g OPTION`          | Set for all windows   | 
| `setw -g mode-keys vi`    | Enable vi-mode        |
| `set -g prefix C-a`       | Set prefix            |

### Misc

| Command | Description |
| :--- | :--- |
| `swap-pane -s 3 -t 1` | Swap pane |
| `swap-window -t -1` | Move to left |
| `setw synchronize-panes` | Sync Panes |
| `join-pane -t :#` | Join pane |

