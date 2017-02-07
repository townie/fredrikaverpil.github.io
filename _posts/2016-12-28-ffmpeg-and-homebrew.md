---
layout: post
title: ffmpeg and Homebrew
tags: [osx]
---

Quick note on how to install ffmpeg (using Homebrew) for mp4 format converisons.

<!--more-->

This requires Homebrew.


## Install ffmpeg

    brew install ffmpeg --with-fdk-aac --with-sdl2 --with-freetype --with-libass --with-libvorbis --with-libvpx --with-opus --with-x265


## Convert .webm to .mp4 without re-encoding

    ffmpeg -i LostInTranslation.mkv -vcodec copy -acodec copy LostInTranslation.mp4

### Convert all files in the same directory

```bash
for i in *mkv; do ffmpeg -i $i -vcodec copy -acodec copy $i.mp4; done
```
