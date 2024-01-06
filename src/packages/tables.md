# Tables
## Tablex: general purpose tables library

```typ
#import "@preview/tablex:0.0.7": tablex, rowspanx, colspanx

#tablex(
  columns: 4,
  align: center + horizon,
  auto-vlines: false,

  // indicate the first two rows are the header
  // (in case we need to eventually
  // enable repeating the header across pages)
  header-rows: 2,

  // color the last column's cells
  // based on the written number
  map-cells: cell => {
    if cell.x == 3 and cell.y > 1 {
      cell.content = {
        let value = int(cell.content.text)
        let text-color = if value < 10 {
          red.lighten(30%)
        } else if value < 15 {
          yellow.darken(13%)
        } else {
          green
        }
        set text(text-color)
        strong(cell.content)
      }
    }
    cell
  },

  /* --- header --- */
  rowspanx(2)[*Username*], colspanx(2)[*Data*], (), rowspanx(2)[*Score*],
  (),                 [*Location*], [*Height*], (),
  /* -------------- */

  [John], [Second St.], [180 cm], [5],
  [Wally], [Third Av.], [160 cm], [10],
  [Jason], [Some St.], [150 cm], [15],
  [Robert], [123 Av.], [190 cm], [20],
  [Other], [Unknown St.], [170 cm], [25],
)
```

```typ
#import "@preview/tablex:0.0.7": tablex, hlinex, vlinex, colspanx, rowspanx

#pagebreak()
#v(80%)

#tablex(
  columns: 4,
  align: center + horizon,
  auto-vlines: false,
  repeat-header: true,

  /* --- header --- */
  rowspanx(2)[*Names*], colspanx(2)[*Properties*], (), rowspanx(2)[*Creators*],
  (),                 [*Type*], [*Size*], (),
  /* -------------- */

  [Machine], [Steel], [5 $"cm"^3$], [John p& Kate],
  [Frog], [Animal], [6 $"cm"^3$], [Robert],
  [Frog], [Animal], [6 $"cm"^3$], [Robert],
  [Frog], [Animal], [6 $"cm"^3$], [Robert],
  [Frog], [Animal], [6 $"cm"^3$], [Robert],
  [Frog], [Animal], [6 $"cm"^3$], [Robert],
  [Frog], [Animal], [6 $"cm"^3$], [Robert],
  [Frog], [Animal], [6 $"cm"^3$], [Rodbert],
)
```

```typ
#import "@preview/tablex:0.0.7": tablex, gridx, hlinex, vlinex, colspanx, rowspanx

#tablex(
  columns: 4,
  auto-lines: false,

  // skip a column here         vv
  vlinex(), vlinex(), vlinex(), (), vlinex(),
  colspanx(2)[a], (),  [b], [J],
  [c], rowspanx(2)[d], [e], [K],
  [f], (),             [g], [L],
  //   ^^ '()' after the first cell are 100% ignored
)

#tablex(
  columns: 4,
  auto-vlines: false,
  colspanx(2)[a], (),  [b], [J],
  [c], rowspanx(2)[d], [e], [K],
  [f], (),             [g], [L],
)

#gridx(
  columns: 4,
  (), (), vlinex(end: 2),
  hlinex(stroke: yellow + 2pt),
  colspanx(2)[a], (),  [b], [J],
  hlinex(start: 0, end: 1, stroke: yellow + 2pt),
  hlinex(start: 1, end: 2, stroke: green + 2pt),
  hlinex(start: 2, end: 3, stroke: red + 2pt),
  hlinex(start: 3, end: 4, stroke: blue.lighten(50%) + 2pt),
  [c], rowspanx(2)[d], [e], [K],
  hlinex(start: 2),
  [f], (),             [g], [L],
)
```

```typ
#import "@preview/tablex:0.0.7": tablex, colspanx, rowspanx

#tablex(
  columns: 3,
  map-hlines: h => (..h, stroke: blue),
  map-vlines: v => (..v, stroke: green + 2pt),
  colspanx(2)[a], (),  [b],
  [c], rowspanx(2)[d], [ed],
  [f], (),             [g]
)
```

```typ
#import "@preview/tablex:0.0.7": tablex, colspanx, rowspanx

#tablex(
  columns: 4,
  auto-vlines: true,

  // make all cells italicized
  map-cells: cell => {
    (..cell, content: emph(cell.content))
  },

  // add some arbitrary content to entire rows
  map-rows: (row, cells) => cells.map(c =>
    if c == none {
      c  // keeping 'none' is important
    } else {
      (..c, content: [#c.content\ *R#row*])
    }
  ),

  // color cells based on their columns
  // (using 'fill: (column, row) => color' also works
  // for this particular purpose)
  map-cols: (col, cells) => cells.map(c =>
    if c == none {
      c
    } else {
      (..c, fill: if col < 2 { blue } else { yellow })
    }
  ),

  colspanx(2)[a], (),  [b], [J],
  [c], rowspanx(2)[dd], [e], [K],
  [f], (),             [g], [L],
)
```

```typ
#import "@preview/tablex:0.0.7": gridx

#gridx(
  columns: 3,
  rows: 6,
  fill: (col, row) => (blue, red, green).at(calc.rem(row + col - 1, 3)),
  map-cols: (col, cells) => {
    let last = cells.last()
    last.content = [
      #cells.slice(0, cells.len() - 1).fold(0, (acc, c) => if c != none { acc + eval(c.content.text) } else { acc })
    ]
    last.fill = aqua
    cells.last() = last
    cells
  },
  [0], [5], [10],
  [1], [6], [11],
  [2], [7], [12],
  [3], [8], [13],
  [4], [9], [14],
  [s], [s], [s]
)
```

## Tablem: markdown tables

> See documentation [there](https://github.com/OrangeX4/typst-tablem)

Render markdown tables in Typst.

```typ
#import "@preview/tablem:0.1.0": tablem

#tablem[
  | *Name* | *Location* | *Height* | *Score* |
  | ------ | ---------- | -------- | ------- |
  | John   | Second St. | 180 cm   |  5      |
  | Wally  | Third Av.  | 160 cm   |  10     |
]
```

### Custom render

```typ
#import "@preview/tablex:0.0.6": tablex, hlinex
#import "@preview/tablem:0.1.0": tablem

#let three-line-table = tablem.with(
  render: (columns: auto, ..args) => {
    tablex(
      columns: columns,
      auto-lines: false,
      align: center + horizon,
      hlinex(y: 0),
      hlinex(y: 1),
      ..args,
      hlinex(),
    )
  }
)

#three-line-table[
  | *Name* | *Location* | *Height* | *Score* |
  | ------ | ---------- | -------- | ------- |
  | John   | Second St. | 180 cm   |  5      |
  | Wally  | Third Av.  | 160 cm   |  10     |
]
```

### Tbl

Compact syntax and some new features:

```````typ
#import "@preview/tbl:0.0.4"
#show: tbl.template.with(box: true, tab: "|")

```tbl
      R | L
      R   N.
software|version
_
     AFL|2.39b
    Mutt|1.8.0
    Ruby|1.8.7.374
TeX Live|2015
```
```````