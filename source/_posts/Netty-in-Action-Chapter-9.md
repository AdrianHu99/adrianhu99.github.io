---
title: Netty in Action Chapter 9
top: false
cover: false
toc: true
mathjax: true
date: 2020-04-17 08:23:59
summary: Reading notes for Chapter 9 of &laquo;Netty in Action&raquo;
img: /medias/featureimages/netty_in_action.jpg
categories: Tech
tags:
    - Java
    - Netty
password:
---

# Chapter 9 - Unit test

In this chapter, it introduces the use of **EmbeddedChannel**, we can write data into the channel (no matter it's inbound or outbound data), and check the output at the end of the pipeline. It's convenient especially for unit tests.
![EmbeddedChannel data flow](embedded_channel_workflow.png)
In doc of **EmbeddedChannel**, you may find that only this channel has an initialization method where you can put a list of handlers, which is easy for writing tests.
In [here](https://github.com/adrrrrrrrian/programs-for-language-learning/tree/master/Java/Netty/Chapter9), unit tests for inbound traffic, outbound traffic and exception handling are listed.