# Color & Gradients

## Gradients

Gradients may be very cool for presentations or just a pretty look.

```typ
/// author: frozolotl
#set page(paper: "presentation-16-9", margin: 0pt)
#set text(fill: white, font: "Inter")

#let grad = gradient.linear(rgb("#953afa"), rgb("#c61a22"), angle: 135deg)

#place(horizon + left, image(width: 60%, "../img/landscape.png"))

#place(top, polygon(
  (0%, 0%),
  (70%, 0%),
  (70%, 25%),
  (0%, 29%),
  fill: white,
))
#place(bottom, polygon(
  (0%, 100%),
  (100%, 100%),
  (100%, 30%),
  (60%, 30% + 60% * 4%),
  (60%, 60%),
  (0%, 64%),
  fill: grad,
))

#place(top + right, block(inset: 7pt, image(height: 19%, "../img/tub.png")))

#place(bottom, block(inset: 40pt)[
  #text(size: 30pt)[
    Presentation Title
  ]

  #text(size: 16pt)[#lorem(20) | #datetime.today().display()]
])
```