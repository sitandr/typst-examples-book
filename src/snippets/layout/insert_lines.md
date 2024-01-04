# Lines between list items

```typ
/// author: frozolotl
#show enum.where(tight: false): it => {
  it.children
    .enumerate()
    .map(((n, item)) => block(below: .6em, above: .6em)[#numbering("1.", n + 1) #item.body])
    .join(line(length: 100%))
}

+ Item 1

+ Item 2

+ Item 3
```

The same approach may be easily adapted to style the enums as you want.