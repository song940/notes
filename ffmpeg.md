---
title: FFmpeg
layout: default
---

# FFmpeg

![](https://i.namu.wiki/i/8NdXryEFjMXYhItCYvNx7vdTinXJfouFFrhngaj7rfIOCBB0LvassnR7eEGt5RXsxQEecZlqDQLZrsh0MIY1mA.svg)

ffmpeg is a complete, cross-platform solution to record, convert and stream audio and video. It is the reference multimedia library for the FFmpeg project.

查看 FFmpeg 支持的容器

```shell
~$ ffmpeg -formats
```

编码

- H.264
- H.265

上面的编码格式都是有版权的，但是可以免费使用。此外，还有几种无版权的视频编码格式

- VP8
- VP9
- AV1

常用的音频编码格式

- MP3
- AAC

```shell
~$ ffmpeg -codecs
```

```shell
~$ ffmpeg -encoders
```

## FFmpeg 命令格式

FFmpeg 的命令行参数非常多，可以分成五个部分

```shell
~$ ffmpeg {1} {2} -i {3} {4} {5}
```

1. 全局参数
2. 输入文件参数
3. 输入文件
4. 输出文件参数
5. 输出文件

### Concat Videos

```shell
ffmpeg -i "concat:1.avi|2.avi" -codec copy output.avi
ffmpeg -f concat -i input.txt -c copy output.mp4
```

First, create a file that contains the list of all your .avi files. You can do this manually, but if your files are named in a sequence like 01.avi, 02.avi, 03.avi, and so on, you can generate this list automatically using a bash command. Here's how you can do it:

```shell
for f in *.avi; do echo "file '$f'" >> mylist.txt; done
```

This will create a file mylist.txt that contains a list of your .avi files in this format:

```shell
file '01.avi'
file '02.avi'
file '03.avi'
...
```

```shell
ffmpeg -f concat -safe 0 -i mylist.txt -c copy output.avi
```

### Merge Audio and Video

```shell
ffmpeg -i video.mp4 -i audio.wav -c copy output.mkv
```

```shell
ffmpeg -i video.mp4 -i audio.wav -c:v copy -c:a aac output.mp4
```

### Convert to MP4

```shell
ffmpeg -i input.avi -c:v copy -c:a copy output.mp4
ffmpeg -i input.webm -c:v copy -c:a copy output.mp4
```

```shell
ffmpeg -i input.webm -c:v libx264 -preset slow -crf 22 -c:a aac -b:a 128k output.mp4
```

### Video Compression

```shell
ffmpeg -i input.mp4 -c:v libvpx-vp9 -b:v 0 -crf 30 -preset superfast output.mp4
ffmpeg -i input.mp4 -c:v libaom-av1 -crf 30 -b:v 0 -strict experimental output.mp4
ffmpeg -i input.mp4 -c:v libx264 -tag:v avc1 -movflags faststart -crf 30 -preset superfast output.mp4
```

### Clip Video

```shell
ffmpeg -i input.mp4 -ss 30 -c copy output.mp4
ffmpeg -ss 00:06:38 -to 00:10:38 -i input.mp4 -c copy output.mp4
```

### List Devices

```shell
~$ ffmpeg -f avfoundation -list_devices true -i ""
[...]
[AVFoundation indev @ 0x14d9042f0] AVFoundation video devices:
[AVFoundation indev @ 0x14d9042f0] [0] FaceTime HD Camera
[AVFoundation indev @ 0x14d9042f0] [1] Lsong’s iPhone 13 Pro Camera
[AVFoundation indev @ 0x14d9042f0] [2] Capture screen 0
[AVFoundation indev @ 0x14d9042f0] AVFoundation audio devices:
[AVFoundation indev @ 0x14d9042f0] [0] LarkAudioDevice
[AVFoundation indev @ 0x14d9042f0] [1] Lsong’s iPhone 13 Pro Microphone
[AVFoundation indev @ 0x14d9042f0] [2] MacBook Pro Microphone
: Input/output error
```

https://ffmpeg.org/ffmpeg-devices.html

### Record Screen Capture

```shell
# ffmpeg -f avfoundation -i "<screen device index>:<audio device index>" output.mkv
# [2] Capture screen 0
# [2] MacBook Pro Microphone
ffmpeg -f avfoundation -i "2:2" output.mkv
```
https://trac.ffmpeg.org/wiki/Capture/Desktop

### Record FaceTime Camera

```shell
# [0] FaceTime HD Camera
~$ ffmpeg -f avfoundation -r 30 -pix_fmt uyvy422 -i "0" -y out.mov
```

### Record Screen with Camera

```shell
~$ ffmpeg -y \
  -f avfoundation -r 30 -video_size 1920x1080 -capture_cursor true -capture_mouse_clicks true -i "2:2" \
  -f avfoundation -r 30 -video_size 1280x720 -i "0" \
  -filter_complex "[1]scale=iw/2:ih/2 [pip]; [0][pip] overlay=W-w-50:H-h-50" \
  output.mkv
```

### YouTube Live

Record Screen with Camera and Push to YouTube

```bash
#!/usr/bin/env sh

RTMP_STREAM_URL="rtmp://a.rtmp.youtube.com/live2/<token>"

ffmpeg -y \
  -f avfoundation -r 30 -video_size 1920x1080 -capture_cursor true -capture_mouse_clicks true -i "2:2" \
  -f avfoundation -r 30 -video_size 1280x720 -i "0" \
  -filter_complex "[1]scale=iw/2:ih/2 [pip]; [0][pip] overlay=W-w-50:H-h-50" \
  -f flv "$RTMP_STREAM_URL"
```

### Capture Image from RTSP

```shell
ffmpeg -i rtsp://admin:xxx@192.168.2.102/stream1 -vframes 1 -q:v 2 output.jpg
```


---
