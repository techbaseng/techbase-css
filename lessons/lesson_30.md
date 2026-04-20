---
render_with_liquid: false
title: "CSS Pseudo-elements — Styling Parts of Elements Without Changing Your HTML"
nav_order: 30
---

# Lesson 30 — CSS Pseudo-elements: Styling Parts of Elements Without Changing Your HTML

---

## Lesson Introduction

Imagine you are a newspaper editor. You want the very first letter of every article to be huge, bold, and decorative — like the letter "T" in old books that takes up four lines. You could wrap that letter in a `<span>` tag manually in every article. But what if you have hundreds of articles? There must be a smarter way.

That smarter way is **CSS pseudo-elements**.

A pseudo-element lets you target and style a *specific part* of an element — the first letter, the first line, virtual content injected before or after the element, list markers, or highlighted selected text — all without touching your HTML.

In this lesson you will learn:

- What a pseudo-element is and why it is different from a pseudo-class
- The `::` double-colon notation and why it matters
- All major pseudo-elements: `::first-letter`, `::first-line`, `::before`, `::after`, `::marker`, `::selection`
- The powerful `content` property and all its values
- How to combine pseudo-elements with other selectors
- Real-world professional use cases
- A complete mini-project: a styled article page that uses pseudo-elements throughout

---

## Prerequisite Concepts

Before continuing, make sure you understand these ideas. Short explanations are provided.

### What Is a CSS Selector?

A selector is the part of a CSS rule that tells the browser *which* HTML element to style.

```css
p {              /* ← this is the selector — targets all <p> elements */
  color: blue;
}
```

### What Is a CSS Property and Value?

Inside the curly braces `{}`, you write property-value pairs:

```css
p {
  color: blue;       /* property: color, value: blue */
  font-size: 18px;   /* property: font-size, value: 18px */
}
```

### What Is a Pseudo-class? (Brief Reminder)

A pseudo-class targets an element in a specific **state**. It uses a single colon `:`.

```css
a:hover {        /* Styles a link ONLY when the mouse hovers over it */
  color: red;
}
```

### What Is a Pseudo-element? (Preview)

A pseudo-element targets a specific **part** of an element — not the whole element, but a *piece* of it. It uses a **double colon** `::`.

```css
p::first-letter { /* Styles ONLY the very first letter of a paragraph */
  font-size: 3em;
  color: crimson;
}
```

The difference in a nutshell:
- Pseudo-class = targets an element in a *state* (`:hover`, `:focus`, `:nth-child`)
- Pseudo-element = targets a *part* of an element (`::first-letter`, `::before`, `::after`)

---

## Part 1 — What Is a Pseudo-element?

### The Big Idea

Every HTML element renders content on screen. Most of the time, that content is exactly what you wrote in your HTML file. But sometimes you want to:

- Style just the first letter of a paragraph differently
- Style just the first visible line of text
- Insert a decorative icon or label *before* some text — without adding HTML
- Insert extra text or a symbol *after* a link
- Change how a bullet point looks in a list
- Change the background colour when a user highlights text

All of these are jobs for pseudo-elements. They are like invisible "virtual" elements that CSS creates and attaches to your real elements.

**Real-world analogy:** Think of a pseudo-element like a sticky note you place on a book. The book itself (your HTML) is unchanged — the sticky note is separate from the original content but is visually present and styled.

### The Double-Colon Syntax

All pseudo-elements use a **double colon** `::` before their name:

```css
selector::pseudo-element {
  css-property: value;
}
```

Examples:

```css
p::first-letter   { ... }
p::first-line     { ... }
p::before         { ... }
p::after          { ... }
li::marker        { ... }
::selection       { ... }
```

> **Historical note:** In CSS1 and CSS2, a single colon `:` was used for both pseudo-classes and pseudo-elements. In CSS3, the W3C introduced the double colon `::` specifically for pseudo-elements, to clearly distinguish them from pseudo-classes. For backward compatibility, browsers still accept the old single-colon syntax for the four original pseudo-elements (`::first-letter`, `::first-line`, `::before`, `::after`). However, you should always write the modern double-colon notation.

### Quick Reference Table

| Pseudo-element    | What It Targets                                       | Category |
|-------------------|-------------------------------------------------------|----------|
| `::first-letter`  | The very first letter of a block of text              | Text     |
| `::first-line`    | The first visible line of a block of text             | Text     |
| `::before`        | A virtual element inserted *before* the content       | Content  |
| `::after`         | A virtual element inserted *after* the content        | Content  |
| `::marker`        | The bullet or number of a list item                   | Content  |
| `::selection`     | The text highlighted/selected by the user             | Content  |

---

## Part 2 — Text Pseudo-elements

Text pseudo-elements target specific portions of existing text content.

---

### `::first-letter` — Style Just the First Letter

#### What Is It?

`::first-letter` targets the very first letter (or character) of a block-level element's text content. It is most famous for creating **drop caps** — a typographic technique where the first letter of an article is much larger than the rest of the text.

You have seen this in novels, magazines, and newspaper articles. It signals the start of an important section and draws the reader's eye.

#### Why Does This Exist?

Before pseudo-elements, developers had to wrap the first letter in a `<span>` tag manually:

```html
<!-- OLD way — messy, requires editing HTML -->
<p><span class="dropcap">O</span>nce upon a time...</p>
```

With `::first-letter`, no HTML changes are needed:

```css
/* MODERN way — pure CSS, no HTML change needed */
p::first-letter {
  font-size: 3em;
  color: crimson;
}
```

#### Simple Example

```html
<!-- HTML -->
<p>Once upon a time, in a land far away, there lived a young web developer
who knew nothing about CSS pseudo-elements. One day, they discovered the
magic of the double colon and their designs were never the same again.</p>
```

```css
/* CSS */
p::first-letter {
  font-size: 3em;
  color: crimson;
  font-weight: bold;
}
```

**Expected Output:**
```
 ___
|   |
| O |nce upon a time, in a land far away,
|___|there lived a young web developer...
```

The letter "O" renders at three times the normal font size and in crimson red. All other letters render normally.

#### Properties Allowed on `::first-letter`

Not every CSS property works with `::first-letter`. Here are the ones that do:

- Font properties: `font-family`, `font-size`, `font-weight`, `font-style`, `font-variant`, `line-height`
- Colour: `color`
- Background: `background-color`, `background-image`
- Spacing: `margin`, `padding`, `border`
- Layout: `float`, `vertical-align`, `text-decoration`, `text-transform`

> **Important rule:** `::first-letter` only works on **block-level elements** (like `<p>`, `<div>`, `<h1>–<h6>`). It does NOT work on inline elements like `<span>` or `<a>`.

#### Targeting Specific Elements

You can target only certain paragraphs with a class:

```html
<!-- HTML -->
<p class="intro">This paragraph will have a styled first letter.</p>
<p>This paragraph will NOT have a styled first letter.</p>
```

```css
/* CSS */
p.intro::first-letter {
  font-size: 2.5em;
  color: navy;
  font-weight: bold;
  float: left;              /* Float the letter so text wraps around it */
  margin-right: 4px;        /* Space between the large letter and the rest */
  line-height: 0.85;        /* Keeps the large letter vertically aligned */
}
```

**Expected Output:** Only the first `<p>` gets the oversized letter. The second paragraph renders normally.

> 💭 **Think about it:** What happens if the first character is a punctuation mark like `"` or `'`? The pseudo-element includes it along with the first letter. What if there are spaces before the text? Spaces are skipped — it finds the actual first letter.

---

### `::first-line` — Style Just the First Line of Text

#### What Is It?

`::first-line` targets the first rendered line of text inside a block element. This is dynamic — the "first line" changes depending on the screen width, font size, and browser window size.

#### Why Does This Exist?

In printed books and quality editorial design, the opening line of a chapter often receives special treatment: a different font, small-caps, or a slightly different colour. `::first-line` brings this control to the web.

#### Simple Example

```html
<!-- HTML -->
<p>The history of the internet is a story of human ingenuity,
collaboration, and the relentless pursuit of connection. What began
as a military research project in the 1960s grew into the most
significant communication network ever built by humankind.</p>
```

```css
/* CSS */
p::first-line {
  color: darkblue;
  font-variant: small-caps;
  font-weight: bold;
}
```

**Expected Output (in a 500px-wide container):**
```
THE HISTORY OF THE INTERNET IS A STORY OF   ← first line: dark blue, small-caps, bold
human ingenuity, collaboration, and the      ← normal styling from here on
relentless pursuit of connection...
```

Only the first line gets the special styling. Every other line renders with the default paragraph styles.

#### Dynamic First Line

The first line changes as the browser window resizes. If the window narrows, fewer words fit on the first line, so the styled portion shrinks. If the window widens, more words fit, so the styled portion grows. You never need to update your CSS — the browser handles this automatically.

#### Properties Allowed on `::first-line`

Like `::first-letter`, only a subset of CSS properties work:

- Font properties: `font-family`, `font-size`, `font-weight`, `font-style`, `font-variant`, `line-height`
- Colour: `color`
- Background: `background-color`
- Text: `text-decoration`, `text-transform`, `word-spacing`, `letter-spacing`, `vertical-align`

> **Important rule:** `::first-line` only works on **block-level elements**. It does NOT work on inline elements.

#### Second Example — Combining `::first-line` and `::first-letter`

You can use both on the same element simultaneously! CSS applies them independently:

```css
/* CSS */
p::first-line {
  color: #4a90d9;
  font-variant: small-caps;
}

p::first-letter {
  font-size: 4em;
  color: #e74c3c;
  float: left;
  margin-right: 5px;
  line-height: 0.8;
}
```

**Expected Output:** The first letter is large and red (from `::first-letter`). The rest of the first line is blue and in small-caps (from `::first-line`). Lines two and onwards are unstyled.

> 💭 **Think about it:** When both `::first-letter` and `::first-line` target the same letter, which styles win? Because `::first-letter` is *more specific* (it targets a single character inside the first line), `::first-letter` styles take precedence over `::first-line` styles on that one character.

---

## Part 3 — Content Pseudo-elements: `::before` and `::after`

These are the most powerful and widely used pseudo-elements. They let you inject virtual content into the page — decorations, icons, labels, shapes — all using pure CSS, with zero HTML changes.

### Understanding the Mental Model

Think of every HTML element as having three parts:

```
[::before content] [actual HTML content] [::after content]
```

For example, this HTML:

```html
<p>Hello World</p>
```

With `::before` and `::after`, it acts as if it were:

```html
<!-- Not real HTML — just how the browser treats it -->
<p>
  <pseudo-before>★ </pseudo-before>
  Hello World
  <pseudo-after> ★</pseudo-after>
</p>
```

The "pseudo-before" and "pseudo-after" elements exist only in the browser's rendering — they are **not** in the HTML source, not in the DOM (Document Object Model), and cannot be selected with JavaScript like normal elements.

---

### The `content` Property — The Heart of `::before` and `::after`

**This is critical:** `::before` and `::after` pseudo-elements **MUST have a `content` property** to render anything. Without `content`, they are completely invisible — they do not appear at all.

Even if you want an empty pseudo-element (for purely visual/shape purposes), you must write:

```css
.box::before {
  content: "";   /* Empty string — element exists but shows nothing as text */
  /* Then you style it with width, height, background, etc. */
}
```

#### The `content` Property Values

The `content` property accepts several types of values:

---

**1. A Text String**

Inserts literal text. Enclose the text in quotes.

```css
p::before {
  content: "Read this → ";   /* Inserts this text before the paragraph */
  color: crimson;
  font-weight: bold;
}
```

**Expected Output:**

```
Read this → Once upon a time, in a land far away...
```

---

**2. An Empty String `""`**

Inserts nothing visible as text, but the pseudo-element still exists. Used for purely decorative shapes, lines, and overlays.

```css
.card::after {
  content: "";           /* No text */
  display: block;
  width: 100%;
  height: 3px;
  background-color: #4a90d9;  /* Decorative bottom border */
}
```

---

**3. A URL (Image)**

Inserts an image from a URL. The image appears inline.

```css
a::before {
  content: url("icon-link.png");   /* Adds a link icon before every anchor */
}
```

---

**4. `attr()` — Pull a Value from an HTML Attribute**

The `attr()` function reads an attribute from the HTML element and uses its value as the content. This is powerful for tooltips, print stylesheets, and data-driven labels.

```html
<!-- HTML -->
<a href="https://example.com">Visit Example</a>
```

```css
/* CSS — adds the URL in brackets after the link text */
a::after {
  content: " (" attr(href) ")";
  color: gray;
  font-size: 0.8em;
}
```

**Expected Output:**

```
Visit Example (https://example.com)
```

This technique is extremely useful for **print stylesheets** — when someone prints a webpage, they can see the actual URLs of links.

---

**5. `open-quote` and `close-quote`**

Automatically inserts the correct quotation mark characters based on the language and nesting level.

```html
<!-- HTML -->
<p class="quote">The best way to learn is by doing.</p>
```

```css
/* CSS */
p.quote::before {
  content: open-quote;   /* Inserts " */
  font-size: 1.5em;
  color: #888;
}

p.quote::after {
  content: close-quote;  /* Inserts " */
  font-size: 1.5em;
  color: #888;
}
```

**Expected Output:**

```
"The best way to learn is by doing."
```

---

**6. A Counter**

Automatically numbers elements using CSS counters.

```css
body {
  counter-reset: section;   /* Initialise a counter called "section" */
}

h2::before {
  counter-increment: section;            /* Increase the counter by 1 each time */
  content: "Section " counter(section) ": ";  /* Output the number */
  color: #4a90d9;
  font-weight: bold;
}
```

**Expected Output (with three `<h2>` headings):**

```
Section 1: Introduction
Section 2: Core Concepts
Section 3: Practice Exercises
```

---

### `::before` — Inserting Content Before an Element

#### What Is It?

`::before` creates a virtual child element that is placed as the **first child** of the selected element — before all other content inside it.

#### Simple Example — Alert Label

```html
<!-- HTML -->
<p class="warning">Please save your work before closing the browser.</p>
```

```css
/* CSS */
.warning::before {
  content: "⚠ Warning: ";
  color: darkorange;
  font-weight: bold;
}
```

**Expected Output:**

```
⚠ Warning: Please save your work before closing the browser.
```

The "⚠ Warning: " text is injected by CSS — not present in the HTML at all.

#### Second Example — Decorative Shape (Empty Content)

```html
<!-- HTML -->
<h2 class="section-title">Our Services</h2>
```

```css
/* CSS */
.section-title {
  position: relative;
  padding-left: 20px;
}

.section-title::before {
  content: "";              /* Empty — no text */
  position: absolute;
  left: 0;
  top: 4px;
  width: 8px;
  height: 80%;
  background-color: #4a90d9;  /* A blue vertical bar before the heading */
  border-radius: 2px;
}
```

**Expected Output:** A blue vertical bar on the left side of the heading text — a common design pattern on dashboards and content sites.

---

### `::after` — Inserting Content After an Element

#### What Is It?

`::after` creates a virtual child element that is placed as the **last child** of the selected element — after all other content inside it.

#### Simple Example — Required Field Marker

```html
<!-- HTML — a form label -->
<label class="required">Email Address</label>
<input type="email" />
```

```css
/* CSS */
label.required::after {
  content: " *";
  color: red;
  font-weight: bold;
}
```

**Expected Output:**

```
Email Address *     [input box]
```

The red asterisk is generated by CSS. Every `<label>` with class `required` automatically gets the marker without any HTML changes.

#### Second Example — External Link Indicator

A professional design pattern: add an arrow icon after all external links so users know they are leaving the site.

```css
/* CSS */
a[href^="https://"]::after {     /* Targets only links starting with https:// */
  content: " ↗";
  font-size: 0.8em;
  color: #888;
}
```

**Expected Output:**

```
Visit our partner site ↗
Read the documentation ↗
Back to Homepage         ← (internal link — no arrow)
```

#### Third Example — Clearfix (Classic Layout Technique)

One of the most famous uses of `::after` is the **clearfix** technique, which fixes a layout problem with floated elements. You will learn about floats in detail in a later lesson, but here is a preview:

```css
/* CSS — the clearfix */
.clearfix::after {
  content: "";        /* Must be present */
  display: table;     /* Creates a block formatting context */
  clear: both;        /* Clears floated children */
}
```

This pattern is used in millions of websites and frameworks. It works because the empty `::after` element causes the parent container to correctly wrap around all its floated children.

---

### `::before` vs `::after` — Key Differences

| Feature                  | `::before`                          | `::after`                           |
|--------------------------|-------------------------------------|-------------------------------------|
| Position in element      | First child (before real content)   | Last child (after real content)     |
| Stacking (z-order)       | Behind `::after` by default         | On top of `::before` by default     |
| `content` required?      | Yes                                 | Yes                                 |
| Can be positioned?       | Yes (`position: absolute` etc.)     | Yes                                 |
| Visible in DOM inspector?| Yes (as pseudo-elements)            | Yes (as pseudo-elements)            |
| Selectable by JavaScript?| Not directly                        | Not directly                        |

---

## Part 4 — `::marker` — Styling List Bullets and Numbers

### What Is It?

Every list item (`<li>`) has an automatically generated **marker** — the bullet point (•) for unordered lists or the number (1, 2, 3…) for ordered lists. The `::marker` pseudo-element lets you style this marker directly.

Before `::marker` existed, styling list markers required workarounds: hiding the default marker with `list-style: none` and creating fake markers with `::before`. Now you can style the real marker directly.

### Simple Example — Coloured Bullets

```html
<!-- HTML -->
<ul>
  <li>HTML — the skeleton</li>
  <li>CSS — the skin</li>
  <li>JavaScript — the muscles</li>
</ul>
```

```css
/* CSS */
li::marker {
  color: #e74c3c;      /* Red bullet points */
  font-size: 1.3em;    /* Slightly larger bullets */
}
```

**Expected Output:**

```
● HTML — the skeleton
● CSS — the skin
● JavaScript — the muscles
```

The bullet colour and size change without touching the list item text itself.

### Example — Styled Ordered List Numbers

```html
<!-- HTML -->
<ol>
  <li>Plan your project</li>
  <li>Write the HTML structure</li>
  <li>Apply CSS styles</li>
  <li>Test in the browser</li>
</ol>
```

```css
/* CSS */
ol li::marker {
  color: #4a90d9;
  font-weight: bold;
  font-size: 1.1em;
}
```

**Expected Output:**

```
1. Plan your project
2. Write the HTML structure
3. Apply CSS styles
4. Test in the browser
```

The numbers are blue and bold. The list item text remains in the default colour.

### Changing the Marker Symbol with `content`

You can also use the `content` property on `::marker` to completely replace the default bullet or number:

```css
/* CSS */
li::marker {
  content: "✅ ";    /* Replace bullet with a checkmark */
}
```

**Expected Output:**

```
✅  Plan your project
✅  Write the HTML structure
✅  Apply CSS styles
```

### CSS Properties Allowed on `::marker`

Only a limited set of properties work on `::marker`:

- `color`
- `font` properties (`font-family`, `font-size`, `font-weight`, `font-style`)
- `content`
- `unicode-bidi`, `direction`
- Animation and transition properties

You cannot use `margin`, `padding`, `background`, or most layout properties on `::marker`.

---

## Part 5 — `::selection` — Styling Highlighted Text

### What Is It?

When a user clicks and drags to highlight text on a webpage, the browser applies a default blue highlight colour. The `::selection` pseudo-element lets you customise that highlight to match your brand's colour scheme.

### Why Use It?

Brand consistency. Many professional websites customise the selection colour so that even the act of highlighting text feels on-brand. It is a small but memorable detail.

### Simple Example

```css
/* CSS */
::selection {
  background-color: #ffcc00;   /* Yellow highlight */
  color: #000000;              /* Black text */
}
```

**Expected Output:** When a user selects any text on the page, it highlights in yellow with black text instead of the default browser blue.

### Targeting Specific Elements

You can apply `::selection` to specific elements only:

```css
/* CSS */
p::selection {
  background-color: #4a90d9;  /* Blue highlight for paragraphs */
  color: white;
}

h1::selection {
  background-color: #e74c3c;  /* Red highlight for headings */
  color: white;
}
```

### CSS Properties Allowed on `::selection`

Very few properties work on `::selection`:

- `color`
- `background-color` (not `background` shorthand)
- `text-decoration`
- `text-shadow`
- `cursor`
- `outline`

> **Note:** You cannot change `font-size`, `padding`, `margin`, or most other properties via `::selection`.

---

## Part 6 — Combining Pseudo-elements with Other Selectors

Pseudo-elements can be combined with class selectors, element selectors, pseudo-classes, and attribute selectors. This is where they become extremely powerful.

### With a Class Selector

```css
/* Only paragraphs with class="intro" get the styled first letter */
p.intro::first-letter {
  font-size: 2.5em;
  color: #e74c3c;
  float: left;
  margin-right: 4px;
}
```

### With a Pseudo-class (Hover Effect)

You can combine `:hover` with `::after` to create hover-triggered content:

```css
/* A tooltip that appears on hover */
.tooltip-item {
  position: relative;
  cursor: help;
}

.tooltip-item::after {
  content: attr(data-tip);    /* Read from the data-tip HTML attribute */
  position: absolute;
  bottom: 125%;
  left: 50%;
  transform: translateX(-50%);
  background-color: #333;
  color: white;
  padding: 4px 10px;
  border-radius: 4px;
  font-size: 12px;
  white-space: nowrap;
  opacity: 0;               /* Hidden by default */
  pointer-events: none;
}

.tooltip-item:hover::after {
  opacity: 1;               /* Visible on hover */
}
```

```html
<!-- HTML -->
<span class="tooltip-item" data-tip="This is a tooltip!">Hover over me</span>
```

**Expected Output:** The text "Hover over me" appears normally. When hovered, a dark tooltip box appears above it saying "This is a tooltip!"

### With an Attribute Selector

```css
/* Add a PDF icon after links pointing to PDF files */
a[href$=".pdf"]::after {
  content: " 📄";   /* Only links ending in .pdf get the icon */
  font-size: 0.8em;
}
```

```html
<!-- HTML -->
<a href="report.pdf">Download Report</a>   ← Gets the 📄 icon
<a href="homepage.html">Go Home</a>        ← No icon
```

**Expected Output:**

```
Download Report 📄
Go Home
```

---

## Part 7 — Guided Practice Exercises

### Exercise 1 — Drop Cap Paragraph

**Objective:** Apply a classic drop cap effect to the opening paragraph of an article.

**Scenario:** You are designing a digital magazine. The editor wants the opening paragraph of every article to begin with a large, bold drop cap letter in the magazine's brand colour (#8B1A1A — a deep red).

**Steps:**

1. Create an HTML page with a `<div class="article">` container.
2. Inside it, add a `<p class="opening">` and fill it with two or three sentences.
3. Add a second `<p>` after it with regular text.
4. Apply `::first-letter` only to `.opening`, not to the second paragraph.

**Your Code:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    body {
      font-family: Georgia, serif;
      max-width: 600px;
      margin: 40px auto;
      color: #333;
      line-height: 1.7;
    }

    .opening::first-letter {
      font-size: 4.5em;
      color: #8B1A1A;
      font-weight: bold;
      float: left;
      line-height: 0.75;
      margin-right: 6px;
      margin-top: 4px;
      font-family: "Times New Roman", serif;
    }

    p {
      margin-bottom: 16px;
    }
  </style>
</head>
<body>
  <div class="article">
    <p class="opening">
      Nigeria stands at a turning point in its technological history. 
      With a young and growing population hungry for innovation, the next 
      decade promises to reshape Africa's digital landscape in ways never 
      before seen. The question is not whether change will come — it is 
      whether we are ready to lead it.
    </p>
    <p>
      The infrastructure challenges that have long constrained progress 
      are giving way to creative workarounds, from mobile-first platforms 
      to offline-capable applications designed specifically for low-bandwidth 
      environments.
    </p>
  </div>
</body>
</html>
```

**Expected Output:** The first paragraph has a large "N" in deep red, floating left with the text wrapping beside it. The second paragraph renders normally.

**Self-check Questions:**
- What happens if you remove `float: left`?
- Why does the second paragraph NOT get the drop cap?
- What happens if you change `font-size: 4.5em` to `font-size: 1.5em`?

---

### Exercise 2 — Automatic Warning Labels

**Objective:** Use `::before` to automatically label different types of notice boxes.

**Scenario:** You are building a documentation website. Some paragraphs are warnings, some are tips, and some are notes. You want to automatically prepend a label to each based on its class — no manual text writing in the HTML.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    .notice {
      padding: 12px 16px;
      border-radius: 6px;
      margin: 12px 0;
      font-size: 14px;
      line-height: 1.5;
    }

    /* Warning box */
    .warning {
      background-color: #fff3cd;
      border-left: 4px solid #ffc107;
      color: #856404;
    }
    .warning::before {
      content: "⚠ Warning: ";
      font-weight: bold;
    }

    /* Tip box */
    .tip {
      background-color: #d4edda;
      border-left: 4px solid #28a745;
      color: #155724;
    }
    .tip::before {
      content: "💡 Tip: ";
      font-weight: bold;
    }

    /* Note box */
    .note {
      background-color: #d1ecf1;
      border-left: 4px solid #17a2b8;
      color: #0c5460;
    }
    .note::before {
      content: "📝 Note: ";
      font-weight: bold;
    }
  </style>
</head>
<body>

  <div class="notice warning">
    Always back up your database before running migrations.
  </div>

  <div class="notice tip">
    You can use keyboard shortcut Ctrl + Z to undo the last action.
  </div>

  <div class="notice note">
    This feature is only available in browsers that support CSS Grid.
  </div>

</body>
</html>
```

**Expected Output:**

```
⚠ Warning: Always back up your database before running migrations.

💡 Tip: You can use keyboard shortcut Ctrl + Z to undo the last action.

📝 Note: This feature is only available in browsers that support CSS Grid.
```

Each box automatically has its label. The HTML content itself contains no label text — it all comes from `::before`.

**Self-check Questions:**
- What would happen if you removed all the `content` properties?
- Why is `::before` a better choice than `::after` for a label at the START of text?
- How would you add a "Danger" box with a red style? Write the CSS yourself.

---

### Exercise 3 — Styled Navigation List with Custom Bullets

**Objective:** Remove default bullets from a navigation list and use `::marker` to add custom styled markers.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 300px;
      margin: 40px auto;
    }

    h3 {
      color: #4a90d9;
      margin-bottom: 10px;
    }

    ul.nav-list {
      padding-left: 24px;
    }

    ul.nav-list li {
      margin-bottom: 8px;
      font-size: 15px;
      color: #333;
    }

    /* Style the marker with a coloured arrow */
    ul.nav-list li::marker {
      content: "▶ ";
      color: #4a90d9;
      font-size: 0.9em;
    }

    ul.nav-list li:hover::marker {
      content: "▶ ";
      color: #e74c3c;   /* Red arrow on hover */
    }
  </style>
</head>
<body>
  <h3>Table of Contents</h3>
  <ul class="nav-list">
    <li>Introduction to CSS</li>
    <li>Selectors and Specificity</li>
    <li>The Box Model</li>
    <li>Flexbox and Grid</li>
    <li>Animations and Transitions</li>
  </ul>
</body>
</html>
```

**Expected Output:** A list where each item has a blue `▶` arrow as the bullet. On hover, the arrow turns red.

---

### Exercise 4 — Print-Friendly Link URLs

**Objective:** Use `::after` with `attr()` to show actual URLs beside links when the page is printed.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 600px;
      margin: 40px auto;
      line-height: 1.6;
    }

    a {
      color: #4a90d9;
    }

    /* Only in print mode: show the URL after each link */
    @media print {
      a[href]::after {
        content: " [" attr(href) "]";
        font-size: 0.85em;
        color: #555;
        font-style: italic;
      }
    }

    /* For testing on screen: show a preview of the effect */
    .print-preview a::after {
      content: " [" attr(href) "]";
      font-size: 0.85em;
      color: #888;
      font-style: italic;
    }
  </style>
</head>
<body>
  <h2>Useful Resources</h2>
  <div class="print-preview">
    <p>
      Learn more at <a href="https://developer.mozilla.org">MDN Web Docs</a> or
      practice your skills at <a href="https://www.w3schools.com">W3Schools</a>.
      For career advice, visit <a href="https://css-tricks.com">CSS-Tricks</a>.
    </p>
  </div>
  <p><em>(The URL display is normally only visible in print mode, but shown here for the exercise preview.)</em></p>
</body>
</html>
```

**Expected Output (on screen with `.print-preview` class):**

```
Learn more at MDN Web Docs [https://developer.mozilla.org] or practice your
skills at W3Schools [https://www.w3schools.com]. For career advice, visit
CSS-Tricks [https://css-tricks.com].
```

---

## Part 8 — Mini Project: Styled Article Page

### Project Overview

You will build a complete styled article page that uses all six pseudo-elements you have learned. The final result looks like a professional magazine-style article.

**Pseudo-elements used:**
- `::first-letter` — Drop cap on the opening paragraph
- `::first-line` — Special first-line styling on the opening paragraph
- `::before` — Section labels, blockquote decoration, warning notices
- `::after` — Clearfix, external link markers, section dividers
- `::marker` — Custom list bullets
- `::selection` — Brand-coloured text selection

---

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>The Future of African Tech — Magazine Article</title>
  <link rel="stylesheet" href="article.css" />
</head>
<body>

  <article class="magazine-article">

    <header class="article-header">
      <span class="category">Technology</span>
      <h1>The Future of African Technology</h1>
      <p class="byline">By Chidi Okonkwo · April 2026</p>
    </header>

    <section class="article-body">

      <p class="opening-paragraph">
        Africa is no longer waiting for the world to bring technology to its shores.
        The continent is building, inventing, and shipping products that solve
        uniquely African problems with breathtaking creativity. From fintech
        innovations in Lagos to agri-tech breakthroughs in Nairobi, a new
        generation of builders is rewriting the story of African development.
      </p>

      <p>
        The statistics are striking. Mobile money transactions in Sub-Saharan
        Africa reached $700 billion in 2023 — a figure that continues to grow
        at pace. Startup ecosystems from Cape Town to Cairo are attracting
        record levels of funding, while local developer communities are growing
        faster than anywhere else on earth.
      </p>

      <h2>Key Sectors Leading the Charge</h2>

      <p>
        Several industries stand out as particularly ripe for disruption across
        the continent, driven by local necessity and global ambition.
      </p>

      <ul class="article-list">
        <li>Fintech — redefining access to banking and payments</li>
        <li>Agri-tech — transforming smallholder farming with data</li>
        <li>Health-tech — closing gaps in rural healthcare delivery</li>
        <li>EdTech — expanding quality education beyond city centres</li>
        <li>Logistics — solving the last-mile delivery challenge</li>
      </ul>

      <blockquote class="pull-quote">
        The most valuable innovations are the ones that were built by the very
        people experiencing the problem — not imported from outside.
      </blockquote>

      <h2>Challenges Still to Overcome</h2>

      <p>
        Progress is real, but so are the obstacles. Infrastructure gaps,
        regulatory uncertainty, and inconsistent internet connectivity remain
        significant headwinds.
      </p>

      <div class="notice warning">
        Internet penetration in rural Africa still lags urban centres by over 40%
        in many countries, making offline-first design a critical skill for
        African developers.
      </div>

      <p>
        Despite these hurdles, the entrepreneurial energy is undeniable.
        For more data, visit
        <a href="https://africatechreport.org">Africa Tech Report</a> or
        <a href="https://disrupt-africa.com">Disrupt Africa</a>.
      </p>

    </section>

    <footer class="article-footer">
      <p>© 2026 Tech Horizon Magazine. All rights reserved.</p>
    </footer>

  </article>

</body>
</html>
```

---

### Stage 2 — CSS (`article.css`)

```css
/* =============================================
   RESET AND BASE STYLES
   ============================================= */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Georgia, "Times New Roman", serif;
  background-color: #f5f0eb;
  color: #2c2c2c;
  line-height: 1.75;
  padding: 40px 16px;
}

.magazine-article {
  max-width: 680px;
  margin: 0 auto;
  background-color: #ffffff;
  padding: 40px 48px;
  border-radius: 4px;
  box-shadow: 0 2px 20px rgba(0,0,0,0.08);
}

/* =============================================
   ARTICLE HEADER
   ============================================= */
.article-header {
  border-bottom: 2px solid #8B1A1A;
  padding-bottom: 20px;
  margin-bottom: 30px;
}

.category {
  font-size: 11px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: #8B1A1A;
  font-family: Arial, sans-serif;
}

.article-header h1 {
  font-size: 2.2em;
  line-height: 1.2;
  margin: 8px 0;
  color: #1a1a1a;
}

.byline {
  font-size: 13px;
  color: #888;
  font-family: Arial, sans-serif;
}

/* =============================================
   PSEUDO-ELEMENT 1: ::first-letter (Drop Cap)
   ============================================= */
.opening-paragraph::first-letter {
  font-size: 5em;
  color: #8B1A1A;
  float: left;
  line-height: 0.78;
  margin-right: 8px;
  margin-top: 5px;
  font-family: Georgia, serif;
  font-weight: bold;
}

/* =============================================
   PSEUDO-ELEMENT 2: ::first-line (Opening Line Styling)
   ============================================= */
.opening-paragraph::first-line {
  font-variant: small-caps;
  letter-spacing: 1px;
  color: #555;
}

/* =============================================
   CLEARFIX (uses ::after)
   ============================================= */
.opening-paragraph::after {
  content: "";
  display: table;
  clear: both;
}

/* =============================================
   BODY TEXT
   ============================================= */
.article-body p {
  margin-bottom: 20px;
  font-size: 1em;
}

/* =============================================
   HEADINGS WITH ::before DECORATIVE BAR
   ============================================= */
.article-body h2 {
  font-size: 1.35em;
  color: #1a1a1a;
  font-family: Arial, sans-serif;
  font-weight: bold;
  margin: 30px 0 14px 0;
  padding-left: 14px;
  position: relative;
}

/* PSEUDO-ELEMENT 3: ::before — Decorative bar beside headings */
.article-body h2::before {
  content: "";
  position: absolute;
  left: 0;
  top: 2px;
  width: 4px;
  height: 90%;
  background-color: #8B1A1A;
  border-radius: 2px;
}

/* =============================================
   PSEUDO-ELEMENT 4: ::marker — Custom List Bullets
   ============================================= */
.article-list {
  padding-left: 28px;
  margin-bottom: 24px;
}

.article-list li {
  margin-bottom: 8px;
  font-size: 0.97em;
}

.article-list li::marker {
  content: "◆ ";
  color: #8B1A1A;
  font-size: 0.8em;
}

/* =============================================
   PSEUDO-ELEMENT 5: ::before — Blockquote decoration
   ============================================= */
.pull-quote {
  margin: 28px 0;
  padding: 18px 24px 18px 50px;
  background-color: #fdf6f0;
  border-left: 3px solid #8B1A1A;
  font-size: 1.1em;
  font-style: italic;
  color: #444;
  position: relative;
}

.pull-quote::before {
  content: "\201C";        /* Unicode for left double quotation mark " */
  font-size: 5em;
  color: #8B1A1A;
  opacity: 0.25;
  position: absolute;
  top: -10px;
  left: 10px;
  line-height: 1;
  font-family: Georgia, serif;
}

/* =============================================
   PSEUDO-ELEMENT 3 (second use): ::before — Warning Notice
   ============================================= */
.notice.warning {
  background-color: #fff8ec;
  border-left: 4px solid #e67e22;
  padding: 12px 16px;
  border-radius: 0 4px 4px 0;
  margin: 20px 0;
  font-family: Arial, sans-serif;
  font-size: 0.9em;
  color: #7d4e05;
  line-height: 1.5;
}

.notice.warning::before {
  content: "⚠ Important: ";
  font-weight: bold;
  color: #e67e22;
}

/* =============================================
   PSEUDO-ELEMENT 6: ::after — External Link Indicator
   ============================================= */
a {
  color: #8B1A1A;
  text-decoration: underline;
}

a[href^="https://"]::after {
  content: " ↗";
  font-size: 0.75em;
  color: #aaa;
  font-style: normal;
  font-family: Arial, sans-serif;
}

/* =============================================
   PSEUDO-ELEMENT (bonus): ::after — Section Divider
   ============================================= */
.article-body h2::after {
  content: "";
  display: block;
  width: 40px;
  height: 2px;
  background-color: #e0e0e0;
  margin-top: 6px;
}

/* =============================================
   PSEUDO-ELEMENT 7: ::selection — Brand highlight colour
   ============================================= */
::selection {
  background-color: #8B1A1A;
  color: #ffffff;
}

/* =============================================
   ARTICLE FOOTER
   ============================================= */
.article-footer {
  border-top: 1px solid #e0e0e0;
  padding-top: 16px;
  margin-top: 30px;
  font-size: 12px;
  color: #aaa;
  font-family: Arial, sans-serif;
}
```

---

### Stage 3 — Final Output Description

Your finished article page should display:

- A clean magazine-style header with a deep red accent
- The opening paragraph's first letter as a large, floating drop cap in deep red
- The first line of the opening paragraph in small-caps
- Section headings with a thin red vertical bar on the left and a short grey underline
- A custom list with red diamond `◆` markers instead of default bullets
- A blockquote with a large decorative faded `"` quote mark in the background
- A warning notice box with the label auto-prepended by `::before`
- External links with a small `↗` indicator automatically appended by `::after`
- Text selected by the user highlights in deep red with white text

**Reflection Questions:**

1. Count every place in the CSS file where a pseudo-element is used. How many do you find?
2. Which pseudo-element did you use in the most creative or unexpected way?
3. Remove all `content: ""` empty values from `::before` and `::after` elements. What visual changes do you notice?
4. What would break if you removed `position: relative` from `.pull-quote` and `.article-body h2`?
5. The `::first-line` and `::first-letter` both apply to `.opening-paragraph`. What happens to the first letter — does it get `::first-line` styles or `::first-letter` styles? Why?

**Optional Advanced Extensions:**

- Add a `::before` counter to auto-number the `<h2>` headings (hint: use `counter-reset` and `counter-increment`)
- Create a hover tooltip using `data-tip` attribute and `::after` on a term in the article
- Add a print stylesheet using `@media print` that shows link URLs via `::after { content: attr(href) }`

---

## Part 9 — Common Beginner Mistakes

### Mistake 1 — Forgetting the `content` Property on `::before` or `::after`

```css
/* WRONG — nothing will appear */
.badge::before {
  background-color: red;
  width: 10px;
  height: 10px;
  border-radius: 50%;
}
```

```css
/* CORRECT — content must be present, even if empty */
.badge::before {
  content: "";           /* Even an empty string is required */
  display: block;
  background-color: red;
  width: 10px;
  height: 10px;
  border-radius: 50%;
}
```

**Why:** `::before` and `::after` pseudo-elements only render when the `content` property is present and has a value other than `normal` or `none`. Without it, the browser simply does not create the pseudo-element at all.

---

### Mistake 2 — Using a Single Colon Instead of Double Colon

```css
/* OUTDATED — works in browsers but is incorrect modern CSS */
p:first-letter { font-size: 3em; }

/* CORRECT — always use double colon for pseudo-elements */
p::first-letter { font-size: 3em; }
```

**Why:** Single-colon pseudo-elements belong to CSS1/CSS2. The double colon `::` was introduced in CSS3 to clearly separate pseudo-elements from pseudo-classes. Write `::` consistently in all new code.

---

### Mistake 3 — Applying `::first-letter` or `::first-line` to an Inline Element

```css
/* WRONG — span is an inline element */
span::first-letter {
  font-size: 3em;
  color: red;
}
```

```css
/* CORRECT — use a block-level element */
p::first-letter {
  font-size: 3em;
  color: red;
}

/* OR convert the span to block-level */
span {
  display: block;
}
span::first-letter {
  font-size: 3em;
  color: red;
}
```

**Why:** `::first-letter` and `::first-line` only work on block-level elements. If you apply them to inline elements (`<span>`, `<a>`, `<strong>`), they have no effect.

---

### Mistake 4 — Putting Important Content Inside `::before` or `::after`

```css
/* PROBLEMATIC — this text may not be read by screen readers */
.contact-number::after {
  content: "+234 800 TECH HELP";
}
```

```html
<!-- CORRECT — put real, important information in the HTML -->
<p class="contact-number">+234 800 TECH HELP</p>
```

**Why:** Content inserted via the CSS `content` property is not reliably announced by screen readers in all browsers. Important information — phone numbers, addresses, prices, error messages — must be in the actual HTML so it is accessible to everyone. Use `::before` and `::after` for decorative and supplementary content only.

---

### Mistake 5 — Using `::before`/`::after` on Self-Closing (Replaced) Elements

```css
/* WRONG — img is a replaced element; it has no content to precede or follow */
img::before {
  content: "Photo: ";
}

/* ALSO WRONG */
input::before {
  content: "→ ";
}
```

```html
<!-- CORRECT — use a wrapper element -->
<figure class="photo-caption">
  <img src="photo.jpg" alt="City view" />
</figure>
```

```css
.photo-caption::before {
  content: "📷 Photo: ";
  display: block;
  font-size: 0.8em;
  color: #888;
}
```

**Why:** `::before` and `::after` inject content *inside* an element. Self-closing elements like `<img>`, `<input>`, `<br>`, `<hr>` have no inner content — they cannot have `::before` or `::after`. Wrap them in a container element and apply pseudo-elements to that instead.

---

### Mistake 6 — Trying to Style `::marker` with Unsupported Properties

```css
/* WRONG — padding and margin don't work on ::marker */
li::marker {
  padding-left: 10px;
  margin-right: 5px;
  background-color: yellow;
}
```

```css
/* CORRECT — only use supported properties */
li::marker {
  color: navy;
  font-size: 1.2em;
  font-weight: bold;
  content: "→ ";
}
```

**Why:** `::marker` only supports a small subset of CSS properties. Most visual styling properties (background, padding, margin, border) are not in that list. If you need more control over the marker appearance, use `list-style: none` and create a custom bullet with `li::before` instead.

---

## Part 10 — Reflection Questions

Think through each question carefully before moving on:

1. What is the key syntactic difference between a pseudo-class and a pseudo-element? Give one example of each.
2. Why must `::before` and `::after` always have a `content` property?
3. What types of elements can `::first-letter` and `::first-line` be applied to? What types cannot use them?
4. Which value of the `content` property would you use to read a value from an HTML attribute like `data-label`?
5. A designer asks you to add an `✓` checkmark in front of every completed task in a list, without changing the HTML. How would you do it using only CSS?
6. What is the difference between `::before` and `::after` in terms of where their content appears?
7. You want the list markers on your navigation to be blue arrows `→` instead of bullets. Write the CSS rule.
8. Why is it bad practice to put a phone number inside the CSS `content` property?
9. What CSS property and value would you write to make selected text appear with a dark blue background?
10. Explain in plain English what this CSS rule does: `a[href$=".pdf"]::after { content: " (PDF)"; }`

---

## Lesson Completion Checklist

Before moving to the next lesson, confirm you can answer "yes" to every item:

- [ ] I understand what a pseudo-element is and how it differs from a pseudo-class
- [ ] I always write the double-colon `::` notation
- [ ] I can use `::first-letter` to create a drop cap effect
- [ ] I can use `::first-line` to style the first visible line of a paragraph
- [ ] I understand that `::before` and `::after` require the `content` property
- [ ] I can use all `content` values: string, empty, `attr()`, `open-quote`/`close-quote`, counter
- [ ] I know the difference between `::before` (first child) and `::after` (last child)
- [ ] I can style list markers with `::marker`
- [ ] I can customise text selection with `::selection`
- [ ] I know which CSS properties are restricted for `::first-letter`, `::first-line`, `::marker`, and `::selection`
- [ ] I know NOT to put important content in the `content` property
- [ ] I know that `::before`/`::after` do not work on self-closing/replaced elements
- [ ] I completed all four guided practice exercises
- [ ] I completed the magazine article mini-project
- [ ] I can answer the reflection questions above

---

## Lesson Summary

CSS pseudo-elements are one of the most elegant tools in the language. They let you style specific *parts* of existing elements and inject virtual content into the page — all without touching your HTML.

The six pseudo-elements covered in this lesson are:

**Text pseudo-elements** (target parts of existing text):
- `::first-letter` — styles the very first letter; block-level elements only; creates drop caps
- `::first-line` — styles the first visible line; dynamic and responsive to container width

**Content pseudo-elements** (inject or style generated content):
- `::before` — creates a virtual first-child element; must have `content`; cannot be used on replaced elements
- `::after` — creates a virtual last-child element; must have `content`; widely used for clearfix, decorations, external link markers
- `::marker` — styles the bullet or number of a list item; limited CSS property support
- `::selection` — styles the text currently highlighted by the user; accepts only a few properties

The `content` property is the heart of `::before` and `::after`. Its values include:
- A string: `content: "text"` 
- Empty: `content: ""`
- A URL: `content: url("image.png")`
- An attribute: `content: attr(href)` 
- A quote: `content: open-quote` / `content: close-quote`
- A counter: `content: counter(myCounter)`

Always use the double-colon `::` notation. Never put important information in the `content` property. Never use `::before`/`::after` on `<img>`, `<input>`, or other replaced elements.

In the next lesson, you will study **CSS Opacity** — controlling how transparent or opaque elements and their children appear.

---

*Sources: W3Schools CSS Pseudo-elements Tutorial, W3Schools CSS Pseudo-element Text, W3Schools CSS Pseudo-element Content, MDN Web Docs CSS Pseudo-elements, MDN `::before`, MDN `content` property, web.dev Learn CSS Pseudo-elements, CSS-Tricks `content` property, freeCodeCamp CSS Before and After, Manuel Matuzovic — Here's what I didn't know about "content"*
