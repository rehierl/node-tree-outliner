
<!-- ======================================================================= -->
# Formal language

Could this become relevant with regards to trees?

* nodes as symbols, sub-sequences as words
* reason - recognition via turing machines

<!-- ======================================================================= -->
## wikipedia, formal language

* a set of strings of symbols formed based on a set of rules
* alphabet - the set of symbols
* words - the strings formed based on the given rules
* well-formed words - words that belong to a particular language
* often defined by means of a formal grammar
* formal language theory - studies the syntactical aspects

used in ...

* mathematics, computer science and linguistics
* e.g. used to define the grammar of programming languages
* computational complexity theory, decision problems
* logic - used to define axiomatic systems

words over an alphabet

* alphabet (S/Sigma) - in general any set of elements
* alphabet - aka. vocabulary
* elements - aka. letters
* word - a finite sequence/string of letters
* word - formula, sentence
* S* - the set of all words over the alphabet S
* empty word - length - aka. e, eps, epsilon, lambda

different perspectives

* initially as a letter-word metaphor
* also used as word-sentence metaphor
* i.e. the underlying concept is the concatenation of symbols
* i.e. whether these symbols are understood as letters or as whole words

definition of "formal language"

* formal language L, alphabet S, L subset-of S*
* rules and constraints define well-formed expressions
* in general a (possibly infinite) set of finite-length strings

construction

* empty language - L := {}

specification formalisms

* e.g. formal grammar, regular expression, automaton, turing machine, etc.
* expressive power - comparison of formalisms
* recognizability - does a given word belong to L?
* comparability - do formalisms describe the same language?

operations on languages

* standard set operations - i.e. union, intersection, complement
* element-wise application of string operations
* e.g. concatenation, intersection, reversal
* operations used to study closure - i.e. is the result also in L?

formal theories/systems/proofs

* formal theory - a set of sentences expressed in a formal language
* deductive system - a set of transformation rules
* formal system - derive one expression from one or more other expressions
* formal proof - a sequence of well-formed formulas

interpretations and models

* formal languages are purely syntactic
* give meaning to the elements - i.e. semantics
* e.g. in logic by assigning truth values
* formal semantics - study of interpretations, model theory

<!-- ======================================================================= -->
## wikipedia, formal grammar

* a set of production rules for strings in a formal language
* used as the basis of a recognizer - i.e. (w in L)?

definition

* grammar G := (N,S,P,s)
* non-terminal symbols N - (G & N) is empty
* i.e. no (n in N) is in G itself
* terminal symbols S - (S & N) is empty
* a set of production rules P
* a start symbol (s in N)

remarks

* e.g. start symbol S, (1) S -> aSb, (2) S -> ab
* left-hand side (LHS), right-hand side (RHS)

chomsky hierarchy

* type-0: unrestricted grammars - turing machine
* type-1: context-sensitive grammars
* type-2: context-free grammars - ll parsers
* type-3: regular grammars - automata
* note - increasingly strict production rules

context-free grammars

* LHS of each rule has one non-terminal only
* context-free language, if it has a context-free grammar
* context-free => requires no additional context (i.e. terminal, non-terminal)
* context-free - recognition in O(n³)
* deterministic context-free - in O(n)

regular grammars

* context free + RHS restricted
* RHS is empty xor single terminal xor terminal+non-terminal
* recognition in O(n)

<!-- ======================================================================= -->
## wikipedia, chomsky hierarchy

* a containment hierarchy of classes of formal grammars
* does not include "recursive languages"

type-0: recursively enumerable

* turing machine
* no restrictions

type-1: context-sensitive

* (aAb -> acb) - i.e. replace some non-terminal
* linear-bounded, non-deterministic turing machine

type-2: context-free

* LHS - non-terminal only
* non-deterministic pushdown automaton
* LL parsers operate on slightly more restricted languages

type-3: regular

* RHS - empty, terminal, (terminal + non-terminal)
* finite state automaton
* obtained by regular expressions

<!-- ======================================================================= -->
## wikipedia, omega language

* aka. w-language
* w-language: a set of infinite-length sequences of symbols
* S* - the set of finite words over S
* S{w} - the set of all infinite words over S
* S{i} - the set of all finite and infinte words over S
* i.e. a w-language is a subset of S{w}

operations

* intersection, union
* left-concatenation - (K × L) for (K subset-of S*) and (L subset-of S{w})
* omega, infinite iteration
* pref(w): all finite prefixes of (w in S{w})
* limit - an w-word that is in the limit of a finite-length language

<!-- ======================================================================= -->
## wikipedia, omega-regular language

* aka. w-regular language
* recognizable by büchi-automata
* a class of w-languages
* generalize regular languages to infinite words

definition

* a w-language L is w-regular, if ...
* A{w} - A is the non-empty regular language, not containing eps
* (A × B) - regular language A, w-regular language B
* note - BA is not well-defined
* (A union B) - A and B are w-regular

remarks

* (w in A{w}) - infinitely often concatenate words in A

**SKIPPED** - equivalence to Büchi automata
