---
render_with_liquid: false
title: "CSS Text Effects — Overflow, Word Wrapping, Line Breaking, and Writing Modes"
nav_order: 52
---

# Lesson 52 — CSS Text Effects: Overflow, Word Wrapping, Line Breaking & Writing Modes

---

## Lesson Introduction

Text is the heart of almost every webpage — headlines, paragraphs, product descriptions, blog posts, and menus all rely on it. But what happens when text is **too long** to fit inside its container? Or when a single word is so enormous that it breaks your layout? Or when you need text to run **vertically** instead of horizontally for a creative design?

CSS gives you four powerful properties to solve exactly these problems:

- `text-overflow` — control what users see when text is cut off
- `word-wrap` — allow very long words to break and wrap onto the next line
- `word-break` — decide exactly where words are allowed to break
- `writing-mode` — change the direction that text flows (horizontal or vertical)

These are called **CSS Text Effect properties**, and they are used every day in real websites — from product name tags that must fit inside small cards, to Japanese and Chinese websites that display text top-to-bottom, to tooltips that must stay within a fixed-width area.

By the end of this lesson you will be able to confidently use all four properties, understand why each one exists, and apply them in realistic projects.

> **Who is this lesson for?** Complete beginners who know basic CSS (selectors, properties, values). No advanced knowledge needed.

---

## Prerequisite Concepts

Before we dive in, let us make sure three foundational ideas are solid.

### What Is a CSS Property?

A **CSS property** is an instruction that tells the browser how to display an element. For example, `color: red` tells the browser to make text red. In this lesson we will learn four new properties that specifically deal with how text behaves when it overflows or changes direction.

### What Is `overflow`?

`overflow` is a CSS property that controls what happens when content inside an element is **bigger than the element's box**. Think of it like filling a glass with water — if you pour too much, it spills over. The `overflow` property lets you decide whether that "spill" is visible, hidden, or scrollable.

```css
/* The content will be hidden if it overflows */
overflow: hidden;

/* The content will show scrollbars if it overflows */
overflow: scroll;

/* The content spills out visibly (default) */
overflow: visible;
```

### What Is `white-space: nowrap`?

By default, a browser wraps long text onto new lines so it fits inside its container. `white-space: nowrap` **prevents that wrapping** — it forces all the text to stay on one line, even if it overflows the container.

```css
/* Prevents text from wrapping to a new line */
white-space: nowrap;
```

> **Why does this matter?** Two of the four text-effect properties in this lesson (`text-overflow` in particular) only work when text is prevented from wrapping. Understanding `overflow` and `white-space` is the key to making them work.

---

## Section 1 — The Problem: Text That Doesn't Fit

Imagine you have a product card that is only 200 pixels wide, but the product name is very long:

```
┌────────────────────┐
│ Ultra Premium Delu │  ← text gets cut off, no signal to user
└────────────────────┘
```

Or a paragraph with a word like `supercalifragilisticexpialidocious`:

```
┌────────────────────┐
│ The magic word is  │
│ supercalifragili   │
│ sticexpialidocious │  ← word flows out of the box with no control
└────────────────────┘
```

CSS Text Effect properties solve both of these problems cleanly and professionally.

---

## Section 2 — `text-overflow`

### What Is It?

The `text-overflow` property tells the browser **what to show the user when text is too long** to fit in its container and has been hidden by `overflow: hidden`.

### Why Does It Exist?

When text is cut off, users have no way of knowing there is more text they cannot see. `text-overflow` solves this by either **clipping** the text cleanly or showing a visual signal — the **ellipsis** (`...`) — telling the user "there is more here."

### The Two Required Companions

`text-overflow` will **not work** on its own. It requires two other properties to also be set on the same element:

```css
white-space: nowrap;   /* stop text from wrapping to a new line */
overflow: hidden;      /* hide the text that overflows the box */
/* NOW text-overflow can control how the hidden text is signalled */
```

Think of it like a team of three workers:
- `white-space: nowrap` keeps all the text on one line (so it CAN overflow)
- `overflow: hidden` hides the overflow (so it doesn't spill out visually)
- `text-overflow` decides HOW to signal the cut-off to the user

### The Two Main Values

#### Value 1: `clip`

`clip` simply cuts the text off at the edge of the container. No visual signal. The text just stops.

```css
p {
  width: 200px;
  border: 1px solid black;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: clip;   /* just cuts the text off */
}
```

**Visual result:**
```
┌────────────────────┐
│ This is some long  │
└────────────────────┘
```
The text is cut off at the box edge. The user can see something is missing, but there is no specific signal.

#### Value 2: `ellipsis`

`ellipsis` shows `...` (three dots) at the end of the visible text, signalling that there is more content that is not visible.

```css
p {
  width: 200px;
  border: 1px solid black;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;   /* shows "..." at the cut-off */
}
```

**Visual result:**
```
┌────────────────────┐
│ This is some lon…  │
└────────────────────┘
```
The `...` tells the user: "There is more text here that is not shown."

### Complete Side-by-Side Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Shared styles for both paragraphs */
    p.test1, p.test2 {
      width: 200px;
      border: 1px solid #000000;
      white-space: nowrap;    /* keep text on one line */
      overflow: hidden;       /* hide what doesn't fit */
    }

    /* Clip: just cut the text */
    p.test1 {
      text-overflow: clip;
    }

    /* Ellipsis: show "..." at the cut */
    p.test2 {
      text-overflow: ellipsis;
    }
  </style>
</head>
<body>

  <h3>text-overflow: clip</h3>
  <p class="test1">This is some long text that will not fit in the box</p>

  <h3>text-overflow: ellipsis</h3>
  <p class="test2">This is some long text that will not fit in the box</p>

</body>
</html>
```

**Expected output:**

```
text-overflow: clip
┌────────────────────┐
│ This is some long  │
└────────────────────┘

text-overflow: ellipsis
┌────────────────────┐
│ This is some lon…  │
└────────────────────┘
```

> **Thinking prompt:** Which value is more user-friendly — `clip` or `ellipsis`? Why?

**Answer:** `ellipsis` is generally more user-friendly because it gives the user a clear signal that there is more content. `clip` can be confusing — the user might think the content is complete when it is actually cut off.

---

### Bonus: Revealing Overflow on Hover

A very common pattern in real websites is to hide overflowing text normally, but reveal it when the user hovers over the element. This is easy to do:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      width: 200px;
      border: 1px solid black;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    /* When the user hovers, reveal all the text */
    p:hover {
      overflow: visible;   /* removes the hiding */
    }
  </style>
</head>
<body>

  <p>This is some long text that will not fit in the box normally.</p>
  <p>Hover over me to see all the text revealed!</p>

</body>
</html>
```

**What happens:**
- Normally: text shows `...` at the cut-off
- On hover: `overflow` changes to `visible` and ALL the text is revealed

**Expected output (normal state):**
```
┌────────────────────┐
│ This is some lon…  │
└────────────────────┘
```

**Expected output (hover state):**
```
┌────────────────────┐
│ This is some long text that will not fit in the box normally.
└────────────────────┘
```

> **Real-world use case:** Product listing pages often show truncated product names inside small cards. On hover, the full product name appears. This is a clean, professional UX pattern used by Amazon, Etsy, and countless e-commerce sites.

---

## Section 3 — `word-wrap`

### What Is It?

The `word-wrap` property (also written as `overflow-wrap` in modern CSS) allows **long words that are too big for their container** to be broken apart and wrapped onto the next line.

### Why Does It Exist?

By default, if a word is longer than its container, the browser simply lets the word overflow outside the box. This can completely break a layout. `word-wrap: break-word` gives the browser permission to split the word mid-way and continue it on the next line, keeping it neatly inside the container.

> **Analogy:** Imagine fitting a very long sausage into a lunchbox. Normally (without `word-wrap`), the sausage would stick out the side. With `word-wrap: break-word`, you get permission to bend the sausage so it stays inside the box.

### The Problem Without `word-wrap`

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      width: 200px;
      border: 1px solid black;
      background-color: lightyellow;
    }
  </style>
</head>
<body>
  <p>This paragraph contains a very long word:
  thisisaveryveryveryveryveryverylongword. The long word will overflow.</p>
</body>
</html>
```

**Expected output (WITHOUT word-wrap):**
```
┌────────────────────┐
│ This paragraph     │
│ contains a very    │
│ long word:         │
│ thisisaveryveryvery│veryverylongword.   ← overflows outside box!
│ The long word      │
│ will overflow.     │
└────────────────────┘
```

The long word bursts out of the box and may overlap other content. This is a real layout bug.

### The Fix: `word-wrap: break-word`

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      width: 200px;
      border: 1px solid black;
      background-color: lightgreen;
      word-wrap: break-word;   /* allow long words to break and wrap */
    }
  </style>
</head>
<body>
  <p>This paragraph contains a very long word:
  thisisaveryveryveryveryveryverylongword. The long word will break and wrap.</p>
</body>
</html>
```

**Expected output (WITH word-wrap: break-word):**
```
┌────────────────────┐
│ This paragraph     │
│ contains a very    │
│ long word:         │
│ thisisaveryveryvery│
│ veryveryverylongwor│
│ d. The long word   │
│ will break and     │
│ wrap.              │
└────────────────────┘
```

The long word is split across multiple lines. It stays cleanly inside the box. Layout is preserved.

### Second Example — Email Address in a Narrow Container

Email addresses are a common real-world case. They can be very long and contain no natural break points.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .email-box {
      width: 180px;
      border: 2px solid steelblue;
      padding: 8px;
      background-color: #e8f4fc;
    }

    .email-box.fixed {
      word-wrap: break-word;   /* fixed version */
    }
  </style>
</head>
<body>

  <h3>Without word-wrap (broken layout):</h3>
  <div class="email-box">
    Contact: verylongemailaddress@somedomainname.com
  </div>

  <br>

  <h3>With word-wrap: break-word (fixed):</h3>
  <div class="email-box fixed">
    Contact: verylongemailaddress@somedomainname.com
  </div>

</body>
</html>
```

**Expected output:**

Without fix — email address overflows outside the box.

With fix — email address wraps neatly inside the box, no overflow.

> **Thinking prompt:** Can you think of other types of content (besides very long words and emails) that might cause this overflow problem?

**Possible answers:** URLs/web links, file paths, product codes, serial numbers, hashtags, or any user-generated content where the user might type a very long single word.

---

## Section 4 — `word-break`

### What Is It?

The `word-break` property specifies **exactly how line breaks are decided** when text reaches the end of its container. While `word-wrap` asks "can we break long words?", `word-break` asks "at exactly what point do we break them, and do we apply these rules to ALL words?"

### Why Does It Exist?

Different languages have different rules about where words can be split. English words should ideally only break between syllables or at hyphens. Chinese and Japanese text can break anywhere (since each character is essentially its own unit). `word-break` lets you control these rules explicitly.

### The Three Main Values

#### Value 1: `normal` (Default)

Uses the browser's default line-breaking rules for the text's language. For most Latin (English) text, this means words only break at natural break points like spaces or hyphens.

```css
p {
  word-break: normal;   /* default behaviour */
}
```

**Visual result:**
```
┌────────────────────┐
│ This paragraph     │
│ contains some      │
│ text. This line    │
│ will-break-at-     │
│ hyphens.           │
└────────────────────┘
```
Normal words wrap at spaces; hyphenated words can wrap at the hyphen.

#### Value 2: `break-all`

Allows words to be broken at **any character** to prevent overflow — not just at natural word boundaries. Every character becomes a potential break point.

```css
p {
  word-break: break-all;   /* break at ANY character */
}
```

**Visual result:**
```
┌────────────────────┐
│ This paragraph con │
│ tains some text. T │
│ he lines will brea │
│ k at any character │
│ .                  │
└────────────────────┘
```
Words are cut mid-character wherever the line runs out. This keeps all content within the box but can look unnatural for long text.

#### Value 3: `keep-all`

Prevents words from breaking at all. Content will overflow rather than break mid-word. Useful for CJK (Chinese, Japanese, Korean) text where this is a cultural rule.

```css
p {
  word-break: keep-all;   /* never break words */
}
```

### Complete Three-Way Comparison Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      width: 200px;
      border: 1px solid #555;
      background-color: #f9f9f9;
      padding: 6px;
      margin-bottom: 16px;
    }

    p.normal   { word-break: normal; }
    p.break-all { word-break: break-all; }
    p.keep-all { word-break: keep-all; }
  </style>
</head>
<body>

  <h3>word-break: normal (default)</h3>
  <p class="normal">
    This paragraph contains some text. This line will-break-at-hyphens.
  </p>

  <h3>word-break: break-all</h3>
  <p class="break-all">
    This paragraph contains some text. The lines will break at any character.
  </p>

  <h3>word-break: keep-all</h3>
  <p class="keep-all">
    This paragraph contains some text. Words will not break at all.
  </p>

</body>
</html>
```

**Expected output for `normal`:**
Text wraps at spaces and hyphens only. Natural, readable.

**Expected output for `break-all`:**
Text is cut at any character — looks choppy but nothing overflows.

**Expected output for `keep-all`:**
Words are never broken — long words may overflow the container.

---

### `word-wrap` vs `word-break` — What Is the Difference?

This is a very common point of confusion for beginners. Here is the clearest way to understand them:

| Property | Question It Answers | When It Acts |
|---|---|---|
| `word-wrap: break-word` | "If a word is TOO LONG to fit, can we break it?" | Only breaks words that are genuinely too long to fit on any line |
| `word-break: break-all` | "Should ALL words break at any character, everywhere?" | Aggressively breaks ANY word at ANY character to fill lines |

> **Simple analogy:** `word-wrap` is a polite last resort: "I'll only break this word if there's absolutely no other choice." `word-break: break-all` is aggressive: "Break every word wherever the line ends, no exceptions."

**In practice:**
- Use `word-wrap: break-word` for most situations (more natural-looking results)
- Use `word-break: break-all` for compact code displays, tables, or situations where every pixel of space must be used

---

## Section 5 — `writing-mode`

### What Is It?

The `writing-mode` property controls **the direction in which text flows** — whether lines are written horizontally (left-to-right, like English) or vertically (top-to-bottom, like traditional Japanese or Chinese).

### Why Does It Exist?

Not all languages and writing systems flow the same way. Japanese, Chinese, and traditional Mongolian text can be written vertically. In web design, vertical text is also used for creative effects: rotated labels, side navigation bars, stylistic headings, and print-like magazine layouts.

### The Three Main Values

#### Value 1: `horizontal-tb` (Default)

Text flows horizontally from **left to right**, and lines stack from **top to bottom**. This is the normal English direction.

- `horizontal` = text goes left → right
- `tb` = top-to-bottom (each new line goes below the previous one)

```css
p {
  writing-mode: horizontal-tb;   /* normal — this is the default */
}
```

**Visual result:**
```
Hello, this is normal text flowing left to right.
Next line appears below.
```

#### Value 2: `vertical-rl`

Text flows **vertically from top to bottom**, and columns stack from **right to left**.

- `vertical` = text goes top → bottom
- `rl` = right-to-left (each new column appears to the left of the previous)

```css
p {
  writing-mode: vertical-rl;
}
```

**Visual result:**
```
H N
e e
l x
l t
o
```
(Characters stack top to bottom; multiple lines of text appear as columns going from right to left)

#### Value 3: `vertical-lr`

Text flows **vertically from top to bottom**, and columns stack from **left to right**.

- `vertical` = text goes top → bottom
- `lr` = left-to-right (each new column appears to the right of the previous)

```css
p {
  writing-mode: vertical-lr;
}
```

**Visual result:**
Same vertical character direction as `vertical-rl`, but columns progress from left to right instead.

### Simple Isolated Example — Vertical Text on a `<span>`

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      writing-mode: horizontal-tb;  /* normal paragraph */
    }

    span {
      writing-mode: vertical-rl;    /* just this span goes vertical */
      border: 1px solid red;
      padding: 4px;
    }
  </style>
</head>
<body>

  <p>Here is a text with a
    <span>vertical</span>
  span element with a vertical-rl writing-mode.</p>

</body>
</html>
```

**Expected output:**
```
Here is a text with a │v│ span element with a vertical-rl writing-mode.
                       │e│
                       │r│
                       │t│
                       │i│
                       │c│
                       │a│
                       │l│
```

The paragraph text flows normally, but the `<span>` rotates its content vertically (top to bottom).

### Three-Way Comparison Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      border: 1px solid darkblue;
      padding: 8px;
      display: inline-block;
      margin: 10px;
      background-color: #eef;
      font-size: 16px;
    }

    p.mode1 { writing-mode: horizontal-tb; }
    p.mode2 { writing-mode: vertical-rl; }
    p.mode3 { writing-mode: vertical-lr; }
  </style>
</head>
<body>

  <h3>horizontal-tb (default):</h3>
  <p class="mode1">Hello World</p>

  <h3>vertical-rl:</h3>
  <p class="mode2">Hello World</p>

  <h3>vertical-lr:</h3>
  <p class="mode3">Hello World</p>

</body>
</html>
```

**Expected output:**

`horizontal-tb`: Text reads left to right, normal.

`vertical-rl`: Text reads top to bottom in a tall, narrow column.

`vertical-lr`: Text reads top to bottom in a tall, narrow column (columns progress left to right).

> **Real-world use case:** `writing-mode: vertical-rl` is used in Japanese web design, digital magazine layouts, book-like reading experiences, and side navigation labels that run along the edge of a page.

> **Thinking prompt:** Can you think of a place on a real website where vertical text would look better than horizontal text?

**Ideas:** Column headers in a very narrow data table, decorative side labels in a hero banner, chapter labels running along the side of a long article, or section dividers in a vertical timeline.

---

## Section 6 — Complete Properties Reference Table

| Property | Values | What It Controls |
|---|---|---|
| `text-overflow` | `clip`, `ellipsis` | How to signal hidden overflow text to the user |
| `word-wrap` | `normal`, `break-word` | Whether long words can break and wrap to the next line |
| `word-break` | `normal`, `break-all`, `keep-all` | Line-breaking rules for all words |
| `writing-mode` | `horizontal-tb`, `vertical-rl`, `vertical-lr` | Whether text flows horizontally or vertically |
| `text-justify` | `auto`, `inter-word`, `inter-character`, `none` | How justified text is aligned and spaced |

### About `text-justify`

The `text-justify` property controls how the browser distributes space in **justified text** (`text-align: justify`). It is a companion property to `text-align: justify`:

- `auto` — lets the browser decide the best method
- `inter-word` — adds extra space between words only
- `inter-character` — adds extra space between individual characters
- `none` — disables justification

```css
p {
  text-align: justify;
  text-justify: inter-word;   /* space distributed between words */
}
```

---

## Guided Practice Exercises

### Exercise 1 — Product Title Truncation (Warm-Up)

**Objective:** Apply `text-overflow: ellipsis` to create a product title that fits neatly inside a fixed-width card.

**Scenario:** You are building a product grid for an online store. Each product card is 180px wide. Product titles must never overflow their cards — instead, truncate with `...`.

**Steps:**
1. Create a `div` with class `product-card`, width `180px`, border, padding `10px`
2. Inside it, put an `h3` with a long product title
3. Style the `h3` with `width: 100%`, `white-space: nowrap`, `overflow: hidden`, and `text-overflow: ellipsis`

**Hint:** All three properties (`white-space`, `overflow`, `text-overflow`) must be present.

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .product-card {
      width: 180px;
      border: 1px solid #ccc;
      padding: 10px;
      background-color: #fff;
      box-shadow: 2px 2px 6px rgba(0,0,0,0.1);
      border-radius: 6px;
    }

    .product-card h3 {
      margin: 0;
      font-size: 14px;
      white-space: nowrap;        /* keep title on one line */
      overflow: hidden;           /* hide what doesn't fit */
      text-overflow: ellipsis;    /* show "..." at the cut */
    }

    .product-card p {
      font-size: 13px;
      color: #555;
      margin: 6px 0 0 0;
    }
  </style>
</head>
<body>

  <div class="product-card">
    <h3>Ultra Premium Deluxe Executive Wireless Ergonomic Mouse</h3>
    <p>$49.99</p>
  </div>

</body>
</html>
```

**Expected output:**
```
┌──────────────────────┐
│ Ultra Premium Delu…  │
│ $49.99               │
└──────────────────────┘
```

**Self-check Questions:**
- What happens if you remove `white-space: nowrap`?
- What happens if you remove `overflow: hidden`?
- What happens if you change `ellipsis` to `clip`?

---

### Exercise 2 — Fixing a Long URL in a Narrow Column

**Objective:** Use `word-wrap: break-word` to prevent a long URL from overflowing a narrow sidebar.

**Scenario:** A website sidebar shows recently visited links. Some URLs are very long. Without fixing, they overflow and break the layout.

**Steps:**
1. Create a `div` with class `sidebar`, width `200px`, border
2. Inside, add a `p` tag containing a very long URL (e.g., `https://www.example-website.com/very/long/path/to/some/deeply/nested/page`)
3. First view it WITHOUT `word-wrap` (see the overflow)
4. Then add `word-wrap: break-word` to fix it

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .sidebar {
      width: 200px;
      border: 2px solid steelblue;
      padding: 10px;
      background-color: #f0f7ff;
      font-size: 13px;
    }

    /* Try commenting this out to see the broken version */
    .sidebar p {
      word-wrap: break-word;
    }
  </style>
</head>
<body>

  <div class="sidebar">
    <strong>Recent Links:</strong>
    <p>https://www.example-website.com/very/long/path/to/some/deeply/nested/page</p>
    <p>https://another-site.org/resources/documentation/css-text-properties</p>
  </div>

</body>
</html>
```

**Expected output (with word-wrap):**
```
┌──────────────────────┐
│ Recent Links:        │
│ https://www.example- │
│ website.com/very/lon │
│ g/path/to/some/deepl │
│ y/nested/page        │
└──────────────────────┘
```

**Self-check Questions:**
- What does the layout look like WITHOUT `word-wrap: break-word`?
- Could you use `text-overflow: ellipsis` instead? What would be different about the user experience?
- Why is `word-wrap` better here than `text-overflow`?

---

### Exercise 3 — Comparing `word-break` Values Side by Side

**Objective:** Build three paragraphs using the same content but different `word-break` values so you can visually compare all three behaviours.

**Steps:**
1. Create three `p` elements, each with width `180px` and a border
2. Use `word-break: normal`, `word-break: break-all`, and `word-break: keep-all`
3. Use the same long content in each: `"This is a short sentence. Thenthislongwordhas nospaces init."`
4. Label each paragraph with its value

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      width: 180px;
      border: 1px solid #333;
      padding: 8px;
      margin-bottom: 20px;
      background-color: #fffde7;
      font-size: 14px;
    }

    .normal    { word-break: normal; }
    .break-all { word-break: break-all; }
    .keep-all  { word-break: keep-all; }
  </style>
</head>
<body>

  <h3>normal:</h3>
  <p class="normal">
    This is a short sentence. Thenthislongwordhasnospacesinit.
  </p>

  <h3>break-all:</h3>
  <p class="break-all">
    This is a short sentence. Thenthislongwordhasnospacesinit.
  </p>

  <h3>keep-all:</h3>
  <p class="keep-all">
    This is a short sentence. Thenthislongwordhasnospacesinit.
  </p>

</body>
</html>
```

**Self-check Questions:**
- In `normal` mode, does the long word overflow?
- In `break-all` mode, are even normal words split mid-character?
- In `keep-all` mode, does anything overflow?
- For a comment section on a social media app, which value would be safest to use?

---

### Exercise 4 — Vertical Text Label for a Sidebar Navigation

**Objective:** Use `writing-mode: vertical-rl` to create a rotated sidebar category label.

**Scenario:** You are building a magazine-style webpage. The sidebar has vertical category labels (like "TECHNOLOGY", "HEALTH", "SPORTS") running top to bottom beside their article sections.

**Steps:**
1. Create a `div` with class `sidebar-label`
2. Style it: background colour, padding, small height, `writing-mode: vertical-rl`
3. Put a text label inside it (e.g., "TECHNOLOGY")

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: sans-serif;
      display: flex;
      gap: 20px;
      padding: 20px;
    }

    .sidebar-label {
      writing-mode: vertical-rl;  /* text flows top to bottom */
      background-color: #2c3e50;
      color: white;
      padding: 12px 8px;
      font-size: 13px;
      font-weight: bold;
      letter-spacing: 2px;
      text-transform: uppercase;
      border-radius: 4px;
    }

    .article-content {
      flex: 1;
      border: 1px solid #ccc;
      padding: 16px;
      background-color: #fafafa;
    }
  </style>
</head>
<body>

  <div class="sidebar-label">Technology</div>

  <div class="article-content">
    <h2>Latest Tech News</h2>
    <p>This is the article content area. The label to the left runs vertically
    using writing-mode: vertical-rl, giving the page a magazine-style layout.</p>
  </div>

</body>
</html>
```

**Expected output:**
```
┌───┐ ┌─────────────────────────────────┐
│ T │ │ Latest Tech News                │
│ e │ │                                 │
│ c │ │ This is the article content     │
│ h │ │ area. The label to the left     │
│ n │ │ runs vertically using           │
│ o │ │ writing-mode: vertical-rl...    │
│ l │ └─────────────────────────────────┘
│ o │
│ g │
│ y │
└───┘
```

**Self-check Questions:**
- Try `writing-mode: vertical-lr` — what changes?
- Try `writing-mode: horizontal-tb` — what happens to the label?
- Can you add a second sidebar label for "Health" beside the first?

---

## Mini Project — Styled Content Cards with All Four Text Effects

Now we combine everything from this lesson into one polished, realistic project. We will build a set of **content cards** that a news website or blog might use — incorporating all four text effect properties.

### Project Overview

We will create three article preview cards, each demonstrating a different challenge and solution:
- **Card 1:** `text-overflow: ellipsis` for a truncated headline
- **Card 2:** `word-wrap: break-word` for handling a long URL source citation
- **Card 3:** `writing-mode: vertical-rl` for a rotated category label

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html>
<head>
  <title>News Cards — CSS Text Effects</title>
</head>
<body>

  <div class="card-grid">

    <!-- Card 1: text-overflow ellipsis -->
    <div class="card card-1">
      <div class="category-label">BREAKING</div>
      <h3 class="card-title">Scientists Discover New Planet That May Support Human Life Beyond The Solar System</h3>
      <p class="card-excerpt">Researchers at the International Space Agency announced a groundbreaking discovery today...</p>
      <span class="card-source">space.com</span>
    </div>

    <!-- Card 2: word-wrap -->
    <div class="card card-2">
      <div class="category-label">TECH</div>
      <h3 class="card-title">AI Research Update</h3>
      <p class="card-excerpt">Read the full technical report at this address...</p>
      <span class="card-source">https://research.openai.com/papers/technical-documentation/ai-report-2026-final-version</span>
    </div>

    <!-- Card 3: writing-mode vertical label -->
    <div class="card card-3">
      <div class="vertical-label">HEALTH</div>
      <div class="card-body">
        <h3 class="card-title">Daily Walking Reduces Heart Disease Risk By 40%</h3>
        <p class="card-excerpt">A new study from Harvard Medical School confirms that 30 minutes of walking per day...</p>
        <span class="card-source">health.gov</span>
      </div>
    </div>

  </div>

</body>
</html>
```

### Stage 2 — CSS Styles

```css
/* ===================== */
/* Base Layout */
/* ===================== */
body {
  font-family: 'Segoe UI', sans-serif;
  background-color: #f2f4f7;
  padding: 30px;
}

.card-grid {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

/* ===================== */
/* Shared Card Styles */
/* ===================== */
.card {
  background-color: white;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  padding: 16px;
  width: 240px;
  box-sizing: border-box;
}

.category-label {
  font-size: 11px;
  font-weight: bold;
  color: white;
  background-color: #e74c3c;
  display: inline-block;
  padding: 3px 8px;
  border-radius: 3px;
  margin-bottom: 10px;
  letter-spacing: 1px;
}

.card-title {
  font-size: 15px;
  margin: 0 0 10px 0;
  color: #2c3e50;
  line-height: 1.4;
}

.card-excerpt {
  font-size: 13px;
  color: #555;
  margin: 0 0 10px 0;
}

.card-source {
  font-size: 11px;
  color: #888;
  display: block;
}

/* ===================== */
/* Card 1: text-overflow */
/* ===================== */
.card-1 .card-title {
  /* The title is very long — truncate with ellipsis */
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

/* ===================== */
/* Card 2: word-wrap */
/* ===================== */
.card-2 .card-source {
  /* The source URL is very long — allow it to wrap */
  word-wrap: break-word;
  font-size: 10px;
  color: steelblue;
}

/* ===================== */
/* Card 3: writing-mode */
/* ===================== */
.card-3 {
  display: flex;
  gap: 12px;
  padding: 12px;
}

.vertical-label {
  writing-mode: vertical-rl;    /* text flows top to bottom */
  font-size: 11px;
  font-weight: bold;
  color: white;
  background-color: #27ae60;
  padding: 8px 5px;
  border-radius: 4px;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.card-3 .card-body {
  flex: 1;
}
```

### Stage 3 — Complete Final Code

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #f2f4f7;
      padding: 30px;
    }

    .card-grid {
      display: flex;
      gap: 20px;
      flex-wrap: wrap;
    }

    .card {
      background-color: white;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      padding: 16px;
      width: 240px;
      box-sizing: border-box;
    }

    .category-label {
      font-size: 11px;
      font-weight: bold;
      color: white;
      background-color: #e74c3c;
      display: inline-block;
      padding: 3px 8px;
      border-radius: 3px;
      margin-bottom: 10px;
      letter-spacing: 1px;
    }

    .card-title {
      font-size: 15px;
      margin: 0 0 10px 0;
      color: #2c3e50;
      line-height: 1.4;
    }

    .card-excerpt {
      font-size: 13px;
      color: #555;
      margin: 0 0 10px 0;
    }

    .card-source {
      font-size: 11px;
      color: #888;
      display: block;
    }

    /* Card 1 — text-overflow ellipsis on headline */
    .card-1 .card-title {
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    /* Card 2 — word-wrap on long URL */
    .card-2 .card-source {
      word-wrap: break-word;
      font-size: 10px;
      color: steelblue;
    }

    /* Card 3 — vertical writing-mode label */
    .card-3 {
      display: flex;
      gap: 12px;
      padding: 12px;
    }

    .vertical-label {
      writing-mode: vertical-rl;
      font-size: 11px;
      font-weight: bold;
      color: white;
      background-color: #27ae60;
      padding: 8px 5px;
      border-radius: 4px;
      letter-spacing: 2px;
      text-transform: uppercase;
    }

    .card-3 .card-body {
      flex: 1;
    }
  </style>
</head>
<body>

  <h2>Latest Articles</h2>

  <div class="card-grid">

    <!-- Card 1: text-overflow: ellipsis -->
    <div class="card card-1">
      <div class="category-label">BREAKING</div>
      <h3 class="card-title">Scientists Discover New Planet That May Support Human Life Beyond The Solar System</h3>
      <p class="card-excerpt">Researchers at the International Space Agency announced a groundbreaking discovery today that could change humanity forever.</p>
      <span class="card-source">space.com</span>
    </div>

    <!-- Card 2: word-wrap: break-word -->
    <div class="card card-2">
      <div class="category-label">TECH</div>
      <h3 class="card-title">AI Research Update 2026</h3>
      <p class="card-excerpt">Read the full technical report at this address:</p>
      <span class="card-source">https://research.openai.com/papers/technical-documentation/ai-full-report-2026-final</span>
    </div>

    <!-- Card 3: writing-mode: vertical-rl -->
    <div class="card card-3">
      <div class="vertical-label">Health</div>
      <div class="card-body">
        <h3 class="card-title">Daily Walking Reduces Heart Disease Risk</h3>
        <p class="card-excerpt">A new study confirms that 30 minutes of walking per day significantly reduces cardiovascular disease risk.</p>
        <span class="card-source">health.gov</span>
      </div>
    </div>

  </div>

</body>
</html>
```

**Milestone output:** Three polished news cards side by side. Card 1 shows a truncated headline with `...`. Card 2 shows a long URL wrapping neatly across multiple lines. Card 3 shows the category label running vertically down the left side.

**Reflection Questions:**
- Card 1 uses `text-overflow: ellipsis` on the headline. What would happen if you also added the hover-reveal trick (`p:hover { overflow: visible; }`) to show the full headline on hover?
- What would Card 2 look like if you used `word-break: break-all` instead of `word-wrap: break-word`? Would the result look different?
- Can you add a fourth card that uses `writing-mode: horizontal-tb` (normal) and `word-break: break-all` to display a code snippet or serial number?

**Optional Advanced Extensions:**
- Add a `transition` to Card 1's title so the overflow change on hover animates smoothly
- Try giving Card 3's vertical label a `transform: rotate(180deg)` to make the text read from bottom to top instead of top to bottom
- Add a tooltip to Card 1 using the `title` HTML attribute so the full headline is accessible even when truncated

---

## Common Beginner Mistakes

### Mistake 1 — Using `text-overflow` Without `white-space: nowrap` and `overflow: hidden`

```css
/* WRONG — text-overflow does nothing without its companions */
p {
  width: 200px;
  text-overflow: ellipsis;    /* ← this has NO effect alone */
}

/* CORRECT — all three must work together */
p {
  width: 200px;
  white-space: nowrap;        /* step 1: stop wrapping */
  overflow: hidden;           /* step 2: hide the overflow */
  text-overflow: ellipsis;    /* step 3: signal the cut-off */
}
```

**Why it matters:** `text-overflow` only applies to text that has already overflowed and been hidden. Without `overflow: hidden`, there is nothing to signal. Without `white-space: nowrap`, the text wraps naturally and never overflows in the first place.

---

### Mistake 2 — Confusing `word-wrap` and `word-break`

```css
/* Beginners often use these interchangeably — they are not the same */

/* word-wrap: break-word — gentle: only breaks words that are TOO LONG */
p { word-wrap: break-word; }

/* word-break: break-all — aggressive: breaks EVERY word at EVERY line end */
p { word-break: break-all; }
```

**Rule of thumb:**
- Use `word-wrap: break-word` for user-generated content and body text
- Only use `word-break: break-all` for compact technical displays like code or serial numbers

---

### Mistake 3 — Forgetting That `text-overflow` Only Affects Inline Overflow

`text-overflow` only works for text that overflows **horizontally** in a single-line context. It does not work for text that overflows **vertically** (too many lines).

```css
/* text-overflow works here — single line, horizontal overflow */
p {
  width: 200px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;   /* ✓ works */
}

/* text-overflow does NOT help here — multi-line, vertical overflow */
p {
  width: 200px;
  height: 50px;        /* fixed height — text overflows vertically */
  overflow: hidden;
  text-overflow: ellipsis;   /* ✗ has no effect on vertical overflow */
}
```

For multi-line ellipsis (cutting text after 2 or 3 lines), you need the `-webkit-line-clamp` technique — a more advanced topic.

---

### Mistake 4 — Applying `writing-mode` to Block Elements Without Layout Adjustment

When you change `writing-mode` on a block element, its width and height meanings can be swapped, confusing beginners.

```css
/* This might look unexpected — width and height swap meaning in vertical mode */
p {
  width: 100px;        /* in vertical-rl, this controls the HEIGHT */
  writing-mode: vertical-rl;
}
```

**Tip:** When using `writing-mode` on block elements, always test in the browser and check that padding, width, and height values look right. The safest approach for beginners is to apply `writing-mode` to `inline-block` or `flex` items where you can control sizing more predictably.

---

### Mistake 5 — Expecting `word-break: keep-all` to Work Like `word-wrap`

```css
/* keep-all PREVENTS breaks — it will CAUSE overflow for long words */
p {
  width: 200px;
  word-break: keep-all;    /* long words will OVERFLOW, not wrap */
}
```

`keep-all` is not a solution for preventing overflow. It is a directive saying "do not break words" — which can actually CAUSE overflow. Use `word-wrap: break-word` if you want long words to wrap without overflow.

---

## Reflection Questions

Think carefully about these questions:

1. Why does `text-overflow: ellipsis` require both `white-space: nowrap` AND `overflow: hidden` to work? What is the role of each companion property?

2. You are building a comment section for a website where users can type anything. Which `word-wrap` or `word-break` value would you choose to prevent layout-breaking comments? Why?

3. What is the key difference in behaviour between `word-wrap: break-word` and `word-break: break-all`? Give an example scenario where each is the better choice.

4. Name three real-world contexts (websites, apps, or documents) where `writing-mode: vertical-rl` would be appropriate or useful.

5. If a `<p>` element has `overflow: hidden` but no `text-overflow` set, what does the user see? Is there any visual indicator that text has been cut off?

6. Can you use `text-overflow` and `word-wrap` together on the same element? What would the combined effect be?

---

## Completion Checklist

Go through this checklist to confirm you have mastered this lesson:

- [ ] I understand what `text-overflow` does and know its two main values: `clip` and `ellipsis`
- [ ] I know that `text-overflow` requires `white-space: nowrap` and `overflow: hidden` to work
- [ ] I can implement the hover-reveal pattern to show full text on `:hover`
- [ ] I understand what `word-wrap: break-word` does and when to use it
- [ ] I know the difference between `word-wrap` and `word-break`
- [ ] I understand all three `word-break` values: `normal`, `break-all`, `keep-all`
- [ ] I understand what `writing-mode` does and know its three values: `horizontal-tb`, `vertical-rl`, `vertical-lr`
- [ ] I can apply `writing-mode: vertical-rl` to create a rotated label
- [ ] I have completed all four guided practice exercises
- [ ] I have completed the mini project (news article cards)
- [ ] I know at least three common beginner mistakes to avoid

---

## Lesson Summary

CSS Text Effect properties give you precise control over how text behaves when it doesn't fit neatly in its container or when it needs to flow in an unconventional direction.

`text-overflow` controls what users see when text is hidden due to overflow. The two useful values are `clip` (text simply stops) and `ellipsis` (shows `...` at the cut). It must always be used together with `white-space: nowrap` and `overflow: hidden` to function.

`word-wrap: break-word` is a gentle permission slip for the browser to split long words across lines when they are too long to fit — used with regular text, emails, URLs, and user-generated content.

`word-break` gives more granular control over line-breaking rules. `normal` uses default language rules, `break-all` breaks at any character aggressively, and `keep-all` prevents any word breaking.

`writing-mode` changes the fundamental flow of text. `horizontal-tb` is the default (left-to-right, top-to-bottom). `vertical-rl` flows top-to-bottom with columns from right to left — used in Japanese/Chinese typography and creative web layouts. `vertical-lr` flows top-to-bottom with columns from left to right.

Together, these four properties give you complete mastery over text that might otherwise overflow, break, or need to be displayed in non-traditional directions.

| Property | Use When... |
|---|---|
| `text-overflow: ellipsis` | Text in a fixed container must be truncated with a visual indicator |
| `word-wrap: break-word` | Long single words or URLs might overflow their container |
| `word-break: break-all` | You need aggressive character-level line breaking for dense content |
| `writing-mode: vertical-rl` | Text needs to run vertically for design or language reasons |

> **Next lesson:** CSS Custom Fonts — where you will learn how to load and use any font on the web using `@font-face` and Google Fonts, bringing typographic creativity to your projects.
