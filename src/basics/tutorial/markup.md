# Markup language
## Starting
```typ
Starting typing in Typst is easy.
No including packages or other weird things.

Blank line will move text to new paragraph.

Btw, you can use any language and unicode symbols
with no problems by default: ßçœ̃ɛ̃ø∀αβёыა😆…

(as long as current font supports it)
```

## Markup
```typ
= Markup

This was a heading. Number of `=` in front of name corresponds to heading level.

===== Fifth-level heading

Okay, let's move to _emphasis_ and *bold* text.
Markup syntax is generally similar to
`AsciiDoc` (this was `raw` for monospace text!)
```

## New lines & Escaping
```typ
You can break \
line anywhere you \
want using \\ symbol.

Also you can use that symbol to
escape \_all the symbols you want\_,
if you don't want it to be interpreted as markup
or other special symbols.
```

## Comments & codeblocks
```````typ
You can write comments with `//` and `/* comment */`:
// Like this
/* Or even like
this */

```typ
Just in case you didn't read source,
this is how it is written:

// Like this
/* Or even like
this */

By the way, I'm writing it all in a _fenced code block_ with *syntax highlighting*!
```
```````

## Smart quotes
```typ
== What else?

There are not much things in basic "markup" syntax,
but we will see much more interesting things very soon!
I hope you noticed auto-matched "smart quotes" there.
```

## Lists
```typ
- Writing lists in a simple way is great.
- Nothing complex, start your points with `-`
  and this will become a list.
  - Indented lists are created via indentation.

+ Numbered lists start with `+` instead of `-`.
+ There is no alternative markup syntax for lists
+ So just remember `-` and `+`, all other symbols
  wouldn't work in an unintended way.
  + That is a general property of Typst's markup.
  + Unlike Markdown, there is only one way
    to write something with it.
```

**Notice:**
```typ
Typst doesn't support markdown-like syntax for lists:
1. Apple
1. Pair
1. Soup
```

## Math
```typ
I will just mention math ($a + b/c = sum_i x^i$) 
is possible there and is quite pretty:

$
7.32 beta +
  sum_(i=0)^nabla
    (Q_i (a_i - epsilon)) / 2
$

To learn more about math, see corresponding chapter.
```
