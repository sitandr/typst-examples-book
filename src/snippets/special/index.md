# Special documents
## Signature places
```typ
#block(width: 150pt)[
  #line(length: 100%)
  #align(center)[Signature]
]
```

## Presentations
See [polylux](../../packages/).


## Forms
### Form with placeholder
```typ
#grid(
  columns: 2,
  rows: 4,
  gutter: 1em,

  [Student:],
  [#block()#align(bottom)[#line(length: 10em, stroke: 0.5pt)]],
  [Teacher:],
  [#block()#align(bottom)[#line(length: 10em, stroke: 0.5pt)]],
  [ID:],
  [#block()#align(bottom)[#line(length: 10em, stroke: 0.5pt)]],
  [School:],
  [#block()#align(bottom)[#line(length: 10em, stroke: 0.5pt)]],
)
```

### Interactive
> Presentation interactive forms are coming! They are currently under heavy work by @tinger.
