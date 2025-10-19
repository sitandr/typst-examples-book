# First line indent

[Official docs](https://typst.app/docs/reference/model/par/#parameters-first-line-indent)

A very common need in terms of text formatting is adding indent to first line of all paragraph. That is known as pilcrow (¶) or "red line" in some languages or conventions.

By default, Typst applies it to all paragraphs _except the first_ (or one coming after title). To change it, use (all: true):

```typ
#set block(spacing: 1.2em)
#set par(
  first-line-indent: 1.5em,
  spacing: 0.65em,
)

The first paragraph is not affected
by the indent.

But the second paragraph is.

#line(length: 100%)

#set par(first-line-indent: (
  amount: 1.5em,
  all: true,
))

Now all paragraphs are affected
by the first line indent.

Even the first one.
```
