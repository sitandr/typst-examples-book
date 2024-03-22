# Counters
<div class="warning">This section is outdated. It may be still useful, but it is strongly recommended to study new context system (using the reference).</div>


Counters are special states that _count_ elements of some type.
As with states, you can create your own with identifier strings.

_Important:_ to initiate counters of elements, you need to _set numbering for them_.

## States methods
Counters are states, so they can do all things states can do.

```typ
#set heading(numbering: "1.")

= Background
#counter(heading).update(3)
#counter(heading).update(n => n * 2)

== Analysis
Current heading number: #counter(heading).display().
```

```typ
#let mine = counter("mycounter")
#mine.display()

#mine.step()
#mine.display()

#mine.update(c => c * 3)
#mine.display()
```

## Displaying counters
```typ
#set heading(numbering: "1.")

= Introduction
Some text here.

= Background
The current value is:
#counter(heading).display()

Or in roman numerals:
#counter(heading).display("I")
```

Counters also support displaying _both current and final values_ out-of-box:

```typ
#set heading(numbering: "1.")

= Introduction
Some text here.

#counter(heading).display(both: true) \
#counter(heading).display("1 of 1", both: true) \
#counter(heading).display(
  (num, max) => [#num of #max],
   both: true
)

= Background
The current value is: #counter(heading).display()
```

## Step
That's quite easy, for counters you can increment value using `step`. It works the same way as `update`.
```typ
#set heading(numbering: "1.")

= Introduction
#counter(heading).step()

= Analysis
Let's skip 3.1.
#counter(heading).step(level: 2)

== Analysis
At #counter(heading).display().
```

## You can use counters in your functions:
```typ
#let c = counter("theorem")
#let theorem(it) = block[
  #c.step()
  *Theorem #c.display():*
  #it
]

#theorem[$1 = 1$]
#theorem[$2 < 3$]
```
