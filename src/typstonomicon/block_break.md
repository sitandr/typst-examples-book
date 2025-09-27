# Breakpoints on broken blocks

### Implementation with table headers & footers

See a demo project (more comments, I stripped some of them) [there](https://typst.app/project/r-yQHF952iFnPme9BWbRu3).

```typ
/// author: isuffix

// Underlying counter and zig-zag functions
#let counter-family(id) = {
  let parent = counter(id)
  let parent-step() = parent.step()
  let get-child() = counter(id + str(parent.get().at(0)))
  return (parent-step, get-child)
}

// A fun zig-zag line!
#let zig-zag(fill: black, rough-width: 6pt, height: 4pt, thick: 1pt, angle: 0deg) = {
  layout((size) => {
    // Use layout to get the size and measure our horizontal distance
    // Then get the per-zigzag width with some maths.
    let count = int(calc.round(size.width / rough-width))
    // Need to add extra thickness since we join with `h(-thick)`
    let width = thick + (size.width - thick) / count
    // One zig and one zag:
    let zig-and-zag = {
      let line-stroke = stroke(thickness: thick, cap: "round", paint: fill)
      let top-left = (thick/2, thick/2)
      let bottom-mid = (width/2, height - thick/2)
      let top-right = (width - thick/2, thick/2)
      let zig = line(stroke: line-stroke, start: top-left, end: bottom-mid)
      let zag = line(stroke: line-stroke, start: bottom-mid, end: top-right)
      box(place(zig) + place(zag), width: width, height: height, clip: true)
    }
    let zig-zags = ((zig-and-zag,) * count).join(h(-thick))
    rotate(zig-zags, angle)
  })
}

// ---- Define split-box ---- //

// Customizable options for a split-box border:
#let default-border = (
  // The starting and ending lines
  above: line(length: 100%),
  below: line(length: 100%),
  // Lines to put between the box over multiple pages
  btwn-above: line(length: 100%, stroke: (dash:"dotted")),
  btwn-below: line(length: 100%, stroke: (dash:"dotted")),
  // Left/right lines
  // These *must* use `grid.vline()`, otherwise you will get an error.
  // To remove the lines, set them to: `grid.vline(stroke: none)`.
  // You could probably configure this better with a rowspan, but I'm lazy.
  left: grid.vline(),
  right: grid.vline(),
)

// Create a box for content which spans multiple pages/columns and
// has custom borders above and below the column-break.
#let split-box(
  // Set the border dictionary, see `default-border` above for options
  border: default-border,
  // The cell to place content in, this should resolve to a `grid.cell`
  cell: grid.cell.with(inset: 5pt),
  // The last positional arg or args are your actual content
  // Any extra named args will be sent to the underlying grid when called
  // This is useful for fill, align, etc.
  ..args
) = {
  // See `utils.typ` for more info.
  let (parent-step, get-child) = counter-family("split-box-unique-counter-string")
  parent-step() // Place the parent counter once.
  // Keep track of each time the header is placed on a page.
  // Then check if we're at the first placement (for header) or the last (footer)
  // If not, we'll use the 'between' forms of the  border lines.
  let border-above = context {
    let header-count = get-child()
    header-count.step()
    context if header-count.get() == (1,) { border.above } else { border.btwn-above }
  }
  let border-below = context {
    let header-count = get-child()
    if header-count.get() == header-count.final() { border.below } else { border.btwn-below }
  }
  // Place the grid!
  grid(
    ..args.named(),
    columns: 3,
    border.left,
    grid.header(border-above , repeat: true),
    ..args.pos().map(cell),
    grid.footer(border-below, repeat: true),
    border.right,
  )
}

// ---- Examples ---- //

#set page(width: 7.2in, height: 3in, columns: 6)

// Tada!
#split-box[
  #lorem(20)
]

// And here's a fun example:

#let fun-border = (
  // gradients!
  above: line(length: 100%, stroke: 2pt + gradient.linear(..color.map.rainbow)),
  below: line(length: 100%, stroke: 2pt + gradient.linear(..color.map.rainbow, angle: 180deg)),
  // zig-zags!
  btwn-above: move(dy: +2pt, zig-zag(fill: blue, angle: 3deg)),
  btwn-below: move(dy: -2pt, zig-zag(fill: orange, angle: 177deg)),
  left: grid.vline(stroke: (cap: "round", paint: purple)),
  right: grid.vline(stroke: (cap: "round", paint: purple)),
)

#split-box(border: fun-border)[
  #lorem(25)
]

// And some more tame friends:

#split-box(border: (
  above: move(dy: -0.5pt, line(length: 100%)),
  below: move(dy: +0.5pt, line(length: 100%)),
  // zig-zags!
  btwn-above: move(dy: -1.1pt, zig-zag()),
  btwn-below: move(dy: +1.1pt, zig-zag(angle: 180deg)),
  left: grid.vline(stroke: (cap: "round")),
  right: grid.vline(stroke: (cap: "round")),
))[
  #lorem(10)
]

#split-box(
  border: (
    above: line(length: 100%, stroke: luma(50%)),
    below: line(length: 100%, stroke: luma(50%)),
    btwn-above: line(length: 100%, stroke: (dash: "dashed", paint: luma(50%))),
    btwn-below: line(length: 100%, stroke: (dash: "dashed", paint: luma(50%))),
    left: grid.vline(stroke: none),
    right: grid.vline(stroke: none),
  ),
  cell: grid.cell.with(inset: 5pt, fill: color.yellow.saturate(-85%))
)[
  #lorem(20)
]

```

### Implementation via headers, footers and stated

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

  let startMarkers = query(startSelector)
  let endMarkers = query(endSelector)
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
  header: context {
    let boundaryCount = countBoundaries(here(), true)

    if boundaryCount.end > boundaryCount.start {
      // Decorate this header with an opening decoration
      [Block break top: $-->$]
    }
  },
  footer: context {
    let boundaryCount = countBoundaries(here(), false)

    if boundaryCount.start > boundaryCount.end {
      // Decorate this footer with a closing decoration
      [Block break end: $<--$]
    }
  }
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
