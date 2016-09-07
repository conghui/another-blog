---
layout: post
title: "Set up Java in Gentoo"
modified:
categories: Linux
excerpt:
tags: [gentoo]
icon: icon-gentoo
---

This guide tell you how to set up java developping environment in Gentoo in brief

### Installing the programming environment

The first thing you need to do is to get a developing kit for java, that is JDK, to get this, use the command

```
sudo emerge sun-jdk
```

### Installing the checkstyle and findbugs

checkstyle can check and warn you about the style you use in java, and findbugs
can try to find the bugs in your program, these are two handy and quite useful
tools that can help you while you are developing java programs, to get them,
just emerge them

```
sudo emerge checkstyle findbugs
```
