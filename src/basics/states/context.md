## Context for styling
<div class="warning">This section may be not very complete and fully updated for last Typst versions. Any contribution is very welcome!.</div>

> [Context in Reference](https://typst.app/docs/reference/context/)

(if you haven't read the `state` section yet, read it; the `context` is started to be discussed there)

As we've already seen in `states` chapter, `context` is kind of object that stores the "layout instructions" of content that may be heavily dependent on outer states. These instructions are rendered later.

What is important to know is that _the "outer states" I mention there include not just `state`_ (and counters, that are just special states for counting), but also _styling_.

What do I mean?

Well, see yourself:

### Getting current style

```typ
Current font: #context text.font
```

We just got the current font that easily, and that works basically for **any settable property**! Isn't that neat?

See another example that demonstrates the properties of context better. Let's create a `box` that would be always the color of text:

```typ
#let colorful-rect = context box(stroke: text.fill, inset: 0.3em)[#repr(text.fill)]

Current color in box of the same color: #colorful-rect.

#set text(red)

Current color in box of the same color: #colorful-rect.
```

### How to get things out of context?

That's the neat part, _you don't_!

Why? That's easy: for Typst the `context` block is a black box that can be opened only during rendering, when put inside the documents.

So if you want to get something, you should get it _inside `context`_.

### Writing functions

Important fact: function, as any other content, may be _context-depending_ without any declarations. And it is usually better to allow user to wrap them in context themselves instead of putting it in `context`.


Let's say you want to create a list that depends on some style (or maybe `state`) things. It would require context, so you can wrap it in context:

```typ
(Bad)

#let page-dimensions = context (page.width, page.height)
#page-dimensions, representation of that object is: #repr(page-dimensions)
```

That object would be almost useless. It's black box, so you can only put into the doc and that's all.

Hover, you can do this instead:

```typ
(Good!)

// To be context-dependent function it needs to be function, not just a fixed content
#let page-dimensions() = (page.width, page.height)

#context page-dimensions()

#context [
    #let (x, y) = page-dimensions()
    Half-width is: #(x/2), height is #y
]
```

So with context-dependent functions you allow user to put `context` anywhere they want.

### Rules inside of context

As we've already discussed, `context` captures the _outer_ state of the document, and doesn't see anything that happens inside it. So if you do

```typ
#context [
    Text, color: #text.fill

    #set text(blue)

    Text, color: #text.fill
]
```

...right, the rules inside wouldn't affect style inside the context.