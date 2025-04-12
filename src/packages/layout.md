# Layouting

General useful things.

## Pinit: relative place by pins

The idea of [pinit](https://github.com/OrangeX4/typst-pinit) is pinning pins on the normal flow of the text, and then placing the content relative to pins.

```typ
#import "@preview/pinit:0.2.2": *
#set page(height: 6em, width: 20em)

#set text(size: 24pt)

A simple #pin(1)highlighted text#pin(2).

#pinit-highlight(1, 2)

#pinit-point-from(2)[It is simple.]
```

More complex example:

```typ
#import "@preview/pinit:0.2.2": *

// Pages
#set page(paper: "presentation-4-3")
#set text(size: 20pt)
#show heading: set text(weight: "regular")
#show heading: set block(above: 1.4em, below: 1em)
#show heading.where(level: 1): set text(size: 1.5em)

// Useful functions
#let crimson = rgb("#c00000")
#let greybox(..args, body) = rect(fill: luma(95%), stroke: 0.5pt, inset: 0pt, outset: 10pt, ..args, body)
#let redbold(body) = {
  set text(fill: crimson, weight: "bold")
  body
}
#let blueit(body) = {
  set text(fill: blue)
  body
}

// Main body
#block[
  = Asymptotic Notation: $O$

  Use #pin("h1")asymptotic notations#pin("h2") to describe asymptotic efficiency of algorithms.
  (Ignore constant coefficients and lower-order terms.)

  #greybox[
    Given a function $g(n)$, we denote by $O(g(n))$ the following *set of functions*:
    #redbold(${f(n): "exists" c > 0 "and" n_0 > 0, "such that" f(n) <= c dot g(n) "for all" n >= n_0}$)
  ]

  #pinit-highlight("h1", "h2")

  $f(n) = O(g(n))$: #pin(1)$f(n)$ is *asymptotically smaller* than $g(n)$.#pin(2)

  $f(n) redbold(in) O(g(n))$: $f(n)$ is *asymptotically* #redbold[at most] $g(n)$.

  #pinit-line(stroke: 3pt + crimson, start-dy: -0.25em, end-dy: -0.25em, 1, 2)

  #block[Insertion Sort as an #pin("r1")example#pin("r2"):]

  - Best Case: $T(n) approx c n + c' n - c''$ #pin(3)
  - Worst case: $T(n) approx c n + (c' \/ 2) n^2 - c''$ #pin(4)

  #pinit-rect("r1", "r2")

  #pinit-place(3, dx: 15pt, dy: -15pt)[#redbold[$T(n) = O(n)$]]
  #pinit-place(4, dx: 15pt, dy: -15pt)[#redbold[$T(n) = O(n)$]]

  #blueit[Q: Is $n^(3) = O(n^2)$#pin("que")? How to prove your answer#pin("ans")?]

  #pinit-point-to("que", fill: crimson, redbold[No.])
  #pinit-point-from("ans", body-dx: -150pt)[
    Show that the equation $(3/2)^n >= c$ \
    has infinitely many solutions for $n$.
  ]
]
```

## Margin notes

```````typ
#import "@preview/drafting:0.2.2": *

#let (l-margin, r-margin) = (1in, 2in)
#set page(
  margin: (left: l-margin, right: r-margin, rest: 0.1in),
)
#set-page-properties(margin-left: l-margin, margin-right: r-margin)

= Margin Notes
== Setup
Unfortunately `typst` doesn't expose margins to calling functions, so you'll need to set them explicitly. This is done using `set-page-properties` *before you place any content*:

// At the top of your source file
// Of course, you can substitute any margin numbers you prefer
// provided the page margins match what you pass to `set-page-properties`

== The basics
#lorem(20)
#margin-note(side: left)[Hello, world!]
#lorem(10)
#margin-note[Hello from the other side]

#lorem(25)
#margin-note[When notes are about to overlap, they're automatically shifted]
#margin-note(stroke: aqua + 3pt)[To avoid collision]
#lorem(25)

#let caution-rect = rect.with(inset: 1em, radius: 0.5em, fill: orange.lighten(80%))
#inline-note(rect: caution-rect)[
  Be aware that notes will stop automatically avoiding collisions if 4 or more notes
  overlap. This is because `typst` warns when the layout doesn't resolve after 5 attempts
  (initial layout + adjustment for each note)
]
```````

```````typ
#import "@preview/drafting:0.2.2": *

#let (l-margin, r-margin) = (1in, 2in)
#set page(
  margin: (left: l-margin, right: r-margin, rest: 0.1in),
)
#set-page-properties(margin-left: l-margin, margin-right: r-margin)

== Adjusting the default style
All function defaults are customizable through updating the module state:

#lorem(4) #margin-note(dy: -2em)[Default style]
#set-margin-note-defaults(stroke: orange, side: left)
#lorem(4) #margin-note[Updated style]


Even deeper customization is possible by overriding the default `rect`:

#import "@preview/colorful-boxes:1.1.0": stickybox

#let default-rect(stroke: none, fill: none, width: 0pt, content) = {
  stickybox(rotation: 30deg, width: width/1.5, content)
}
#set-margin-note-defaults(rect: default-rect, stroke: none, side: right)

#lorem(20)
#margin-note(dy: -25pt)[Why not use sticky notes in the margin?]

// Undo changes from last example
#set-margin-note-defaults(rect: rect, stroke: red)

== Multiple document reviewers
#let reviewer-a = margin-note.with(stroke: blue)
#let reviewer-b = margin-note.with(stroke: purple)
#lorem(20)
#reviewer-a[Comment from reviewer A]
#lorem(15)
#reviewer-b(side: left)[Comment from reviewer B]

== Inline Notes
#lorem(10)
#inline-note[The default inline note will split the paragraph at its location]
#lorem(10)
/*
// Should work, but doesn't? Created an issue in repo.
#inline-note(par-break: false, stroke: (paint: orange, dash: "dashed"))[
  But you can specify `par-break: false` to prevent this
]
*/
#lorem(10)
```````

```````typ
#import "@preview/drafting:0.2.2": *

#let (l-margin, r-margin) = (1in, 2in)
#set page(
  margin: (left: l-margin, right: r-margin, rest: 0.1in),
)
#set-page-properties(margin-left: l-margin, margin-right: r-margin)

== Hiding notes for print preview
#set-margin-note-defaults(hidden: true)

#lorem(20)
#margin-note[This will respect the global "hidden" state]
#margin-note(hidden: false, dy: -2.5em)[This note will never be hidden]

= Positioning
== Precise placement: rule grid
Need to measure space for fine-tuned positioning? You can use `rule-grid` to cross-hatch
the page with rule lines:

#rule-grid(width: 10cm, height: 3cm, spacing: 20pt)
#place(
  dx: 180pt,
  dy: 40pt,
  rect(fill: white, stroke: red, width: 1in, "This will originate at (180pt, 40pt)")
)

// Optionally specify divisions of the smallest dimension to automatically calculate
// spacing
#rule-grid(dx: 10cm + 3em, width: 3cm, height: 1.2cm, divisions: 5, square: true,  stroke: green)

// The rule grid doesn't take up space, so add it explicitly
#v(3cm + 1em)

== Absolute positioning
What about absolutely positioning something regardless of margin and relative location? `absolute-place` is your friend. You can put content anywhere:

#context {
  let (dx, dy) = (25%, here().position().y)
  let content-str = (
    "This absolutely-placed box will originate at (" + repr(dx) + ", " + repr(dy) + ")"
    + " in page coordinates"
  )
  absolute-place(
    dx: dx, dy: dy,
    rect(
      fill: green.lighten(60%),
      radius: 0.5em,
      width: 2.5in,
      height: 0.5in,
      [#align(center + horizon, content-str)]
    )
  )
}
#v(1in)

The "rule-grid" also supports absolute placement at the top-left of the page by passing `relative: false`. This is helpful for "rule"-ing the whole page.
```````

## Dropped capitals

> Get more info [here](https://github.com/EpicEricEE/typst-plugins/tree/master/droplet)

### Basic usage

```typ
#import "@preview/droplet:0.3.1": dropcap

#dropcap(gap: -2pt, hanging-indent: 8pt)[
  #lorem(42)
]
```

### Extended styling

```typ
#import "@preview/droplet:0.3.1": dropcap

#dropcap(
  height: 2,
  justify: true,
  gap: 6pt,
  transform: letter => context {
    let height = measure(letter).height

    grid(columns: 2, gutter: 6pt,
      align(center + horizon, text(blue, letter)),
      // Use "place" to ignore the line's height when
      // the font size is calculated later on.
      place(horizon, line(
        angle: 90deg,
        length: height + 6pt,
        stroke: blue.lighten(40%) + 1pt
      )),
    )
  }
)[
  #lorem(42)
]
```

## Headings for actual current chapter

> See [hydra](https://github.com/tingerrr/hydra)

```typ-nopreamble
#import "@preview/hydra:0.6.1": hydra

#set page(header: context hydra() + line(length: 100%))
#set heading(numbering: "1.1")
#show heading.where(level: 1): it => pagebreak(weak: true) + it

= Introduction
#lorem(750)

= Content
== First Section
#lorem(500)
== Second Section
#lorem(250)
== Third Section
#lorem(500)

= Annex
#lorem(10)
```