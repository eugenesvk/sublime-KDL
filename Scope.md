### Exposed scopes

  | KDL construct	| Scope name
  | :------------	| :----------
  | Entity       	| `entity.name.` `tag.node`¦`type` <br> `entity.other.attribute-name` `.kdl`
  | Elemens      	| `meta.` `node`¦`block.child`¦`argument.value`¦`property.` ` `¦`name`¦`separator`¦`value` `.kdl`
  | Mappings     	| `meta.mapping.` `key`¦`separator`¦`value` <br> `punctuation.separator.key-value` `punctuation.section.mapping.` `begin`¦`end` `.kdl`
  | Number       	| `constant.numeric.` `decimal`¦`float`¦`integer.` ` `¦`binary`¦`octal`¦`hexadecimal` <br> `constant.numeric.` `base`¦`exponent`¦`significand`¦`value`  <br> `punctuation.separator.` `decimal`¦`exponent`¦`number` `.kdl`
  | String       	| `meta.string` `storage.type.string` `string.quoted.double.` ` `¦`raw` <br> `punctuation.definition.string.` `begin`¦`end` `.kdl`
  | Comment      	| `comment.block` `comment.block.documentation` `comment.` `block`¦`line.` `double-slash` <br> `punctuation.definition.comment.` `begin`¦`end` `.kdl`
  | Annotation   	| `meta.annotation` `punctuation.separator.annotation.` `begin`¦`end` `.kdl`
  | Others       	| `constant.character.` `escape`¦`escape.unicode.16-bit-hex` <br> `constant.language.` `boolean`¦`null` <br> `keyword.` `other`¦`operator.arithmetic` `punctuation.separator.continuation.line` `punctuation.terminator.node` <br> `invalid.illegal.` ` `¦`muted`¦`position`¦`muted.position` `.kdl` <br> `text` `.kdl.1`¦`.kdl.2` (depending on the identified version)
