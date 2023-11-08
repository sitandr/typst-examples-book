# Fonts

## Set math font

**Important:** The font you want to set for math should _contain_ necessary math symbols. That should be a special font with math. If it isn't, you will probable _an error_.

```
#show math.equation: set text(font: "Fira Math", fallback: false)

$
emptyset\

integral_a^b sum (A + B)/C dif x\
$
```