# Tables and grids

While tables are not that necessary to know if you don't plan to use them in your documents, grids may be very useful for _document layout_. We will use both of them them in the book later.

Let's not bother with copying examples from official documentation. Just make sure to skim through it, okay?

== Basic snippets

=== Spreading

Spreading operators (see [there](../scripting/arguments.md)) may be especially useful for the tables:

```typ
#set text(size: 9pt)

#let yield_cells(n) = {
  for i in range(0, n + 1) {
    for j in range(0, n + 1) {
      let product = if i * j != 0 {
        // math is used for the better look 
        if j <= i { $#{ j * i }$ } 
        else {
          // upper part of the table
          text(gray.darken(50%), str(i * j))
        }
      } else {
        if i == j {
          // the top right corner 
          $times$
        } else {
          // on of them is zero, we are at top/left
          $#{i + j}$
        }
      }
      // this is an array, for loops merge them together
      // into one large array of cells
      (
        table.cell(
          fill: if i == j and j == 0 { orange } // top right corner
          else if i == j { yellow } // the diagonal
          else if i * j == 0 { blue.lighten(50%) }, // multipliers
          product,),
      )
    }
  }
}

#let n = 10
#table(
  columns: (0.6cm,) * (n + 1), rows: (0.6cm,) * (n + 1), align: center + horizon, inset: 3pt, ..yield_cells(n),
)
```

=== Splitting tables

Tables are split between pages automatically.
```typ
#set page(height: 8em)
#(
table(
  columns: 5,
  [Aligner], [publication], [Indexing], [Pairwise alignment], [Max. read length  (bp)],
  [BWA], [2009], [BWT-FM], [Semi-Global], [125],
  [Bowtie], [2009], [BWT-FM], [HD], [76],
  [CloudBurst], [2009], [Hashing], [Landau-Vishkin], [36],
  [GNUMAP], [2009], [Hashing], [NW], [36]
  )
)
```

However, if you want to make it breakable inside other element, you'll have to make that element breakable too:

```typ
#set page(height: 8em)
// Without this, the table fails to split upon several pages
#show figure: set block(breakable: true)
#figure(
table(
  columns: 5,
  [Aligner], [publication], [Indexing], [Pairwise alignment], [Max. read length  (bp)],
  [BWA], [2009], [BWT-FM], [Semi-Global], [125],
  [Bowtie], [2009], [BWT-FM], [HD], [76],
  [CloudBurst], [2009], [Hashing], [Landau-Vishkin], [36],
  [GNUMAP], [2009], [Hashing], [NW], [36]
  )
)
```