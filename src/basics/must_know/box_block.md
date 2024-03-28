# Boxing & Blocking
```typ
You can use boxes to wrap anything
into text: #box(image("../tiger.jpg", height: 2em)).

Blocks will always be "separate paragraphs".
They will not fit into a text: #block(image("../tiger.jpg", height: 2em))
```

Both have similar useful properties:
```typ
#box(stroke: red, inset: 1em)[Box text]
#block(stroke: red, inset: 1em)[Block text]
```

## `rect`
There is also `rect` that works like `block`, but has useful default inset and stroke:
```typ
#rect[Block text]
```

## Figures

For the purposes of adding a _figure_ to your document, use `figure` function. Don't try to use boxes or blocks there.

Figures are that things like centered images (probably with captions), tables, even code.


```typ
@tiger shows a tiger. Tigers
are animals.

#figure(
  image("../tiger.jpg", width: 80%),
  caption: [A tiger.],
) <tiger>
```

In fact, you can put there anything you want:

```typ
They told me to write a letter to you. Here it is:

#figure(
  {text(size: 5em)[I]},
  caption: [I'm cool, right?],
) 
```

