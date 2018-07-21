
<!-- ======================================================================= -->
# Order structures - examples

* i.e. examples of particular orders

<!-- ======================================================================= -->
## Number-based orders

### wikipedia, cardinal number

* cardinals, cardinal numbers - generalization of natural numbers
* used to measure the cardinality/size of sets

### wikipedia, ordinal number

* ordinal, ordinal number - generalization of natural numbers
* used to arrange a collection of objects one after another
* i.e. label the objects with distinct numbers
* used to describe the order-type of well-ordered sets

characteristic

* trichotomy - (a < b) xor (a > b) xor (a = b)
* transitive - (a < b) and (b < c) then (a < c)
* well-founded - every non-empty subset has a least element

### wikipedia, transfinite number

* numbers larger than all finite numbers
* not necessarily absolutely infinite
* transfinite cardinals and ordinals

### wikipedia, ranking

* ranking - a relation on a set of items such that
  for any pair of items, one is ranked higher than the other
* aka. a weak order, or a total preorder
* not necessarily a total order - items may have the same ranking (a tie)
* the rankings themselves are totally ordered - e.g. degrees of hardness
* reduce measures to a sequence of ordinal numbers

1224 ranking - standard competition ranking

* equal items receive the same ranking
* numbers are skipped according to the number of equal items
* i.e. leave gaps after the items (2-4)
* i.e. resolving the tie won't affect lower ranked items

1334 ranking - modified competition ranking

* i.e. leave gaps before the items (1-3)
* items need to score higher than all

1223 ranking - dense ranking

* i.e. no gaps behind (2-3) or before (1-2) the items

1234 ranking - ordinal ranking

* all items receive distinct ordinal numbers
* tie resolution may be random or (consistently) arbitrary

1,2.5,2.5,4 ranking - fractional ranking

* equal items receive mean ranking
* sum of rankings is the same under ordinal ranking

<!-- ======================================================================= -->
## Sequence-based orders

### wikipedia, alphabetical order

* short - alpha-order
* the system used to order strings of characters
* one of the methods of collation
* collation - written information in standard order

```
compare(s1,s2) being
  imax = min(#s1,#s2)
  for i in [1,imax] begin
    if(s1[i] < s2[i]) return (-1)
    if(s1[i] > s2[i]) return (+1)
  end
  if(#s1 < imax) return (-1)
  if(#s2 < imax) return (+1)
  return (0)
end
```

* conventions may be adopted depending on case-sensitivity, spaces, etc.
* results in nested sets - i.e. groups with same prefix

### wikipedia, lexicographical order

* short - lex-order
* aka. lexical order, lexicographic(al) order, lexicographic(al) product
* a generalization of the way words are alphabetically ordered
* i.e. ordering of sequences analogous to the alphabetical order

definition - lexicographic order

* given a totally-ordered finite set A - alphabet
* a total order on the sequences/words of A
* (w1 < w2) if (ai < bi) for the first (i)
* i.e. the lexical-order depends on prefixes
* pad the shorter word with "blanks"
* blanks - a theoretical element smaller than any in A
* i.e. a lex-order on `xN*`

### wikipedia, shortlex order

* aka. radix-order, length-lexicographic-order, genealogical-order
* a variant of the lexical-order used in e.g. combinatorics
* a word is smaller than any longer word
* i.e. primarily ordered by length
* e.g. system for representing numbers

<!-- ======================================================================= -->
## Other orders

### wikipedia, interval order

* a collection of intervals on the real numbers
* a partial order that corresponds to the left-to-right precedence
* i.e. (l1 < l2) => l1 is completely left of l2

formally

* a poset P := (X,<=)
* a bijection (f: X -> (L,R)) exists such that
* (xi < xj) in P when (Ri < Lj)

remarks

* unit-length intervals - i.e. (i,i+1)
* semiorders - subclass of interval orders in case of unit-length intervals
* interval graph - the complement of the interval-order's comparability graph

**TODO** - interval dimension
**TODO** - combinatorics

### wikipedia, containment order

* a poset that results from the subset-containment
* every poset is isomorphic to a containment order

remarks

* given poset a P = (X,<=)
* associate to each (b in X) the set
* X(b) = { a | (a <= b) for (a in X) }
* transitivity ensures that
* (X(a) subset-of X(b)) if (a <= b)

remarks

* serveral important poset classes arise as containment orders
* e.g. interval-containment-orders (note - not the same as interval-order)
* e.g. circle-orders - disks in the plane

<!-- ======================================================================= -->
## Social orders

### wikipedia, order of battle

* "order of appearance" referred-to "order of battle"
* shows hierarchical organization, command structure, strength, etc.

### wikipedia, order of precedence

* sequential hierarchy of nominal importance of persons
* an order of ceremonial or historical relevance
* occasionally aka. order of succession

examples

* ordered list of state leaders
* ordered list of former leaders

### wikipedia, order of succession

* sequence of people who hold a high office as head of state
* or sequence of people who hold a title of nobility
* answers the question - who ist next in line if one becomes incapacitated

succession planning

* the process for identifying and developing new leaders

### wikipedia, order of operations

* aka. order of precedence
* a collection of rules that allow to determine which operation to execute next
* parentheses > multiplication > addition
