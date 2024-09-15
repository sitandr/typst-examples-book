## Multiple show rules

Sometimes there is a need to apply several rules that look very similar. Or generate them from code. One of the ways to deal with this, the most cursed one, is this:

```typ
#let rules = (math.sum, math.product, math.root)

#let apply-rules(rules, it) = {
  if rules.len() == 0 {
    return it
  }
  show rules.pop(): math.display
  apply-rules(rules, it)
}

$product/sum root(3, x)/2$

#show: apply-rules.with(rules)

$product/sum root(3, x)/2$
```

The recursion problem may be avoided with the power of `fold`, with basically the same idea:

```typ
// author: Eric
#let kind_supp = (code: "Listing", algo: "Algorithme")
#show: it => kind_supp.pairs().fold(it, (acc, (kind, supp)) => {
  show figure.where(kind: kind): set figure(supplement: supp)
  acc
})
```

Note that just in case of symbols (if you don't need element functions), one can use regular expressions. That is a more robust way:

```typ
#show regex("[" + math.product + math.sum + "]"): math.display

$product/sum root(3, x)/2$
```