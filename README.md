# Motivation

This version of `lsof` utility is based on same sources as the one shipped with Mac OS X by default. The difference is that we strip it of all the details we do not care about. This version only reports details about regular files. Every other entity (pipes, sockets, ...) is ignored and will be flagged as `unknown file type: $code`. 

We do this because all we care about is to find out which of our regular files are still opened and we want this information fast:

```
$ time lsof -n > /dev/null
> 0,23s user 0,90s system 99% cpu 1,140 total
```
vs

```
$ time this-lsof > /dev/null
> 0,04s user 0,02s system 89% cpu 0,065 total
```

# Building

To build this you will need Xcode installed and some MacOSX sdk. Also you should run it with the default `make` (GNU version installed via homebrew might fail).

 1. clone this repository: ``git clone https://github.com/zuzkins/mac-lsof-regular-files-only``
 2. cd into it: ``cd mac-lsof-regular-files-only``
 4. ``make LSOF_INCLUDE="`xcrun -sdk / --show-sdk-path`/usr/include"``
 5. should produce `/tmp/lsof/Build/lsof` binary
