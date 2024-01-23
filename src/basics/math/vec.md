# Vectors, matrices, semicolumn syntax

## Vectors

> By vector we mean a column there. \
> To write arrow notations for letters, use `$arrow(v)$` \
> I recommend to create shortcut for this, like `#let arr = math.arrow`

To write columns, use `vec` command:

```typ
$
vec(a, b, c) + vec(1, 2, 3) = vec(a + 1, b + 2, c + 3)
$
```

### Delimiter
You can change parentheses around the column or even remove them:

```typ
$
vec(1, 2, 3, delim: "{") \
vec(1, 2, 3, delim: "||") \
vec(1, 2, 3, delim: #none)
$
```

### Gap

You can change the size of gap between rows:

```typ
$
vec(a, b, c)
vec(a, b, c, gap:#0em)
vec(a, b, c, gap:#1em)
$
```

### Making gap even

You can easily note that the gap isn't necessarily even or the same in different vectors:

```typ
$
vec(a/b, a/b, a/b) = vec(1, 1, 1)
$
```
That happens because `gap` refers to _spacing between_ elements, not the distance between their centers.

To fix this, you can use [this snippet](../../snippets/math/vecs.md).

## Matrix

> See [official reference](https://typst.app/docs/reference/math/mat/)

Matrix is very similar to `vec`, but accepts rows, separated by `;`:

```typ
$
mat(
    1, 2, ..., 10;
    2, 2, ..., 10;
    dots.v, dots.v, dots.down, dots.v;
    10, 10, ..., 10; // `;` in the end is optional
)
$
```

### Delimiters and gaps

You can specify them the same way as for vectors.

<div class="warning">
    Specify the arguments either before the content, or <strong>after the semicolon</strong>. The code will panic if there is no semicolon!
</div>

```typ
$
mat(
    delim: "|",
    1, 2, ..., 10;
    2, 2, ..., 10;
    dots.v, dots.v, dots.down, dots.v;
    10, 10, ..., 10;
    gap: #0.3em
)
$
```

## Semicolon syntax

When you use semicolons, the arguments _between the semicolons_ are merged into arrays. See yourself:

```typ
#let fun(..args) = {
    args.pos()
}

$
fun(1, 2;3, 4; 6, ; 8)
$
```

If you miss some of elements, they will be replaced by `none`-s.

You can mix semicolon syntax and named arguments, but be careful!

```typ
#let fun(..args) = {
    repr(args.pos())
    repr(args.named())
}

$
fun(1, 2; gap: #3em, 4)
$
```

For example, this will not work:

```typ-norender
$
//         ↓ there is no `;`, so it tries to add (gap:) to array
mat(1, 2; 4, gap: #3em)
$
```
