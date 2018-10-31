
<!-- ======================================================================= -->
# (loosely) contains/embedded

a node loosely contains a distant descendant -
a node strictly contains a child -
a set loosely contains a child set -
a set strictly contains a distant set -
both notions are "inverse" to each other -
needs to be fixed before we move on to content injection

**CLARIFICATION**
Set A is said to **(loosely) contain** set C
because C is a subset of A.

Note that this "contains" definition is with regards to the `subset-of` operator
and therefore needs to be understood as "contains the elements of" instead of
"contains as an element". In order to distinguish both notions, one could use
qualifiers similar to "loosely contains" (i.e. contains the elements of) and
"strictly contains" (i.e. contains as an element):

* A (loosely) contains C => C has no border in A.
* synonymous - resolved-into, merged-into
* B strictly contains C => C has a border in B.
* synonymous - an element of

Note that set A can be said to contain itself.
In contrary to that, set A neither contains D nor E.

**CLARIFICATION**
Set C is said to be **(loosely) embedded** into set A
because C is a strict subset of A.

Note that similar as before, the "loose" definition is with regards to C
being a subset of A and A having one or more additional elements. In contrary
to that, the "strict" counterpart would be if set C would be an element of A
in addition to A having one or more additional elements.

* C is (loosely) embedded into A => C has no border in A.
* C is strictly embedded into B => C has a border in B.

Note that set A can not be said to be embedded into itself.
That is, A is neither loosely nor strictly embedded into itself.

**CLARIFICATION**
"(strictly/loosely) contains" vs. "(strictly/loosely) embedded into":

* contains <=> (simple) subset
* embedded <=> strict subset
* embedded => contains
* if "embedded", then also "contains", but not necessarily vice versa
* loosely contains/embedded -> resolved/merged into
* strictly contains/embedded -> an element of

Note that the "contains" vs. "embedded" distinction is used to clarify whether
or not a super-set is known to have more elements than a sub-set.

Note that the "loosely" vs. "strictly" distinction could be used to clarify how
content was injected into some other content.
