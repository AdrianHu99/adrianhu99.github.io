---
title: Netty in Action Chapter 8
top: false
cover: false
toc: true
mathjax: true
date: 2020-04-14 14:54:16
summary: Reading notes for Chapter 8 of &laquo;Netty in Action&raquo;
img: /medias/featureimages/netty_in_action.jpg
categories: Tech
tags:
    - Java
    - Netty
password:
---

# Chapter 8 - Bootstrapping

In 8.1, the bootstrapping steps common to both server and client are handled by AbstractBootstrap, steps specific to clients/servers are handled by Bootstrap or ServerBootstrap.

In 8.2, *Bootstrap* class is responsible to create Channels for clients and for applications using connectionless protocols.
![Bootstrapping process](bootstrapping_process.png)
We must make sure to not mix OioEventLoopGroup with NioSocketChannel, it will throw exceptions.

In 8.3, *ServerBootstrap* creates *ServerChannel* to create Channels which represents accepted connections.
In 8.4, we are able to bootstrap clients from a Channel, in case we need to act as a client to a third system while processing a client request. And one general guideline from Netty is to reuse EventLoops wherever possible to reduce the cost of thread creation.
![EventLoop shared among Channels](eventLoop_shared_among_channels.png)
In 8.5, we know that we can add more than one ChannelHandlers during a bootstrap by adding them in the pipeline attached to the bootstrap.
In 8.6, we are able to use ChannelOptions to apply configurations for all Channels automatically, it includes low-level properties and buffer settings.
Netty also offers *AttributeMaps* to associate data item with both client and server Channels.
In 8.8, when we need to shut down the application, we will need to shut down the *EventLoopGroup*, which is a matter of calling *EventLoopGroup.shutdownGracefully()*, we can also call *Channel.close()*.