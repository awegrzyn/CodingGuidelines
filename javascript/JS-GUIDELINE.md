# ALICE O<sup>2</sup> JavaScript Coding Guideline

This document is based on [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html) under the [CC-By 3.0 License](https://creativecommons.org/licenses/by/3.0/deed.en_US). 

# Introduction
This document serves as the complete definition of ALICE O<sup>2</sup> coding standards for source code in the JavaScript programming language (including node.js). A JavaScript source file meets ALICE O<sup>2</sup> coding standard if and only if it adheres to the rules herein.

### Terminology
The term comment always refers to implementation comments. We do not use the phrase documentation comments, instead using the common term *JSDoc* for both human-readable text and machine-readable annotations within ```/** … */```.

This Style Guide uses [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt) terminology when using the phrases *must*, *must not*, *should*, *should not*, and *may*. The terms *prefer* and *avoid* correspond to *should* and *should not* respectively. Imperative and declarative statements are prescriptive and correspond to *must*.

# Source file basics

## File name
File names must be all lowercase and may include dashes *(-)*, but no additional punctuation. Follow the convention that your project uses. Filenames’ extension must be *.js*.

**Exception**: jQuery widget file names should be suffixed with *.widget* eg. WebSocket jQuery widget file should be called *websocket.widget.js*.

## File encoding
Source files are encoded in UTF-8.

## Special characters
Aside from the line terminator sequence, the ASCII horizontal space character (0x20) is the only whitespace character that appears anywhere in a source file. This implies that:

 * All other whitespace characters in string literals are escaped
 * Tab characters are not used for indentation.

# Source file structure
A source file consists of, in order:

1. @fileoverview (optional as it's currently omitted by Markdown API generator)
2. @author
2. Require statements
3. The file's implementation

## Require statements
Imports are done with require statements, grouped together immediately following the module declaration. Each require is assigned to a single constant alias, or else destructured into several constant aliases. These aliases are the only acceptable way to refer to the required dependency, whether in code or in type annotations: the fully qualified name is never used except as the argument to require. If a module is imported only for its side effects, the assignment may be omitted, but the fully qualified name may not appear anywhere else in the file. Alias names should match the final dot-separated component of the imported module name when possible, though additional components may be included.

If a long alias or module name would cause a line to exceed the 100-column limit, it must not be wrapped: require lines are an exception to the 100-column limit.

Example:
```javascript
const MyClass = require('some.package.MyClass');
const NsMyClass = require('other.ns.MyClass');
const testingAsserts = require('testing.asserts');
const than80columns = require('pretend.this.is.longer.than80columns');
const {clear, forEach, map} = require('array');
```
## The file’s implementation
The actual implementation follows after all dependency information is declared (separated by at least one blank line).
This may consist of any module-local declarations (constants, variables, classes, functions, etc), as well as any exported symbols.

# Formatting

## Braces
Braces are required for all control structures (i.e. if, else, for, do, while, as well as any others), even if the body contains only a single statement. The first statement of a non-empty block must begin on its own line.

Braces follow the Kernighan and Ritchie style (Egyptian brackets) for nonempty blocks and block-like constructs:

No line break before the opening brace.
Line break after the opening brace.
Line break before the closing brace.
Line break after the closing brace if that brace terminates a statement or the body of a function or class statement, or a class method. Specifically, there is no line break after the brace if it is followed by else, catch, while, or a comma, semicolon, or right-parenthesis.
Example:
```javascript
class InnerClass {
  constructor() {}

  /** @param {number} foo */
  method(foo) {
    if (condition(foo)) {
      try {
        // Note: this might fail.
        something();
      } catch (err) {
        recover();
      }
    }
  }
}
```

An empty block or block-like construct may be closed immediately after it is opened, with no characters, space, or line break in between (i.e. {}), unless it is a part of a multi-block statement (one that directly contains multiple blocks: if/else or try/catch/finally).

Example:
```javascript
function doNothing() {}
```

## Block indentation: +2 spaces
Each time a new block or block-like construct is opened, the indent increases by two spaces. When the block ends, the indent returns to the previous indent level. The indent level applies to both code and comments throughout the block.