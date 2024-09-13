# Advanced arguments
## Spreading arguments from list

Spreading operator allows you to "unpack" the list of values into arguments of function:

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

# Managing arbitrary arguments

Typst allows taking as many arbitrary positional and key arguments as you want.

In that case function is given special `arguments` object that stores in it
positional and named arguments.

> Link to [reference](https://typst.app/docs/reference/foundations/arguments/)

```typ
#let f(..args) = [
  #args.pos()\
  #args.named()
]

#f(1, "a", width: 50%, block: false)
```

You can combine them with other arguments. Spreading operator will "eat" all remaining arguments:

```typ
#let format(title, ..authors) = {
  let by = authors
    .pos()
    .join(", ", last: " and ")

  [*#title* \ _Written by #by;_]
}

#format("ArtosFlow", "Jane", "Joe")
```

## Optional argument

_Currently the only way in Typst to create optional positional arguments is using `arguments` object:_

TODO
