---
layout: post
title: "Install fonts in Gentoo"
modified:
categories: Linux
excerpt:
tags: [gentoo]
icon: icon-gentoo
---

Giving that you have installed your window manager properly, KDE, GNOME, or Xfce.
To support the UTF-8 fonts displaying, you should install the following fonts for CJK.

```bash
 emerge -j  media-fonts/font-isas-misc media-fonts/wqy-bitmapfont \
   media-fonts/bitstream-cyberbit media-fonts/droid media-fonts/ja-ipafonts \
   media-fonts/wqy-microhei media-fonts/wqy-zenhei
```

rebuild the font cache with the following command:

``` bash
fc-cache -fv
```

enable wqy-bitmapsong with the command:

```
eselect fontconfig enable 85-wqy-bitmapsong.conf
```

reboot your system, and fireup a browser, have a look at if the chinese fonts are display properly.
