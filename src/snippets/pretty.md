# Pretty things
## Set bar to the text's left
(also known as quote formatting)

```typ
#let line-block = rect.with(fill: luma(240), stroke: (left: 0.25em))

+ #lorem(10) \
  #line-block[
    *Solution:* #lorem(10)

    $ a_(n+1)x^n = 2... $
  ]
```

## Text on box top
```typ
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

## Book Ornament

```typ
// author: thevec

#let parSepOrnament = [\ \ #h(1fr) $#line(start:(0em,-.15em), end:(12em,-.15em), stroke: (cap: "round", paint:gradient.linear(white,black,white))) #move(dx:.5em,dy:0em,"🙠")#text(15pt)[🙣] #h(0.4em) #move(dy:-0.25em,text(12pt)[✢]) #h(0.4em) #text(15pt)[🙡]#move(dx:-.5em,dy:0em,"🙢") #line(start:(0em,-.15em), end:(12em,-.15em), stroke: (cap: "round", paint:gradient.linear(white,black,white)))$ #h(1fr)\ \ ];

#lorem(30)
#parSepOrnament
#lorem(30)
```
