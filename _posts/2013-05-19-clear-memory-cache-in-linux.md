---
layout: post
title: "Clear memory cache in Linux"
categories: Linux
tags: [basic]
icon: fa-linux
---

Just by using a really simple command:

``` bash
sync; echo 3 > /proc/sys/vm/drop_caches
```

- echo 3 is clearing pagecache, dentries and inodes
- echo 1 to free pagecache only
- echo 2 to free dentries and inodes.
