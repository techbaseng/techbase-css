---
render_with_liquid: false
title: "CSS Padding — Inner Space, Shorthand & the box-sizing Fix"
nav_order: 9
---

# Lesson 09 — CSS Padding: Creating Comfortable Space Inside Your Elements

---

## Lesson Introduction

Imagine a picture in a frame. The actual photograph is the content. But between the photograph and the hard edge of the frame, there is usually a small white border — a gap that stops the picture from feeling cramped. That gap is called a **mat** in framing. In CSS, the exact same idea is called **padding**.

Padding is the **space between an element's content and its border**. It lives *inside* the element, pushing the content away from the edges. Without padding, text and images would be pressed right up against the element's border — looking cramped, unreadable, and unprofessional.

Every button you have ever clicked, every card you have ever read, every navigation bar you have ever used — all of them rely on padding to breathe. Padding is one of the most frequently used CSS properties in all of web development.

By the end of this lesson you will be able to:

- Understand exactly what padding is and where it lives in the CSS Box Model
- Set padding on each individual side of an element (top, right, bottom, left)
- Use the `padding` shorthand to write all four sides in one line
- Use percentage values for padding
- Understand how padding interacts with `width` — and why adding padding can unexpectedly grow an element
- Solve that problem permanently with `box-sizing: border-box`
- Write clean, professional CSS that handles padding correctly every time

---

## Prerequisite Concepts

### The CSS Box Model — a quick reminder

Every HTML element is a rectangular box. That box has four layers:

```
┌─────────────────────────────────────┐
│              MARGIN                 │  ← Outside the element (space between elements)
│  ┌───────────────────────────────┐  │
│  │            BORDER             │  │  ← The visible edge/frame of the element
│  │  ┌─────────────────────────┐  │  │
│  │  │         PADDING         │  │  │  ← Space INSIDE the element, around content
│  │  │  ┌───────────────────┐  │  │  │
│  │  │  │      CONTENT      │  │  │  │  ← The actual text, image, or child elements
│  │  │  └───────────────────┘  │  │  │
│  │  └─────────────────────────┘  │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

This lesson focuses entirely on the **padding layer** — the space between the content and the border.

### Key distinction: Padding vs Margin

- **Padding** = space **inside** the element (between content and border) — part of the element itself; inherits the element's background colour
- **Margin** = space **outside** the element (between the border and neighbouring elements) — always transparent; shows the parent's background

> **Analogy:** A cardboard box. The **padding** is the bubble wrap inside that protects the item — it is *part of the box*. The **margin** is the empty space on the shelf between boxes — it belongs to the surrounding environment.

---

## Part 1 — Introduction to CSS Padding

### What is padding?

CSS `padding` properties add space **inside** an HTML element — between the element's content and its border. This inner breathing room makes content easier to read, makes buttons comfortable to click, and makes cards look polished.

### Why does it exist?

Without padding, every box of content would have text or images crammed right against its edges. Padding is the most direct way to create comfortable visual breathing room *within* an element without affecting the element's external spacing relationships.

### How padding works — the four sides

An element has four sides: top, right, bottom, and left. You can control each side's padding independently using four individual properties:

```css
element {
  padding-top:    value;
  padding-right:  value;
  padding-bottom: value;
  padding-left:   value;
}
```

### What values can padding use?

| Unit | Example | Meaning |
|---|---|---|
| `px` (pixels) | `padding: 20px` | Fixed pixel amount — most common for precise control |
| `%` (percentage) | `padding: 5%` | Percentage of the **parent element's width** — even for vertical padding |
| `em` | `padding: 1.5em` | Relative to the element's own font size |
| `rem` | `padding: 1rem` | Relative to the root (`html`) element's font size |

> ⚠️ **Important:** Padding values **cannot be negative**. If you need to pull an element inward, that is a different problem solved with different properties. Negative values on padding are invalid.

---

## Part 2 — Individual Padding Properties

### `padding-top`

Sets the padding space above the content, between the top of the content and the top border.

**Simple Example:**
```html
<style>
  p {
    padding-top: 50px;
    background-color: #def0ff;
    border: 2px solid #3399ff;
  }
</style>

<p>This paragraph has 50px of top padding.</p>
```

**Expected Output:**
The paragraph text has a large 50px gap between the top border and the start of the text. The light blue background fills that gap — confirming the padding is **inside** the element.

> **Thinking Prompt:** If padding is inside the element, the background colour fills the padding area. If you use `margin-top` instead, the space would be transparent (no background colour there). Try imagining the difference.

---

### `padding-right`

Sets padding space to the right of the content.

```css
p {
  padding-right: 30px;
  background-color: #def0ff;
}
```

**Expected Output:**
A 30px gap appears between the right edge of the text and the right border of the paragraph. The background colour fills this gap.

---

### `padding-bottom`

Sets padding space below the content.

```css
p {
  padding-bottom: 40px;
  background-color: #def0ff;
}
```

**Expected Output:**
A 40px gap appears between the last line of text and the bottom border of the element.

---

### `padding-left`

Sets padding space to the left of the content.

```css
p {
  padding-left: 80px;
  background-color: #def0ff;
}
```

**Expected Output:**
The paragraph text is indented 80px from the left border. The background colour fills that left gap.

---

### Example — All four sides set individually

```html
<style>
  div {
    padding-top:    25px;
    padding-right:  50px;
    padding-bottom: 25px;
    padding-left:   50px;
    background-color: #fffbe6;
    border: 2px solid #f5a623;
  }
</style>

<div>
  This box has 25px top/bottom padding and 50px left/right padding.
</div>
```

**Expected Output:**
The text has more horizontal breathing room (50px on each side) than vertical (25px on each side). The yellow background and orange border make the padding space clearly visible.

---

### Real-World Comparison — Button with and without padding

**Without padding (bad UX):**
```css
.btn {
  background-color: #007bff;
  color: white;
}
```
The button text would be cramped right against the edges — almost unreadable and very hard to click.

**With padding (good UX):**
```css
.btn {
  background-color: #007bff;
  color: white;
  padding-top:    12px;
  padding-right:  24px;
  padding-bottom: 12px;
  padding-left:   24px;
}
```
The button now has comfortable click area, readable text with clear breathing room, and a professional appearance.

---

## Part 3 — The `padding` Shorthand Property

Writing all four `padding-*` properties individually works but is repetitive. CSS provides a **shorthand** property called `padding` that sets all four sides in one declaration.

### Shorthand with 4 values

```css
padding: top  right  bottom  left;
```

The order is **clockwise starting from the top**: Top → Right → Bottom → Left.

A memory trick: **TRouBLe** — **T**op, **R**ight, **B**ottom, **L**eft.

```css
div {
  padding: 25px 50px 75px 100px;
}
```

- `padding-top:    25px`
- `padding-right:  50px`
- `padding-bottom: 75px`
- `padding-left:   100px`

**Expected Output:**
The div has different padding on all four sides. The bottom has the most space (75px) and the top has the least (25px).

---

### Shorthand with 3 values

```css
padding: top  right-and-left  bottom;
```

When you give 3 values: the first is top, the second applies to *both* right and left, the third is bottom.

```css
div {
  padding: 10px 30px 20px;
}
```

- `padding-top:    10px`
- `padding-right:  30px`
- `padding-bottom: 20px`
- `padding-left:   30px`  ← same as right

---

### Shorthand with 2 values

```css
padding: top-and-bottom  right-and-left;
```

When you give 2 values: the first sets top and bottom together, the second sets right and left together.

```css
div {
  padding: 20px 40px;
}
```

- `padding-top:    20px`
- `padding-right:  40px`
- `padding-bottom: 20px`  ← same as top
- `padding-left:   40px`  ← same as right

This is the most commonly used shorthand in real projects. It says: *"Give me this much vertical padding and that much horizontal padding."*

---

### Shorthand with 1 value

```css
padding: all-four-sides;
```

When you give 1 value, **all four sides** get the same padding.

```css
div {
  padding: 20px;
}
```

- `padding-top:    20px`
- `padding-right:  20px`
- `padding-bottom: 20px`
- `padding-left:   20px`

---

### Complete Visual Summary of Shorthand

```css
/* 4 values: top | right | bottom | left */
padding: 10px 20px 30px 40px;

/* 3 values: top | right+left | bottom */
padding: 10px 20px 30px;

/* 2 values: top+bottom | right+left */
padding: 10px 20px;

/* 1 value: all four sides */
padding: 10px;
```

> **Thinking Prompt:** Which shorthand would you use to create a button with 12px top/bottom padding and 24px left/right padding? *(Answer: `padding: 12px 24px;`)*

---

### Side-by-Side Examples with Expected Outputs

**Example A — Uniform card padding:**
```css
.card {
  padding: 24px;
  background-color: white;
  border: 1px solid #ddd;
}
```
**Output:** 24px of equal space on all four sides inside the card.

**Example B — Navigation link padding:**
```css
nav a {
  padding: 14px 20px;
  display: inline-block;
  background-color: #2c3e50;
  color: white;
}
```
**Output:** Navigation links have 14px top/bottom spacing (making them taller and easier to click) and 20px left/right spacing (making them wider and more distinct).

**Example C — Article content padding:**
```css
article {
  padding: 40px 60px 40px 60px;   /* or: padding: 40px 60px; */
  max-width: 800px;
}
```
**Output:** Article body content has generous horizontal padding (60px each side) to create a comfortable reading column, and vertical padding (40px) for top/bottom breathing room.

---

## Part 4 — Padding and Element Width: The Surprise Problem

### The critical problem you need to understand

This is one of the most confusing moments for beginners. Let's work through it carefully.

Suppose you create a `<div>` with a `width` of 300px and add some padding:

```css
div {
  width:   300px;
  padding: 25px;
  background-color: lightblue;
}
```

**Question:** How wide is the div on screen?

**Beginner's guess:** 300px.
**Actual answer (by default):** **350px** — because the padding is *added on top of* the width!

### Why does this happen?

By default, CSS uses a sizing model called **`content-box`** (the original CSS box model). In this model, the `width` property sets **only the content area** — it does not include padding or border. So when you add padding, the total rendered width becomes:

```
Total width = content-width + padding-left + padding-right + border-left + border-right
Total width = 300px + 25px + 25px + 0 + 0
Total width = 350px
```

Let's confirm this with a concrete example:

```html
<style>
  div.box1 {
    width: 300px;
    padding: 25px;
    background-color: lightblue;
    border: 1px solid steelblue;
  }
</style>

<div class="box1">
  I am supposed to be 300px wide!
</div>
```

**Expected Output:**
Despite `width: 300px`, the element visually measures **352px** wide (300px content + 25px left padding + 25px right padding + 1px left border + 1px right border = 352px).

> **Why is this a problem?** Imagine you are building a two-column layout where each column should be exactly 50% wide. If one column has padding added, it will overflow and break the layout, because its actual size exceeds 50%.

---

### Visualising the problem

```
content-box model (default — padding ADDS to the width):

│←─── 25px ───→│←── 300px content ──→│←─── 25px ───→│
│   padding-left │      CONTENT         │  padding-right │
│←──────────────── TOTAL: 350px ──────────────────────→│
```

---

## Part 5 — `box-sizing: border-box`: The Fix

### What is `box-sizing`?

`box-sizing` is a CSS property that controls **how an element's total size is calculated** — specifically, whether `width` and `height` refer to just the content area, or to the element's total rendered size including padding and border.

It has two values:

| Value | Meaning |
|---|---|
| `content-box` | Default. `width`/`height` = content only. Padding and border are *added* on top. |
| `border-box` | `width`/`height` = content + padding + border *all included*. Nothing is added. |

### `box-sizing: border-box` — the solution

With `border-box`, the `width` you set is the **final, total width** of the element. CSS then automatically shrinks the content area to make room for padding and border *inside* that total width. Nothing is added outside.

```html
<style>
  div.box2 {
    width: 300px;
    padding: 25px;
    background-color: lightblue;
    border: 1px solid steelblue;
    box-sizing: border-box;  /* ← the fix */
  }
</style>

<div class="box2">
  Now I am actually 300px wide!
</div>
```

**Expected Output:**
The element is exactly **300px** wide on screen. The padding (25px each side) and border (1px each side) are absorbed inside that 300px. The actual content area is shrunk to `300 - 25 - 25 - 1 - 1 = 248px` — but the *total element size* is exactly 300px.

### Visualising the fix

```
border-box model (padding INCLUDED in the width):

│← 25px →│←── 248px content ──→│← 25px →│
│  padding │      CONTENT          │ padding │
│←──────────── TOTAL: still 300px ─────────→│
```

---

### Comparing `content-box` vs `border-box` side by side

```css
/* CONTENT-BOX (default) — total size EXPANDS */
.box-content {
  width: 300px;
  padding: 25px;
  box-sizing: content-box;  /* default — no need to write this */
  /* Total rendered width: 300 + 25 + 25 = 350px */
}

/* BORDER-BOX — total size STAYS at 300px */
.box-border {
  width: 300px;
  padding: 25px;
  box-sizing: border-box;
  /* Total rendered width: exactly 300px — padding is inside */
}
```

---

### The universal `border-box` reset — standard professional practice

Because `border-box` is almost always what developers want and need, professional CSS always starts with this universal reset at the very top of the stylesheet:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

**What this does:** Applies `border-box` sizing to every single element on the page (including pseudo-elements). From this point forward, any `width` or `height` you set is the element's **actual total size** — padding and border are always included within that size, never added outside it.

> **This single rule eliminates the most common layout-breaking surprise in CSS.** It is included in virtually every professional CSS project, every CSS framework (Bootstrap, Tailwind, etc.), and every CSS reset stylesheet.

---

### Why not just use `content-box`?

Historically, `content-box` was the only option — it was the original CSS box model. But web developers universally found it counter-intuitive and layout-breaking. `border-box` was introduced specifically to fix this, and today it is universally preferred. The only reason `content-box` is still the default is to avoid breaking old websites that were built expecting the original behaviour.

---

## Part 6 — Padding with Percentage Values

Padding can also be set using percentage values. This makes an element's inner spacing **responsive** — it adapts proportionally as the screen or parent element resizes.

### How percentage padding works

When you use a percentage value for padding (any side — top, right, bottom, or left), that percentage is always calculated as a percentage of the **parent element's width** — even for `padding-top` and `padding-bottom`.

```css
div {
  padding: 5%;
}
```

If the parent element is 1000px wide, all four sides get `50px` of padding (5% × 1000 = 50px). If the screen shrinks and the parent becomes 600px wide, the padding becomes 30px (5% × 600 = 30px).

---

### Simple Example — Responsive card padding

```html
<style>
  .container {
    width: 80%;
    background-color: #f0f0f0;
  }

  .responsive-card {
    padding: 5%;
    background-color: white;
    border: 1px solid #ddd;
  }
</style>

<div class="container">
  <div class="responsive-card">
    <p>This card's padding adjusts as the screen resizes.</p>
  </div>
</div>
```

**Expected Output:**
On a wide screen, the card has generous padding. On a narrow screen (like a mobile phone), the padding shrinks proportionally. The layout breathes naturally at all screen sizes.

---

### Important gotcha: Percentage padding and `box-sizing`

When using `box-sizing: border-box` with percentage padding, the padding is still calculated from the parent's width — but it is then included inside the element's own width. Everything still behaves predictably.

---

### When to use percentage padding vs pixel padding?

| Use `px` when | Use `%` when |
|---|---|
| Fixed-size components (buttons, tags, badges) | Responsive sections that scale with screen size |
| Precise pixel-perfect designs | Cards and containers that flex with layout |
| Small consistent spacing (e.g., `padding: 8px 16px`) | Aspect-ratio tricks (more on this below) |

---

### Advanced: The "aspect ratio box" trick using percentage padding

One famous use of percentage padding is creating a responsive element that maintains a fixed **aspect ratio**. Since `padding-top: 56.25%` always equals 56.25% of the element's width, a div with zero height and `padding-top: 56.25%` will always maintain a 16:9 aspect ratio as it scales:

```css
.video-wrapper {
  width: 100%;
  padding-top: 56.25%;  /* 9/16 = 56.25% — creates 16:9 ratio */
  position: relative;
  background-color: black;
}
```

This technique is used extensively for responsive video embeds and image placeholders in professional development.

---

## Part 7 — All Padding Properties Reference Table

| Property | Description | Example |
|---|---|---|
| `padding-top` | Sets top inner spacing | `padding-top: 20px;` |
| `padding-right` | Sets right inner spacing | `padding-right: 15px;` |
| `padding-bottom` | Sets bottom inner spacing | `padding-bottom: 20px;` |
| `padding-left` | Sets left inner spacing | `padding-left: 15px;` |
| `padding` (1 value) | Sets all four sides equally | `padding: 20px;` |
| `padding` (2 values) | Sets top/bottom and right/left | `padding: 10px 20px;` |
| `padding` (3 values) | Sets top, right/left, bottom | `padding: 10px 20px 30px;` |
| `padding` (4 values) | Sets top, right, bottom, left | `padding: 10px 20px 30px 40px;` |
| `box-sizing: border-box` | Includes padding inside the element's width | `box-sizing: border-box;` |

---

## Part 8 — Guided Practice Exercises

### Exercise 1 — Read and Predict

Before you write any CSS, study each rule and **predict the output** for all four padding values. Then check your answers.

**Question A:**
```css
p {
  padding: 30px 60px;
}
```
What are the four individual padding values?

**Answer A:**
- `padding-top: 30px`
- `padding-right: 60px`
- `padding-bottom: 30px`
- `padding-left: 60px`

---

**Question B:**
```css
div {
  padding: 10px 20px 30px;
}
```
What are the four individual padding values?

**Answer B:**
- `padding-top: 10px`
- `padding-right: 20px`
- `padding-bottom: 30px`
- `padding-left: 20px`  ← same as right

---

**Question C:**
```css
section {
  padding: 5px 10px 15px 20px;
}
```
What are the four individual padding values?

**Answer C:**
- `padding-top: 5px`
- `padding-right: 10px`
- `padding-bottom: 15px`
- `padding-left: 20px`

---

**Question D:**
```css
.card {
  width: 400px;
  padding: 20px;
  border: 2px solid black;
  /* NO box-sizing set — content-box default applies */
}
```
What is the total rendered width of `.card`?

**Answer D:**
`400 + 20 + 20 + 2 + 2 = 444px`

---

**Question E:**
Same card, but now with `box-sizing: border-box`:
```css
.card {
  width: 400px;
  padding: 20px;
  border: 2px solid black;
  box-sizing: border-box;
}
```
What is the total rendered width? What is the content area width?

**Answer E:**
- Total rendered width: **400px** (the `width` value — nothing added outside)
- Content area width: `400 - 20 - 20 - 2 - 2 = 356px`

---

### Exercise 2 — Profile Card Styling

**Objective:** Apply padding knowledge to build a styled profile card using the `padding` shorthand and `box-sizing: border-box`.

**Scenario:** You are building a user profile card for a small app.

**HTML (given — do not modify):**
```html
<!DOCTYPE html>
<html>
<head>
  <title>Profile Card</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <div class="profile-card">
    <div class="profile-header">
      <h2>Adeola Bello</h2>
      <span class="role">UX Designer</span>
    </div>
    <div class="profile-body">
      <p>Passionate about making digital experiences accessible and beautiful for everyone.</p>
    </div>
    <div class="profile-footer">
      <a href="#" class="btn-follow">Follow</a>
      <a href="#" class="btn-message">Message</a>
    </div>
  </div>

</body>
</html>
```

**Your Task (write `style.css`):**

1. Apply the universal `box-sizing: border-box` reset at the top.
2. Style `body` with a light grey background (`#f0f2f5`).
3. Style `.profile-card`:
   - `width: 340px`
   - `padding: 0` (the sections inside will have their own padding)
   - White background, `1px solid #ddd` border, `border-radius: 10px`
   - Centre it using `margin: 60px auto`
4. Style `.profile-header`:
   - `padding: 24px 24px 16px 24px`
   - A subtle top border radius to match the card
5. Style `.profile-body`:
   - `padding: 0 24px 20px 24px`
6. Style `.profile-footer`:
   - `padding: 16px 24px`
   - A `1px solid #eee` top border to visually separate from body
7. Style both buttons `.btn-follow` and `.btn-message`:
   - `padding: 8px 20px`
   - `border-radius: 20px`
   - Appropriate colours for each

**Solution — `style.css`:**
```css
/* Step 1 — Universal box-sizing reset */
*,
*::before,
*::after {
  box-sizing: border-box;
}

/* Step 2 — Body */
body {
  background-color: #f0f2f5;
  font-family: Arial, sans-serif;
  margin: 0;
}

/* Step 3 — Profile card */
.profile-card {
  width: 340px;
  padding: 0;
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 10px;
  margin: 60px auto;
}

/* Step 4 — Header section */
.profile-header {
  padding: 24px 24px 16px 24px;
}

.profile-header h2 {
  margin: 0 0 4px 0;
  font-size: 20px;
  color: #1a1a2e;
}

.role {
  font-size: 13px;
  color: #888;
}

/* Step 5 — Body section */
.profile-body {
  padding: 0 24px 20px 24px;
}

.profile-body p {
  margin: 0;
  font-size: 14px;
  line-height: 1.6;
  color: #555;
}

/* Step 6 — Footer section */
.profile-footer {
  padding: 16px 24px;
  border-top: 1px solid #eee;
  display: flex;
  gap: 10px;
}

/* Step 7 — Buttons */
.btn-follow,
.btn-message {
  padding: 8px 20px;
  border-radius: 20px;
  font-size: 13px;
  text-decoration: none;
  font-weight: bold;
}

.btn-follow {
  background-color: #007bff;
  color: white;
}

.btn-message {
  background-color: #f0f2f5;
  color: #333;
  border: 1px solid #ddd;
}
```

**Expected Output:**
A clean, professional profile card centred on the page. Adeola's name and role appear in the header with comfortable inner spacing. The bio paragraph has left/right padding aligning it with the header. The footer section has a subtle top border and two side-by-side buttons with pill-shaped padding.

**Self-check Questions:**
- Why was `box-sizing: border-box` added? What problem does it prevent here?
- The card has `width: 340px` and the header has `padding: 24px`. Without `border-box`, how wide would the header section be? With `border-box`, how wide is it?
- Change `.profile-footer` padding to `padding: 8px 24px` — what visual change do you observe?

---

### Exercise 3 — Fix the Broken Layout

**Objective:** Identify and fix the `box-sizing` problem.

**Given CSS (broken layout):**
```css
/* WITHOUT box-sizing fix */
.sidebar {
  width: 30%;
  padding: 20px;
  background-color: #f4f4f4;
  float: left;
}

.main-content {
  width: 70%;
  padding: 20px;
  background-color: white;
  float: left;
}
```

**HTML:**
```html
<div class="sidebar">Sidebar content</div>
<div class="main-content">Main content</div>
```

**Problem:**
The sidebar is 30% + 40px (left+right padding) = more than 30%.
The main content is 70% + 40px = more than 70%.
30% + 70% = 100%, but the real sizes add up to more than 100% — **the layout breaks and wraps to a second line**.

**Your task:** Fix this with one rule.

**Solution:**
```css
*,
*::before,
*::after {
  box-sizing: border-box;
}

.sidebar {
  width: 30%;
  padding: 20px;
  background-color: #f4f4f4;
  float: left;
}

.main-content {
  width: 70%;
  padding: 20px;
  background-color: white;
  float: left;
}
```

**Expected Output after fix:**
Sidebar takes exactly 30% of the parent width (padding included inside). Main content takes exactly 70%. The layout sits side by side correctly without overflowing.

---

## Part 9 — Mini Project: Notification Card System

Build a complete notification card system with four different types of alerts, each using padding correctly and `box-sizing: border-box`.

### Project Brief

You are building a notification/alert component for a web application. There are four types: `success`, `warning`, `error`, and `info`. Each card should have consistent inner spacing and a left accent border to visually signal its type.

---

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Notification Cards</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <div class="notification-container">

    <div class="alert alert-success">
      <strong>✅ Success!</strong>
      <p>Your profile has been updated successfully. Changes are live.</p>
    </div>

    <div class="alert alert-warning">
      <strong>⚠️ Warning</strong>
      <p>Your session will expire in 5 minutes. Please save your work.</p>
    </div>

    <div class="alert alert-error">
      <strong>❌ Error</strong>
      <p>Unable to process your payment. Please check your card details and try again.</p>
    </div>

    <div class="alert alert-info">
      <strong>ℹ️ Info</strong>
      <p>System maintenance is scheduled for Sunday 2–4 AM. Some features may be unavailable.</p>
    </div>

  </div>

</body>
</html>
```

---

### Stage 2 — Base Reset and Body

```css
/* ===== RESET ===== */
*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background-color: #f5f5f5;
  margin: 0;
  padding: 40px;            /* ← padding on body gives page breathing room */
  color: #333;
}
```

**Milestone:** Page background is light grey. There is a comfortable 40px gap on all sides of the viewport edge. Note: `box-sizing: border-box` on `body` means its padding is absorbed inside its 100% width — it does not add scrollbars.

---

### Stage 3 — Notification Container

```css
/* ===== CONTAINER ===== */
.notification-container {
  max-width: 680px;
  margin: 0 auto;           /* centres the container */
  padding: 0;               /* the cards inside have their own padding */
}
```

---

### Stage 4 — Base Alert Card

```css
/* ===== BASE ALERT ===== */
.alert {
  padding: 16px 20px 16px 20px;     /* uniform inner spacing */
  margin-bottom: 16px;              /* space between cards */
  border-radius: 6px;
  border-left: 5px solid transparent;  /* accent left border (colour set per type) */
  background-color: white;
  border-top: 1px solid rgba(0,0,0,0.06);
  border-right: 1px solid rgba(0,0,0,0.06);
  border-bottom: 1px solid rgba(0,0,0,0.06);
}

.alert strong {
  display: block;
  font-size: 15px;
  margin-bottom: 6px;
}

.alert p {
  margin: 0;
  font-size: 14px;
  line-height: 1.5;
  color: #555;
}
```

**Milestone:** All four cards render with white background, equal inner spacing, and slight border on three sides. The left border is placeholder (transparent) — you'll add colour next.

---

### Stage 5 — Type-Specific Colours and Left Accents

```css
/* ===== ALERT TYPES ===== */

/* Success — green */
.alert-success {
  border-left-color: #28a745;
  background-color: #f0fff4;
}
.alert-success strong {
  color: #1e7e34;
}

/* Warning — amber */
.alert-warning {
  border-left-color: #ffc107;
  background-color: #fffdf0;
}
.alert-warning strong {
  color: #856404;
}

/* Error — red */
.alert-error {
  border-left-color: #dc3545;
  background-color: #fff5f5;
}
.alert-error strong {
  color: #721c24;
}

/* Info — blue */
.alert-info {
  border-left-color: #17a2b8;
  background-color: #f0faff;
}
.alert-info strong {
  color: #0c5460;
}
```

**Final Output:**
Four beautifully distinct notification cards stacked vertically on a grey page background. Each card has a bold coloured left accent line (5px), a matching light tinted background, the same inner padding (16px top/bottom, 20px left/right), a bold heading and body text. The entire layout is stable and predictable thanks to `box-sizing: border-box`.

---

### Reflection Questions

1. The `.alert` has `padding: 16px 20px 16px 20px`. This uses 4 values. Could you simplify this to a 2-value shorthand? What would it be?
2. The `body` has `padding: 40px`. Without `box-sizing: border-box`, would this cause a horizontal scrollbar? Why or why not?
3. If you changed `.alert` padding to `padding: 30px 20px`, which sides change and how?
4. Each card has `border-left: 5px solid transparent` in the base style, then each type overrides `border-left-color`. Why not just set `border-left: 5px solid green` directly in `.alert-success`?
5. A new team member says: "I'll remove `box-sizing: border-box` and instead just set `padding: 0` so there is no sizing problem." Why is this not a good solution?

---

## Part 10 — Common Beginner Mistakes

### Mistake 1 — Confusing padding and margin

**Wrong thinking:**
"I need space between my card and the next card. Let me add padding."

**Why it's wrong:** Padding adds space *inside* the element. If you want space *between* elements, you need `margin`.

**Correct thinking:**
- Space inside an element (between content and border) → use `padding`
- Space outside an element (between this element and its neighbours) → use `margin`

```css
/* WRONG — padding does not create space between elements */
.card {
  padding-bottom: 30px;   /* creates space inside the card at the bottom */
}

/* CORRECT — margin creates space between elements */
.card {
  margin-bottom: 30px;    /* creates space between this card and the next */
}
```

---

### Mistake 2 — Forgetting `box-sizing: border-box` and being confused by element overflow

**Wrong:**
```css
.two-columns .column {
  width: 50%;
  padding: 20px;
  float: left;
  /* No box-sizing — default content-box */
}
```

The two columns total: `(50% + 40px) + (50% + 40px) = 100% + 80px` → overflows the container and breaks to two rows.

**Correct:**
```css
*,
*::before,
*::after {
  box-sizing: border-box;
}

.two-columns .column {
  width: 50%;
  padding: 20px;
  float: left;
  /* With border-box: total = 50% + 50% = 100% — perfect */
}
```

---

### Mistake 3 — Using negative padding values

**Wrong:**
```css
p {
  padding: -10px;   /* INVALID — CSS padding cannot be negative! */
}
```

**Why it's wrong:** Negative padding is not allowed in CSS. The browser ignores the declaration.

**Correct:**
If you need to pull content inward or adjust positioning, use `margin` with negative values (which is allowed), or use `position` properties instead.

---

### Mistake 4 — Getting the 4-value shorthand order wrong

**Wrong (common confusion):**
```css
/* Thinking: left, right, top, bottom */
padding: 20px 30px 10px 5px;
```

**Why it's wrong:** Many beginners assume the order goes left-to-right or some other intuitive direction.

**Correct — always clockwise from top:**
```css
/* Top | Right | Bottom | Left (clockwise) */
padding: 20px 5px 10px 30px;
/*       top   right bottom  left */
```

**Memory aid:** **TRouBLe** — **T**op, **R**ight, **B**ottom, **L**eft.

---

### Mistake 5 — Forgetting that `%` padding is relative to the **parent's WIDTH** (not height)

**Wrong assumption:**
```css
.box {
  height: 200px;
  padding-top: 10%;   /* You might expect 10% of 200px = 20px */
}
```

**Reality:** `padding-top: 10%` calculates as 10% of the **parent's width**, not the element's own height. If the parent is 600px wide, `padding-top: 10%` = 60px.

**Correct understanding:** All percentage padding values — even `padding-top` and `padding-bottom` — are calculated relative to the **parent element's width**. Keep this in mind when using percentage padding for vertical spacing.

---

### Mistake 6 — Using `padding` to vertically centre text (it doesn't always work)

**Wrong approach for centring:**
```css
.header {
  height: 60px;
  padding-top: 20px;   /* Trying to "eyeball" vertical centre */
}
```

**Better approach:**
```css
.header {
  height: 60px;
  display: flex;
  align-items: center;   /* True vertical centring */
  padding: 0 20px;       /* Horizontal padding only */
}
```

Padding can help with spacing, but for true vertical centring, use flexbox `align-items: center` or `line-height` tricks.

---

## Part 11 — Reflection Questions

1. In your own words, what is the difference between padding and margin? Use the cardboard box analogy if it helps.
2. Write the shorthand `padding` declaration equivalent to:
   - `padding-top: 15px; padding-right: 30px; padding-bottom: 15px; padding-left: 30px;`
3. An element has `width: 200px`, `padding: 10px`, and `border: 2px solid black`.
   - Without `box-sizing: border-box`, what is the total rendered width?
   - With `box-sizing: border-box`, what is the total rendered width?
4. Why do virtually all professional CSS projects start with `box-sizing: border-box` applied universally?
5. You have a container that is 500px wide. You set `padding: 10%` on a child element inside it. What is the actual padding value in pixels on all four sides?
6. Describe a real website element you use regularly (e.g., a search bar, a login button, a news article card). How does padding affect how that element looks and feels?
7. What happens if you set `padding: -5px`? Why?

---

## Completion Checklist

- [ ] I can explain what padding is and where it lives in the CSS box model
- [ ] I understand the difference between padding (inside) and margin (outside)
- [ ] I can set padding on each side individually using `padding-top`, `padding-right`, `padding-bottom`, `padding-left`
- [ ] I can use the `padding` shorthand with 1, 2, 3, and 4 values and know what each means
- [ ] I know the correct order for 4-value padding shorthand (Top → Right → Bottom → Left)
- [ ] I understand how percentage padding is calculated (relative to parent width — always)
- [ ] I understand the default `content-box` model and why padding can make elements wider than expected
- [ ] I understand how `box-sizing: border-box` solves the width problem
- [ ] I can write the universal `box-sizing: border-box` reset from memory
- [ ] I completed Exercise 1 (Read and Predict — all 5 questions)
- [ ] I completed Exercise 2 (Profile Card Styling)
- [ ] I completed Exercise 3 (Fix the Broken Layout)
- [ ] I completed the Mini Project (Notification Card System)
- [ ] I can identify and fix the 6 common beginner mistakes

---

## Lesson Summary

CSS padding creates **inner space** between an element's content and its border — the breathing room that makes everything on a webpage readable, clickable, and visually comfortable.

The four individual properties — `padding-top`, `padding-right`, `padding-bottom`, and `padding-left` — let you control each side independently. The `padding` shorthand collapses all four into one declaration: with 1 value for uniform padding on all sides; with 2 values for top/bottom and right/left pairs; with 3 values for top, right/left, and bottom separately; and with 4 values for all four sides individually in clockwise order (Top → Right → Bottom → Left, remembered as TRouBLe).

Padding can use any valid CSS length unit. Pixel values give fixed, precise spacing. Percentage values create responsive padding that scales with the parent element's width — crucially, this applies to all four sides including top and bottom.

The most important concept in this lesson is the relationship between padding and element width. By default, CSS uses the `content-box` model where `width` measures only the content area, and padding is added on top of it — causing elements to grow beyond their declared width. This breaks layouts. The fix is `box-sizing: border-box`, which redefines `width` to include both content and padding (and border), so the element's total size is always exactly what you declared. The professional standard is to apply this universally at the top of every CSS file using `*, *::before, *::after { box-sizing: border-box; }` — a single rule that makes layout arithmetic reliable and intuitive throughout the entire project.

---

*Sources: W3Schools CSS Padding (https://www.w3schools.com/css/css_padding.asp), CSS Padding and box-sizing (https://www.w3schools.com/css/css_padding_box-sizing.asp), and CSS Padding Code Challenges (https://www.w3schools.com/css/css_challenges_padding.asp)*
