# States & Query

<div class="warning">This section may be not very complete and fully updated for last Typst versions. Any contribution is very welcome!.</div>

Typst tries to be a _pure language_ as much as possible.

That means, a function can't change anything outside of it. That also means, if you call function, the result should be always the same.

Unfortunately, our world (and therefore our documents) isn't pure.
If you create a heading №2, you want the next number to be three.

That section will guide you to using impure Typst. Don't overuse it, as this knowledge comes close to the Dark Arts of Typst!
