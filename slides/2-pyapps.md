# Lab 3 (We're going oh so slow) #

## Today we'll try the following exercises ##

### 1. Write a python program that takes a file as an argument and treats that as the config file
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

### 2. Open the link: https://github.com/brmson/dataset-sts/data/sts/sick2014
### There is a SICK_train.txt file here which contains sentence pairs. You can read the
### corresponding readme.txt and see how what the format of the data is.
### 1. A first step in any process is to clean the data.
###   - Which steps would you take to clean the data?
###   - Of which things would the data be cleaned?
### 2. Second step would be to transform the data into a form that is efficient.
###   - Why isn't the data efficient in this form?
###   - To which forms can it be changed?
###   - What else needs to be done for this language data?
### Write a Python program that performs the requisite steps.


