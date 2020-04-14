---
title: Netty in Action - Chapter 2
top: false
cover: false
toc: true
mathjax: true
date: 2020-03-31 21:09:34
summary: Reading notes for Chapter 2 of &laquo;Netty in Action&raquo;
img: /medias/featureimages/netty_in_action.jpg
categories: Tech
tags:
    - Java
    - Netty
password:
---

# Chapter 2 - First Netty Application - Echo Client and Server

## Echo Server
1. At least one ChannelHandler - implementation of data processing
2. Bootstrapping - startup code that configures server.


## Echo Client
The client will: 
1. Connect to the server
2. Send one or more messages
3. For each message, wait for and receive the same message back from the server
4. Close the connection

**NOTE**: SimpleChannelInboundHandler takes care of releasing the memory reference to the ByteBuf that holds the message.
## [Sample Code](https://github.com/adrrrrrrrian/programs-for-language-learning/tree/master/Java/Netty/Chapter2)