## Fractional grids

For tables with lines of changing length, you can try using _grids in grids_. 

<div class="warning">
Don't use this where <a href="https://typst.app/docs/reference/model/table/#definitions-cell-colspan">cell.colspan and rowspan</a> will do.
</div>

```typ
// author: jimpjorps

#grid(
  columns: (1fr,),
  grid(
    columns: (1fr,)*2, inset: 5pt, stroke: 1pt, [hello], [world]
  ),
  grid(
    columns: (1fr,)*3, inset: 5pt, stroke: 1pt, [foo], [bar], [baz]
  ),
  grid.cell(inset: 5pt, stroke: 1pt)[abcxyz]
)
```

## Automerge adjacent cells with same values

This example works for adjacent cells horizontally, but it's not hard to upgrade it to columns too.

```typ
// author: tebine
#let merge(children, n-cols) = {
  let rows = children.chunks(n-cols)
  let new-children = ()
  for r in rows {
    // First group starts at index 0
    let i = 0 
    // Search next group
    while i < r.len() {
      // Group starts with one cell
      let c = r.at(i).body
      let n = 1
      for j in range(i+1, r.len()) {
        let c-next = r.at(j).body
        if c-next == c {
          // Add cell to group
          n += 1
        } else {
          break
        }
      }
      // Group is finished
      new-children.push(table.cell(colspan: n, c))
      i += n
    }
  }
  return new-children
}
#show table: it => {
  let merged = merge(it.children, it.columns.len())
  if it.children.len() == merged.len() { // trick to avoid recursion
    return it
  }
  table(columns: it.columns.len(), ..merged)
}
#table(columns: 2,
  [1], [2],
  [3], [3],
  [4], [5],
)
```

## Slanted column headers with slanted borders

```typ
// author: tebine
#let slanted(it, alpha: 45deg, len: 2.5cm) = layout(size => {
  let width = size.width
  let b = box(inset: 5pt, rotate(-alpha, reflow: true, it))
  let b-size = measure(b)
  let l = line(angle: -alpha, length: len)
  let l-width = len * calc.cos(alpha)
  let l-height = len * calc.sin(alpha)
  place(bottom+left, l)
  place(bottom+left, l, dx: width)
  place(bottom+left, line(length: width), dx: l-width, dy: -l-height)
  place(bottom+left, dx: width/2, b)
  box(height: l-height) // invisible box to set the height
})

#table(
  columns: 2,
  align: center,
  table.header(
    table.cell(stroke: none, inset: 0pt, slanted[*AAA*]),
    table.cell(stroke: none, inset: 0pt, slanted[*BBBBBB*]),
  ),
  [aaaaa], [bbbbbb], [c], [d],
)
```
