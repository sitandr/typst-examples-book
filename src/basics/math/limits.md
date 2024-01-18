# Setting limits

Sometimes we want to change how the default attaching should work. 

## Limits
For example, in many countries it is common to write definite integrals with limits below and above.
To set this, use `limits` function:

```typ
$
integral_a^b\
limits(integral)_a^b
$
```

You can set this by default using `show` rule:

```typ
#show math.integral: math.limits

$
integral_a^b
$

This is inline equation: $integral_a^b$
```

## Only display mode

Notice that this will also affect inline equations. To enable limits for display math only, use `limits(inline: false)`:

```typ
#show math.integral: math.limits.with(inline: false)

$
integral_a^b
$

This is inline equation: $integral_a^b$.
```

Of course, it is possible to move them back as bottom attachments:

```typ
$
sum_a^b, scripts(sum)_a^b
$
```


## Operations

The same scheme works for operations. By default, they are attached to the bottom and top:

```typ
$a =_"By lemme 1" b, a scripts(=)_+ b$
```
