# Setting limits

Sometimes we want to change how the default attaching should work. 

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

Notice that this will also affect inline equations. To enable limits for display math only, use `limits(inline: false)`:

```typ
#show math.integral: math.limits.with(inline: false)

$
integral_a^b
$

This is inline equation: $integral_a^b$.
```