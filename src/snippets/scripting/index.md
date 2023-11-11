# Scripting

## Unflatten arrays

```
// author: PgSuper
#let unflatten(arr, n) = {
  let columns = range(0, n).map(_ => ())
  for (i, x) in arr.enumerate() {
    columns.at(calc.rem(i, n)).push(x)
  }
  array.zip(..columns)
}

#unflatten((1, 2, 3, 4, 5, 6), 2)
#unflatten((1, 2, 3, 4, 5, 6), 3)
```

## Create an abbreviation

```
#let full-name = "Federal University of Ceará"

#let letts = {
  full-name
    .split()
    .map(word => word.at(0)) // filter only capital letters
    .filter(l => upper(l) == l)
    .join()
}
#letts
```