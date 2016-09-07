---
layout: post
title: "Check root previledge in bash script"
modified:
categories: Linux
excerpt:
tags: []
icon: fa-linux
---

UID is an important environment variable that can be used to check whether the
current script has been run as root user or regular user. For example:

```
if [ ${UID} -ne 0 ]; then
    echo "Not root user. Please run as root"
else
    echo "Root user"
fi
```

The UID for the root user is 0
