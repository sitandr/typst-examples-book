# Advanced arguments

## Spreading arguments from list

```
#let func(a, b, c, d, e) = [#a #b #c #d #e]
#func(..(([hi],) * 5))
```

This may be super useful in tables:

```
#let a = ("hi", "b", "c")

#table(columns: 3,
  [test], [x], [hello],
  ..a
)
```