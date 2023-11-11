# Logos & Figures
Using SVG-s images is totally fine. Totally. But if you are lazy and don't want to search for images, here are some logos you can just copy-paste in your document.

**Important**: _Typst in text doesn't need a special writing (unlike LaTeX)_. Just write "Typst", maybe "**Typst**", and it is okay.

## LaTeX
```typ
#let LaTeX = {
  set text(font: "New Computer Modern", weight: "regular")
  box(width: 2.55em, {
    [L]
    place(top, dx: 0.3em, text(size: 0.7em)[A])
    place(top, dx: 0.7em)[T]
    place(top, dx: 1.26em, dy: 0.22em)[E]
    place(top, dx: 1.8em)[X]
  })
}

I'd like to avoid writing #LaTeX if I can.
```

// TODO: math/emptyset
