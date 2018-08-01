
<!-- ======================================================================= -->
# Type theory (TT)

<!-- ======================================================================= -->
## wikipedia, type theory

* a class of formal systems
* every "term" has a "type"
* operations are restricted to terms of a certain type
* closely related to "type systems"

concept

* terms such as "4", "2+2", etc.
* each term has a type "2:Nat"
* conversion rules, reduction rule
* "2+2" can be reduced to "4"

difference to set theory (ST)

* ST is built on top of logic
* ST - an element can belong to multiple sets
* TT - terms generally belong to one type only
* ST encodes numbers as sets - see hereditary sets
* TT encodes numbers as functions

normalization

* normal form - a term that can not be reduced any further
* strongly normalizing system - all terms have a normal form
* i.e. such a system has no cycles
* weakly normalizing - some orders of reductions may loop
* open term - a term that has parameters - e.g. "x+2"
* closed term - a term without parameters
* element - closed terms that reduce to the same normal form
* convertible - two terms can be reduced to the same term

dependent types

* a type that depends on another term or type
* e.g. the type returned by a function which depends on the function's argument

inductive types

* i.e. a set of base types
* type constructors - used to generate types with certain properties

<!-- ======================================================================= -->
## wikipedia, type system

* a set of rules that assigns a type to constructs of a computer program
* e.g. variables, expressions, functions, modules, etc.
* used to enforce consistency - i.e. no type errors
* static and/or dynamic checking
* aims to analyze the flow of values
* in general used to remove logic errors

type error

* i.e. verify type safety
* division-by-zero is by itself type safe
* will be left to produce a runtime error

<!-- ======================================================================= -->
## wikipedia, logic error

* causes a program to operate incorrectly
* without abnormal termination - i.e. crash
* a program with logic errors is valid in the language
* e.g. "a+b/2" instead of "(a+b)/2"
