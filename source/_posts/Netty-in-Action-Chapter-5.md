---
title: Netty in Action Chapter 5
top: false
cover: false
toc: true
mathjax: true
date: 2020-04-03 14:41:57
summary: Reading notes for Chapter 5 of &laquo;Netty in Action&raquo;
categories: Tech
tags:
    - Java
    - Netty
password:
---


# Chapter 5 - ByteBuf
<!--more-->
## 5.1 The ByteBuf API

Advantages of *ByteBuf* API: 

1.  It’s extensible to user-defined buffer types.
2.  Transparent zero-copy is achieved by a built-in composite buffer type.
3.  Capacity is expanded on demand (as with the JDK StringBuilder).
4.  Switching between reader and writer modes doesn't require calling ByteBuffer's flip() method.
5.  Reading and writing employ distinct indices.
6.  Method chaining is supported.
7.  Reference counting is supported.
8.  Pooling is supported.

## 5.2 Class ByteBuf

ByteBuf has two indexes, *readerIndex* and *writerIndex*:

![ByteBuf](bytebuf.png)

The max capacity of a ByteBuf can be specified, moving writerIndex past this value will cause an exception

### 5.2.2 ByteBuf usage patterns
**Heap Buffers**
Store data in the JVM heap space.
**Direct Buffers**
Store data outside of heap, this is to avoid copying the buffer content to/from an intermediate buffer before/after a native I/O operation. This is **ideal** for network data transfer.
On the other side, it's harder to allocate and release than heap-based buffers.
**Composite Buffers**
It aggregates multiple **ByteBufs**. 
If we don't want to reallocate both bufferes for each message, it's a good fit. (if messages contain same body but different headers, we can keep the body and replace header every time)

## 5.3 Byte-level operations

1. We are able to access *ByteBuf* randomly by giving the index of the byte we want to get
![ByteBuf internal segmentation](bytebuf_internal_segmentation.png)
2. The segment that is already read is discardable, which will be cleaned by calling *discardReadBytes()*, which will increase the size of writable bytes, but it also causes memory coping by moving the readable bytes to the beginning of the byteBuf.
3. We can use *ByteBufProcessor* as a parameter of forEachByte() method of *ByteBuf* to do searching
4. We can copy a byteBuf or slice it.
5. There are many variants of *read* and *write* operations of *ByteBuf*
6. Netty uses the *PooledByteBufAllocator* by default, which can be changed via *ChannelConfig*

## 5.6 Reference counting

It tracks the number of active references to a specific object, starting with 0. 
As long as it's greater than 0, the object is guaranteed not to be released.