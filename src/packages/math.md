# Math

## `physica`

Physica (Latin for _natural sciences_) provides utilities that simplify
otherwise complex and repetitive mathematical expressions in natural sciences.

Its [manual](https://github.com/Leedehai/typst-physics/blob/master/physica-manual.pdf)
provides a full set of demonstrations of how the package could be helpful.

| | | |
|:--|:--|:--|
|[Differentials](#differentials)|[Ordinary derivatives](#ordinary-derivatives)|[Partial derivatives](#partial-derivatives)|
|[Vectors and fields](#vectors-and-fields)|[Matrices](#matrices)|[Dirac brakets](#dirac-brakets)|
|[Tensors](#tensors)|[Braces](#braces)|[Taylor expansion](#taylor-expansion)|
[Matrix transpose](#matrix-transpose)|[Matrix dagger](#matrix-dagger-conjugate-transpose)| |

### Differentials

Function `dd(*args, **kwargs)` excels at typesetting multi-variable
differentials.

```typ
#import "@preview/physica:0.9.1": dd, vb, var, difference
#set math.equation(numbering: "(1)")

#table(
  columns: (auto, auto), align: horizon, stroke: none,

[$ dd(f) quad dd(f,2) quad dd(x,y,2) quad dd(vb(x),t,[3,]) $], // (1)

// A standalone order number applies to all variables; an array applies members
// to each variable individually. If the order number missing or fewer than
// needed, it's assumed to be 1.
[$ dd(x,y) quad dd(x,y,2)quad dd(x,y, [2,]) \
   dd(x,y, [2,3]) quad dd(x,y,z, [2,3]) $], // (2)

// Like Typst's "dif", there is a thin space between the function and the
// differential symbol, as advised by the TeXBook.
[$ integral_S f(r,theta) dd(r,theta) $], // (3)

// Surreally complex.
[$ dd(x_1,hat(y),(z^1), [[1,1], rho+1, n_1]) $], // (4)

// Changing the "d" symbol. There are also two shorthands:
// * variations `var` for `dd(..., d:delta)`
// * difference `difference` for `dd(..., d:Delta)`
[$ dd(x, d:upright(D)) quad dd(x,y, d:d) quad
   var(x,y, d:delta)   quad difference(x,y, 2, d:Delta) $], // (5)

// Joining the d-units with, say the exterior product symbol, by argument "p".
[$ dd(x,y,z, p:and) $], // (6)
)
```

### Ordinary derivatives

Function `dv(f, *args, **kwargs)` helps you assemble ordinary derivatives with
ease.

```typ
#import "@preview/physica:0.9.1": dv, vb
#set math.equation(numbering: "(1)")

#table(
  columns: (auto, auto), align: horizon, stroke: none,

  // The function name can be ommitted. If the order number missing,
  // it's assumed to be 1.
  [$ dv(,x), dv(,x, 2), dv(f,x, k+1) $], // (1)
  [$ dv(,vb(r)), dv((f+g),vb(r)_e, 2) $], // (2)

  // Changing the "d" symbol.
  [$ dv(,x, d:delta), dv(,x, 2, d:Delta), dv(vb(u),t, 2, d: upright(D)) $], // (3)

  // Use "s" to designate a separator, e.g. a slash.
  [$ dv(f,x,k, s:slash) $], // (4)
)
```

### Partial derivatives

Partial derivatives `pdv(f, *args, **kwargs)` can handle mixed orders. It
attempts to compute the total order based on partial orders specified by the
user, but the result is overridable.

```typ
#import "@preview/physica:0.9.1": pdv, vb
#set math.equation(numbering: "(1)")

#table(
  columns: (auto, auto, auto), align: horizon, stroke: none,

  // The function name can be ommitted. A standalone order number applies to
  // all variables; an array applies members to each variable individually.
  // If the order number missing or fewer than needed, it's assumed to be 1.
  [$ pdv(,x), pdv(,t, 2), pdv(f,x,y,[k,2]) $], // (1)
  [$ pdv(f,vb(r)), pdv(phi,vb(r)_e, 2) $], // (2)

  // The total order is automatically calculated.
  [$ pdv(,x,y), pdv(,x,y, [1+k,1]) $], // (3)

  // Use "s" to designate a separator, e.g. a slash.
  [$ pdv(f,x,y, s:slash) $], // (4)

  // Override the automatic addition result with argument "total".
  [$ pdv(,x,y,z,t, [1, xi, 2, eta+2]) $], // (5)
  [$ pdv(,x,y,z,t, [1, xi, 2, eta+2], total: 5+eta+xi) $], // (6)
)
```

### Vectors and fields

In addition to Typst's built-in `vec()` for column vectors, physica provides
`vecrow()` for row vectors for symmetry. In addition, physica provides `vb()`,
`vu()`, `va()` to typset vectors.

```typ
#set math.equation(numbering: "(1)")

#import "@preview/physica:0.9.1": vecrow, vb, vu, va
$
vecrow(alpha, b) quad vb(a) vb(mu_1) quad vu(a) vu(mu_1) quad va(a) va(mu_1)
$ // (1)

#import "@preview/physica:0.9.1": grad, div, curl, laplacian, vb
$
grad phi quad div vb(E) quad curl vb(B) quad
diaer(u) = c^2 laplacian u =: c^2 laplace u
$ // (2)

#import "@preview/physica:0.9.1": dprod, cprod, iprod
$ a dprod b, a cprod b, a iprod b $ // (3)
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

Diagonal matrix `dmat(...)`, antidiagonal matrix `admat(...)`,
identity matrix `imat(n)`, and zero matrix `zmat(n)`.
```typ
#import "@preview/physica:0.9.1": dmat, admat, imat, zmat

$ dmat(1, 2) dmat(1, a_1, xi, fill:0) quad
  admat(1, 2) admat(1, a_1, xi, fill:dot, delim:"[") quad
  imat(2) imat(3, delim:"{",fill:*) quad
  zmat(2) zmat(3, delim:"|") $
```

Jacobian matrix with `jmat(func; ...)` or the longer name `jacobianmatrix`,
Hessian matrix with `hmat(func; ...)` or the longer name `hessianmatrix`, and
finally `xmat(row, col, func)` (or its longer name `xmatrix`) to build a matrix.
```typ
#import "@preview/physica:0.9.1": jmat, hmat, xmat

$
jmat(f_1,f_2; x,y) jmat(f,g; x,y,z; delim:"[") quad
hmat(f; x,y)       hmat(; x,y; big:#true) quad

#let elem-ij = (i,j) => $g^(#(i - 1)#(j - 1)) = #calc.pow(i,j)$
xmat(2, 2, #elem-ij)
$
```

### Dirac brakets

Physica provides `bra`, `ket`, `braket`, `ketbra`, and `mel`.

```typ
#import "@preview/physica:0.9.1": bra, ket, braket, ketbra, mel

$
bra(u) quad ket(v) quad
braket(u) quad braket(u, v) quad ketbra(u) quad ketbra(u, v) \
mel(psi, hat(A), phi) =^"def" bra(psi)(hat(A) ket(phi)) = (bra(psi)hat(A))ket(phi)
$
```

### Tensors

The [Abstract index notation](https://en.wikipedia.org/wiki/Abstract_index_notation)
makes the contravariant and covariant "slots" explicit, and the indices must be
vertically separated. With physica's `tensor` function, you may use `+`/`-`
to denote a (contravariant) upper index or a (covariant) lower index.

```typ
#import "@preview/physica:0.9.1": tensor, grad

// Position matters. The spacing is flexible, so don't worry about wide symbols.
$ tensor(T,+a,-b,-c) != tensor(T,+a,+b,-c) != tensor(T,-c,+a,+b) wide
  tensor(T,-a_42,+b_12306,-c) $
```

### Braces

In addition to Typst's built-in absolute value `abs` and norm `norm`, physica
defines several other braces frequently used in scientific writing.

```typ
#import "@preview/physica:0.9.1": order, Set, eval, expval
#set math.equation(numbering: "(1)")

#table(
  columns: (auto, auto), align: horizon, stroke: none,

  // The big-O notation.
  [$ order(x^2), order(sum_(i=0)^oo f_i (x)) $], // (1)

  // Set builder.
  // It is not a all-lowercase word "set" to avoid colliding with a Typst keyword.
  [$ Set(a_n), Set(m/(sum_i a_i), m > 0 \, m != 1) $], // (2)

  // Evaluation boundary, a.k.a. restriction.
  [$ eval(f(tau))_0^t, eval(f(x)/g(x))_(x=0) $], // (3)

  // Expectation value.
  [$ expval(u), expval(f/N) $], // (4)
)
```

### Taylor expansion

Taylor expansion is a frequent guest in the study of nature, so Physica provides
a way to write each n-th term more efficiently.

```typ
#import "@preview/physica:0.9.1": taylorterm

$
taylorterm(f,x,a,0), quad taylorterm(f,x,a,1), quad
// Physica removes the parenthesis appropriately.
taylorterm(f,x,(1+xi),2), quad taylorterm(f,x,x_0,(n+1))
$
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
sign "+" as the conjugate transpose operator (a.k.a. Hermitian conjugate)
i.e. a dagger, just like handwriting, so that reapted words `dagger` would not
visually clutter the source code of the equation.

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
