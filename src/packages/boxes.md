# Custom boxes

## Showbox

```typ
#import "@preview/showybox:2.0.1": showybox

#showybox(
  [Hello world!]
)
```

```typ
#import "@preview/showybox:2.0.1": showybox

// First showybox
#showybox(
  frame: (
    border-color: red.darken(50%),
    title-color: red.lighten(60%),
    body-color: red.lighten(80%)
  ),
  title-style: (
    color: black,
    weight: "regular",
    align: center
  ),
  shadow: (
    offset: 3pt,
  ),
  title: "Red-ish showybox with separated sections!",
  lorem(20),
  lorem(12)
)

// Second showybox
#showybox(
  frame: (
    dash: "dashed",
    border-color: red.darken(40%)
  ),
  body-style: (
    align: center
  ),
  sep: (
    dash: "dashed"
  ),
  shadow: (
	  offset: (x: 2pt, y: 3pt),
    color: yellow.lighten(70%)
  ),
  [This is an important message!],
  [Be careful outside. There are dangerous bananas!]
)
```

```typ
#import "@preview/showybox:2.0.1": showybox

#showybox(
  title: "Stokes' theorem",
  frame: (
    border-color: blue,
    title-color: blue.lighten(30%),
    body-color: blue.lighten(95%),
    footer-color: blue.lighten(80%)
  ),
  footer: "Information extracted from a well-known public encyclopedia"
)[
  Let $Sigma$ be a smooth oriented surface in $RR^3$ with boundary $diff Sigma equiv Gamma$. If a vector field $bold(F)(x,y,z)=(F_x (x,y,z), F_y (x,y,z), F_z (x,y,z))$ is defined and has continuous first order partial derivatives in a region containing $Sigma$, then

  $ integral.double_Sigma (bold(nabla) times bold(F)) dot bold(Sigma) = integral.cont_(diff Sigma) bold(F) dot dif bold(Gamma) $
]
```

```typ
#import "@preview/showybox:2.0.1": showybox

#showybox(
  title-style: (
    weight: 900,
    color: red.darken(40%),
    sep-thickness: 0pt,
    align: center
  ),
  frame: (
    title-color: red.lighten(80%),
    border-color: red.darken(40%),
    thickness: (left: 1pt),
    radius: 0pt
  ),
  title: "Carnot cycle's efficiency"
)[
  Inside a Carnot cycle, the efficiency $eta$ is defined to be:

  $ eta = W/Q_H = frac(Q_H + Q_C, Q_H) = 1 - T_C/T_H $
]
```

```typ
#import "@preview/showybox:2.0.1": showybox

#showybox(
  footer-style: (
    sep-thickness: 0pt,
    align: right,
    color: black
  ),
  title: "Divergence theorem",
  footer: [
    In the case of $n=3$, $V$ represents a volume in three-dimensional space, and $diff V = S$ its surface
  ]
)[
  Suppose $V$ is a subset of $RR^n$ which is compact and has a piecewise smooth boundary $S$ (also indicated with $diff V = S$). If $bold(F)$ is a continuously differentiable vector field defined on a neighborhood of $V$, then:

  $ integral.triple_V (bold(nabla) dot bold(F)) dif V = integral.surf_S (bold(F) dot bold(hat(n))) dif S $
]
```

```typ
#import "@preview/showybox:2.0.1": showybox

#showybox(
  frame: (
    border-color: red.darken(30%),
    title-color: red.darken(30%),
    radius: 0pt,
    thickness: 2pt,
    body-inset: 2em,
    dash: "densely-dash-dotted"
  ),
  title: "Gauss's Law"
)[
  The net electric flux through any hypothetical closed surface is equal to $1/epsilon_0$ times the net electric charge enclosed within that closed surface. The closed surface is also referred to as Gaussian surface. In its integral form:

  $ Phi_E = integral.surf_S bold(E) dot dif bold(A) = Q/epsilon_0 $
]
```

## Colorful boxes

```typ
#import "@preview/colorful-boxes:1.2.0": colorbox, slantedColorbox, outlinebox, stickybox

#colorbox(
  title: lorem(5),
  color: "blue",
  radius: 2pt,
  width: auto
)[
  #lorem(50)
]

#slantedColorbox(
  title: lorem(5),
  color: "red",
  radius: 0pt,
  width: auto
)[
  #lorem(50)
]

#outlinebox(
  title: lorem(5),
  color: none,
  width: auto,
  radius: 2pt,
  centering: false
)[
  #lorem(50)
]

#outlinebox(
  title: lorem(5),
  color: "green",
  width: auto,
  radius: 2pt,
  centering: true
)[
  #lorem(50)
]

#stickybox(
  rotation: 3deg,
  width: 7cm
)[
  #lorem(20)
]
```

## Theorems

See [math](./math.md)

TODO: ctheorems, lemmify