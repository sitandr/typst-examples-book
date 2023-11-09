# Fonts

## Set math font

**Important:** The font you want to set for math should _contain_ necessary math symbols. That should be a special font with math. If it isn't, you are very likely to get _an error_ (remember to set `fallback: false` and check `typst fonts` to debug the fonts).

```
#show math.equation: set text(font: "Fira Math", fallback: false)

$
emptyset\

integral_a^b sum (A + B)/C dif x\
$
```