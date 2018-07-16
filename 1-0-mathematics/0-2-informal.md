
<!-- ======================================================================= -->
# Informal definitions

* `-Inf, -Infinity` := negative infinity
* `+Inf, +Infinity` := positive infinity

synonyms, groups

* frequently, names or identifiers are grouped together using (/)
* "name1/name2" may be used to express that ...
* 1) "name1" and "name2" are understood to be synonymous
* 2) the context in which such a pattern is used applies to all names

labels/indexes

* `l:a`:= entity `a` can be referred to by using the specified label `l`
* `a:i, ai` := some value `a` that corresponds with index/identifier `i`

number intervals/ranges

* `[a,*] := [a,+Inf)`, likewise `[*,b] := (-Inf,b]`
* `i in [a,*]` := value `i` may have any value from `a` to `+Infinity`

regular expression like patterns

* `<e>{a,b}` := expression `<e>` repeated `a` to `b` times, for `[a,b] in [0,*]`
* `<e>{a,*}` := `<e>` may appear `[a,+Inf)` times
* `<e>{0,1}, <e>{?}` := `<e>` may appear once, or not at all
* `<e>{0,*}, <e>{*}` := `<e>` may appear `i` times, for `i in [0,+Inf]`
* `<e>{1,*}, <e>{+}` := `<e>` may appear `i` times, for `i in [1,+Inf]`
* `<e>{a,a}, <e>{a}` := `<e>` must appear exactly `a` times
* `<e>{1}, <e>{1,1}` := `<e>`
