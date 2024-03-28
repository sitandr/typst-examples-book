# Tables and grids

While tables are not that necessary to know if you don't plan to use them in your documents, grids may be very useful for _document layout_. We will use both of them them in the book later.

Let's not bother with copying examples from official documentation. Just make sure to skim through it, okay?

Most 


== Basic snippets



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