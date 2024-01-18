# Operators

> See [reference](https://typst.app/docs/reference/math/op/).

There are lots of built-in "text operators" in Typst math. This is a symbol that behaves very close to plain text. Nevertheless, it is different:

```typ
$
lim x_n, "lim" x_n, "lim"x_n
$
```
## Predefined operators

Here are all text operators Typst has built-in:

```typ
$
arccos, arcsin, arctan, arg, cos, cosh, cot, coth, csc,\
csch, ctg, deg, det, dim, exp, gcd, hom, id, im, inf, ker,\
lg, lim, liminf, limsup, ln, log, max, min, mod, Pr, sec,\
sech, sin, sinc, sinh, sup, tan, tanh, tg "and" tr
$
```

## Creating custom operator

Of course, there always will be some text operators you will need that are not in the list.

But don't worry, it is very easy to add your own:

```typ
#let arcsinh = math.op("arcsinh")

$
arcsinh x
$
```

### Limits for operators

When creating operators (upright text with proper spacing), you can set limits for _display mode_ at the same time:

```typ
$
op("liminf")_a, op("liminf", limits: #true)_a
$
```

This is roughly equivalent to

```typ
$
limits(op("liminf"))_a
$
```

Everything can be combined to create new operators:

```typ
#let liminf = math.op(math.underline(math.lim), limits: true)
#let limsup = math.op(math.overline(math.lim), limits: true)
#let integrate = math.op($integral dif x$)

$
liminf_(x->oo)\
limsup_(x->oo)\
integrate x^2
$
```
