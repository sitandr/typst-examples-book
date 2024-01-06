# Alignment

## General alignment

By default display math is center-aligned, but that can be set up with `show` rule:

```typ
#show math.equation: set align(right)

$
(a + b)/2
$
```

## Alignment points

When equations include multiple alignment points (&), this creates blocks of alternatingly _right-_ and _left-_ aligned columns.

In the example below, the expression `(3x + y) / 7` is _right-aligned_ and `= 9` is _left-aligned_.

```typ
$ (3x + y) / 7 &= 9 && "given" \
  3x + y &= 63 & "multiply by 7" \
  3x &= 63 - y && "subtract y" \
  x &= 21 - y/3 & "divide by 3" $
```

The word "given" is also left-aligned because `&&` creates two alignment points in a row, _alternating the alignment twice_.

`& &` and `&&` behave exactly the same way.
Meanwhile, "multiply by 7" is left-aligned because just one `&` precedes it.

**Each alignment point simply alternates between right-aligned/left-aligned.**