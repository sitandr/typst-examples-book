# Try&Catch

```typ
// author: laurmaedge
// Renders an image or a placeholder if it doesn't exist.
// Don’t try this at home, kids!
#let maybe-image(path, ..args) = locate(loc => {
  let path-label = label(path)
  let first-time = query(locate(_ => {}).func(), loc).len() == 0
  if first-time or query(path-label, loc).len() > 0 {
    [#image(path, ..args)#path-label]
  } else {
    rect(width: 50%, height: 5em, fill: luma(235), stroke: 1pt)[
      #set align(center + horizon)
      Could not find #raw(path)
    ]
  }
})

#maybe-image("../tiger.jpg")
#maybe-image("../tiger1.jpg")
```