# Labels
## Get chapter of label
```typ
#let ref-heading(label) = context {
  let elems = query(label)
  if elems.len() != 1 {
    panic("found multiple elements")
  }
  let element = elems.first()
  if element.func() != heading {
    panic("label must target heading")
  }
  link(label, element.body)
}

= Design <design>
#lorem(20)

= Implementation
In #ref-heading(<design>), we discussed...
```
