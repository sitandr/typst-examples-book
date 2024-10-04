# Symbols

Multiletter words in math refer either to local variables, functions, text operators, spacing or _special symbols_.
The latter are very important for advanced math.

```typ
$
forall v, w in V, alpha in KK: alpha dot (v + w) = alpha v + alpha w
$
```

You can write the same with unicode:

```typ
$
∀ v, w ∈ V, α ∈ 𝕂: α ⋅ (v + w) = α v + α w
$
```

## Symbols naming

> See all available symbols list [there](https://typst.app/docs/reference/symbols/sym/).

### General idea

Typst wants to define some "basic" symbols with small easy-to-remember words, and build complex ones using
combinations. For example,

```typ
$
// cont — contour
integral, integral.cont, integral.double, integral.square, sum.integral\

// lt — less than, gt — greater than
lt, lt.circle, lt.eq, lt.not, lt.eq.not, lt.tri, lt.tri.eq, lt.tri.eq.not, gt, lt.gt.eq, lt.gt.not
$
```

I highly recommend using WebApp/Typst LSP when writing math with lots of complex symbols.
That helps you to quickly choose the right symbol within all combinations.

Sometimes the names are not obvious, for example, sometimes it is used prefix `n-` instead of `not`:

```typ
$
gt.nequiv, gt.napprox, gt.ntilde, gt.tilde.not
$
```


### Common modifiers

- `.b, .t, .l, .r`: bottom, top, left, right. Change direction of symbol.
    ```typ
    $arrow.b, triangle.r, angle.l$
    ```
- `.bl, tr`: bottom-left, top-right and so on. Where diagonal directions are possible.
- `.bar, .circle, .times, ...`: adds corresponding element to symbol
- `.double, .triple, .quad`: combine symbol 2, 3 or 4 times
- `.not` crosses the symbol
- `.cw, .ccw`: clock-wise and counter-clock-wise. For arrows and other things.
- `.big, .small`:
    ```typ
    $plus.circle.big plus.circle, times.circle.big plus.circle$
    ```
- `.filled`: fills the symbol
    ```typ
    $square, square.filled, diamond.filled, arrow.filled$
    ```

### Greek letters

Lower case letters start with lower case letter, upper case start with upper case.

For different versions of letters, use `.alt`

```typ
$
alpha, Alpha, beta, Beta, beta.alt, gamma, pi, Pi,\
pi.alt, phi, phi.alt, Phi, omicron, kappa, kappa.alt, Psi,\
theta, theta.alt, xi, zeta, rho, rho.alt, kai, Kai,
$
```

### Blackboard letters

Just use double of them. If you want to make some other symbol blackboard, use `bb`:

```typ
$bb(A), AA, bb(1)$
```

## Fonts issues

Default font is **New Computer Modern Math**. It is a good font, but there are some inconsistencies.

Typst maps symbol names to unicode, so if the font has wrong symbols, Typst will display wrong ones.

### Empty set
See example:

```typ
// nothing in default math font is something bad
$nothing, nothing.rev, diameter$

#show math.equation: set text(font: "Fira Math")

// Fira math is more consistent
$nothing, nothing.rev, diameter$
```

However, you can fix this with font feature:

```typ
#show math.equation: set text(features: ("cv01",))

$nothing, nothing.rev, diameter$
```

Or simply using "show" rule:

```typ
#show math.nothing: math.diameter

$nothing, nothing.rev, diameter$
```