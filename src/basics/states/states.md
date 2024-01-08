# States
Before we start something practical, it is important to understand states in general.

Here is a good explanation of why do we _need_ them: [Official Reference about states](https://typst.app/docs/reference/meta/state/). It is highly recommended to read it first.

So instead of
```typ-norender
#let x = 0
#let compute(expr) = {
  // eval evaluates string as Typst code
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

**DOES NOT COMPILE:** Variables from outside the function are read-only and cannot be modified

You should write
```typ
#let s = state("x", 0)
#let compute(expr) = [
  #s.update(x =>
    eval(expr.replace("x", str(x)))
  )
  New value is #s.display().
]

#compute("10") \
#compute("x + 3") \
#compute("x * 2") \
#compute("x - 5")

The computations will be made _in order_ they are located in the document:

#let more = [
  #compute("x * 2") \
  #compute("x - 5")
]

#compute("10") \
#compute("x + 3") \
#more
```

## Operations with states
### Creating new state
```typ
#let x = state("state-id")
#let y = state("state-id", 2)

#x, #y

#x.display() \
#y.display(n => "State is " + str(n))
```

### Update
Updating is _a content_ that tells that in this place of document the state _should be updated_.

```typ
#let x = state("x", 0)
#x.display() \
#let _ = x.update(3)
// nothing happens, we don't put `update` into the document flow
#x.display() \
#repr(x.update(3)) \ // this is how that content looks \
#x.update(3)
#x.display() // Finally!
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
  y.display()
}

#let a = f(2)
#let b = f(3)

#a, #b \
#repr(a), #repr(b)
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

#x.display(), #y.display()

#x.update(3)

#x.display(), #y.display()
```
