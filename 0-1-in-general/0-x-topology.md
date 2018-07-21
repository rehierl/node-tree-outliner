
<!-- ======================================================================= -->
# Topology

<!-- ======================================================================= -->
## wikipedia, topology

* study of space under continuous deformations
* i.e. stretching, crumpling, bending, not tearing, not gluing
* studied based upon topological space - open sets, collection of subsets
* developed out of geometry and set theory
* had become a major branch of mathematics

introduction

* objects taken from a topological space
* the study of properties invariant under transformation
* topological spaces show up in several branches of mathematics
* i.e. topology is a unifying idea in mathematics
* squares and circles have properties in common
* i.e. it is more important how objects are put together
* i.e. one must know what the relevant properties really are

topologies on sets

* T is referred to as a topology on X, if
* 0 - X is a set and T a family of subsets
* 1 - {} and X are elements of T
* 2 - (a + b) and (a & b) in T for any (a,b in T)

remarks

* topology tells how the elements of a set relate spatially
* (X,T) is referred to as a "topological space"
* i.e. similar to "ordered set", a set paired with a "topology"
* the elements of T are all "open sets" in X
* a subset of X is a "closed set", if its complement is in T
* a subset may be open, closed, or both (aka. clopen set)

general topology

* aka. point-set topology
* deals with the set-theoretic definitions and constructions
* i.e. core topological aspects
* 1 - continuity - take nearby points to nearby points
* 2 - compactedness - sets can be covered by smaller ones
* 3 - connectedness - sets can not be divided into distant parts

<!-- ======================================================================= -->
## wikipedia, net

* aka. moore-smith sequence
* generalizes the notion of a sequence
* a sequence is a function/map (f) such that
* 1 - the domain is the set of natrual numbers
* 2 - the codomain is a topological space
* however, the following two conditions are not equivalent
* 1 - (f) is continuous (in topological sense)
* 2 - the composition of (f) converges to f(x) (in sequential sense)

definition

* (f: A -> X) is a "net" - i.e. the elements in A are mapped to X
* (A,>=) is a directed set, and (X,T) a topology

remarks

* every non-empty totally ordered set is directed
* e.g. the natural numbers - i.e. every sequence is a net

<!-- ======================================================================= -->
## wikipedia, open set

* the generalization of an open interval on real numbers
* i.e. a set is open if it has no boundaries
* the union/intersection of open sets is open

example

* A: (x^2 + y^2 = r^2) - a circle, a boundary set
* B: (x^2 + y^2 < r^2) - an open set
* (A + B): (x^2 + y^2 <= r^2) - a closed set

remarks

* topology includes a notion of nearness
* without having a clear definition of distance
* two points are distinguishable, if an open set contains one, but not both
* i.e. two points are considered to be "near" if they can not be distinguished
* e.g. (x +/- epsilon) for some (x in Real)

<!-- ======================================================================= -->
## wikipedia, closed set

* a set whose complement is open
* contains all its limit points
* alt. a closed set is equal to its closure
* (a + b) and (a & b) are closed if a and b are closed
* {} and X are closed

<!-- ======================================================================= -->
## wikipedia, clopen set

* aka. closed-open set
* a clopen set is both - open and closed
* note - the definitions are not mutually exclusive

examples

* {} and X are both open sets
* both are elements of the topological space
* both are also complement to each other
* hence, both are also closed

remarks

* connected - the topological space only contains {} and X as clopen sets
