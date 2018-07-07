---
layout: post
title:  "Computation of Isomorpism between 2 groups"
date:   2018-06-11
excerpt: "Week 3-4 and Week 6"
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
Implement methods to compute the ismorphism between 2 groups. The current implementation is specific to finite groups and a few special cases of infinite groups where isomorphism could be decided easily. Given two groups `G` and `H`, the pretty straight-forward way to compute the isomorophism compute all the bijections between `G` and `H` and check is the bijections is a valid homomorphism from `G` to `H`. The complexity in computing the bijections would be `O(n!)`, where `n` is the order of the groups and to check if the bijection is a valid homomorohism would take O(n**2).
## Algorithm 
 An alternative and an efficient way to implement this can be done by an algorithm suggested by Robert Tarjan. The algorithm for for this methods of isomorphism computation has been mentioned in [this blog](https://www.naftaliharris.com/blog/groupiso/). The basic idea is to map a set the set of generators to a subset in `H` and check if the mapping can be extended to a bijective homomorphism. This would be more efficient than computing all the bijections and checking if the bijection is a valid homomorphism.

However, isomorphism could be directly decided between 2 group in the following cases:
* When the two group are cyclic and are of the same order.
* Infinite groups with differently ordered relators. 
* Infinite groups where a mapping could be made between the realtors. For example: 
    ```
    F1, a, b = free_group("a, b")
    F2, c, d = free_group("c, d")
    G = FpGroup(F1, [a**2])
    H = FpGroup(F2, [c**2])
    ```
    `G` and `H` here,  are clearly isomorphic

## Implementation (Week 3 and 4)

* `group_isomorphism` method which compute the isomorphism between the two groups.
* A default variable `isomorphism` is given as ann argument to the `group_isomorphism` method. When `isomorphism=False` this method returns a boolean(only checks if an isomorphism exists between the groups).When `isomorphism=True` it returns a 2-tuple, (boolean, instance of `GroupHomomorphism` class). 
* To calculate a subset of `H` we convert the group into a `PermutationGroup` isomorphic to it using the `_to_perm_group` method(only when `H` is an `FpGroup`).
* The raw implementation would be to loop through all the elements of the map and check if the map could extend a homomorphism. We check for a counter-example (f(g*h) != f(g)*f(h)) while extending the map. 
* If no counter example is found a homorohism from `G` to `H` is returned with `gens=G.generators` and `image=subset_of_H`.

**This PR has been closed due to a few minor issues with the implementation, the modified implementation is again done on Week-6**

## Implementation (Week 6)
* Slight modifications have been made to the implementations 'coz of a few issues with the implementation. 
* Intead of looking for the counter-example in the map, this implementation checks for the homomorphism between `G` and `H` defined on `gen = G.generators` and `images = subset_of_H` using the `_check_homomorphism` method and returns a homomorphism when if the homomorphism is bijective.
* As suggested by [valglad](https://github.com/valglad), more generalised way of check if a group is cyclic could be checking if the order is square free instead of prime.

## Discussions 

* Implementation of isomorphism for a few special cases of infinite groups. 
* Cyclic groups of same order are isomorphic.
* A method `is_isomorphic` has been implemented for convenient usage, which calls `group_isomorphism(..., isomorphism=False)` 

## Trvial example 
The word is recuded using the automaton as follows:
```
>>> F, a, b = free_group("a, b")
>>> G = FpGroup(F, [a**3, b**3, (a*b)**2])
>>> H = AlternatingGroup(4)
>>> check, T = group_isomorphism(G, H)
>>> check
True
>>> T(b*a*b**-1*a**-1*b**-1)
Permutation(0 2 3)
```

## PR
[Here](https://github.com/sympy/sympy/pull/14861) is the link to the PR 'Add methods for isomorphism computatio'. This, currently, still needs minor changes and will be finalised soon. 

## References 
* [1] [Blog](https://www.naftaliharris.com/blog/groupiso/) by [Naftali Harris](https://www.naftaliharris.com/) which talks about Tarjan's method for isomorpihsm computation.  

