---
layout: default
---

<h2 id="toc">Table of contents</h2>

<div markdown="1">
### [HTML](#html)

- [HTML syntax](#html-syntax)
- [HTML5 doctype](#html5-doctype)
- [Language attribute](#language-attribute)
- [IE compatibility mode](#ie-compatibility-mode)
- [Character encoding](#character-encoding)
- [CSS and JavaScript includes](#css-and-javascript-includes)
- [Practicality over purity](#practicality-over-purity)
- [Semantic HTML](#semantic-html)
- [Attribute order](#attribute-order)
- [Boolean attributes](#boolean-attributes)
- [Reduce markup](#reduce-markup)
- [Editor preferences](#editor-preferences)
</div>

<div markdown="1">
### [CSS](#css)

- [CSS syntax](#css-syntax)
- [Declaration order](#declaration-order)
- [Colors](#colors)
- [Logical properties](#logical-properties)
- [Avoid @import`s](#avoid-imports)
- [Media query placement](#media-query-placement)
- [Container queries](#container-queries)
- [Subgrid](#subgrid)
- [Single declarations](#single-declarations)
- [Shorthand notation](#shorthand-notation)
- [CSS nesting](#css-nesting)
- [Operators in preprocessors](#operators-in-preprocessors)
- [Comments](#comments)
- [Class names](#class-names)
- [Selectors](#selectors)
- [Modern pseudo-classes](#modern-pseudo-classes)
- [Child and descendant selectors](#child-and-descendant-selectors)
- [Cascade layers](#cascade-layers)
- [Organization](#organization)
</div>

## Golden rule

Enforce these, or your own, agreed upon guidelines at all times. Small or large, call out what's incorrect. For additions or contributions to this Code Guide, please [open an issue on GitHub](https://github.com/mdo/code-guide/issues/new).

> Every line of code should appear to be written by a single person, no matter the number of contributors.

## HTML

<div markdown="1">
### Syntax
{: #html-syntax }

- Don't capitalize tags, including the doctype.
- Use soft tabs with two spaces—they're the only way to guarantee code renders the same in any environment.
- Nested elements should be indented once (two spaces).
- Always use double quotes, never single quotes, on attributes.
- Don't include a trailing slash in self-closing elements—the [HTML5 spec](https://html.spec.whatwg.org/multipage/syntax.html#syntax-start-tag) says they're optional.
- Don’t omit optional closing tags (e.g. `</li>` or `</body>`).
</div>

```html
<!doctype html>
<html>
  <head>
    <title>Page title</title>
  </head>
  <body>
    <img src="images/company-logo.png" alt="Company">
    <h1 class="hello-world">Hello, world!</h1>
  </body>
</html>
```

<div markdown="1">
### HTML5 doctype

Enforce [standards mode](https://developer.mozilla.org/en-US/docs/Web/HTML/Quirks_Mode_and_Standards_Mode) and more consistent rendering in every browser possible with this simple doctype at the beginning of every HTML page. In keeping with the suggested syntax, keep it lowercase.

</div>

```html
<!doctype html>
<html>
  <head>
    <!-- ... -->
  </head>
  <body>
    <!-- ... -->
  </body>
</html>
```

<div markdown="1">
### Language attribute

From the HTML5 spec:

> Authors are encouraged to specify a lang attribute on the root html element, giving the document's language. This aids speech synthesis tools to determine what pronunciations to use, translation tools to determine what rules to use, and so forth.

Read more about the `lang` attribute [in the spec](https://html.spec.whatwg.org/multipage/semantics.html#the-html-element). Head to the <abbr title="Internet Assigned Numbers Authority">IANA</abbr> for a [list of language codes](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry).
</div>

```html
<html lang="en">
  <!-- ... -->
</html>
```

<div markdown="1">
### IE compatibility mode

There's no need to include the Internet Explorer document compatibility `<meta>` tag these days, unless you need support for IE10 and older. The tag was dropped in IE11 and isn't used in Microsoft Edge (legacy or otherwise).

For more information, [read this awesome Stack Overflow article](https://stackoverflow.com/questions/6771258/what-does-meta-http-equiv-x-ua-compatible-content-ie-edge-do).
</div>

```html
<!-- IE10 and below only -->
<meta http-equiv="x-ua-compatible" content="ie=edge">
```

<div markdown="1">
### Character encoding

Ensure proper content rendering by declaring an explicit character encoding. This also allows you to use regular characters instead of their HTML entities, like `—` instead of `&emdash;`, provided their encoding matches that of the document. For some reserved XML characters—like ampersand, non-breaking spaces, less/greater than, and quotes—you may still need to use the HTML character entities.

UTF-8 is the recommended encoding.
</div>

```html
<head>
  <meta charset="utf-8">
</head>
<body>
  <p>Use an em dash like so—no HTML entity required.</p>
</body>
```

<div markdown="1">
### CSS and JavaScript includes

Per HTML5 spec, typically there is no need to specify a `type` when including CSS and JavaScript files as `text/css` and `text/javascript` are their respective defaults.

#### HTML5 spec links

- [Using link](https://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-link-element)
- [Using style](https://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-style-element)
- [Using script](https://www.w3.org/TR/2011/WD-html5-20110525/scripting-1.html#the-script-element)
</div>

```html
<!-- External CSS -->
<link rel="stylesheet" href="code-guide.css">

<!-- In-document CSS -->
<style>
  /* ... */
</style>

<!-- JavaScript -->
<script src="code-guide.js"></script>
```

<div markdown="1">
### Practicality over purity

Strive to maintain HTML standards and semantics, but not at the expense of practicality. Use the least amount of markup with the fewest intricacies whenever possible.
</div>

```html
<!-- Good -->
<button>...</button>

<!-- Not good -->
<div class="btn" onClick="...">...</div>
```

<div markdown="1">
### Semantic HTML

Use semantic HTML5 elements to improve accessibility, SEO, and code maintainability. Semantic markup is critical for search engines, screen readers, and AI systems.

**Common semantic elements:**

```html
<!-- Good: Semantic structure -->
<article>
  <header>
    <h1>Article Title</h1>
    <p>Published on <time datetime="2026-01-17">January 17, 2026</time></p>
  </header>

  <p>Article content...</p>

  <section>
    <h2>Section heading</h2>
    <p>Section content...</p>
  </section>

  <footer>
    <p>Author information</p>
  </footer>
</article>

<!-- Bad: Generic divs -->
<div class="article">
  <div class="header">
    <h1>Article Title</h1>
  </div>
  <div class="content">...</div>
</div>
```

**Element reference:**

- `<header>` — Introductory content or navigation (can be used multiple times)
- `<nav>` — Navigation sections
- `<main>` — Primary content (only one per page)
- `<article>` — Self-contained content (blog posts, comments, widgets)
- `<section>` — Thematic grouping of content with heading
- `<aside>` — Tangentially related content (sidebars, pull quotes)
- `<footer>` — Footer content (can be used multiple times)
- `<figure>` and `<figcaption>` — Images, diagrams, code with captions
- `<time>` — Dates and times (use datetime attribute)

**Accessibility guidelines:**

```html
<!-- Good: One h1, logical hierarchy -->
<main>
  <h1>Page Title</h1>

  <section>
    <h2>Section 1</h2>
    <h3>Subsection 1.1</h3>
  </section>

  <section>
    <h2>Section 2</h2>
  </section>
</main>

<!-- Bad: Multiple h1s, skipped levels -->
<div>
  <h1>Page Title</h1>
  <h1>Another Title</h1>  <!-- Multiple h1s -->
  <h3>Section</h3>  <!-- Skipped h2 -->
</div>
```

**Quick checklist:**
- Use only one `<h1>` per page
- Don't skip heading levels (h1 → h2 → h3, never h1 → h3)
- Prefer semantic elements over `<div>` with role attributes
- Use `<button>` for actions, `<a>` for navigation
- Always include alt attributes on images
</div>

<div markdown="1">
### Attribute order

HTML attributes should come in this particular order for easier reading of code.

- `class`
- `id`, `name`
- `data-*`
- `src`, `for`, `type`, `href`, `value`
- `title`, `alt`
- `role`, `aria-*`
- `tabindex`
- `style`

Attributes that are most commonly used for identifying elements should come first—`class`, `id`, `name`, and `data` attributes. Miscellaneous attributes unique to specific elements come second, followed by accessibility and style related attributes.
</div>

```html
<a class="..." id="..." data-toggle="modal" href="#">
  Example link
</a>

<input class="form-control" type="text">

<img src="..." alt="...">
```

<div markdown="1">
### Boolean attributes

A boolean attribute is one that needs no declared value. XHTML required you to declare a value, but HTML5 has no such requirement.

For further reading, consult the [WhatWG section on boolean attributes](https://html.spec.whatwg.org/multipage/common-microsyntaxes.html#boolean-attributes)

> The presence of a boolean attribute on an element represents the true value, and the absence of the attribute represents the false value.

If you <em>must</em> include the attribute's value, and **you don't need to**, follow this WhatWG guideline:

> If the attribute is present, its value must either be the empty string or [...] the attribute's canonical name, with no leading or trailing whitespace.

In short, **don't add a value**.
</div>

```html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

<div markdown="1">
### Reduce markup

Whenever possible, avoid superfluous parent elements when writing HTML. Many times this requires iteration and refactoring, but produces less HTML.
</div>

```html
<!-- Not so great -->
<span class="avatar">
  <img src="...">
</span>

<!-- Better -->
<img class="avatar" src="...">
```

<div markdown="1">
### Editor preferences

Set your editor to the following settings to avoid common code inconsistencies and dirty diffs:

- Use soft-tabs set to two spaces.
- Trim trailing white space on save.
- Set encoding to UTF-8.
- Add new line at end of files.

Consider documenting and applying these preferences to your project's `.editorconfig` file. For an example, see [the one in Bootstrap](https://github.com/twbs/bootstrap/blob/main/.editorconfig). Learn more [about EditorConfig](https://editorconfig.org).
</div>

## CSS

<div markdown="1">
### Syntax
{: #css-syntax }

- Use soft tabs with two spaces—they're the only way to guarantee code renders the same in any environment.
- When grouping selectors, keep individual selectors to a single line.
- Include one space before the opening brace of declaration blocks for legibility.
- Place closing braces of declaration blocks on a new line.
- Include one space after `:` for each declaration.
- Each declaration should appear on its own line for more accurate error reporting.
- End all declarations with a semi-colon. The last declaration's is optional, but your code is more error prone without it.
- Comma-separated property values should include a space after each comma (e.g., `box-shadow`).
- Use space-separated values for color properties (e.g., `color: rgb(0 0 0 / .5)`). [See the Colors section for more information.](#colors)
- Don't prefix property values or color parameters with a leading zero (e.g., `.5` instead of `0.5` and `-.5px` instead of `-0.5px`).
- Lowercase all hex values, e.g., `#fff`. Lowercase letters are much easier to discern when scanning a document as they tend to have more unique shapes.
- Use shorthand hex values where available, e.g., `#fff` instead of `#ffffff`.
- Quote attribute values in selectors, e.g., `input[type="text"]`. [They’re only optional in some cases](https://mathiasbynens.be/notes/unquoted-attribute-values#css), and it’s a good practice for consistency.
- Avoid specifying units for zero values, e.g., `margin: 0;` instead of `margin: 0px;`.

Questions on the terms used here? See the [syntax section of the Cascading Style Sheets article](https://en.wikipedia.org/wiki/Cascading_Style_Sheets#Syntax) on Wikipedia.
</div>

```scss
// Bad CSS
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF;
}

// Good CSS
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin-bottom: 15px;
  background-color: rgb(0 0 0 / .5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```

<div markdown="1">
### Declaration order

Property declarations should be grouped together in the following order:

1. Positioning
2. Box model
3. Typographic
4. Visual
5. Misc

Positioning comes first because it can remove an element from the normal document flow and override box model related styles. The box model—whether it's flex, float, grid, or table—follows as it dictates a component's dimensions, placement, and alignment. Everything else takes place _inside_ the component or without impacting the previous two sections, and thus they come last.

While `border` is part of the box model, most systems globally reset the [`box-sizing`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing) to `border-box` so that `border-width` doesn't affect overall dimensions. This, combined with keeping `border` near `border-radius`, is why it's under the Visual section instead.

Preprocessor mixins and functions should appear wherever most appropriate. For example, a `border-top-radius()` mixin would go in place of `border-radius` properties, while a `responsive-font-size()` function would go in place of `font-size` properties.

For a complete list of properties and their order, please see the [property order for Stylelint](https://github.com/stormwarning/stylelint-config-recess-order) used by [Bootstrap](https://getbootstrap.com).
</div>

```scss
.declaration-order {
  // Positioning
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  // Box model
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;

  // Typography
  font: normal 14px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;
  text-decoration: underline;

  // Visual
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  // Misc
  opacity: 1;
}
```



<div markdown="1">
### Colors

With CSS Color Level 4 supported in all modern browsers, rgba() and hsla() are now aliases for rgb() and hsl().

Use space-separated syntax instead of comma-separated:
- rgb(255 255 255 / .5) instead of rgba(255, 255, 255, 0.5)
- hsl(200 100% 50% / .8) instead of hsla(200, 100%, 50%, 0.8)

For devices with P3 or wider color gamuts, consider using oklch() for more vibrant colors:
- oklch(lightness chroma hue / alpha)
- Example: oklch(0.7 0.2 150) produces a vibrant green beyond sRGB range

Ensure all color choices meet WCAG contrast ratios (4.5:1 for small text, 3:1 for large).
</div>

```css
// Old syntax (avoid)
.element {
  color: rgba(255, 255, 255, 0.65);
  background-color: rgba(0, 0, 0, 0.95);
}

// Modern syntax (use)
.element {
  color: rgb(255 255 255 / .65);
  background-color: rgb(0 0 0 / .95);
}

// For wider color gamuts (P3 displays)
.element {
  color: oklch(0.95 0.05 200 / .65);
  background-color: oklch(0.1 0.02 0 / .95);
}
```

<div markdown="1">
### Avoid `@import`s

Compared to `<link>`s, `@import` is slower, adds extra page requests, and can cause other unforeseen problems. Avoid them and instead opt for an alternate approach:

- Use multiple `<link>`elements
- Compile your CSS with a preprocessor like [Sass](https://sass-lang.com/) or [Less](https://lesscss.org/) into a single file
- Concatenate your CSS files with features provided in Rails, Jekyll, and other environments

For more information, [read this article by Steve Souders](https://www.stevesouders.com/blog/2009/04/09/dont-use-import/).
</div>

```html
<!-- Use link elements -->
<link rel="stylesheet" href="core.css">

<!-- Avoid @imports -->
<style>
  @import url("more.css");
</style>
```

<div markdown="1">
### Media query placement

Place media queries as close to their relevant rule sets whenever possible. Don't bundle them all in a separate stylesheet or at the end of the document. Doing so only makes it easier for folks to miss them in the future. Here's a typical setup.
</div>

```css
.element { ... }
.element-avatar { ... }
.element-selected { ... }

@media (min-width: 480px) {
  .element { ... }
  .element-avatar { ... }
  .element-selected { ... }
}
```

<div markdown="1">
### Container queries

Container queries allow components to adapt based on their container size rather than viewport size. This enables truly reusable, responsive components. Browser support reached 92% in 2023.

**Basic usage:**

```css
// Define a container
.card-wrapper {
  container-type: inline-size;
}

// Query based on container width
@container (min-width: 400px) {
  .card {
    display: grid;
    grid-template-columns: 150px 1fr;
  }
}

@container (min-width: 600px) {
  .card {
    grid-template-columns: 200px 1fr 150px;
  }
}
```

**Named containers for specificity:**

```css
.sidebar {
  container-type: inline-size;
  container-name: sidebar;
}

.main-content {
  container-type: inline-size;
  container-name: main;
}

@container sidebar (min-width: 300px) {
  .widget { /* styles */ }
}

@container main (min-width: 800px) {
  .article { /* styles */ }
}
```

**When to use container queries vs media queries:**
- Use **media queries** for layout-level changes (header, sidebar, overall grid)
- Use **container queries** for component-level changes (cards, widgets, modules)

**Benefits:**
- Components adapt to their space, not screen size
- More reusable across different layouts
- Components can be responsive in sidebars, grids, or full-width
- Reduces need for component variants

Place container queries near their component styles, just like media queries.
</div>

<div markdown="1">
### Subgrid

Subgrid allows nested grid items to participate in their parent's grid, solving alignment problems in complex layouts. Browser support reached 78% in 2024.

```css
.grid-container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  gap: 1rem;
}

// Child inherits parent's column tracks
.grid-item {
  display: grid;
  grid-template-columns: subgrid;

  // Now child items align with parent's columns
}
```

**Practical example (card grid):**

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.card {
  display: grid;
  grid-template-columns: subgrid;
  grid-template-rows: auto 1fr auto;
}

// All card titles, bodies, and footers align across cards
.card-title { grid-column: 1 / -1; }
.card-body { grid-column: 1 / -1; }
.card-footer { grid-column: 1 / -1; }
```

**Use cases:**
- Aligning content across cards in a grid
- Form layouts with consistent label/input columns
- Complex nested layouts

**Browser support note:**
Supported in Firefox (2019), Safari (2023), Chrome (2024). For older browsers, provide fallback:

```css
.grid-item {
  display: grid;
  grid-template-columns: repeat(3, 1fr);  // Fallback
}

@supports (grid-template-columns: subgrid) {
  .grid-item {
    grid-template-columns: subgrid;
  }
}
```
</div>

<div markdown="1">
### Single declarations

In instances where a rule set includes **only one declaration**, consider removing line breaks for readability and faster editing. Any rule set with multiple declarations should be split to separate lines.

The key factor here is error detection—e.g., a CSS validator stating you have a syntax error on Line 183. With a single declaration, there's no missing it. With multiple declarations, separate lines is a must for your sanity.
</div>

```scss
// Single declarations on one line
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }

// Multiple declarations, one per line
.sprite {
  display: inline-block;
  width: 16px;
  height: 15px;
  background-image: url("../img/sprite.png");
}
.icon           { background-position: 0 0; }
.icon-home      { background-position: 0 -20px; }
.icon-account   { background-position: 0 -40px; }
```

<div markdown="1">
### Shorthand notation

Limit shorthand declaration usage to instances where you must explicitly set all available values. Frequently overused shorthand properties include:

- `padding`
- `margin`
- `font`
- `background`
- `border`
- `border-radius`

Usually we don't need to set all the values a shorthand property represents. For example, HTML headings only set top and bottom margin, so when necessary, only override those two values. A `0` value implies an override of either a browser default or previously specified value.

Excessive use of shorthand properties leads to sloppier code with unnecessary overrides and unintended side effects.

The Mozilla Developer Network has a great article on [shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) for those unfamiliar with notation and behavior.
</div>

```scss
// Bad example
.element {
  margin: 0 0 10px;
  background: red;
  background: url("image.jpg");
  border-radius: 3px 3px 0 0;
}

// Good example
.element {
  margin-bottom: 10px;
  background-color: red;
  background-image: url("image.jpg");
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
```

<div markdown="1">
### Logical properties

Modern CSS uses logical properties instead of directional properties for better internationalization support. Logical properties have universal browser support and automatically adapt to different writing modes (RTL, vertical text).

**Block axis** refers to the vertical direction in horizontal writing modes (top/bottom)
**Inline axis** refers to the horizontal direction in horizontal writing modes (left/right)

```css
// Directional properties (old approach)
.element {
  margin-left: auto;
  margin-right: auto;
  padding-left: 1rem;
  padding-right: 1rem;
  border-top: 1px solid #e5e5e5;
  border-bottom: 1px solid #e5e5e5;
}

// Logical properties (modern approach)
.element {
  margin-inline: auto;
  padding-inline: 1rem;
  border-block: 1px solid #e5e5e5;
}
```

**Common conversions:**

| Directional | Logical | Use case |
|------------|---------|----------|
| margin-left, margin-right | margin-inline | Horizontal margins |
| margin-top, margin-bottom | margin-block | Vertical margins |
| padding-left, padding-right | padding-inline | Horizontal padding |
| padding-top, padding-bottom | padding-block | Vertical padding |
| border-left | border-inline-start | Start border |
| border-right | border-inline-end | End border |
| width | inline-size | Element width |
| height | block-size | Element height |

**Why use logical properties?**
- Automatic RTL support (Arabic, Hebrew)
- Support for vertical writing modes (CJK languages)
- More concise code (one property instead of two)
- Future-proof for international projects
</div>

<div markdown="1">
### CSS nesting

Native CSS nesting is supported in all major browsers since August 2023. Preprocessors are no longer required for nesting, though they remain useful for variables and mixins.

**Native CSS syntax:**

```css
.table {
  width: 100%;
  border-collapse: collapse;

  // Nested element selector
  & thead {
    background-color: #f5f5f5;

    & th {
      padding: 10px;
      text-align: left;
    }
  }

  // Direct child combinator
  & > tbody > tr {
    border-bottom: 1px solid #e5e5e5;

    &:hover {
      background-color: #fafafa;
    }
  }
}
```

**Best practices:**
- Limit nesting to 2-3 levels for readability
- Use the & symbol explicitly (required for certain selectors)
- Avoid over-nesting—flat selectors are often clearer and more performant

**Good example:**

```css
.card {
  padding: 1rem;

  & .card-title {
    font-size: 1.25rem;
  }

  & .card-body {
    margin-top: 0.5rem;
  }
}
```

**Bad example (too deep):**

```css
.page {
  & .content {
    & .section {
      & .card {
        & .title {  // Too nested, hard to override
          /* ... */
        }
      }
    }
  }
}
```

**When preprocessors are still useful:**
- CSS variables with default values
- Mixins and functions
- Mathematical operations
- Build-time optimizations
</div>

<div markdown="1">
### Operators in preprocessors

For improved readability, wrap all math operations in parentheses with a single space between values, variables, and operators.
</div>

```scss
// Bad example
.element {
  margin: 10px 0 @variable*2 10px;
}

// Good example
.element {
  margin: 10px 0 (@variable * 2) 10px;
}
```

<div markdown="1">
### Comments

Code is written and maintained by people. Ensure your code is descriptive, well commented, and approachable by others. Great code comments convey context or purpose. Do not simply reiterate a component or class name. Use the `//` syntax when writing CSS with preprocessors. When shipping CSS to production, remove all comments.

Be sure to write in complete sentences for larger comments and succinct phrases for general notes.
</div>

```scss
// Bad example
// Modal header
.modal-header {
  ...
}

// Good example
// Wrapping element for .modal-title and .modal-close
.modal-header {
  ...
}
```

<div markdown="1">
### Class names

- Keep classes lowercase and use dashes (not underscores or camelCase). Dashes serve as natural breaks in related class (e.g., `.btn` and `.btn-danger`).
- Avoid excessive and arbitrary shorthand notation. `.btn` is useful for _button_, but `.s` doesn't mean anything.
- Keep classes as short and succinct as possible.
- Use meaningful names; use structural or purposeful names over presentational.
- Prefix classes based on the closest parent or base class.
- Use `.js-*` classes to denote behavior (as opposed to style), but keep these classes out of your CSS.

It's also useful to apply many of these same rules when creating custom properties and preprocessor variable names.

**Naming methodologies**

For large projects, consider adopting a naming methodology like BEM (Block Element Modifier):

```css
// Block (standalone component)
.card { }

// Element (part of block)
.card__header { }
.card__body { }
.card__footer { }
.card__title { }

// Modifier (variation)
.card--featured { }
.card--compact { }

// Element with modifier
.card__title--large { }
```

**BEM benefits:**
- Clear component hierarchy
- No specificity conflicts
- Self-documenting class names
- Easier maintenance in large teams

**Alternatives:**
- **OOCSS** (Object-Oriented CSS) — Separation of structure and skin
- **SMACSS** — Scalable and Modular Architecture
- **Utility-first** (Tailwind CSS) — Small, single-purpose classes

Choose based on project size and team preferences. For small projects, simple descriptive names may suffice.
</div>

```scss
// Bad example
.t { ... }
.red { ... }
.header { ... }

// Good example
.tweet { ... }
.important { ... }
.tweet-header { ... }
```

<div markdown="1">
### Selectors

- Use classes over generic element tags for more explicit and reliable styling that isn't dependent on your markup.
- Avoid using several attribute selectors (e.g., `[class^="..."]`) on commonly occuring components. Browser performance is known to be impacted by these.
- Keep selectors short and strive to limit the number of elements in each selector to three.
- Scope classes to the closest parent `only` when necessary (e.g., when not using prefixed classes).

**Additional reading:**

- [Scope CSS classes with prefixes](https://markdotto.com/2012/02/16/scope-css-classes-with-prefixes/)
- [Stop the cascade](https://markdotto.com/2012/03/02/stop-the-cascade/)
</div>

```scss
// Bad example
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }

// Good example
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
```

<div markdown="1">
### Modern pseudo-classes

**The :has() selector**

The :has() pseudo-class (called "parent selector") is supported in all major browsers since December 2023. It allows selecting parent elements based on their children.

```css
// Style form when it contains invalid input
form:has(input:invalid) {
  border: 2px solid #c00;
}

// Style card only if it has an image
.card:has(img) {
  display: grid;
  grid-template-columns: 200px 1fr;
}

// Style heading when followed by specific element
h2:has(+ .intro-text) {
  margin-bottom: 0.5rem;
}

// Exclude case: style articles that don't have images
.article:not(:has(img)) {
  max-width: 600px;
}
```

**:is() and :where() for grouping**

```css
// :is() takes highest specificity from arguments
:is(h1, h2, h3) {
  line-height: 1.2;
}

// Equivalent to:
h1, h2, h3 {
  line-height: 1.2;
}

// :where() always has 0 specificity (easier to override)
:where(header, main, footer) a {
  color: blue;
}
```

**Benefits:**
- Reduce JavaScript for conditional styling
- More declarative and maintainable code
- Better performance than JS-based solutions
- Powerful combinations with other selectors
</div>

<div markdown="1">
### Child and descendant selectors

When necessary, it may be helpful to use [the child combinator (`>`)](https://developer.mozilla.org/en-US/docs/Web/CSS/Child_combinator) to limit the cascade of some styles in elements like `<table>`s that are often recursively nested. Use it to limit styles to the immediate children elements of a parent element to avoid unnecessary overrides later on.
</div>

```css
.custom-table > tbody > tr > td,
.custom-table > tbody > tr > th {
  /* ... */
}
```

<div markdown="1">
### Cascade layers

Cascade layers (@layer) provide explicit control over CSS specificity without using !important. Layers are particularly useful for managing third-party styles and large codebases.

**Basic usage:**

```css
// Declare layer order upfront (lowest to highest priority)
@layer reset, base, components, utilities;

@layer reset {
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
}

@layer base {
  body {
    font-family: system-ui, sans-serif;
    line-height: 1.6;
  }
}

@layer components {
  .button {
    padding: 10px 20px;
    border-radius: 4px;
  }
}

@layer utilities {
  .m-0 { margin: 0; }
  .p-0 { padding: 0; }
}
```

**Managing third-party CSS:**

```css
@layer framework, custom;

@layer framework {
  @import url('bootstrap.css');
}

@layer custom {
  // Your styles automatically override framework layer
  .button {
    /* Custom button styles */
  }
}
```

**Layer precedence order:**
1. Unlayered styles (highest priority)
2. Layers in declaration order (last declared wins)
3. Inline styles
4. !important in reverse order

**Benefits:**
- Safely integrate third-party CSS without specificity wars
- Organize large codebases with clear priority structure
- Reduce or eliminate !important usage
- Better maintainability in team environments
</div>

<div markdown="1">
### Organization

- Organize sections of code by component.
- Develop a consistent commenting hierarchy.
- Use consistent white space to your advantage when separating sections of code for scanning larger documents.
- When using multiple CSS files, break them down by component instead of page. Pages can be rearranged and components moved.
</div>

```scss
//
// Component section heading
//

.element { ... }


//
// Component section heading
//
// Sometimes you need to include optional context for the entire component. Do that up here if it's important enough.
//

.element { ... }

// Contextual sub-component or modifer
.element-heading { ... }
```
</div>