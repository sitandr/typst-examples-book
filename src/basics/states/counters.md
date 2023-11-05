# Counters

```
#set heading(numbering: "1.")

= Introduction
Some text here.

= Background
The current value is:
#counter(heading).display()

Or in roman numerals:
#counter(heading).display("I")
```

```
#set heading(numbering: "1.")

= Introduction
#counter(heading).step()

= Background
#counter(heading).update(3)
#counter(heading).update(n => n * 2)

= Analysis
Let's skip 7.1.
#counter(heading).step(level: 2)

== Analysis
Still at #counter(heading).display().
```

```
#let mine = counter("mycounter")
#mine.display() \
#mine.step()
#mine.display() \
#mine.update(c => c * 3)
#mine.display() \
```

```
#let c = counter("theorem")
#let theorem(it) = block[
  #c.step()
  *Theorem #c.display():* #it
]

#theorem[$1 = 1$]
#theorem[$2 < 3$]
```