# Make all math display math

<div class="warning">
    May slightly interfere with math blocks.
</div>

```typ
// author: eric1102
#show math.equation: it => {
  if it.body.fields().at("size", default: none) != "display" {
    return math.display(it)
  }
  it
}

Inline math: $sum_(n=0)^oo e^(x^2 - n/x^2)$\
Some other text on new line.


$
sum_(n=0)^oo e^(x^2 - n/x^2)
$
```