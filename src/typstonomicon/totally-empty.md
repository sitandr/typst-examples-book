# Empty pages without numbering

## Empty pages before chapters starting at odd pages

`````typ
// author: janekfleper

#set page(height: 20em)

#let find-labels(name) = {
  return query(name).map(label => label.location().page())
}

#let page-header = context {
  let empty-pages = find-labels(<empty-page>)
  let new-chapters = find-labels(<new-chapter>)
  if new-chapters.len() > 0 {
    if new-chapters.contains(here().page()) [
      _a new chapter starts on this page_
      #return
    ]

    // get the index of the next <new-chapter> label
    let new-chapter-index = new-chapters.position(page => page > here().page())
    if new-chapter-index != none {
      let empty-page = empty-pages.at(new-chapter-index)
      if empty-page < here().page() [
        _this is an empty page to make the next chapter start on an odd page_
        #return
      ]
    }
  }

  [and this would be a regular header]
  line(length: 100%)
}

#let page-footer = context {
  // since the page breaks in chapter-heading() are inserted after the <empty-page> label,
  // the selector has to look "before" the current page to find the relevant label
  let empty-page-labels = query(selector(<empty-page>).before(here()))
  if empty-page-labels.len() > 0 {
    let empty-page = empty-page-labels.last().location().page()
    // look back at the most recent <new-chapter> label
    let new-chapter = query(selector(<new-chapter>).before(here())).last().location().page()
    // check that there is no <new-chapter> label on the current page
    if (new-chapter != here().page()) and (empty-page + 1 == here().page()) [
      _this is an empty page where the page number should be omitted_
      #return
    ]
  }

  let page-display = counter(page).display(here().page-numbering())
  h(1fr) + page-display + h(1fr)
}

#show heading.where(level: 1): it => [
  #[] <empty-page>
  #pagebreak(to: "even", weak: true)
  #[] <new-chapter>
  #pagebreak(to: "odd", weak: true)
  #it.body
  #v(2em)
]


#show outline.entry.where(level: 1): it => {
  // reverse the results of the label queries to find the last <empty-page> label for the targeted page
  // the method array.position() will always return the first one...
  let empty-pages = find-labels(<empty-page>).rev()
  let new-chapters = query(<new-chapter>).rev()
  let empty-page-index = empty-pages.position(page => page == int(it.page.text))
  let new-chapter = new-chapters.at(empty-page-index)
  link(new-chapter.location())[#it.body #box(width: 1fr)[#it.fill] #new-chapter.location().page()]
}

#set page(header: page-header, footer: page-footer, numbering: "1")

#outline()

= The explanation

```
These queries reveal where the corresponding tags are found. The actual empty page is always at the location of the label <empty-page> + 1. If an empty page is actually inserted by the pagebreaks, the two labels will cover the page of the heading and one page before that. If no empty page was inserted, both labels will point to the same page which is not an issue either. And even then we can check for the <new-chapter> label first to give it a higher priority.

The first <empty-page> label is always on page 1 and can just be ignored since it points to the (non-existing) empty page before the first chapter.

pages with the label <empty-page>: #context find-labels(<empty-page>)
pages with the label <new-chapter>: #context find-labels(<new-chapter>)
```

= A heading
#lorem(190)

= Another heading
#lorem(100)

= The last heading
#lorem(400)
`````