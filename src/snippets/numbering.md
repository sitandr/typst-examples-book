# Numbering

## "Clean" numbering
```
// original author: tromboneher

// Number sections according to a number of schemes, omitting previous leading elements.
// For example, where the numbering pattern "A.I.1." would produce:
//
// A. A part of the story
//   A.I. A chapter
//   A.II. Another chapter
//     A.II.1. A section
//       A.II.1.a. A subsection
//       A.II.1.b. Another subsection
//     A.II.2. Another section
// B. Another part of the story
//   B.I. A chapter in the second part
//   B.II. Another chapter in the second part
//
// clean_numbering("A.", "I.", "1.a.") would produce:
//
// A. A part of the story
//   I. A chapter
//   II. Another chapter
//     1. A section
//       1.a. A subsection
//       1.b. Another subsection
//     2. Another section
// B. Another part of the story
//   I. A chapter in the second part
//   II. Another chapter in the second part
//
#let clean_numbering(..schemes) = {
  (..nums) => {
    let (section, ..subsections) = nums.pos()
    let (section_scheme, ..subschemes) = schemes.pos()

    if subsections.len() == 0 {
      numbering(section_scheme, section)
    } else if subschemes.len() == 0 {
        numbering(section_scheme, ..nums.pos())
    }
    else {
      clean_numbering(..subschemes)(..subsections)
    }
  }
}

#set heading(numbering: clean_numbering("A.", "I.", "1.a."))

= Part
== Chapter
== Another chapter
=== Section
==== Subsection
==== Another subsection
= Another part of the story
== A chapter in the second part
== Another chapter in the second part
```

## Math numbering

See [there](./math/numbering.md).