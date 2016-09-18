---
layout: post
title: "Install packets using pip without Internet access"
categories: Linux
tags: [python]
icon: icon-python
---

Pip is useful for installing python-based packets such as tensorflow. However, The restriction of it is that it needs Internet connection, which is usually impossible for some servers that only restricts to internal network connections for security reasons.

One approach to enable pip installation on servers without Internet access is to use the offline feature of pip. The basic procedures are:

- download and/or install the packet such as tensorflow using pip on a machine (machine A) that has Internet access.
- copy the downloaded packets and dependencies to the machine (machine B) without Internet access.
- install the packet using pip with the offline installation feature on machine B.

## Download the necessary packets on machine A
First, we need to download the necessary packets and dependencies for the packet you want to install. For example, if you want to install numpy, you can download and install it via

``` bash
pip install --download /path/to/some/dir numpy
```

The ``--download`` flag will download `numpy` and all its dependencies to `/path/to/some/dir/`, which is needed for offline installation later.

## Copy the packets to machine B

It is simple.

``` bash
scp -r /path/to/some/dir username@machineB:/new/path/dir/
```

## Pip offline installation on machine B

Now, you are at machine B where the downloaded packets are avaiable on this machine (just copied). Now you can install the packet offline.

``` bash
pip install --no-index --find-links /new/path/dir/ numpy
```

That's all of it.
