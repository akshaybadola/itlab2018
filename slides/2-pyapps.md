# Lab 3 Regex, File and URL Handling #

## First we'll look at some regular expression
## Then we'll try some exercises 
## These are not really exercises on data but learning how to do 
## such things will be handy in the long run
##

0.1. Build a regular expression to match all pdf links in an html page
	   Note, that a link will start with <a href=...> and end with </a>
0.2. Build a regular expression to match all sentences which begin with 'The'.
	   You'd have to match till the first full stop occurs.
0.3. Build a regular expression that matches numbers, including letters in numbers
	   but only if occurs at the end of a line. e.g.
	   
		   There is a light that never goes out 12345blah2343
matches
0.4. Write a python program to split a text file at dates where a date is
	   expected to be of type 'yyyy-mm-dd', e.g. '2014-02-20'
0.5. Write a python program that takes a url and gets all the urls it points to
	   Use urllib3.
0.6. Write a python program that takes a date as input and gives you the
	   corresponding Dilbert comic.

## Then we'll try the following exercises ##

#### 1. Write a python program that takes a file as an argument and treats that as the config file
#### If the file/path doesn't exist, it is created and a default skeleton is created, else it is
#### read and parsed. The configuration file can hold keyword entries with sections, e.g.

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

#### 2. Open the link: https://github.com/brmson/dataset-sts/data/sts/sick2014
There is a SICK_train.txt file here which contains sentence pairs. You can read the
corresponding readme.txt and see how what the format of the data is.
1. A first step in any process is to clean the data.
  - Which steps would you take to clean the data?
  - Of which things would the data be cleaned?
2. Second step would be to transform the data into a form that is efficient.
  - Why isn't the data efficient in this form?
  - To which forms can it be changed?
  - What else needs to be done for this language data?
Write a Python program that performs the requisite steps.
