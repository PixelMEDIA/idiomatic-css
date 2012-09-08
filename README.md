# Principles of writing consistent, idiomatic CSS

The following document outlines a reasonable style guide for CSS development.
It is not meant to be prescriptive and I do not wish to impose my style
preferences on other people's code. However, these guidelines do strongly
encourage the use of existing, common, sensible patterns.

This is a living document and new ideas are always welcome. Please
contribute.




## Table of contents

1. [General principles](#general-principles)
2. [Whitespace](#whitespace)
3. [Comments](#comments)
4. [Format](#format)
5. [Naming](#naming)
6. [Practical example](#example)
7. [Organization](#organization)
<!--
8. [Build and deployment](#build-and-deployment)
-->

[Acknowledgements](#acknowledgements)


<a name="general-principles"></a>
## 1. General principles

> "Part of being a good steward to a successful project is realizing that
> writing code for yourself is a Bad Idea™. If thousands of people are using
> your code, then write your code for maximum clarity, not your personal
> preference of how to get clever within the spec." - Idan Gazit

* You are not a human code compiler/compressor, so don't try to be one.
* All code in any code-base should look like a single person typed it, no
  matter how many people contributed.
* Strictly enforce the agreed upon style.
* If in doubt when deciding upon a style, use existing, common patterns.


<a name="whitespace"></a>
## 2. Whitespace

Only one style should exist across the entire source of your code-base. Always
be consistent in your use of whitespace. Use whitespace to improve
readability.

* _Never_ mix spaces and tabs for indentation.
* Preference is for tabs rather than spaces.

Tip: configure your editor to "show invisibles". This will allow you to
eliminate end of line whitespace, eliminate unintended blank line whitespace,
and avoid polluting commits.

Tip: use an [EditorConfig](http://editorconfig.org/) file (or equivalent) to
help maintain the basic whitespace conventions that have been agreed for your
code-base.


<a name="comments"></a>
## 3. Comments

Well commented code is extremely important. Take time to describe components,
how they work, their limitations, and the way they are constructed. Don't leave
others in the team guessing as to the purpose of uncommon or non-obvious
code.

Comment style should be simple and consistent within a single code base.

* Place comments on a new line above their subject.
* Avoid end of line comments.
* Keep line-length to a sensible maximum, e.g., 80 columns.
* Make liberal use of comments to break CSS code into discrete sections.
* Use "sentence case" comments and consistent text indentation.

Tip: configure your editor to provide you with shortcuts to output agreed-upon
comment patterns.

#### Example:

```css
/* ==========================================================================
   Section comment block
   ========================================================================== */

/* Sub-section comment block
   ========================================================================== */

/**
 * Short description using Doxygen-style comment format
 *
 * Long description first sentence starts here and continues on this line for a
 * while finally concluding here at the end of this paragraph.
 *
 * The long description is ideal for more detailed explanations and
 * documentation. It can include example HTML, URLs, or any other information
 * that is deemed necessary or useful.
 *
 * @tag This is a tag named 'tag'
 *
 * @todo This is a todo statement that describes an atomic task to be completed
 *   at a later date. It wraps after 80 characters and following lines are
 *   indented by 2 spaces.
 */

/* Basic comment */
```


<a name="format"></a>
## 4. Format

The chosen code format must ensure that code is: easy to read; easy to clearly
comment; minimizes the chance of accidentally introducing errors; and results
in useful diffs and blames.

* Use one discrete selector per line in multi-selector rulesets.
* Include a single space before the opening brace of a ruleset.
* Include one declaration per line in a declaration block.
* Use one level of indentation for each declaration.
* Include single space after the colon of a declaration.
* Use lowercase and shorthand hex values, e.g., `#aaa`.
* Use single or double quotes consistently. Preference is for double quotes,
  e.g., `content: ""`.
* Quote attribute values in selectors, e.g., `input[type="checkbox"]`.
* _Where allowed_, avoid specifying units for zero-values, e.g., `margin: 0`.
* Include a space after each comma in comma-separated property or function
  values.
* Include a semi-colon at the end of the last declaration in a declaration
  block.
* Place the closing brace of a ruleset in the same column as the first
  character of the ruleset.
* Separate each ruleset by a blank line.

```css
.selector-1,
.selector-2,
.selector-3[type="text"] {
      -webkit-box-sizing: border-box;
      -moz-box-sizing: border-box;
    box-sizing: border-box;
    display: block;
    font-family: helvetica, arial, sans-serif;
    color: #333;
    background: #fff;
    background: linear-gradient(#fff, rgba(0, 0, 0, 0.8));
}
```

#### Property order

Properties should be ordered alphabetically, with a few exceptions. Position properties (top, right, bottom, left) should be located after the "position" property and indented. Properties with vendor prefixes should be located directly above the non prefixed property and indented.

```css
.selector {
    background: #000;
    border: 10px solid #333;
      -webkit-box-sizing: border-box;
      -moz-box-sizing: border-box;
    box-sizing: border-box;
    color: #fff;
    display: inline-block;
    font-family: sans-serif;
    font-size: 16px;
    height: 100px;
    margin: 10px;
    overflow: hidden;
    padding: 10px;
    position: absolute;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
    text-align: right;
    width: 100px;
    z-index: 10;
}
```

#### Exceptions and slight deviations

Large blocks of single declarations can use a slightly different, single-line
format. In this case, a space should be included after the opening brace and
before the closing brace.

```css
.selector-1 { width: 10%; }
.selector-2 { width: 20%; }
.selector-3 { width: 30%; }
```

Long, comma-separated property values - such as collections of gradients or
shadows - can be arranged across multiple lines in an effort to improve
readability and produce more useful diffs. There are various formats that could
be used; one example is shown below.

```css
.selector {
    background-image:
        linear-gradient(#fff, #ccc),
        linear-gradient(#f3c, #4ec);
    box-shadow:
        1px 1px 1px #000,
        2px 2px 1px 1px #ccc inset;
}
```

### Preprocessors: additional format considerations

Different CSS preprocessors have different features, functionality, and syntax.
Your conventions should be extended to accommodate the particularities of any
preprocessor in use. The following guidelines are in reference to Sass.

* Limit nesting to 1 level deep. Reassess any nesting more than 2 levels deep.
  This prevents overly specific CSS selectors.
* Avoid large numbers of nested rules. Break them up when readability starts to
  be affected. Preference to avoid nesting that spreads over more than 20
  lines.
* Always place `@extend` statements on the first lines of a declaration
  block.
* Where possible, group `@include` statements at the top of a declaration
  block, after any `@extend` statements.
* Consider prefixing custom functions with `x-` or another namespace. This
  helps to avoid any potential to confuse your function with a native CSS
  function, or to clash with functions from libraries.

```scss
.selector-1 {
    @extend .other-rule;
    @include clearfix();
    @include box-sizing(border-box);
    width: x-grid-unit(1);
    // other declarations
}
```


<a name="naming"></a>
## 5. Naming

Naming is hard, but very important. It's a crucial part of the process of
developing a maintainable code base, and ensuring that you have a relatively
scalable interface between your HTML and CSS.

* Avoid _systematic_ use of abbreviated class names. Don't make things
  difficult to understand.
* Use clear, thoughtful, and appropriate names for _HTML classes_.
* Pick an understandable and consistent naming pattern that makes sense both
  within HTML files and CSS files.
* Selectors for components should uses class names; avoid the use of generic
  tags and unique ids.

```css
/* Example of code with bad names */

.s-scr {
    overflow: auto;
}

.cb {
    background: #000;
}

/* Example of code with better names */

.is-scrollable {
    overflow: auto;
}

.column-body {
    background: #000;
}
```


<a name="example"></a>
## 6. Practical example

An example of various conventions.

```css
/* ==========================================================================
   Grid layout
   ========================================================================== */

/**
 * Example HTML:
 *
 * <div class="grid">
 *     <div class="cell cell-5"></div>
 *     <div class="cell cell-5"></div>
 * </div>
 */

.grid {
    /* Remove inter-cell whitespace */
    font-size: 0;
    height: 100%;
    overflow: visible;
    /* Prevent inline-block cells wrapping */
    white-space: nowrap;
}

.cell {
    border: 2px solid #333;
    box-sizing: border-box;
    display: inline-block;
    /* Reset font-size */
    font-size: 16px;
    height: 100%;
    overflow: hidden;
    /* Set the inter-cell spacing */
    padding: 0 10px;
    position: relative;
    vertical-align: top;
    /* Reset white-space */
    white-space: normal;
    width: 20%;
}

/* Cell states */

.cell.is-animating {
    background-color: #fffdec;
}

/* Cell dimensions
   ========================================================================== */

.cell-1 { width: 10%; }
.cell-2 { width: 20%; }
.cell-3 { width: 30%; }
.cell-4 { width: 40%; }
.cell-5 { width: 50%; }

/* Cell modifiers
   ========================================================================== */

.cell--detail,
.cell--important {
    border-width: 4px;
}
```


<a name="organization"></a>
## 7. Organization

Code organization is an important part of any CSS code base, and crucial for
large code bases.

* Logically separate distinct pieces of code.
* Use separate files (concatenated by a build step) to help break up code for
  distinct components.
* If using a preprocessor, abstract common code into variables for color,
  typography, etc.

<!--
<a name="build-and-deployment"></a>
## 8. Build and deployment

Projects should always attempt to include some generic means by which source
can be linted, tested, compressed, and versioned in preparation for production
use. For this task, [grunt](https://github.com/cowboy/grunt) by Ben Alman is an
excellent tool.
-->

<a name="acknowledgements"></a>
## Acknowledgements

Thanks to everyone who has contributed to
[idiomatic.js](https://github.com/rwldrn/idiomatic.js). It was a source of
inspiration, quotations, and guidelines.
