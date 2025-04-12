# Glossary

## glossarium

>[Link to the universe](https://typst.app/universe/package/glossarium)

Package to manage glossary and abbreviations.

<div class="info">One of the very first cool packages of Typst, made specially for (probably) the first thesis written in Typst.<div>

```typ
#import "@preview/glossarium:0.5.4": make-glossary, register-glossary, print-glossary, gls, glspl
#show: make-glossary

// for better link visibility
#show link: set text(fill: blue.darken(60%))

#let entry-list = (
    (
    // minimal term
    (key: "kuleuven", short: "KU Leuven"),

    // a term with a long form and a group
    (key: "unamur", short: "UNamur", long: "Namur University", group: "Universities"),

    // a term with a markup description
    (
      key: "oidc",
      short: "OIDC",
      long: "OpenID Connect",
      description: [OpenID is an open standard and decentralized authentication protocol promoted by the non-profit
      #link("https://en.wikipedia.org/wiki/OpenID#OpenID_Foundation")[OpenID Foundation].],
      group: "Accronyms",
    ),

    // a term with a short plural
    (
      key: "potato",
      short: "potato",
      // "plural" will be used when "short" should be pluralized
      plural: "potatoes",
      description: [#lorem(10)],
    ),

    // a term with a long plural
    (
      key: "dm",
      short: "DM",
      long: "diagonal matrix",
      // "longplural" will be used when "long" should be pluralized
      longplural: "diagonal matrices",
      description: "Probably some math stuff idk",
    ),
  )
)

#register-glossary(entry-list)

// Your document body
#print-glossary(
 entry-list
)

// referencing the OIDC term using gls
#gls("oidc")
// displaying the long form forcibly
#gls("oidc", long: true)

// referencing the OIDC term using the reference syntax
@oidc

Plural: #glspl("potato")

#gls("oidc", display: "whatever you want")
```
