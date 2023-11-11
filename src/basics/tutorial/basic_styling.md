# Basic styling


## Let's start with justifying
```typ
#set page(width: 15cm, margin: (left: 4cm, right: 4cm))

Okay, that was great, but using functions everywhere,
specifying all arguments every time is awfully cumbersome.

That's way Typst has _rules_. No, not for you, for the document.

#set par(justify: true)

And the first rule we will consider there is `set` rule.
As you see, I've just used it on `par` (which is short from paragraph)
and now all paragraphs became _justified_.

It will apply to all paragraphs after the rule,
but will work only in it's _scope_ (we will discuss them later).

#par(justify: false)[
    Of course, you can override a `set` rule.
    This rule just sets the _default value_
    of an argument of an element.
]

And in start of this document (snippet) 
I've reduced page size to make justifying more visible,
and also increased margins to add blank space on edges. 
```

## A bit about length units

```typ
There are several absolute length units in Typst:

#set rect(height: 1em)

#table(
    columns: 2,
    [Points], rect(width: 72pt),
    [Millimeters], rect(width: 25.4mm),
    [Centimeters], rect(width: 2.54cm),
    [Inches], rect(width: 1in),
    [Relative to font size], rect(width: 6.5em)
)

`1 em` = current font size.\
It is a very convenient unit,
so we are going to use it a lot

```

## Setting something else

Of course, you can use `set` rule with all built-in functions
and all their named arguments to make something "default".

For example, let's make all quotes there authored by that book:

```typ
#set quote(block: true, attribution: [Typst Examples Book])

#quote[
    Typst is great!
]

#quote[
    The problem with quotes on the internet is
    that it is hard to verify their authenticity.
]
```

## Opinionated defaults

That allows you to set the defaults for the document in general as you want:

```typ
#set par(justify: true)
#set list(indent: 1em)
#set enum(indent: 1em)
#set page(numbering: "1")

- List item
- List item

+ Enum item
+ Enum item
```

Don't complain about bad defaults! Set your own.

## Numbering

```typ
= Numbering
Some of elements have a property called "numbering".
They accept so-called "numbering patterns" and
are very useful with set rules. Let's see what I mean.

#set heading(numbering: "I.1:")

= This is first level
= Another first
== Second
== Another second
=== Now third
== And second again
= Now returning to first
= These are actual romanian numerals
```

Of course, there are lots of other cool properties
that can be _set_, so feel free to dive into Reference
and explore them!

And we are now moving to something much more interesting…