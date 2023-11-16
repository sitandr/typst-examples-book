# Drawing
## `cetz`

Cetz is an analogue of LaTeX's `tikz`. Maybe it is not as powerful yet, but certainly easier to learn and use.

It is the best choice in most of cases you want to draw something in Typst.

```typ
#import "@preview/cetz:0.1.2"

#cetz.canvas(length: 1cm, {
  import cetz.draw: *
  import cetz.angle: angle
  let (a, b, c) = ((0,0), (-1,1), (1.5,0))
  line(a, b)
  line(a, c)
  set-style(angle: (radius: 1, label-radius: .5), stroke: blue)
  angle(a, c, b, label: $alpha$, mark: (end: ">"), stroke: blue)
  set-style(stroke: red)
  angle(a, b, c, label: n => $#{n/1deg} degree$,
    mark: (end: ">"), stroke: red, inner: false)
})
```

```typ
#import "@preview/cetz:0.1.2": canvas, draw

#canvas(length: 1cm, {
  import draw: *
  intersections(name: "demo", {
    circle((0, 0))
    bezier((0,0), (3,0), (1,-1), (2,1))
    line((0,-1), (0,1))
    rect((1.5,-1),(2.5,1))
  })
  for-each-anchor("demo", (name) => {
    circle("demo." + name, radius: .1, fill: black)
  })
})
```

```typ
#import "@preview/cetz:0.1.2": canvas, draw

#canvas(length: 1cm, {
  import draw: *
  let (a, b, c) = ((0, 0), (1, 1), (2, -1))
  line(a, b, c, stroke: gray)
  bezier-through(a, b, c, name: "b")
  // Show calculated control points
  line(a, "b.ctrl-1", "b.ctrl-2", c, stroke: gray)
})
```

```typ
#import "@preview/cetz:0.1.2": canvas, draw

#canvas(length: 1cm, {
  import draw: *
  group(name: "g", {
    rotate(45deg)
    rect((0,0), (1,1), name: "r")
    copy-anchors("r")
  })
  circle("g.top", radius: .1, fill: black)
})
```
