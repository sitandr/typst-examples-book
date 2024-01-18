# Classes

> See [official documentation](https://typst.app/docs/reference/math/class/)

Each math symbol has its own "class", the way it behaves. That's one of the main reasons why they are layouted differently.

## Classes

```typ
$
a b c\
a class("normal", b) c\
a class("punctuation", b) c\
a class("opening", b) c\
a lr(b c]) c\
a lr(class("opening", b) c ]) c // notice it is moved vertically \
a class("closing", b) c\
a class("fence", b) c\
a class("large", b) c\
a class("relation", b) c\
a class("unary", b) c\
a class("binary", b) c\
a class("vary", b) c\
$
```

## Setting class for symbol

```typ
Default:

$square circle square$

With `#h(0)`:

$square #h(0pt) circle #h(0pt) square$

With `math.class`:

#show math.circle: math.class.with("normal")
$square circle square$
```
