# Location and sizes

We talked already about display and inline math.
They differ not only by aligning and spacing, but also by size and style:

```typ
Inline: $a/(b + 1/c), sum_(n=0)^3 x_n$

$
a/(b + 1/c), sum_(n=0)^3 x_n
$
```

The size and style of current environment is described by Math Size, see [reference](https://typst.app/docs/reference/math/sizes).

There are for sizes:

- Display math size (`display`)
- Inline math size (`inline`)
- Script math size (`script`)
- Sub/super script math size (`sscript`)

Each time thing is used in fraction, script or exponent, it is moved several "levels lowers", becoming smaller and more "crapping". `sscript` isn't reduced father:

```typ
$
"display:" 1/("inline:" a + 1/("script:" b + 1/("sscript:" c + 1/("sscript:" d + 1/("sscript:" e + 1/f)))))
$
```

## Setting sizes manually

Just use the corresponding command:

```typ
Inine: $sum_0^oo e^x^a$\
Inline with limits: $limits(sum)_0^oo e^x^a$\
Inline, but like true display: $display(sum_0^oo e^x^a)$
```
