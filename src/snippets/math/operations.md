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

$A\/B, #mfrac($A$, $B$)$
```