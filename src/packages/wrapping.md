# Wrapping figures

The better native support for wrapping is planned, however, something is already possible via package:

```typ
#import "@preview/wrap-it:0.1.0": wrap-content, wrap-top-bottom

#set par(justify: true)
#let fig = figure(
  rect(fill: teal, radius: 0.5em, width: 8em),
  caption: [A figure],
)
#let body = lorem(40)
#wrap-content(fig, body)

#wrap-content(
  fig,
  body,
  align: bottom + right,
  column-gutter: 2em
)

#let boxed = box(fig, inset: 0.5em)
#wrap-content(boxed)[
  #lorem(40)
]

#let fig2 = figure(
  rect(fill: lime, radius: 0.5em),
  caption: [Another figure],
)
#wrap-top-bottom(boxed, fig2, lorem(60))
```

<div class="warning">Limitations: non-ideal spacing near warping, only top-bottom left/right are supported.</div>