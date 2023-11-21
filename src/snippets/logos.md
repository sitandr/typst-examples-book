# Logos & Figures
Using SVG-s images is totally fine. Totally. But if you are lazy and don't want to search for images, here are some logos you can just copy-paste in your document.

**Important**: _Typst in text doesn't need a special writing (unlike LaTeX)_. Just write "Typst", maybe "**Typst**", and it is okay.

## TeX and LaTeX
```typ

#let TeX = {
  set text(font: "New Computer Modern", weight: "regular")
  box(width: 1.7em, {
    [T]
    place(top, dx: 0.56em, dy: 0.22em)[E]
    place(top, dx: 1.1em)[X]
  })
}

#let LaTeX = {
  set text(font: "New Computer Modern", weight: "regular")
  box(width: 2.55em, {
    [L]
    place(top, dx: 0.3em, text(size: 0.7em)[A])
    place(top, dx: 0.7em)[#TeX]
  })
}

Typst is not that hard to learn when you know #TeX and #LaTeX.
```

TODO: math/emptyset
