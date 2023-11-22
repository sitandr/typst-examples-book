# Logos & Figures
Using SVG-s images is totally fine. Totally. But if you are lazy and don't want to search for images, here are some logos you can just copy-paste in your document.

**Important**: _Typst in text doesn't need a special writing (unlike LaTeX)_. Just write "Typst", maybe "**Typst**", and it is okay.

## TeX and LaTeX
```typ

#let TeX = {
  set text(font: "New Computer Modern", weight: "regular")
  box(width: 1.7em, {
    [T]
    place(top, dx: 0.56em, dy: 0.22em)[E]
    place(top, dx: 1.1em)[X]
  })
}

#let LaTeX = {
  set text(font: "New Computer Modern", weight: "regular")
  box(width: 2.55em, {
    [L]
    place(top, dx: 0.3em, text(size: 0.7em)[A])
    place(top, dx: 0.7em)[#TeX]
  })
}

Typst is not that hard to learn when you know #TeX and #LaTeX.
```

## Typst guy

<!--TODO: Make scrollable-->
```typ
#import "@preview/cetz:0.1.2": *

#set page(width: auto, height: auto)

#canvas(length: 1pt, {
  import draw: *
  let color = rgb("239DAD")
  scale((y: -1))
  set-style(fill: color, stroke: none,)

  // body
  merge-path({
    bezier(
      (112.847, 134.007),
      (114.835, 143.178),
      (112.847, 138.562),
      (113.509, 141.619),
      name: "b"
    )
    bezier(
      "b.end",
      (122.063, 145.515),
      (116.16, 144.736),
      (118.569, 145.515),
      name: "b"
    )
    bezier(
      "b.end",
      (135.977, 140.121),
      (125.677, 145.515),
      (130.315, 143.717)
    )
    bezier(
      (139.591, 146.055),
      (113.389, 159.182),
      (128.99, 154.806),
      (120.256, 159.182),
      name: "b"
    )
    bezier(
      "b.end",
      (97.1258, 154.327),
      (106.522, 159.182),
      (101.101, 157.563),
      name: "b"
    )
    bezier(
      "b.end",
      (91.1626, 136.704),
      (93.1503, 150.97),
      (91.1626, 145.096),
      name: "b"
    )
    line(
      (rel: (0, -47.1126), to: "b.end"),
      (rel: (-9.0352, 0)),
      (80.6818, 82.9381),
      (91.1626, 79.7013),
      (rel: (0, -8.8112)),
      (112.847, 61),
      (rel: (0, 19.7802)),
      (134.17, 79.1618),
      (132.182, 90.8501),
      (112.847, 90.1309)
    )
  })

  // left pupil
  merge-path({
    bezier(
      (70.4667, 65.6833),
      (71.9727, 70.5068),
      (71.4946, 66.9075),
      (71.899, 69.4091)
    )
    bezier(
      (71.9727, 70.5068),
      (75.9104, 64.5912),
      (72.9675, 69.6715),
      (75.1477, 67.319)
    )
    bezier(
      (75.9104, 64.5912),
      (72.0556, 60.0005),
      (76.8638, 61.1815),
      (74.4045, 59.7677)
    )
    bezier(
      (72.0556, 60.0005),
      (66.833, 64.3859),
      (70.1766, 60.1867),
      (67.7909, 63.0017)
    )
    bezier(
      (66.833, 64.3859),
      (70.4667, 65.6833),
      (67.6159, 64.3083),
      (69.4388, 64.4591)
    )
  })

  // right pupil
  merge-path({
    bezier(
      (132.37, 61.668),
      (133.948, 66.7212),
      (133.447, 62.9505),
      (133.87, 65.5712)
    )
    bezier(
      (133.948, 66.7212),
      (138.073, 60.5239),
      (134.99, 65.8461),
      (137.274, 63.3815)
    )
    bezier(
      (138.073, 60.5239),
      (134.034, 55.7145),
      (139.066, 56.9513),
      (136.495, 55.4706)
    )
    bezier(
      (134.034, 55.7145),
      (128.563, 60.3087),
      (132.066, 55.9066),
      (129.567, 58.8586),
    )
    bezier(
      (128.563, 60.3087),
      (132.37, 61.668),
      (129.383, 60.2274),
      (131.293, 60.3855),
    )
  })

  set-style(
    stroke: (paint: rgb("239DAD"), thickness: 6pt, cap: "round"),
    fill: none,
  )

  // left eye
  merge-path({
    bezier(
      (58.5, 64.7273),
      (73.6136, 52),
      (58.5, 58.3636),
      (64.0682, 52.7955),
      name: "b"
    )
    bezier(
      "b.end",
      (84.75, 64.7273),
      (81.5682, 52),
      (84.75, 57.5682),
      name: "b"
    )
    bezier(
      "b.end",
      (71.2273, 76.6591),
      (84.75, 71.8864),
      (79.1818, 76.6591),
      name: "b"
    )
    bezier(
      "b.end",
      (58.5, 64.7273),
      (63.2727, 76.6591),
      (58.5, 71.0909)
    )
  })
  // eye lash
  line(
    (62.5, 55),
    (59.5, 52),
  )

  merge-path({
    bezier(
      (146.5, 61.043),
      (136.234, 49),
      (146.5, 52.7634),
      (141.367, 49)
    )
    bezier(
      (136.234, 49),
      (121.569, 62.5484),
      (125.969, 49),
      (120.836, 54.2688)
    )
    bezier(
      (121.569, 62.5484),
      (134.034, 72.3333),
      (122.302, 70.8279),
      (128.168, 72.3333)
    )
    bezier(
      (134.034, 72.3333),
      (146.5, 61.043),
      (139.901, 72.3333),
      (146.5, 69.3225)
    )
  })

  set-style(stroke: (thickness: 4pt))

  // right arm
  merge-path({
    bezier(
      (109.523, 115.614),
      (127.679, 110.918),
      (115.413, 115.3675),
      (122.283, 113.112)
    )
    bezier(
      (127.679, 110.918),
      (137, 106.591),
      (130.378, 109.821),
      (132.708, 108.739)
    )
  })

  // right first finger
  bezier(
    (137, 106.591),
    (140.5, 98.0908),
    (137.385, 102.891),
    (138.562, 99.817)
  )

  // right second finger
  bezier(
    (137, 106.591),
    (146, 101.591),
    (139.21, 103.799),
    (142.425, 101.713)
  )

  // right third finger
  line(
    (137, 106.591),
    (148, 106.591)
  )

  //right forth finger
  bezier(
    (137, 106.591),
    (146, 111.091),
    (140.243, 109.552),
    (143.119, 110.812)
  )

  // left arm
  bezier(
    (95.365, 116.979),
    (73.5, 107.591),
    (88.691, 115.549),
    (80.587, 112.887)
  )

  // left first finger
  line(
    (73.5, 107.591),
    (rel: (0, -9.5))
  )
  // left second finger
  line(
    (73.5, 107.591),
    (65.396, 100.824)
  )
  // left third finger
  line(
    (73.5, 107.591),
    (63.012, 105.839)
  )
  // left fourth finger
  bezier(
    (73.5, 107.591),
    (63.012, 111.04),
    (70.783, 109.121),
    (67.214, 111.255)
  )
})
```

