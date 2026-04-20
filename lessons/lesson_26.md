---
render_with_liquid: false
title: "CSS display: inline-block — The Best of Both Worlds"
nav_order: 26
---

# Lesson 26 — CSS `display: inline-block`

---

## Lesson Introduction

Have you ever wanted an element to sit **side by side** with other elements (like text or buttons), but also be able to control its **exact width, height, and spacing**? That sounds like a contradiction — and for a long time, web developers had to choose one or the other. Then came `display: inline-block`, which gives you **both superpowers at once**.

In this lesson you will learn:
- What `inline`, `block`, and `inline-block` mean, from scratch
- Exactly how `display: inline-block` combines the best features of both
- How to compare all three display types with working code examples
- How to build a real horizontal navigation menu using `inline-block`
- How to avoid the most common beginner mistakes

By the end of this lesson, you will be able to confidently lay out elements side by side while still controlling their size and spacing — a skill used in almost every real-world website.

---

## Prerequisite Concepts

Before diving into `inline-block`, let's make sure you understand three simpler ideas it builds on. Think of these as the building blocks you need before assembling something more powerful.

### 1. What is the CSS `display` Property?

Every HTML element is a **box** on the screen. The `display` property in CSS controls **how that box behaves** — specifically, whether it sits alone on its own line, or shares a line with other elements.

```css
/* General pattern */
selector {
  display: value;
}
```

The most common display values you will encounter are:
- `inline`
- `block`
- `inline-block`

### 2. What is a Block Element?

A **block element** acts like a large box that takes up the **full width** of its container. It always starts on a **new line** and pushes everything else above and below it.

**Common block elements:** `<div>`, `<p>`, `<h1>` to `<h6>`, `<section>`, `<article>`

**Analogy:** Think of a block element like a paragraph in a book. Each paragraph begins on a new line and stretches across the full width of the page.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      background-color: lightblue;
      border: 2px solid blue;
      padding: 10px;
    }
  </style>
</head>
<body>
  <div>I am Block Box 1</div>
  <div>I am Block Box 2</div>
  <div>I am Block Box 3</div>
</body>
</html>
```

**Expected Output (visually):**
```
[ I am Block Box 1 ————————————————————————— ]
[ I am Block Box 2 ————————————————————————— ]
[ I am Block Box 3 ————————————————————————— ]
```
Each box is on its own line and stretches to full width.

**Key rules for block elements:**
- Start on a new line ✅
- Stretch to full width ✅
- You can set `width`, `height`, `margin-top`, `margin-bottom` ✅

### 3. What is an Inline Element?

An **inline element** flows **inside text** — it sits on the same line as surrounding content, and its size is determined only by the content inside it.

**Common inline elements:** `<span>`, `<a>`, `<strong>`, `<em>`, `<img>`

**Analogy:** Think of an inline element like a single word highlighted in a sentence. It doesn't break the flow of the paragraph; it just highlights part of it.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    span {
      background-color: yellow;
      border: 2px solid orange;
      padding: 5px;
    }
  </style>
</head>
<body>
  <p>I love <span>CSS</span> and <span>web design</span> a lot.</p>
</body>
</html>
```

**Expected Output (visually):**
```
I love [CSS] and [web design] a lot.
```
Both spans sit inside the sentence on the same line.

**Key rules for inline elements:**
- Stay on the same line as surrounding content ✅
- Size is only as big as the content inside them ✅
- You **cannot** set `width`, `height`, `margin-top`, or `margin-bottom` ❌

> **💡 Why can't you set width/height on inline elements?** Because inline elements are designed to flow inside text. Giving them a fixed width would break the natural text flow. This is a frustrating limitation — and `inline-block` was created to solve it!

---

## Conceptual Understanding

### What is `display: inline-block`?

`display: inline-block` is a **hybrid** display type that combines the most useful features of both `inline` and `block` elements.

**Here is the simple definition:**

> An `inline-block` element sits **on the same line** as other elements (like inline), BUT you can still set its **width, height, margin-top, and margin-bottom** (like block).

**Analogy:** Imagine you are building a shelf to display books. Each book stands upright next to the others (inline behaviour — side by side). But each book has its own specific height and width (block behaviour — controllable size). `inline-block` is exactly like that.

### The Three Display Types — Side by Side Comparison

| Feature | `inline` | `block` | `inline-block` |
|---|---|---|---|
| Sits on same line as others? | ✅ Yes | ❌ No (new line) | ✅ Yes |
| Stretches to full width? | ❌ No | ✅ Yes | ❌ No |
| You can set `width`? | ❌ No | ✅ Yes | ✅ Yes |
| You can set `height`? | ❌ No | ✅ Yes | ✅ Yes |
| You can set `margin-top`/`margin-bottom`? | ❌ No | ✅ Yes | ✅ Yes |
| You can set `padding`? | ⚠️ Partially | ✅ Yes | ✅ Yes |

> **💡 Think of it like this:**
> - `inline` = words in a sentence (flows with text, no size control)
> - `block` = paragraphs (own line, full control of size)
> - `inline-block` = buttons in a toolbar (side by side, full control of size)

---

## Simple Standalone Examples

### Example 1 — Comparing `inline`, `inline-block`, and `block` on `<span>` Elements

This is the most important example in this lesson. We will apply all three display values to three separate `<span>` elements and observe the different results.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Span A — default inline behaviour */
    span.a {
      display: inline;      /* This is the default for <span> */
      padding: 5px;
      border: 2px solid red;
    }

    /* Span B — inline-block: side by side BUT with size control */
    span.b {
      display: inline-block;
      width: 100px;         /* We CAN set width now! */
      height: 35px;         /* We CAN set height now! */
      padding: 5px;
      border: 2px solid red;
    }

    /* Span C — block: takes its own full line */
    span.c {
      display: block;
      width: 100px;
      height: 35px;
      padding: 5px;
      border: 2px solid red;
    }
  </style>
</head>
<body>

  <h2>display: inline</h2>
  <span class="a">Hello!</span>
  <span class="a">World!</span>
  <span class="a">CSS!</span>

  <h2>display: inline-block</h2>
  <span class="b">Hello!</span>
  <span class="b">World!</span>
  <span class="b">CSS!</span>

  <h2>display: block</h2>
  <span class="c">Hello!</span>
  <span class="c">World!</span>
  <span class="c">CSS!</span>

</body>
</html>
```

**Expected Output (visually):**

```
display: inline
[Hello!] [World!] [CSS!]       ← All on one line, size fits content

display: inline-block
[Hello!   ] [World!   ] [CSS!  ]  ← All on one line, all exactly 100px wide, 35px tall

display: block
[Hello!           ]
[World!           ]
[CSS!             ]            ← Each on its own full line
```

**Breaking down the code — line by line:**

`display: inline;` — This is the natural default for `<span>`. The element flows like a word in text. Even though we set `padding` and `border`, the height and width cannot be explicitly controlled.

`display: inline-block;` — Now the element sits beside others on the same line, BUT the `width: 100px` and `height: 35px` we specified are actually applied. This is the new power!

`display: block;` — The element takes up its own full line. Even though it has `width: 100px`, it still forces a new line for the next element.

> **🤔 Thinking prompt:** What happens if you remove the `width` and `height` from `span.b`? Try it — the element will still sit inline but shrink to just fit its content, just like `inline`. Width and height are optional with `inline-block`.

---

### Example 2 — Why You Can't Control Size with `inline` (A Common Frustration)

This example shows the limitation of `inline` and why `inline-block` was invented.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    span.fail {
      display: inline;
      width: 200px;       /* This will be IGNORED by the browser */
      height: 50px;       /* This will also be IGNORED */
      background-color: lightgreen;
      padding: 5px;
    }

    span.success {
      display: inline-block;
      width: 200px;       /* This WORKS! */
      height: 50px;       /* This WORKS! */
      background-color: lightgreen;
      padding: 5px;
    }
  </style>
</head>
<body>

  <p>Inline (width and height are ignored):</p>
  <span class="fail">I wanted to be 200px wide...</span>

  <p>Inline-block (width and height are respected):</p>
  <span class="success">I am exactly 200px wide!</span>

</body>
</html>
```

**Expected Output (visually):**
```
Inline (width and height are ignored):
[I wanted to be 200px wide...]   ← Only as wide as the text content

Inline-block (width and height are respected):
[I am exactly 200px wide!        ]  ← Exactly 200px wide, 50px tall
```

This example proves the core value of `inline-block`: **you regain full size control without losing the side-by-side placement**.

---

## Using `inline-block` to Build a Horizontal Navigation Menu

One of the most common, practical uses for `display: inline-block` in real web development is creating **horizontal navigation menus** — the row of links you see at the top of most websites (Home | About | Services | Contact).

### Why `inline-block` for Navigation?

Normally, `<li>` list items are block elements. This means they stack vertically. To make them sit side by side in a horizontal menu, we change their `display` to `inline-block`. This also lets us apply padding around each link to give them a proper clickable area.

### Example 3 — A Horizontal Navigation Menu with `inline-block`

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Style the container (the <ul> list) */
    .nav {
      background-color: lightgray;  /* Gray background for the whole nav bar */
      list-style-type: none;        /* Remove bullet points from list items */
      padding: 0;                   /* Remove default padding */
      margin: 0;                    /* Remove default margin */
    }

    /* Style each menu item (each <li>) */
    .nav li {
      display: inline-block;   /* THIS is the key — makes list items sit side by side */
      font-size: 18px;
      padding: 15px;           /* Adds space around each menu item for a comfortable click area */
    }

    /* Optional: style the links inside */
    .nav li a {
      text-decoration: none;
      color: #333;
    }

    .nav li a:hover {
      color: royalblue;
    }
  </style>
</head>
<body>

  <ul class="nav">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Services</a></li>
    <li><a href="#">Portfolio</a></li>
    <li><a href="#">Contact</a></li>
  </ul>

</body>
</html>
```

**Expected Output (visually):**
```
[ Home ]  [ About ]  [ Services ]  [ Portfolio ]  [ Contact ]
(All items appear in a single horizontal row on a gray background)
```

**Breaking down the code — line by line:**

`list-style-type: none;` — Removes the default bullet points (`•`) that `<ul>` lists show by default. In a navigation bar, we don't want bullets.

`padding: 0; margin: 0;` — Browsers add default spacing around `<ul>` and `<li>` elements. We reset both to zero so we can control the spacing ourselves.

`display: inline-block;` — This single rule transforms the list items from stacking vertically to sitting horizontally in a row. Without this, all five nav items would appear in a vertical list.

`padding: 15px;` — Adds 15 pixels of space on all four sides of each nav item. This makes each item look like a proper button and gives users a comfortable area to click.

> **🌍 Real-World Connection:** Almost every website you visit uses this exact pattern (or a modern version of it with Flexbox) for their navigation bar. The header menu of news websites, online shops, and business sites all use horizontal navigation built with techniques like this.

> **🤔 Thinking prompt:** What happens if you change `display: inline-block` to `display: block` in the `.nav li` rule? Try it — the menu items will go back to stacking vertically like a standard list.

---

## Guided Practice Exercises

### Exercise 1 — Warm-Up: Spot the Difference

**Objective:** Understand visually how `inline` vs `inline-block` behaves differently.

**Scenario:** You are building a small widget that shows three status labels for a weather app: "Sunny", "Windy", and "Rainy".

**Your task:** Write the HTML and CSS below, then **change `display: inline-block` to `display: inline`** and observe how the boxes lose their set height.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .label {
      display: inline-block;   /* Change this to inline and observe */
      width: 80px;
      height: 40px;
      background-color: #4a90d9;
      color: white;
      text-align: center;
      line-height: 40px;       /* Vertically centers text inside the 40px height */
      margin: 5px;
      border-radius: 5px;
    }
  </style>
</head>
<body>
  <span class="label">Sunny</span>
  <span class="label">Windy</span>
  <span class="label">Rainy</span>
</body>
</html>
```

**Expected Output (with `inline-block`):**
```
[ Sunny ]  [ Windy ]  [ Rainy ]
(Three equally-sized blue pill-shaped labels side by side)
```

**Expected Output (if you switch to `inline`):**
```
[Sunny][Windy][Rainy]
(The width and height settings are ignored — boxes shrink to text size only)
```

**Self-check Questions:**
1. Did the height change when you switched to `inline`?
2. Is the text still centered vertically when you use `inline`? Why not?
3. What does `line-height: 40px` do? (Hint: it matches the `height` value.)

---

### Exercise 2 — Build a Button Row

**Objective:** Use `inline-block` to create a row of styled action buttons.

**Scenario:** You are building a simple order management panel. You need three buttons — "Approve", "Reject", and "Hold" — to appear in a horizontal row with consistent sizing.

**Steps:**

1. Create an HTML file with three `<a>` tags (links styled as buttons).
2. Apply `display: inline-block` to each button.
3. Set a specific `width` of `120px` and `height` of `40px` for each.
4. Add `background-color`, `color`, `text-align: center`, and `line-height: 40px` for styling.

**Starter Code:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .btn {
      display: inline-block;
      width: 120px;
      height: 40px;
      text-align: center;
      line-height: 40px;        /* Centers text vertically */
      text-decoration: none;
      font-size: 16px;
      border-radius: 4px;
      margin: 5px;
    }

    .btn-approve {
      background-color: #27ae60;  /* Green */
      color: white;
    }

    .btn-reject {
      background-color: #e74c3c;  /* Red */
      color: white;
    }

    .btn-hold {
      background-color: #f39c12;  /* Orange */
      color: white;
    }
  </style>
</head>
<body>
  <h3>Order #1042 — Pending Review</h3>

  <a href="#" class="btn btn-approve">Approve</a>
  <a href="#" class="btn btn-reject">Reject</a>
  <a href="#" class="btn btn-hold">Hold</a>
</body>
</html>
```

**Expected Output (visually):**
```
Order #1042 — Pending Review

[ Approve ]  [ Reject ]  [ Hold ]
  (green)     (red)      (orange)
  120px wide, 40px tall each, all on one line
```

**Hints:**
- If the buttons are stacking vertically, make sure `display: inline-block` is set on `.btn`.
- If text is not centered vertically, check that `line-height` equals the `height` value.
- If the buttons are too close together, increase the `margin` value.

**What-if challenge:** What happens if you set `width: 100%` on `.btn`? Try it and observe. Can you explain why the buttons stack vertically when you do that?

---

### Exercise 3 — Build a Simple Icon Toolbar

**Objective:** Combine `inline-block` with text and emoji content to make a toolbar.

**Scenario:** You are building a simple text-editor toolbar with formatting buttons: Bold, Italic, Underline, and Link.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .toolbar {
      background-color: #f5f5f5;
      border: 1px solid #ccc;
      padding: 8px;
      border-radius: 4px;
    }

    .tool-btn {
      display: inline-block;
      width: 36px;
      height: 36px;
      line-height: 36px;
      text-align: center;
      background-color: white;
      border: 1px solid #ccc;
      border-radius: 3px;
      cursor: pointer;
      margin: 2px;
      font-weight: bold;
    }

    .tool-btn:hover {
      background-color: #dce8ff;
      border-color: #4a90d9;
    }
  </style>
</head>
<body>
  <div class="toolbar">
    <span class="tool-btn">B</span>
    <span class="tool-btn"><em>I</em></span>
    <span class="tool-btn"><u>U</u></span>
    <span class="tool-btn">🔗</span>
  </div>
</body>
</html>
```

**Expected Output (visually):**
```
┌──────────────────────────────────┐
│  [B]  [I]  [U]  [🔗]            │
└──────────────────────────────────┘
(Four square buttons, side by side, in a toolbar container)
```

**Self-check Questions:**
1. What would happen if you removed `display: inline-block` from `.tool-btn`?
2. Why do we set both `height: 36px` and `line-height: 36px` to the same value?
3. What does `cursor: pointer` do? (Try removing it and notice the cursor change.)

---

## Mini Project — Building a Complete Website Navigation Bar

Now you will bring everything together to build a full, styled navigation bar for a fictional tech company called **"NovaTech"**.

### Project Overview

You will build a horizontal navigation bar that includes the company name on the left and a list of nav links on the right. All nav links will be made with `display: inline-block`.

---

### Stage 1 — Setup: The HTML Structure

```html
<!DOCTYPE html>
<html>
<head>
  <title>NovaTech — Navigation Bar</title>
  <link rel="stylesheet" href="navbar.css">
</head>
<body>

  <nav class="navbar">

    <!-- Left side: Company name -->
    <span class="brand">NovaTech</span>

    <!-- Right side: Navigation links -->
    <ul class="nav-links">
      <li><a href="#">Home</a></li>
      <li><a href="#">Products</a></li>
      <li><a href="#">Solutions</a></li>
      <li><a href="#">Pricing</a></li>
      <li><a href="#" class="cta-btn">Get Started</a></li>
    </ul>

  </nav>

</body>
</html>
```

**Milestone Output after Stage 1:** You should see plain unstyled text with a bullet list. That's fine — the CSS in Stage 2 will fix it.

---

### Stage 2 — Core Logic: Applying `inline-block` to the Nav

Create a file called `navbar.css` and add:

```css
/* Reset browser defaults */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

/* The nav container */
.navbar {
  background-color: #1a1a2e;     /* Dark navy background */
  padding: 0 30px;               /* Left and right padding only */
  height: 60px;                  /* Fixed height for the bar */
  line-height: 60px;             /* Vertically centers text in the 60px bar */
}

/* Company name on the left */
.brand {
  display: inline-block;         /* Allows it to sit beside the nav links */
  font-size: 22px;
  font-weight: bold;
  color: #e94560;                /* Bright red accent colour */
  letter-spacing: 1px;
}

/* The navigation list — float right to push links to the right side */
.nav-links {
  display: inline-block;
  float: right;                  /* Pushes the list to the right side of the bar */
  list-style-type: none;        /* No bullet points */
}

/* Each list item */
.nav-links li {
  display: inline-block;         /* THE KEY: side-by-side placement */
}

/* Each link inside a list item */
.nav-links li a {
  display: inline-block;
  padding: 0 18px;               /* Horizontal padding for spacing */
  color: #ccc;
  text-decoration: none;
  font-size: 15px;
  height: 60px;
  line-height: 60px;
  transition: color 0.2s;
}

.nav-links li a:hover {
  color: white;
}
```

**Milestone Output after Stage 2:**
```
┌───────────────────────────────────────────────────────────────────┐
│  NovaTech          Home  Products  Solutions  Pricing  Get Started │
└───────────────────────────────────────────────────────────────────┘
(Dark navy bar, company name left, nav links right, all on one line)
```

---

### Stage 3 — Enhancement: Style the "Get Started" Button

Add this to `navbar.css`:

```css
/* Special "Get Started" call-to-action button */
.cta-btn {
  background-color: #e94560;    /* Red background */
  color: white !important;      /* White text regardless of hover */
  padding: 8px 20px !important; /* Override the default link padding */
  border-radius: 4px;
  height: auto !important;
  line-height: normal !important;
  margin-top: 12px;             /* Slightly lower to vertically center within bar */
}

.cta-btn:hover {
  background-color: #c73652 !important;
}
```

**Milestone Output after Stage 3:**
```
┌───────────────────────────────────────────────────────────────────┐
│  NovaTech      Home  Products  Solutions  Pricing  [Get Started]  │
└───────────────────────────────────────────────────────────────────┘
(The "Get Started" link now appears as a bright red pill button)
```

---

### Stage 4 — Final Output (Complete Combined File)

Here is the full project in one file for easy testing:

```html
<!DOCTYPE html>
<html>
<head>
  <title>NovaTech — Navigation Bar</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    .navbar {
      background-color: #1a1a2e;
      padding: 0 30px;
      height: 60px;
      line-height: 60px;
    }

    .brand {
      display: inline-block;
      font-size: 22px;
      font-weight: bold;
      color: #e94560;
      letter-spacing: 1px;
    }

    .nav-links {
      display: inline-block;
      float: right;
      list-style-type: none;
    }

    .nav-links li {
      display: inline-block;
    }

    .nav-links li a {
      display: inline-block;
      padding: 0 18px;
      color: #ccc;
      text-decoration: none;
      font-size: 15px;
      height: 60px;
      line-height: 60px;
      transition: color 0.2s;
    }

    .nav-links li a:hover {
      color: white;
    }

    .cta-btn {
      background-color: #e94560;
      color: white !important;
      padding: 8px 20px !important;
      border-radius: 4px;
      height: auto !important;
      line-height: normal !important;
      margin-top: 12px;
    }

    .cta-btn:hover {
      background-color: #c73652 !important;
    }
  </style>
</head>
<body>

  <nav class="navbar">
    <span class="brand">NovaTech</span>
    <ul class="nav-links">
      <li><a href="#">Home</a></li>
      <li><a href="#">Products</a></li>
      <li><a href="#">Solutions</a></li>
      <li><a href="#">Pricing</a></li>
      <li><a href="#" class="cta-btn">Get Started</a></li>
    </ul>
  </nav>

  <p style="padding: 20px; color: #555;">Page content goes here...</p>

</body>
</html>
```

**Reflection Questions:**
1. Which CSS rule is the most important one for making the nav items appear horizontally?
2. What would happen if you forgot `list-style-type: none`?
3. Why did we set `height: 60px` and `line-height: 60px` to the same value on the `<a>` tags?

**Optional advanced extensions:**
- Add a dropdown menu that appears when you hover over "Products"
- Make the navbar responsive so it stacks vertically on small screens using a media query
- Add an active state (different colour) to the currently selected page link

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting That `inline-block` Still Has a Small Gap Between Elements

When you place multiple `inline-block` elements side by side, browsers add a tiny gap between them (usually 3–4px). This gap comes from **whitespace in the HTML** (the line breaks and spaces between your tags).

**The problem:**
```html
<span class="box">A</span>
<span class="box">B</span>
<span class="box">C</span>
```
```
[A] [B] [C]
     ↑ tiny gaps here
```

**Why this happens:** The browser sees the newline and space characters between `</span>` and `<span>` as text content — just like a space between two words.

**Fix Option 1 — Remove whitespace in HTML (not very readable):**
```html
<span class="box">A</span><span class="box">B</span><span class="box">C</span>
```

**Fix Option 2 — Use `font-size: 0` on the parent (clean approach):**
```css
.container {
  font-size: 0;          /* Eliminates the whitespace gap */
}
.box {
  display: inline-block;
  font-size: 16px;       /* Re-apply font size to the children */
}
```

**Fix Option 3 — Use negative margin:**
```css
.box {
  display: inline-block;
  margin-right: -4px;    /* Offsets the gap */
}
```

> **💡 Pro tip:** In modern projects, developers often use Flexbox (`display: flex`) to avoid this gap entirely. But `inline-block` is still important to understand and perfectly valid for many use cases.

---

### Mistake 2 — Trying to Use `width` and `height` on an `inline` Element

```css
/* WRONG — width and height are ignored on inline elements */
span {
  display: inline;
  width: 200px;    /* ← IGNORED by the browser */
  height: 50px;   /* ← IGNORED by the browser */
}

/* CORRECT — change to inline-block first */
span {
  display: inline-block;
  width: 200px;    /* ← Now this WORKS */
  height: 50px;   /* ← Now this WORKS */
}
```

---

### Mistake 3 — Confusing `inline-block` with `float`

Both `inline-block` and `float` can make elements appear side by side. But they work very differently:

| | `inline-block` | `float` |
|---|---|---|
| Element stays in document flow? | ✅ Yes | ❌ No (floated elements are pulled out of flow) |
| Causes layout issues with siblings? | ❌ Rarely | ✅ Often (needs clearfix) |
| Aligns vertically with siblings? | ✅ Yes (controlled by `vertical-align`) | ❌ Complex |
| Best used for | Buttons, nav items, inline content | Wrapping text around images |

**Rule of thumb:** Use `inline-block` for nav bars, button rows, and horizontal lists. Use `float` mainly for wrapping text around images.

---

### Mistake 4 — Forgetting `list-style-type: none` When Making Horizontal Nav Menus

```css
/* WRONG — bullet points will appear in your nav bar */
.nav li {
  display: inline-block;
  padding: 10px;
}

/* CORRECT — remove bullet points */
.nav {
  list-style-type: none;   /* Remove bullets from the list */
  padding: 0;
  margin: 0;
}

.nav li {
  display: inline-block;
  padding: 10px;
}
```

---

### Mistake 5 — Not Understanding Vertical Alignment

When multiple `inline-block` elements have different heights, they may not align the way you expect. By default, they align to their **baseline** (the bottom of text).

```css
/* Fix misaligned inline-block elements */
.box {
  display: inline-block;
  vertical-align: top;    /* Aligns tops of all boxes */
  /* Other options: middle, bottom, baseline */
}
```

**Example of the problem:**
```
[Short box]     [This is a
                 tall box with
                 more text]
↑ The short box aligns to the baseline of the tall box's text — looks uneven
```

**Fix:** Add `vertical-align: top` to align the tops of all boxes.

---

## Reflection Questions

1. **What is the core difference between `inline` and `inline-block`?** Write your answer in one sentence without looking above.

2. **Can you set `width: 300px` on a `<span>` element by default?** What do you need to change first?

3. **Why do we use `display: inline-block` on `<li>` elements in a navigation bar?** What would happen if we didn't?

4. **What causes the small gap between `inline-block` elements?** How can you fix it?

5. **Name two properties that work on `inline-block` but NOT on `inline` elements.**

6. **You have a row of three product cards that are `inline-block`. The middle card is taller than the others. They all look misaligned. What CSS property can you add to fix this?**

7. **You are building a data dashboard. You need to display 6 statistic boxes side by side, each exactly 150px wide and 100px tall. Which display value would you use and why?**

---

## Completion Checklist

Before moving on to the next lesson, confirm you can do all of the following:

- [ ] Explain in simple words what `display: inline` does
- [ ] Explain in simple words what `display: block` does
- [ ] Explain what `display: inline-block` gives you that neither `inline` nor `block` alone can
- [ ] Write CSS that makes a `<span>` have a specific `width` and `height` while staying on the same line as other elements
- [ ] Build a horizontal navigation menu from a `<ul>` list using `display: inline-block`
- [ ] Identify and fix the small gap that appears between `inline-block` elements
- [ ] Use `vertical-align` to control how `inline-block` elements align with each other
- [ ] Know when to prefer `inline-block` over `float`
- [ ] Complete the NovaTech mini-project navigation bar from scratch

---

## Lesson Summary

In this lesson, you mastered one of CSS's most useful layout tools: `display: inline-block`.

Here is what you learned, from the ground up:

**The problem `inline-block` solves:** You often want elements to sit side by side (like `inline`), but also control their exact size and spacing (like `block`). Neither `inline` alone nor `block` alone gives you both at once.

**The solution:** `display: inline-block` is a hybrid. It places elements on the same line as neighbouring content (inline behaviour), while allowing full control over `width`, `height`, `margin-top`, and `margin-bottom` (block behaviour).

**The three display types compared:**
- `inline` — flows with text, cannot control size
- `block` — full new line, full size control
- `inline-block` — stays on same line AND has full size control

**Most important real-world use:** Building horizontal navigation menus by applying `display: inline-block` to `<li>` elements in a `<ul>`, combined with `list-style-type: none` and appropriate padding.

**The whitespace gap quirk:** Multiple `inline-block` elements can have tiny gaps between them caused by whitespace in the HTML. Fix with `font-size: 0` on the parent or by removing whitespace between tags.

**CSS Property Reference:**

| Property | What it does |
|---|---|
| `display: inline` | Element flows with text, no size control |
| `display: block` | Element takes full width on its own line |
| `display: inline-block` | Element sits inline but accepts width, height, and vertical margins |
| `list-style-type: none` | Removes bullet points from `<ul>` and `<ol>` |
| `vertical-align` | Controls vertical alignment among `inline-block` siblings |

> **🌍 Real-World Significance:** `display: inline-block` is used in virtually every website for navigation bars, button rows, tag clouds, product grids, and toolbars. Understanding it deeply gives you a reliable tool that works in every browser without any additional frameworks.

---

*End of Lesson 26 — You are now ready to move on to CSS Alignment techniques in Lesson 27!*
