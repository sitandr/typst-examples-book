# Types, part I
Each value in Typst has a type. You don't have to specify it, but it is important.

## Content (`content`)
> [Link to Reference](https://typst.app/docs/reference/foundations/content/).

We have already seen it. A type that represents what is displayed in document.
```typ
#let c = [It is _content_!]

// Check type of c
#(type(c) == content)

#c

// repr gives an "inner representation" of value
#repr(c)
```

**Important:** It is very hard to convert _content_ to _plain text_, as _content_ may contain *anything*! Sp be careful when passing and storing content in variables.

## None (`none`)
Nothing. Also known as `null` in other languages. It isn't displayed, converts to empty content.
```typ
#none
#repr(none)
```

## String (`str`)
> [Link to Reference](https://typst.app/docs/reference/foundations/str/).

String contains only plain text and no formatting. Just some chars. That allows us to work with chars:
```typ
#let s = "Some large string. There could be escape sentences: \n,
 line breaks, and even unicode codes: \u{1251}"
#s \
#type(s) \
`repr`: #repr(s)

#let s = "another small string"
#s.replace("a", sym.alpha) \
#s.split(" ") // split by space
```

## Boolean (`bool`)
> [Link to Reference](https://typst.app/docs/reference/foundations/bool/).

true/false. Used in `if` and many others
```typ
#let b = false
#b \
#repr(b) \
#(true and not true or true) = #((true and (not true)) or true) \
#if (4 > 3) {
  "4 is more than 3"
}
```

## Integer (`int`)
> [Link to Reference](https://typst.app/docs/reference/foundations/int/).

A whole number.

The number can also be specified as hexadecimal, octal, or binary by starting it with a zero followed by either x, o, or b.

You can convert a value to an integer with this type's constructor.
```typ
#let n = 5
#n \
#(n += 1) \
#n \
#calc.pow(2, n) \
#type(n) \
#repr(n)
```

```typ
#(1 + 2) \
#(2 - 5) \
#(3 + 4 < 8)
```

```typ
#0xff \
#0o10 \
#0b1001
```

```typ
#int(false) \
#int(true) \
#int(2.7) \
#(int("27") + int("4"))
```

## Float (`float`)
> [Link to Reference](https://typst.app/docs/reference/foundations/float/).

Works the same way as integer, but can store floating point numbers.
However, precision may be lost.
```typ
#let n = 5.0

// You can mix floats and integers, 
// they will be implicitly converted
#(n += 1) \
#calc.pow(2, n) \
#(0.2 + 0.1) \
#type(n) 
```

```
#3.14 \
#1e4 \
#(10 / 4)
```

```
#float(40%) \
#float("2.7") \
#float("1e5")
```
