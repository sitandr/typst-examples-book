# Image with original size

```typ
#let natural-image(..args) = style(styles => {
  let (width, height) = measure(image(..args), styles)
  image(..args, width: width, height: height)
})

#natural-image("../tiger.jpg")
```