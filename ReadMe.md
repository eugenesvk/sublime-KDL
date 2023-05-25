<p align="center">
A Sublime Text 4 syntax highlighting package for the <a href="https://kdl.dev"><b>KDL</b> cuddly document language</a>
</p>

## Introduction

This package adds support for the `KDL` document language (for files with `.kdl` extension)

## Installation

- __Via [Package Control](https://packagecontrol.io)__: open `Command Palette` → `Package Control: Install Package` → `kdl`<br>
                                          <kbd>^Ctrl</kbd>/<kbd>⌘Cmd</kbd><kbd>⇧Shift</kbd><kbd>P</kbd>

- __Manually__: clone this repository to your [Packages directory](https://www.sublimetext.com/docs/packages.html) and rename it to `kdl`
```sh
cd /path/to/sublime/packages/directory
git clone https://github.com/eugenesvk/sublime-kdl.git
mv sublime-kdl KDL
```

## Usage

Open any `kdl` file (e.g. [syntax_example_screen.kdl](./test/syntax_example_screen.kdl)) and verify that the selected syntax is `KDL` and KDL-specific contexts are properly scoped[^1] and highlighted, maybe like so (depending on your color scheme):

![KDL syntax screenshot solarized](https://github.com/eugenesvk/sublime-KDL/blob/main/doc/KDL_syntax_dark.png?raw=true "Custom solarized scheme")

![KDL syntax screenshot default](https://github.com/eugenesvk/sublime-KDL/blob/main/doc/KDL_syntax_light.png?raw=true "Default color scheme")

[^1]: scope naming is supposed to conform to [ST's scope naming guidelines](https://www.sublimetext.com/docs/scope_naming.html)

### Exposed scopes
<details>
<summary>List of scope names</summary>

  | KDL construct	| Scope name
  | :------------	| :----------
  | Mappings     	| `meta.mapping` `.key`/`.value` <br> `punctuation.separator.key-value` `punctuation.section.mapping` `.begin`/`.end` `.kdl`
  | Number       	| `meta.number` `.decimal`/`.float` <br> `.integer` `.binary`/`.decimal`/`.hexadecimal`/`.octal` <br> `constant.numeric` `.base`/`.exponent`/`.integer`/`.mantissa`/`.value` <br> `punctuation.separator` `.decimal`/`.exponent` `.kdl`
  | String       	| `meta.string` `storage.type.string` `string.quoted.double` `string.quoted.double.raw` <br> `punctuation.definition.string` `.begin`/`.end` `.kdl`
  | Comment      	| `comment.block` `comment.block.documentation` `comment.line.double-slash` <br> `punctuation.definition.comment` `begin`/`end` `.kdl`
  | Annotation   	| `meta.annotation` `punctuation.separator.annotation` `.begin`/`.end` `.kdl`
  | Entity       	| `entity.name` `.tag`/`.type`/`.tag.node` <br> `entity.other.attribute-name` `.kdl`
  | Others       	| `constant.character` `.escape`/`.escape.unicode.16-bit-hex` <br> `constant.language` `.boolean`/`.null` <br> `keyword.operator.arithmetic` `punctuation.separator.continuation.line` `punctuation.terminator.node` `.kdl`

</details>

### Keybindings

This plugin adds two keybindings for the `kdl` scope: `"`/`'` that auto-pair double/single quotes even after string modifiers

Add `"kdl.keybind_disable":true` to your `Preferences.sublime-settings` to disable

## Known issues

- Only works in Sublime Text 4 since build __4075__ (10 July 2020) since it's using [version 2](https://www.sublimetext.com/docs/syntax.html) of the syntax

## Credits

The default packages' syntax files ([Python](https://github.com/sublimehq/Packages/blob/master/Python/Python.sublime-syntax), [Bash](https://github.com/sublimehq/Packages/blob/master/ShellScript/Bash.sublime-syntax), [PHP](https://github.com/sublimehq/Packages/blob/master/PHP/PHP.sublime-syntax)), as well as [fish](https://github.com/Phidica/sublime-fish/blob/master/fish.sublime-syntax) and [vscode-kdl](https://github.com/kdl-org/vscode-kdl)
