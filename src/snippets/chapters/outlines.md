# Outlines

# Outlines

> Lots of outlines examples are already available in [official reference](https://typst.app/docs/reference/meta/outline/)

## Table of contents

```typ
#outline()

= Introduction
#lorem(5)

= Prior work
#lorem(10)
```

## Outline of figures

```typ
#outline(
  title: [List of Figures],
  target: figure.where(kind: table),
)

#figure(
  table(
    columns: 4,
    [t], [1], [2], [3],
    [y], [0.3], [0.7], [0.5],
  ),
  caption: [Experiment results],
)
```

You can use arbitrary selector there, so you can do any crazy things.

<!--TODO: crazy example with labels and selector combinations-->

## Ignore low-level headings

```typ
#set heading(numbering: "1.")
#outline(depth: 2)

= Yes
Top-level section.

== Still
Subsection.

=== Nope
Not included.
```

## Set indentation

```typ
#set heading(numbering: "1.a.")

#outline(
  title: [Contents (Automatic)],
  indent: auto,
)

#outline(
  title: [Contents (Length)],
  indent: 2em,
)

#outline(
  title: [Contents (Function)],
  indent: n => [→ ] * n,
)

= About ACME Corp.
== History
=== Origins
#lorem(10)

== Products
#lorem(10)
```

## Replace default dots

```typ
#outline(fill: line(length: 100%), indent: 2em)

= First level
== Second level
```

## Make different outline levels look different

```typ
#set heading(numbering: "1.")

#show outline.entry.where(
  level: 1
): it => {
  v(12pt, weak: true)
  strong(it)
}

#outline(indent: auto)

= Introduction
= Background
== History
== State of the Art
= Analysis
== Setup
```

## Long and short captions for the outline

```typ
// author: laurmaedje
// Put this somewhere in your template or at the start of your document.
#let in-outline = state("in-outline", false)
#show outline: it => {
  in-outline.update(true)
  it
  in-outline.update(false)
}

#let flex-caption(long, short) = context if in-outline.get() { short } else { long }

// And this is in the document.
#outline(title: [Figures], target: figure)

#figure(
  rect(),
  caption: flex-caption(
    [This is my long caption text in the document.],
    [This is short],
  )
)
```