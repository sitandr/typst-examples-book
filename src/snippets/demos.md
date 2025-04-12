# Demos

## Resume (using template)

```typ
#import "@preview/modern-cv:0.8.0": *

#show: resume.with(
  author: (
    firstname: "John",
    lastname: "Smith",
    email: "js@example.com",
    homepage: "https://example.com",
    phone: "(+1) 111-111-1111",
    github: "DeveloperPaul123",
    twitter: "typstapp",
    scholar: "",
    orcid: "0000-0000-0000-000X",
    birth: "January 1, 1990",
    linkedin: "Example",
    address: "111 Example St. Example City, EX 11111",
    positions: (
      "Software Engineer",
      "Software Architect",
      "Developer",
    ),
  ),
  profile-picture: none,
  date: datetime.today().display(),
  language: "en",
  colored-headers: true,
  show-footer: false,
  paper-size: "us-letter",
)

= Experience

#resume-entry(
  title: "Senior Software Engineer",
  location: "Example City, EX",
  date: "2019 - Present",
  description: "Example, Inc.",
  title-link: "https://github.com/DeveloperPaul123",
)

#resume-item[
  - #lorem(20)
  - #lorem(15)
  - #lorem(25)
]

#resume-entry(
  title: "Software Engineer",
  location: "Example City, EX",
  date: "2011 - 2019",
  description: "Previous Company, Inc.",
)

#resume-item[
  // content doesn't have to be bullet points
  #lorem(72)
]

#resume-entry(
  title: "Intern",
  location: "Example City, EX",
)

#resume-item[
  - #lorem(20)
  - #lorem(15)
  - #lorem(25)
]

= Projects

#resume-entry(
  title: "Thread Pool C++ Library",
  location: [#github-link("DeveloperPaul123/thread-pool")],
  date: "May 2021 - Present",
  description: "Designer/Developer",
)

#resume-item[
  - Designed and implemented a thread pool library in C++ using the latest C++20 and C++23 features.
  - Wrote extensive documentation and unit tests for the library and published it on Github.
]

#resume-entry(
  title: "Event Bus C++ Library",
  location: github-link("DeveloperPaul123/eventbus"),
  date: "Sep. 2019 - Present",
  description: "Designer/Developer",
)

#resume-item[
  - Designed and implemented an event bus library using C++17.
  - Wrote detailed documentation and unit tests for the library and published it on Github.
]

= Skills

#resume-skill-item(
  "Languages",
  (strong("C++"), strong("Python"), "Java", "C#", "JavaScript", "TypeScript"),
)
#resume-skill-item("Spoken Languages", (strong("English"), "Spanish"))
#resume-skill-item(
  "Programs",
  (strong("Excel"), "Word", "Powerpoint", "Visual Studio"),
)

= Education

#resume-entry(
  title: "Example University",
  location: "Example City, EX",
  date: "August 2014 - May 2019",
  description: "B.S. in Computer Science",
)

#resume-item[
  - #lorem(20)
  - #lorem(15)
  - #lorem(25)
]
```

## Book cover
```typ
// author: bamdone
#let accent  = rgb("#00A98F")
#let accent1 = rgb("#98FFB3")
#let accent2 = rgb("#D1FF94")
#let accent3 = rgb("#D3D3D3")
#let accent4 = rgb("#ADD8E6")
#let accent5 = rgb("#FFFFCC")
#let accent6 = rgb("#F5F5DC")

#set page(paper: "a4",margin: 0.0in, fill: accent)

#set rect(stroke: 4pt)
#move(
  dx: -6cm, dy: 1.0cm,
  rotate(-45deg,
    rect(
      width: 100cm,
      height: 2cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent1,
)))

#set rect(stroke: 4pt)
#move(
  dx: -2cm, dy: -1.0cm,
  rotate(-45deg,
    rect(
      width: 100cm,
      height: 2cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent2,
)))

#set rect(stroke: 4pt)
#move(
  dx: 8cm, dy: -10cm,
  rotate(-45deg,
    rect(
      width: 100cm,
      height: 1cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent3,
)))

#set rect(stroke: 4pt)
#move(
  dx: 7cm, dy: -8cm,
  rotate(-45deg,
    rect(
      width: 1000cm,
      height: 2cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent4,
)))

#set rect(stroke: 4pt)
#move(
  dx: 0cm, dy: -0cm,
  rotate(-45deg,
    rect(
      width: 1000cm,
      height: 2cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent1,
)))

#set rect(stroke: 4pt)
#move(
  dx: 9cm, dy: -7cm,
  rotate(-45deg,
    rect(
      width: 1000cm,
      height: 1.5cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent6,
)))

#set rect(stroke: 4pt)
#move(
  dx: 16cm, dy: -13cm,
  rotate(-45deg,
    rect(
      width: 1000cm,
      height: 1cm,
      radius: 50%,
      stroke: 0pt,
      fill:accent2,
)))

#align(center)[
  #rect(width: 30%,
    fill: accent4,
    stroke:none,
    [#align(center)[
      #text(size: 60pt,[Title])
    ]
    ])
]

#align(center)[
  #rect(width: 30%,
    fill: accent4,
    stroke:none,
    [#align(center)[
      #text(size: 20pt,[author])
    ]
    ])
]
```