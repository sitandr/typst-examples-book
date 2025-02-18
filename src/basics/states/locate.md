# Locate
<div class="warning">This section may be not very complete and fully updated for last Typst versions. Any contribution is very welcome!.</div>

## Location
> Link to [reference](https://typst.app/docs/reference/meta/location/)

```typ
My location: #context #here()!
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
