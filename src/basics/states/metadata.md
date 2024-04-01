# Metadata

Metadata is invisible content that can be extracted using query or other content.
This may be very useful with `typst query` to pass values to external tools.

```typ
// Put metadata somewhere.
#metadata("This is a note") <note>

// And find it from anywhere else.
#context {
  query(<note>).first().value
}
```