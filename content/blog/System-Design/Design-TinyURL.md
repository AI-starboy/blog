+++
author = "Bowen She"
categories = ["System Design"]
tags = ["TinyURL"]
date = "2018-12-15"
description = "how to design a url shortening service like TinyURL"
featured = "1.jpg"
featuredalt = "headline"
featuredpath = "/img/system-design/tinyURL"
linktitle = ""
title = "Designing a URL Shortening service like TinyURL"
type = "post"

+++
# Why do we need URLs shortening?

URL shortening is used to create shorter aliases for long URLs. We call these shortened
aliases "short links". Users are redirected to the original URLs when they hit those short
links. Short links save a lot of space when displayed, printed, messaged, tweeted. Additionally,
users are less likely to mistype shorter URLs.  

The shortened URL is nearly one-third of the size of the actual URL.

URLs shortening is used for optimizing links across devices, tracking individual links to
analyze audience and campaign performance, and hiding affiliated original URLs.

# Requirements and Goals of the System
