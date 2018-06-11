---
layout: post
title:  "Using automaton for word reduction in Rewriting Systems"
date:   2018-05-28
excerpt: "GSoC'18 Week 1 and 2"
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
The current implementation of the word reduction in rewriting systems is implemented by reducing the words based on the set of rules (S). In the previous implementation of the  Knuth-Bendix process , most of the time is taken up in reducing the words to equivalent irreducible forms using the set of rules. Using the automaton for the word reduction method helps in completing the task of word reduction in a much more efficient way.

## Algorithm 
This [paper](https://www.sciencedirect.com/science/article/pii/S0747717108800934) talks about the implementation of the automaton in word reduction. From the given set of rules S, we construct the states of the finite state machine(M). The proper prefixes of the left-hand rules are the accept states of the automaton and the complete left-hand rules are the dead states of the automaton, i.e, the non-final states in M are essentially the left-hand side of the rules, because, the left-hand side of the rules can further be reduced. The transitions are defined from one state to another and thus the automaton is constructed.

Word Reduction: A rule (x, y) in S says that an element 'x' that can be reduced to 'y'. Consider the example, w = abc with the set of rules S and an automaton M. Let b be the first occurrence of a left-hand rule in w from the given set of rules S. Thus this can be reduced into another form based on the corresponding rule. As mentioned in the handbook, when the word w is fed into the automaton M, and when we read the symbol b, we find a dead state for the prefix ab of w. Then we locate a rule (b, x) that belongs to S such that b can be reduced to another symbol x. This process is repeated until the word, w, cannot be reduced further.

## Implementation

* `StateMachine` class to store the details about the finite state automata. This is basically a collection of states that belong to the fsm. 
* `State` class which essentially stores the detials of every state. All the transitions of a particular state are stored in a dictionary. Every state has an attribute indicatiting the type of the state(start, accept or final). 
* `construct_automaton` is implemented as a method of the `RewritingSystem` class. This method constructs the automaton using the current set of rules defined for the rewriting system.
* `reduce_using_automaton` is a method which reduces the word using the automaton constructed. 

## Discussions 

The above section is just a raw implemenation of the word reduction using automaton. Further discussions led to the further optimisation and accuracy of the implentation. A method `compute_inverse_rules` has been added to compute the inverse rules for a given set of rules. This was primiarily done because of the difference in the rules produced by the system in Python2 and Python3. The basic idea is to derive the inverse rules for a given rule and add it to the automaton. 

Another method `add_to_automaton` has been added to add new states to the automaton whenever a new rule is added to the system. This method also modifies (only if necesary) the transistions at the states previously present in the automaton. 

## Trvial example 
The word is recuded using the automaton as follows:
```
>>> from sympy.combinatorics.fp_groups import FpGroup
>>> from sympy.combinatorics.free_groups import free_group
>>> F, a, b = free_group("a, b")
>>> G = FpGroup(F, [a*b*a**-1*b**-1])
>>> a, b = G.generators
>>> R = G._rewriting_system
>>> R.reduce_using_automaton(b**2*a*b**3)
a*b**5
```

## PR
[Here](https://github.com/sympy/sympy/pull/14735) is the link to the PR 'Add automaton for word reduction in rewriting systems'. This, currently, still needs minor changes and will be finalised soon. 

## References 
* [1] Derek F.Holt, Bettina Fick, Eamonn A.O'Brian. Handbook of Computational Group Theory.
* [2] [Article](https://www.sciencedirect.com/science/article/pii/S0747717108800934) on The Use of Knuth-Bendix Methods to Solve the Word Problem in Automatic Groups by D.B.A.Epstetein, D.F.Holt and S.E.Rees.  

