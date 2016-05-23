---
layout: post
title: 'Nuke script: Read node from Write node'
tags: [nuke, python]
---

Originally posted in 2011; A Python script for [Nuke](https://www.thefoundry.co.uk/products/nuke/), which takes any Write node and creates a Read node from it. Now updated to fix some bugs and offer support for more scenarios.

<!--more-->

The script will attempt to load an image sequence or a single file (such as a movie file), based off the selected Write node.

The script comes with a couple of options:

- `FILEPATH_KNOBS` - File knobs which should be parsed (this makes it possible to generate Read nodes from *any* node)
- `SINGLE_FILE_FORMATS` - A list of filetypes which are expected to contain more than one frame but in fact has more than one frame (e.g. `.mov`)

Download:
- [Nukepedia](http://www.nukepedia.com/python/misc/readfromwrite)
- [Github](https://raw.github.com/fredrikaverpil/nuke/master/scripts/readFromWrite.py)

- v2.0:
  - Completely rewritten from scratch
  - Improved detection of frame range
  - Supports any padding format (not only %04d)
  - Applies colorspace to Read node
  - Supports not only Write nodes (see FILEPATH_KNOBS variable)
  - Supports definition of "single file image sequence" formats
  - PEP8 compliant!

Place the Python script in the /scripts dir inside your `NUKE_PATH` (see my [previous post]({{ site.baseurl }}2011/10/28/nuke-63-small-studio-setup-for-windows-osx/) on setting this up). Add the following to your `menu.py`:

```python
import readFromWrite
nuke.menu( 'Nuke' ).addCommand( 'My file menu/Read from Write', 'readFromWrite.ReadFromWrite()', 'shift+r' )
```

You should now be able to select any Write node and hit `shift+r` to generate a Read node!
