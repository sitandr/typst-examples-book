# Measure, Layout
## Style & Measure

> Style [documentation](https://typst.app/docs/reference/foundations/style/).

> Measure [documentation](https://typst.app/docs/reference/layout/measure/).

`measure` returns _the element size_. This command is extremely helpful when doing custom layout with `place`.

However, there is a catch. Element size depends on styles, applied to this element.

```typ
#let content = [Hello!]
#content
#set text(14pt)
#content
```

So if we will set the big text size for some part of our text, to measure the element's size,
we have to know _where the element is located_. Without knowing it, we can't tell what styles should be applied.

So we need a scheme similar to `locate`.

This is what `styles` function is used for. It is _a content_, which, when located in document, calls a function inside on _current styles_.

Now, when we got fixed `styles`, we can get the element's size using `measure`:

```typ
#let thing(body) = style(styles => {
  let size = measure(body, styles)
  [Width of "#body" is #size.width]
})

#thing[Hey] \
#thing[Welcome]
```

# Layout

Layout is similar to `measure`, but it returns current scope **parent size**.

If you are putting elements in block, that will be block's size. If you are just putting right on the page, that will be page's size.

As parent's size depends on it's place in document, it uses the similar scheme to `locate` and `style`:

```typ
#layout(size => {
  let half = 50% * size.width
  [Half a page is #half wide.]
})
```

It may be extremely useful to combine `layout` with `measure`, to get width of things that depend on parent's size:

```typ
#let text = lorem(30)
#layout(size => style(styles => [
  #let (height,) = measure(
    block(width: size.width, text),
    styles,
  )
  This text is #height high with
  the current page width: \
  #text
]))
```