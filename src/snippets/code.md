# Code formatting

## Inline highlighting

```
#let r = raw.with(lang: "r")

This can then be used like: #r("x <- c(10, 42)")
```

## Tab size

```````
#set raw(tab-size: 8)
```tsv
Year	Month	Day
2000	2	3
2001	2	1
2002	3	10
```
```````

## Theme

See [reference](https://typst.app/docs/reference/text/raw/#parameters-theme)

## Enable ligatures for code

```
#show raw: set text(ligatures: true, font: "Cascadia Code")

Then the code becomes `x <- a`
```

## Advanced formatting

See [packages]() section.
