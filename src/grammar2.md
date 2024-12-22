`document`	:= `bom`? `version`? `nodes`

# Nodes
`nodes`	:= (`line-space`* `node`)* `line-space`*

`base-node`	:=   `slashdash`? `type`? `node-space`* `string`
  (`node-space`+ `slashdash`? `node-prop-or-arg`)* // slashdashed node-children must always be after props and args
  (`node-space`+ `slashdash`  `node-children`)*
  (`node-space`+              `node-children`)?
  (`node-space`+ `slashdash`  `node-children`)*
   `node-space`*
`node`      	:= `base-node` `node-terminator`
`final-node`	:= `base-node` `node-terminator`?

# Entries
`node-prop-or-arg`	:= `prop` | `value`
`node-children`   	:= `{` `nodes` `final-node`? `}`
`node-terminator` 	:= `single-line-comment` | `newline` | ; | `eof`

`prop` 	:= `string` `node-space`* = `node-space`* `value`
`value`	:= `type`?  `node-space`*                (`string` | `number` | `keyword`)
`type` 	:= `(`      `node-space`*                 `string`                         `node-space`* `)`

# Strings
`string`	:= `identifier-string` | `quoted-string` | `raw-string` ¶

`identifier-string`             	:= `unambiguous-ident` | `signed-ident` | `dotted-ident`
`unambiguous-ident`             	:=           ((`identifier-char` - `digit` - `sign` - .) `identifier-char`*) - `disallowed-keyword-strings`
`signed-ident`                  	:= `sign`    ((`identifier-char` - `digit`          - .) `identifier-char`*)?
`dotted-ident`                  	:= `sign`? . ((`identifier-char` - `digit`             ) `identifier-char`*)?
`identifier-char`               	:= `unicode` - `unicode-space` - `newline` - `[\/(){};[]"#=]` - `disallowed-literal-code-points`
`disallowed-keyword-identifiers`	:= true | false | null | inf | '-inf' | nan

`quoted-string`          	:= `"`             `single-line-string-body` `"`
  →                      	 | `"""` `newline` `multi-line-string-body` `newline` (`unicode-space` | `ws-escape`)* `"""`
`single-line-string-body`	:= (              `string-character` - `newline`)*
`multi-line-string-body` 	:= ((`"`|`""`)?   `string-character`            )*
`string-character`       	:= `usv-escape` | `ws-escape` | `[^\"]` - `disallowed-literal-code-points`
`usv-escape`             	:= `\` (`["\bfnrts]`    | `u{` `hex-digit`{1,6} `}`)
`ws-escape`              	:= `\` (`unicode-space` | `newline`                )+
`hex-digit`              	:= [0-9a-fA-F]

`raw-string`                 	:= # `raw-string-quotes` #
  →                          	 | # `raw-string`        #
`raw-string-quotes`          	:=      `"`   `single-line-raw-string-body`   `"` | `"""` `newline` `multi-line-raw-string-body` `newline` `unicode-space`* `"""`
`single-line-raw-string-body`	:= '' |     (`single-line-raw-string-char` - `"`) `single-line-raw-string-char`* ?
  →                          	      | `"` (`single-line-raw-string-char` - `"`) `single-line-raw-string-char`* ?
`single-line-raw-string-char`	:=  `unicode` - `newline` - `disallowed-literal-code-points`
`multi-line-raw-string-body` 	:= (`unicode` - `disallowed-literal-code-points`)* ?

# Numbers
number	:= `keyword-number` | `hex` | `octal` | `binary` | `decimal`

`decimal` 	:=      `sign`? `integer` (. `integer`)? `exponent`?
`exponent`	:= [eE] `sign`? `integer`
`integer` 	:= `digit` (`digit`|_)*
`digit`   	:= [0-9]
`sign`    	:= [+-]

`hex`   	:= `sign`? 0x `hex-digit` (`hex-digit` | _)*
`octal` 	:= `sign`? 0o [0-7] [0-7_]*
`binary`	:= `sign`? 0b [0 1] [0 1_]*

# Keywords and booleans
`keyword`       	:= `boolean` | #null
`keyword-number`	:= #inf  | `#-inf` | #nan
`boolean`       	:= #true | #false

# Specific code points
`bom`                           	:= '\u{FEFF}'
`disallowed-literal-code-points`	:= See Table (Disallowed Literal Code Points)
`unicode`                       	:= Any Unicode Scalar Value
`unicode-space`                 	:= See Table (All White_Space unicode characters which are not ``newline``)

# Comments
`single-line-comment`	:= `//` ^`newline`* (`newline` | `eof`)
`multi-line-comment` 	:= `/*` `commented-block`
`commented-block`    	:= `*/` | (`multi-line-comment` | `*` | `/` | [^*/]+) `commented-block`
`slashdash`          	:= `/-` `line-space`*

# Whitespace
`ws`     	:= `unicode-space` | `multi-line-comment`
`escline`	:= '\\' `ws`* (`single-line-comment` | `newline` | `eof`)
`newline`	:= See Table (All Newline White_Space)
# Whitespace where newlines are allowed
`line-space`	:= `node-space` | `newline` | `single-line-comment`
# Whitespace within nodes, where newline-ish things must be esclined.
`node-space`	:= `ws`* `escline` `ws`* | `ws`+

# Version marker
`version`	:= '/-' `unicode-space`* 'kdl-version' `unicode-space`+ ([12]) `unicode-space`* `newline`

### Grammar language

`[^\"]` are not literals, just escaped to avoid `\\`

The grammar language syntax is a combination of ABNF with some regex spice thrown in.

* Single quotes (`'`) are used to denote literal text. `\` within a literal string is used for escaping other single-quotes, for initiating unicode characters using hex values (`\u{FEFF}`), and for escaping `\` itself (`\\`).
* `*` is used for "zero or more", `+` is used for "one or more", and `?` is used for "zero or one". Per standard regex semantics, `*` and `+` are *greedy*; they match as many instances as possible without failing the match.
* `*?` (used only in raw strings) indicates a *non-greedy* match; it matches as *few* instances as possible without failing the match.
* `¶` is a *cut point*. It always matches and consumes no characters, but once matched, the parser is not allowed to backtrack past that point in the source
  If a parser would rewind past the cut point, it must instead fail the overall parse, as if it had run out of options.
  (only for `raw-string` to ensure the 1st instance of the appropriate closing quote sequence ends it)
* `()` can be used to group matches that must be matched together.
* `a | b` means `a or b`, whichever matches first. If multiple items are before a `|`, they are a single group. `a b c | d` is equivalent to `(a b c) | d`
* `[]` are used for regex-style character matches, where any character between the brackets will be a single match. `\` is used to escape `\`, `[`, `]`. They also support character ranges (`0-9`), and negation (`^`)
* `-` is used for "except for" or "minus" whatever follows it. For example, `a - 'x'` means "any `a`, except something that matches the literal `'x'`".
* `^` prefix = "does not match" whatever follows it: `^foo` = "must not match `foo`"
* A single definition may be split over multiple lines. Newlines are treated as spaces
* `//` followed by text on its own line is used as comment syntax
