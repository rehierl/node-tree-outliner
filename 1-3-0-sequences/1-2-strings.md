
<!-- ======================================================================= -->
# Strings

<!-- ======================================================================= -->
## wikipedia, strings

* a sequence of characters or more general a list of some other data
* formal - a finite sequence of symbols over the non-empty alphabet (A)
* no assumption is made about the nature of the symbols within A
* `#s`, `|s|`, length := the number of symbols within the string
* A{n} := the set of strings of length `n`
* A* := the countably infinite set of strings of any length
* A* - aka. Kleene closure of A
* B is a formal language over A, if (B subset-of A*)

concatenation: (A*,A*) -> A*

* synonymous - concatenation, concat, add, append, &, +
* associative, non-commutative
* e, eps, epsilon, "" - the empty string, the identity element
* `(s × e) = (e × s) = s`
* i.e. append and A* form a monoid
* length() defines a monoid homomorphism from A* to [0,*]
* `t` is a substring-of `s`, iff `u` and `v` exist such that `s=(u×t×v)`
* substring-of defines a partial order on A*
* i.e. the least element element is eps

prefix, suffix

* `t` is a prefix-of `s`, iff `u` exists such that `s = (t × u)`
* `t` is a suffix-of `s`, iff `u` exists such that `s = (u × t)`
* strict/proper prefix/suffix if (u != eps)
* any prefix/suffix is also a substring
* prefix-of and suffix-of form prefix-orders

remarks

* rotation - `t = uv` is a rotation of `s = vu`
* note - `u` and `v` are themselves strings, not symbols
* reversal - `t = abc` is reverse to `s = cba`
* note - all symbols in `t` are in reversed order
* note - (rotation != reversal)

**SKIPPED** - implementation-specific aspects

<!-- ======================================================================= -->
## wikipedia, string operations

* empty string - "", e, eps, epsilon, lambda, etc.
* concatenation - (s × t), associative
* language - an (in)finite set of strings
* set operations with languages - e.g. union, intersection, etc.
* (S × T) := { (s × t) | (s in S) and (t in T) }
* (S × {}) => {}, whereas (S × {e}) => S
* Alpha(s) := the set of characters of a string
* Alpha(S) := the set of characters of a language
* (/see/ "set of elements E()" /)

substitution

* 1) substitution of characters acts as the basis
* f(a)=L', where (L' subset-of S*)
* 2) extended to strings
* f(eps)=eps, f(sa)=f(s)×f(a)
* for (s in S*) and (a in S)
* 3) extended to entire languages
* f(L) = { f(s) | (s in L) }
* regular and context-free languages are closed under substitution

homomorphism

* each character is replaced by a single string - i.e. f(a)=s
* homomorphic image - f(L)
* inverse image - f°(L) = { w | f(w)=s }

projection

* remove all characters not in S
* pi(s)=eps if (s=eps)
* pi(t) if (s=ta) and (a !in S)
* pi(t)a if (a in S)

right-quotient

* truncate a character from a string
* (sa)/b = s if (a=b), eps if (a!=b)

**SKIPPED** - syntactic relation

right-cancellation

* remove the first occurrence of c from s
* search for c, beginning at the end
* (sa)÷c = s if (a=b), (s÷c)a if (a!=b)

prefixes

* prefix-of s: pref(s) = { t | (s=tu) for (t,u in S*) }
* prefix-closure: pref(L) = { t | (s=tu), (s in L) and (t,u in S*) }
* prefix-closed: (pref(L) = L)
* idempotent: pref(pref(L)) = pref(L)
* prefix relation: (s <= t) iff (s in pref(t))
* i.e. an example of prefix-order

<!-- ======================================================================= -->
## wikipedia, concatenation

* used in formal language theory and computer programming
* the operation of joining strings "end-to-end"
* i.e. one end of a string joined with one end of another
* e.g. "ab" × "cd" = "abcd"

extensions

* sets-of-strings often referred to as "formal language"
* string-with-set: (s × T) := { (s × t) | (t in T) }
* set-with-string: (S x t) := { (s × t) | (s in S) }
* sets-of-strings: (S × T) := { (s × t) | (s in S) and (t in T) }

<!-- ======================================================================= -->
## wikipedia, substring

* a contiguous sequence of characters within a string
* e.g. ("bc" substring-of "abcd")
* "subsequence" is a generalization of "substring"
* e.g. ("bd" subsequence-of "abcd")

definition

* s := s1 .. sn, t := t1 .. tm
* where (t1 = (si+1)), .., (tm = (si+m))
* where (0 <= i) and ((m+i) <= n)

remarks

* prefix: ("ab" prefix-of "abcd")
* suffix: ("cd" suffix-of "abcd")
* border: ("a" border-of "abca")
* superstring: contains all (s in {s1 .. sk})
* substring: a prefix of a suffix -or- a suffix of a prefix
* (substring -> subsequence), but not vice versa
* aka. subwords (US), factors (EU)

<!-- ======================================================================= -->
## wikipedia, linguistics

affix, adfix

* word: in linguistics a freestanding unit
* morpheme: may or may not be freestanding
* affix: a morpheme attached to a word stem
* e.g. infixes, prefixes (un-), suffix (-ed)
* adfix: either a pre- or a suffix

infix, prefix, suffix

* infix: an affix inserted inside a word stem
* prefix: placed before a word stem
* suffix: placed after a word stem
