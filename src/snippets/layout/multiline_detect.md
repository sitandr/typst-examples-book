# Multiline detection

Detects if figure caption (may be any other element) _has more than one line_.

If the caption is multiline, it makes it left-aligned.

<div class="warning">
 Breaks on manual linebreaks.
</div>

`````typ
#show figure.caption: it => {
  layout(size => style(styles => [
    #let text-size = measure(
      it.supplement + it.separator + it.body,
      styles,
    )

    #let my-align

    #if text-size.width < size.width {
      my-align = center
    } else {
      my-align = left
    }

    #align(my-align, it)

  ]))
}

#figure(caption: lorem(6))[
    ```rust
    pub fn main() {
        println!("Hello, world!");
    }
    ```
]

#figure(caption: lorem(20))[
    ```rust
    pub fn main() {
        println!("Hello, world!");
    }
    ```
]
`````
