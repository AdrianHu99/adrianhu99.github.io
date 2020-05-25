---
title: The Pragmatic Programmer-Chapter 2
top: false
cover: false
toc: true
mathjax: true
date: 2020-05-25 16:12:35
summary:
tags: [Career]
categories: [Tech]
password:
---



# Chapter 2 A Pragmatic Approach
<!--more-->
## Topic 8: The essence of good design

-   Good design is easier to change than bad design
-   If you can't make sure what form change will take, 1. try to make what you write replaceable; 2. treat this as a way to develop instincts

## Topic 9: DRY

-   DRY principle: Every piece of knowledge must have a single, unambiguous, authoritative representation within a system.
-   Do you find yourself making a change in multiple places, and in multiple different formats? If so, your code isn't dry
-   Not all code duplication is knowledge duplication
-   Comments can be duplicated as well. If the code can say what it does, why we need docs?
-   Whenever a module exposes a data structure, you're coupling all the code that uses that structure to the implementation of that module.
-   Foster an environment where it's easier to find and reuse existing stuff than to write it yourself.

## Topic 10: Orthogonality

-   Two things are orthogonal if changes in one do not affect any of the others
-   Two major benefits of orthogonal systems: increased productivity and reduced risk

	-   Changes are localized
	-   It promotes reuse
	-   Diseased code is isolated
	-   System is less fragile
	-   Better for testing
	-   Not tightly tied to a particular vendor

-   Ask yourself, if I dramatically change the requirements behind a particular function, how many modules are affected? The answer should be one for orthogonal system
-   How to maintain orthogonality:

	-   Keep your code decoupled - Law of Demeter, if you need to change an object's state, get the object to do it for you.
	-   Avoid global data
	-   Avoid similar functions - take a look at Strategy Pattern

## Topic 11: Reversibility

-   You can't plan for rapid change of architectural volatility. But what you can do is to make it easy to change
-   Hide third-party APIs behind your own abstraction layers
-   Break code into components

## Topic 12 Tracer Bullets

-   With tracer ability, we are able to track the progress
-   Advantages of trace code
	-   Users get to see something working early and tell you how close to the target
	-   Developers build a structure to work in
	-   An integration platform
	-   You have something to demonstrate
	-   You have a better feel for progress

-   Tracer code vs. Prototyping
	-   Tracer code makes the whole structure, while prototyping focuses on one part of the structure
	-   Prototyping generates disposable code, while tracer code is lean but complete.

## Topic 13: Prototypes and Post-it notes

-   How to use prototypes
	-   Correctness - may use dummy data
	-   Completeness - may function in a very limited case
	-   Robustness - Error checking is likely to be incomplete or missing
	-   Style - Won't have much in the way of comments or documentation

## Topic 14: Domain Languages

-   Internal domain language gives you the advantage of power your pipeline, but it limits the choice of the language;
-   External domain language needs a parser, but you don't have any restrictions on what language to use;
-   The rule is: Don't spend more effort than you save

## Topic 15: Estimate

-   Where do estimates come from?
	-   Understand what's being asked - the scope
	-   Build a model of the system - mental model for the project
	-   Break it into components
	-   Give each parameter a value - to work out which parameter have the most impact on the result
	-   Keep track of the estimations

-   PERT (Programming Evaluation Review Technique) usually has an optimistic, a most likely, and a pessimistic estimate