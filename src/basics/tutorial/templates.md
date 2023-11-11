# Templates
## Templates
If you want to reuse styling in other files, you can use the _template_ idiom.
Because `set` and `show` rules are only active in their current scope, they
will not affect content in a file you imported your file into. But functions
can circumvent this in a predictable way:
```typ-norender
// define a function that:
// - takes content
// - applies styling to it
// - returns the styled content
#let apply-template(body) = [
  #show heading.where(level: 1): emph
  #set heading(numbering: "1.1")
  // ...
  #body
]
```

This is equivalent to:
```typ-norender
// we can reduce the number of hashes needed here by using scripting mode
// same as above but we exchanged `[...]` for `{...}` to switch from markup
// into scripting mode
#let apply-template(body) = {
  show heading.where(level: 1): emph
  set heading(numbering: "1.1")
  // ...
  body
}
```

Then in your main file:
```typ-norender
#import "template.typ": apply-template
#show: apply-template
```

_This will apply a "template" function to the rest of your document!_

### Passing arguments
```typ-norender
// add optional named arguments
#let apply-template(body, name: "My document") = {
  show heading.where(level: 1): emph
  set heading(numbering: "1.1")

  align(center, text(name, size: 2em))

  body
}
```

Then, in template file:
```typ-norender
#import "template.typ": apply-template

// `func.with(..)` applies the arguments to the function and returns the new
// function with those defaults applied
#show: apply-template.with(name: "Report")

// it is functionally the same as this
#let new-template(..args) = apply-template(name: "Report", ..args)
#show: new-template
```

Writing templates is fairly easy if you understand [scripting](../scripting/index.md).

See more information about writing templates in [Official Tutorial](https://typst.app/docs/tutorial/making-a-template/).
