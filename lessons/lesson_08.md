---
render_with_liquid: false
title: "CSS Margins and Margin Collapse"
nav_order: 8
---

# Lesson 08 — CSS Margins and Margin Collapse

---

## Lesson Introduction

Welcome to Lesson 08! In this lesson you will learn how to control the **space around elements** on a webpage using the CSS `margin` property. Margins are one of the most frequently used CSS tools in existence — every professional layout you have ever seen on the internet uses margins to create breathing room, separation, and alignment between elements.

You will also learn about a surprising and often confusing CSS behaviour called **margin collapse** — where two margins that should add together instead merge into one. Once you understand this, a whole category of mysterious "why won't my spacing work?" bugs will suddenly make sense.

By the end of this lesson you will be able to:

- Understand what a margin is and why it is essential to layout design
- Set individual margins on all four sides of an element
- Use the shorthand `margin` property with 1, 2, 3, or 4 values
- Use `margin: auto` to horizontally centre an element
- Use `margin: inherit` to copy a margin from a parent element
- Understand what margin collapse is, why it happens, and when to expect it
- Identify and solve common margin-related layout problems
- Build a complete webpage layout using margins as your main spacing tool

---

## Prerequisite Concepts

Before diving in, let's quickly review the ideas that margin builds on.

### The CSS Box Model

Every single HTML element on a page is treated as a **rectangular box** by the browser. This box has four layers:

```
+-------------------------------------------+
|                  MARGIN                   |  ← outside space (transparent)
|   +-----------------------------------+   |
|   |             BORDER                |   |  ← the visible edge
|   |   +---------------------------+   |   |
|   |   |          PADDING          |   |   |  ← inside space (fills with background)
|   |   |   +-------------------+   |   |   |
|   |   |   |     CONTENT       |   |   |   |  ← your text, images, etc.
|   |   |   +-------------------+   |   |   |
|   |   +---------------------------+   |   |
|   +-----------------------------------+   |
+-------------------------------------------+
```

**Margin** is the outermost layer — the transparent space **outside** the element's border. It pushes other elements away.

> 💡 **Analogy:** Imagine a photograph in a frame. The photograph is the content. The white space around the photograph inside the frame is the padding. The frame itself is the border. And the gap between this frame and the neighbouring frame on the wall is the margin.

---

### Block vs. Inline Elements (Quick Reminder)

- **Block elements** (like `<div>`, `<p>`, `<h1>`) take up the full width of their container and stack vertically. Margins work on all four sides.
- **Inline elements** (like `<span>`, `<a>`, `<strong>`) only take up as much space as their content. Top and bottom margins have limited effect on inline elements. Left and right margins do work.

This lesson focuses mainly on block elements, where margins are most straightforward to understand.

---

## Part 1 — CSS Margins: All Four Sides

---

### 1.1 What is a Margin?

A **margin** is transparent empty space placed **outside** an element's border. It creates distance between that element and the elements around it.

Margins are completely invisible — you cannot give them a colour or background. They are pure space.

**Why do we need margins?**

Without margins, every element on a page would be squished directly against every other element. Text would run into headings. Paragraphs would sit directly on top of each other. Images would collide with buttons. Margins give elements the breathing room they need to be readable and visually pleasing.

---

### 1.2 Individual Margin Properties

CSS gives you four individual properties to set the margin on each side of an element separately:

| Property | Which side |
|---|---|
| `margin-top` | Space above the element |
| `margin-right` | Space to the right of the element |
| `margin-bottom` | Space below the element |
| `margin-left` | Space to the left of the element |

**Syntax:**

```css
element {
  margin-top: value;
  margin-right: value;
  margin-bottom: value;
  margin-left: value;
}
```

---

**Example 1 — Setting all four sides individually:**

```css
p {
  margin-top: 100px;
  margin-bottom: 100px;
  margin-right: 150px;
  margin-left: 80px;
}
```

**Line-by-line explanation:**
- `margin-top: 100px;` → push 100 pixels of space above every paragraph
- `margin-bottom: 100px;` → push 100 pixels of space below every paragraph
- `margin-right: 150px;` → push 150 pixels of space to the right of every paragraph
- `margin-left: 80px;` → push 80 pixels of space to the left of every paragraph

**Expected result:** Each paragraph is surrounded by space on all four sides, creating a large amount of visible separation from neighbouring elements and from the container edges.

---

**Example 2 — Different margins on different sides:**

```css
.news-article {
  margin-top: 30px;
  margin-right: 20px;
  margin-bottom: 40px;
  margin-left: 20px;
}
```

**Expected result:** News article boxes have a larger gap below them (40px) than above (30px), and equal space on both sides (20px each). This is a common pattern for article layouts.

---

> 💡 **Thinking Prompt:** What would the page look like if you set `margin-left: 0` and `margin-right: 0` but kept `margin-top: 30px` and `margin-bottom: 30px`? The elements would touch both sides of the container but have vertical breathing room between them.

---

### 1.3 Margin Values — What Can You Use?

CSS margins accept several types of values:

| Value type | Example | What it means |
|---|---|---|
| `px` (pixels) | `margin: 20px` | A fixed, exact pixel amount |
| `em` | `margin: 1.5em` | Relative to the current font size |
| `rem` | `margin: 2rem` | Relative to the root (html) font size |
| `%` | `margin: 5%` | A percentage of the parent element's width |
| `auto` | `margin: auto` | Browser calculates the value automatically (very useful!) |
| `inherit` | `margin: inherit` | Copy the margin value from the parent element |
| `0` | `margin: 0` | No margin at all (zero — no unit needed) |

> ⚠️ **Important:** The value `0` is the only CSS value that does not need a unit. `margin: 0;` is perfectly valid. But `margin: 20;` (without `px` or another unit) is invalid and will be ignored by the browser.

---

**Example 3 — Using percentage margin:**

```css
.container {
  width: 800px;
}

.content-box {
  margin-left: 10%;   /* 10% of 800px = 80px */
  margin-right: 10%;  /* 10% of 800px = 80px */
}
```

**Expected result:** The content box has 80px of space on each side inside an 800px container. If the container resizes, the margins resize proportionally.

---

**Example 4 — Removing all margins with zero:**

```css
* {
  margin: 0;
  padding: 0;
}
```

**What this does:** This is called a **CSS reset**. The `*` selector targets every element on the page. Setting both `margin` and `padding` to `0` removes all the default spacing that browsers add. Professional developers often start a project with this rule so they have a clean, consistent baseline.

**Expected result:** All browser default spacing is removed. Elements appear tightly packed — you then add your own margins exactly where you want them.

---

### 1.4 Negative Margins

CSS margins can be **negative**. This pulls the element in the opposite direction — towards or even over adjacent elements.

**Example 5 — Negative margin-top:**

```css
.overlap-box {
  margin-top: -20px;
}
```

**Expected result:** The element moves 20 pixels upward, potentially overlapping the element above it. This is an advanced technique used for visual effects and special layouts — use it carefully!

---

## Part 2 — The Shorthand `margin` Property

---

### 2.1 Why Use Shorthand?

Writing four separate properties every time is verbose. CSS provides a shorthand `margin` property that lets you set all four sides in a single line.

```css
element {
  margin: value(s);
}
```

The number of values you provide changes which sides they apply to. This follows a specific pattern you must learn by heart.

---

### 2.2 Shorthand with 4 Values — All Four Sides

```css
element {
  margin: top  right  bottom  left;
}
```

**Memory trick:** Think of a clock starting at the top and going clockwise — **T**op → **R**ight → **B**ottom → **L**eft. You can remember it as **"TRouBLe"** (T, R, B, L).

**Example 6 — Four values:**

```css
p {
  margin: 25px  50px  75px  100px;
}
```

- Top margin: `25px`
- Right margin: `50px`
- Bottom margin: `75px`
- Left margin: `100px`

**Expected result:** The paragraph has unequal margins on all four sides — smallest on top, largest on the left.

---

### 2.3 Shorthand with 3 Values — Top, Left/Right, Bottom

```css
element {
  margin: top  left-and-right  bottom;
}
```

The middle value applies to both the left AND right sides equally.

**Example 7 — Three values:**

```css
p {
  margin: 25px  50px  75px;
}
```

- Top margin: `25px`
- Right margin: `50px`
- Left margin: `50px` (same as right)
- Bottom margin: `75px`

**Expected result:** The paragraph has equal left and right spacing (50px each), a small top gap (25px), and a larger bottom gap (75px).

---

### 2.4 Shorthand with 2 Values — Top/Bottom and Left/Right

```css
element {
  margin: top-and-bottom  left-and-right;
}
```

The first value applies to top AND bottom. The second applies to left AND right.

**Example 8 — Two values:**

```css
p {
  margin: 25px  50px;
}
```

- Top margin: `25px`
- Bottom margin: `25px` (same as top)
- Right margin: `50px`
- Left margin: `50px` (same as right)

**Expected result:** The paragraph has consistent vertical spacing (25px top and bottom) and consistent horizontal spacing (50px left and right).

---

### 2.5 Shorthand with 1 Value — All Four Sides Equal

```css
element {
  margin: all-sides;
}
```

One single value applies to all four sides equally.

**Example 9 — One value:**

```css
p {
  margin: 25px;
}
```

- Top margin: `25px`
- Right margin: `25px`
- Bottom margin: `25px`
- Left margin: `25px`

**Expected result:** The paragraph has the same 25px margin on every side — a clean, even spacing all around.

---

### 2.6 Quick Reference Summary Table

| Shorthand | Top | Right | Bottom | Left |
|---|---|---|---|---|
| `margin: 10px 20px 30px 40px` | 10px | 20px | 30px | 40px |
| `margin: 10px 20px 30px` | 10px | 20px | 30px | 20px |
| `margin: 10px 20px` | 10px | 20px | 10px | 20px |
| `margin: 10px` | 10px | 10px | 10px | 10px |

---

> 💡 **Thinking Prompt:** If you write `margin: 20px 40px`, what is the left margin? Answer: `40px` — it shares the value with the right margin. The second value is always left and right together.

---

## Part 3 — The `auto` Value: Centring Elements Horizontally

---

### 3.1 What Does `margin: auto` Do?

When you set a margin to `auto`, the browser **automatically calculates** the margin value. By itself, `auto` on one side just gives that side all the remaining space.

The real power comes when you set **both the left and right margins to `auto`** simultaneously. When both sides are `auto`, the browser splits the remaining horizontal space **equally** between both sides — and this centres the element horizontally inside its container.

---

### 3.2 The Centering Technique

```css
element {
  width: [some fixed width];
  margin: 0 auto;
}
```

This is the most classic and widely used technique for horizontally centring a block element. You **must** set a `width` — otherwise the element takes up the full container width and there is no remaining space to split.

**Example 10 — Centring a div:**

```css
div {
  width: 300px;
  margin: 0 auto;
  background-color: lightblue;
}
```

**Line-by-line explanation:**
- `width: 300px;` → the element is 300 pixels wide
- `margin: 0 auto;` → top and bottom margin are 0; left and right are calculated automatically (equal halves of the remaining space)
- `background-color: lightblue;` → makes the box visible so you can see it centred

**Expected result:** The lightblue box sits perfectly in the centre of the page. If the page is 1200px wide and the box is 300px, the browser puts 450px of space on both the left and the right sides.

---

**Example 11 — Centring a content wrapper (extremely common pattern):**

```css
.wrapper {
  width: 960px;
  margin: 0 auto;
}
```

**Expected result:** The wrapper div (which contains all your page content) is centred on the page. This is the basis of almost every website layout ever built — your page content sits in a centred container with empty space on both sides.

---

> ⚠️ **Common Mistake:** Using `margin: auto` without a defined `width` has no centering effect on block elements. The element already fills the full container width, so there is no remaining space to split.

```css
/* WRONG - no width, so auto has no centering effect */
div {
  margin: 0 auto;
}

/* CORRECT - width defined, auto can centre it */
div {
  width: 600px;
  margin: 0 auto;
}
```

---

**Example 12 — auto with only top and bottom set separately:**

```css
.photo-frame {
  width: 400px;
  margin-top: 30px;
  margin-bottom: 30px;
  margin-left: auto;
  margin-right: auto;
}
```

**Expected result:** The photo frame is centred horizontally AND has 30px of vertical breathing room above and below. This is equivalent to writing `margin: 30px auto;`.

---

## Part 4 — The `inherit` Value

---

### 4.1 What is `inherit`?

CSS properties are sometimes passed down from parent elements to their children — this is called **inheritance**. Not all properties inherit automatically, but you can force any property to inherit using the `inherit` value.

When you write `margin: inherit;` on an element, it copies the margin value from its **direct parent** element.

**Example 13 — margin-left: inherit:**

```html
<!-- HTML structure -->
<div class="parent-box">
  <p class="child-paragraph">I inherit my left margin.</p>
</div>
```

```css
.parent-box {
  border: 1px solid red;
  margin-left: 100px;   /* parent has 100px left margin */
}

.child-paragraph {
  margin-left: inherit;  /* child copies 100px from parent */
}
```

**Expected result:** The red-bordered div has 100px of space on the left. The paragraph inside it also has 100px of left margin — it inherited the value from `.parent-box`.

---

**Why would you use `inherit`?**

`inherit` is useful when you want a child element's spacing to stay consistent with its parent's spacing without hardcoding the same number in two places. If you later change the parent's margin, all children using `inherit` update automatically.

---

## Part 5 — Margin Collapse

---

### 5.1 Introduction: The Most Confusing CSS Behaviour for Beginners

Let's say you have two paragraphs stacked on top of each other. The first paragraph has a bottom margin of `50px`. The second paragraph has a top margin of `20px`. If you add those together, you might expect `70px` of space between them.

**But that is NOT what happens.**

Instead, the browser gives you only **50px** of space between them — the larger of the two values. The two margins do not add up; they **collapse** into a single margin equal to the largest one.

This behaviour is called **margin collapse**, and it is one of the most surprising things beginners encounter in CSS.

---

### 5.2 The Rule: When Do Margins Collapse?

**Margin collapse ONLY happens between vertical (top and bottom) margins.**

Left and right margins NEVER collapse. Only top and bottom margins can collapse together.

More specifically, margin collapse occurs when:
- The **bottom margin** of one element meets the **top margin** of the element directly below it
- Both elements are **block-level elements** in normal document flow
- There is no border, padding, or other content between the two margins

---

### 5.3 Example: Two Different-Sized Vertical Margins

**HTML:**

```html
<h1>This is a Heading</h1>
<h2>This is a Subheading</h2>
```

**CSS:**

```css
h1 {
  background-color: lightcoral;
  margin-bottom: 50px;   /* large bottom margin */
}

h2 {
  background-color: lightblue;
  margin-top: 20px;      /* smaller top margin */
}
```

**What you might expect:**
- Bottom margin of `h1` = 50px
- Top margin of `h2` = 20px
- Total gap between `h1` and `h2` = 50 + 20 = **70px**

**What actually happens:**
- The two margins collapse into **one single margin of 50px** (the larger of the two)
- The total visible gap between `h1` and `h2` is only **50px**

**Expected visual result:** The gap between the coral heading and the blue subheading is 50px — not 70px.

---

### 5.4 Example: Two Equal Vertical Margins

**HTML:**

```html
<p>First paragraph</p>
<p>Second paragraph</p>
```

**CSS:**

```css
p {
  margin-top: 30px;
  margin-bottom: 30px;
  background-color: lightyellow;
  padding: 10px;
}
```

**What you might expect:**
- Bottom margin of first `p` = 30px
- Top margin of second `p` = 30px
- Total gap between them = 30 + 30 = **60px**

**What actually happens:**
- The two equal margins collapse into a single margin of **30px**
- Total visible gap between the two paragraphs = **30px**

**Expected visual result:** The space between two consecutive yellow paragraphs is 30px — not 60px.

---

> 💡 **Analogy for Margin Collapse:** Imagine two people standing back to back. Person A takes one step backwards (their bottom margin). Person B also takes one step backwards (their top margin). How far apart are they? You might think 2 steps, but they are standing back to back — so the larger of the two steps is what separates them. That is exactly how CSS margin collapse works.

---

### 5.5 The Key Rule to Remember

> **When two vertical margins meet, CSS uses the LARGER of the two values as the final gap — not the sum of both.**

If both margins are equal (e.g. both `30px`), the final gap is `30px` — not `60px`.

---

### 5.6 What Margin Collapse Does NOT Apply To

Margin collapse is only a vertical phenomenon. It never happens with:
- **Left and right margins** — these always add up normally
- **Elements with borders** between them — a border prevents collapse
- **Elements with padding** between them — padding prevents collapse
- **Flex and Grid containers** — margin collapse does not occur inside flexbox or CSS grid layouts
- **Absolutely positioned elements**

---

### 5.7 Visualising the Difference

```
WITHOUT collapse (what beginners expect):
┌────────────────────┐
│    First element   │
└────────────────────┘
         ↕ 50px  (bottom margin of first)
         ↕ 20px  (top margin of second)
┌────────────────────┐
│    Second element  │
└────────────────────┘
Total gap = 70px ← WRONG

WITH collapse (what actually happens):
┌────────────────────┐
│    First element   │
└────────────────────┘
         ↕ 50px  (larger margin wins, smaller is absorbed)
┌────────────────────┐
│    Second element  │
└────────────────────┘
Total gap = 50px ← CORRECT
```

---

## Part 6 — Guided Practice Exercises

---

### Exercise 1 — Individual Margin Practice

**Objective:** Write margins for all four sides using individual properties.

**Scenario:** You are styling a blog post article. The article needs extra breathing room from other elements.

**Your task:** Write CSS for a `.blog-post` class that:
- Has 40px of space above it
- Has 20px of space on both the left and right sides
- Has 60px of space below it (posts should be well-separated)

**Starting point:**

```css
.blog-post {
  background-color: white;
  border: 1px solid #e0e0e0;
  padding: 25px;
  /* add your margin properties here */
}
```

**Your solution:**

```css
.blog-post {
  background-color: white;
  border: 1px solid #e0e0e0;
  padding: 25px;
  margin-top: 40px;
  margin-right: 20px;
  margin-bottom: 60px;
  margin-left: 20px;
}
```

**Expected result:** Blog posts are nicely separated from each other (60px gap below), indented slightly from the page edges (20px), and have a reasonable gap from whatever is above them (40px).

---

**Self-check questions:**
- Could you write this using shorthand? (Hint: `margin: 40px 20px 60px 20px;`)
- What would happen if you removed `margin-bottom` entirely? The posts would appear much closer together.

---

### Exercise 2 — Shorthand Practice

**Objective:** Decode shorthand margin values.

For each shorthand below, write out the individual top, right, bottom, and left values:

**Question A:**
```css
div { margin: 15px; }
```
- Top: `15px` | Right: `15px` | Bottom: `15px` | Left: `15px`

**Question B:**
```css
div { margin: 10px 30px; }
```
- Top: `10px` | Right: `30px` | Bottom: `10px` | Left: `30px`

**Question C:**
```css
div { margin: 5px 15px 25px; }
```
- Top: `5px` | Right: `15px` | Bottom: `25px` | Left: `15px`

**Question D:**
```css
div { margin: 5px 10px 15px 20px; }
```
- Top: `5px` | Right: `10px` | Bottom: `15px` | Left: `20px`

---

**Now go the other direction — write shorthand for these individual values:**

**Question E:** Top `20px`, Right `20px`, Bottom `20px`, Left `20px`
- Answer: `margin: 20px;`

**Question F:** Top `0`, Right `auto`, Bottom `0`, Left `auto`
- Answer: `margin: 0 auto;`

**Question G:** Top `10px`, Right `50px`, Bottom `10px`, Left `50px`
- Answer: `margin: 10px 50px;`

---

### Exercise 3 — Centring an Element

**Objective:** Use `margin: auto` to horizontally centre a box on the page.

**Scenario:** You are building a login form page. The form needs to appear centred on the screen.

**HTML:**

```html
<div class="login-form">
  <h2>Sign In</h2>
  <p>Enter your details below.</p>
</div>
```

**Task:** Write CSS to:
1. Give the `.login-form` a width of `400px`
2. Centre it horizontally using `margin: auto`
3. Add `40px` of top and bottom margin so it is not jammed at the top of the page
4. Give it a background, padding, and a subtle border so it looks like a form card

**Solution:**

```css
.login-form {
  width: 400px;
  margin: 40px auto;         /* 40px top and bottom, centred horizontally */
  background-color: white;
  padding: 30px;
  border: 1px solid #dddddd;
  border-radius: 8px;
}
```

**Expected result:** A white form card that is perfectly centred on the page with 40px of space above and below. No matter what the screen width is, the form stays centred.

---

### Exercise 4 — Understanding Margin Collapse

**Objective:** Calculate the actual visible gap after margin collapse.

**Scenario:** Predict the actual gap between these elements and explain why.

**Case A:**

```css
h1 { margin-bottom: 50px; }
p  { margin-top: 20px; }
```

Question: What is the visible gap between `h1` and `p`?
Answer: **50px** — the two margins collapse, and the larger value (50px) wins.

---

**Case B:**

```css
p.first  { margin-bottom: 30px; }
p.second { margin-top: 30px; }
```

Question: What is the visible gap between the two paragraphs?
Answer: **30px** — two equal margins collapse into one 30px margin (not 60px).

---

**Case C:**

```css
div { margin-right: 30px; }
div { margin-left: 30px; }
```

Question: Two side-by-side divs. What is the visible gap between them?
Answer: **60px** — left and right margins NEVER collapse. They add up normally.

---

**Case D:**

```css
h2 { margin-bottom: 80px; }
h3 { margin-top: 10px; }
```

Question: What is the visible gap between `h2` and `h3`?
Answer: **80px** — collapse applies, and the larger value wins.

---

## Part 7 — Code Challenge Practice (from W3Schools Challenges)

These challenges mirror the style of questions in the W3Schools CSS Margins Code Challenge page. Work through each one on your own before reading the solution.

---

### Challenge 1 — Set All Four Margins

**Task:** Set the top and bottom margins of all `<p>` elements to `25px`, and the left and right margins to `50px`. Use the shorthand `margin` property.

**Solution:**

```css
p {
  margin: 25px 50px;
}
```

**Explanation:** Two-value shorthand — first value applies to top AND bottom (25px), second value applies to left AND right (50px).

---

### Challenge 2 — Centre a div

**Task:** Centre a `<div>` element that has a `width` of `300px` horizontally on the page. Use the `margin` property.

**Solution:**

```css
div {
  width: 300px;
  margin: auto;
}
```

**Explanation:** When `margin` is set to `auto` on a block element with a defined width, the browser splits remaining horizontal space equally between left and right, producing centred alignment.

---

### Challenge 3 — Inherit a Margin

**Task:** Make the `<p>` element inherit its left margin from its parent `<div>`. The parent has `margin-left: 100px`.

**HTML:**

```html
<div class="parent">
  <p class="child">I inherit from my parent.</p>
</div>
```

**Solution:**

```css
.parent {
  margin-left: 100px;
}

.child {
  margin-left: inherit;
}
```

**Expected result:** The child paragraph is indented by 100px — the same amount as the parent div.

---

### Challenge 4 — Explain the Gap

**Task:** Without running the code, predict the space between these two elements:

```css
h2 { margin-bottom: 40px; }
p  { margin-top: 15px; }
```

**Answer:** The visible gap is **40px** — margin collapse gives us the larger of the two values (40px), not the sum (55px).

---

## Part 8 — Mini Project: Blog Article Layout

Build a fully styled, multi-section blog article page using margins as your primary layout tool.

---

### Stage 1 — HTML Structure

Create a file called `blog.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>The Art of Good Spacing</title>
  <link rel="stylesheet" href="blog.css">
</head>
<body>

  <header class="site-header">
    <h1>The Daily Dev Blog</h1>
  </header>

  <main class="page-wrapper">

    <article class="blog-post">

      <h2 class="post-title">The Art of Good Spacing</h2>
      <p class="post-meta">Published April 2026 · 4 min read</p>

      <p class="post-body">
        Good spacing is the invisible ingredient in every great design.
        When you visit a well-designed website, you might not consciously
        notice the margins and padding — but you feel the calm and clarity
        they create. Remove the spacing, and suddenly everything feels
        cramped and hard to read.
      </p>

      <p class="post-body">
        CSS margins are your primary tool for controlling space between
        elements. They work on all four sides of every block element, and
        they give you precise control over how much breathing room your
        content gets.
      </p>

      <h3 class="section-heading">Why Spacing Matters</h3>

      <p class="post-body">
        Research in typography consistently shows that generous line spacing
        and paragraph margins improve reading speed and comprehension.
        Users make faster decisions, feel less overwhelmed, and trust
        content more when it is well-spaced.
      </p>

      <p class="post-body">
        Start with generous margins and reduce them gradually. It is much
        easier to tighten spacing than to loosen it once a layout is set.
      </p>

    </article>

    <aside class="sidebar">
      <h3 class="sidebar-title">About the Author</h3>
      <p class="sidebar-text">
        A frontend developer passionate about clean, accessible design.
        Writing about CSS, layout, and the web since 2020.
      </p>
    </aside>

  </main>

  <footer class="site-footer">
    <p>© 2026 The Daily Dev Blog. All rights reserved.</p>
  </footer>

</body>
</html>
```

---

### Stage 2 — CSS with Margin-Focused Styling

Create a file called `blog.css`:

```css
/*
  ================================================
  blog.css
  Project: Blog Article Layout
  Focus: CSS Margins as primary layout tool
  ================================================
*/


/* ==============================
   SECTION 1: RESET + BASE
   ============================== */

* {
  margin: 0;           /* Remove all browser default margins */
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Georgia, "Times New Roman", serif;
  background-color: #f7f4ef;   /* Warm off-white page background */
  color: #2d2d2d;
  line-height: 1.8;
}


/* ==============================
   SECTION 2: SITE HEADER
   ============================== */

.site-header {
  background-color: #1c1c2e;
  color: white;
  padding: 20px;
  /* No margin needed — header stretches full width */
}

.site-header h1 {
  /* Centre the blog name inside the header */
  width: fit-content;
  margin: 0 auto;
  font-size: 28px;
  letter-spacing: 2px;
}


/* ==============================
   SECTION 3: PAGE WRAPPER
   (Centres all main content)
   ============================== */

.page-wrapper {
  width: 880px;
  margin: 50px auto;           /* 50px top/bottom + centred horizontally */
  display: flex;
  gap: 40px;
  align-items: flex-start;
}


/* ==============================
   SECTION 4: BLOG ARTICLE
   ============================== */

.blog-post {
  flex: 1;                     /* Takes up remaining space next to sidebar */
  background-color: white;
  padding: 40px;
  border-left: 4px solid #e07b39;  /* Orange accent border */
}

.post-title {
  font-size: 28px;
  color: #1c1c2e;
  margin-bottom: 8px;          /* Small gap below title before meta line */
}

.post-meta {
  font-size: 13px;
  color: #888888;
  margin-bottom: 30px;         /* Larger gap before body text begins */
}

.post-body {
  font-size: 16px;
  margin-bottom: 22px;         /* Space between paragraphs */
}

.post-body:last-of-type {
  margin-bottom: 0;            /* Remove margin from last paragraph */
}

.section-heading {
  font-size: 20px;
  color: #e07b39;              /* Match accent colour */
  margin-top: 36px;            /* Space above sub-heading */
  margin-bottom: 14px;         /* Space below sub-heading before text */
}


/* ==============================
   SECTION 5: SIDEBAR
   ============================== */

.sidebar {
  width: 220px;
  flex-shrink: 0;              /* Sidebar stays fixed width */
  background-color: #1c1c2e;
  color: white;
  padding: 24px;
  border-radius: 6px;
}

.sidebar-title {
  font-size: 16px;
  margin-bottom: 12px;         /* Gap between title and text */
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #e07b39;
}

.sidebar-text {
  font-size: 14px;
  line-height: 1.7;
  color: #cccccc;
}


/* ==============================
   SECTION 6: FOOTER
   ============================== */

.site-footer {
  background-color: #1c1c2e;
  color: #aaaaaa;
  text-align: center;
  padding: 20px;
  margin-top: 0;               /* Page wrapper already has bottom margin */
  font-size: 13px;
}
```

---

### Stage 3 — Milestone Check

Open `blog.html` in your browser. You should see:

- A dark navy header with the blog name centred inside it
- A main content area centred on the page at 880px wide
- A blog article on the left with clear spacing between the title, meta line, and body paragraphs
- An orange-accented sub-heading with extra space above and below
- A dark sidebar on the right with the author bio
- A dark footer at the bottom

Every gap you see between elements is controlled by a `margin` property in the CSS.

---

### Stage 4 — Margin Collapse Observation

**Experiment:** Add these two elements to your HTML just before `</main>`:

```html
<div class="collapse-demo">
  <p class="demo-a" style="background:lightcoral; margin-bottom:50px;">
    I have margin-bottom: 50px
  </p>
  <p class="demo-b" style="background:lightblue; margin-top:30px;">
    I have margin-top: 30px
  </p>
</div>
```

**Question:** What is the gap between these two coloured paragraphs?
**Answer:** 50px — the larger margin wins due to collapse.

**Verify it:** Open DevTools (`F12`), click the first paragraph, and look at the "Box Model" diagram in the Styles panel. You will see the 50px bottom margin displayed. Now click the second paragraph — its 30px top margin is shown, but in reality it is being absorbed by the first element's larger margin.

---

### Stage 5 — Enhancement Challenges (Optional)

1. **Responsive adjustment:** Change `.page-wrapper` width from `880px` to `90%` and observe how the layout adapts as you resize the browser window.
2. **Margin experiment:** Change the `margin-bottom` on `.post-body` from `22px` to `0` and observe how the article becomes harder to read without paragraph spacing.
3. **Centering challenge:** Remove `width: 880px` from `.page-wrapper`. What happens to `margin: auto`? The layout breaks — this shows why a defined width is essential for `auto` to work.
4. **Negative margin experiment:** Add `margin-top: -20px` to `.site-header h1` and observe the effect. Then remove it.

---

### Reflection Questions

1. Open your `blog.css`. Can you identify every place where `margin` creates visible spacing on the page?
2. In `.section-heading`, the rule has `margin-top: 36px` and `.post-body` has `margin-bottom: 22px`. What is the actual gap between a paragraph and the sub-heading that follows it? (Remember margin collapse!)
3. Why does `margin: 50px auto` work for `.page-wrapper` but not for `.site-header h1`?
4. If you removed `margin-bottom: 0` from `.post-body:last-of-type`, what would happen to the spacing at the bottom of the article box?

---

## Common Beginner Mistakes

---

### Mistake 1 — Forgetting a Unit

```css
/* WRONG */
p { margin: 20; }

/* CORRECT */
p { margin: 20px; }
```

`margin: 20;` is invalid. The browser silently ignores it. Always add a unit (`px`, `em`, `%`, etc.). The only exception is `0` which never needs a unit.

---

### Mistake 2 — Expecting `margin: auto` to Centre Without a Width

```css
/* WRONG - no width, so centering does not work on block elements */
div {
  margin: 0 auto;
}

/* CORRECT */
div {
  width: 600px;
  margin: 0 auto;
}
```

A block element naturally expands to fill its container. With no width set, there is no remaining space to split — so `auto` does nothing visible.

---

### Mistake 3 — Confusing Margin and Padding

Both create space, but they are fundamentally different:

```css
.box {
  padding: 20px;  /* space INSIDE the border — gets the background colour */
  margin: 20px;   /* space OUTSIDE the border — always transparent */
}
```

If you want space between the element's content and its border → use **padding**.
If you want space between the element and the elements around it → use **margin**.

---

### Mistake 4 — Being Surprised by Margin Collapse

```css
/* You write this expecting 60px gap between elements */
p { margin-bottom: 30px; }
p { margin-top: 30px; }

/* But you get 30px — because of collapse */
```

Remember: vertical margins between adjacent block elements collapse. The actual gap equals the **larger** of the two margins, not their sum.

---

### Mistake 5 — Getting the Shorthand Order Wrong

```css
/* WRONG mental model - thinking it goes left-to-right */
margin: left right top bottom;  /* NO! */

/* CORRECT - clockwise from top (TRouBLe) */
margin: top right bottom left;  /* YES! */
```

Always think: **Top → Right → Bottom → Left** (clockwise from top).

---

### Mistake 6 — Trying to Set Vertical Margins on Inline Elements

```css
span {
  margin-top: 50px;     /* has no visible effect on inline elements */
  margin-bottom: 50px;  /* has no visible effect on inline elements */
}
```

Top and bottom margins are largely ignored on inline elements like `<span>`, `<a>`, or `<strong>`. To get vertical spacing on such elements, either convert them to block or inline-block: `display: inline-block;`.

---

## Completion Checklist

Before finishing this lesson, confirm you can do all of the following:

- [ ] I understand that margin is transparent space **outside** an element's border
- [ ] I can set individual margins using `margin-top`, `margin-right`, `margin-bottom`, and `margin-left`
- [ ] I know the shorthand value order: Top → Right → Bottom → Left (TRouBLe)
- [ ] I can correctly decode all four shorthand patterns (1, 2, 3, and 4 values)
- [ ] I can use `margin: 0 auto` to horizontally centre an element (with a defined width)
- [ ] I can use `margin: inherit` to copy a margin from a parent element
- [ ] I understand what margin collapse is: vertical margins that meet collapse into the larger one
- [ ] I know that margin collapse only affects **top and bottom** margins, never left and right
- [ ] I know that `0` is the only margin value that does not need a unit
- [ ] I completed the Blog Article Layout mini project
- [ ] I used browser DevTools to observe the Box Model for a margin-collapsed element

---

## Real-World Connections

**Every website layout ever built uses margins** to control spacing. When you visit a news site, e-commerce store, or social media platform, the gaps between headlines, articles, cards, and buttons are all controlled by `margin`.

**The `margin: 0 auto` centring technique** is used in virtually every web project on the planet. The pattern of creating a centred content wrapper (`width: X; margin: 0 auto;`) is the foundation of fixed-width layout design.

**Margin collapse** was an intentional CSS design decision. It exists to make typography feel natural — when you stack paragraphs, headings, and text blocks, their vertical spacing collapses so that the total space between elements reflects the visual hierarchy rather than accumulating mechanically.

**CSS Frameworks like Bootstrap and Tailwind** build on top of margin fundamentals. When you use utility classes like `mt-4` (margin-top) in Tailwind or spacing utilities in Bootstrap, you are using exactly the same underlying margin properties you learned in this lesson.

---

## Lesson Summary

In this lesson you covered the complete picture of CSS margins — from basic individual properties all the way through the surprising behaviour of margin collapse.

**CSS Margins — Core Properties:**
- `margin-top`, `margin-right`, `margin-bottom`, `margin-left` control individual sides
- Values can be `px`, `em`, `rem`, `%`, `auto`, `inherit`, or `0`
- Negative margins are allowed and move elements in the opposite direction

**The Shorthand `margin` Property:**
- 4 values → top, right, bottom, left (clockwise)
- 3 values → top, left-and-right, bottom
- 2 values → top-and-bottom, left-and-right
- 1 value → all four sides equal

**Special Values:**
- `margin: auto` on left and right (with a defined width) horizontally centres a block element
- `margin: inherit` copies the margin value from the parent element
- `margin: 0` removes all margin — no unit needed for zero

**Margin Collapse:**
- When two vertical margins (top and bottom) of adjacent block elements meet, they do not add up — they collapse into a single margin equal to the **larger** of the two
- Horizontal (left and right) margins **never** collapse
- Understanding collapse is essential to predicting and debugging vertical spacing in your layouts

---

*End of Lesson 08 — CSS Margins and Margin Collapse*
