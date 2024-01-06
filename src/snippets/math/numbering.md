# Numbering
## Number by current heading

> See also built-in numbering in [math package section](../../packages/math.md#theorems)

```typ
/// original author: indicatelove
#set heading(numbering: "1.")
#show heading.where(level:1): it => {
  counter(math.equation).update(0)
  it
}

#set math.equation(numbering: it => {
  locate(loc => {
    let count = counter(heading.where(level:1)).at(loc).last()
    numbering("(1.1)", count, it)
  })
})

= Section
== Subsection

$ 5 + 3 = 8 $
$ 5 + 3 = 8 $

= New Section
== Subsection
$ 5 + 3 = 8 $
== Subsection
$ 5 + 3 = 8 $
```

## Number only labeled equations
### Simple code
```typ
// author: shampoohere
#show math.equation:it => {
  if it.fields().keys().contains("label"){
    math.equation(block: true, numbering: "(1)", it)
    // change your numbering style in `numbering`
  } else {
    it
  }
}

$ sum_x^2 $
$ dif/(dif x)(A(t)+B(x))=dif/(dif x)A(t)+dif/(dif x)B(t) $ <ep-2>
$ sum_x^2 $
$ dif/(dif x)(A(t)+B(x))=dif/(dif x)A(t)+dif/(dif x)B(t) $ <ep-3>
```

### Make the hacked references clickable again
```typ
// author: gijsleb
#show math.equation:it => {
  if it.has("label"){
    math.equation(block:true, numbering: "(1)", it)
  } else {
    it
  }
}

#show ref: it => {
  let el = it.element
  if el != none and el.func() == math.equation {
    link(el.location(), numbering(
      "(1)",
      counter(math.equation).at(el.location()).at(0) + 1
    ))
  } else {
    it
  }
}

$ sum_x^2 $ 
$ dif/(dif x)(A(t)+B(x))=dif/(dif x)A(t)+dif/(dif x)B(t) $ <ep-2>
$ sum_x^2 $ 
$ dif/(dif x)(A(t)+B(x))=dif/(dif x)A(t)+dif/(dif x)B(t) $ <ep-3>
In @ep-2 and @ep-3 we see equations
```
