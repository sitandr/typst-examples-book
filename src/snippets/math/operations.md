# Operations

## Fractions

```
$
p/q, p slash q, p\/q
$
```

### Slightly moved:
```
#let mfrac(a, b) = move(a, dy: -0.2em) + "/" + move(b, dy: 0.2em, dx: -0.1em)
$A\/B, #mfrac($A$, $B$)$,
```

### Large fractions

```
#let dfrac(a, b) = $display(frac(#a, #b))$
$(x + y)/(1/x + 1/y) quad (x + y)/(dfrac(1,x) + dfrac(1, y))$
```