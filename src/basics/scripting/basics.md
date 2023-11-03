# Basics

```
Let's start with _variables_.
The concept is very simple, just some value you can reuse:

#let author = "John Doe"

This is a book by #author. #author is a great guy.

#quote(block: true, attribution: author)[
    \<Some quote\>
]
```

You can store _any_ Typst value in variable:

```
#let block_text = block(stroke: red, inset: 1em)[Text]

#block_text

#figure(caption: "The block", block_text)
```