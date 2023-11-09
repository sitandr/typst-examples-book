# Boxing&Blocking

```
You can use boxes to wrap anything
into text: #box(image("../tiger.jpg", height: 2em)).

Blocks will always be "separate paragraphs".
They will not fit into a text: #block(image("../tiger.jpg", height: 2em))
```

Both have similar useful properties:

```
#box(stroke: red, inset: 1em)[Box text]
#block(stroke: red, inset: 1em)[Block text]
```

## `rect`

There is also `rect` that works like `block`, but has useful default inset and stroke:

```
#rect[Block text]
```