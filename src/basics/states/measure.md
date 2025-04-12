# Measure, Layout
<div class="warning">This section is outdated. It may be still useful, but it is strongly recommended to study new context system (using the reference).</div>

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

So yep, you are right. We need the `context`.

```typ
#let thing(body) = context {
  let size = measure(body)
  [Width of "#body" is #size.width]
}

#thing[Hey] \
#thing[Welcome]
```

# Layout

Layout is similar to `measure`, but it returns current scope **parent size**.

If you are putting elements in block, that will be block's size. If you are just putting right on the page, that will be page's size.

For some technical reasons, however, it can't use `context` and needs to use the very similar scheme (it is the one the `context` has emerged from, in fact):

```typ
/// It's a black box that receives the parent size and renders something with it:
#layout(size => {
  let half = 50% * size.width
  [Half a page is #half wide.]
})
```

It may be extremely useful to combine `layout` with `measure`, to get width of things that depend on parent's size:

```typ
#let text = lorem(30)
#layout(size => context [
  #let (height,) = measure(
    block(width: size.width, text)
  )
  This text is #height high with
  the current page width: \
  #text
])
```