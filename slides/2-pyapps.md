# Lab 3 (We're going oh so slow)
### 1. Write a function that takes a file as an argument and treats that as the config file
### If the file/path doesn't exist, it is created and a default skeleton is created, else it is
### read and parsed. The configuration file can hold keyword entries with sections, e.g.

```Ini
[general]
home = /home/user
env = xterm
description  = "A simple example config"
[codec_options]  # '#' indicates a comment in the file just like python
codec = mp4
trellis = True
bitrate = 480
```

