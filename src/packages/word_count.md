# Counting words

## Wordometr

```typ
#import "@preview/wordometer:0.1.4": word-count, total-words

#show: word-count

In this document, there are #total-words words all up.

#word-count(total => [
  The number of words in this block is #total.words
  and there are #total.characters letters.
])
```

### Excluding elements
You can exclude elements by name (e.g., `"caption"`), function (e.g., `figure.caption`), where-selector (e.g., `raw.where(block: true)`), or `label` (e.g., `<no-wc>`).

```typ
#import "@preview/wordometer:0.1.4": word-count, total-words

#show: word-count.with(exclude: (heading.where(level: 1), strike))

= This Heading Doesn't Count
== But I do!

In this document #strike[(excluding me)], there are #total-words words all up.

#word-count(total => [
  You can exclude elements by label, too.
  #[That was #total-words, excluding this sentence!] <no-wc>
], exclude: <no-wc>)
```