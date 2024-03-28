---
layout: default
title: bspwm
parent: Linux
---

# bspwm

bspwm is a window manager for X11.

## Display Configuration

```bash
# Define the workspace names for the default monitor
bspc monitor -d 1 2 3 4

# Define the workspace names for the HDMI1 monitor
bspc monitor HDMI1 -d I II III IV V VI VII VIII IX X
```

## Workspace Split Configuration

```bash
# Set the split ratio between windows
bspc config split_ratio 0.52

# Enable borderless mode for monocle layout
bspc config borderless_monocle true
```

## General Configuration

```bash
# Set the window border width
bspc config border_width 5

# Set the gap between windows
bspc config window_gap 3

# Set the border radius
bspc config border_radius 2

# Set the padding at the top of the screen
bspc config top_padding 60

# Enable the setting where focus follows the mouse pointer
bspc config focus_follows_pointer true

# Enable gapless monocle layout
bspc config gapless_monocle true

# Padding configurations for monocle layout
bspc config top_monocle_padding 20
bspc config left_monocle_padding 20 
bspc config right_monocle_padding 20 
bspc config bottom_monocle_padding 20 

# Ignore EWMH struts for a cleaner desktop look
bspc config ignore_ewmh_struts true
```

## Window Rules

```bash
# Assign firefox to workspace 2
bspc rule -a firefox  desktop='^2'

# Assign thunar to workspace 3
bspc rule -a thunar desktop='^3'

# Don't manage Rofi windows
bspc rule -a Rofi manage=off

# Don't manage Polybar and set it to a lower layer
bspc rule -a Polybar manage=off layer=below
```

## Autostart Applications

```bash
# Start picom if it's not running
pgrep -x picom > /dev/null || picom &

# Start sxhkd if it's not running
pgrep -x sxhkd > /dev/null || sxhkd &

# Start polybar
$HOME/.config/polybar/launch.sh

# Set the desktop background
feh --bg-scale $HOME/Pictures/Wallpapers/wallpaper
```