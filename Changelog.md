# Changelog
All notable changes to this project will be documented in this file

[unreleased]: https://github.com/eugenesvk/sublime-kdl/compare/0.9.3...HEAD
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

- __Added__
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
