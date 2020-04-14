---
title: Netty-in-Action-Chapter 7
top: false
cover: false
toc: true
mathjax: true
date: 2020-04-09 09:04:33
summary: Reading notes for Chapter 7 of &laquo;Netty in Action&raquo;
img: /medias/featureimages/netty_in_action.jpg
categories: Tech
tags:
    - Java
    - Netty
password:
---

# Chapter 7 - EventLoop

In 7.1, it introduces Executor's threading model in JDK, where there is a thread pool, and an available is selected from it to process a task, the thread will be returned back to the pool once the task is completed.
![Executor Logic](executor_logic.png)
It has performance issues when the number of threads increases, and can be very complex in larger scope.

In 7.2, it introduces *EventLoop* in Netty, the basic idea is that each task is an instance of **Runnable**. An *EventLoop* will only be associated to one thread that never changes, but it could be assigned to serve multiple *Channels*.
All I/O operations are handled by the thread that is assigned to the *EventLoop*.
The key difference is: **In Netty, the task assignment is seperated from the thread creation**, which makes it much  more flexible.

In 7.3, it gives us examples of how Java NIO implements scheduled tasks, and how Netty does that, the difference is Java NIO will have to create a thread pool, which is not ideal performance wise. For Netty, we are able to just use the *EventLoop* associated to that *Channel*, and make a scheduled task.

In 7.4, implementation details of Netty threading model is introduced. For an *EventLoop*, if incoming task is in the same thread assigned to that *EventLoop*, it will be executed, otherwise it will be put in a queue.
The EventLoop/thread allocation is shown in the screenshot below.
![EventLoop Allocation](eventloop_allocation.png)