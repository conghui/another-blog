---
layout: post
title: "Maxcompilersim error: Address already in use"
categories: Linux
tags: [fpga]
icon: fa-linux
---

If you compile the tutorial code but the compiler complains, with the following error:

``` cpp
/opt/maxeler/bin/maxcompilersim -c`java -cp ../../../bin:/opt/maxeler/lib/MaxCompiler.jar config.BoardModel` restart
Killing simulated system...
Simulated system killed
Error binding to socket maxelerosd.sock: Address already in use
ERROR: Failed to start maxeleros daemon.
make: ** [run-sim] Error 1
```

The Solution is:

find the PID of maxeleros with the command:

```
  /usr/sbin/lsof | grep maxeleros
```

kill existing maxeleros process (root privilege required, maybe)

```
  sudo kill -9 pid_of_maxeleros
```

export the following variables

```
export MAXELEROSDIR=$MAXCOMPILERDIR/lib/maxeleros-sim
export LD_PRELOAD=$MAXELEROSDIR/lib/libmaxeleros.so:$LD_PRELOAD
```

recompile the code and run the program
