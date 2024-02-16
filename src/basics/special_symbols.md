# Special symbols

> _Important:_ I'm not great with special symbols, so I would additionally appreciate additions and corrections.

Typst has a great support of _unicode_. That also means it supports _special symbols_. They may be very useful for typesetting.

In most cases, you shouldn't use these symbols directly often. If possible, use them with show rules (for example, replace all `-th` with `\u{2011}th`, a non-breaking hyphen).

## Non-breaking symbols

Non-breaking symbols can make sure the word/phrase will not be separated. Typst will try to put them as a whole.

### Non-breaking space

> _Important:_ As it is spacing symbols, copy-pasting it will not help.
> Typst will see it as just a usual spacing symbol you used for your source code to look nicer in your editor. Again, it will interpret it _as a basic space_.

This is a symbol you should't use often (use Typst boxes instead), but it is a good demonstration of how non-breaking symbol work:

```typ
#set page(width: 9em)

// Cruel and world are separated.
// Imagine this is a phrase that can't be split, what to do then?
Hello cruel world

// Let's connect them with a special space!

// No usual spacing is allowed, so either use semicolumn...
Hello cruel#sym.space.nobreak;world

// ...parentheses...
Hello cruel#(sym.space.nobreak)world

// ...or unicode code
Hello cruel\u{00a0}world

// Well, to achieve the same effect I recommend using box:
Hello #box[cruel world]
```

### Non-breaking hyphen

```typ
#set page(width: 8em)

This is an $i$-th element.

This is an $i$\u{2011}th element.

// the best way would be
#show "-th": "\u{2011}th"

This is an $i$-th element.
```

## Connectors and separators

### World joiner

Initially, world joiner indicates that no line break should occur at this position. It is also a zero-width symbol (invisible), so it can be used as a space removing thing:

```typ
#set page(width: 9em)
#set text(hyphenate: true)

Thisisawordthathastobreak

// Be careful, there is no line break at all now!
Thisi#sym.wj;sawordthathastobreak

// code from `physica` package
// word joiner here is used to avoid extra spacing
#let just-hbar = move(dy: -0.08em, strike(offset: -0.55em, extent: -0.05em, sym.planck))
#let hbar = (sym.wj, just-hbar, sym.wj).join()

$ a #just-hbar b, a hbar b$
```

### Zero width space

Similar to word-joiner, but this is a _space_. It doesn't prevent word break. On the contrary, it breaks it without any hyphen at all!

```typ
#set page(width: 9em)
#set text(hyphenate: true)

// There is a space inside!
Thisisa#sym.zws;word

// Be careful, there is no hyphen at all now!
Thisisawo#sym.zws;rdthathastobreak
```