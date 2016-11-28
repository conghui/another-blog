---
layout: post
title: "Use system-wide command even you've installed linuxbrew"
categories: Linux
tags:
icon: fa-linux
---

Linuxbrew provides a good solutions for manage applications even if you don't have the root permissions to install system-wide softwares using `yum` or `apt-get` commands. With Linuxbrew, you can have a system-wide toolkits as well as a per-user toolkits alone with you. It greatly enables user to install different kinds of packages with only one command conveniently without considering the dependencies, which will automatically installed by Linuxbrew. However, the default compilation environment will also be changed to that of Linuxbrew, which usually employs the latest `gcc` and `glibc`. The latest `gcc` works well with some projects such as the toy programs written my our own, however, it doesn't work for compiling certain kind of popular tools, such as `CUDA`, `OPENCV` and `MaxCompiler`.

If you use the system-wide compiler `/usr/bin/gcc` for some libraries such as `opencv` and the Linuxbrew-based compiler `~/.Linuxbrew/bin/gcc` for other projects that invokes `opencv`, you probably encounter errors when linking the object files and libraries, such as
```bash
undefined reference to `ibv_alloc_pd@IBVERBS_1.1`
```

## Possible solutions
The simplest way to resolve the error is to use the same compiler for compiling the source codes and the libraries. In this case, the Linuxbrew-based compiler doesn't work for `opencv` and we can only use the system-wide compiler.

So the question become how to use the system-wide compiler when your default compiling environment is Linuxbrew-based one.

One solution is the remove the binary path of Linuxbrew from the environment variable `PATH`. By default, you need to remove `~/.Linuxbrew/bin` from `PATH`. This can be achieved by the following code snippets.

``` bash
function remove_PATH() {
  # only one path is allowed at a time
  if [[ -d "$1" ]]; then
    export PATH=`echo -n $PATH | awk -v RS=: -v ORS=: '$0 != "'$1'"' | sed 's/:$//'`
  fi
}

remove_PATH /home/rice/.Linuxbrew/bin
```

However, you will unable to use any utility installed by `brew` the brew path is not in the `PATH`. It is as if the linuxbrew is not installed at your server, which seems to go to the opposite side of the beginning. One solution to alleviate the problem is to use the `direnv` utility, which allows per-directory environment management. With `direnv`, you are able to remove the linuxbrew environment only within a specific directory other than the whole system. However, the linuxbrew-based utilities still unaviable inside the directory that is restricted.

## Suggested solution
As we are heavily relied on the linuxbrew-based utilities, we are not willing to use the system-wide compiling tools at the cost of abandoning the linuxbrew-based utilities. So a good solution needs to satisfy the following requirements.
- we can use the system-wide compilation environment as well as the linuxbrew-based utilities in our projects directory
- we can use the linuxbrew-based environment outside of that projects directory
- the linuxbrew will be not skewed

To satisfy the per-directory environment variable management, we employ `direnv` to modify `PATH` so that the environment changed in the current directory won't make any effect when we leave the directory. In order to use the system-wide compilation environment in the project directory, we prefix/prepend the path where the system-wide compiler stays (usually `/usr/bin/`) to the `PATH` variable with `direnv`. Basically, it is

``` bash
# file: .envrc
export PATH=/usr/bin:$PATH
```

In this way, we can satisfy the requirements above.

## Discussions

1. Why don't we prepend `/usr/bin/` all the time? Putting `/usr/bin/` before `~/.linuxbrew/bin/` means the command we use will first be looked up in `/usr/bin/` instead of `~/.linuxbrew/bin`. This will partially disable Linuxbrew if the commands you use are in both places. The commands in `/usr/bin/` hide those in linuxbrew binary directory. The Linuxbrew will be skewed because it cannot find the compiler it desires when installing packages. It always found the ones in `/usr/bin/`. Other commands such as `python` that appears in both places will also work unexpectedly.

2. The disadvantage of this solution is that it will partially disable Linuxbrew. The reason is explained above. So the effective usage would be use as few system-wide commands as possible. The system-command will hide the one in Linuxbrew if they have the same names.
