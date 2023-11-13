# Using spacing
Most time you will pass spacing into functions. There are special function fields that take only _size_.
They are usually called like `width, length, in(out)set, spacing` and so on.

Like in CSS, one of the ways to set up spacing in Typst is setting margins and padding of elements.
However, you can also insert spacing directly using functions `h` (horizontal spacing) and `v` (vertical spacing).

> Links to reference: [h](https://typst.app/docs/reference/layout/h/), [v](https://typst.app/docs/reference/layout/v/).

```typ
Horizontal #h(1cm) spacing.
#v(1cm)
And some vertical too!
```

# Absolute length units
> Link to [reference](https://typst.app/docs/reference/layout/length/)

Absolute length (aka just "length") units are not affected by outer content and size of parent.
```typ
#set rect(height: 1em)
#table(
  columns: 2,
  [Points], rect(width: 72pt),
  [Millimeters], rect(width: 25.4mm),
  [Centimeters], rect(width: 2.54cm),
  [Inches], rect(width: 1in),
)
```

## Relative to current font size
`1em = 1 current font size`:

```typ
#set rect(height: 1em)
#table(
  columns: 2,
  [Centimeters], rect(width: 2.54cm),
  [Relative to font size], rect(width: 6.5em)
)

Double font size: #box(stroke: red, baseline: 40%, height: 2em, width: 2em)
```

It is a very convenient unit, so it is used a lot in Typst.

## Combined

```typ
Combined: #box(rect(height: 5pt + 1em))

#(5pt + 1em).abs
#(5pt + 1em).em
```


# Ratio length
> Link to [reference](https://typst.app/docs/reference/layout/ratio/)

`1% = 1% from parent size in that dimension`

```typ
This line width is 50% of available page size (without margins):

#line(length: 50%)

This line width is 50% of the box width: #box(stroke: red, width: 4em, inset: (y: 0.5em), line(length: 50%))
```

# Relative length
> Link to [reference](https://typst.app/docs/reference/layout/relative/)

You can _combine_ absolute and ratio lengths into _relative length_:

```typ
#rect(width: 100% - 50pt)

#(100% - 50pt).length \
#(100% - 50pt).ratio
```

# Fractional length
> Link to [reference](https://typst.app/docs/reference/layout/fraction/)

Single fraction length just takes _maximum size possible_ to fill the parent:

```typ
Left #h(1fr) Right

#rect(height: 1em)[
  #h(1fr)
]
```

There are not many places you can use fractions, mainly those are `h` and `v`.

## Several fractions
If you use several fractions inside one parent, they will take all remaining space
_proportional to their number_:

```typ
Left #h(1fr) Left-ish #h(2fr) Right
```

## Nested layout

Remember that fractions work in parent only, don't _rely on them in nested layout_:

```typ
Word: #h(1fr) #box(height: 1em, stroke: red)[
  #h(2fr)
]
```