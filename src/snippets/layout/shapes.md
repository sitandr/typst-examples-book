# Shaped boxes with text

(I guess that will make a package eventually, but let it be a snippet for now)

```typ
/// author: JustForFun88
#import "@preview/oxifmt:0.2.1": strfmt

#let shadow_svg_path = `
<svg
    width="{canvas-width}"
    height="{canvas-height}"
    viewBox="{viewbox}"
    version="1.1"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:svg="http://www.w3.org/2000/svg">
    <!-- Definitions for reusable components -->
    <defs>
        <filter id="shadowing" >
            <feGaussianBlur in="SourceGraphic" stdDeviation="{blur}" />
        </filter>
    </defs>

    <!-- Drawing the rectangle with a fill and feGaussianBlur effect -->
    <path
        style="fill: {flood-color}; opacity: {flood-opacity}; filter:url(#shadowing)"
        d="{vertices} Z" />
</svg>
`.text

#let parallelogram(width: 20mm, height: 5mm, angle: 30deg) = {
	let δ = height * calc.tan(angle)
	(
    (      + δ,     0pt   ),
    (width + δ * 2, 0pt   ),
    (width + δ,     height),
    (0pt,           height),
	)
}

#let hexagon(width: 100pt, height: 30pt, angle: 30deg) = {
  let dy = height / 2;
	let δ = dy * calc.tan(angle)
	(
    (0pt,           dy    ),
    (      + δ,     0pt   ),
    (width + δ,     0pt   ),
    (width + δ * 2, dy    ),
    (width + δ,     height),
    (      + δ,     height),
	)
}

#let shape_size(vertices) = {
    let x_vertices = vertices.map(array.first);
    let y_vertices = vertices.map(array.last);

    (
      calc.max(..x_vertices) - calc.min(..x_vertices),
      calc.max(..y_vertices) - calc.min(..y_vertices)
    )
}

#let shadowed_shape(shape: hexagon, fill: none,
  stroke: auto, angle: 30deg, shadow_fill: black, alpha: 0.5, 
  blur: 1.5, blur_margin: 5, dx: 0pt, dy: 0pt, ..args, content
) = layout(size => context {
    let named = args.named()
    for key in ("width", "height") {
      if key in named and type(named.at(key)) == ratio {
        named.insert(key, size.at(key) * named.at(key))
      }
    }

    let opts = (blur: blur, flood-color: shadow_fill.to-hex())
       
    let content = box(content, ..named)
    let size = measure(content)

    let vertices = shape(..size, angle: angle)
    let (shape_width, shape_height) = shape_size(vertices)
    let margin = opts.blur * blur_margin * 1pt

    opts += (
      canvas-width:  shape_width  + margin,
      canvas-height: shape_height + margin,
      flood-opacity: alpha
    )

    opts.viewbox = (0, 0, opts.canvas-width.pt(), opts.canvas-height.pt()).map(str).join(",")

    opts.vertices = "";
    let d = margin / 2;
    for (i, p) in vertices.enumerate() {
        let prefix = if i == 0 { "M " } else { " L " };
        opts.vertices += prefix + p.map(x => str((x + d).pt())).join(", ");
    }

    let svg-shadow = image(strfmt(shadow_svg_path, ..opts))
    place(dx: dx, dy: dy, svg-shadow)
    place(path(..vertices, fill: fill, stroke: stroke, closed: true))
    box(h((shape_width - size.width) / 2) + content, width: shape_width)
})

#set text(3em);

#shadowed_shape(shape: hexagon,
    inset: 1em, fill: teal,
    stroke: 1.5pt + teal.darken(50%),
    shadow_fill: red,
    dx: 0.5em, dy: 0.35em, blur: 3)[Hello there!]
#shadowed_shape(shape: parallelogram,
    inset: 1em, fill: teal,
    stroke: 1.5pt + teal.darken(50%),
    shadow_fill: red,
    dx: 0.5em, dy: 0.35em, blur: 3)[Hello there!]

```