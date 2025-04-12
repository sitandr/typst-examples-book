# Duplicate content

<div class="warning">
    Notice that this implementation will mess up with labels and similar things.
    For complex cases see one below.
</div>
```typ
#set page(paper: "a4", flipped: true)
#show: body => grid(
  columns: (1fr, 1fr),
  column-gutter: 1cm,
  body, body,
)
#lorem(200)
```

## Advanced
```typ
/// author: frozolotl
#set page(paper: "a4", flipped: true)
#set heading(numbering: "1.1")
#show ref: it => {
  if it.element != none {
    it
  } else {
    let targets = query(it.target)
    if targets.len() == 2 {
      let target = targets.first()
      if target.func() == heading {
        let num = numbering(target.numbering, ..counter(heading).at(target.location()))
        [#target.supplement #num]
      } else if target.func() == figure {
        let num = numbering(target.numbering, ..target.counter.at(target.location()))
        [#target.supplement #num]
      } else {
        it
      }
    } else {
      it
    }
  }
}
#show link: it => context {
  let dest = query(it.dest)
  if dest.len() == 2 {
    link(dest.first().location(), it.body)
  } else {
    it
  }
}
#show: body => context grid(
  columns: (1fr, 1fr),
  column-gutter: 1cm,
  body,
  {
    let reset-counter(kind) = counter(kind).update(counter(kind).get())
    reset-counter(heading)
    reset-counter(figure.where(kind: image))
    reset-counter(figure.where(kind: raw))
    set heading(outlined: false)
    set figure(outlined: false)
    body
  },
)

#outline()

= Foo <foo>
See @foo and @foobar.

#figure(rect[This is an image], caption: [Foobar], kind: raw) <foobar>

== Bar
== Baz
#link(<foo>)[Click to visit Foo]
```