# Placing, Moving, Scale & Hide

This is **a very important section** if you want to do arbitrary things with layout,
create custom elements and hacking a way around current Typst limitations.

TODO: WIP, add text and better examples

# Place

> Link to [reference](https://typst.app/docs/reference/layout/place/)

```typ
#set page(height: 60pt)
Hello, world!

#place(
  top + right,
  square(
    width: 20pt,
    stroke: 2pt + blue
  ),
)
```

### Basic floating for place
```typ-norender
#set page(height: 150pt)
#let note(where, body) = place(
  center + where,
  float: true,
  clearance: 6pt,
  rect(body),
)

#lorem(10)
#note(bottom)[Bottom 1]
#note(bottom)[Bottom 2]
#lorem(40)
#note(top)[Top]
#lorem(10)
```

### dx
```typ
#set page(height: 100pt)
#for i in range(16) {
  let amount = i * 4pt
  place(center, dx: amount - 32pt, dy: amount)[A]
}
```

# Move
> Link to [reference](https://typst.app/docs/reference/layout/move/)

```typ
#rect(inset: 0pt, move(
  dx: 6pt, dy: 6pt,
  rect(
    inset: 8pt,
    fill: white,
    stroke: black,
    [Abra cadabra]
  )
))
```

# Scale
> Link to [reference](https://typst.app/docs/reference/layout/scale/)

```typ
#scale(x: -100%)[This is mirrored.]
```

```typ
A#box(scale(75%)[A])A \
B#box(scale(75%, origin: bottom + left)[B])B
```

# Hide
> Link to [reference](https://typst.app/docs/reference/layout/hide/)

```
Hello Jane \
#hide[Hello] Joe
```
