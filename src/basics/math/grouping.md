# Grouping

Every grouping can be (currently) done by parenthesis.
So the parenthesis may be both "real" parenthesis and grouping ones.

For example, these parentheses specify nominator of the fraction:

```typ
$ (a^2 + b^2)/2 $
```

## Left-right
> See [official documentation](https://typst.app/docs/reference/math/lr).

If there are two matching braces of any kind, they will be wrapped as `lr` (left-right) group.

```typ
$
{[((a + b)/2) + 1]_0}
$
```

You can disable it by escaping.

You can also match braces of any kind by using `lr` directly:

```typ
$
lr([a/2, b)) \
lr([a/2, b), size: #150%)
$
```

## Fences

Fences _are not matched automatically_ because of large amount of false-positives.

You can use `abs` or `norm` to match them:

```typ
$
abs(a + b), norm(a + b), floor(a + b), ceil(a + b), round(a + b)
$
```