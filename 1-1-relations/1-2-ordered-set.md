
<!-- ======================================================================= -->
# Ordered sets

simple sets of values

* a set is a group of values in which all values are different
* the values in a (simple) set have no order whatsoever
* a simple set has no first, no last, and no n-th value
* a set can essentially only answer the "element-of" question
* due to "no order" and the "in" operator, a set appears as a black box

ordered sets of values

* a (simple) set of elements that is paired with some order
* the order relation defines the relationship between the elements

countable sets, total/well order

* can be totally ordered in various ways
* well-orders (see ordinal numbers) - natural numbers, least element
* other - integers, not guaranteed to have a least element
* key definition of whether a total order is also a well order

<!-- ======================================================================= -->
## wikipedia, ranking

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
