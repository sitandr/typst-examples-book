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
```
pub fn main() {
    println!("Hello, world!");
}
```

#disable-codly()
``````