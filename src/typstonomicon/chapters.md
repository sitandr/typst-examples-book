# Create zero-level chapters

```typ
// author: tinger

#let chapter = figure.with(
  kind: "chapter",
  // same as heading
  numbering: none,
  // this cannot use auto to translate this automatically as headings can, auto also means something different for figures
  supplement: "Chapter",
  // empty caption required to be included in outline
  caption: [],
)

// emulate element function by creating show rule
#show figure.where(kind: "chapter"): it => {
  set text(22pt)
  counter(heading).update(0)
  if it.numbering != none { strong(it.counter.display(it.numbering)) } + [ ] + strong(it.body)
}

// no access to element in outline(indent: it => ...), so we must do indentation in here instead of outline
#show outline.entry: it => {
  if it.element.func() == figure {
    // we're configuring chapter printing here, effectively recreating the default show impl with slight tweaks
    let res = link(it.element.location(), 
      // we must recreate part of the show rule from above once again
      if it.element.numbering != none {
        numbering(it.element.numbering, ..it.element.counter.at(it.element.location()))
      } + [ ] + it.element.body
    )

    if it.fill != none {
      res += [ ] + box(width: 1fr, it.fill) + [ ] 
    } else {
      res += h(1fr)
    }

    res += link(it.element.location(), it.page())
    strong(res)
  } else {
    // we're doing indenting here
    h(1em * it.level) + it
  }
}

// new target selector for default outline
#let chapters-and-headings = figure.where(kind: "chapter", outlined: true).or(heading.where(outlined: true))

//
// start of actual doc prelude
//

#set heading(numbering: "1.")

// can't use set, so we reassign with default args
#let chapter = chapter.with(numbering: "I")

// an example of a "show rule" for a chapter
// can't use chapter because it's not an element after using .with() anymore
#show figure.where(kind: "chapter"): set text(red)

//
// start of actual doc
//

// as you can see these are not elements like headings, which makes the setup a bit harder
// because the chapters are not headings, the numbering does not include their chapter, but could using a show rule for headings

#outline(target: chapters-and-headings)

#chapter[Chapter]
= Chap Heading
== Sub Heading

#chapter[Chapter again]
= Chap Heading
= Chap Heading
== Sub Heading
=== Sub Sub Heading
== Sub Heading

#chapter[Chapter yet again]
```
