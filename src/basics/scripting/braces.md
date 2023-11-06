# Braces, brackets and default
## Square brackets
You may remember that square brackets
convert everything inside to *content*.

```
#let v = [Some text, _markup_ and other #strong[functions]]
#v
```

We may use same for functions bodies:

```
#let f(name) = [Hello, #name]
#f[World] // also don't forget we can use it to pass content!
```

**Important:** It is very hard to convert _content_ to _plain text_, as _content_ may contain *anything*!

## Braces
However, we often want to use code inside functions.
That's when we use `{}`:
```
#let f(name) = {
    // this is code mode

    // First part of our output
    "Hello, "

    // we check if name is empty, and if it is,
    // insert placeholder
    if name == "" {
        "anonym"
    } else {
        name
    }
    
    // finish sentence
    "!"
}

#f("")
#f("Joe")
#f("world")
```

## Default values

What we made just now was inventing "default values".
They are very common in styling, so there is a special syntax for them:

```
#let f(name: "anonym") = [Hello, #name!]
#f()
#f(name: "Joe")
#f(name: "world")
```

You may have noticed that the argument became _named_ now.
In Typst, named argument is an argument _that has default value_.
