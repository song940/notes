---
layout: default
title: macOS
has_children: true
---

# macOS

macOS is a Unix-like operating system developed by Apple Inc. It is the operating system that powers the Macintosh family of computers.

Setting up a new Macbook will be tough and cumbersome. Every time I am getting a new Macbook, I go over the same steps on how to set it up for my working experience.

I create a record of my setup, hoping it's helpful for others too!

## Get started

### Enable Tap to Click

When setting up a new Macbook, one of the first changes we make is enabling the tap-to-click feature for the trackpad.

Go「**System Preference -> Trackpad -> Point & Click**」and enable 「**Tap to click**」 option.

![](https://raw.githubusercontent.com/maoxiaoke/setup-a-mac-for-frontend-dev/main/enable-tap-to-click.png)

```shell
$ defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad Clicking -int 1
```

### Enable Three Finger Dragging

In general, "tap to click" on your Macbook to avoid a force-click on the trackpad. But this doesn't work when it comes to dragging and repositioning windows.

Also, I'm big fan of tree finger dragging.

1. Go 「**System Preference -> Accessibility**」.
2. In the Accessibility sidebar, choose option 「**Pointer Control**」.
3. Click the button 「**Trackpad Options**」.
4. Enable dragging and select 「**three finger drag**」.

![](https://raw.githubusercontent.com/maoxiaoke/setup-a-mac-for-frontend-dev/main/enable-three-finger-drag.png)

```shell
$ defaults write com.apple.AppleMultitouchTrackpad TrackpadThreeFingerDrag -int 1
```

### Enable App Exposé with trackpad

"App Exposé" lets you see shows you all open and unhidden windows for your current app.

![](https://raw.githubusercontent.com/maoxiaoke/setup-a-mac-for-frontend-dev/main/app-exposé.png)

1. Go 「**System Preference -> Trackpad**」.
2. Click the 「**More Gestures**」.
3. Enable "App Exposé" and select 「**Swipe down with four fingers**」.

![](https://raw.githubusercontent.com/maoxiaoke/setup-a-mac-for-frontend-dev/main/enable-app-exposé.png)

### Enable Stage Manager

Compared to multiple windows, I prefer [Stage Manager](https://support.apple.com/en-ph/102355). This feature arrived with macOS Ventura, and provides a little bit of ability to make your windows less cluttered.

1. Click Control Center in the menu bar, then click Stage Manager.

![](https://raw.githubusercontent.com/maoxiaoke/setup-a-mac-for-frontend-dev/main/enable-stage-manager.png)


## Setting Up Your Mouse

### Activate Misson Control with a mouse button

![](https://raw.githubusercontent.com/maoxiaoke/setup-a-mac-for-frontend-dev/main/mouse-mission-control.png)