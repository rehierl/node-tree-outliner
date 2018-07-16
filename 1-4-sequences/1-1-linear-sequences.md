
<!-- ======================================================================= -->
## linear sequence

* `(is-linear s), (is-linear s) := isLinear(s)`
* `isLinear(s)` := `(s[i] != s[j])` for any `i,j in [1,#s]` and `(i != j)`

A sequence is said to be linear, if the sequence holds unique/distinct elements
only. That is, a linear sequence contains none of its elements more than once.
As such, a linear sequence can be understood to define a simple set of elements.

In addition to that, a linear sequence defines an ordered set (see relations),
if the order of positions is understood to correspond with the set's order of
elements. Depending on the respective context, the semantics of the element
order may therefore be:

* `(s[i] before s[i+1])`, `(s[i] presequent-to s[i+1])`
* `(s[i+1] after s[i])`, `(s[i+1] subsequent-to s[i])`

The word "linear" therefore needs to be understood
with regards to the "linear order" it defines.

Note that set-based operators can be used in combination with linear sequences.
