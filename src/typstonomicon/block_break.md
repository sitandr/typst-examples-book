# Breakpoints on broken blocks

<div class="warning">
  Limitations: <strong>works only with one-column layout and one break</strong>.
</div>

```typ
#let countBoundaries(loc, fromHeader) = {
  let startSelector = selector(label("boundary-start"))
  let endSelector = selector(label("boundary-end"))

  if fromHeader {
    // Count down from the top of the page
    startSelector = startSelector.after(loc)
    endSelector = endSelector.after(loc)
  } else {
    // Count up from the bottom of the page
    startSelector = startSelector.before(loc)
    endSelector = endSelector.before(loc)
  }

  let startMarkers = query(startSelector, loc)
  let endMarkers = query(endSelector, loc)
  let currentPage = loc.position().page

  let pageStartMarkers = startMarkers.filter(elem =>
    elem.location().position().page == currentPage)

  let pageEndMarkers = endMarkers.filter(elem =>
    elem.location().position().page == currentPage)

  (start: pageStartMarkers.len(), end: pageEndMarkers.len())
}

#set page(
  margin: 2em,
  // ... other page setup here ...
  header: locate(loc => {
    let boundaryCount = countBoundaries(loc, true)

    if boundaryCount.end > boundaryCount.start {
      // Decorate this header with an opening decoration
      [Block break top: $-->$]
    }
  }),
  footer: locate(loc => {
    let boundaryCount = countBoundaries(loc, false)

    if boundaryCount.start > boundaryCount.end {
      // Decorate this footer with a closing decoration
      [Block break end: $<--$]
    }
  })
)

#let breakable-block(body) = block({
  [
    #metadata("boundary") <boundary-start>
  ]
  stack(
    // Breakable list content goes here
    body
  )
  [
    #metadata("boundary") <boundary-end>
  ]
})

#set page(height: 10em)

#breakable-block[
    #([Something \ ]*10)
]
```
