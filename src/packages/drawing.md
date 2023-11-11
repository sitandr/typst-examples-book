# Drawing
## `cetz`

Cetz is an analogue of LaTeX's `tikz`. Maybe it is not as powerful yet, but certainly easier to learn and use.

It is the best choice in most of cases you want to draw something in Typst.

### Draw a graph in polar coords
```typ
#import "@preview/cetz:0.1.2": canvas, plot

#figure(
canvas(length: 1cm, {
  plot.plot(size: (5, 5),
    x-tick-step: 5,
    y-tick-step: 5,
    x-max: 20,
    y-max: 20,
    x-min: -20,
    y-min: -20,
    x-grid: true,
    y-grid: true,
    {
      plot.add(
        domain: (0,2*calc.pi),
        samples: 100,
        t => (13*calc.cos(t)-5*calc.cos(2*t)-2*calc.cos(3*t)-calc.cos(4*t), 16*calc.sin(t)*calc.sin(t)*calc.sin(t))
        )
    })
}), caption: "Plot made with cetz",)
```
