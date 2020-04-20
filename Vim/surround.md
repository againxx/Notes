# Surround

## Commands
* `ds <target>`
* `cs <target> <replacement>`
* `cS <target> <replacement>` placeing the surrounded text on its own line
* `ys <motion/textobj> <replacement>`
* `yss <replacement>` surround current line, ignoring leading whitespace
* `yS <motion/textobj> <replacement>` placing on its own line
* `ySS <replacement>` placing on its own line
* `vS <replacement>` visual-line mode, surroundings are placed on seprate lines and indented; visual-block mode, each line is surrounded.

## Targets
* `(`, `) / b`
* `{`, `} / B`
* `[`, `] / r`
* `<`, `> / a`
* All opening marks contain a whitespace
* `'`, `"`, `` ` `` only searched for current line
* `t` HTML or XML tags, specify a numerical argument to get a tag other than the innermost one
* `w`, `W`, `s`, `p` (word, WORD, sentence, paragraph), when used with `cs`, one could consider them as shortcut for `ysi` (`cswb` == `ysiwb`)

## Replacement
* `)`, `}`, `]`, `>` wrapped without whitespace (`b` `B` `r` `a` are aliases)
* `(`, `{`, `[` append an additional space
* `<C-]` add { } on lines seprate from the content
* `t / <` HTML/XML tag
* `f` wrapped with (), `F` adds addtional spaces, `<C-f>` inserts function name inside ()
* `s` a leading but not trailing sapce is added, useful for removing parentheses from a function call with `csbs`

