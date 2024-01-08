---
layout: default
title: Proxmark3
---

# Proxmark3

Proxmark3 是一款开源的 RFID 研究工具，用于读取、分析和模拟无线射频标签（RFID）和近场通信（NFC）设备。

![Proxmark 3 Easy](https://proxmark.com/user/pages/03.proxmark-3-hardware/05.proxmark-3-easy/PM3-Easy-Trans.png)

本指南将帮助你快速入门 Proxmark3 的基本用法。

## 获取 Proxmark3

首先，你需要获取 Proxmark3 设备。你可以选择购买现成的设备，或者自行组装一个。确保你的设备配备了正确的天线，以便与 RFID 标签进行通信。

## 安装 Proxmark3 软件

Proxmark3 软件是开源的，并且可以在 GitHub 上找到，原版的 Proxmark 官方仓库已经不再维护，这里推荐使用 [Iceman Fork](https://github.com/RfidResearchGroup/proxmark3)：

使用以下命令拉取 Proxmark3 存储库：

```shell
git clone https://github.com/RfidResearchGroup/proxmark3
```

进入目录：

```shell
cd proxmark3
```

### 编译 Proxmark3 软件

如果你和我一样使用 macOS 系统，可以参考这里 [macOS - Compilation from source instructions](https://github.com/RfidResearchGroup/proxmark3/blob/master/doc/md/Installation_Instructions/macOS-Compile-From-Source-Instructions.md)


```shell
brew install readline qt5 pkgconfig coreutils
brew install RfidResearchGroup/proxmark3/arm-none-eabi-gcc
```

也可以从源码编译

```shell
make clean && make all
```

### 连接 Proxmark3 设备

将 Proxmark3 设备连接到你的计算机。通常，你需要通过 USB 线连接 Proxmark3 设备，并确保设备已正确安装驱动程序。

### 启动 Proxmark3 软件

```shell
proxmark3 /dev/tty.usbmodemiceman1
```

### 基本操作

一旦启动了 Proxmark3 软件，你可以执行以下基本操作：

```shell
21:12:34 in ~ took 13m 37s
➜ proxmark3 /dev/cu.usbmodemiceman1
[=] Session log /Users/Lsong/.proxmark3/logs/log_20231010131235.txt
[+] loaded from JSON file `/Users/Lsong/.proxmark3/preferences.json`
[=] Using UART port /dev/cu.usbmodemiceman1
[=] Communicating with PM3 over USB-CDC


  8888888b.  888b     d888  .d8888b.
  888   Y88b 8888b   d8888 d88P  Y88b
  888    888 88888b.d88888      .d88P
  888   d88P 888Y88888P888     8888"
  8888888P"  888 Y888P 888      "Y8b.
  888        888  Y8P  888 888    888
  888        888   "   888 Y88b  d88P
  888        888       888  "Y8888P"    [ ☕ ]

Release v4.17140 - Raccoon
  [ Proxmark3 RFID instrument ]

    MCU....... AT91SAM7S512 Rev B
    Memory.... 512 KB ( 60% used )

    Client.... Iceman/master/v4.17140 2023-09-09 11:00:00
    Bootrom... Iceman/master/v4.16717-9-gadfebd651 2023-06-26 21:52:08
    OS........ Iceman/master/v4.16717-9-gadfebd651 2023-06-26 21:52:14
    Target.... PM3 GENERIC


[!] ⚠️   --> ARM firmware does not match the source at the time the client was compiled
[!] ⚠️   --> Make sure to flash a correct and up-to-date version
```

#### 硬件状态

```shell
[usb] pm3 --> hw ping
[=] Ping sent with payload len 32
[+] Ping response received and content () ok )
```

```shell
[usb] pm3 --> hw status
[#] Memory
[#]   BigBuf_size............. 42712
[#]   Available memory........ 42712
[#] Tracing
[#]   tracing ................ 0
[#]   traceLen ............... 0
[#] Current FPGA image
[#]   mode.................... LF image 2s30vq100 2023-05-24 14:12:56
[#] LF Sampling config
[#]   [q] divisor............. 95 ( 125.00 kHz )
[#]   [b] bits per sample..... 8
[#]   [d] decimation.......... 1
[#]   [a] averaging........... yes
[#]   [t] trigger threshold... 0
[#]   [s] samples to skip..... 0
[#]
[#] LF T55XX config
[#]            [r]               [a]   [b]   [c]   [d]   [e]   [f]   [g]
[#]            mode            |start|write|write|write| read|write|write
[#]                            | gap | gap |  0  |  1  | gap |  2  |  3
[#] ---------------------------+-----+-----+-----+-----+-----+-----+------
[#] fixed bit length (default) |  31 |  20 |  18 |  50 |  15 | N/A | N/A |
[#]     long leading reference |  31 |  20 |  18 |  50 |  15 | N/A | N/A |
[#]               leading zero |  31 |  20 |  18 |  40 |  15 | N/A | N/A |
[#]    1 of 4 coding reference |  31 |  20 |  18 |  34 |  15 |  50 |  66 |
[#]
[#] HF 14a config
[#]   [a] Anticol override.... std    ( follow standard )
[#]   [b] BCC override........ std    ( follow standard )
[#]   [2] CL2 override........ std    ( follow standard )
[#]   [3] CL3 override........ std    ( follow standard )
[#]   [r] RATS override....... std    ( follow standard )
[#] Transfer Speed
[#]   Sending packets to client...
[#]   Time elapsed................... 500ms
[#]   Bytes transferred.............. 300544
[#]   Transfer Speed PM3 -> Client... 601088 bytes/s
[#] Various
[#]   Max stack usage......... 4952 / 8480 bytes
[#]   Debug log level......... 1 ( error )
[#]   ToSendMax............... 6
[#]   ToSend BUFFERSIZE....... 2308
[#]   Slow clock.............. 31011 Hz
[#] Installed StandAlone Mode
[#]   LF HID26 standalone - aka SamyRun (Samy Kamkar)
[#]
```

#### 扫描卡

```shell
[usb] pm3 --> auto
[=] lf search

[=] NOTE: some demods output possible binary
[=] if it finds something that looks like a tag
[=] False Positives ARE possible
[=]
[=] Checking for known tags...
[=]
[!] ⚠️  Specify one authentication mode
[-] ⛔ No known 125/134 kHz tags found!
[=] Couldn't identify a chipset
[=] hf search
 🕕  Searching for ISO14443-A tag...
[+]  UID: D3 8F 46 4E
[+] ATQA: 00 04
[+]  SAK: 08 [2]
[+] Possible types:
[+]    MIFARE Classic 1K
[=] proprietary non iso14443-4 card found, RATS not supported
[+] Prng detection: weak
[#] Auth error
[?] Hint: try `hf mf` commands


[+] Valid ISO 14443-A tag found
```

#### 自动攻破

```shell
[usb] pm3 --> hf mf autopwn
[!] ⚠️  no known key was supplied, key recovery might fail
[+] loaded 56 keys from hardcoded default array
[=] running strategy 1
[=] Chunk 0.3s | found 32/32 keys (56)
[+] target sector   0 key type A -- found valid key [ FFFFFFFFFFFF ] (used for nested / hardnested attack)
[+] target sector   0 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   1 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   1 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   2 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   2 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   3 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   3 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   4 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   4 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   5 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   5 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   6 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   6 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   7 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   7 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   8 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   8 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   9 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector   9 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector  10 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector  10 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector  11 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector  11 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector  12 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector  12 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector  13 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector  13 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector  14 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector  14 key type B -- found valid key [ FFFFFFFFFFFF ]
[+] target sector  15 key type A -- found valid key [ FFFFFFFFFFFF ]
[+] target sector  15 key type B -- found valid key [ FFFFFFFFFFFF ]

[+] found keys:

[+] -----+-----+--------------+---+--------------+----
[+]  Sec | Blk | key A        |res| key B        |res
[+] -----+-----+--------------+---+--------------+----
[+]  000 | 003 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  001 | 007 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  002 | 011 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  003 | 015 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  004 | 019 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  005 | 023 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  006 | 027 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  007 | 031 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  008 | 035 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  009 | 039 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  010 | 043 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  011 | 047 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  012 | 051 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  013 | 055 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  014 | 059 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+]  015 | 063 | FFFFFFFFFFFF | D | FFFFFFFFFFFF | D
[+] -----+-----+--------------+---+--------------+----
[=] ( D:Dictionary / S:darkSide / U:User / R:Reused / N:Nested / H:Hardnested / C:statiCnested / A:keyA  )


[+] Generating binary key file
[+] Found keys have been dumped to /Users/Lsong/hf-mf-D38F464E-key-001.bin
[=] --[ FFFFFFFFFFFF ]-- has been inserted for unknown keys where res is 0
[=] transferring keys to simulator memory ( ok )
[=] dumping card content to emulator memory (Cmd Error: 04 can occur)
[=] downloading card content from emulator memory
[+] saved 1024 bytes to binary file /Users/Lsong/hf-mf-D38F464E-dump-001.bin
[+] saved 64 blocks to text file /Users/Lsong/hf-mf-D38F464E-dump-001.eml
[+] saved to json file /Users/Lsong/hf-mf-D38F464E-dump-001.json
[=] autopwn execution time: 2 seconds
```

#### 将数据还原到新卡

```shell
[usb] pm3 --> hf mf restore --1k --uid D38F464E -k hf-mf-D38F464E-key.bin -f hf-mf-D38F464E-dump.bin
[=] Using key file `hf-mf-D38F464E-key-002.bin`
[+] loaded 1024 bytes from binary file `hf-mf-D38F464E-dump.bin`

[=]  blk | data                                            | status
[=] -----+-------------------------------------------------+----------------
[=]    0 | D3 8F 46 4E 54 08 04 00 62 63 64 65 66 67 68 69 | ( ok )
[=]    1 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]    2 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]    3 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]    4 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]    5 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]    6 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]    7 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]    8 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]    9 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   10 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   11 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]   12 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   13 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   14 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   15 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]   16 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   17 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   18 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   19 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]   20 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   21 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   22 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   23 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]   24 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   25 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   26 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   27 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]   28 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   29 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   30 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   31 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]   32 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   33 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   34 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   35 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]   36 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   37 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   38 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   39 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]   40 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   41 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   42 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   43 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]   44 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   45 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   46 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   47 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]   48 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   49 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   50 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   51 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]   52 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   53 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   54 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   55 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]   56 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   57 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   58 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   59 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=]   60 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   61 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   62 | 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 | ( ok )
[=]   63 | FF FF FF FF FF FF FF 07 80 69 FF FF FF FF FF FF | ( ok )
[=] -----+-------------------------------------------------+----------------

[=] Done!
```

[Cheat Sheet](https://github.com/RfidResearchGroup/proxmark3/blob/master/doc/cheatsheet.md)

### 学习更多

Proxmark3 是一个强大的工具，具有丰富的功能和选项。要深入了解其更高级的用法，请查阅 Proxmark3 文档和社区资源。

- https://proxmark.com
- https://github.com/RfidResearchGroup/proxmark3
- https://github.com/wh201906/Proxmark3GUI/releases

### 注意事项

- 使用 Proxmark3 进行 RFID 研究时，请遵守法律法规，确保你的活动合法且合规。
- 在进行实验之前，务必备份并保存重要数据，以防意外损失。
- 谨慎操作，避免损坏 RFID 标签或设备。

希望这份快速入门指南能够帮助你开始使用 Proxmark3 进行 RFID 研究。如果你想深入学习，请参考 Proxmark3 的官方文档和社区支持资源。
