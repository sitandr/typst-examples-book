# Misc

# Formatting strings

## `oxifmt`, general purpose string formatter

```typ
#import "@preview/oxifmt:0.2.0": strfmt
#strfmt("I'm {}. I have {num} cars. I'm {0}. {} is {{cool}}.", "John", "Carl", num: 10) \
#strfmt("{0:?}, {test:+012e}, {1:-<#8x}", "hi", -74, test: 569.4) \
#strfmt("{:_>+11.5}", 59.4) \
#strfmt("Dict: {:!<10?}", (a: 5))
```

```typ
#import "@preview/oxifmt:0.2.0": strfmt
#strfmt("First: {}, Second: {}, Fourth: {3}, Banana: {banana} (brackets: {{escaped}})", 1, 2.1, 3, label("four"), banana: "Banana!!")\
#strfmt("The value is: {:?} | Also the label is {:?}", "something", label("label"))\
#strfmt("Values: {:?}, {1:?}, {stuff:?}", (test: 500), ("a", 5.1), stuff: [a])\
#strfmt("Left5 {:_<5}, Right6 {:*>6}, Center10 {centered: ^10?}, Left3 {tleft:_<3}", "xx", 539, tleft: "okay", centered: [a])\
```

```typ
#import "@preview/oxifmt:0.2.0": strfmt
#repr(strfmt("Left-padded7 numbers: {:07} {:07} {:07} {3:07}", 123, -344, 44224059, 45.32))\
#strfmt("Some numbers: {:+} {:+08}; With fill and align: {:_<+8}; Negative (no-op): {neg:+}", 123, 456, 4444, neg: -435)\
#strfmt("Bases (10, 2, 8, 16(l), 16(U):) {0} {0:b} {0:o} {0:x} {0:X} | W/ prefixes and modifiers: {0:#b} {0:+#09o} {0:_>+#9X}", 124)\
#strfmt("{0:.8} {0:.2$} {0:.potato$}", 1.234, 0, 2, potato: 5)\
#strfmt("{0:e} {0:E} {0:+.9e} | {1:e} | {2:.4E}", 124.2312, 50, -0.02)\
#strfmt("{0} {0:.6} {0:.5e}", 1.432, fmt-decimal-separator: ",")
```

## `name-it`, integer to text
```typ
#import "@preview/name-it:0.1.0": name-it

- #name-it(2418345)
```

## `nth`, Nth element
```typ
#import "@preview/nth:0.2.0": nth
#nth(3), #nth(5), #nth(2421)
```