# Code

## `codly`

> See docs [there](https://github.com/Dherse/codly)

``````typ
#import "@preview/codly:0.1.0": codly-init, codly, disable-codly
#show: codly-init.with()

#codly(languages: (
        typst: (name: "Typst", color: rgb("#41A241"), icon: none),
    ),
    breakable: false
)

```typst
#import "@preview/codly:0.1.0": codly-init
#show: codly-init.with()
```

// Still formatted!
```rust
pub fn main() {
    println!("Hello, world!");
}
```

#disable-codly()
``````

## Codelst

``````typ
#import "@preview/codelst:2.0.0": sourcecode

#sourcecode[```typ
#show "ArtosFlow": name => box[
  #box(image(
    "logo.svg",
    height: 0.7em,
  ))
  #name
]

This report is embedded in the
ArtosFlow project. ArtosFlow is a
project of the Artos Institute.
```]
``````