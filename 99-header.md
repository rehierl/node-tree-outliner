
<!-- ======================================================================= -->
# Example - the header element

https://www.w3.org/TR/html5/common-idioms-without-dedicated-elements.html

```
<header>
  <h1> title </h1>
  <p> subtitle </p>
</header>
```

- intended to contain a section's heading
- the issue here - the `h1` element still is a sectioning node

```
<header>
  <title> page title </title>
  <p> subtitle </p>
</header>
```

- the `h1` element is not intended to represent a sectioning node
- neither is the `header` element intended to be such a node

```
<h1> section title </h1>
<header>
  <h1> a different section title </1>
</header>
```

- not defined to be a section's first node
- defined to refer to the nearest sectioning root/content element
- not defined to be used with heading elements

<!-- ======================================================================= -->
## issue with outline (toc)

```
<body>
  <h1> section title </h1>

  <header>
    <h1> document title </h1>
    <p> document subtitle </p>
  </header>
</body>
```

- the intended toc is

```
document title
  section title
```

- the actual toc is

```
section title
  document title
```

<!-- ======================================================================= -->
## possible issue with transformations

- same issue with the footer element
- this element also refers to the nearest sectioning root/content element
- must explicitly end all inner sections before the footer element

```
<body>
  <h1> section title </h1>

  <header>
    <h1> document title </h1>
    <p> document subtitle </p>
  </header>
</body>
```

- the intended result is

```
<body>
  <section>
    <h1> section title </h1>
  </section>

  <header>
    <h1> document title </h1>
    <p> document subtitle </p>
  </header>
</body>
```

- the probable result is however

```
<body>
  <section>
    <h1> section title </h1>

    <header>
      <h1> document title </h1>
      <p> document subtitle </p>
    </header>
  </section>
</body>
```

- that is, because the header element is
  associated with the h1 element's section
- however - the first element of heading content ...
