---
layout: post
title:  "GSoC 2018 Final Report"
date:   2018-08-14
excerpt: "This post summarizes the work done on the Group Theory part of the combinatorics module during 2018 summers as a part of the GSoC programme"
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

This page summarizes the work done on the Group Theory part of the combinatorics module during 2018 summers as a part of the GSoC programme. Much deeper description of the work done during the summers could be found on my [blog posts](https://ravicharann.github.io/blog/posts/).

## About me

I am a 3rd-year student at Indian Institute of Information Technology, Allahabad pursuing B.Tech in IT. I work on MacOS (Sierra currently) with Visual Studio Code as my primary code editor. 

## Project abstract

This project mainly aimed at improving the Group Theory part of the combinatorics module. It was majorly divided into 3 phases : 

* *Phase1:* <br>
&nbsp;&nbsp;&nbsp;1. Implementing an automaton for word reduction <br>
&nbsp;&nbsp;&nbsp;2. Implementation of algorithms to compute and check the isomorphism between 2 groups. 

* *Phase2:* <br>
&nbsp;&nbsp;&nbsp;1. Implementation of the modified Todd-Coxeter algorithm for subgroup presentation.<br>
&nbsp;&nbsp;&nbsp;2. Polycyclic presentation and corressponding methods.**(Work in progress)**

* *Phase3:* <br>
&nbsp;&nbsp;&nbsp;1. Computing the quotient of groups<br>
&nbsp;&nbsp;&nbsp;2.Computing map from subgroup(Defined on a new `FreeGroup`) to the parent group.<br>
&nbsp;&nbsp;&nbsp;3.Compute the coset representative of a given coset.

## Pull requests 

### Merged
#### Implementation of an automaton for word reduction:

For word reduction in rewriting system, the Knuth Benedix process consumed a lot of time in converting the sub-words to the equivalent irreducible forms. A much better way was to make use of an automaton for the word reduction. The idea suggested in this [paper](https://www.sciencedirect.com/science/article/pii/S0747717108800934) was taken as reference for the implementation. This PR took around a month to get merged as it went through many changes in the implementation. <br>
* Blog post link: [Word Reduction](https://ravicharann.github.io/blog//Word-Reduction/)<br>
* PR link: [#14735](https://github.com/sympy/sympy/pull/14735)

#### Computation of isomorphism between 2 given groups

Implemented methods to compute the isomorphism between 2 groups. The current implementation is specific to finite groups and a few special cases of infinite groups where isomorphism could be decided easily. The basic idea was to map a set the set of generators to a subset in one group and check if the mapping can be extended to a bijective homomorphism.

* Blog post link: [Isomorphism computation](https://ravicharann.github.io/blog//Isomorphism/)
* PR link: [#14861](https://github.com/sympy/sympy/pull/14861)

#### Modified Todd-Coxeter methods

Implemented methods for modified coset enumeration. This is used to carry out the coset enumeration using a modified coset table, also called the modified Todd-Coxeter procedure. References for the implementation of the modified methods were taken from 'The Handbook of Computational Group Theory'. 

* Blog post link: [Modfied coset enumeration](https://ravicharann.github.io/blog//modif-todd-coxeter/)
* PR link: [#14830](https://github.com/sympy/sympy/pull/14830)

#### Compute map from subgroup to parent group

Implemented methods to compute an injective map from subgroup(defined on a new `FreeGroup`) to the parent group. Initially, this wasn't mentioned in the proposal but we realized that it was essential for the computation of the quotient groups where generators and the relators of the subgroup should be defined on the same `FreeGroup` as that of the parent group. 

A simple backtracking algorithm for the computation of the coset-representative for a given coset table was also included as a part of this PR.

* Blog post link: [Injective homomorphism from subgroup to parent group](https://ravicharann.github.io/blog//misc/) **This post contains the work of Quotient methods as well along with it**
* PR link: [#14968](https://github.com/sympy/sympy/pull/14968)

### Unmerged 

#### Quotient methods

A method to compute the subgroup quotients was implemented. The presentation of the quotient G/H is given by adding the generators of G to the relators of H.

Another method to compute the largest abelian quotient was included as a part of this PR. The maximal abelian quotient is simply the quotient of the group with its commutator subgroup.

Additionally, the isomorphism method was modified to compute all(or just check) the epimorphisms/the monomorphisms as specified by the user. This was also included as a part of this PR.

**(This PR is almost ready and will be merged soon.)**

* Blog post link: [Subgroup quotient methods](https://ravicharann.github.io/blog//misc/)
* PR link: [#14981](https://github.com/sympy/sympy/pull/14981)


#### Polycyclic groups and presentations

The work done so far on this PR include the computation of the polycyclic series of a given `FpGroup`, solving word problem for Polycyclic groups using the collection algorithm. Elementary methods of the `PcGroup`(polycyclic group) class such as computation of the polycyclic generating sequence, computation of relative orders...etc.

The work that needs to be done includes the computation polycyclic presentation of a given polycyclic group and the existing methods in this PR should be tested as well.

* Blog post link: [Polycyclic groups - Part1](https://ravicharann.github.io/blog//polycylic-groups-part1/), [Polycycylic groups - Part2](https://ravicharann.github.io/blog//misc/)
* PR link: [#14879](https://github.com/sympy/sympy/pull/14879)

## Future Work

* The work that needs to be done majorly includes testing of the polycyclic methods and the computation of the polycyclic presentation.


## Conclusion

This summer was really fun and had been a great learning experience. I'd like to thank my mentors [Valeriia](https://github.com/valglad), [Kalevi](https://github.com/jksuon) and [Aaron](https://github.com/asmeurer) for being really helpful throughout the project. I would mostly stick around after the GSoC period as well and continue contributing to Sympy, hopefully, I exploring the other modules as well. Overall, I've had a really great experience working with Sympy this summer.
