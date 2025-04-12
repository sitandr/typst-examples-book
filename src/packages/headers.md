# Headers

## `hydra`: Contextual headers

We have discussed in `Typst Basics` how to get current heading with `query(selector(heading).before(here()))` for headers. However, this works badly for nested headings with numbering and similar things. For these cases there is `hydra`:

```typ
#import "@preview/hydra:0.6.1": hydra

#set page(height: 10 * 20pt, margin: (y: 4em), numbering: "1", header: context {
  if calc.odd(here().page()) {
    align(right, emph(hydra(1)))
  } else {
    align(left, emph(hydra(2)))
  }
  line(length: 100%)
})
#set heading(numbering: "1.1")
#show heading.where(level: 1): it => pagebreak(weak: true) + it

= Introduction
#lorem(50)

= Content
== First Section
#lorem(50)
== Second Section
#lorem(100)
```
