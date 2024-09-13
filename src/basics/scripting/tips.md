# Tips

There are lots of elements in Typst scripting that are not obvious, but important. All the book is designated to show them, but some of them

## Equality

Equality doesn't mean objects are really the same, like in many other objects:

```typ
#let a = 7
#let b = 7.0
#(a == b)
#(type(a) == type(b))
```

That may be less obvious for dictionaries. In dictionaries **the order may matter**, so equality doesn't mean they behave exactly the same way:

```typ
#let a = (x: 1, y: 2)
#let b = (y: 2, x: 1)
#(a == b)
#(a.pairs() == b.pairs())
```

## Check key is in dictionary

Use the keyword `in`, like in `Python`:

```typ
#let dict = (a: 1, b: 2)

#("a" in dict)
// gives the same as
#(dict.keys().contains("a"))
```

Note it works for lists too:

```typ
#("a" in ("b", "c", "a"))
#(("b", "c", "a").contains("a"))
```