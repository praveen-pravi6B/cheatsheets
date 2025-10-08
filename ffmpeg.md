---
title: ffmpeg
category: CLI
---

### Common switches

```bash
-codecs          # list codecs
-c:v             # video codec (-vcodec) - 'copy' to copy stream
-c:a             # audio codec (-acodec)
-ss              # Stream Seek (90 = 1min 30sec, 01:00:00 = 1hr)
-t               # Time Duration (10 for first 10 sec)
```

```bash
-fs SIZE         # limit file size (bytes)
```

### Bitrate

```bash
-b:v 1M          # video bitrate (1M = 1Mbit/s)
-b:a 1M          # audio bitrate
```

### Video

```bash
-aspect RATIO    # aspect ratio (4:3, 16:9, or 1.25)
-r RATE          # frame rate per sec
-s WIDTHxHEIGHT  # frame size
-vn              # no video
-pix_fmt FORMAT  # Pixel Format (yuv420p, yuv420p10le)
-crf LEVEL       # Constant rate factor (0-51 lower value for high quality)
```

### Audio

```bash
-aq QUALITY      # audio quality (codec-specific)
-ar 44100        # audio sample rate (hz)
-ac 1            # audio channels (1=mono, 2=stereo)
-an              # no audio
-vol N           # volume (256=normal)
```

## Example

### Ringtone conversion using ffmpeg

```bash
ffmpeg -i foo.mp3 -ac 1 -ab 128000 -f mp4 -acodec libfaac -y target.m4r
```
### Stream Selection in ffmpeg

```bash
ffmpeg -i input1.mp4 -i input2.mp4 -map 0:v:0 -map 1:a:0 output.mp4
# To create output file with video from 1st file & audio from 2nd file.

ffmpeg -i input1.mp4 -i input2.mp3 -map 0:v -map 1:a output.mkv
# To create output file with all video streams from 1st file & audio streams from 2nd file.

# -map [INPUT_FILE_INDEX]:[STREAM_SPECIFIER]
# -map [INPUT_FILE_INDEX]:[STREAM_SPECIFIER]:[STREAM_INDEX]
```


### To web

```bash
# no audio
ffmpeg -i input.mov -vcodec h264   -an -strict -2 output.mp4
ffmpeg -i input.mov -vcodec libvpx -an output.webm
```

```bash
ffmpeg -i input.mov -vcodec h264 -acodec aac -strict -2 output.mp4
ffmpeg -i input.mov -vcodec libvpx -acodec libvorbis output.webm
```

```html
<video width="320" height="240" controls>
  <source src="movie.mp4" type='video/mp4'></source>
  <source src="movie.webm" type='video/ogg'></source>
</video>
```
