---
render_with_liquid: false
title: "Sass — A Complete Beginner's Guide to Smarter CSS"
nav_order: 72
---

# Lesson 72 — Sass: A Complete Beginner's Guide to Smarter CSS

---

## Lesson Introduction

Have you ever been working on a website's stylesheet and thought: *"I keep typing the same colour code over and over again. There has to be a better way."* Or maybe your CSS file has grown so large it feels impossible to manage?

That is exactly the problem Sass was built to solve.

In this lesson you will learn Sass from absolute zero. By the end, you will be able to write cleaner, smarter, reusable CSS code just like professional front-end developers do every day — at companies, design agencies, and on open-source projects worldwide.

This lesson covers everything from what Sass is, to installing it, to all its most important features: variables, nesting, importing, mixins, and extending. Every concept is taught with step-by-step examples, real-world analogies, guided exercises, and a mini-project you will build from scratch.

---

## What You Need to Know Before Starting

This lesson assumes you have a basic understanding of two things:

**HTML** — the language used to create the structure of a webpage (headings, paragraphs, buttons, links, etc.).

**CSS** — the language used to style that structure (colours, fonts, spacing, layout).

If you are not yet familiar with CSS, think of it like this: HTML is the blueprint of a house, and CSS is the paint, furniture, and decoration. Sass is a smarter pen you use to write your CSS plans — it does not change what the house looks like, but it makes designing it far easier.

---

## Section 1 — What is Sass?

### The Problem with Plain CSS

Imagine you are building a website for a company. The brand colour is a deep blue: `#1a3c6e`. You use this colour for the navigation bar, the headings, the button backgrounds, the footer links, and more — maybe 30 different places in your CSS file.

Now the client says: "We changed our brand colour. Please update it everywhere."

In plain CSS, you would have to hunt through every single line and change each one manually. If you miss even one, the design breaks.

This is just one of the pain points that makes maintaining large CSS codebases exhausting.

### What is Sass?

**Sass** stands for **Syntactically Awesome Stylesheet**. It is a **CSS pre-processor** — a tool that extends CSS with powerful programming features that plain CSS does not have.

Sass was designed by Hampton Catlin and developed by Natalie Weizenbaum in 2006. It is free to download and use.

Think of Sass as a supercharged version of CSS. You write your styles in Sass format, and then a tool called a **transpiler** converts it into regular CSS that browsers can read.

> 💡 **Transpiling** means taking code written in one language and automatically translating it into another. Your browser only reads CSS — so Sass code gets converted to CSS before the browser ever sees it.

### What Can Sass Do That CSS Cannot?

Sass gives you the ability to use features that plain CSS either does not support or makes very tedious to manage. The big ones are:

- **Variables** — store values like colours, font sizes, and spacing in one place and reuse them everywhere.
- **Nesting** — write your selectors in a nested structure that mirrors your HTML, making your code easier to read.
- **Imports** — split your styles across multiple files and import them into a master file.
- **Mixins** — create reusable blocks of style code, almost like functions in programming.
- **Extend/Inheritance** — share a set of styles between multiple selectors without repeating code.

These features reduce repetition, save time, and make your stylesheets much easier to maintain.

### How Does Sass Work? The Transpiling Flow

Here is the journey your Sass code takes before a browser can use it:

```
You write Sass code   →   Sass transpiler converts it   →   Regular CSS file   →   Browser reads CSS
   (style.scss)                (automatically)              (style.css)
```

You never deliver the `.scss` file to the browser. You deliver the output `.css` file. The Sass source file is just for you (and your team) to work in.

### Sass File Type

Sass files use the `.scss` file extension. For example: `style.scss`, `_variables.scss`, `_buttons.scss`.

### Sass Comments

Sass supports two kinds of comments:

**Block comments** (same as CSS — they appear in the compiled CSS output):
```scss
/* This is a block comment — it survives transpiling */
```

**Inline comments** (Sass-only — they are removed during transpiling and do not appear in the final CSS):
```scss
// This is an inline comment — only for Sass developers
```

**Example combining both:**

```scss
/* Define the primary colour */
$brand-color: #1a3c6e;   // dark navy blue

.header {
  background-color: $brand-color;  // apply the brand color here
}
```

---

## Section 2 — Installing Sass

### System Requirements

- **Operating system:** Sass is platform-independent — it works on Windows, Mac, and Linux.
- **Browser support:** The compiled CSS output works in all modern browsers including Edge, Firefox, Chrome, Safari, and Opera.
- **Runtime:** Sass was originally built with Ruby, but the modern Dart Sass version is a standalone tool.

### How to Install Sass

There are several ways to install Sass depending on your workflow. You can find the full list of options on the official Sass website: **https://sass-lang.com/install**

The most common methods are:

**Option 1 — Using npm (Node Package Manager):**
If you have Node.js installed, open your terminal or command prompt and run:
```bash
npm install -g sass
```
This installs Sass globally on your computer.

**Option 2 — Using a GUI App:**
There are graphical applications for Mac, Windows, and Linux that handle Sass compilation with a visual interface, such as Scout-App or Koala. These are ideal if you prefer not to use the command line.

### Compiling a Sass File

Once Sass is installed, you compile a `.scss` file to `.css` using this terminal command:

```bash
sass style.scss style.css
```

This tells Sass: "Take my `style.scss` file, compile it, and output the result as `style.css`."

You can also watch a file for changes automatically (so you don't have to recompile manually every time):

```bash
sass --watch style.scss:style.css
```

> 💡 In modern projects using tools like Webpack, Vite, or Parcel, Sass compilation is often set up automatically as part of the build pipeline — so you may never need to run these commands manually.

---

## Section 3 — Sass Variables

### What is a Variable?

A **variable** is a named container that stores a value. Instead of typing the same value over and over, you store it once in a variable and then use the variable name everywhere.

Think of it like a sticky label on a bottle. The label says "Brand Blue." Whenever you need that specific shade of blue, you just look at the label — you don't have to remember the exact hex code every time.

### Why Use Variables in Sass?

Without variables:
```css
/* CSS — the old way */
.header { background-color: #1a3c6e; }
.footer { background-color: #1a3c6e; }
.button { background-color: #1a3c6e; }
/* If the colour changes, you must update ALL three manually */
```

With Sass variables:
```scss
/* Sass — the smarter way */
$brand-color: #1a3c6e;

.header { background-color: $brand-color; }
.footer { background-color: $brand-color; }
.button { background-color: $brand-color; }
/* Now if the colour changes, update ONLY the variable — done! */
```

### Sass Variable Syntax

The `$` symbol declares a variable. The syntax is:

```scss
$variable-name: value;
```

- `$` — tells Sass this is a variable (not a CSS property)
- `variable-name` — you choose a descriptive name (use hyphens or underscores)
- `:` — separates the name from the value
- `value` — whatever you are storing (a colour, a number, a font name, etc.)

### What Can Variables Store?

Sass variables can hold any of these types of values:

- **Strings (text):** `$font-stack: Helvetica, sans-serif;`
- **Numbers (with or without units):** `$font-size: 18px;` or `$ratio: 1.5;`
- **Colours:** `$primary: #ff6347;` or `$bg: lightblue;`
- **Booleans:** `$debug-mode: true;`
- **Lists:** `$spacing: 10px 20px 15px;`
- **Nulls:** `$no-value: null;`

### Simple Example: Four Variables

```scss
/* SASS — declaring variables */
$myFont: Helvetica, sans-serif;
$myColor: red;
$myFontSize: 18px;
$myWidth: 680px;

/* Using the variables */
body {
  font-family: $myFont;     /* uses the font variable */
  font-size: $myFontSize;   /* uses the font-size variable */
  color: $myColor;          /* uses the colour variable */
}

#container {
  width: $myWidth;          /* uses the width variable */
}
```

**Expected CSS Output (after transpiling):**
```css
body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: red;
}

#container {
  width: 680px;
}
```

> 🤔 **Thinking prompt:** What happens if you change `$myColor: red;` to `$myColor: navy;`? The answer: every place where `$myColor` is used will automatically update — the `body` colour becomes navy without you needing to touch the `body` rule.

### A More Realistic Example: Brand Colours

```scss
/* Define primary brand colours once */
$primary_1: #a2b9bc;   /* muted teal */
$primary_2: #b2ad7f;   /* warm khaki */
$primary_3: #878f99;   /* steel grey */

/* Apply them throughout */
.main-header {
  background-color: $primary_1;
}

.menu-left {
  background-color: $primary_2;
}

.menu-right {
  background-color: $primary_3;
}
```

**Expected CSS Output:**
```css
.main-header {
  background-color: #a2b9bc;
}

.menu-left {
  background-color: #b2ad7f;
}

.menu-right {
  background-color: #878f99;
}
```

When the brand colours change, you only update three lines at the top.

---

### Variable Scope — Local vs. Global

**Variable scope** means the area of code in which a variable is accessible.

By default, Sass variables defined inside a rule (inside `{}` curly braces) are **local** — only available within that rule. Variables defined outside all rules are **global** — available everywhere.

**Example of local vs. global scope:**

```scss
$myColor: red;    /* GLOBAL variable */

h1 {
  $myColor: green;   /* LOCAL variable — only inside h1 */
  color: $myColor;   /* Uses the LOCAL value: green */
}

p {
  color: $myColor;   /* Uses the GLOBAL value: red */
}
```

**Expected CSS Output:**
```css
h1 {
  color: green;
}

p {
  color: red;
}
```

> 🤔 **Why is this useful?** Scope protects your variables. A temporary variable inside one rule doesn't accidentally overwrite the global one.

### Using `!global` to Promote a Variable

What if you want a variable that starts inside a rule but should also be available globally? You use the `!global` flag:

```scss
$myColor: red;    /* global starts as red */

h1 {
  $myColor: green !global;   /* this OVERWRITES the global value */
  color: $myColor;           /* green */
}

p {
  color: $myColor;           /* also green now (global was changed) */
}
```

**Expected CSS Output:**
```css
h1 {
  color: green;
}

p {
  color: green;
}
```

> 💡 **Best Practice:** Avoid using `!global` inside rules if you can. Instead, define all your global variables at the top of a dedicated `_variables.scss` file so they are easy to find and update.

---

## Section 4 — Sass Nesting

### What is Nesting?

**Nesting** means placing CSS rules inside other CSS rules, mirroring the structure of your HTML.

In plain CSS, when you want to style elements inside other elements, you repeat the parent selector:

```css
/* Plain CSS — repetitive selectors */
nav ul { margin: 0; padding: 0; list-style: none; }
nav li { display: inline-block; }
nav a { display: block; padding: 6px 12px; text-decoration: none; }
```

In Sass, you write the child rules *inside* the parent rule — much cleaner:

```scss
/* Sass — nested selectors */
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li {
    display: inline-block;
  }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

**Expected CSS Output (after transpiling):**
```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

Sass automatically prepends the parent selector `nav` to each nested rule. The output is identical to the plain CSS version — but the Sass source is far easier to read and maintain.

> 🤔 **Thinking prompt:** Notice how the Sass version shows the structure clearly — you can immediately tell that `ul`, `li`, and `a` are all *inside* the `nav`. Does this visual nesting make the code easier to understand compared to the flat CSS version?

### Another Nesting Example: A Card Component

```scss
.card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 20px;

  h2 {
    font-size: 22px;
    color: #333;
  }

  p {
    font-size: 16px;
    line-height: 1.6;
  }

  .card-footer {
    border-top: 1px solid #eee;
    padding-top: 10px;
    font-size: 12px;
    color: #999;
  }
}
```

**Expected CSS Output:**
```css
.card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 20px;
}

.card h2 {
  font-size: 22px;
  color: #333;
}

.card p {
  font-size: 16px;
  line-height: 1.6;
}

.card .card-footer {
  border-top: 1px solid #eee;
  padding-top: 10px;
  font-size: 12px;
  color: #999;
}
```

All the related card styles are grouped together visually. When you need to update the card, you open one block — not search through a giant flat stylesheet.

### Nesting Properties with Shared Prefixes

Many CSS properties share a common prefix: `font-family`, `font-size`, `font-weight` all start with `font-`. Similarly, `text-align`, `text-transform`, `text-overflow` all start with `text-`.

Sass lets you group these with a colon after the prefix:

```scss
.element {
  font: {
    family: Helvetica, sans-serif;
    size: 18px;
    weight: bold;
  }

  text: {
    align: center;
    transform: lowercase;
    overflow: hidden;
  }
}
```

**Expected CSS Output:**
```css
.element {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  font-weight: bold;
  text-align: center;
  text-transform: lowercase;
  text-overflow: hidden;
}
```

> ⚠️ **Common Beginner Mistake:** Nesting too deeply. Nesting more than 3–4 levels deep creates overly specific CSS that is hard to override later and may slow down browser rendering. Keep nesting shallow and purposeful.

**Bad — too deeply nested:**
```scss
/* Avoid this */
.page {
  .content {
    .article {
      .paragraph {
        .link {
          color: blue;  /* creates: .page .content .article .paragraph .link */
        }
      }
    }
  }
}
```

**Better — shallow nesting:**
```scss
.article {
  .link {
    color: blue;
  }
}
```

---

## Section 5 — Sass `@import` and Partials

### The Problem: One Giant File

As your website grows, your CSS file can become thousands of lines long. Finding the rule you need becomes slow and painful. You start mixing button styles with navigation styles with form styles — all jumbled together.

### The Solution: Split Into Multiple Files

Sass lets you break your styles into many small, focused files and then combine them into one final CSS output. This is called **modular CSS** organisation.

The benefit: your team can work on different parts of the styling simultaneously, and you can quickly find any style because it is in a logical, dedicated file.

### The `@import` Directive

The `@import` directive pulls the contents of one Sass file into another.

**Syntax:**
```scss
@import "filename";
```

You do not need to include the `.scss` extension — Sass adds it automatically.

**Example: Importing multiple files into `main.scss`:**
```scss
@import "variables";
@import "colors";
@import "reset";
@import "typography";
@import "buttons";
@import "navigation";
```

> 💡 **Why is this better than CSS `@import`?**
> Regular CSS `@import` makes an extra HTTP request to the server every time it is used — this slows down your page. Sass `@import` is different: it **inlines** the content of the imported file directly into the compiled CSS. No extra requests. Zero performance cost.

### Sass Partials — Files That Are Not Compiled Directly

By default, Sass compiles every `.scss` file into a `.css` file. But if you have a file of variables or mixins that should only be used when imported elsewhere — not compiled on its own — you use a **partial**.

**A partial is a Sass file whose name starts with an underscore `_`.**

This underscore tells Sass: "Do not compile this file directly. It is only meant to be imported."

**Partial naming syntax:**
```
_filename.scss
```

**Example: A partial file called `_colors.scss`:**
```scss
/* _colors.scss — a partial (will NOT be compiled by itself) */

$myPink: #EE82EE;
$myBlue: #4169E1;
$myGreen: #8FBC8F;
```

**Importing the partial into another file:**
```scss
/* main.scss */
@import "colors";   /* Notice: no underscore needed when importing! */

body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: $myBlue;    /* $myBlue is available because we imported _colors.scss */
}
```

**Expected CSS Output from `main.scss`:**
```css
body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: #4169E1;
}
```

### A Realistic Project File Structure

Here is how a professional Sass project might be organised:

```
scss/
│
├── main.scss             ← the master file (imports everything)
│
├── _variables.scss       ← colours, fonts, sizes
├── _reset.scss           ← CSS reset/normalise
├── _typography.scss      ← headings, body text, links
├── _buttons.scss         ← button styles
├── _navigation.scss      ← nav bar styles
├── _forms.scss           ← input, textarea, select styles
└── _footer.scss          ← footer styles
```

`main.scss` would look like:
```scss
@import "variables";
@import "reset";
@import "typography";
@import "buttons";
@import "navigation";
@import "forms";
@import "footer";
```

Everything compiles into a single `main.css` file.

> 💡 This modular approach is used by every professional web framework including Bootstrap, Foundation, and Material UI — all are built on exactly this pattern.

### Real-World Example: Reset File + Main File

**`_reset.scss` (partial):**
```scss
html,
body,
ul,
ol {
  margin: 0;
  padding: 0;
}
```

**`standard.scss` (main file — imports the reset):**
```scss
@import "reset";

body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: red;
}
```

**Expected CSS Output from `standard.scss`:**
```css
html, body, ul, ol {
  margin: 0;
  padding: 0;
}

body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: red;
}
```

The reset styles are blended in automatically — clean and seamless.

---

## Section 6 — Sass `@mixin` and `@include`

### What is a Mixin?

A **mixin** is a reusable block of CSS rules that you can include in any selector. Think of it like a recipe that you write once and cook many times.

**The problem without mixins:**
```css
/* You write the same styles again and again */
.warning-box {
  color: red;
  font-size: 25px;
  font-weight: bold;
  border: 1px solid blue;
}

.alert-box {
  color: red;
  font-size: 25px;
  font-weight: bold;
  border: 1px solid blue;
  /* ...plus some unique styles */
}
```

This is code duplication. Every time the design changes, you must update every copy.

**The solution with a mixin:**
Write the shared styles once in a mixin, then include it wherever needed.

### Defining a Mixin

Use `@mixin` followed by a name:

```scss
@mixin important-text {
  color: red;
  font-size: 25px;
  font-weight: bold;
  border: 1px solid blue;
}
```

- `@mixin` — the keyword that creates a mixin
- `important-text` — the name you choose (hyphens and underscores are treated the same)
- `{ ... }` — the block of CSS properties the mixin contains

### Using a Mixin with `@include`

Use `@include` followed by the mixin name inside any selector:

```scss
.danger {
  @include important-text;
  background-color: green;
}
```

**Expected CSS Output:**
```css
.danger {
  color: red;
  font-size: 25px;
  font-weight: bold;
  border: 1px solid blue;
  background-color: green;
}
```

Sass copies all the mixin's properties into `.danger` — and then adds the unique `background-color` on top.

> 🤔 **Thinking prompt:** Imagine you had 10 different selectors all including `@include important-text`. If you need to change `font-size: 25px` to `font-size: 20px`, you only change it once — in the mixin. All 10 selectors update automatically.

### A Mixin Can Include Other Mixins

Mixins can be composed together:

```scss
@mixin special-text {
  @include important-text;    /* includes another mixin */
  @include link;
  @include special-border;
}
```

This lets you build layers of reusable style systems.

### Passing Variables (Arguments) into a Mixin

This is where mixins become truly powerful. You can make a mixin flexible by passing different values into it — like function arguments in programming.

**Defining a mixin with parameters:**
```scss
/* Define mixin with two arguments: $color and $width */
@mixin bordered($color, $width) {
  border: $width solid $color;
}
```

- `$color` and `$width` — these are parameters (placeholders)
- When you include the mixin, you provide actual values

**Using the mixin with different arguments:**
```scss
.myArticle {
  @include bordered(blue, 1px);   /* border: 1px solid blue */
}

.myNotes {
  @include bordered(red, 2px);    /* border: 2px solid red */
}
```

**Expected CSS Output:**
```css
.myArticle {
  border: 1px solid blue;
}

.myNotes {
  border: 2px solid red;
}
```

One mixin, two completely different borders — with different colours and widths.

### Default Values for Mixin Arguments

You can set default values for parameters so you don't always have to provide them:

```scss
@mixin bordered($color: blue, $width: 1px) {
  border: $width solid $color;
}

/* Using with default values — only change what you need */
.myTips {
  @include bordered($color: orange);
  /* $width defaults to 1px, only $color is changed */
}
```

**Expected CSS Output:**
```css
.myTips {
  border: 1px solid orange;
}
```

### Real-World Use: Vendor Prefixes

In web development, some CSS properties need **vendor prefixes** — special versions for different browsers. Writing them manually is tedious and error-prone. A mixin solves this beautifully:

```scss
@mixin transform($property) {
  -webkit-transform: $property;   /* for older Safari/Chrome */
  -ms-transform: $property;       /* for older IE */
  transform: $property;           /* the standard version */
}

/* Using the mixin */
.myBox {
  @include transform(rotate(20deg));
}

.myCircle {
  @include transform(scale(1.5));
}
```

**Expected CSS Output for `.myBox`:**
```css
.myBox {
  -webkit-transform: rotate(20deg);
  -ms-transform: rotate(20deg);
  transform: rotate(20deg);
}
```

You write one line in Sass, and three lines appear in the CSS. Changing the property in the mixin updates all three prefixes everywhere it is used.

---

## Section 7 — Sass `@extend` and Inheritance

### What is `@extend`?

The `@extend` directive lets one selector **inherit** (copy) all the CSS properties from another selector.

**The real-world analogy:** Imagine you have a blueprint for a basic chair (four legs, a seat, a back). A "dining chair" and an "office chair" are both chairs — they share the blueprint. But an office chair *extends* the basic chair with wheels and height adjustment.

In Sass: the basic chair is your base class. The dining and office chairs extend it.

### When Should You Use `@extend`?

Use `@extend` when you have elements that are **almost identical** but differ in a few specific details. Common examples:

- Different types of buttons (primary, danger, success) that share the same shape
- Different alert types (info, warning, error) that share the same layout
- Different card variants that share the same border and padding

### Basic `@extend` Example

```scss
/* Base button style — shared by all buttons */
.button-basic {
  border: none;
  padding: 15px 30px;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
}

/* "Report" button inherits all of .button-basic, plus has its own colour */
.button-report {
  @extend .button-basic;
  background-color: red;
}

/* "Submit" button inherits all of .button-basic, plus its own colours */
.button-submit {
  @extend .button-basic;
  background-color: green;
  color: white;
}
```

**Expected CSS Output:**
```css
/* Sass groups all extended selectors together */
.button-basic, .button-report, .button-submit {
  border: none;
  padding: 15px 30px;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
}

.button-report {
  background-color: red;
}

.button-submit {
  background-color: green;
  color: white;
}
```

Notice how Sass is smart about this: instead of copying the base styles into each selector (which would repeat them), it adds both `.button-report` and `.button-submit` to the `.button-basic` selector group. This produces the most efficient, minimal CSS possible.

### Practical `@extend` Example: Alert Messages

```scss
.alert {
  padding: 15px;
  border-radius: 4px;
  font-size: 14px;
  margin-bottom: 20px;
}

.alert-success {
  @extend .alert;
  background-color: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
}

.alert-warning {
  @extend .alert;
  background-color: #fff3cd;
  color: #856404;
  border: 1px solid #ffeeba;
}

.alert-danger {
  @extend .alert;
  background-color: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
}
```

**Expected CSS Output:**
```css
.alert, .alert-success, .alert-warning, .alert-danger {
  padding: 15px;
  border-radius: 4px;
  font-size: 14px;
  margin-bottom: 20px;
}

.alert-success {
  background-color: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
}

.alert-warning {
  background-color: #fff3cd;
  color: #856404;
  border: 1px solid #ffeeba;
}

.alert-danger {
  background-color: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
}
```

**In your HTML, you only need one class per element:**
```html
<div class="alert-success">Saved successfully!</div>
<div class="alert-warning">Low disk space.</div>
<div class="alert-danger">Error: invalid input.</div>
```

No need for: `<div class="alert alert-success">` — the `@extend` handles the inheritance automatically.

> 💡 The `@extend` directive helps keep your Sass code **DRY** — Don't Repeat Yourself.

### `@extend` vs. `@mixin` — When to Use Which?

This is a common point of confusion. Here is a simple guide:

| Situation | Use |
|---|---|
| Sharing styles that are always *identical* between elements | `@extend` |
| Sharing styles that need *different values* in different places | `@mixin` with arguments |
| Adding vendor prefixes | `@mixin` |
| Creating button/alert variants | `@extend` |
| Creating flexible utility functions | `@mixin` |

**`@extend` keeps your CSS output small** by grouping selectors. **`@mixin` copies code** into each selector that includes it (which can increase output size but gives more flexibility).

---

## Section 8 — Guided Practice Exercises

### Exercise 1: Brand Variables

**Objective:** Practice creating and using Sass variables.

**Scenario:** You are building the stylesheet for "TechStart Lagos" — a tech hub. Their brand colours are coral (`#FF6B6B`), dark navy (`#1A1A2E`), and white (`#FFFFFF`). The body font is `'Segoe UI', sans-serif`, body text size is `16px`, and heading text size is `28px`.

**Steps:**
1. Declare 5 variables: two colours, one font, two font sizes.
2. Create a `body` rule using the font and text size variables.
3. Create an `.hero` rule with a background colour and white text.
4. Create an `h1` rule with the large font size.

**Your Sass (try writing it first):**

```scss
/* Step 1 — Declare variables */
$brand-coral: #FF6B6B;
$brand-navy: #1A1A2E;
$brand-white: #FFFFFF;
$body-font: 'Segoe UI', sans-serif;
$body-size: 16px;
$heading-size: 28px;

/* Step 2 — Body */
body {
  font-family: $body-font;
  font-size: $body-size;
  background-color: $brand-white;
  color: $brand-navy;
}

/* Step 3 — Hero section */
.hero {
  background-color: $brand-navy;
  color: $brand-white;
  padding: 60px 40px;
}

/* Step 4 — Heading */
h1 {
  font-size: $heading-size;
  color: $brand-coral;
}
```

**Expected CSS Output:**
```css
body {
  font-family: 'Segoe UI', sans-serif;
  font-size: 16px;
  background-color: #FFFFFF;
  color: #1A1A2E;
}

.hero {
  background-color: #1A1A2E;
  color: #FFFFFF;
  padding: 60px 40px;
}

h1 {
  font-size: 28px;
  color: #FF6B6B;
}
```

**Self-check questions:**
- What is the value of `$brand-coral`?
- If the design team changes the navy colour to `#0D0D1A`, how many lines do you change?
- What is the difference between a Sass variable and a CSS custom property (`--var`)?

---

### Exercise 2: Nested Navigation

**Objective:** Practice Sass nesting.

**Scenario:** Build the CSS for a navigation bar for a news website.

```scss
.site-nav {
  background-color: #222;
  padding: 0 20px;

  ul {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
  }

  li {
    display: inline-block;
  }

  a {
    display: block;
    color: white;
    padding: 14px 18px;
    text-decoration: none;
    font-size: 15px;
  }

  a:hover {
    background-color: #444;
    color: #ff6b6b;
  }
}
```

**Expected CSS Output:**
```css
.site-nav {
  background-color: #222;
  padding: 0 20px;
}

.site-nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
}

.site-nav li {
  display: inline-block;
}

.site-nav a {
  display: block;
  color: white;
  padding: 14px 18px;
  text-decoration: none;
  font-size: 15px;
}

.site-nav a:hover {
  background-color: #444;
  color: #ff6b6b;
}
```

**Self-check:** The `a:hover` rule nested inside `.site-nav` outputs as `.site-nav a:hover` — can you see how the nesting hierarchy maps to the selector hierarchy?

---

### Exercise 3: Mixin for Flex Containers

**Objective:** Practice creating and using a mixin with arguments.

**Scenario:** Many sections of your website use flexbox. Create a mixin that sets up flex layout with customisable direction and justification.

```scss
/* Define the mixin */
@mixin flex-layout($direction: row, $justify: flex-start, $align: stretch) {
  display: flex;
  flex-direction: $direction;
  justify-content: $justify;
  align-items: $align;
}

/* Use the mixin */
.hero-section {
  @include flex-layout(row, center, center);
  height: 400px;
  background-color: #f5f5f5;
}

.sidebar-layout {
  @include flex-layout(row, space-between, flex-start);
  gap: 20px;
}

.card-stack {
  @include flex-layout(column, flex-start, center);
  padding: 20px;
}
```

**Expected CSS Output:**
```css
.hero-section {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  height: 400px;
  background-color: #f5f5f5;
}

.sidebar-layout {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: flex-start;
  gap: 20px;
}

.card-stack {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  padding: 20px;
}
```

---

### Exercise 4: Extend for Button Variants

**Objective:** Practice `@extend` for shared base styles.

```scss
/* Base button */
.btn {
  display: inline-block;
  padding: 10px 24px;
  border: none;
  border-radius: 6px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: opacity 0.2s;
}

.btn:hover {
  opacity: 0.85;
}

/* Variant buttons */
.btn-primary {
  @extend .btn;
  background-color: #007bff;
  color: white;
}

.btn-success {
  @extend .btn;
  background-color: #28a745;
  color: white;
}

.btn-danger {
  @extend .btn;
  background-color: #dc3545;
  color: white;
}
```

**Expected CSS Output:**
```css
.btn, .btn-primary, .btn-success, .btn-danger {
  display: inline-block;
  padding: 10px 24px;
  border: none;
  border-radius: 6px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: opacity 0.2s;
}

.btn:hover, .btn-primary:hover, .btn-success:hover, .btn-danger:hover {
  opacity: 0.85;
}

.btn-primary {
  background-color: #007bff;
  color: white;
}

.btn-success {
  background-color: #28a745;
  color: white;
}

.btn-danger {
  background-color: #dc3545;
  color: white;
}
```

Notice how the `:hover` style is automatically extended to all variant classes too — that is `@extend` being smart about related selectors.

---

## Section 9 — Mini-Project: A Complete Website Stylesheet

### Project Overview

You will build a complete, production-quality Sass stylesheet for a fictional company called **GreenPath — Sustainable Living Blog**. The stylesheet will use all five Sass features you have learned: variables, nesting, `@import`, mixins, and `@extend`.

### Stage 1: Setup — File Structure and Variables

Create the following files:

```
scss/
├── main.scss           ← imports everything
├── _variables.scss     ← all design tokens
├── _reset.scss         ← base reset
├── _layout.scss        ← page structure
├── _components.scss    ← buttons, cards, alerts
└── _navigation.scss    ← site navigation
```

**`_variables.scss`:**
```scss
/* GREENPATH — Design Tokens */

/* Colours */
$green-dark:    #2d6a4f;
$green-mid:     #52b788;
$green-light:   #d8f3dc;
$accent:        #f77f00;
$text-dark:     #1b1b1b;
$text-muted:    #6c757d;
$white:         #ffffff;

/* Typography */
$font-body:     'Georgia', serif;
$font-heading:  'Helvetica Neue', Arial, sans-serif;
$font-size-sm:  14px;
$font-size-md:  16px;
$font-size-lg:  20px;
$font-size-xl:  32px;

/* Spacing */
$spacing-sm:    8px;
$spacing-md:    20px;
$spacing-lg:    40px;
$spacing-xl:    80px;

/* Layout */
$container-width: 1100px;
$border-radius:   8px;
```

### Stage 2: Reset and Base Layout

**`_reset.scss`:**
```scss
/* Box model reset */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: $font-body;
  font-size: $font-size-md;
  color: $text-dark;
  background-color: $white;
  line-height: 1.7;
}

img {
  max-width: 100%;
  display: block;
}

a {
  color: $green-dark;
  text-decoration: none;

  &:hover {
    color: $accent;
    text-decoration: underline;
  }
}
```

**`_layout.scss`:**
```scss
/* Layout containers and wrappers */
.container {
  max-width: $container-width;
  margin: 0 auto;
  padding: 0 $spacing-md;
}

.section {
  padding: $spacing-xl 0;
}

.section-title {
  font-family: $font-heading;
  font-size: $font-size-xl;
  color: $green-dark;
  margin-bottom: $spacing-md;
}
```

### Stage 3: Mixins for Reusable Patterns

Add these to the top of `_components.scss` or a dedicated `_mixins.scss`:

```scss
/* Flexbox layout helper */
@mixin flex-center {
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Box shadow levels */
@mixin shadow($level: 1) {
  @if $level == 1 {
    box-shadow: 0 1px 4px rgba(0, 0, 0, 0.1);
  } @else if $level == 2 {
    box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
  } @else {
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
  }
}

/* Card base pattern */
@mixin card-base {
  background-color: $white;
  border-radius: $border-radius;
  padding: $spacing-md;
  @include shadow(1);
}
```

### Stage 4: Components

**`_components.scss`:**
```scss
/* === BUTTONS === */

.btn {
  display: inline-block;
  padding: 12px 28px;
  border: none;
  border-radius: $border-radius;
  font-family: $font-heading;
  font-size: $font-size-sm;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.25s ease;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.btn-primary {
  @extend .btn;
  background-color: $green-dark;
  color: $white;

  &:hover {
    background-color: darken($green-dark, 8%);
  }
}

.btn-outline {
  @extend .btn;
  background-color: transparent;
  color: $green-dark;
  border: 2px solid $green-dark;

  &:hover {
    background-color: $green-light;
  }
}

.btn-accent {
  @extend .btn;
  background-color: $accent;
  color: $white;

  &:hover {
    background-color: darken($accent, 8%);
  }
}

/* === CARDS === */

.card {
  @include card-base;
  overflow: hidden;

  .card-image {
    margin: -$spacing-md;
    margin-bottom: $spacing-md;

    img {
      width: 100%;
      height: 220px;
      object-fit: cover;
    }
  }

  .card-category {
    font-size: $font-size-sm;
    color: $green-mid;
    text-transform: uppercase;
    font-weight: 700;
    letter-spacing: 1px;
    margin-bottom: $spacing-sm;
  }

  .card-title {
    font-family: $font-heading;
    font-size: $font-size-lg;
    color: $text-dark;
    margin-bottom: $spacing-sm;
    line-height: 1.3;
  }

  .card-excerpt {
    color: $text-muted;
    font-size: $font-size-sm;
    margin-bottom: $spacing-md;
  }
}

/* === ALERTS === */

.alert {
  padding: $spacing-md;
  border-radius: $border-radius;
  font-size: $font-size-sm;
  margin-bottom: $spacing-md;
  border-left: 4px solid transparent;
}

.alert-info {
  @extend .alert;
  background-color: $green-light;
  color: $green-dark;
  border-left-color: $green-mid;
}

.alert-warning {
  @extend .alert;
  background-color: #fff3cd;
  color: #856404;
  border-left-color: #ffc107;
}
```

### Stage 5: Navigation

**`_navigation.scss`:**
```scss
.site-header {
  background-color: $white;
  border-bottom: 2px solid $green-light;
  position: sticky;
  top: 0;
  z-index: 100;
  @include shadow(1);

  .nav-inner {
    max-width: $container-width;
    margin: 0 auto;
    padding: 0 $spacing-md;
    @include flex-center;
    justify-content: space-between;
    height: 70px;
  }

  .nav-logo {
    font-family: $font-heading;
    font-size: $font-size-lg;
    font-weight: 900;
    color: $green-dark;

    span {
      color: $accent;
    }
  }

  .nav-links {
    list-style: none;
    display: flex;
    gap: $spacing-md;

    a {
      font-family: $font-heading;
      font-size: $font-size-sm;
      font-weight: 600;
      color: $text-dark;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      padding: 8px 0;
      border-bottom: 2px solid transparent;
      transition: border-color 0.2s;

      &:hover {
        color: $green-dark;
        border-bottom-color: $green-mid;
        text-decoration: none;
      }
    }
  }
}
```

### Stage 6: Master Import File

**`main.scss`:**
```scss
/* GreenPath — Main Stylesheet */
/* Import order matters: variables must come first */

@import "variables";
@import "reset";
@import "layout";
@import "components";
@import "navigation";
```

**Compile with:**
```bash
sass main.scss main.css
```

### Milestone Reflection

After completing the project, ask yourself:

1. If the client asks to change the primary green to `#3a7d5f`, how many files do you update? (Answer: Just `_variables.scss` — change `$green-dark`.)
2. How many times is the `.btn` base style written in the final CSS? (It appears once, shared by all three button variants.)
3. What would happen if instead of `@extend`, you had used `@mixin` for the button styles? (Each button would get its own copy of the base styles — more repetition in the output.)

---

## Section 10 — Common Beginner Mistakes

### Mistake 1: Forgetting the `$` When Using a Variable

```scss
/* WRONG */
$brand-color: #336699;

.button {
  background-color: brand-color;  /* CSS property, not a variable — won't work! */
}

/* CORRECT */
.button {
  background-color: $brand-color;  /* add the $ */
}
```

### Mistake 2: Defining a Variable After Using It

```scss
/* WRONG — variable used before declaration */
.header {
  background-color: $primary;
}

$primary: navy;   /* Too late — Sass reads top to bottom */

/* CORRECT — declare first, use after */
$primary: navy;

.header {
  background-color: $primary;
}
```

### Mistake 3: Over-Nesting

```scss
/* WRONG — 5 levels deep creates .page .wrapper .content .article .text */
.page {
  .wrapper {
    .content {
      .article {
        .text { color: black; }
      }
    }
  }
}

/* CORRECT — shallow and purposeful */
.article {
  .text { color: black; }
}
```

### Mistake 4: Importing With the Underscore or `.scss` Extension

```scss
/* WRONG */
@import "_colors.scss";     /* do not include underscore or extension */
@import "_colors";          /* still wrong — no underscore needed */

/* CORRECT */
@import "colors";           /* Sass handles the underscore and extension */
```

### Mistake 5: Using `@extend` on Complex Selectors

```scss
/* WRONG — cannot extend a nested selector from outside */
.parent .child {
  color: red;
}

.other {
  @extend .parent .child;  /* this may cause unexpected results */
}

/* BETTER — extend simple, standalone class selectors */
.base-style {
  color: red;
}

.other {
  @extend .base-style;
}
```

### Mistake 6: Mixin Without `@include`

```scss
/* WRONG — calling a mixin without @include */
.box {
  important-text;   /* This does nothing — just looks like an error */
}

/* CORRECT */
.box {
  @include important-text;
}
```

---

## Section 11 — Reflection Questions

Take a moment to think through these questions to solidify your understanding:

1. In your own words, explain the difference between a Sass **variable** and a **mixin**. When would you use each one?

2. You have a `.card` component that has 4 variations: `.card-featured`, `.card-minimal`, `.card-dark`, `.card-highlighted`. They all share the same padding, border-radius, and box-shadow, but have different backgrounds and fonts. Which Sass feature would you use for the shared styles, and why?

3. A teammate added `$font-size: 16px;` inside the `.hero` selector, and now the global font size variable is not working elsewhere. What went wrong, and how would you fix it using what you learned about scope and `!global`?

4. Your project has grown to 8 Sass files. You notice that when you add a new mixin to `_mixins.scss`, it is not available in `_navigation.scss` even though both are imported into `main.scss`. What could be causing this, and what is the fix? (Hint: think about import order.)

5. When should you choose `@extend` over `@mixin`? Give one concrete real-world example of each.

---

## Section 12 — Completion Checklist

Go through this checklist to confirm you have mastered the lesson:

- [ ] I can explain what Sass is and why it is useful compared to plain CSS
- [ ] I understand what "transpiling" means and can describe the Sass workflow
- [ ] I know how to install Sass and compile a `.scss` file to `.css`
- [ ] I can declare and use Sass variables with the `$` symbol
- [ ] I understand variable scope and know what `!global` does
- [ ] I can write nested CSS rules in Sass and explain what output they produce
- [ ] I know the risk of over-nesting and can write clean, shallow nesting
- [ ] I understand nested properties (like `font: { family: ... }`)
- [ ] I can use `@import` to combine multiple Sass files
- [ ] I understand what a **partial** is and why its filename starts with `_`
- [ ] I can define a `@mixin` with and without arguments
- [ ] I can use `@include` to apply a mixin to a selector
- [ ] I can set default values for mixin arguments
- [ ] I can use `@extend` to share styles between related selectors
- [ ] I understand the difference between `@extend` and `@mixin`
- [ ] I have completed all four guided exercises
- [ ] I have completed the GreenPath mini-project

---

## Lesson Summary

Congratulations — you have completed the full Sass lesson! Here is what you now know:

**Sass** is a CSS pre-processor that adds programming features to CSS. It is compiled (transpiled) to plain CSS before the browser reads it. Sass files use the `.scss` extension.

**Variables** (`$name: value`) let you store design values like colours, fonts, and sizes once and reuse them everywhere. Changing one variable updates every place it is used.

**Nesting** lets you write child selectors inside parent selectors, mirroring your HTML structure and making your code more readable and organised.

**`@import` and Partials** let you split your stylesheet into many small, focused files. Files starting with `_` are partials (not compiled directly). This enables modular, maintainable codebases.

**`@mixin` and `@include`** let you create reusable blocks of CSS code — with optional arguments — that you can include anywhere. They are ideal for patterns that need to vary slightly in different contexts (like borders with different colours, or vendor prefix groups).

**`@extend`** lets one selector inherit all the properties of another, perfect for button variants, alert types, and any situation where elements are almost identical but differ in a few details. It produces clean, deduplicated CSS output.

Together, these five features make Sass a tool used in virtually every professional front-end project in the world — from corporate websites to government platforms to popular open-source UI frameworks. You now have the foundation to use them all.

---

*Sources: W3Schools Sass Tutorial — https://www.w3schools.com/sass/*
