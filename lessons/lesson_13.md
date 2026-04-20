---
render_with_liquid: false
title: "Lesson 13: CSS Text Styling — Color, Alignment, Decoration, Transformation, Spacing & Shadow"
nav_order: 13
---

# Lesson 13: CSS Text Styling — Color, Alignment, Decoration, Transformation, Spacing & Shadow

---

## Lesson Introduction

Welcome to one of the most exciting lessons in CSS! In this lesson, you will learn how to **style text** — the most fundamental content on any webpage. Everything you read online, every headline, paragraph, label, and button — all of it is text, and CSS gives you enormous power over how that text looks, feels, and behaves.

By the end of this lesson, you will be able to:

- Change the **color** of text in any way you like
- Control how text is **aligned** on a page (left, centre, right, or justified)
- Add **decorations** like underlines, overlines, and line-throughs — and then style those decorations beautifully
- **Transform** text into uppercase, lowercase, or capitalised form automatically
- Fine-tune **spacing** between letters, words, and lines of text
- Add dramatic **text shadows** that bring your text to life

Think of CSS text styling like the controls on a professional word processor — but far more powerful. A graphic designer working on a magazine uses these kinds of controls to make a headline bold and imposing or a caption delicate and light. As a web developer, these are your tools too.

---

## Prerequisite Concepts

Before diving in, let's make sure you are comfortable with two important ideas. If you already know these, feel free to skim quickly.

### What is a CSS Property?

A **CSS property** is an instruction you give to the browser that says: "Hey, display this HTML element in this specific way." Every property has a **name** and a **value**, written like this:

```css
property-name: value;
```

For example:

```css
color: red;
```

This tells the browser: "Make the text colour red."

### What is a CSS Selector?

A **CSS selector** tells the browser *which* HTML element(s) you want to style. For example:

```css
p {
  color: blue;
}
```

This selects every `<p>` (paragraph) element on the page and makes its text blue.

### A Quick Reminder: Where Does CSS Go?

You can write CSS in three places:

1. **External stylesheet** — a separate `.css` file linked to your HTML
2. **Internal style** — inside a `<style>` tag in your `<head>` section
3. **Inline style** — directly on an HTML element using the `style` attribute

For all examples in this lesson, we will use the **internal style** approach so everything is in one place and easy to test:

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      /* CSS goes here */
    </style>
  </head>
  <body>
    <!-- HTML content goes here -->
  </body>
</html>
```

---

## Part 1: CSS Text Color

### What Is It?

The `color` property in CSS controls the **colour of the text** inside an HTML element. It does NOT control the background colour — just the text itself.

Think of it like changing the ink colour in a pen. If you pick a red pen, the words you write are red. If you pick blue, the words are blue.

### Why Does It Exist?

Without text colour control, every webpage would have identical black text on a white background. Text colour lets designers:

- Create visual hierarchy (e.g., red headings stand out from black body text)
- Match brand colours (e.g., a bank might use dark navy text)
- Improve readability (e.g., white text on a dark background)
- Draw attention to important information

### How to Specify a Colour

CSS gives you three main ways to write a colour value:

**1. By name** — use one of CSS's 140+ named colours:

```css
color: red;
color: blue;
color: darkgreen;
color: tomato;
color: cornflowerblue;
```

**2. By HEX code** — a `#` followed by 6 characters (letters A–F and digits 0–9):

```css
color: #ff0000;    /* red */
color: #0000ff;    /* blue */
color: #333333;    /* dark grey */
```

> **Analogy:** A HEX code is like a precise paint mixing formula. `#ff0000` means "maximum red, no green, no blue."

**3. By RGB value** — three numbers from 0 to 255 representing Red, Green, Blue:

```css
color: rgb(255, 0, 0);    /* red */
color: rgb(0, 0, 255);    /* blue */
color: rgb(100, 100, 100); /* medium grey */
```

### Simple Example: Changing Text Colour

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      body {
        color: black;
      }
      h1 {
        color: darkblue;
      }
      h2 {
        color: #e74c3c;
      }
      p {
        color: rgb(60, 60, 60);
      }
    </style>
  </head>
  <body>
    <h1>This heading is dark blue</h1>
    <h2>This heading is red (using HEX)</h2>
    <p>This paragraph is dark grey (using RGB)</p>
  </body>
</html>
```

**Expected Output (visual):**
- The `<h1>` text appears in dark blue
- The `<h2>` text appears in a red-ish colour
- The `<p>` text appears in dark grey

> **Important:** The `color` property set on the `body` selector applies to all text on the page by default. Individual selectors like `h1` or `p` then **override** that default.

### Text Colour AND Background Colour Together

You will often set both text colour and background colour together for readability:

```html
<style>
  .highlight {
    color: white;
    background-color: #2c3e50;
  }
</style>

<p class="highlight">This is white text on a dark background.</p>
```

**Expected Output:** White text sitting on a very dark navy-blue background.

> **Tip:** Always think about **contrast**. Light text on a dark background and dark text on a light background are easiest to read. Never use yellow text on a white background — it will be nearly invisible!

### Thinking Prompt

What happens if you set `color: white` on the body but forget to set a dark background colour? Try it and observe. Why does that cause a problem?

---

## Part 2: CSS Text Alignment

### What Is It?

Text alignment controls **where text sits horizontally** inside its container element. It's the same concept as "Align Left," "Center," "Align Right," and "Justify" in Microsoft Word.

### Why Does It Exist?

Different layouts need different alignment styles:

- Blog article body text → usually left-aligned for readability
- Page headings → often centred for dramatic effect
- Prices or numbers in a table → right-aligned so decimal points line up
- Printed-style body text → sometimes justified so both edges are clean

### The `text-align` Property

The `text-align` property accepts these values:

| Value | What It Does |
|---|---|
| `left` | Aligns text to the left edge (default for most languages) |
| `right` | Aligns text to the right edge |
| `center` | Centres text horizontally |
| `justify` | Stretches text so both left AND right edges are perfectly even |

### Example 1: Basic Alignment

```html
<style>
  .left-text    { text-align: left; }
  .centre-text  { text-align: center; }
  .right-text   { text-align: right; }
</style>

<p class="left-text">This text is aligned to the left side.</p>
<p class="centre-text">This text is centred.</p>
<p class="right-text">This text is aligned to the right side.</p>
```

**Expected Output:**
```
This text is aligned to the left side.
                    This text is centred.
                            This text is aligned to the right side.
```

### Example 2: Justified Text

Justified text is common in newspapers and books. It spaces words out so both the left and right edges form a perfectly straight vertical line.

```html
<style>
  p {
    text-align: justify;
    width: 400px;
  }
</style>

<p>
  The quick brown fox jumps over the lazy dog. The five boxing wizards jump
  quickly. Pack my box with five dozen liquor jugs. How vexingly quick daft
  zebras jump!
</p>
```

**Expected Output:** A paragraph where both the left and right edges are perfectly aligned — like a newspaper column.

> **Beginner Mistake:** Many beginners think `text-align: center` will centre their whole block (like a `<div>`) on the page. It only centres the **text INSIDE** the element. To centre the block itself, you need a different technique like `margin: auto`.

### The `text-align-last` Property

`text-align-last` lets you control how the very **last line** of a paragraph is aligned, separately from the rest. This is especially useful with `justify`:

```html
<style>
  p {
    text-align: justify;
    text-align-last: center;
  }
</style>

<p>
  This is a justified paragraph. All lines except the last one will be
  fully stretched to fill the width. The very last line will be centred.
</p>
```

**Expected Output:** Every full line is justified (stretched edge-to-edge), but the short final line is centred.

### Text Direction with `direction` and `unicode-bidi`

Some languages like Arabic and Hebrew read from right to left (RTL). CSS supports this with the `direction` property:

```css
direction: rtl;  /* right-to-left */
direction: ltr;  /* left-to-right (default) */
```

When you use `direction: rtl` inside an inline element, you should also use `unicode-bidi: bidi-override` to ensure it works correctly:

```html
<style>
  p {
    direction: rtl;
    unicode-bidi: bidi-override;
  }
</style>

<p>This text will appear right-to-left.</p>
```

**Expected Output:** The text appears starting from the right side of the page.

### The `vertical-align` Property

`vertical-align` controls how an element aligns **vertically** relative to surrounding text. It is most commonly used with images and table cells.

Common values: `baseline` (default), `top`, `middle`, `bottom`, `text-top`, `text-bottom`, or a specific pixel/percentage value.

```html
<style>
  img.top    { vertical-align: top; }
  img.middle { vertical-align: middle; }
  img.bottom { vertical-align: bottom; }
</style>

<p>
  Text <img src="icon.png" class="top" alt="icon"> aligned top.
</p>
<p>
  Text <img src="icon.png" class="middle" alt="icon"> aligned middle.
</p>
<p>
  Text <img src="icon.png" class="bottom" alt="icon"> aligned bottom.
</p>
```

---

## Part 3: CSS Text Decoration

### What Is It?

Text decoration refers to **lines added to or around text** — lines running underneath, through the middle, or above the text. The most familiar decoration is the underline you see on hyperlinks.

### Why Does It Exist?

- **Underlines** signal clickable links
- **Line-through** (strikethrough) shows deleted or crossed-out content (e.g., a sale price that's been replaced)
- **Overlines** are used in some mathematical and linguistic notations
- **Removing underlines** from links is common in modern design where links are styled with colour instead

### The `text-decoration-line` Property

`text-decoration-line` adds a line to text. Its values are:

| Value | What It Does |
|---|---|
| `none` | Removes any decoration (even link underlines!) |
| `underline` | Adds a line beneath the text |
| `overline` | Adds a line above the text |
| `line-through` | Adds a line through the middle of the text |

### Example 1: All Four Decoration Lines

```html
<style>
  .no-decor    { text-decoration-line: none; }
  .underline   { text-decoration-line: underline; }
  .overline    { text-decoration-line: overline; }
  .strike      { text-decoration-line: line-through; }
</style>

<p class="no-decor">No decoration at all.</p>
<p class="underline">This text has an underline.</p>
<p class="overline">This text has an overline.</p>
<p class="strike">This text has a line through it.</p>
```

**Expected Output:**
- First line: plain text, no lines
- Second line: text with a line below it
- Third line: text with a line above it
- Fourth line: text with a line crossing through its middle

### Example 2: Combining Two Decorations

You can add more than one line at once:

```html
<style>
  p {
    text-decoration-line: underline overline;
  }
</style>

<p>This text has both an underline and an overline!</p>
```

**Expected Output:** Text with a line both above AND below it.

### Removing the Underline from Links

By default, all `<a>` (anchor/link) tags have an underline. You can remove it:

```html
<style>
  a {
    text-decoration: none;
    color: #e74c3c;
  }
</style>

<a href="#">Click me — no underline, just red text!</a>
```

> **Design Note:** If you remove the underline from links, make sure your links are still visually distinct — use a different colour, bold weight, or hover effect so users know they can click.

---

## Part 4: CSS Text Decoration Styles

### What Is It?

Once you know how to add a decoration line, you can go further and **style that line** itself — changing its colour, thickness, and the pattern of the line (solid, dashed, dotted, wavy, etc.).

Think of this like choosing what kind of pen you use to underline something: a solid red pen, a dashed pencil, a thick marker, or a squiggly highlighter.

### The Key Properties

| Property | What It Controls |
|---|---|
| `text-decoration-color` | The colour of the decoration line |
| `text-decoration-style` | The pattern of the line (solid, double, dotted, dashed, or wavy) |
| `text-decoration-thickness` | How thick the line is |

### `text-decoration-color`

```html
<style>
  .red-line   { text-decoration-line: underline; text-decoration-color: red; }
  .blue-line  { text-decoration-line: underline; text-decoration-color: blue; }
  .green-line { text-decoration-line: underline; text-decoration-color: green; }
</style>

<p class="red-line">Underlined in red.</p>
<p class="blue-line">Underlined in blue.</p>
<p class="green-line">Underlined in green.</p>
```

**Expected Output:** Three paragraphs each with an underline, but the underline colours are different from the text colour.

### `text-decoration-style`

```html
<style>
  .solid   { text-decoration-line: underline; text-decoration-style: solid; }
  .double  { text-decoration-line: underline; text-decoration-style: double; }
  .dotted  { text-decoration-line: underline; text-decoration-style: dotted; }
  .dashed  { text-decoration-line: underline; text-decoration-style: dashed; }
  .wavy    { text-decoration-line: underline; text-decoration-style: wavy; }
</style>

<p class="solid">Solid underline (default).</p>
<p class="double">Double underline (two parallel lines).</p>
<p class="dotted">Dotted underline (. . . . .).</p>
<p class="dashed">Dashed underline (- - - -).</p>
<p class="wavy">Wavy underline (like a spell-check squiggle!).</p>
```

**Expected Output:** Five paragraphs with underlines using five different line styles. The wavy one will look exactly like Microsoft Word's red spell-check squiggle!

### `text-decoration-thickness`

```html
<style>
  .thin   { text-decoration-line: underline; text-decoration-thickness: 1px; }
  .medium { text-decoration-line: underline; text-decoration-thickness: 3px; }
  .thick  { text-decoration-line: underline; text-decoration-thickness: 8px; }
  .auto   { text-decoration-line: underline; text-decoration-thickness: auto; }
</style>

<p class="thin">Thin underline (1px).</p>
<p class="medium">Medium underline (3px).</p>
<p class="thick">Thick underline (8px — very bold!).</p>
<p class="auto">Auto thickness (browser decides).</p>
```

**Expected Output:** Four paragraphs with underlines of increasing thickness.

### The Shorthand: `text-decoration`

Instead of writing three separate properties, you can combine them into one line:

```css
text-decoration: line style color thickness;
```

Example:

```html
<style>
  p {
    text-decoration: underline wavy red 2px;
  }
</style>

<p>A 2px wavy red underline in one line!</p>
```

**Expected Output:** Text with a red, wavy, 2-pixel underline.

> **Order tip:** In the shorthand, you can write the values in any order, but the most common convention is: line → style → colour → thickness.

### Thinking Prompt

Look at a website you use regularly (like a news site or an e-commerce store). Can you spot any custom text decorations? Are link underlines solid or wavy? Are they the same colour as the text?

---

## Part 5: CSS Text Transformation

### What Is It?

`text-transform` controls the **capitalisation** of text — whether it appears as UPPERCASE, lowercase, or Capitalized — without you having to actually retype the content.

### Why Does It Exist?

This is incredibly useful because:

- You can store text in your database as mixed case but display it as ALL CAPS for a heading
- You can ensure consistent style across a page without editing source content
- It's great for navigation menus, buttons, and headings

### The `text-transform` Property

| Value | Effect |
|---|---|
| `none` | No transformation — shows text exactly as written |
| `uppercase` | CONVERTS ALL TEXT TO CAPITAL LETTERS |
| `lowercase` | converts all text to small letters |
| `capitalize` | Makes The First Letter Of Each Word Capital |

### Example 1: All Four Transformations

```html
<style>
  .upper  { text-transform: uppercase; }
  .lower  { text-transform: lowercase; }
  .cap    { text-transform: capitalize; }
  .none   { text-transform: none; }
</style>

<p class="upper">this will become uppercase.</p>
<p class="lower">THIS WILL BECOME LOWERCASE.</p>
<p class="cap">this will become capitalised.</p>
<p class="none">This stays exactly as typed.</p>
```

**Expected Output:**

```
THIS WILL BECOME UPPERCASE.
this will become lowercase.
This Will Become Capitalised.
This stays exactly as typed.
```

### Real-World Use Case

Navigation menus often use `text-transform: uppercase` for a clean, professional look:

```html
<style>
  nav a {
    text-transform: uppercase;
    font-size: 14px;
    letter-spacing: 2px;
  }
</style>

<nav>
  <a href="#">home</a>
  <a href="#">about</a>
  <a href="#">contact</a>
</nav>
```

**Expected Output:** The links will display as HOME, ABOUT, CONTACT — even though the HTML says "home", "about", "contact".

> **Important:** `text-transform: capitalize` only capitalises the **first letter of each word**. It does NOT check grammar — it won't make the "i" in "I am" into "I" if there's no space before it in certain contexts. Always preview your result.

---

## Part 6: CSS Text Spacing

### What Is It?

CSS gives you five powerful properties to control the **spacing of text** — the gaps between individual letters, between words, between lines, and the indent at the start of a paragraph. Spacing greatly affects how readable and professional your text appears.

### Why Does It Exist?

- **Too little space** makes text feel cramped and hard to read
- **Too much space** makes text feel disconnected and strange
- Designers use spacing to create rhythm, emphasis, and elegance in typography

### The Five Key Text-Spacing Properties

| Property | What It Controls |
|---|---|
| `text-indent` | The empty space before the first line of a paragraph |
| `letter-spacing` | The extra space between individual characters |
| `word-spacing` | The extra space between individual words |
| `line-height` | The space between lines of text (line spacing) |
| `white-space` | How the browser handles spaces and line breaks in HTML |

### Property 1: `text-indent`

`text-indent` pushes the first line of a paragraph inward — just like the Tab key in Word:

```html
<style>
  p {
    text-indent: 50px;
  }
</style>

<p>
  This paragraph's first line is indented by 50 pixels. The rest of the
  paragraph continues at the normal left edge, as you'd find in a book.
</p>
```

**Expected Output:** The first word of the paragraph starts 50 pixels from the left edge. Subsequent lines align to the normal left margin.

You can also use **negative values** to create a "hanging indent" (first line sticks out to the left):

```css
p {
  text-indent: -30px;
  padding-left: 30px;  /* needed to prevent text going off-screen */
}
```

### Property 2: `letter-spacing`

`letter-spacing` adds or removes space between every character (letter) in the text:

```html
<style>
  .normal  { letter-spacing: normal; }
  .wide    { letter-spacing: 5px; }
  .wider   { letter-spacing: 10px; }
  .tight   { letter-spacing: -2px; }
</style>

<p class="normal">Normal letter spacing.</p>
<p class="wide">W i d e r   l e t t e r s   ( 5 p x )</p>
<p class="wider">V e r y   w i d e   ( 1 0 p x )</p>
<p class="tight">Tight letters (-2px)</p>
```

**Expected Output:** Each paragraph shows text with different amounts of space between the individual characters.

**Real-world use:** Wide letter-spacing (e.g., `letter-spacing: 3px`) on uppercase heading text creates a sophisticated, editorial look — like a luxury brand's logo.

### Property 3: `word-spacing`

`word-spacing` adds or removes space between **words** (not individual letters):

```html
<style>
  .normal { word-spacing: normal; }
  .wide   { word-spacing: 10px; }
  .tight  { word-spacing: -3px; }
</style>

<p class="normal">Normal word spacing between all words.</p>
<p class="wide">Extra   word   spacing   (10px).</p>
<p class="tight">Tight word spacing (-3px).</p>
```

**Expected Output:** Three paragraphs where the gaps between words are different sizes.

> **Thinking Prompt:** What happens if you apply both `letter-spacing: 3px` and `word-spacing: 8px` to the same paragraph? Would both apply? Try it!

### Property 4: `line-height`

`line-height` is perhaps the most important spacing property for readability. It controls the **vertical space between lines of text** in a paragraph.

```html
<style>
  .tight  { line-height: 1; }
  .normal { line-height: 1.5; }
  .airy   { line-height: 2.5; }
  .pixels { line-height: 40px; }
</style>

<p class="tight">
  Tight line height (1). The lines are very close together. This can feel
  cramped for long reading. Notice how the descenders of one line almost
  touch the ascenders of the next line.
</p>

<p class="normal">
  Normal line height (1.5). This is the standard used on most websites.
  It gives text room to breathe and improves readability significantly.
</p>

<p class="airy">
  Airy line height (2.5). The lines are very spread apart. This might suit
  a heading but would feel too spread out for a long article.
</p>
```

**Expected Output:** Three paragraphs with very different spacing between their lines.

> **Best Practice:** For body text, a `line-height` between `1.4` and `1.7` is generally considered ideal for readability. Using a unitless value like `1.5` is recommended over pixels because it scales proportionally with font size.

### Property 5: `white-space`

`white-space` controls how extra spaces and line breaks in your HTML source are handled:

| Value | Behaviour |
|---|---|
| `normal` | Multiple spaces collapse to one; text wraps automatically (default) |
| `nowrap` | Text never wraps — goes on one line forever |
| `pre` | Preserves all spaces and line breaks exactly as typed |
| `pre-wrap` | Preserves spaces, but wraps when needed |
| `pre-line` | Collapses extra spaces, but preserves line breaks |

```html
<style>
  .no-wrap { white-space: nowrap; }
  .pre     { white-space: pre; }
</style>

<p class="no-wrap">
  This very long sentence will never wrap to the next line no matter
  how narrow the browser window is.
</p>

<p class="pre">
  This   text   keeps
  all     its   spaces
  and line breaks!
</p>
```

**Expected Output:**
- First `<p>`: One single line of text that causes horizontal scrolling if too long
- Second `<p>`: Text displayed with all its extra spaces and line breaks preserved — like a preformatted code block

---

## Part 7: CSS Text Shadow

### What Is It?

`text-shadow` adds a **shadow effect** to text. It works just like dropping a shadow behind a physical object — the text appears to float above the page.

### Why Does It Exist?

Text shadows are used to:

- Make text stand out over a busy background (e.g., white text over a photograph)
- Create a dramatic, stylised look for headings
- Add depth and dimension to flat designs
- Create "glowing" text effects for creative or gaming websites

### The `text-shadow` Property Syntax

```css
text-shadow: horizontal-offset vertical-offset blur-radius color;
```

Let's understand each part:

- **horizontal-offset** — how far the shadow moves left (negative) or right (positive)
- **vertical-offset** — how far the shadow moves up (negative) or down (positive)
- **blur-radius** — how blurry/soft the shadow is (0 = sharp, higher = blurrier)
- **color** — the colour of the shadow

### Example 1: A Simple Basic Shadow

```html
<style>
  h1 {
    text-shadow: 2px 2px red;
  }
</style>

<h1>Hello with a red shadow!</h1>
```

**Expected Output:** The heading text has a red shadow slightly offset to the right and below the main text.

Breaking it down:
- `2px` → move shadow 2 pixels to the RIGHT
- `2px` → move shadow 2 pixels DOWN
- `red` → shadow colour is red

### Example 2: Adding Blur

```html
<style>
  h1 {
    text-shadow: 2px 2px 5px red;
  }
</style>

<h1>Hello with a blurred red shadow!</h1>
```

**Expected Output:** Same as before, but the shadow is softly blurred — it blends into the background instead of being a hard edge.

### Example 3: A Classic Drop Shadow

```html
<style>
  h1 {
    color: #ffffff;
    text-shadow: 2px 2px 4px #000000;
    background-color: #3498db;
    padding: 20px;
  }
</style>

<h1>White text, black shadow, blue background</h1>
```

**Expected Output:** White text on a blue background, with a soft black shadow beneath the text — this is a classic professional look.

### Example 4: Neon Glow Effect

A glow effect is created by using the same colour as the text but with a large blur radius:

```html
<style>
  h1 {
    color: #39ff14;             /* neon green text */
    text-shadow: 0 0 10px #39ff14,
                 0 0 20px #39ff14,
                 0 0 40px #39ff14;
    background-color: #000000;
    padding: 20px;
    text-align: center;
  }
</style>

<h1>NEON GLOW TEXT</h1>
```

**Expected Output:** A dark background with glowing bright green text — like a neon sign!

> **Notice:** In this example we used **multiple shadows** separated by commas. Each shadow is applied on top of the previous, creating layers of glow.

### Example 5: Multiple Shadows for a 3D Effect

```html
<style>
  h1 {
    color: #ff6b6b;
    text-shadow: 1px 1px 0 #c0392b,
                 2px 2px 0 #c0392b,
                 3px 3px 0 #c0392b,
                 4px 4px 0 #c0392b,
                 5px 5px 0 #c0392b;
    font-size: 48px;
  }
</style>

<h1>3D Text!</h1>
```

**Expected Output:** Bold red text that appears to have a 3D depth, as if the letters are raised off the page.

### Tip: Negative Offsets

```html
<style>
  h1 {
    text-shadow: -2px -2px 5px blue;
  }
</style>

<h1>Shadow goes UP and to the LEFT</h1>
```

**Expected Output:** The shadow appears above and to the left of the text (opposite direction from usual).

---

## Guided Practice Exercises

### Exercise 1: Style a Colour Palette Card

**Objective:** Practise `color`, `background-color`, and `text-align`

**Scenario:** You are building a colour reference card for a design team.

**Steps:**

1. Create an HTML file with 4 `<div>` elements
2. Give each `<div>`:
   - A different background colour
   - White or black text (whichever has better contrast)
   - Centred text alignment
   - The name of the colour written inside

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      .card {
        width: 200px;
        height: 80px;
        text-align: center;
        line-height: 80px;
        font-size: 18px;
        margin: 10px;
        display: inline-block;
      }
      .coral   { background-color: #e74c3c; color: white; }
      .navy    { background-color: #2c3e50; color: white; }
      .gold    { background-color: #f39c12; color: white; }
      .sage    { background-color: #27ae60; color: white; }
    </style>
  </head>
  <body>
    <div class="card coral">Coral Red</div>
    <div class="card navy">Navy Blue</div>
    <div class="card gold">Golden Yellow</div>
    <div class="card sage">Sage Green</div>
  </body>
</html>
```

**Expected Output:** Four coloured rectangular boxes, each with the colour name centred inside in white text.

**Self-check Questions:**
- Does each card have clearly readable text?
- What would happen if you changed `color: white` to `color: yellow` on the coral card?

---

### Exercise 2: Article Typography

**Objective:** Practise `text-align`, `line-height`, `text-indent`, and `letter-spacing`

**Scenario:** You are styling a magazine-style article page.

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      body {
        max-width: 600px;
        margin: 0 auto;
        font-size: 18px;
        color: #333;
      }

      h1 {
        text-align: center;
        letter-spacing: 4px;
        text-transform: uppercase;
        color: #2c3e50;
      }

      .byline {
        text-align: center;
        color: #7f8c8d;
        font-size: 14px;
        letter-spacing: 2px;
      }

      p {
        text-align: justify;
        line-height: 1.8;
        text-indent: 40px;
      }
    </style>
  </head>
  <body>
    <h1>the art of typography</h1>
    <p class="byline">by a curious learner — april 2026</p>
    <p>
      Typography is the art and technique of arranging type. It involves
      selecting typefaces, point sizes, line lengths, line spacing, and
      letter spacing. Good typography makes text beautiful and easy to read.
    </p>
    <p>
      Web designers use CSS to control all these elements. With just a few
      lines of code, a page can be transformed from raw text into a polished,
      professional article worthy of any magazine.
    </p>
  </body>
</html>
```

**Expected Output:**
- An uppercase heading with wide letter spacing
- A grey, small byline centred below
- Body paragraphs that are justified with comfortable line spacing and an indented first line

**Self-check Questions:**
- How does `line-height: 1.8` change the reading experience compared to `line-height: 1`?
- Why do we use `text-indent: 40px` on the paragraph but NOT on the heading?

---

### Exercise 3: Sale Badge with Strikethrough

**Objective:** Practise `text-decoration`, `text-decoration-color`, and `text-decoration-style`

**Scenario:** You're building a product card for an e-commerce site that shows the original and sale price.

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      .product-card {
        border: 1px solid #ddd;
        padding: 20px;
        width: 250px;
        font-family: sans-serif;
      }
      .original-price {
        text-decoration: line-through;
        text-decoration-color: #e74c3c;
        text-decoration-thickness: 2px;
        color: #7f8c8d;
        font-size: 20px;
      }
      .sale-price {
        color: #e74c3c;
        font-size: 28px;
        font-weight: bold;
      }
      .badge {
        background-color: #e74c3c;
        color: white;
        padding: 4px 8px;
        font-size: 12px;
        text-transform: uppercase;
        letter-spacing: 1px;
      }
    </style>
  </head>
  <body>
    <div class="product-card">
      <p><span class="badge">Sale</span></p>
      <p>Premium Wireless Headphones</p>
      <p class="original-price">₦45,000</p>
      <p class="sale-price">₦29,999</p>
    </div>
  </body>
</html>
```

**Expected Output:** A card showing the original price struck through with a red line, and the sale price displayed prominently in red below.

---

## Mini Project: Personal Profile Card

**Goal:** Combine everything you have learned in this lesson to build a professional-looking personal profile card.

### Project Description

You will create a profile card for an imaginary person (or yourself!). The card should use:

- Text colour and background colour
- Text alignment (centred name, left-aligned bio)
- Text decoration (styled link)
- Text transformation (uppercase role title)
- Letter spacing and line height
- Text shadow on the name

### Stage 1: Setup & Structure

Start with the HTML structure:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Profile Card</title>
    <style>
      /* We'll fill this in during Stages 2–4 */
    </style>
  </head>
  <body>
    <div class="card">
      <div class="card-header">
        <h1 class="name">Amara Okonkwo</h1>
        <p class="role">software engineer</p>
      </div>
      <div class="card-body">
        <p class="bio">
          Amara is a passionate developer who builds accessible, beautiful
          web applications. She specialises in front-end technologies and
          loves teaching others about CSS.
        </p>
        <a href="#" class="contact-link">Get in Touch</a>
      </div>
    </div>
  </body>
</html>
```

### Stage 2: Card Header Styling

```css
body {
  background-color: #ecf0f1;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  margin: 0;
}

.card {
  background-color: #ffffff;
  width: 340px;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0,0,0,0.1);
}

.card-header {
  background-color: #2c3e50;
  padding: 30px 20px;
  text-align: center;
}

.name {
  color: #ffffff;
  text-shadow: 2px 2px 6px rgba(0,0,0,0.5);
  letter-spacing: 2px;
  margin: 0 0 8px 0;
}
```

**Milestone Output:** A dark-coloured card header with white name text that has a subtle shadow and wide letter spacing.

### Stage 3: Role and Body Styling

```css
.role {
  text-transform: uppercase;
  letter-spacing: 4px;
  font-size: 12px;
  color: #bdc3c7;
  margin: 0;
}

.card-body {
  padding: 20px;
}

.bio {
  color: #555555;
  line-height: 1.7;
  text-align: justify;
  font-size: 15px;
  margin-bottom: 20px;
}
```

**Milestone Output:** The role title appears in small uppercase text with wide spacing. The bio reads comfortably with justified text and generous line height.

### Stage 4: Contact Link Styling

```css
.contact-link {
  display: block;
  text-align: center;
  color: #2c3e50;
  text-decoration: underline;
  text-decoration-color: #e74c3c;
  text-decoration-thickness: 2px;
  text-decoration-style: solid;
  letter-spacing: 1px;
  text-transform: uppercase;
  font-size: 13px;
  padding: 10px;
  border: 2px solid #2c3e50;
  border-radius: 4px;
}
```

**Milestone Output:** A styled contact button/link with a custom red underline decoration, uppercase text, and a border.

### Final Output

The complete card should display:
- A dark header with the person's name in white with a shadow and wide letter spacing
- Their role in small, uppercase, grey spaced text below
- A body section with a justified, comfortable bio paragraph
- A styled contact link with custom text decoration

**Reflection Questions:**
- Which property made the biggest visual difference to the card's appearance?
- How would you change the card to suit a different person — say, a doctor or an artist?
- What would you add to make the card even more polished?

**Optional Advanced Extensions:**
- Add a `:hover` effect to the contact link that changes the underline colour
- Try adding a `text-shadow` with a colour-matching glow to the role text
- Change the card theme by swapping all the colour values (e.g., a warm terracotta palette)

---

## Common Beginner Mistakes

### Mistake 1: Confusing `color` with `background-color`

❌ **Wrong:**
```css
p {
  color: yellow;  /* trying to make background yellow */
}
```

✅ **Correct:**
```css
p {
  background-color: yellow;  /* this colours the background */
  color: black;              /* this colours the text */
}
```

**Why:** `color` only changes the text/ink colour. `background-color` changes the box behind the text.

---

### Mistake 2: Thinking `text-align: center` Centres the Element

❌ **Wrong assumption:** "I used `text-align: center` but my `<div>` is still on the left!"

**The truth:** `text-align: center` centres the **text content INSIDE** the element. It does not centre the element/box itself on the page.

✅ **To centre a block element:**
```css
div {
  width: 300px;
  margin: 0 auto;  /* this centres the div */
}
```

---

### Mistake 3: Forgetting Units on Spacing Properties

❌ **Wrong:**
```css
letter-spacing: 5;      /* ❌ no unit! */
text-shadow: 2 2 red;   /* ❌ no px! */
```

✅ **Correct:**
```css
letter-spacing: 5px;
text-shadow: 2px 2px red;
```

**Why:** CSS spacing values need a unit (like `px`, `em`, `rem`). Without units, the browser ignores the declaration entirely.

---

### Mistake 4: Using `text-decoration: none` and Wondering Why It Doesn't Show

❌ **Wrong mental model:** "I set `text-decoration: underline` but then also `text-decoration: none` and now there's no underline."

**Explanation:** `text-decoration: none` removes all decorations. If you want a decoration, don't use `none`.

✅ **The fix:** Choose ONE value:
```css
/* Add an underline */
text-decoration: underline;

/* OR remove it */
text-decoration: none;
```

---

### Mistake 5: Applying `text-shadow` Without a Colour

❌ **Wrong:**
```css
h1 {
  text-shadow: 3px 3px;  /* missing colour! */
}
```

✅ **Correct:**
```css
h1 {
  text-shadow: 3px 3px #000000;
}
```

---

### Mistake 6: Confusing `letter-spacing` and `word-spacing`

`letter-spacing` → spaces between every individual character (e, v, e, r, y  l, e, t, t, e, r)
`word-spacing` → spaces between whole words (like this)

They are different properties and do different things!

---

### Mistake 7: Using `text-transform: capitalize` to Fix ALL CAPS Text

❌ **Wrong assumption:** "I have all-caps text and I want it to look normal. I'll use `text-transform: capitalize`."

`capitalize` only capitalises the first letter of each word. It does NOT convert `SCREAMING TEXT` into `Normal Text`.

✅ **Correct:**
```css
text-transform: lowercase;  /* converts EVERYTHING to lowercase */
```

Then use `capitalize` if you want the first letter of each word to be upper.

---

## Reflection Questions

1. If you were designing a news website, which text alignment would you choose for article body text, and why?

2. When would you remove the underline from a link? What visual cue would you use instead to tell users the text is clickable?

3. What is the difference between `letter-spacing` and `word-spacing`? Give a real-world scenario where you would use each.

4. You want your heading to look like it is glowing in purple. Which CSS property would you use, and what values would you write?

5. A client asks you to make their logo text appear in ALL CAPITALS but they want to keep the HTML text as mixed-case for SEO reasons. Which CSS property lets you do this without changing the HTML?

6. What would happen if you used `white-space: nowrap` on a paragraph with a very long sentence on a mobile phone screen? Why could this be a problem?

7. Why is it generally better to write `line-height: 1.6` (unitless) rather than `line-height: 24px` (in pixels)?

---

## Completion Checklist

Before moving to the next lesson, confirm you can do each of these:

- [ ] Set text colour using a colour name, HEX code, and RGB value
- [ ] Set both `color` and `background-color` correctly on the same element
- [ ] Use `text-align` with `left`, `right`, `center`, and `justify` values
- [ ] Explain the difference between `text-align` and centering a block element
- [ ] Add an underline, overline, and strikethrough using `text-decoration-line`
- [ ] Remove the default underline from an `<a>` tag
- [ ] Change the colour, style (solid/dashed/dotted/wavy), and thickness of a decoration line
- [ ] Use the `text-decoration` shorthand property correctly
- [ ] Apply `text-transform: uppercase`, `lowercase`, and `capitalize`
- [ ] Set `text-indent` to indent the first line of a paragraph
- [ ] Use `letter-spacing` to spread or tighten individual characters
- [ ] Use `word-spacing` to control space between words
- [ ] Set a comfortable `line-height` for body text (e.g., `1.5` to `1.8`)
- [ ] Understand what `white-space: nowrap` does
- [ ] Write a `text-shadow` with horizontal offset, vertical offset, blur, and colour
- [ ] Combine multiple text-shadow values for a glow or 3D effect
- [ ] Complete the profile card mini-project using multiple text properties together

---

## Lesson Summary

In this lesson, you mastered the complete set of CSS text-styling properties:

**Text Color** (`color`) — You can paint your text any colour using names, HEX codes, or RGB values. The body selector sets a page-wide default, and individual selectors override it.

**Text Alignment** (`text-align`, `text-align-last`, `direction`, `vertical-align`) — Text can be aligned left, right, centred, or justified. `text-align-last` targets only the final line of a block. `direction` controls RTL/LTR reading direction.

**Text Decoration** (`text-decoration-line`) — You can add underlines, overlines, and line-throughs to text. You can remove decorations entirely using `none`.

**Decoration Styles** (`text-decoration-color`, `text-decoration-style`, `text-decoration-thickness`) — The decoration line itself can be styled with any colour, made solid, double, dotted, dashed, or wavy, and given a specific thickness. The shorthand `text-decoration` combines all four values in one line.

**Text Transformation** (`text-transform`) — CSS can automatically convert your text to `uppercase`, `lowercase`, or `capitalize` without changing the HTML — perfect for consistent heading styles.

**Text Spacing** (`text-indent`, `letter-spacing`, `word-spacing`, `line-height`, `white-space`) — These five properties give you fine-grained control over every dimension of spacing around and within text. `line-height: 1.5` to `1.7` is the sweet spot for readable body text.

**Text Shadow** (`text-shadow`) — Shadows bring text to life. The four values — horizontal, vertical, blur, colour — can be layered multiple times using commas to create glows, 3D effects, and dramatic drop-shadows.

Together, these properties are the foundation of beautiful, readable, professional web typography. Every website you visit uses them — and now you can use them too.

---

*Next lesson: CSS Fonts — font families, sizes, web-safe fonts, Google Fonts, and the font shorthand.*
