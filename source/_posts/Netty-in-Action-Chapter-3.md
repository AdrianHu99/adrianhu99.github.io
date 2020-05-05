---
title: Netty in Action - Chapter 3
top: false
cover: false
toc: true
mathjax: true
date: 2020-04-02 08:19:04
summary: Reading notes for Chapter 3 of &laquo;Netty in Action&raquo;
categories: Tech
tags:
    - Java
    - Netty
password:
---


# Chapter 3 - Netty components and design
<!--more-->
Channel - Sockets
EventLoop - Control flow, multithreading, concurrency
ChannelFuture - Asynchronous notification, a placeholder for the result of an operation that's to be executed in the future.

### Interface EventLoop

1.  An *EventLoopGroup* can contain multiple *EventLoops*
2.  An *EventLoop* is bound to a single Thread for its lifetime
3.  All I/O events processed by an *EventLoop* are handled on its dedicated Thread
4.  A channel is registered for its lifetime with a single *EventLoop*
5.  A single *EventLoop* may be assigned to one or more *Channels*

![Channel and EventLoop](channel_eventLoop.png)

### Interface ChannelHandler

Primary component of Netty which serves as the container for all application logic that applies to inbound and outbound data. 

### Interface ChannelPipeline

*ChannelHandlers* are installed in *ChannelPipeline* as follows: 
1.  The *ChannelInitializer* implementation is registered with a *ServerBootstrap*
2.  When *ChannelInitializer*.*initChannel*() is called, it will install a custom set of *ChannelHandlers* in the pipeline
3.  The *ChannelInitializer* removes itself from the *ChannelPipeline*

![ChannelPipeline](channelPipeline.png)

There are two ways of sending messages in Netty: 
1. Write directly to the *Channel*, which will cause the message to start from the tail of the pipeline
2. Write to a *ChannelHandlerContext*, which will cause the message to start from the next handler in the pipeline

### Encoder and decoder

When inbound message comes in, it will be decoded
When outbound message goes out, it will be encoded

The encoder/decoder adapter classes provided by Netty implement either *ChannelInboundHandler* or *ChannelOutboundHandler*
For each inbound message, it will call decode() and forward the decoded bytes to the next *ChannelInboundHandler* in the pipeline; An encoder converts the message to bytes and forwards them to the next *ChannelOutboundHandler*

### Bootstrapping
*bootstrapping a server*: bind a process to a given port (**ServerBootstrap**)
*bootstrapping a client*: connect one process to another one running on a host at a specific port (**Bootstrap**)

A server needs two distinct set of *Channels*:
1. The first set will contain a single *ServerChannel* representing the server's own listening socket, bound to a local port.
2. The second set will contain all of the *Channels* that have been created to handle incoming client connections - one for each connection the server accepted.

This explains why two distinct *EventLoopGroups* are required

![Server with EventLoopGroups](eventLoopGroup.png)

The first group will assign an *EventLoop* that is responsible for creating *Channels* for incoming connection requests. The second group will assign *EventLoop* to handle the *Channel*


