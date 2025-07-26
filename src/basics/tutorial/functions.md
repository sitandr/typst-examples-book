# Functions
## Functions

```typ
Okay, let's now move to more complex things.

First of all, there are *lots of magic* in Typst.
And it major part of it is called "scripting".

To go to scripting mode, type `#` and *some function name*
after that. We will start with _something dull_:

#lorem(50)

_That *function* just generated 50 "Lorem Ipsum" words!_
```

## More functions

```typ
#underline[functions can do everything!]

#text(orange)[L]ike #text(size: 0.8em)[Really] #sub[E]verything!

#figure(
  caption: [
    This is a screenshot from one of first theses written in Typst. \
    _All these things are written with #text(blue)[custom functions] too._
  ],
  image("../boxes.png", width: 80%)
)

In fact, you can #strong[forget] about markup
and #emph[just write] functions everywhere!

#list[
  All that markup is just a #emph[syntax sugar] over functions!
]
```

## How to call functions

```typ
First, start with `#`. Then write the name.
Finally, write some parentheses and maybe something inside.

You can navigate lots of built-in functions
in #link("https://typst.app/docs/reference/")[Official Reference].

#quote(block: true, attribution: "Typst Examples Book")[
  That's right, links, quotes and lots of
  other document elements are created with functions.
]
```

## Function arguments

```typ
There are _two types_ of function arguments:

+ *Positional.* Like `50` in `lorem(50)`.
  Just write them in parentheses and it will be okay.
  If you have many, use commas.
+ *Named.* Like in `#quote(attribution: "Whoever")`.
  Write the value after a name and a colon.

If argument is named, it has some _default value_.
To find out what it is, see
#link("https://typst.app/docs/reference/")[Official Typst Reference].
```

## Content

Now we should probably try writing our own functions

```typ
The most "universal" type in Typst language is *content*.
Everything you write in the document becomes content.

#[
  But you can explicitly create it with
  _scripting mode_ and *square brackets*.

  There, in square brackets, you can use any markup
  functions or whatever you want.
]
```

## Markup and code modes
```typ
When you use `#`, you are "switching" to code mode.
When you use `[]`, you turn back into _markup_ (or content) mode:

// +-- going from markup (the default mode) to scripting for that function
// |                 +-- scripting mode: calling `text`, the last argument is markup
// |     first arg   |
// v     vvvvvvvvv   vvvv
   #rect(width: 5cm, text(red)[hello *world*])
//  ^^^^                       ^^^^^^^^^^^^^ just a markup argument for `text`
//  |
//  +-- calling `rect` in scripting mode, with two arguments: width and other content
```

## Passing content into functions
```typ
So what are these square brackets after functions?

If you *write content right after
function, it will be passed as positional argument there*.

#quote(block: true)[
  So #text(red)[_that_] allows me to write
  _literally anything in things
  I pass to #underline[functions]!_
]
```

## Passing content, part II

`````typ
So, just to make it clear, when I write

```typ
- #text(red)[red text]
- #text([red text], red)
- #text("red text", red)
//      ^        ^
// Quotes there mean a plain string, not a content!
// This is just text.
```

It all will result in a #text([red text], red).
`````
