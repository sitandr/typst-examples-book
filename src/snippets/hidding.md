# Hiding things

```
// author: GeorgeMuscat
#let redact(text, fill: black, height: 1em) = {
  box(rect(fill: fill, height: height)[#hide(text)])
}

Example:
  - Unredacted text
  - Redacted #redact("text")
```