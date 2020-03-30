---
title: Advanced Programming in Unix - Chapter 2
top: false
cover: false
toc: true
mathjax: true
date: 2020-03-30 14:58:45
summary: Reading notes for Chapter 2 of &laquo;Advanced Programming in Unix&raquo;
categories: Tech
tags:
    - Operating System
img: /medias/featureimages/advanced_programming_in_unix_cover.png
password:
---

# UNIX Standardization and Implementations





## Unix Standardization

#### FIPS

FIPS stands for Federal Information Processing Standard.

## Unix System Implementations

#### Linux

Linux is an OS that provides rich UNIX programming environment, and is freely available under the GPU Public License. 
Linux is distributed by often being the first OS that supports new hardware.

## Limits

There are two types of limits: 
	1. Runtime limits (`how many characters in a filename`)
	2. Compile-time limits (`what's the largest value of a short integer`)


NOTE: a particular value may not be included in the header if the actual value depends on the available memory on the system, POSIX.1 provides sysconf, pathconf and fpathconf for us to call during runtime. There is a problem: some values do not have upper bound.

## sysconf, pathconf and fpathconf

They return `-1` and set `errno` to EINVAL if the name isn't one of the appropriate constants. 
Some names can return either the value of the variable or an indication that it's indefinite, where return value is `-1` but no change on `errno`.


## Differences between Standards

There are differences between ISO C standard and POSIX.1. If it happens, POSIX.1 defers to the ISO C standard. 

Example: 
	1. `clock_t`, where ISO C does not provide unit, but POSIX.1 does.
    2. ISO C standards specifies a function but not as strongly as POSIX.1