# Placing, Moving, Scale & Hide

This is **a very important section** if you want to do arbitrary things with layout,
create custom elements and hacking a way around current Typst limitations.

TODO: WIP, add text and better examples

# Place

_Ignore layout_, just put some object somehow relative to parent and current position.
The placed object _will not_ affect layouting

> Link to [reference](https://typst.app/docs/reference/layout/place/)

```typ
#set page(height: 60pt)
Hello, world!

#place(
  top + right, // place at the page right and top
  square(
    width: 20pt,
    stroke: 2pt + blue
  ),
)
```

### Basic floating with place
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

### dx, dy
Manually change position by `(dx, dy)` relative to intended.

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

Scale content _without affecting the layout_.

> Link to [reference](https://typst.app/docs/reference/layout/scale/)

```typ
#scale(x: -100%)[This is mirrored.]
```

```typ
A#box(scale(75%)[A])A \
B#box(scale(75%, origin: bottom + left)[B])B
```

# Hide

Don't show content, but leave empty space there.

> Link to [reference](https://typst.app/docs/reference/layout/hide/)

```typ
Hello Jane \
#hide[Hello] Joe
```
