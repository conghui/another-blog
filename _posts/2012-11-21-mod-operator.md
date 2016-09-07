---
layout: post
title: "A good way to use % (mod) operator"
description: ""
categories: Programing
tags: [c++]
icon: fa-desktop
---

## Question
If you want to iterate an array from the **ith** element, and continue scaning
up to **n** elements and when you reach the end of the array, you should
continue scaning from the first element. What's your idea?

------------------------------

## Previous Idea
It is an easy question. We can use the **if/else** conditional statement to
guard that if the next element will exceed the array, if so, just assign the
iterator to the first element.

``` cpp
for (it = i; n-- > 0; it++) {
    if (it + 1 == arraySize) { /* reach the end */
        it = 0; /* reset the iterator */
    }
    /* your stuff here */
}
```

Such a approach works, but the code is quite fat and dummy. Now I have another
idea.

------------------------------------

## Current Idea
We can use **%** (mod) operator. While moving the iterator forward, the iterator
will go out of the bound of the array. How to restrict the iterator within the
bound? Yes, that is the **%** (mod) operator. How the following code ?

``` cpp
for (it = i; n-- > 0; it = (it + 1) % arraySize) { /* keep an eye on % operator */
    /* your stuff here */
}
```

----------------------------------------

## Usage
It is obvious that if the iterator increase with the **%** (mod) operator, it
will move around and around, just treat the array as a cicle array (list). So
when you implement a cicle list with a array, you can use such approach.
