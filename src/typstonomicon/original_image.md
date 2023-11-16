# Image with original size
This function renders image with the size it "naturally" has.

This works because measure conceptually places the image onto a page with infinite size and then the image defaults to 1pt per pixel instead of becoming infinitely larger itself.

```typ
// author: laurmaedje
#let natural-image(..args) = style(styles => {
  let (width, height) = measure(image(..args), styles)
  image(..args, width: width, height: height)
})

#natural-image("../tiger.jpg")
```