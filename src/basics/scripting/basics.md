# Basics
## Variables I
Let's start with _variables_.

The concept is very simple, just some value you can reuse:
```typ
#let author = "John Doe"

This is a book by #author. #author is a great guy.

#quote(block: true, attribution: author)[
  \<Some quote\>
]
```

## Variables II
You can store _any_ Typst value in variable:

```typ
#let block_text = block(stroke: red, inset: 1em)[Text]

#block_text

#figure(caption: "The block", block_text)
```

## Functions
We have already seen some "custom" functions
in [Advanced Styling](../tutorial/advanced_styling.md) chapter.

Functions are values that take some values
and output some values:

```typ
// This is a syntax that we have seen earlier
#let f = (name) => "Hello, " + name

#f("world!")
```

### Alternative syntax
You can write the same shorter:

```typ
// The following syntaxes are equivalent
#let f = (name) => "Hello, " + name
#let f(name) = "Hello, " + name

#f("world!")
```
