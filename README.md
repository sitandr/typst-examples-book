# Typst Examples Book

See the book there: https://sitandr.github.io/typst-examples-book/book/

## Highlight & rendering

Currently powered by https://github.com/sitandr/mdbook-typst-highlight.

## Contributing

If you have a snippet you want to have in a book, feel free to create an issue.

Any PR-s are very welcome!

Generally encouraged:

- Editing (expanding examples, fixing bad language issues)
- Selecting any really useful code examples from Discord and Github
- Ideas (just any ideas how to make the book more useful)

Currently needed:
- Help with updating state manual to context expressions.
- Updating examples with possibilities of new Typst versions
- Some impressive demos

If you think you can do some large work, please DM me in Discord (@sitandr) or mail (andr.sitnikov34@gmail.com) to avoid duplication.

Also please DM me if I'm forgetting about your PR. I have bad memory.

## Rules

1. Many snippets are taken from Discord, Github or other places. Without using them that book would much, much more harder to write. However, getting a consent for every snippet will be a total disaster.
    So, as a general rule, if the snippet is a non-trivial one (one that combines typst functions in a smart way), there should be a credit to original author (of course, the credit will be removed if author objects).
2. In "Typst by Example" section the concepts that are not told yet should be avoided if possible. Although it is okay to use them if they are really intuitive and without them the demonstration would be too dull.
3. "Typst Snippets" and "Typstonomicon" should not include staff that is already present in official packages. Instead, there should be a link to a package. However, it is allowed to use packages as a tool in snippets, if the package using is "secondary" there or the idea of using that package for that task is not obvious.
4. Giant queries and hack things should go to "Typstonomicon", not "Typst snippets", even if they are super-useful. "Typst snippets" should contain code as clean as possible.

## Cleaning cached Typst files

```bash
git clean -d -X -i
```

Make sure to avoid deleting something useful.

## Compiling

To compile the book, you need `typst` cli installed, `mdbook` and my highlighting & rendering preprocessor `mdbook-typst-highlight`. Assuming `typst` is already installed, installation using cargo:

```bash
cargo install mdbook
cargo install --git https://github.com/sitandr/mdbook-typst-highlight
```

Alternatively you can install them precompiled from `mdbook` and `mdbook-typst-highlight` releases. In the end you should have to have the latest versions of them all in your PATH.

After everything installed, `mdbook build` will build the book. You can also use `mdbook watch` for continuous rebuilding, and `--open` option to open the book in your browser. For more details on building, see `mdbook` documentation.
