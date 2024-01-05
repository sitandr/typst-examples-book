# Setting limits

Sometimes we want to change how the default attaching should work. 

## Limits
For example, in many countries it is common to write definite integrals with limits below and above.
To set this, use `limits` function:

```typ
$
integral_a^b\
limits(integral)_a^b
$
```

You can set this by default using `show` rule:

```typ
#show math.integral: math.limits

$
integral_a^b
$

This is inline equation: $integral_a^b$
```

## Only display mode

Notice that this will also affect inline equations. To enable limits for display math only, use `limits(inline: false)`:

```typ
#show math.integral: math.limits.with(inline: false)

$
integral_a^b
$

This is inline equation: $integral_a^b$.
```

Of course, it is possible to move them back as bottom attachments:

```typ
$
sum_a^b, scripts(sum)_a^b
$
```


## Operations

The same scheme works for operations. By default, they are attached to the bottom and top:

```typ
$a =_"By lemme 1" b, a scripts(=)_+ b$
```

## Operators

When creating operators (upright text with proper spacing), you can set limits for _display mode_ at the same time:

```typ
$
op("liminf")_a, op("liminf", limits: #true)_a
$
```

Everything can be combined to create new operators:

```typ
#let liminf = math.op(math.underline(math.lim), limits: true)
#let limsup = math.op(math.overline(math.lim), limits: true)

$
liminf_(x->oo)
$
```

# Relates snippets
## Make every character upright when used in subscript

```typ
// author: emilyyyylime

$f_a, f_b, f^a, f_italic("word")$
#show math.attach: it => {
  import math: *
  if it.has("b") and it.b.func() != upright[].func() and it.b.has("text") and it.b.text.len() == 1 {
    let args = it.fields()
    let _ = args.remove("base")
    let _ = args.remove("b")
    attach(it.base, b: upright(it.b), ..args)
  } else {
    it
  }
}

$f_a, f_b, f^a, f_italic("word")$
```