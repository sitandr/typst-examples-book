# Operations

## Fractions

```typ
$
p/q, p slash q, p\/q
$
```

### Slightly moved:
```typ
#let mfrac(a, b) = move(a, dy: -0.2em) + "/" + move(b, dy: 0.2em, dx: -0.1em)
#let dfrac(a, b) = $display(frac(#a, #b))$

$A\/B, #mfrac($A$, $B$)$,\
$(x + y)/(1/x + 1/y) quad (x + y)/(dfrac(1,x) + dfrac(1, y))$
```