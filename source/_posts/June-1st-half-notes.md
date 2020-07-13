---
title: June 1st half notes
top: false
cover: false
toc: true
mathjax: true
date: 2020-07-01 23:00:05
summary:
tags: [Sharing, Architecture]
categories: [Tech]
password:
---

# June 1st half note
<!--more-->
## Analyzing Architecture: Code Metrics

[link](https://www.youtube.com/watch?v=pELKNy8B5Nw&list=PLdsOZAx8I5umhnn5LLTNJbFgwA3xbycar&index=71)

## Cyclomatic complexity

It provides a numeric value representing the complexity of a function or method

V(G) = e - n + 2

e - number of edges

n - number of nodes

## Core metrics

1. number of classes per package - trend analysis
2. number of lines of source code (based on a context) - trend analysis
3. average complexity (1+ num_paths_thru_method; range: 2-4)
4. DIT (depth of inheritance tree) across components
5. WMC (weighted methods/class; sum of CC) - trend analysis
6. CE (efferent coupling count)
7. CA (afferent coupling count)

## Refactoring: Business Justification

[link](Refactoring: Business Justification)

When we want to break the monolith, from technical point of view, we can make these justifications:

1. components will be more decoupled;
2. each part will use fewer jvm resources;
3. deployment is limited to a separate application unit, thereby reducing deployment time and increasing robustness

But customers will not pay for that, how we can convince customers to pay for that? We can make these business justifications:

1. new functionality can be delivered faster to market;
2. overall application quality will be improved, thereby reducing bugs and costs of fixing them;
3. development costs with developing new functionality will be significantly reduced

Then the next question would be, once we decide to go this way, how do we measure to prove that it really works? We need business metrics:

1. for reducing overall costs:
   1. number of bugs
   2. actual development and testing hours
2. for better time to market:
   1. actual development and testing hours
   2. end-to-end calendar time from development to release
3. better user satisfaction:
   1. number of bugs
   2. number of reported bugs
   3. performance metrics and trends