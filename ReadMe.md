<p align="center">
A Sublime Text 4 syntax highlighting package for the <a href="https://kdl.dev"><b>KDL</b> cuddly document language</a>
</p>

## Introduction

This package adds support for the `KDL` document language (for files with `.kdl` extension)

## Install

- __Via [Package Control](https://packagecontrol.io)__: open `Command Palette` → `Package Control: Install Package` → `kdl`<br>
                                          <kbd>^Ctrl</kbd>/<kbd>⌘Cmd</kbd><kbd>⇧Shift</kbd><kbd>P</kbd>

- __Manually__: clone this repository to your [Packages directory](https://www.sublimetext.com/docs/packages.html) and rename it to `kdl`
```sh
cd /path/to/sublime/packages/directory
git clone https://github.com/eugenesvk/sublime-kdl.git
mv sublime-kdl KDL
```

- Your color scheme likely needs to be patched to ignore or take full advantages of the /-slashdashed comment blocks:
  - to style /-slashdashed elements with muted colors:
    - add ` -comment` to your scopes, e.g.,
      `{"name":"Tag name","foreground":"var(blue6)","scope":"entity.name.tag -comment"},`
    - add a copy of the same rule with an extra ` comment` scope and a blending color function, e.g.,
      `{"name":"Tag name C","foreground":"color(var(blue6) blend(#000 60% hsl))","scope":"entity.name.tag comment"},`
  - to style /-slashdashed elements like regular comments add `comment.line.slash-dash.kdl` scope to your __Comment__ rule (e.g., `{"name":"Comment","foreground":"black","scope":"comment, comment.line.slash-dash.kdl"},`) so that its 4 level specificity overrides other rules like `entity.other.attribute-name`
  Patched examples used for the screenshots below: [solarized](./src/ESCombo.sublime-color-scheme) [default](./src/Mariana.sublime-color-scheme)

## Uses

Open any `kdl` file (e.g. [syntax_example_screen.kdl](./test/syntax_example_screen.kdl)) and verify that the selected syntax is `KDL` and KDL-specific contexts are properly scoped[^1] and highlighted, maybe like so (depending on your color scheme):

![KDL syntax screenshot solarized](https://github.com/eugenesvk/sublime-KDL/blob/main/doc/KDL_syntax_dark.png?raw=true "Custom solarized scheme")

![KDL syntax screenshot default](https://github.com/eugenesvk/sublime-KDL/blob/main/doc/KDL_syntax_light.png?raw=true "Default color scheme")

[^1]: scope naming is supposed to conform to [ST's scope naming guidelines](https://www.sublimetext.com/docs/scope_naming.html)

### Exposed scopes
<details>
<summary>List of scope names</summary>

  | KDL construct	| Scope name
  | :------------	| :----------
  | Entity       	| `entity.name.` `tag.node`¦`type` <br> `entity.other.attribute-name` `.kdl`
  | Elemens      	| `meta.` `node`¦`block.child`¦`argument.value`¦`property.` ` `¦`name`¦`separator`¦`value` `.kdl`
  | Mappings     	| `meta.mapping.` `key`¦`separator`¦`value` <br> `punctuation.separator.key-value` `punctuation.section.mapping.` `begin`¦`end` `.kdl`
  | Number       	| `constant.numeric.` `decimal`¦`float`¦`integer.` ` `¦`binary`¦`octal`¦`hexadecimal` <br> `constant.numeric.` `base`¦`exponent`¦`significand`¦`value`  <br> `punctuation.separator.` `decimal`¦`exponent`¦`number` `.kdl`
  | String       	| `meta.string` `storage.type.string` `string.quoted.double.` ` `¦`raw` <br> `punctuation.definition.string.` `begin`¦`end` `.kdl`
  | Comment      	| `comment.block` `comment.block.documentation` `comment.` `block`¦`line.` `double-slash` <br> `punctuation.definition.comment.` `begin`¦`end` `.kdl`
  | Annotation   	| `meta.annotation` `punctuation.separator.annotation.` `begin`¦`end` `.kdl`
  | Others       	| `constant.character.` `escape`¦`escape.unicode.16-bit-hex` <br> `constant.language.` `boolean`¦`null` <br> `keyword.` `other`¦`operator.arithmetic` `punctuation.separator.continuation.line` `punctuation.terminator.node` <br> `invalid.illegal.` ` `¦`muted`¦`position`¦`muted.position` `.kdl`

</details>

### Keybindings

This plugin adds two keybindings for the `kdl` scope: `"`/`'` that auto-pair double/single quotes even after string modifiers

Add `"kdl.keybind_disable":true` to your `Preferences.sublime-settings` to disable

## Known issues

- Only works in Sublime Text 4 since build __4075__ (10 July 2020) since it's using [version 2](https://www.sublimetext.com/docs/syntax.html) of the syntax

## Credits

The default packages' syntax files ([Python](https://github.com/sublimehq/Packages/blob/master/Python/Python.sublime-syntax), [Bash](https://github.com/sublimehq/Packages/blob/master/ShellScript/Bash.sublime-syntax), [PHP](https://github.com/sublimehq/Packages/blob/master/PHP/PHP.sublime-syntax)), as well as [fish](https://github.com/Phidica/sublime-fish/blob/master/fish.sublime-syntax) and [vscode-kdl](https://github.com/kdl-org/vscode-kdl)
