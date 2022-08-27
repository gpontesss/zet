---
id: 20220826234311421
tags: ["vim", "regex", "non-greedy"]
---

# Non-greedy and multiple-line matching regexes in vim

Vim has flexible regex syntax that comes to be very powerful. I wanted to make
everything inside every pair of parenthesis bold with Markdown. To do it,
non-greedy and multiple-line matchings are required:

+ For non-greedy matching use `\{-}` after what you're trying to match; (See
    `help non-greedy` for more details);
+ For multiple-line matching, use `\_` before a collection you're trying to
    match. It will include the "\n" (newline) character in the collection.

So, to make everything bold between parenthesis respecting line breaks, just
run: `%s:(\_.\{-}):**&**:g`. (Maybe try it in this file.)
