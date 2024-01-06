# Presentations
## Polylux

> See [polylux book](https://polylux.dev/book/)

```typ
// Get Polylux from the official package repository
#import "@preview/polylux:0.3.1": *

// Make the paper dimensions fit for a presentation and the text larger
#set page(paper: "presentation-16-9")
#set text(size: 25pt)

// Use #polylux-slide to create a slide and style it using your favourite Typst functions
#polylux-slide[
  #align(horizon + center)[
    = Very minimalist slides

    A lazy author

    July 23, 2023
  ]
]

#polylux-slide[
  == First slide

  Some static text on this slide.
]

#polylux-slide[
  == This slide changes!

  You can always see this.
  // Make use of features like #uncover, #only, and others to create dynamic content
  #uncover(2)[But this appears later!]
]
```

## Slydst
> See the documentation [there](https://github.com/glambrechts/slydst?ysclid=lr2gszrkck541184604).

Much more simpler and less powerful than polulyx:

```typ
#import "@preview/slydst:0.1.0": *

#show: slides.with(
  title: "Insert your title here", // Required
  subtitle: none,
  date: none,
  authors: (),
  layout: "medium",
  title-color: none,
)

== Outline

#outline()

= First section

== First slide

#figure(rect(width: 60%), caption: "Caption")

#v(1fr)

#lorem(20)

#definition(title: "An interesting definition")[
  #lorem(20)
]
```