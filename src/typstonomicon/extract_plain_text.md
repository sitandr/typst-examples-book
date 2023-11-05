# Extracting plain text

```
// author: laurmaedge
#let plain-text(it) = {
  if it == [ ] {
    " "
  } else if it.func() == text {
    it.text
  } else if it.func() == smartquote {
    if it.double { "\"" } else { "'" } // "
  } else if it.func() == [].func() {
    it.children.map(plain-text).join()
  } else {
    it
  }
}

#locate(loc => {
  query(heading.where(level: 2).after(<Details>), loc).map(it => {
    plain-text(it.body)
  })
})

= Test <Details>

== Foo
== Bar
== Baz (Baj) "ok"
```