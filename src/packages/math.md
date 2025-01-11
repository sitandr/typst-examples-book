# Math

## General
### `physica`

> Physica (Latin for _natural sciences_) provides utilities that simplify
> otherwise complex and repetitive mathematical expressions in natural sciences.

> Its [manual](https://github.com/Leedehai/typst-physics/blob/master/physica-manual.pdf)
> provides a full set of demonstrations of how the package could be helpful.

#### Common notations

* Calculus: differential, ordinary and partial derivatives
  * Optional function name,
  * Optional order number or an array of thereof,
  * Customizable "d" symbol and product joiner (say, exterior product),
  * Overridable total order calculation,
* Vectors and vector fields: div, grad, curl,
* Taylor expansion,
* Dirac braket notations,
* Tensors with abstract index notations,
* Matrix transpose and dagger (conjugate transpose).
* Special matrices: determinant, (anti-)diagonal, identity, zero, Jacobian,
Hessian, etc. <!-- TODO Add rotation and gram matrices in physica:0.9.2 -->

Below is a preview of those notations.

```typ
#import "@preview/physica:0.9.1": * // Symbol names annotated below

#table(
  columns: 4, align: horizon, stroke: none, gutter: 1em,

  // vectors: bold, unit, arrow
  [$ vb(a), vb(e_i), vu(a), vu(e_i), va(a), va(e_i) $],
  // dprod (dot product), cprod (cross product), iprod (innerproduct)
  [$ a dprod b, a cprod b, iprod(a, b) $],
  // laplacian (different from built-in laplace)
  [$ dot.double(u) = laplacian u =: laplace u $],
  // grad, div, curl (vector fields)
  [$ grad phi, div vb(E), \ curl vb(B) $],
)
```

```typ
#import "@preview/physica:0.9.1": * // Symbol names annotated below

#table(
  columns: 4, align: horizon, stroke: none, gutter: 1em,

  // Row 1.
  // dd (differential), var (variation), difference
  [$ dd(f), var(f), difference(f) $],
  // dd, with an order number or an array thereof
  [$ dd(x,y), dd(x,y,2), \ dd(x,y,[1,n]), dd(vb(x),t,[3,]) $],
  // dd, with custom "d" symbol and joiner
  [$ dd(x,y,p:and), dd(x,y,d:Delta), \ dd(x,y,z,[1,1,n+1],d:d,p:dot) $],
  // dv (ordinary derivative), with custom "d" symbol and joiner
  [$ dv(phi,t,d:Delta), dv(phi,t,d:upright(D)), dv(phi,t,d:delta) $],

  // Row 2.
  // dv, with optional function name and order
  [$ dv(,t) (dv(x,t)) = dv(x,t,2) $],
  // pdv (partial derivative)
  [$ pdv(f,x,y,2), pdv(,x,y,[k,]) $],
  // pdv, with auto-added overridable total
  [$ pdv(,x,y,[i+2,i+1]), pdv(,y,x,[i+1,i+2],total:3+2i) $],
  // In a flat form
  [$ dv(u,x,s:slash), \ pdv(u,x,y,2,s:slash) $],
)
```

<!--
// TODO Add Order/order once physica:0.9.2 is merged.
// TODO Demo expval(A, phi) once physica:0.9.2 is merged.
-->
```typ
#import "@preview/physica:0.9.1": * // Symbol names annotated below

#table(
  columns: 3, align: horizon, stroke: none, gutter: 1em,

  // tensor
  [$ tensor(T,+a,-b,-c) != tensor(T,-b,-c,+a) != tensor(T,+a',-b,-c) $],
  // Set builder notation
  [$ Set(p, {q^*, p} = 1) $],
  // taylorterm (Taylor series term)
  [$ taylorterm(f,x,x_0,1) \ taylorterm(f,x,x_0,(n+1)) $],
)
```
```typ
#import "@preview/physica:0.9.1": * // Symbol names annotated below

#table(
  columns: 3, align: horizon, stroke: none, gutter: 1em,

  // expval (mean/expectation value), eval (evaluation boundary)
  [$ expval(X) = eval(f(x)/g(x))^oo_1 $],
  // Dirac braket notations
  [$
    bra(u), braket(u), braket(u, v), \
    ket(u), ketbra(u), ketbra(u, v), \
    mel(phi, hat(p), psi) $],
  // Superscript show rules that need to be enabled explicitly.
  // If put in a content block, they only control that block's scope.
  [
    #show: super-T-as-transpose // "..^T" just like handwriting
    #show: super-plus-as-dagger // "..^+" just like handwriting
    $ op("conj")A^T =^"def" A^+ \
      e^scripts(T), e^scripts(+) $ ], // Override with scripts()
)
```

#### Matrices

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

$ dmat(1, 2)  dmat(1, a_1, xi, fill:0)               quad
  admat(1, 2) admat(1, a_1, xi, fill:dot, delim:"[") quad
  imat(2)     imat(3, delim:"{",fill:*) quad
  zmat(2)     zmat(3, delim:"|") $
```

Jacobian matrix with `jmat(func; ...)` or the longer name `jacobianmatrix`,
Hessian matrix with `hmat(func; ...)` or the longer name `hessianmatrix`, and
finally `xmat(row, col, func)` to build a matrix.
```typ
#import "@preview/physica:0.9.1": jmat, hmat, xmat

$
jmat(f_1,f_2; x,y) jmat(f,g; x,y,z; delim:"[") quad
hmat(f; x,y)       hmat(; x,y; big:#true)      quad

#let elem-ij = (i,j) => $g^(#(i - 1)#(j - 1)) = #calc.pow(i,j)$
xmat(2, 2, #elem-ij)
$
```

### `mitex`

> MiTeX provides LaTeX support powered by WASM in Typst, including real-time rendering of LaTeX math equations.
> You can also use LaTeX syntax to write `\ref` and `\label`.

> Please refer to the [manual](https://github.com/mitex-rs/mitex) for more details.

```typ
#import "@preview/mitex:0.2.4": *

Write inline equations like #mi("x") or #mi[y].

Also block equations:

#mitex(`
  \newcommand{\f}[2]{#1f(#2)}
  \f\relax{x} = \int_{-\infty}^\infty
    \f\hat\xi\,e^{2 \pi i \xi x}
    \,d\xi
`)

Text mode:

#mitext(`
  \iftypst
    #set math.equation(numbering: "(1)", supplement: "equation")
  \fi

  An inline equation $x + y$ and block \eqref{eq:pythagoras}.

  \begin{equation}
    a^2 + b^2 = c^2 \label{eq:pythagoras}
  \end{equation}
`)
```


### `i-figured`

Configurable equation numbering per section in Typst.
There is also figure numbering per section, see more examples in its [manual](https://github.com/RubixDev/typst-i-figured).


```typ
#import "@preview/i-figured:0.2.3"

// make sure you have some heading numbering set
#set heading(numbering: "1.1")

// apply the show rules (these can be customized)
#show heading: i-figured.reset-counters
#show math.equation: i-figured.show-equation.with(
  level: 1,
  zero-fill: true,
  leading-zero: true,
  numbering: "(1.1)",
  prefix: "eqt:",
  only-labeled: false,  // numbering all block equations implicitly
  unnumbered-label: "-",
)


= Introduction

You can write inline equations such as $x + y$, and numbered block equations like:

$ phi.alt := (1 + sqrt(5)) / 2 $ <ratio>

To reference a math equation, please use the `eqt:` prefix. For example, with @eqt:ratio, we have:

$ F_n = floor(1 / sqrt(5) phi.alt^n) $


= Appdendix

Additionally, you can use the <-> tag to indicate that a block formula should not be numbered:

$ y = integral_1^2 x^2 dif x $ <->

Subsequent math equations will continue to be numbered as usual:

$ F_n = floor(1 / sqrt(5) phi.alt^n) $
```



## Theorems
### `ctheorem`

A numbered theorem environment in Typst. See more examples in its
[manual](https://github.com/sahasatvik/typst-theorems/blob/main/manual.pdf).

```typ
#import "@preview/ctheorems:1.1.0": *
#show: thmrules

#set page(width: 16cm, height: auto, margin: 1.5cm)
#set heading(numbering: "1.1")

#let theorem = thmbox("theorem", "Theorem", fill: rgb("#eeffee"))
#let corollary = thmplain("corollary", "Corollary", base: "theorem", titlefmt: strong)
#let definition = thmbox("definition", "Definition", inset: (x: 1.2em, top: 1em))

#let example = thmplain("example", "Example").with(numbering: none)
#let proof = thmplain(
  "proof", "Proof", base: "theorem",
  bodyfmt: body => [#body #h(1fr) $square$]
).with(numbering: none)

= Prime Numbers
#lorem(7)
#definition[ A natural number is called a #highlight[_prime number_] if ... ]
#example[
  The numbers $2$, $3$, and $17$ are prime. See @cor_largest_prime shows that
  this list is not exhaustive!
]
#theorem("Euclid")[There are infinitely many primes.]
#proof[
  Suppose to the contrary that $p_1, p_2, dots, p_n$ is a finite enumeration
  of all primes. ... a contradiction.
]
#corollary[
  There is no largest prime number.
] <cor_largest_prime>
#corollary[There are infinitely many composite numbers.]
```

### `lemmify`

Lemmify is another theorem evironment generator with many selector and numbering
capabilities. See documentations in its [readme](https://github.com/Marmare314/lemmify).

```typ
#import "@preview/lemmify:0.1.5": *

#let my-thm-style(
  thm-type, name, number, body
) = grid(
  columns: (1fr, 3fr),
  column-gutter: 1em,
  stack(spacing: .5em, [#strong(thm-type) #number], emph(name)),
  body
)
#let my-styling = ( thm-styling: my-thm-style )
#let (
  definition, theorem, proof, lemma, rules
) = default-theorems("thm-group", lang: "en", ..my-styling)
#show: rules
#show thm-selector("thm-group"): box.with(inset: 0.8em)
#show thm-selector("thm-group", subgroup: "theorem"): it => box(
  it, fill: rgb("#eeffee"))

#set heading(numbering: "1.1")

= Prime numbers
#lorem(7) @proof and @thm[theorem]
#definition[ A natural number is called a #highlight[_prime number_] if ... ]
#theorem(name: "Theorem name")[There are infinitely many primes.]<thm>
#proof[
  Suppose to the contrary that $p_1, p_2, dots, p_n$ is a finite enumeration
  of all primes. ... #highlight[_a contradiction_].]<proof>
#lemma[There are infinitely many composite numbers.]
```

### `frame-it`
[Frame-It](https://typst.app/universe/package/frame-it/) is enables highlighting theorems with 2 pre-defined styles
and the option to define arbitrary custom styles. 
If no color is provided for a frame, it is automatically generated.
For documentation, have a look at the [README](https://github.com/marc-thieme/frame-it).

```typst
#import "@preview/frame-it:1.0.0": *

// You have to define the kinds of frames you need
#let (theorem, lemma, definition, important) = make-frames(
  // This identifies the counter used for all theorems in this definition
  "counter-id",
  theorem: ("Theorem",),
  // You can provide a color or leave it out and it will be generated
  lemma: ("Lemma", gray),
  // For each frame kind, you have to provide its supplement title to be displayed
  definition: ("Definition",),
  // You can add as many as you want
  important: ("Important", blue.lighten(25%)),
)

= Primes

Your frames will have a title.

#definition[Prime Number][
  A natural number greater than 1 is called a _prime number_ 
  if it is divisible only by 1 and itself. For example, 2, 3, 5, and 7 
  are all prime numbers.
]

Which you can also leave out if you want. 

#lemma[][Each prime number greater than 2 is divisible by 2 or is an odd number, 
  but no prime number is divisible by any even number other than 2 itself.
]

If you need a custom style, look at the project README to see how to define a custom styling function.
By default, there are two different styles predefined.
This is the second one:

#important(style: styles.hint)[Unique Prime Factorization][Heads–Up][
  Every positive integer greater than 1 can be uniquely factored 
  into prime numbers. This is known as the Fundamental Theorem of Arithmetic. 
  It’s crucial for understanding the structure of integers in number theory.
]

An additional feature is to add tags with additional information

#theorem[Euclid's Theorem][Very Important][Exam relevant][
  There are infinitely many prime numbers. 
  This fundamental result in number theory demonstrates 
  that primes cannot be exhausted, no matter how large the set of primes discovered.
]
```
