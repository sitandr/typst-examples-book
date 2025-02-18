# Counters
<div class="warning">This section may be not very complete and fully updated for last Typst versions. Any contribution is very welcome!.</div>

Counters are special states that _count_ elements of some type.
As with states, you can create your own with identifier strings.

_Important:_ to initiate counters of elements, you need to _set numbering for them_.

## States methods
Counters are states, so they can do all things states can do. In particular, everything about `context` still applies there.

```typ
#set heading(numbering: "1.")

= Background
#counter(heading).update(3)
#counter(heading).update(n => n * 2)

== Analysis
Current heading number: #context counter(heading).get().

You can also display it with a special method that can render it beautifully with arbitrary numbering pattern: #context counter(heading).display("I: 1.").

Or use current display style: #context counter(heading).display()

It depends on current set style:

#set heading(numbering: ":1:1:")
#context counter(heading).display()
```

Ok, here are some more examples. They are quite simple, so I hope no comments are needed. `:)`

```typ
#let mine = counter("mycounter")
#context mine.display()

#mine.step()
#context mine.display()

#mine.update(c => c * 3)
#context mine.display()
```

Counters also support displaying _both current and final values_ out-of-box, this requires option `both: true`:

```typ
#set heading(numbering: "1.")

= Introduction
Some text here.

#context counter(heading).display(both: true) \
#context counter(heading).display("1 of 1", both: true) \
#context counter(heading).display(
  (num, max) => [#num of #max],
   both: true
)

= Background
The current value is: #context counter(heading).display()
```

## Step

That's quite easy, for counters you can increment value using `step`. It works the same way as `update`.
```typ
#set heading(numbering: "1.")

= Introduction
#context counter(heading).step()

= Analysis
Let's skip 3.1.
#context counter(heading).step(level: 2)

== Analysis
At #context counter(heading).display().
```

## You can use counters in your functions:
```typ
#let c = counter("theorem")
#let theorem(it) = block[
  #c.step()
  *Theorem #context c.display():*
  #it
]

#theorem[$1 = 1$]
#theorem[$2 < 3$]
```
