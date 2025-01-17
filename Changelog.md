# Changelog
All notable changes to this project will be documented in this file

[unreleased]: https://github.com/eugenesvk/sublime-kdl/compare/2.0.2...HEAD
## [Unreleased]
<!-- - __Added__ -->
  <!-- + :sparkles:  -->
  <!-- new features -->
<!-- - __Changed__ -->
  <!-- +   -->
  <!-- changes in existing functionality -->
<!-- - __Fixed__ -->
  <!-- + :beetle:  -->
  <!-- bug fixes -->
<!-- - __Deprecated__ -->
  <!-- + :poop:  -->
  <!-- soon-to-be removed features -->
<!-- - __Removed__ -->
  <!-- + :wastebasket:  -->
  <!-- now removed features -->
<!-- - __Security__ -->
  <!-- + :lock:  -->
  <!-- vulnerabilities -->

- __Changed__
  + slashdash error highlights
  + raw multiline string missing newline error scoping
  + scope only 1 sym in raw multiline as error, not 2
  + Misc tests
  + Don't color partial hex
  + better highlight pre-ending multiline errors `/-`
- __Fixed__
  + consuming node end after bare ids in args/props, preventing a different number of pops in/outside of children
  + no error highlight misc invalid numbers with decimal separator
  + no error highlight on children without separators
  + mark glued slashdashed as illegal
  + no error on the 1st `_` after `.` in decimals
  + no error on empty types
  + no error on escaped whitespace in dedentsp in raw strings
  + eof misfiring on regular newlines due to a wrong rule
  + bare ids not recognizing the start of non-whitespace node space
  + bare ids treating child begin/end markers as invalid
  + no error on ending multiline string when its newline is "eaten" by an escape-chars
  + child node term not popping enough with `/-`
  + child node not requiring space before it
  + missing `node_end4` rule
  + slashdash newline before entry failing
  + unnecessary errors on multiple ␤ in esclines
  + `char-esc` lower priority in strings over error `\"""`
  + wrong spacing after `/-{child` preventing `\` escline from working
  + `w␠⎋s` definition
  + handle more escaped chars in multiline str `/-`
  + handle closing multiline quotes in contiguous space rule

[2.0.2]: https://github.com/eugenesvk/sublime-kdl/releases/tag/2.0.2
## [2.0.2]
- __Changed__
  + scope to `text.kdl.1` from `text.kdl1` (same for `2`) to allow using shared rules even in files with a single forced version

[2.0.1]: https://github.com/eugenesvk/sublime-kdl/releases/tag/2.0.1
## [2.0.1]
- __Fixed__
  + unhide the main `KDL` syntax to work around a `AFileIcon` bug that overrides the syntax to a plain text

[2.0.0]: https://github.com/eugenesvk/sublime-kdl/releases/tag/2.0.0
## [2.0.0]
- __Added__
  + ✨ support for `v2`
  + support for the version marker
  + support for `kdl1` `kdl2` file extensions
- __Changed__
  + v1 syntax to `KDL1`
  + scope to `text.kdl1` from `source.kdl1` (the latter is for programming languages)

[0.9.3]: https://github.com/eugenesvk/sublime-kdl/releases/tag/0.9.3
## [0.9.3]
- __Fixed__
  + :beetle: add vertical tab to the list of whitespace characters
  + :beetle: fix meta scope (quoted node name) bleeding into non-node strings

[0.9.2]: https://github.com/eugenesvk/sublime-kdl/releases/tag/0.9.2
## [0.9.2]
- __Fixed__
  + :beetle: invalid multiline raw strings

[0.9.1]: https://github.com/eugenesvk/sublime-kdl/releases/tag/0.9.1
## [0.9.1]
- __Fixed__
  + :beetle: ending `}` breaking the following `}` in children

[0.9.0]: https://github.com/eugenesvk/sublime-kdl/releases/tag/0.9.0
## [0.9.0]
- __Added__
  + :sparkles: scopes to `/-`slashdashed commented blocks to allow coloring them, e.g., in muted colors
  + color schemes used for the screenshots and illustrating the `/-`slashdashed commented blocks highlights
- __Changed__
  + :recycle: substantially improve spec compliance by differentiating between node elements (property vs. argument) and mandating spaces where necessary
  + expand syntax test
  + example document for a screenshot and screenshots

[0.1.1]: https://github.com/eugenesvk/sublime-kdl/releases/tag/0.1.1
## [0.1.1]
- __Added__
  + :sparkles: KDL syntax
  + add keymap to auto-pair quotes after string modifiers
  + preferences for `//line`, `/*block*/`, and `/-slashdash` comments
  + syntax test
  + example document for a screenshot and screenshots
