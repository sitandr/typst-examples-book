# Physics

## `physica`

Physica (Latin for _natural sciences_) provides utilities that simplify
otherwise complex and repetitive mathematical expressions in natural sciences.

Its [manual](https://github.com/Leedehai/typst-physics/blob/master/physica-manual.pdf)
provides a full set of demonstrations of how the package could be helpful.

### Mathematical physics

The [packages/math.md](./math.md) page has more examples on its math
capabilities. Below is a partial preview that may be of particular interest in
the domain of physics: differential, ordinary and partial derivatives (with
overridable total order calculation), vector fields, Taylor expansion,
Dirac brakets, tensors.

```typ
#import "@preview/physica:0.9.1": * // Symbol names annotated below

#table(
  columns: (auto, auto, auto, auto), align: horizon, stroke: none,

  // dd (differential), var (variation), difference
  [$ dd(f), var(f), difference(f) $],
  // Differential, with order numbers
  [$ dd(x,y), dd(x,y,2), \ dd(x,y,[k,]), dd(vb(x),t,[3,1]) $],
  // Differential with custom "d" symbol and joiner
  [$ dd(x,y,z, d:Delta, p:and) \ dd(x,y,z, [a,b,c], d:d) $],
  // dv (ordinary derivative), with optional function name and order
  [$ dv(,t) (dv(x,t)) = dv(x,t,2) $],

  // pdv, with optional function name and order, and overridable total
  [$ pdv(,x,y,[1,i+1]) f = pdv(f,y,x,[i+1,1],total:2+i) $],
  // grad, curl, vb (vector bold)
  [$ curl vb(A) - grad phi $],
  // dv, pdv, grad
  [$ dv(phi,t,d:DD) = pdv(phi,t) + u grad phi $],
  // tensor
  [$ tensor(T,+a,+b,-c) != tensor(T,-c,+a,+b) $],

  // taylorterm (Taylor expansion), va (vector arrow)
  [$ taylorterm(f,va(x),va(x_0),n) $],
  // expval, mel (as a Dirac braket)
  [$ expval(p) = mel(phi, hat(p), phi) $],
  // Dirac brakets
  [$
    bra(u), braket(u), braket(u,v),\ ket(u), ketbra(u), ketbra(u, v)
  $],
  // Superscript show rules that need to be enabled explicitly.
  // If put in a content block, they only control that block's scope.
  [
    #show: super-T-as-transpose
    #show: super-plus-as-dagger
    $ op("conj")A^T =^"def" A^+ \
      e^scripts(T), e^scripts(+) $  // override with scripts()
  ],
)
```

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
