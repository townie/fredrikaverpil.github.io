---
layout: post
title: ffmpeg and Homebrew
tags: [osx]
---

Quick note on how to install ffmpeg (using Homebrew) for mp4 format converisons.

<!--more-->


### .webm and .mp4

```bash
# Install (macOS using Homebrew)
brew install ffmpeg --with-fdk-aac --with-sdl2 --with-freetype --with-libass --with-libvorbis --with-libvpx --with-opus --with-x265

# .webm -> .mp4
ffmpeg -i input.webm -codec copy output.mp4

# .mp4 -> .webm
ffmpeg -i input.mp4 -strict -2 output.webm
```

### Verify ffmpeg build configuration

```bash
ffmpeg -buildconf
```

### Convert all files in the same directory to .mp4

```bash
# Replace WILDCARD with e.g. *webm
for i in WILDCARD; do ffmpeg -i $i [options] $i.mp4; done
```

### Merge .m4a with .mp4

```bash
ffmpeg -i video.mp4 -i audio.m4a -codec copy output.mp4
```

### Extract JPG at given time from video

```bash
# Enter time in hh:mm:ss
ffmpeg -ss 00:00:46 -i input.mp4 -vframes 1 -q:v 2 output.jpg
```
