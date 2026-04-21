---
render_with_liquid: false
title: "CSS Units — Absolute and Relative"
nav_order: 38
---

# Lesson 38: CSS Units — Absolute and Relative

---

## Lesson Introduction

Imagine you are decorating a room. You need to decide how big the furniture should be. You might say "this sofa is exactly 2 metres long" — that is a fixed, absolute measurement. Or you might say "this table should be half the width of the room" — that is a relative measurement, because it depends on the room size.

CSS units work exactly the same way. When you write CSS to style a webpage, you often need to say how wide something should be, how tall, how far apart, or how big the text should be. To do that, you must use **CSS units** — special codes that tell the browser how to measure things.

This lesson will teach you:
- What CSS units are and why they exist
- The difference between **absolute units** (fixed sizes) and **relative units** (flexible sizes)
- Every important unit in detail, with real examples
- When to use each unit and why
- How to build a real mini-project using multiple units together

By the end of this lesson, you will be able to confidently size any element on a webpage using the right unit for the job.

---

## Prerequisite Concepts

Before diving into CSS units, you need to understand a few very basic ideas. If you already know CSS properties like `width`, `font-size`, `margin`, and `padding`, you are ready. If not, here is a quick summary:

**What is a CSS property?** A CSS property is an instruction you give to a browser, like "make this element red" or "make this element 200 pixels wide." Properties always need a **value**, and many values require a **unit**. For example:

```css
p {
  font-size: 16px;   /* 'font-size' is the property, '16px' is the value+unit */
  width: 300px;      /* 'width' is the property, '300px' is the value+unit */
}
```

**What is an element?** An element is any piece of content on your page: a heading, a paragraph, a box, a button, an image — anything you see inside your HTML.

**What is a parent element?** Elements can be nested inside each other. The element that contains another element is called the **parent**. This matters a lot for relative units, as you will see.

```html
<div>          <!-- This is the PARENT element -->
  <p>Hello</p> <!-- This is the CHILD element -->
</div>
```

---

## Conceptual Understanding

### What Are CSS Units?

A **CSS unit** is a code that comes immediately after a number in a CSS value. It tells the browser *what kind of measurement* the number represents.

For example:
- `16px` — the number `16`, measured in **pixels**
- `2em` — the number `2`, measured in **em** (relative to font size)
- `50%` — the number `50`, measured as a **percentage**

> **Rule to remember:** There must be NO space between the number and the unit. `16px` is correct. `16 px` is wrong and will be ignored by the browser.
>
> **Special exception:** If the value is `0`, you do not need to write a unit at all. `margin: 0;` is perfectly valid.

### The Two Big Categories of CSS Units

CSS units are divided into exactly two categories:

**1. Absolute Units** — These are fixed. They do not change no matter what screen, window, or device you use. Think of them like measuring in centimetres with a ruler — 2cm is always 2cm.

**2. Relative Units** — These are flexible. They calculate their actual size based on something else, such as the parent element's font size, the viewport (screen) size, or the root element's font size. Think of them like percentages — "50% of whatever the parent's width is."

---

## Part 1: Absolute CSS Units

### What Are Absolute Units?

Absolute units are **fixed and unchanging**. If you set something to `100px`, it will always be exactly 100 pixels wide — whether viewed on a giant desktop monitor or a small phone screen.

The most important thing to understand: **absolute units do not respond to the user's screen or preferences.** They are locked in place.

**When should you use absolute units?**
- For **print stylesheets** (printing a document to paper, where you know exactly the size of the paper)
- For **fine decorative details** where you want pixel-perfect control
- When the output device size is completely known in advance

**When should you NOT use absolute units?**
- For responsive web design (making websites that look good on all screen sizes)
- For font sizes on screens (because it prevents users from scaling text with their browser's zoom)

### The Complete Table of Absolute CSS Units

| Unit | Full Name | Definition | Equivalent |
|------|-----------|------------|------------|
| `px` | Pixels | 1px = 1/96th of 1 inch | Most common absolute unit |
| `pt` | Points | 1pt = 1/72nd of 1 inch | Common in print/word processors |
| `cm` | Centimetres | Real-world centimetres | 1cm = 37.8px |
| `mm` | Millimetres | Real-world millimetres | 10mm = 1cm |
| `in` | Inches | Real-world inches | 1in = 96px = 2.54cm |
| `pc` | Picas | Typographic unit | 1pc = 12pt |

### Deep Dive: The `px` Unit (Pixels)

`px` stands for **pixel**. On a screen, pixels are the tiny dots of light that make up what you see. Your screen might be 1920 pixels wide and 1080 pixels tall.

In CSS, **1px is defined as 1/96th of one inch**. This is a CSS standard, not the literal physical pixel on the screen.

> **Analogy:** Think of a pixel as one tiny square tile on a mosaic. The more tiles (pixels) you use, the bigger and higher-quality the picture looks.

**Simple Example 1: Setting a box width with px**

```css
div {
  width: 200px;
  height: 100px;
  background-color: lightblue;
}
```

**What this does:**
- `width: 200px;` — Makes the box exactly 200 pixels wide
- `height: 100px;` — Makes the box exactly 100 pixels tall
- The box will always be 200×100 px no matter what

**Expected output:** A light blue rectangle, always the same size regardless of the screen.

---

**Simple Example 2: Setting font size with px**

```css
h1 {
  font-size: 60px;
}

p {
  font-size: 16px;
}
```

**What this does:**
- The `h1` heading will be exactly 60 pixels tall as text
- The `p` paragraph will be exactly 16 pixels tall as text

**Expected output:** A very large heading followed by small, normal-sized paragraph text.

> 🤔 **Thinking prompt:** What happens if a user has poor eyesight and zooms their browser to make text bigger? With `px` set on fonts, this can sometimes cause issues. This is one reason relative units like `em` and `rem` are preferred for text.

---

### The `pt` Unit (Points)

`pt` stands for **point**, a measurement system used in typography (the art of arranging text) and word processing software (like Microsoft Word).

**1pt = 1/72nd of one inch**

If you open Microsoft Word and set your font size to 12pt, that is the same system CSS uses with `pt`.

**When to use `pt`:** Mostly in **print stylesheets**. If you are designing how a webpage will look when printed on paper, `pt` makes sense because printers understand points well.

**Simple Example:**

```css
@media print {
  body {
    font-size: 12pt;  /* Standard print size — like a Word document */
  }
}
```

**Expected output:** When the user prints the page, text will appear at 12pt (normal print size).

---

### The `cm`, `mm`, `in`, and `pc` Units

These units are all based on **real-world physical measurements**. Here is how they relate to each other:

- 1 inch (`in`) = 2.54 centimetres = 96 pixels in CSS
- 1 centimetre (`cm`) = 10 millimetres = about 37.8 pixels
- 1 millimetre (`mm`) = about 3.78 pixels
- 1 pica (`pc`) = 12 points = 16 pixels

**Example using real-world measurements:**

```css
.print-box {
  width: 10cm;        /* 10 centimetres wide */
  height: 5cm;        /* 5 centimetres tall */
  border: 1mm solid black;  /* 1 millimetre thick border */
}
```

**Expected output on screen:** A box that approximates the physical measurements, though it will look slightly different depending on the monitor's pixel density.

> ⚠️ **Important note:** On screens, `cm`, `mm`, and `in` are converted to pixels by the browser. They are NOT literally physical centimetres on the screen. Physical accuracy is only reliable when printing. On a screen, `1cm` might not actually be 1 real centimetre because monitors have different pixel densities.

---

### Absolute Units — Side-by-Side Comparison

Here is how all absolute units compare to each other in CSS:

```
1in = 96px = 2.54cm = 25.4mm = 72pt = 6pc
```

**Quick demo — all measuring the same width:**

```css
.box-px { width: 96px; }    /* same visual width */
.box-pt { width: 72pt; }    /* same visual width */
.box-cm { width: 2.54cm; }  /* same visual width */
.box-in { width: 1in; }     /* same visual width */
```

All four boxes above will appear the same width on screen because they all equal 1 inch in CSS.

---

## Part 2: Relative CSS Units

### What Are Relative Units?

Relative units are **flexible** — their actual size depends on something else. That "something else" might be:
- The **parent element's** font size (for `em`)
- The **root element's** font size (for `rem`)
- The **viewport's** width or height (for `vw`, `vh`)
- The **parent element's** width or height (for `%`)

> **Analogy:** A relative unit is like saying "I want my coffee cup to be twice as tall as my teacup." The actual height changes depending on how tall the teacup is. Change the teacup, and the coffee cup height automatically changes too.

**Why are relative units so powerful?**
- They automatically adapt to different screen sizes
- They respect the user's browser zoom and accessibility settings
- They make responsive design much easier
- Changing one value can cascade and resize many elements at once

### Complete Table of Relative CSS Units

| Unit | Based On | Description |
|------|----------|-------------|
| `em` | Parent element's font size | 2em = twice the parent's font size |
| `rem` | Root element's font size | 2rem = twice the `<html>` element's font size |
| `%` | Parent element's size | 50% = half the parent's width (or height) |
| `vw` | Viewport width | 50vw = 50% of the screen width |
| `vh` | Viewport height | 50vh = 50% of the screen height |
| `vmin` | Smaller of vw or vh | 10vmin = 10% of the smaller screen dimension |
| `vmax` | Larger of vw or vh | 10vmax = 10% of the larger screen dimension |
| `ch` | Width of the "0" character | Useful for setting text line widths |
| `ex` | Height of the lowercase "x" | Based on the font's x-height |
| `lh` | Line height of the element | Useful for spacing based on text line height |

---

### The `em` Unit — Relative to Parent Font Size

`em` is one of the most commonly used relative units. It is relative to the **font size of the current element's parent**.

**1em = the font size of the parent element**

So if the parent element has `font-size: 20px`, then `1em = 20px`, and `2em = 40px`.

**Simple Example 1: `em` for font sizes**

```html
<div class="parent">
  <p class="child">Hello, world!</p>
</div>
```

```css
.parent {
  font-size: 20px;  /* Parent is 20px */
}

.child {
  font-size: 1.5em;  /* 1.5 × 20px = 30px */
}
```

**Expected output:** The paragraph text appears at 30px (1.5 times the parent's 20px).

---

**Simple Example 2: `em` for spacing**

```css
p {
  font-size: 16px;
  margin-bottom: 2em;  /* 2 × 16px = 32px gap below each paragraph */
  padding: 1em;        /* 1 × 16px = 16px padding on all sides */
}
```

**Expected output:** Each paragraph has a 32px gap below it and 16px of breathing room inside.

> 🤔 **Thinking prompt:** What happens if you change `font-size: 16px` to `font-size: 24px`? The margin and padding will also change automatically! `margin-bottom` becomes 48px, and `padding` becomes 24px. This is the power of `em` — everything scales together.

---

**⚠️ The em compounding problem:**

`em` has a famous quirk — it compounds (multiplies) when elements are nested inside each other.

```html
<ul>
  <li>Item 1
    <ul>
      <li>Sub item 1
        <ul>
          <li>Sub-sub item 1</li>  <!-- Gets very large! -->
        </ul>
      </li>
    </ul>
  </li>
</ul>
```

```css
ul {
  font-size: 1.2em;  /* Each nested ul is 1.2× its parent */
}
```

If the root is 16px:
- First level: 1.2 × 16 = 19.2px
- Second level: 1.2 × 19.2 = 23.04px
- Third level: 1.2 × 23.04 = 27.65px

The text keeps getting bigger with every level of nesting! This is why `rem` was invented.

---

### The `rem` Unit — Relative to Root Font Size

`rem` stands for **root em**. It works just like `em`, but instead of being relative to the parent element, it is ALWAYS relative to the **root element** — the `<html>` element.

**This means `rem` NEVER compounds.** It always refers back to the same base size.

**1rem = the font size of the `<html>` element (usually 16px by default)**

**Simple Example 1: rem stays consistent**

```css
html {
  font-size: 16px;  /* Root size = 16px */
}

h1 { font-size: 3rem; }    /* 3 × 16px = 48px */
h2 { font-size: 2rem; }    /* 2 × 16px = 32px */
h3 { font-size: 1.5rem; }  /* 1.5 × 16px = 24px */
p  { font-size: 1rem; }    /* 1 × 16px = 16px */
```

**Expected output:**
- `h1` text appears at 48px
- `h2` text appears at 32px
- `h3` text appears at 24px
- `p` text appears at 16px

No matter how deeply nested these elements are, the sizes will ALWAYS be what is shown above.

---

**Simple Example 2: The real power of rem — global scaling**

```css
html {
  font-size: 16px;  /* Change this ONE value... */
}

h1 { font-size: 3rem; }   /* ...and ALL these change automatically */
h2 { font-size: 2rem; }
p  { font-size: 1rem; }
```

If you change `font-size: 16px` to `font-size: 20px`, suddenly:
- `h1` becomes 60px (3 × 20)
- `h2` becomes 40px (2 × 20)
- `p` becomes 20px (1 × 20)

**By changing just ONE number, you resize your entire website's typography.** This is extremely powerful for design systems.

> 🌍 **Real-world use:** Professional CSS design systems (like Google's Material Design) use `rem` for all font sizes so that the entire typography scale can be adjusted by changing just one root font-size value.

---

### The `%` Unit — Percentage

The percentage unit `%` is one of the most intuitive relative units. It calculates a size **as a percentage of the parent element's size**.

For `width` and `height`: `%` is relative to the **parent's width or height**.
For `font-size`: `%` is relative to the **parent's font size**.
For `margin` and `padding`: `%` is always relative to the **parent's width** (even for top/bottom margin).

**Simple Example 1: Width as percentage**

```html
<div class="container">
  <div class="box">I am 50% wide</div>
</div>
```

```css
.container {
  width: 800px;
}

.box {
  width: 50%;  /* 50% of 800px = 400px */
  background-color: coral;
}
```

**Expected output:** The box is 400px wide (half the container).

---

**Simple Example 2: Font size as percentage**

```css
body {
  font-size: 16px;  /* Base size */
}

p {
  font-size: 150%;  /* 150% of 16px = 24px */
}
```

**Expected output:** Paragraph text appears at 24px.

---

**Simple Example 3: Percentage responding to resize**

```css
.sidebar {
  width: 25%;   /* Always a quarter of its parent */
}

.main-content {
  width: 75%;   /* Always three-quarters of its parent */
}
```

If the parent is 1200px wide: sidebar = 300px, main content = 900px.
If the parent is 800px wide: sidebar = 200px, main content = 600px.

This is the foundation of **responsive design** — layouts that automatically adjust.

---

### The `vw` and `vh` Units — Viewport Width and Height

The **viewport** is the visible area of the browser window. Think of it as the "window" through which you see the webpage.

- `vw` stands for **viewport width**. `1vw = 1% of the viewport width`
- `vh` stands for **viewport height**. `1vh = 1% of the viewport height`
- `100vw` = full viewport width
- `100vh` = full viewport height

**Simple Example 1: Full-screen hero section**

```css
.hero {
  width: 100vw;   /* Exactly as wide as the browser window */
  height: 100vh;  /* Exactly as tall as the browser window */
  background-color: navy;
  color: white;
}
```

**Expected output:** A full-screen navy blue section that fills the entire browser window, no matter what size the window is.

---

**Simple Example 2: Responsive heading with vw**

```css
h1 {
  font-size: 5vw;  /* Font size = 5% of viewport width */
}
```

**Expected output:**
- On a 1000px-wide screen: `5% × 1000 = 50px` font size
- On a 600px-wide screen: `5% × 600 = 30px` font size
- On a 400px-wide screen: `5% × 400 = 20px` font size

The font automatically gets smaller on smaller screens — no media queries needed!

> 🤔 **Thinking prompt:** What happens if someone resizes their browser window while looking at a heading set with `vw`? Try it — the heading will smoothly grow and shrink in real time!

---

**Simple Example 3: Side-by-side panels taking up the full screen**

```css
.left-panel {
  width: 30vw;
  height: 100vh;
  background-color: #2c3e50;
}

.right-panel {
  width: 70vw;
  height: 100vh;
  background-color: #ecf0f1;
}
```

**Expected output:** Two panels that together fill the entire screen: left panel takes 30% of the width, right takes 70% — always, on any screen size.

---

### The `vmin` and `vmax` Units

These two units are special — they pick between `vw` and `vh` based on which is smaller or larger.

- `vmin` — 1% of the **smaller** dimension (width or height)
- `vmax` — 1% of the **larger** dimension (width or height)

**When to use them:** For elements that should look good on both landscape and portrait orientations of a device.

**Example:**

```css
.square {
  width: 50vmin;   /* 50% of the SMALLER of vw or vh */
  height: 50vmin;
  background-color: gold;
}
```

On a screen that is 1000px wide and 700px tall:
- `vmin = 1% of 700px = 7px`
- `50vmin = 350px`

If you rotate the device so it is 700px wide and 1000px tall:
- `vmin = 1% of 700px = 7px` (still the smaller dimension)
- `50vmin = 350px` (the square stays the same size!)

**Expected output:** A square that maintains its size regardless of device orientation.

---

### The `ch` Unit — Character Width

`ch` is based on the **width of the "0" (zero) character** in the current font.

**When to use it:** For setting the **maximum line length of text**. Readability research shows that text is easiest to read at around 45–75 characters per line. You can enforce this with `ch`.

**Example:**

```css
p {
  max-width: 65ch;  /* No more than 65 characters wide */
  font-size: 1rem;
}
```

**Expected output:** Each paragraph will wrap at approximately 65 characters wide, creating optimal reading line length regardless of the font size.

---

### The `ex` Unit — X-Height

`ex` is based on the **height of the lowercase letter "x"** in the current font. This is called the "x-height."

Different fonts have different x-heights even at the same `font-size`. `ex` captures this difference.

**Example:**

```css
sup {
  font-size: 0.8em;
  vertical-align: 1ex;  /* Raise superscript one x-height above baseline */
}
```

This is mostly used in very fine typographic adjustments. You will not use `ex` very often as a beginner, but it is good to know it exists.

---

### The `lh` Unit — Line Height

`lh` is a newer CSS unit that equals the **computed line-height** of the element.

**Example:**

```css
p {
  font-size: 1rem;
  line-height: 1.6;
  margin-bottom: 1lh;  /* Bottom margin = exactly one line height */
}
```

**Expected output:** Perfect vertical spacing where the gap below each paragraph equals exactly the space between two lines of text.

---

## Part 3: `em` vs `rem` — Side-by-Side Comparison

This is one of the most important distinctions to understand. Let us see both in action:

**Scenario:** Both use the same HTML structure, but different units.

```html
<html>
  <body>
    <div class="outer">
      Outer text
      <div class="inner">
        Inner text
      </div>
    </div>
  </body>
</html>
```

**Using em:**

```css
html { font-size: 16px; }

.outer { font-size: 1.5em; }   /* 1.5 × 16px = 24px */
.inner { font-size: 1.5em; }   /* 1.5 × 24px = 36px ← compounds! */
```

**Expected output:**
- Outer text: 24px
- Inner text: 36px (not 24px!)

---

**Using rem:**

```css
html { font-size: 16px; }

.outer { font-size: 1.5rem; }  /* 1.5 × 16px = 24px */
.inner { font-size: 1.5rem; }  /* 1.5 × 16px = 24px ← always root! */
```

**Expected output:**
- Outer text: 24px
- Inner text: 24px (same! No compounding!)

---

> **Key rule of thumb:**
> - Use `rem` for font sizes (safe, predictable, no compounding)
> - Use `em` for margins and padding (so spacing scales with the element's own font size)
> - Use `%` and `vw/vh` for layout widths and heights

---

## Guided Practice Exercises

### Exercise 1: Warm-Up — Absolute Sizing

**Objective:** Practice using `px` for layout sizing.

**Scenario:** You are building a simple business card layout.

**Steps:**

1. Create an HTML file with this structure:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* YOUR CSS GOES HERE */
  </style>
</head>
<body>
  <div class="card">
    <h2>Ada Okafor</h2>
    <p>Web Developer</p>
    <p>ada@example.com</p>
  </div>
</body>
</html>
```

2. Add CSS using only `px` units to make the card look like a business card:

```css
.card {
  width: 350px;
  height: 200px;
  background-color: #2c3e50;
  color: white;
  padding: 30px;
  border-radius: 8px;
}

h2 {
  font-size: 24px;
  margin: 0 0 8px 0;
}

p {
  font-size: 14px;
  margin: 4px 0;
}
```

**Expected output:** A dark blue card, 350×200px, with a name in 24px and details in 14px.

**Self-check questions:**
- What happens if you change `width: 350px` to `width: 500px`?
- What happens if you make the browser window very narrow? Does the card fit?

---

### Exercise 2: Relative Sizing with `rem`

**Objective:** Build a typography scale using only `rem` units.

**Scenario:** You are creating the text hierarchy for a news website.

**Steps:**

```css
html {
  font-size: 16px;  /* Root size — try changing this! */
}

.headline {
  font-size: 3rem;        /* 48px */
  margin-bottom: 0.5rem;  /* 8px */
}

.subheadline {
  font-size: 2rem;        /* 32px */
  margin-bottom: 0.5rem;  /* 8px */
}

.article-body {
  font-size: 1rem;        /* 16px */
  line-height: 1.6;
  max-width: 65ch;        /* About 65 characters wide */
}

.caption {
  font-size: 0.75rem;     /* 12px */
  color: grey;
}
```

**Expected output:** A clear typographic hierarchy: very large headline → large subheadline → readable body text → small caption.

**Challenge:** Change `html { font-size: 16px; }` to `html { font-size: 20px; }`. Watch how EVERY text element scales up automatically!

**Self-check questions:**
- What is `1.5rem` when the root is 16px?
- What is `1.5rem` when the root is 20px?

---

### Exercise 3: Responsive Layout with `%` and `vw`

**Objective:** Create a two-column layout that responds to screen size.

**Scenario:** You are building a blog layout with a sidebar and main content area.

```html
<div class="page">
  <aside class="sidebar">Navigation links</aside>
  <main class="content">Article content here</main>
</div>
```

```css
.page {
  display: flex;
  width: 100vw;    /* Full viewport width */
  min-height: 100vh;  /* Full viewport height */
}

.sidebar {
  width: 25%;          /* Quarter of the page */
  background-color: #34495e;
  color: white;
  padding: 2rem;
}

.content {
  width: 75%;          /* Three-quarters of the page */
  padding: 2rem;
  font-size: 1rem;
  max-width: 70ch;     /* Optimal reading width */
}
```

**Expected output:** A full-screen two-column layout that adjusts proportionally to any screen width.

**What-if challenges:**
- What if you change sidebar to `width: 20%` and content to `width: 80%`?
- What if you change the root font-size? Does the `rem` padding change?

---

### Exercise 4: Viewport-based Full-Screen Section

**Objective:** Create a full-screen banner using `vw` and `vh`.

```css
.hero {
  width: 100vw;
  height: 100vh;
  background: linear-gradient(135deg, #667eea, #764ba2);
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.hero h1 {
  font-size: 6vw;     /* Scales with viewport width */
  color: white;
  margin: 0;
}

.hero p {
  font-size: 2vw;
  color: rgba(255, 255, 255, 0.85);
}
```

**Expected output:** A full-screen purple gradient banner. The text automatically scales with the browser window.

---

## Mini-Project: Personal Profile Card with Mixed Units

Now you will combine everything you have learned into one realistic project: a personal profile card that uses the right unit for each job.

### Project Overview

You will build a profile card component — the kind you see on social media or portfolio websites. It will use:
- `px` for borders and decorative details
- `rem` for typography
- `em` for spacing that scales with text
- `%` for the card's width within its container
- `vw`/`vh` to center it on the full page

---

### Stage 1: HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Profile Card</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="page-wrapper">
    <div class="profile-card">
      <div class="avatar">🧑‍💻</div>
      <h1 class="name">Chioma Nwachukwu</h1>
      <p class="title">Frontend Developer</p>
      <p class="bio">
        Passionate about creating beautiful, accessible user interfaces.
        Based in Lagos, Nigeria.
      </p>
      <div class="stats">
        <div class="stat">
          <span class="stat-number">48</span>
          <span class="stat-label">Projects</span>
        </div>
        <div class="stat">
          <span class="stat-number">3.2k</span>
          <span class="stat-label">Followers</span>
        </div>
        <div class="stat">
          <span class="stat-number">127</span>
          <span class="stat-label">Following</span>
        </div>
      </div>
      <button class="follow-btn">Follow</button>
    </div>
  </div>
</body>
</html>
```

**Milestone output after Stage 1:** Raw HTML with no styling — just text on a white background.

---

### Stage 2: Root Setup and Page Layout

```css
/* style.css */

/* ROOT SETUP — Using rem will reference this */
html {
  font-size: 16px;  /* 1rem = 16px */
}

/* Reset default spacing */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

/* CENTER THE CARD USING VIEWPORT UNITS */
.page-wrapper {
  width: 100vw;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #f0f4f8;
}
```

**Milestone output:** A light grey page that fills the full browser window. Nothing visible yet, but the layout foundation is set.

---

### Stage 3: Card Styling — Core Layout

```css
/* THE CARD ITSELF */
.profile-card {
  width: 90%;          /* % — responsive: 90% of page-wrapper */
  max-width: 380px;    /* px — but never wider than 380 fixed pixels */
  background: white;
  border-radius: 16px; /* px — decorative, precise */
  padding: 2.5rem;     /* rem — scales with font settings */
  text-align: center;
  box-shadow: 0 4px 24px rgba(0, 0, 0, 0.1);
}

/* AVATAR EMOJI/IMAGE */
.avatar {
  font-size: 5rem;     /* rem — scales globally */
  margin-bottom: 1rem; /* rem */
}
```

**Milestone output:** A white card centered on the grey page, with a large emoji at the top.

---

### Stage 4: Typography — Using rem and em

```css
/* NAME */
.name {
  font-size: 1.75rem;        /* rem — 28px at root 16px */
  font-weight: 700;
  color: #1a202c;
  margin-bottom: 0.25em;     /* em — scales with this element's font size */
}

/* JOB TITLE */
.title {
  font-size: 1rem;           /* rem — 16px */
  color: #667eea;
  font-weight: 500;
  margin-bottom: 1em;        /* em — 16px gap below */
  letter-spacing: 0.05em;    /* em — subtle letter spacing */
}

/* BIO TEXT */
.bio {
  font-size: 0.9rem;         /* rem — slightly smaller than base */
  color: #718096;
  line-height: 1.6;
  max-width: 55ch;           /* ch — optimal reading width */
  margin: 0 auto 1.5rem;     /* rem for bottom spacing */
}
```

**Milestone output:** The card now shows nicely sized, well-spaced text in a clear hierarchy.

---

### Stage 5: Stats Row and Button

```css
/* STATS ROW */
.stats {
  display: flex;
  justify-content: space-around;
  margin-bottom: 1.5rem;       /* rem */
  padding: 1.25rem 0;          /* rem — top/bottom padding */
  border-top: 1px solid #e2e8f0;    /* px — thin precise border */
  border-bottom: 1px solid #e2e8f0; /* px */
}

.stat {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;               /* rem — small gap between number and label */
}

.stat-number {
  font-size: 1.5rem;          /* rem — 24px */
  font-weight: 700;
  color: #1a202c;
}

.stat-label {
  font-size: 0.75rem;         /* rem — 12px, small caption */
  color: #a0aec0;
  text-transform: uppercase;
  letter-spacing: 0.1em;      /* em — wide letter spacing for labels */
}

/* FOLLOW BUTTON */
.follow-btn {
  width: 100%;                /* % — full width of the card's content area */
  padding: 0.875rem;          /* rem — comfortable tap/click area */
  background: #667eea;
  color: white;
  border: none;
  border-radius: 8px;         /* px — decorative radius */
  font-size: 1rem;            /* rem */
  font-weight: 600;
  cursor: pointer;
  letter-spacing: 0.05em;     /* em */
}

.follow-btn:hover {
  background: #5a6fd8;
}
```

**Final milestone output:** A beautiful, professional profile card with a name, title, bio, stats, and a follow button — all centered on a full-page background.

---

### Reflection Questions

After completing the mini-project, think about these questions:

1. The card uses `width: 90%` and `max-width: 380px`. Why use both? What does each one do?
2. If you change `html { font-size: 16px; }` to `html { font-size: 20px; }`, what happens to the card? Which parts change, and which stay the same?
3. The button uses `width: 100%`. What is 100% of what, exactly?
4. The bio uses `max-width: 55ch`. What would happen if the user changed their browser's default font size?
5. Why are borders specified in `px` rather than `rem`?

---

## Common Beginner Mistakes

### Mistake 1: Putting a space between the number and the unit

```css
/* ❌ WRONG — space breaks it */
font-size: 16 px;

/* ✅ CORRECT — no space */
font-size: 16px;
```

**Why this matters:** The browser will simply ignore the broken value. The element will have no font-size, or fall back to the default.

---

### Mistake 2: Forgetting that `em` compounds with nesting

```css
/* ❌ RISKY — em will compound in nested lists */
ul { font-size: 1.1em; }

/* ✅ SAFER — rem never compounds */
ul { font-size: 1.1rem; }
```

---

### Mistake 3: Using `px` for font sizes on accessible websites

```css
/* ❌ LESS ACCESSIBLE — user browser zoom may not work properly */
body { font-size: 14px; }

/* ✅ BETTER — respects user preferences */
body { font-size: 0.875rem; }  /* Still 14px at default, but scalable */
```

---

### Mistake 4: Using `px` for layouts instead of flexible units

```css
/* ❌ BREAKS on small screens */
.main-content { width: 960px; }

/* ✅ FLEXIBLE — adapts to any screen */
.main-content {
  width: 90%;
  max-width: 960px;
}
```

---

### Mistake 5: Using `vw` for font sizes without a minimum

```css
/* ❌ TEXT BECOMES TINY on very small screens */
h1 { font-size: 5vw; }

/* ✅ BETTER — use clamp() to set a minimum and maximum */
h1 { font-size: clamp(1.5rem, 5vw, 4rem); }
```

The `clamp()` function means: "never smaller than 1.5rem, scale with 5vw, never bigger than 4rem."

---

### Mistake 6: Mixing incompatible unit systems

```css
/* ❌ CONFUSING — mixing px and rem unpredictably */
.card {
  width: 400px;
  padding: 2rem;
  margin: 30px auto;
  font-size: 1rem;
}

/* ✅ CLEANER — consistent system */
.card {
  width: 25rem;     /* 400px equivalent, scales with root */
  padding: 2rem;
  margin: 1.875rem auto;
  font-size: 1rem;
}
```

---

## Reflection Questions

Test your understanding by answering these questions:

1. What is the difference between an absolute unit and a relative unit?
2. If the root `<html>` font-size is 16px, what is `2.5rem` in pixels?
3. If the parent's font-size is 20px, what is `1.5em` in pixels?
4. Why does `em` sometimes produce unexpected results when elements are nested?
5. What does `100vh` mean? Give an example of when you would use it.
6. Why is `rem` considered better than `px` for font sizes in accessible web design?
7. If you set `width: 60%` on an element, 60% of what?
8. When would you choose `px` over `rem`?
9. What is the `ch` unit based on, and why is it useful for text?
10. You have a card with `width: 90%` and `max-width: 400px`. On a 300px-wide screen, how wide is the card? On a 1000px-wide screen, how wide is the card?

---

## Completion Checklist

Before moving to the next lesson, make sure you can:

- [ ] Explain the difference between absolute and relative CSS units
- [ ] List at least 4 absolute units and describe when to use them
- [ ] Explain what `px`, `pt`, `cm`, and `mm` measure
- [ ] Explain what `em` measures and describe the compounding problem
- [ ] Explain what `rem` measures and why it solves the compounding problem
- [ ] Use `%` for layout widths relative to a parent
- [ ] Use `vw` and `vh` for viewport-relative sizing
- [ ] Know when to use `ch` for text widths
- [ ] Build a card component using a combination of `px`, `rem`, `em`, `%`, and `vw/vh`
- [ ] Identify and fix at least 3 common CSS unit mistakes

---

## Lesson Summary

CSS units are the measurements you use to control the size of everything on a webpage. There are two main categories:

**Absolute units** are fixed and do not change regardless of screen size or user settings. The most important ones are `px` (pixels) — the standard screen unit — and `pt` (points) — common in print. Other absolute units (`cm`, `mm`, `in`, `pc`) are typically only useful for print stylesheets where real physical dimensions matter.

**Relative units** are flexible and calculate their size based on something else. The most important ones are:
- `em` — relative to the parent element's font size (beware of compounding in nested elements)
- `rem` — relative to the root `<html>` font size (predictable, never compounds, best for fonts)
- `%` — relative to the parent element's size (great for flexible layouts)
- `vw` / `vh` — relative to the viewport (browser window) width and height (great for full-screen sections)
- `ch` — relative to the width of the "0" character (perfect for optimal text line lengths)
- `vmin` / `vmax` — relative to the smaller or larger viewport dimension

**The golden rule for choosing units:**
- Use `rem` for font sizes → predictable, accessible, globally scalable
- Use `em` for padding and margin → spacing scales with the element's own text size
- Use `%` for layout widths → flexible, responds to parent containers
- Use `vw` / `vh` for full-screen sections and viewport-relative sizing
- Use `px` for borders, shadows, and very precise decorative details
- Use `pt`, `cm`, `mm` for print stylesheets only

Understanding and choosing the right CSS unit is one of the most important skills in professional web development, because it directly determines how well your design responds to different devices, screen sizes, and user accessibility settings.
