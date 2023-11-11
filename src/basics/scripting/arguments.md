# Advanced arguments
## Spreading arguments from list
```typ
#let func(a, b, c, d, e) = [#a #b #c #d #e]
#func(..(([hi],) * 5))
```

This may be super useful in tables:
```typ
#let a = ("hi", "b", "c")

#table(columns: 3,
  [test], [x], [hello],
  ..a
)
```

## Key arguments
The same idea works with key arguments:
```typ
#let text-params = (fill: blue, size: 0.8em)

Some #text(..text-params)[text].
```
