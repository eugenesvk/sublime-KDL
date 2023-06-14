1. Clauses provide meta-data for the syntax such as the file extensions, as well as some meta-programming
  <name> <parameters> = <value>
    <name> must follow `SCREAMING_SNAKE_CASE`, ↓ reserved
      `NAME`         	: syntax name (|base-name| of the sbnf file)
      `EXTENSIONS`   	: space-separated list of file extensions     = `file_extensions` @sublime-syntax
      `FIRST_LINE`   	: regex for matching the first line of a file = `first_line_match`@sublime-syntax
      `SCOPE`        	: default grammar scope |source.name|
      `SCOPE_POSTFIX`	: postfix appended to all scopes in the grammar (excluding the SCOPE clause) |name|. Can be left empty to leave out the postfix
      `HIDDEN`       	: show syntax in the menu
    <parameters>     	???
2. Rules are the bnf-style rules that define the parsing and scoping of the grammar
  with parameters                	instantiated when used
  match based on                 	`type`+`value` of each parameter
  terminal args                  	matched based on regex equivalence
  rule     args                  	matched       by name
  Free variable                  	identifier without a rule reference (unique to the rule's scope). Matches any argument and may be passed in and or interpolated
  #[var_interpolation]           	in terminal/options
  <name>[<parameters>]{<options>}	: <expression> ;
    <name>                       	must follow `kebab-case`, can use same name with different parameters
    <parameters>                 	for meta-programming
      [<value>,<value>]          	<value> identifier|regex¦literal terminal
    <options>                    	for sublime-syntax specific options, comma-separated list
      {}                         	optional when no options
      {<param>,<key>:<value>}    	illegal chars `,` `:` `}`
      for literal/regex          	terminals
                  <scope>        	scope of        terminal
        <capture>:<scope>        	scope for regex capture group. <capture> must be an integer
      for <rules>                	.
        <meta-scope>             	=`meta_scope` or `meta_content_scope` in sublime-syntax
    <expression>                 	.
      \`<literal>\` {<options>}  	terminal matching text literally
      '<regex>'   {<options>}    	terminal matching text according to a regex
      <identifier>[<arguments>]  	non-terminal matching another rule
       <expr> | <expr>           	alternation   Matches either ← or          →. Lists allowed 'a' | 'b' | 'c'
       <expr>   <expr>           	concatenation Matches        ← followed by →. Lists allowed 'a'   'b'   'c'
      (<expr>)                   	grouping
       <expr>?                   	optional  Matches nothing or the expression
       <expr>*                   	repeating Matches the expression ≥0 times
      ~<expr>                    	passive   Matches any text until the expression matches

SBNF translates into a set of sublime-syntax contexts
  - 'a' 'b' translates into two contexts, one matching the regex 'a' and sets the context that matches the regex 'b'
  - like most other sublime syntaxes, any amount of whitespace is allowed between the contexts, so any ↓ match
    - ab
    - a     b
    - a
    - b
SBNF rules can't replace sublime-syntax regexes for matching a contiguous symbol

`main` and `prototype` are special contexts that can never pop. Thus SNBF makes
  - `main = expr` equivalent to
  - `main = expr*`
