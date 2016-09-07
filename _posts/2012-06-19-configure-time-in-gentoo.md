---
layout: post
title: "Configure time in Gentoo"
categories: [Linux]
excerpt:
tags: [gentoo]
icon: icon-gentoo
---

If you want to set your system time in Gentoo, especially when you want to
dual boot your system, you should have a configuration for Gentoo. I am in
Shanghai, Asia. So I did the following stuffs:

Copy the locale file to /etc


```
cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

Set your time zone

```
echo "Asia/Shanghai" > /etc/timezone
```

Modify hwclock file (/etc/conf.d/hwclock)

```
clock="local"
clock_systohc="YES"
```

Done
