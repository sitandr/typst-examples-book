# Pretty things

## Set bar to the text's left
(also known as quote formatting)

```
+ #lorem(10)\
  #rect(fill: luma(240), stroke: (left: 0.25em))[
    *Solution:* #lorem(10)

    $ a_(n+1)x^n = 2... $
  ]
```
## Text on box top
```
// author: gaiajack
#let todo(body) = block(
  above: 2em, stroke: 0.5pt + red,
  width: 100%, inset: 14pt
)[
  #set text(font: "Noto Sans", fill: red)
  #place(
    top + left,
    dy: -6pt - 14pt, // Account for inset of block
    dx: 6pt - 14pt,
    block(fill: white, inset: 2pt)[*DRAFT*]
  )
  #body
]

#todo(lorem(100))
```