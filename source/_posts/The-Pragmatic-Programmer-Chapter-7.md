---
title: The Pragmatic Programmer - Chapter 7
top: false
cover: false
toc: true
mathjax: true
date: 2020-07-14 23:16:12
summary:
tags: [Career]
categories: [Tech]
password:
---

# The Pragmatic Programmer - Chapter 7 While you are coding
<!--more-->
## Listen to your lizard brain

> The trick is first to notice it is happening, and then to work out why. 
>
> (Page 328). 

## Programming by coincidence

- Always be aware of what you are doing. Fred let things get slowly out of hand, until he ended up boiled, like the frog here. 
- Can you explain the code, in detail, to a more junior programmer? If not, perhaps you are relying on coincidences. 
- Don’t code in the dark. Build an application you don’t fully grasp, or use a technology you don’t understand, and you’ll likely be bitten by coincidences. If you’re not sure why it works, you won’t know why it fails. 
- Proceed from a plan, whether that plan is in your head, on the back of a cocktail napkin, or on a whiteboard.
- Rely only on reliable things. Don’t depend on assumptions. If you can’t tell if something is reliable, assume the worst. 
- Document your assumptions. Topic 23, Design by Contract, can help clarify your assumptions in your own mind, as well as help communicate them to others. 
- Don’t just test your code, but test your assumptions as well. Don’t guess; actually try it. Write an assertion to test your assumptions (see Topic 25, Assertive Programming). If your assertion is right, you have improved the documentation in your code. If you discover your assumption is wrong, then count yourself lucky.
- Prioritize your effort. Spend time on the important aspects; more than likely, these are the hard parts. If you don’t have fundamentals or infrastructure correct, brilliant bells and whistles will be irrelevant. 
- Don’t be a slave to history. Don’t let existing code dictate future code. All code can be replaced if it is no longer appropriate. Even within one program, don’t let what you’ve already done constrain what you do next—be ready to refactor (see Topic 40, Refactoring). This decision may impact the project schedule. The assumption is that the impact will be less than the cost of not making the change.



## Algorithm speed

## Refactoring

> disciplined technique for restructuring an existing body of code, altering its internal structure without changing its external behavior.
>
> -- Martin Fowler

### Refactor scenarios:

1. Duplication
2. Nonorthogonal design
3. requirement change
4. Performance
5. Outdated knowledge

### Refactor tips

1. Don’t try to refactor and add functionality at the same time. 
2. Make sure you have good tests before you begin refactoring. Run the tests as often as possible. That way you will know quickly if your changes have broken anything.
3. Take short, deliberate steps: move a field from one class to another, split a method, rename a variable. Refactoring often involves making many localized changes that result in a larger-scale change. If you keep your steps small, and test after each step, you will avoid prolonged debugging.

## Test to code

- Tests can definitely help drive development, but as with every drive, unless you have a destination in mind, you can end up going in circles.

- Contract

  If module A has two components A1 and A2, we should test: 

  1. A1's contract in full;
  2. A2's contract in full;
  3. A's contract

  If A1 and A2 contact tests passed but A's tests failed, then we are sure the problem is on A or how A uses A1/A2.

- Try to feed tests with real-world data;

- Have a magic URL which exposes diagnostic info of the system;

- Property-based testing can surprise you and help you

## Stay safe our there

1. Minimize attack surface area;
   1. Code complexity
   2. Input data
   3. Authorized user
   4. Unauthenticated services
   5. Output data
   6. Debug info
2. Principle of Least Privilege 
3. Secure Defaults 
   1. The default setting should be the most secure value
4. Encrypt Sensitive Data 
5. Maintain Security Updates

## Naming things

