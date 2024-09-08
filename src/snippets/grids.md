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
