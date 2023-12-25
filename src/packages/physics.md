# Physics

## `physica`

Physica (Latin for _natural sciences_) provides utilities that simplify
otherwise complex and repetitive mathematical expressions in natural sciences.

Its [manual](https://github.com/Leedehai/typst-physics/blob/master/physica-manual.pdf)
provides a full set of demonstrations of how the package could be helpful.

### Mathematical physics

The [packages/math.md](./math.md#common-notations) page has more examples on its
math capabilities. Below is a preview that may be of particular interest in the
domain of physics:
* Calculus: differential, ordinary and partial derivatives
  * Optional function name,
  * Optional order number or array of order numbers,
  * Customizable "d" symbol and product joiner (say, exterior product),
  * Overridable total order calculation,
* Vectors and vector fields,
* Taylor expansion,
* Dirac braket notations,
* Tensors with abstract index notations,
* Matrix transpose and dagger (conjugate transpose).
* Special matrices: determinant, (anti-)diagonal, identity, zero, Jacobian,
Hessian, etc. <!-- TODO Add rotation and gram matrices in physica:0.9.2 -->

### Isotopes

```typ
#import "@preview/physica:0.9.1": isotope

// a: mass number A
// z: the atomic number Z
$
isotope(I, a:127), quad isotope("Fe", z:26), quad
isotope("Tl",a:207,z:81) --> isotope("Pb",a:207,z:82) + isotope(e,a:0,z:-1)
$
```

### Reduced Planck constant (hbar)

In the default font, the Typst built-in symbol `planck.reduce` looks a bit off:
on letter "h" there is a slash instead of a horizontal bar, contrary to the
symbol's colloquial name "h-bar". This package offers `hbar` to render the
symbol in the familiar form⁠. Contrast:

```typ
#import "@preview/physica:0.9.1": hbar

$ E = planck.reduce omega => E = hbar omega, wide
  frac(planck.reduce^2, 2m) => frac(hbar^2, 2m), wide
  (pi G^2) / (planck.reduce c^4) => (pi G^2) / (hbar c^4), wide
  e^(frac(i(p x - E t), planck.reduce)) => e^(frac(i(p x - E t), hbar)) $
```
