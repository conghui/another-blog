---
layout: post
title: "Create ISO9660 Image in Linux From a Folder"
modified:
categories: Linux
excerpt:
tags: [basic]
icon: fa-linux
---

The advantage of an ISO image file is that it is quite easy (fast) to mount it on
the existing hard drive or burn it on disk with the drawback of the
impossibility of modifying the contents in the ISO image. So, it would be
great to you to create ISO images for files or directories that are ready
to publish to others only for reading. Normally, this files are setup files
or applications installation files.

## Create ISO image from command line ##
In Linux command prompt, command `genisoimage` could be used to create an
ISO image from a directory recursively. For example:

``` bash
genisoimage -r -J -hide-rr-moved -o imagefilename.iso srcdir/
```

For more information, you can refer to the [man page](http://linux.die.net/man/1/genisoimage)
