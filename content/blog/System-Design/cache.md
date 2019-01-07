+++
author = "Bowen She"
categories = ["python", "cache"]
tags = ["python"]
date = "2019-01-02"
description = "If the first concern of a developer is to be sure that the code they write works well, the second one is to make sure that it run fast. This is expecially true when you’re dealing with web applications, where the scalability of your application is a crucial topic."
featured = "worldCup.gif"
featuredalt = "quiz time"
featuredpath = "/img"
linktitle = ""
title = "How to make your code faster by using a cache in Python"
type = "post"
+++

🚩 [原文](https://medium.com/the-python-corner/how-to-make-your-code-faster-by-using-a-cache-in-python-fb169fbcbb0b)

Summary points:

A cache system is a component that stores data so that future requests for data we already served in the past, could be accomplished faster.

There are a lot of solutions that can be used to implement a cache system
but today I want to point out a specific solution that allows your Python code to use a cache for everyday use, without setting up a complex (and yet more powerful) system like **Redis** or other: the **package cachetools**.

Suppose you have a function that check the price of a single candy by connecting with a web service of a server in the cloud. Unfortunately, this web service is very slow to response (you should fire the guy who wrote it maybe), so this function that check the price is always very slow.

Developing is often a metter of tradeoffs, think about it not only when you have to decide if to use a cache or not, but always when you start designing a software solution.

## When to use the cache System

1. The web service has some bottleneck such that there are always slow responses from frequent requests.

2. The return values from those slow responses don't vary so often(not frequently updated). We can assume the value won't be updated within 5 minutes, then we don't update the cache within 5 minutes timestamp as well.

## Key Code

```python
from cachetools import cached, TTLCache  # 1 - let's import the "cached" decorator and the "TTLCache" object from cachetools
cache = TTLCache(maxsize=100, ttl=300)  # 2 - let's create the time-to-live cache object.

@cached(cache)  # 3 - it's time to decorate the method to use our cache system!
```

In the example above we have used a “Time To Live Cache”. This cache associates a time to live value to each item stored in cache. Items that expire because they have exceeded their time-to-live are removed automatically, making room for new values. If no expired items are there to remove, the least recently used items will be discarded first to make space when necessary.

Other kinds of cache that are available in the cachetools package are:

the LFUCache (Least Frequently Used), that counts how often an item is retrieved, and discards the items used least often to make space when necessary.
the LRUCache (Least Recently Used), that discards the least recently used items first to make space when necessary.
the RRCache (Random Replacement), that randomly selects candidate items and discards them to make space when necessary.

And all these cache types can be used in a decorator of a function, like we did it before, or simply by creating a cache object and using it directly, choosing at run time what to add to the cache and when to retrieve the values added.
