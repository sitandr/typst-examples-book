# Page numbering

## Separate page numbering for each chapter

```typ
/// author: tinger

// unnumbered title page if needed
// ...

// front-matter
#set page(numbering: "I")
#counter(page).update(1)
#lorem(50)
// ...

// page counter anchor
#metadata(()) <front-matter>

// main document body
#set page(numbering: "1")
#lorem(50)
#counter(page).update(1)
// ...

// back-matter
#set page(numbering: "I")
// must take page breaks into account, may need to be offset by +1 or -1
#context counter(page).update(counter(page).at(<front-matter>).first())
#lorem(50)
// ...
```
