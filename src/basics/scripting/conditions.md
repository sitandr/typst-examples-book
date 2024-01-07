# Conditions & loops

## Conditions
> See [official documentation](https://typst.app/docs/reference/scripting/#conditionals).

In Typst, you can use `if-else` statements.
This is especially useful inside function bodies to vary behavior depending on arguments types or many other things.

```typ
#if 1 < 2 [
  This is shown
] else [
  This is not.
]
```

Of course, `else` is unnecessary:

```typ
#let a = 3

#if a < 4 {
  a = 5
}

#a
```

You can also use `else if` statement (known as `elif` in Python):

```typ
#let a = 5

#if a < 4 {
  a = 5
}
else if a < 6 {
  a = -3
}

#a
```

### Booleans

`if, else if, else` accept _only boolean_ values as a switch.
You can combine booleans as described in [types section](./types.md#boolean-bool):

```typ
#let a = 5

#if (a > 1 and a <= 4) or a == 5 [
    `a` matches the condition
]
```

## Loops

> See [official documentation](https://typst.app/docs/reference/scripting/#loops).

There are two kinds of loops: `while` and `for`. While repeats body while the condition is met:

```typ
#let a = 3

#while a < 100 {
    a *= 2
    str(a)
    " "
}
```

`for` iterates over all elements of sequence. The sequence may be an `array`, `string`
or `dictionary` (`for` iterates over its _key-value pairs_).

```typ
#for c in "ABC" [
  #c is a letter.
]
```

To iterate to all numbers from `a` to `b`, use `range(a, b+1)`:

```typ
#let s = 0

#for i in range(3, 6) {
    s += i
    [Number #i is added to sum. Now sum is #s.]
}
```

Because range is end-exclusive his is equal to

```typ
#let s = 0

#for i in (3, 4, 5) {
    s += i
    [Number #i is added to sum. Now sum is #s.]
}
```

```typ
#let people = (Alice: 3, Bob: 5)

#for (name, value) in people [
    #name has #value apples.
]
```

### Break and continue

Inside loops can be used `break` and `continue` commands. `break` breaks loop, jumping outside. `continue` jumps to next loop iteration.

See the difference on these examples:

```typ
#for letter in "abc nope" {
  if letter == " " {
    // stop when there is space
    break
  }

  letter
}
```

```typ
#for letter in "abc nope" {
  if letter == " " {
    // skip the space
    continue
  }

  letter
}
```
