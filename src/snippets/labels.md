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

## Allow missing references

```typ
// author: Enivex
#set heading(numbering: "1.")

#let myref(label) = context {
    if query(label).len() != 0 {
        ref(label)
    } else {
        // missing reference
        text(fill: red)[???]
    }
}

= Second <test2>

#myref(<test>)

#myref(<test2>)
```
