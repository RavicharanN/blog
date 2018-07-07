---
layout: post
title:  "Modifeid todd Coxeter methods"
date:   2018-06-21
excerpt: "GSoC'18 Week 5"
tag:
- markdown 
- syntax
- sample
- test
- jekyll
comments:  true
future:    true
published: true
---

## Idea 
Implement methods for modified coset enumeration. This is used to carry out the coset enumeration using a modied coset table. It is also called as the modified Todd-Coxeter procedure. The detailed implementation for all the methods has been provided in the Handbook

## Algorithm
All the algorithms for the modified methods are mentioned in the **Section 5.3.2 of the Handbook[1]**.

## Implementation

* All the modified methods have been implemetned along with the regualr methods with an additional modified keyword.
* For example, `modified_scan` is implemented as: 
  ```
  def modfied_scan(): 
    scan(..., modified=True)
  ```
 * A few methods which weren't much similar to the originla methods were implemented seperatetly. 

## Discussions 

* Implementation of methods with a `modified` keyword. 
* Move the existing `scan_and_fill` method to the `scan` method with a `fill` keyword as the implementation is pretty much the same.

## Trvial example 
Modified coset enumeration example.
```
>>> f = FpGroup(F, [x**3, y**3, x**-1*y**-1*x*y])
    >>> C = modified_coset_enumeration_r(f, [x])
    >>> for i in range(len(C.p)):
    ...     if C.p[i] == i:
    ...         print(C.table[i])
    [0, 0, 1, 2]
    [1, 1, 2, 0]
    [2, 2, 0, 1]
```

## PR
[Here](https://github.com/sympy/sympy/pull/14830) is the link to the PR 'Add implementation of the modified coset enumeration'. This, currently, still needs minor changes and will be finalised soon. 

## References 
* [1] Derek F.Holt, Bettina Fick, Eamonn A.O’Brian. Handbook of Computational Group Theory.
