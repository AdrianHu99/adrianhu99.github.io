---
title: June 2nd half notes
top: false
cover: false
toc: true
mathjax: true
date: 2020-07-01 23:00:15
summary:
tags: [Sharing, Architecture]
categories: [Tech]
password:
---

# June 2nd half note
<!--more-->


## Microservice pattern: API gateway

[link](https://hvalls.dev/posts/microservice-pattern-api-gateway)

About API Gateway:

- It acts as router
- It is the only entry point to our collection of microservices. This way, microservices are not needed to be public, anymore, but are behind an internal network and API Gateway is the responsible of making requests against a service or another one (Service Discovery)
- It acts as a data aggregator: API Gateway fetches data from several services and aggregate it to return a single rich response. Depending on the API consumer, data representation may change according the needs, and here is where Backend For Frontend (BFF) comes into play.
- It is a protocol abstraction layer: API Gateway can be exposed as a REST API or GraphQL or whatever, no matter what protocol or technology is being used internally to communicate with the microservices.
- Error management is centralized: When a service is not available, is getting too slow or something like that, API Gateway can provide data from cache, default responses or make smart decisions to avoid bottlenecks or fatal errors propagation. This keeps the circuit closed (Circuit Breaker) and makes the system more resilient and reliable.


## Automating safe hands off deployment

[link](https://aws.amazon.com/builders-library/automating-safe-hands-off-deployments/)

Question regrading pipeline as code: how to achieve version control for splunk alerts, reports, etc...?

## How to Make Yourself Study When You Have ZERO Motivation

[link](https://www.youtube.com/watch?v=9oWOsocN7qg)

1. Go out for a walk
2. Decide on a single task to work on
3. Clear to neutral - clean up your workspace
4. Use "low effort" hack - the blank page is the enemy


## Refactoring Patterns: Migration vs. Adaptation

[link](https://www.youtube.com/watch?v=DKPn0AcvLKo&list=PLdsOZAx8I5umhnn5LLTNJbFgwA3xbycar&index=68)

**Migration pattern:**

1. easier to roll back changes
2. a lot less risk
3. a lot more costs (keep both components need maintenance)
4. requires switching logic (not good if there are too many afferent components that are associated with this component)

**Adaption pattern:**

1. hard to roll back changes
2. a lot more risk
3. less costs (more of refactor instead of replacement)
4. no changes to calling components (afferent components)

**Conclusion**: it depends on the level of coupling, risk and costs.