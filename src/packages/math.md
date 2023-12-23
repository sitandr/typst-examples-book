# Math

## `physica`

Physica (Latin for _natural sciences_) provides utilities that simplify
otherwise complex and repetitive mathematical expressions in natural sciences.

Its [manual](https://github.com/Leedehai/typst-physics/blob/master/physica-manual.pdf)
provides a full set of demonstrations of how the package could be helpful.

| | |
|:--|:--|
|[Differentials](#differentials)| |
|[Ordinary derivatives](#ordinary-derivatives)|[Partial derivatives](#partial-derivatives)|
|[Vectors and vector fields](#vectors-and-vector-fields)|[Matrices](#matrices)|
|[Dirac braket notations](#dirac-braket-notations)|[Reduced Planck constant (hbar)](#reduced-planck-constant-hbar)|
|[Tensors](#tensors)|[Braces](#braces)|
|[Matrix transpose](#matrix-transpose)|[Matrix dagger](#matrix-dagger-conjugate-transpose)|
|[Isotopes](#isotope)|[Taylor expansion](#taylor-expansion)|

### Differentials

Function `dd(*args, **kwargs)` excels at typesetting multi-variable
differentials.
- positional arguments:
    - the variable names,
    - optionally followed by a universal order number e.g. `2`, `n`, or an array
    of individually-applied order numbers e.g. `[2,3]`, `[m n, lambda+1]`. If
    the order number is missing or fewer than needed, the number defaults to
    one.
- optional named arguments:
    - `d`: the differential symbol [default: upright `d`].
    - `p`: the product symbol connecting the components [default: none].
    - `compact`: only effective if `p` is none. If `#true`, it will remove the
    TeXBook-advised thin spaces between the d-units inside the multi-variable
    differential.

```typ
#import "@preview/physica:0.9.1": dd, vb
#set math.equation(numbering: "(1)")

#table(
  columns: (auto, auto), align: horizon, stroke: none,

[$ dd(f) quad dd(f,2) quad dd(x,y,2) quad dd(vb(x),t,[3,]) $], // (1)

// The order number is one by default, if it's missing or fewer than variables.
[$ dd(x,y) quad dd(x,y,2)quad dd(x,y, [2,]) \
    dd(x,y, [2,3]) quad dd(x,y,z, [2,3]) $], // (2)

// Like Typst's "dif", there is a thin space between the function and the
// differential symbol, as advised by the TeXBook.
[$ integral_S f(r,theta) dd(r,theta) $], // (3)

// Surreally complex.
[$ dd(x_1,hat(y),(z^1), [[1,1], rho+1, n_1]) $], // (4)

// Changing the "d" symbol.
[$
dd(x, d:d) quad dd(x,y, d:delta) quad dd(x,y, 2, d:Delta) quad dd(x,y, d:upright(D))
$], // (5)

// Joining the d-units with, say the exterior product symbol.
[$ dd(x,y,z, p:and) $], // (6)
)
```

Variations `var` (or `variation`), and difference `difference`. They are
shorthands for `dd(..., d:delta)` and `dd(..., d:Delta)`, respectively.
```typ
#import "@preview/physica:0.9.1": var, difference

$ var(f), var(x, y), difference(f), difference(x, y) $
```

### Ordinary derivatives

Function `dv(f, *args, **kwargs)` helps you assemble ordinary derivatives with
ease.
- `f`: the function, which can be omitted,
- positional `*args`:
    - the variable name,
    - optionally followed by an order number e.g. `2` [default: `1`].
- named `**kwargs`(all optional):
    - `d`: the differential symbol [default: upright `d`].
    - `s`: the "slash" separating the numerator and denominator
    [default: `#none`], by default it produces the normal fraction form. The
    most common non-default is a slash, so as to create a flat form that fits
    inline.

```typ
#import "@preview/physica:0.9.1": dv, vb
#set math.equation(numbering: "(1)")

#table(
  columns: (auto, auto), align: horizon, stroke: none,

  [$ dv(,x), dv(,x, 2), dv(f,x, k+1) $], // (1)
  [$ dv(,vb(r)), dv((f+g),vb(r)_e, 2) $], // (2)

  // Changing the "d" symbol.
  [$ dv(,x, d:delta), dv(,x, 2, d:Delta), dv(vb(u),t, 2, d: upright(D)) $], // (3)

  // Use "s" to render a slash.
  [$ dv(f,x,k, s:slash) $], // (4)
)
```

### Partial derivatives

Partial derivatives `pdv(f, *args, **kwargs)` can handle mixed orders. It
attempts to compute the total order based on partial orders specified by the
user.
- `f`: the function, which can be #none or omitted,
- positional `*args`:
    - the variable names,
    - optionally followed by a universal order number e.g. `2`, or an array of individually-applied order numbers e.g. `[2,3]`, `[m n, lambda+1]`. If the
    order number is missing or fewer than needed, the number defaults to one.
- named `**kwargs` (all optional):
    - `s`: the "slash" separating the numerator and denominator
    [default: `#none`], by default it produces the normal fraction form. The
    most common non-default is a slash, so as to create a flat form that fits
    inline.
    - `total`: the user-specified total order that appears at the top. If
    absent, physica will try computing the total number for you. You may
    override it with `total` if necessary.

```typ
#import "@preview/physica:0.9.1": pdv, vb
#set math.equation(numbering: "(1)")

#table(
  columns: (auto, auto, auto), align: horizon, stroke: none,

  [$ pdv(,x), pdv(,t, 2), pdv(,xi,[k]) $], // (1)
  [$ pdv(f,vb(r)), pdv(phi,vb(r)_e, 2) $], // (2)

  // The total order is automatically calculated.
  [$ pdv(,x,y), pdv(f,x,y, 2) $], // (3)

  // The order number is one by default, if it's missing or fewer than variables.
  [$ pdv(,x,y, [2,]), pdv(,x,y, [1,2]) $], // (4)

  // If the variable has a superscript, wrap it in (...) to avoid confusion
  // with the order number.
  [$ pdv(f,(x^1),(x^2), 2) $], // (5)

  // Use "s" to render a slash.
  [$ pdv(f,x,y, s:slash) $], // (6)

  // The monotonic adder can handle symbols with best effort.
  [$ pdv(,x,y,z,t, [1, xi, 2, eta+2]) $], // (7)

  // Override the automatic addition with "total".
  [$ pdv(,x,y,z, [xi n, n-1], total:(xi+1)n) $], // (8)
)
```

### Vectors and vector fields

In addition to Typst's built-in `vec()` for column vectors, physica provides
`vecrow()` for row vectors for symmetry. In addition, physica provides `vb()`,
`vu()`, `va()` to typset vectors.

```typ
#import "@preview/physica:0.9.1": vecrow, vb, vu, va

$ vecrow(alpha, b) quad vb(a), vb(mu_1) quad vu(a), vu(mu_1) quad va(a), va(mu_1) $
```

Operators in vector fields: gradient `grad`, divergence `div`, curl `curl`, and
Laplacian `laplacian`.

```typ
#import "@preview/physica:0.9.1": grad, div, curl, laplacian, vb

$ grad phi, div vb(E), curl vb(B), diaer(u) = c^2 laplacian u =: c^2 laplace u $
```

Dot product `dprod`, cross product `cprod`, and inner product `iprod`.

```typ
#import "@preview/physica:0.9.1": dprod, cprod, iprod

$ a dprod b, a cprod b, a iprod b $
```

### Matrices

In addition to Typst's built-in `mat()` to write a matrix, physica provides a
number of handy tools to make it even easier.

```typ
#import "@preview/physica:0.9.1": TT, mdet

$
// Matrix transpose with "TT", though it is recommended to
// use super-T-as-transpose so that "A^T" also works (more on that later).
A^TT,
// Determinant with "mdet(...)".
det mat(a, b; c, d) := mdet(a, b; c, d)
$
```

Diagonal matrix `dmat(...)` and antidiagonal matrix `admat(...)`.
```typ
#import "@preview/physica:0.9.1": dmat, admat

$ dmat(1, 2) dmat(1, a_1, xi, delim:"[", fill:0) quad
  admat(1, 2) admat(1, a_1, xi, fill:dot) $
```

Identity matrix `imat(n)` and zero matrix `zmat(n)`.
```typ
#import "@preview/physica:0.9.1": imat, zmat

$ imat(2) imat(3,delim:"[",fill:*) quad zmat(2) zmat(3,delim:"[") $
```

Jacobian matrix with `jmat(func; ...)` or the longer name `jacobianmatrix`.
```typ
#import "@preview/physica:0.9.1": jmat

$ jmat(f_1,f_2; x,y) quad jmat(f,g; x,y,z; delim:"[") quad
  jmat(f,g;x,y,z;delim:"{",big:#true) $
```

Hessian matrix with `hmat(func; ...)` or the longer name `hessianmatrix`.
```typ
#import "@preview/physica:0.9.1": hmat

$ hmat(f; x,y) quad hmat(; x,y,z; delim:"[") quad
  hmat(;x,y,z;big:#true,delim:"{") $
```

Finally, `xmat(row, col, func)` (or its longer name `xmatrix`) helps you to
build a matrix with a function. That function takes two numbers (row and column)
and returns an equation snippet `$...$`.

```
#import "@preview/physica:0.9.1": xmat
$
// Define a function and pass it to xmat(...)
#let element = (i,j) => $g^(#(i - 1)#(j - 1))$
xmat(2, 2, #element)

// Or just pass in an anonymous function closure.
xmat(2, 3, #(r, c) => {
  $"exp"(#r, #c) = #calc.pow(r, c)$
}, delim:"[")
$
```

### Dirac braket notations

Physica provides `bra`, `ket`, `braket`, `ketbra`, and `mel`.

```typ
#import "@preview/physica:0.9.1": bra, ket, braket, ketbra, mel
#set math.equation(numbering: "(1)")

$ bra(u) quad ket(v) \
  braket(u) quad braket(u, v) quad ketbra(u) quad ketbra(u, v) \
  mel(psi, A, phi) =^"def" bra(psi)(A ket(phi)) = (bra(psi)A)ket(phi) $ // (1)

// The brakets are automatically scaled up.
$ braket(sum_(i=0)^n phi_n, psi)
  mel(phi_n^0, sqrt(h / (pi m omega))(a^dagger + a), phi_n^0) $ // (2)
```

Note: writing brakets used to be very complex, and physica encapsulates some
acrobats to simplify it. After the author's
[PR2760](https://github.com/typst/typst/pull/2760) was merged to Typst, the
package simplified its internal code accordingly and thus requires at least
Typst 0.10.

### Reduced Planck constant (hbar)

In the default font, the Typst built-in symbol `planck.reduce` looks a bit off:
on letter "h" there is a slash instead of a horizontal bar, contrary to the
symbol's colloquial name "h-bar". This package offers `hbar` to render the
symbol in the familiar form⁠. Contrast:

```typ
#import "@preview/physica:0.9.1": hbar

#table(
  columns: (auto, auto), align: horizon, stroke: none,

  [`planck.reduce`], [$ E = planck.reduce omega wide frac(planck.reduce^2, 2m) $],
  [physica `hbar`],  [$ E = hbar omega wide frac(hbar^2, 2m) $],
)
```

### Tensors

Tensors are often expressed with the
[abstract index notation](https://en.wikipedia.org/wiki/Abstract_index_notation),
which makes the contravariant and covariant "slots" explicit. The intuitive
solution of using superscripts and subscripts do not suffice if both upper
(contravariant) and lower (covariant) indices exist, because the notation rules
require the indices be vertically separated.

With physica's `tensor` function, you may use `+` to denote an upper index and
`-` to denote a lower index.

```typ
#import "@preview/physica:0.9.1": tensor, grad

// Position matters. The spacing is flexible, so don't worry about wide symbols.
$ tensor(T,+a,-b,-c) != tensor(T,+a,+b,-c) != tensor(T,-a,+b,-c) wide
  tensor(T,-a_42,+b_12306,-c) $
```

### Braces

In addition to Typst's built-in absolute value `abs` and norm `norm`, physica
defines several other braces frequently used in scentific writing.

```typ
#import "@preview/physica:0.9.1": order, Set, eval, expval
#set math.equation(numbering: "(1)")

#table(
  columns: (auto, auto), align: horizon, stroke: none,

  // Absolute and norm values (Typst built-in)
  [$ abs(phi), abs(phi/2), norm(phi), norm(phi/2) $], // (1)

  // The big-O notation.
  [$ order(x^2), order(sum_(i=0)^oo f_i (x)) $], // (2)

  // Set builder.
  // It is not a all-lowercase word "set" to avoid colliding with a Typst keyword.
  [$ Set(a_n), Set(m/(sum_i a_i), m > 0 \, m != 1) $], // (3)

  // Evaluation boundary, a.k.a. restriction.
  [$ eval(f(tau))_0^t, eval(f(x)/g(x))_(x=0) $], // (4)

  // Expectation value.
  [$ expval(u), expval(f/N) $], // (5)
)
```

### Matrix transpose

Physica provides a show rule that enables users to write single superscript
letter "T" as the transpose operator, just like handwriting.

To enable this feature, you need to invoke it first:
`#show: super-T-as-transpose`. Alternatively, if you only want this feature
inside a paragraph, you may put it inside a `#[...]` content block.

```typ
#import "@preview/physica:0.9.1": super-T-as-transpose, eval, TT, dd
#set math.equation(numbering: "(1)")

#show: super-T-as-transpose

#table(
  columns: (auto, auto), align: horizon, stroke: none,

  [$ (U V_n W')^T = W'^T V_n^T U^T, mat(a; b)^T $], // (1)
  // If the superscript "T" is attached to a limits() or a scripts(), it
  // won't be rendered as a transpose operator.
  [$ limits(sum)^T_(t=0) a_t, scripts(e)^T $], // (2)
  // The superscript "T" won't become a transpose operator with integrals
  // and vertical bars.
  [$ abs(a)^T, integral_0^T f(t) dd(t) = eval(F(t))^T_0 $], // (3)
  // Overrides: to print a transpose operator explicitly, use "TT"; to print
  // an as-is superscript letter T, use "scripts(T)".
  [$ A^TT, 2^scripts(T) $], // (4)
)
```

### Matrix dagger (conjugate transpose)

Physica provides a show rule that enables users to write single superscript plus
sign "+" as the conjugate transpose operator (i.e. dagger), just like
handwriting, so that the word `dagger` would not visually clutter the source
code of the equation.

To enable this feature, you need to invoke it first:
`#show: super-plus-as-dagger`. Alternatively, if you only want this feature
inside a paragraph, you may put it inside a `#[...]` content block.

```typ
#import "@preview/physica:0.9.1": super-plus-as-dagger
#set math.equation(numbering: "(1)")

#show: super-plus-as-dagger

#table(
  columns: (auto, auto, auto, auto, auto), align: horizon, stroke: none,

  [$ U^+U = U U^+ = I $], // (1)
  // If the superscript "+" is attached to a limits() or a scripts(), it
  // won't be rendered as a dagger.
  [$ limits(sum)^T_(t=0) a_t, scripts(e)^T $], // (2)
  // Overrides: to print a dagger explicitly, use the normal "dagger"; to
  // print an as-is superscript plus, use "scripts(+)".
  [$ A^dagger, A^scripts(+) $], // (3)
)
```

### Isotopes

To render a chemical isotope symbol, you may use the `isotope` function.

```typ
#import "@preview/physica:0.9.1": isotope

// a: mass number A
// z: the atomic number Z
$
isotope(I, a:127), quad isotope("Fe", z:26), quad
isotope("Tl",a:207,z:81) --> isotope("Pb",a:207,z:82) + isotope(e,a:0,z:-1)
$
```


### Taylor expansion

Taylor expansion is a frequent guest in the study of nature, so Physica provides
a way to write each n-th term more efficiently.

```typ
#import "@preview/physica:0.9.1": taylorterm
#set math.equation(numbering: "(1)")

$ taylorterm(f,x,a,0), wide taylorterm(f,x,a,1), wide taylorterm(f,x,a,n) $ // (1)

// The expansion point can be more complex. Physica merges the
// parenthesis when appropriate.
$ taylorterm(f,x,(1+xi),2), wide taylorterm(f,x,x_0,(n+1)) $ // (2)
```
