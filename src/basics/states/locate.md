# Locate
> Link to [reference](https://typst.app/docs/reference/meta/locate/)

Many things should be recompiled depending on some external things.
To understand, what those external things are, it should be a content that
_is put into a document_. It works roughly the same way as `state.update`.

Locate takes a function that, when that `locate` is put in the document
and given a _location in the document_, returns some content instead of that `locate`.

## Location
> Link to [reference](https://typst.app/docs/reference/meta/location/)

```typ
#locate(loc => [
  My location: \
  #loc.position()!
])
```

## `state.at(loc)`
Given a location, returns _value of state in that location_.
That allows kind of _time travel_, you can get location at _any place of document_.

`state.display` is roughly equivalent to
```typ
#let display(state) = locate(location => {
  state.at(location)
})

#let x = state("x", 0)
#x.display() \
#x.update(n => n + 3)
#display(x)
```

## Final
Calculates the _final value_ of state.

The location there is needed to restrict what content will change within recompilations.
That greatly increases speed and better resolves "conflicts".
```typ
#let x = state("x", 5)
x = #x.display() \

#locate(loc => [
  The final x value is #x.final(loc)
])

#x.update(-3)
x = #x.display()

#x.update(n => n + 1)
x = #x.display()
```

## Convergence
Sometimes layout _will not converge_. For example, imagine this:

```typ
#let x = state("x", 5)
x = #x.display() \

#locate(loc => [
  // let's set x to final x + 1
  // and see what will go on?
  #x.update(x.final(loc) + 1)
  #x.display()
])
```

**WARNING**: layout did not converge within 5 attempts

It is impossible to resolve that layout, so Typst gives up and gives you a warning.

That means you _should be careful_ with states!

This is a _dark, **dark magic**_ that requires large sacrifices!
