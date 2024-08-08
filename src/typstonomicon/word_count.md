# Word count

<div class="warning">This chapter is deprecated now. It will be removed soon.</div>

## Recommended solution

Use `wordometr` [package](https://github.com/Jollywatt/typst-wordometer):

```typ
#import "@preview/wordometer:0.1.0": word-count, total-words

#show: word-count

In this document, there are #total-words words all up.

#word-count(total => [
  The number of words in this block is #total.words
  and there are #total.characters letters.
])
```

## Just count _all_ words in document
```typ
// original author: laurmaedje
#let words = counter("words")
#show regex("\p{L}+"): it => it + words.step()

== A heading
#lorem(50)

=== Strong chapter
#strong(lorem(25))

// it is ignoring comments

#align(right)[(#words.display() words)]
```

## Count only some elements, ignore others

```typ
// original author: jollywatt
#let count-words(it) = {
    let fn = repr(it.func())
    if fn == "sequence" { it.children.map(count-words).sum() }
    else if fn == "text" { it.text.split().len() }
    else if fn in ("styled") { count-words(it.child) }
    else if fn in ("highlight", "item", "strong", "link") { count-words(it.body) }
    else if fn in ("footnote", "heading", "equation") { 0 }
    else { 0 }
}

#show: rest => {
    let n = count-words(rest)
    rest + align(right, [(#n words)])
}

== A heading (shouldn't be counted)
#lorem(50)

=== Strong chapter
#strong(lorem(25)) // counted too!
```