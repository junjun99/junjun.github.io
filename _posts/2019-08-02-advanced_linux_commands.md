
---
layout: post
comments: true
title: Learning Mакедонски
---

Just a collection of useful commands that I find cool/interesting.
You will require coreutils to run the MacOS commmands. (`brew install coreutils`)
[Don't have homebrew? Please install it](https://brew.sh/)


### Copy N random files from one directory to another. 

Good for messing around with a small sample from a large dataset. You can also add a regex pattern if you wish to filter the population in which the sample will be taken from.

Basic shuffle and copy using xargs.
Must be done within the source directory.

MacOS:
`gshuf -zn <FILE_COUNT> -e <PATTERN> | xargs -0 gcp -vt <TARGET_DIR>`

GNU:
`shuf -zn8 <FILE_COUNT> -e <PATTERN> | xargs -0 cp -vt <TARGET_DIR>`

If the source directory cantains a very lage number of files, you may encounter an error; `shuf: Argument list too long`.
In this case, we can pipe the arguments as follows

MacOS:
`find <SOURCE_DIR> -mindepth 1 -maxdepth 1 ! -name '<PATTERN>' -print0 | gshuf -n <FILE_COUNT> -z | xargs -0  gcp -t <TARGET_DIR>`

GNU:
`find <SOURCE_DIR> -mindepth 1 -maxdepth 1 ! -name '<>PATTERN' -print0 | shuf -n <FILE_COUNT> -z | xargs -0  cp -t <target_directory>`

You can even tweak these commands so that you can copy N random **lines** from one file to another in those cases where all your data is in one file.
