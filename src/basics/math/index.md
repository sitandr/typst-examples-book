# Math

Math is a special environment that has special features related to... math.

## Syntax
To start math environment, `$`. The spacing around `$` will make it either
_inline_ math (smaller, used in text) or _display_ math (used on math equations on their own).

```typ
// This is inline math
Let $a$, $b$, and $c$ be the side
lengths of right-angled triangle.
Then, we know that:

// This is display math
$ a^2 + b^2 = c^2 $

Prove by induction:

// You can use new lines as spacing too!
$
sum_(k=1)^n k = (n(n+1)) / 2
$
```

## Math.equation

The element that math is displayed in is called `math.equation`. You can use it for set/show rules:

```typ
#show math.equation: set text(red)

$
integral_0^oo (f(t) + g(t))/2
$
```

Any symbol/command that is available in math, _is also available_ in code mode using `math.command`:

```typ
#math.integral, #math.underbrace([a + b], [c])
```

## Letters and commands

Typst aims to have as simple and effective syntax for math as possible.
That means no special symbols, just using commands.

To make it short, Typst uses several simple rules:

- All single-letter words _turn into variables_. That includes any _unicode symbols_ too!
- All multi-letter words _turn into commands_. They may be built-in commands (available with math.something outside of math environment).
  Or they may be user-defined variables/functions. If the command **isn't defined**, there will be **compilation error**.
- To write simple text, use quotes: 
    ```typ
    $a "equals to" 2$
    ```
- You can turn it into multi-letter variables using `italic`:
    ```typ
    $(italic("mass") v^2)/2$
    ```

Commands see [there](https://typst.app/docs/reference/math/#definitions) (go to the links to see the commands).

All symbols see [there](https://typst.app/docs/reference/symbols/sym/).

## Multiline equations

To create multiline _display equation_, use the same symbol as in markup mode: `\\`:

```typ
$
a = b\
a = c
$
```

## Escaping

Any symbol that is used may be escaped with `\\`, like in markup mode. For example, you can disable fraction:

```typ
a  / b \
a \/ b
```

The same way it works with any other syntax.

