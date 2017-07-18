---
layout: post
title: ffmpeg and Homebrew
tags: [osx]
---

Quick note on how to install ffmpeg (using Homebrew) for mp4 format converisons.

<!--more-->

This requires Homebrew.


### Install ffmpeg

```
brew install ffmpeg --with-fdk-aac --with-sdl2 --with-freetype --with-libass --with-libvorbis --with-libvpx --with-opus --with-x265
```

### Convert to .mp4 without re-encoding

```
ffmpeg -i MOVIEFILE -vcodec copy -acodec copy output.mp4
```

### Convert all files in the same directory to .mp4

```bash
# Replace WILDCARD with e.g. *webm
for i in WILDCARD; do ffmpeg -i $i -vcodec copy -acodec copy $i.mp4; done
```
