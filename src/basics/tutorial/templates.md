# Templates

## Templates

If you want to reuse code for other files, create a _template_.

In template file:

```typ-norender
// note: that is a "naive" notation,
// see good below
#let apply-template(body) = [
    #show-rule 1
    #show-rule 2
    #set-rule 1
    ...
    #body
]
```

This is equivalent to:

```typ-norender
// we can replace square brackets there with braces,
// see "scripting" section
#let apply-template(body) = {
    show-rule 1
    show-rule 2
    set-rule 1
    ...
    body
}
```

Then in target file:

```typ-norender
#import .../your-template-name.typ: 
#show: apply-template
```

_This will apply "template" function to all your document!_

### Passing arguments

```typ-norender
// add custom arguments
#let apply-template(body, name: "My document") = {
  show-rule 1
  set-rule 1

  align(center, text(name, size: 2em))

  body
}
```

Then, in template file:

```typ-norender
#import .../your-template-name.typ: 
#show: apply-template.with(name: "Report")
```


Writing templates is fairly easy if you understand [scripting](../scripting/README.md).

See more information about writing templates in [Official Tutorial](https://typst.app/docs/tutorial/making-a-template/).
