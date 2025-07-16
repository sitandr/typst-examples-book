# States

<div class="warning">This section may be not very complete and fully updated for last Typst versions. Any contribution is very welcome!.</div>

Before we start something practical, it is important to understand states in general.

Here is a good explanation of why do we _need_ them: [Official Reference about states](https://typst.app/docs/reference/introspection/state/). It is highly recommended to read it first.

So instead of
```typ -norender
#let x = 0
#let compute(expr) = {
  // eval evaluates string as Typst code
  // to calculate new x value
  x = eval(
    expr.replace("x", str(x))
  )
  [New value is #x.]
}

#compute("10") \
#compute("x + 3") \
#compute("x * 2") \
#compute("x - 5")
```

**THIS DOES NOT COMPILE:** Variables from outside the function are read-only and cannot be modified

Instead, you should write

```typ
#let s = state("x", 0)
#let compute(expr) = [
  // updates x current state with this function
  #s.update(x =>
    eval(expr.replace("x", str(x)))
  )
  // and displays it
  New value is #context s.get().
]

#compute("10") \
#compute("x + 3") \
#compute("x * 2") \
#compute("x - 5")

The computations will be made _in order_ they are _located_ in the document. So if you create computations first, but put them in the document later... See yourself:

#let more = [
  #compute("x * 2") \
  #compute("x - 5")
]

#compute("10") \
#compute("x + 3") \
#more
```
## Context magic

So what does this magic `context s.get()` mean?

> [Context in Reference](https://typst.app/docs/reference/context/)

In short, it specifies what part of your code (or markup) can _depend on states outside_. This context-expression is packed then as one object, and it is evaluated on layout stage.

That means it is impossible to look from "normal" code at whatever is inside the `context`. This is a black box that would be known _only after putting it into the document_.

We will discuss `context` features later.

## Operations with states
### Creating new state
```typ
#let x = state("state-id")
#let y = state("state-id", 2)

#x, #y

State is #context x.get() \ // the same as
#context [State is #y.get()] \ // the same as
#context {"State is" + str(y.get())}
```

### Update

Updating is _a content_ that is an instruction. That instruction tells compiler that in this place of document the state _should be updated_.

```typ
#let x = state("x", 0)
#context x.get() \
#let _ = x.update(3)
// nothing happens, we don't put `update` into the document flow
#context x.get()

#repr(x.update(3)) // this is how that content looks \

#context x.update(3)
#context x.get() // Finally!
```

Here we can see one of _important `context` traits_: it "sees" states from outside, but can't see how they change inside it:

```typ
#let x = state("x", 0)

#context {
  x.update(3)
  str(x.get())
}
```

### ID collision

_TLDR; **Never allow colliding states.**_

<div class="warning">
States are described by their id-s, if they are the same, the code will break.
</div>

So, if you write functions or loops that are used several times, _be careful_!

```typ
#let f(x) = {
  // return new state…
  // …but their id-s are the same!
  // so it will always be the same state!
  let y = state("x", 0)
  y.update(y => y + x)
  context y.get()
}

#let a = f(2)
#let b = f(3)

#a, #b \
#raw(repr(a) + "\n" + repr(b))
```

However, this _may seem_ okay:

```typ
// locations in code are different!
#let x = state("state-id")
#let y = state("state-id", 2)

#x, #y
```

But in fact, it _isn't_:

```typ
#let x = state("state-id")
#let y = state("state-id", 2)

#context [#x.get(); #y.get()]

#x.update(3)

#context [#x.get(); #y.get()]
```
