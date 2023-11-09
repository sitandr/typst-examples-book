# States

Before we start something practical, it is important to understand states in general.

Here is a good explanation of why do we _need_ them: [Official Reference about states](https://typst.app/docs/reference/meta/state/). It is highly recommended to read it first.

So instead of

```no-render
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

```
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

```
#let x = state("state-id")
#let y = state("state-id", 2)

#x, #y

#x.display()\
#y.display(n => "State is " + str(n))
```

### Update

Updating is _a content_ that tells that in this place of document the state _should be updated_.

```
#let x = state("x", 0)
#x \
#let _ = x.update(3)
// nothing happens, we don't put x into the document flow
#x \
#repr(x.update(3))\ // this is how that content looks\
#x.update(3)
#x // Finally!
```

### ID collision

_You almost never have to worry about colliding state id-s._
States are described not only by their id-s, but also by their _location in code_.

However, if you write functions or loops that are used several times, _be careful_!

```
#let f(x) = {
    // return new state…
    // …but their id-s and code locations are the same!
    // so it will always be the same state!
    let y = state("x", 0)
    y.update(y => y + x)
    y.display()
}

#let a = f(2)
#let b = f(3)

#a, #b\
#repr(a), #repr(b)
```

However, this is okay:

```
// locations in code are different!
#let x = state("state-id")
#let y = state("state-id", 2)

#x, #y
```
