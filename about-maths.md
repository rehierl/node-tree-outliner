
<!-- ======================================================================= -->
## Sections

```
<- root <-        path-of-nodes         -> leaf ->
<- parent-of                           child-of ->

... x N x N x ... x N x N x ...  (down) belongs-to
      x                      
      S                         (up) contains-node
```

* `s in S` is a section, `S` is the set of all sections
* The tree traversal connects each node with a section
  => first, last => order => `s = (n1,n2,...ni) in NxNx...xN`.
* In general, sections may have any length => `i in [0,+Infinity)`
* All sections in `S` may have any length => different lengths
* If `(n,s) in NxS`, then `s(k) = n` for some `k in [1,+Infinity)`
* Any node is directly (strictly) related to a section => `NxS`, left-total
* If `(n,s) in NxS`, then `(s,n) in SxN` (not left-total, empty section)
* The nodes of a section do not have to be located on the same path
  (special case - a single HTML node, a container with a single node, etc.).
* Two empty sections are not necessarily identical
  => each section depends on a sectioning node (introduces/declares a section)
  => two different sectioning nodes may each introduce its own empty section

strictly related-to

* A node strictly belongs to a section, iif it is strictly related to it.
* A node is located inside of a section, if it strictly belongs to it.
  However, a node may also be seen to be located inside of a section, if it
  loosely belongs to it - this depends on someone's point of view.
* A section strictly contains a node, iif the node is related to it => `SxN`.

loosely related-to

* Any descendant `d` of node `n`, which is strictly related to section `s`
  (i.e. `(n,s) in NxS`), *loosely belongs to* `s`.
* A section `s` loosely contains node `n`, iif `n` loosely belongs to `s`.

```
example
=======
... section-A begins here
<parent-B>          => is located inside
  <descendant-C>    => is located inside
  </descendant-C>
</parent-B>
... section-A ends here
```
* Any ancestor `a` of node `n`, which is strictly related to section `s`
  (i.e. `(n,s) in NxS`), *does not loosely belong to* `s`.
* However, `a` may still be strictly related to it (i.e. `(a,s) not in NxS`).

```
example
=======
<root>        => does not belong to section-A
... section-A begins here
  <node-B>    => is located inside
  </node-B>
... section-A ends here
</root>
```

<!-- ======================================================================= -->
## Conclusion

<!-- ======================================================================= -->
## A memory hook

```
<- root <-          path-of-nodes          -> leaf ->
<- parent-of                              child-of ->

... x N x N x ... x N x N x ...    (down) belongs-to
      x             x
... x S x S x ... x S x S x ...    (up) contains-node

<- parent-section                      sub-section ->
```
