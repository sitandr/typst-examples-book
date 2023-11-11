# Types, part II

In Typst, most of things are **immutable**. You can't change content, you can just create new using this one (for example, using addition).

Immutability is very important for Typst since it tries to be _as pure language as possible_. Functions do nothing outside of returning some value.

However, purity is partly "broken" by these types. They are *super-useful* and not adding them would make Typst much pain.

However, using them adds complexity.

## Arrays (`array`)

> [Link to Reference](https://typst.app/docs/reference/foundations/array/).

Mutable object that stores data with their indices.

### Working with indices
```typ
#let values = (1, 7, 4, -3, 2)

// take value at index 0
#values.at(0) \
// set value at 0 to 3
#(values.at(0) = 3)
// negative index => start from the back
#values.at(-1) \
// add index of something that is even
#values.find(calc.even)
```

### Iterating methods
```typ
#let values = (1, 7, 4, -3, 2)

// leave only what is odd
#values.filter(calc.odd) \
// create new list of absolute values of list values
#values.map(calc.abs) \
// reverse
#values.rev() \
// convert array of arrays to flat array
#(1, (2, 3)).flatten() \
// join array of string to string
#(("A", "B", "C")
    .join(", ", last: " and "))
```

### List operations

```typ
// sum of lists:
#((1, 2, 3) + (4, 5, 6))

// list product:
#((1, 2, 3) * 4)
```

### Empty list

```typ
#() \ // this is an empty list
#(1,)\  // this is a list with one element
BAD: #(1) // this is just an element, not a list!
```

## Dictionaries (`dict`)

> [Link to Reference](https://typst.app/docs/reference/foundations/dictionary/).

Dictionaries are objects that store a string "key" and a value, associated with that key.

```typ
#let dict = (
  name: "Typst",
  born: 2019,
)

#dict.name \
#(dict.launch = 20)
#dict.len() \
#dict.keys() \
#dict.values() \
#dict.at("born") \
#dict.insert("city", "Berlin ")
#("name" in dict)
```

### Empty dictionary

```typ
This is an empty list: #() \
This is an empty dict: #(:)
```