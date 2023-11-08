# Horizontally align something with something

```
// author: tabiasgeehuman
#let inline-with(select, content) = locate(loc => {
  let target = query(
    selector(select),
    loc,
  ).last().location().position().x
  let current = loc.position().x

  box(inset: (x: target - current + 0.3em), content)
})

#let inline-label(name) = [#line(length: 0%) #name]

#inline-with(selector(<start-c>))[= Common values]
#align(left, box[$
    #inline-label(<start-c>) "Circles"(0) =& 0 \
    lim_(x -> 1) "Circles"(0) =& 0
$])
```