# Braces, brackets and default
## Square brackets
You may remember that square brackets convert everything inside to *content*.
```typ
#let v = [Some text, _markup_ and other #strong[functions]]
#v
```

We may use same for functions bodies:
```typ
#let f(name) = [Hello, #name]
#f[World] // also don't forget we can use it to pass content!
```

**Important:** It is very hard to convert _content_ to _plain text_, as _content_ may contain *anything*! So be careful when passing and storing content in variables.

## Braces
However, we often want to use code inside functions.
That's when we use `{}`:
```typ
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

## Scopes
**This is a very important thing to remember**.

_You can't use variables outside of scopes they are defined (unless it is file root, then you can import them)_. _Set and show rules affect things in their scope only._
```typ
#{
  let a = 3;
}
// can't use "a" there.

#[
  #show "true": "false"

  This is true.
]

This is true.
```

## Return
**Important**: by default braces return anything that "returns" into them. For example,
```typ
#let change_world() = {
  // some code there changing everything in the world
  str(4e7)
  // another code changing the world
}

#let g() = {
  "Hahaha, I will change the world now! "
  change_world()
  " So here is my long evil monologue..."
}

#g()
```

To avoid returning everything, return only what you want explicitly, otherwise everything will be joined:
```typ
#let f() = {
  "Some long text"
  // Crazy numbers
  "2e7"
  return none
}

// Returns nothing
#f()
```

## Default values
What we made just now was inventing "default values".

They are very common in styling, so there is a special syntax for them:
```typ
#let f(name: "anonym") = [Hello, #name!]

#f()
#f(name: "Joe")
#f(name: "world")
```

You may have noticed that the argument became _named_ now.
In Typst, named argument is an argument _that has default value_.
