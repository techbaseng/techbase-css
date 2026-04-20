---
render_with_liquid: false
title: "The CSS Box Model"
nav_order: 11
---

# Lesson 11 — The CSS Box Model

---

## Lesson Introduction

Welcome to Lesson 11 — one of the most important lessons in this entire CSS course.

The **CSS Box Model** is the single most foundational concept in all of CSS layout. Every single element you place on a webpage — every heading, paragraph, image, button, card, and container — is treated by the browser as a **rectangular box**. Understanding exactly how that box is structured, how it is measured, and how its layers interact is what separates beginners who guess at spacing from developers who calculate layouts precisely and confidently.

Once you truly understand the Box Model, you will be able to:
- Predict exactly how wide and tall any element on your page will be
- Stop being surprised when adding padding makes your layout break
- Understand why CSS layouts sometimes overflow or collapse unexpectedly
- Control space inside and outside every element with complete confidence

This lesson also introduces `box-sizing: border-box` — a single property that changes how sizing is calculated and that every professional web developer uses on every project they build.

By the end of this lesson you will be able to:
- Name and describe all four layers of the CSS Box Model
- Calculate the total rendered width and height of any element
- Understand the difference between `content-box` (default) and `border-box` sizing
- Apply `box-sizing: border-box` to an entire project using the universal selector
- Use browser DevTools to inspect the Box Model of any live element
- Complete all Box Model code challenges from W3Schools
- Build a complete product card layout using precise Box Model calculations

---

## Prerequisite Concepts

Before we go deeper, let's make sure you are solid on these ideas.

### What is an HTML Element?

An HTML element is a piece of content marked up with a tag, like `<p>`, `<div>`, `<h1>`, or `<button>`. Every element you write in HTML gets rendered in the browser as a visible (or invisible) block of content on the page.

### What is CSS?

CSS (Cascading Style Sheets) is the language used to style HTML elements — controlling their colour, size, font, position, and spacing.

### What is a CSS Property?

A CSS property is an instruction you give to the browser about how to display an element. For example:

```css
p {
  color: navy;
  font-size: 16px;
  width: 300px;
}
```

- `color` → text colour property
- `font-size` → text size property
- `width` → how wide the element should be

In this lesson, the key properties we work with are `width`, `height`, `padding`, `border`, and `margin` — and how they all interact inside the Box Model.

---

## Part 1 — What is the CSS Box Model?

---

### 1.1 The Core Idea: Everything is a Box

Open any webpage right now — a news article, a social media post, an e-commerce product listing. Every single visible piece of content you see on that page, no matter how it looks visually, is a rectangle inside the browser.

The **CSS Box Model** is the system that describes the structure of that rectangle. It defines four distinct layers that surround every element, from the innermost content to the outermost edge.

> 💡 **Analogy — The Gift Box:** Imagine a gift inside a box. The gift itself is the **content**. The tissue paper cushioning the gift inside the box is the **padding**. The cardboard walls of the box form the **border**. The gap between this box and the other boxes sitting next to it on the shelf is the **margin**.

Each of these layers has a CSS property that controls it. Together, they define exactly how much space an element takes up on the page.

---

### 1.2 The Four Layers of the Box Model

Here is the complete diagram of the CSS Box Model:

```
+===============================================+
‖                   MARGIN                      ‖  ← Layer 4: outside space (transparent)
‖   +---------------------------------------+   ‖
‖   |               BORDER                 |   ‖  ← Layer 3: the visible frame/edge
‖   |   +-------------------------------+   |   ‖
‖   |   |           PADDING             |   |   ‖  ← Layer 2: inside space (fills w/ bg)
‖   |   |   +-----------------------+   |   |   ‖
‖   |   |   |       CONTENT         |   |   |   ‖  ← Layer 1: your actual text/image
‖   |   |   |   width × height      |   |   |   ‖
‖   |   |   +-----------------------+   |   |   ‖
‖   |   +-------------------------------+   |   ‖
‖   +---------------------------------------+   ‖
+===============================================+
```

Let's go through each layer from the inside out.

---

#### Layer 1 — Content

The **content area** is where your actual text, images, or other HTML lives. This is what you see when you type words inside a `<p>` tag or place an `<img>` tag on the page.

When you set `width` and `height` in CSS, **by default you are only setting the size of this content area** — not the total size of the element on screen. This is the most important and most misunderstood aspect of the Box Model.

```css
div {
  width: 300px;
  height: 150px;
}
```

This says: "Make the content area inside this div 300px wide and 150px tall." It says nothing about padding, border, or margin — those are separate.

---

#### Layer 2 — Padding

**Padding** is the transparent space between the content and the border. It sits **inside** the border, so it shares the element's background colour.

Think of padding as the cushion or breathing room around your content inside the box.

```css
div {
  padding: 20px;
}
```

This adds 20px of cushioning on all four sides between the content and the border.

**Key fact:** Padding is part of the element's clickable/visible area. If an element has a background colour, the padding area will show that background colour too.

---

#### Layer 3 — Border

The **border** is the line that wraps around the padding and content. It is the element's visible frame or edge.

```css
div {
  border: 5px solid gray;
}
```

This adds a 5px wide, solid grey border around the element. The border has a measurable thickness — and that thickness adds to the element's total size.

---

#### Layer 4 — Margin

**Margin** is the transparent space **outside** the border. It separates this element from neighbouring elements. Margin is never coloured and never shows the element's background — it is always invisible.

```css
div {
  margin: 30px;
}
```

This pushes 30px of empty space on all sides outside the border, creating distance from adjacent elements.

---

### 1.3 All Four Layers Together — A Complete Example

```css
div {
  width: 320px;
  height: 50px;
  padding: 10px;
  border: 5px solid gray;
  margin: 0;
}
```

Let's see each layer in action:

- **Content** is 320px wide and 50px tall
- **Padding** adds 10px on all four sides — cushioning between content and border
- **Border** adds 5px on all four sides — the visible grey frame
- **Margin** is 0 — no space outside the border

This element appears as a grey-bordered box. But what is its **actual total width on screen**? That brings us to the most critical calculation in the entire Box Model.

---

## Part 2 — Calculating Total Width and Height

---

### 2.1 The Big Surprise: `width` Is Not the Full Width

This is the concept that trips up beginners more than anything else in CSS.

When you write `width: 320px`, you are only setting the width of the **content area**. The padding and border are **added on top of** that width to calculate what the browser actually renders.

> ⚠️ **Critical Rule:** By default, `width` and `height` only apply to the **content area**. Padding and border are added on top to get the real rendered size.

---

### 2.2 The Total Width Formula

```
Total Element Width = width
                    + left padding + right padding
                    + left border  + right border
```

---

### 2.3 The Total Height Formula

```
Total Element Height = height
                     + top padding + bottom padding
                     + top border  + bottom border
```

---

### 2.4 Step-by-Step Width Calculation — The W3Schools Example

Let's carefully work through the canonical W3Schools Box Model example:

```css
div {
  width: 320px;
  height: 50px;
  padding: 10px;
  border: 5px solid gray;
  margin: 0;
}
```

**Step 1 — Identify each value:**
- Content width: `320px`
- Content height: `50px`
- Padding: `10px` on all four sides (so left padding = 10, right padding = 10)
- Border: `5px` on all four sides (so left border = 5, right border = 5)
- Margin: `0` (does not affect the element's own size)

**Step 2 — Calculate total width:**

```
Width  =  320px   (content area)
       +   10px   (left padding)
       +   10px   (right padding)
       +    5px   (left border)
       +    5px   (right border)
       = -------
         350px   ← TOTAL RENDERED WIDTH
```

**Step 3 — Calculate total height:**

```
Height =   50px   (content area)
       +   10px   (top padding)
       +   10px   (bottom padding)
       +    5px   (top border)
       +    5px   (bottom border)
       = -------
          80px   ← TOTAL RENDERED HEIGHT
```

**Expected result:** This `div` is painted as a `350px × 80px` box on the screen — even though you only wrote `width: 320px` and `height: 50px`. The padding and border expand it beyond what you declared.

---

### 2.5 What About Margin?

This is a subtle but important point.

**Margin does NOT affect the size of the element itself.** The element's rendered box stops at the border. Margin is space outside the box — it affects how much room the element takes up on the **page**, but it is not counted in the element's own width or height.

The official W3Schools rule states it clearly:

> *"The margin property also affects the total space that the box will take up on the page, but the margin is not included in the actual size of the box. The box's total width and height stops at the border."*

Think of it this way: if you measure a picture frame, you measure up to and including the frame itself. The gap between this frame and the next frame on the wall is real space — but it is not part of this frame's measurement.

---

### 2.6 More Worked Examples

---

**Example A — Large padding, no border:**

```css
.card {
  width: 400px;
  height: 200px;
  padding: 30px;
  border: 0;
  margin: 20px;
}
```

**Total width calculation:**

```
400px  (content)
+ 30px (left padding)
+ 30px (right padding)
+  0px (left border)
+  0px (right border)
= 460px  ← total rendered width
```

**Total height calculation:**

```
200px  (content)
+ 30px (top padding)
+ 30px (bottom padding)
+  0px (top border)
+  0px (bottom border)
= 260px  ← total rendered height
```

Margin (`20px`) does NOT change these sizes — it just creates space around the box.

---

**Example B — Asymmetric padding and border:**

```css
.banner {
  width: 600px;
  height: 80px;
  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 40px;
  padding-right: 40px;
  border-top: 2px solid black;
  border-bottom: 2px solid black;
  border-left: 0;
  border-right: 0;
}
```

**Total width calculation:**

```
600px  (content)
+ 40px (left padding)
+ 40px (right padding)
+  0px (left border — none)
+  0px (right border — none)
= 680px  ← total rendered width
```

**Total height calculation:**

```
 80px  (content)
+ 10px (top padding)
+ 10px (bottom padding)
+  2px (top border)
+  2px (bottom border)
= 104px  ← total rendered height
```

> 💡 **Thinking Prompt:** In Example B, what if you changed `padding-left` to `60px`? The content width stays `600px`, but the total rendered width becomes `600 + 60 + 40 + 0 + 0 = 700px`. The content area itself does not shrink — the whole box grows wider.

---

### 2.7 Why This Causes Problems in Real Layouts

Here is the classic layout-breaking scenario that every developer runs into:

Imagine you want two boxes side by side inside a `600px` container. You give each box `width: 300px` — exactly half. Perfect.

```css
.container {
  width: 600px;
}

.box {
  width: 300px;   /* 300 + 300 = 600, they should fit! */
  padding: 20px;
  border: 2px solid black;
  float: left;
}
```

**What actually happens:**

```
Each box actual width:
300px + 20px + 20px + 2px + 2px = 344px

Two boxes: 344px + 344px = 688px
Container: 600px

688 > 600 → The second box WRAPS to the next line! 💥
```

The layout breaks because `width: 300px` only set the content area. Padding and border pushed each box to 344px, which no longer fits.

This is the exact problem that `box-sizing: border-box` was designed to solve — which we cover in Part 3.

---

## Part 3 — `box-sizing`: Changing How Size is Calculated

---

### 3.1 The Default: `box-sizing: content-box`

By default, every browser uses `box-sizing: content-box`. This is what we have been describing all along:

- `width` and `height` apply **only** to the content area
- Padding and border are **added on top** → the element is larger than declared

```css
/* Default behaviour — content-box */
div {
  box-sizing: content-box;  /* this is the default, you don't need to write it */
  width: 300px;
  padding: 20px;
  border: 5px solid black;
  /* actual rendered width = 300 + 20 + 20 + 5 + 5 = 350px */
}
```

---

### 3.2 The Better Way: `box-sizing: border-box`

When you set `box-sizing: border-box`, the calculation changes completely:

- `width` and `height` define the **total rendered size** including padding and border
- Padding and border are **subtracted from inside** the declared size → the element is exactly as wide as you declared
- The content area shrinks to accommodate the padding and border

```css
/* border-box — the element is exactly 300px total */
div {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
  border: 5px solid black;
  /* actual rendered width = 300px (padding + border eat into content space) */
  /* content area = 300 - 20 - 20 - 5 - 5 = 250px */
}
```

**The total rendered width is exactly `300px` — no wider.**

---

### 3.3 Side-by-Side Comparison

```css
/* Box 1 — content-box (default) */
.box-a {
  box-sizing: content-box;
  width: 300px;
  height: 100px;
  padding: 50px;
  border: 1px solid blue;
}
/* Total rendered width  = 300 + 50 + 50 + 1 + 1 = 402px */
/* Total rendered height = 100 + 50 + 50 + 1 + 1 = 202px */


/* Box 2 — border-box */
.box-b {
  box-sizing: border-box;
  width: 300px;
  height: 100px;
  padding: 50px;
  border: 1px solid red;
}
/* Total rendered width  = 300px (exactly as declared) */
/* Total rendered height = 100px (exactly as declared) */
/* Content area width    = 300 - 50 - 50 - 1 - 1 = 198px */
/* Content area height   = 100 - 50 - 50 - 1 - 1 = -2px → content collapses */
```

> ⚠️ Note: In `.box-b` with `padding: 50px` on each side and only `100px` height, the content area height becomes negative — meaning there is no room for content at all. In practice you would not use such extreme padding. The example shows that `border-box` redistributes the space inward.

**Expected result:** `.box-a` appears much larger than `.box-b` even though both declare `width: 300px`. `.box-a` is 402px wide; `.box-b` is exactly 300px wide.

---

### 3.4 Solving the Two-Box Layout Problem with `border-box`

Remember the layout-breaking problem from Section 2.7? Here is the fix:

```css
.container {
  width: 600px;
}

.box {
  box-sizing: border-box;  /* magic fix */
  width: 300px;   /* NOW this includes padding and border */
  padding: 20px;
  border: 2px solid black;
  float: left;
}
```

**Now each box:**
- Is exactly `300px` wide (total, including padding and border)
- Two boxes: `300 + 300 = 600px`
- Container: `600px`
- They fit perfectly side by side ✅

---

### 3.5 The Universal `border-box` Reset

Because `border-box` is so much more intuitive and predictable, the vast majority of professional developers apply it to every element on every project. The standard way to do this is with the universal selector `*`:

```css
* {
  box-sizing: border-box;
}
```

The `*` selector targets every single HTML element on the page. This one line ensures that `width` and `height` always mean the total box size (including padding and border) for every element — no surprises, no overflow bugs from unexpected box growth.

> 💡 This is considered a **best practice** and is used in virtually every professional CSS project, framework (like Bootstrap and Tailwind), and design system in the world. Most developers add it at the very top of their CSS file before writing anything else.

---

### 3.6 Complete Comparison Table

| Scenario | `content-box` (default) | `border-box` |
|---|---|---|
| `width` applies to | Content area only | Content + padding + border |
| Adding padding | Makes box **grow** beyond declared width | Box stays declared width; content shrinks |
| Adding border | Makes box **grow** beyond declared width | Box stays declared width; content shrinks |
| Layout maths | Harder — must subtract padding/border from width | Easier — `width` is the final size |
| Industry usage | Browser default (legacy) | Used by almost all professionals |

---

## Part 4 — The Box Model in Browser DevTools

---

### 4.1 Seeing the Box Model Live

Every modern browser (Chrome, Firefox, Edge) has a built-in tool that draws the Box Model for any element you click on. This is one of the most valuable debugging tools in web development.

**How to open DevTools:**
- Windows/Linux: `F12` or `Ctrl + Shift + I`
- Mac: `Cmd + Option + I`
- Or: right-click any element on the page → click **Inspect**

---

### 4.2 What You See in the Box Model Panel

In Chrome/Edge DevTools:
1. Click the **Elements** tab at the top
2. Click on any HTML element in the panel
3. Scroll down in the right-hand **Styles** pane until you see the box diagram

The diagram looks like this:

```
+-------------------------------+
|           margin              |
|   +-----------------------+   |
|   |        border         |   |
|   |   +---------------+   |   |
|   |   |    padding    |   |   |
|   |   |   +-------+   |   |   |
|   |   |   |content|   |   |   |
|   |   |   |320×50 |   |   |   |
|   |   |   +-------+   |   |   |
|   |   +---------------+   |   |
|   +-----------------------+   |
+-------------------------------+
```

Each layer is labelled and shows its exact pixel values. Hovering over the diagram highlights that layer on the webpage itself in a different colour:
- **Blue** → content area
- **Green** → padding
- **Orange/yellow** → border
- **Beige/tan** → margin

This makes it extremely easy to:
- See what is causing unexpected sizing
- Verify your calculations are correct
- Identify which layer is pushing elements out of alignment

---

### 4.3 Live Editing in DevTools

You can double-click any value in the DevTools Styles panel and change it instantly. The page updates in real time — without saving any files. This is perfect for experimenting with different spacing values before committing to them in your CSS.

> 💡 **Professional tip:** Never guess spacing values. Open DevTools, inspect the element, tweak the numbers live until it looks right, then copy those final values back into your CSS file.

---

## Part 5 — Guided Practice Exercises

---

### Exercise 1 — Total Width and Height Calculations

Work through each of the following. Calculate the total rendered width and total rendered height for each element.

---

**Problem A:**

```css
.box-a {
  width: 200px;
  height: 100px;
  padding: 15px;
  border: 3px solid black;
  margin: 10px;
}
```

Work it out before reading the answer.

**Total Width:**
```
200px  (content)
+ 15px (left padding)
+ 15px (right padding)
+  3px (left border)
+  3px (right border)
= 236px  ← total rendered width
```

**Total Height:**
```
100px  (content)
+ 15px (top padding)
+ 15px (bottom padding)
+  3px (top border)
+  3px (bottom border)
= 136px  ← total rendered height
```

Margin (`10px`) does NOT affect the element's own size.

---

**Problem B:**

```css
.box-b {
  width: 500px;
  height: 300px;
  padding-top: 20px;
  padding-bottom: 20px;
  padding-left: 40px;
  padding-right: 40px;
  border: 1px solid red;
  margin: 0;
}
```

**Total Width:**
```
500px  (content)
+ 40px (left padding)
+ 40px (right padding)
+  1px (left border)
+  1px (right border)
= 582px  ← total rendered width
```

**Total Height:**
```
300px  (content)
+ 20px (top padding)
+ 20px (bottom padding)
+  1px (top border)
+  1px (bottom border)
= 342px  ← total rendered height
```

---

**Problem C:**

```css
.box-c {
  width: 150px;
  height: 150px;
  padding: 0;
  border: 10px double navy;
  margin: 25px;
}
```

> ⚠️ Note: `double` is a border-style value (two thin lines instead of one solid line). The border thickness is still `10px`.

**Total Width:**
```
150px  (content)
+  0px (left padding)
+  0px (right padding)
+ 10px (left border)
+ 10px (right border)
= 170px  ← total rendered width
```

**Total Height:**
```
150px  (content)
+  0px (top padding)
+  0px (bottom padding)
+ 10px (top border)
+ 10px (bottom border)
= 170px  ← total rendered height (a perfect square)
```

---

**Self-check questions:**
- In Problem A, would a `margin` of `50px` change the total rendered width? (No — margin is outside the box, it does not change the element's own size.)
- In Problem C, is the total rendered size affected by the `double` style vs `solid`? (No — only the thickness value `10px` matters for size calculation, not the style.)

---

### Exercise 2 — Working Backwards: Finding Content Width

Sometimes you know the **total width** you need, and you have to work out what `width` value to set given known padding and border.

**Formula:**
```
Content width = Total desired width
              − left padding − right padding
              − left border  − right border
```

---

**Problem A:**
You want a `.sidebar` to be exactly `280px` wide on screen. It has `padding: 20px` and `border: 2px solid grey`. What `width` value should you set?

```
Content width = 280 − 20 − 20 − 2 − 2
             = 280 − 44
             = 236px
```

**Solution:**

```css
.sidebar {
  width: 236px;      /* content area */
  padding: 20px;
  border: 2px solid grey;
  /* total rendered width: 236 + 20 + 20 + 2 + 2 = 280px ✅ */
}
```

---

**Problem B:**
A `.hero-banner` must be exactly `960px` wide. It has `padding-left: 60px`, `padding-right: 60px`, and `border: 4px solid transparent`. What should `width` be?

```
Content width = 960 − 60 − 60 − 4 − 4
             = 960 − 128
             = 832px
```

**Solution:**

```css
.hero-banner {
  width: 832px;
  padding-left: 60px;
  padding-right: 60px;
  border: 4px solid transparent;
  /* total rendered width: 832 + 60 + 60 + 4 + 4 = 960px ✅ */
}
```

---

**Problem C (with border-box):**
What if you simply use `box-sizing: border-box`? Solve Problem B again.

```css
/* With border-box: you just write the total you want! */
.hero-banner {
  box-sizing: border-box;
  width: 960px;       /* this IS the total — no calculation needed */
  padding-left: 60px;
  padding-right: 60px;
  border: 4px solid transparent;
  /* total rendered width: 960px exactly ✅ */
}
```

> 💡 This is exactly why `border-box` is so widely adopted. The maths disappears — you just write the width you want.

---

### Exercise 3 — Spotting the Problem and Fixing It

**Scenario:** A developer tried to create a three-column layout inside a `900px` container. Each column is supposed to be exactly `300px` wide. But the third column keeps wrapping to the next line. Find the bug and fix it.

**Broken code:**

```css
.container {
  width: 900px;
}

.column {
  width: 300px;
  padding: 15px;
  border: 2px solid #ccc;
  float: left;
}
```

**Diagnosing the bug:**

```
Each column actual width:
300px + 15px + 15px + 2px + 2px = 334px

Three columns: 334 × 3 = 1002px
Container: 900px

1002 > 900 → Third column wraps! 💥
```

**Fix using `border-box`:**

```css
.container {
  width: 900px;
}

.column {
  box-sizing: border-box; /* ← the fix */
  width: 300px;           /* now truly 300px total */
  padding: 15px;
  border: 2px solid #ccc;
  float: left;
}

/* Three columns: 300 × 3 = 900px → fits perfectly ✅ */
```

---

## Part 6 — Code Challenge Practice

These challenges mirror the style of questions from the W3Schools CSS Box Model Code Challenge page.

---

### Challenge 1 — Calculate a Total Width

**Question:** Using the default `box-sizing: content-box`, what is the total rendered width of this element?

```css
div {
  width: 250px;
  padding: 25px;
  border: 5px solid black;
}
```

**Work it out:**
```
250px + 25px + 25px + 5px + 5px = 310px
```

**Answer: 310px**

---

### Challenge 2 — Calculate a Total Height

**Question:** What is the total rendered height of this element?

```css
section {
  height: 120px;
  padding-top: 10px;
  padding-bottom: 30px;
  border-top: 4px solid blue;
  border-bottom: 4px solid blue;
}
```

**Work it out:**
```
120px + 10px + 30px + 4px + 4px = 168px
```

**Answer: 168px**

---

### Challenge 3 — What Does `border-box` Change?

**Question:** With `box-sizing: border-box` applied, what is the total rendered width of this element?

```css
div {
  box-sizing: border-box;
  width: 400px;
  padding: 40px;
  border: 10px solid red;
}
```

**Answer: 400px** — with `border-box`, the declared `width` IS the total. The content area shrinks to accommodate the padding and border: `400 − 40 − 40 − 10 − 10 = 300px` content area.

---

### Challenge 4 — Identify the Difference

**Question:** Two divs both have `width: 300px`. One uses `content-box`, one uses `border-box`. Both have `padding: 20px` and `border: 5px solid`. How much wider is the `content-box` div than the `border-box` div?

**`content-box` total width:**
```
300 + 20 + 20 + 5 + 5 = 350px
```

**`border-box` total width:**
```
300px (exactly as declared)
```

**Difference: `350 − 300 = 50px`**

The `content-box` div is 50px wider on screen, even though both declare the same `width: 300px`.

---

### Challenge 5 — Fix the Overflowing Layout

**Question:** A developer has a container that is `500px` wide. They add two divs inside it, each with `width: 250px`, `padding: 20px`, and `border: 5px solid`. The second div wraps to the next line. Add one property to each div to fix this.

**Fix:**

```css
div {
  box-sizing: border-box;  /* ← add this */
  width: 250px;
  padding: 20px;
  border: 5px solid;
  float: left;
}
/* Each div is now exactly 250px; 250 + 250 = 500px → fits! ✅ */
```

---

### Challenge 6 — Write the CSS for a Given Total Size

**Question:** Write CSS for a `.notification-bar` that:
- Must be exactly `760px` wide and `60px` tall on screen
- Must have `padding: 10px` on all sides
- Must have a `border: 3px solid orange`
- Use `content-box` sizing (no `box-sizing: border-box`)

**Solution:**

Content width = `760 − 10 − 10 − 3 − 3 = 734px`
Content height = `60 − 10 − 10 − 3 − 3 = 34px`

```css
.notification-bar {
  width: 734px;
  height: 34px;
  padding: 10px;
  border: 3px solid orange;
  /* total: 734 + 20 + 6 = 760px wide ✅ */
  /* total: 34 + 20 + 6 = 60px tall  ✅ */
}
```

---

## Part 7 — Mini Project: Product Card with Precise Box Model Control

Build a polished product card component that demonstrates complete mastery of the Box Model — every dimension will be precisely calculated and explained.

---

### Stage 1 — Project Goal and Setup

You will build a product card like you would see on an e-commerce website. The card must:
- Be **exactly 320px wide** as rendered on screen
- Contain an image placeholder, product name, description, price, and a buy button
- Use `box-sizing: border-box` globally
- Have all spacing controlled with precise padding, border, and margin values
- Include a comment for each CSS rule explaining the Box Model reasoning

Create two files: `product.html` and `product.css`.

---

### Stage 2 — HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Product Card — Box Model Demo</title>
  <link rel="stylesheet" href="product.css">
</head>
<body>

  <div class="page">

    <div class="card">

      <!-- Image placeholder -->
      <div class="card-image">
        <span class="image-label">Product Image</span>
      </div>

      <!-- Product details -->
      <div class="card-body">
        <p class="card-category">Electronics</p>
        <h2 class="card-title">Wireless Noise-Cancelling Headphones</h2>
        <p class="card-description">
          Crystal-clear audio with up to 30 hours of battery life.
          Foldable design for easy travel.
        </p>
        <div class="card-footer">
          <span class="card-price">₦89,500</span>
          <button class="card-button">Add to Cart</button>
        </div>
      </div>

    </div>

  </div>

</body>
</html>
```

---

### Stage 3 — CSS with Full Box Model Comments

```css
/*
  =========================================
  product.css
  Project: Product Card — Box Model Demo
  Key concept: Every size is intentional.
               Every dimension is calculated.
  =========================================
*/


/* ==============================
   GLOBAL BOX-SIZING RESET
   Makes width = total box size
   on every element — no surprises
   ============================== */

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}


/* ==============================
   PAGE — centres the card
   ============================== */

body {
  font-family: "Segoe UI", Arial, sans-serif;
  background-color: #f0f2f5;
  color: #1a1a1a;
}

.page {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  min-height: 100vh;
  padding: 60px 20px;
  /*
    Box Model note:
    padding: 60px 20px means 60px top+bottom, 20px left+right.
    Because box-sizing: border-box is on *, this padding is
    consumed within the page's own size, not added to it.
  */
}


/* ==============================
   CARD CONTAINER
   Target total width: 320px
   With border-box: width: 320px
   is exactly what renders.
   ============================== */

.card {
  width: 320px;
  /*
    With box-sizing: border-box applied globally,
    this card will be EXACTLY 320px wide on screen,
    regardless of any padding or border we add.
    Without border-box, this would only set the
    content area — padding + border would make it wider.
  */
  background-color: #ffffff;
  border-radius: 12px;
  border: 1px solid #e0e0e0;
  overflow: hidden;            /* clips image placeholder to rounded corners */
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.08);
}


/* ==============================
   IMAGE PLACEHOLDER
   Full-width area, fixed height
   ============================== */

.card-image {
  width: 100%;
  /*
    width: 100% means: take the full width of the parent (.card).
    Since .card is 320px, this area is also 320px wide.
    Because border-box is applied, any padding here stays inside 320px.
  */
  height: 180px;
  background-color: #d0d8e4;
  display: flex;
  align-items: center;
  justify-content: center;
}

.image-label {
  font-size: 13px;
  color: #7a8599;
  letter-spacing: 1px;
  text-transform: uppercase;
}


/* ==============================
   CARD BODY — content + spacing
   padding creates inner cushion
   ============================== */

.card-body {
  padding: 20px;
  /*
    Box Model note:
    padding: 20px adds 20px of space between the card's
    inner edge and all content inside the body area.
    Because of border-box, this does NOT expand the card
    beyond 320px — the content area becomes 320 - 20 - 20 = 280px wide.
    The padding is the cushion between content and the card border.
  */
}


/* ==============================
   CATEGORY LABEL
   ============================== */

.card-category {
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  color: #e07b39;
  margin-bottom: 8px;
  /*
    margin-bottom: 8px creates 8px of transparent space
    below this element, pushing the title down.
    This is margin — outside the element's border.
  */
}


/* ==============================
   PRODUCT TITLE
   ============================== */

.card-title {
  font-size: 17px;
  font-weight: 700;
  line-height: 1.4;
  color: #1a1a2e;
  margin-bottom: 10px;
}


/* ==============================
   PRODUCT DESCRIPTION
   ============================== */

.card-description {
  font-size: 13px;
  line-height: 1.6;
  color: #555555;
  margin-bottom: 18px;
}


/* ==============================
   CARD FOOTER — price + button
   ============================== */

.card-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-top: 16px;
  border-top: 1px solid #f0f0f0;
  /*
    Box Model note:
    padding-top: 16px adds 16px of inner cushion above
    the footer's content (between the top border-line and
    the price/button text).
    border-top: 1px solid creates a thin divider line.
    Both are inside the card body's 20px side padding.
  */
}


/* ==============================
   PRICE
   ============================== */

.card-price {
  font-size: 20px;
  font-weight: 800;
  color: #1a1a2e;
}


/* ==============================
   ADD TO CART BUTTON
   padding controls button size
   ============================== */

.card-button {
  padding: 10px 18px;
  /*
    Box Model note:
    padding: 10px 18px means 10px top+bottom, 18px left+right.
    This IS the button's visual size — buttons have no fixed width,
    so they size themselves from their content + padding.
    Total button height  = line-height of text + 10 + 10 + borders.
    Total button width   = text width + 18 + 18 + borders.
  */
  background-color: #1a1a2e;
  color: #ffffff;
  border: none;
  border-radius: 6px;
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.card-button:hover {
  background-color: #e07b39;
}
```

---

### Stage 4 — Milestone Check

Open `product.html` in your browser. You should see:

- A centred card on a light grey page background
- A blue-grey image placeholder area at the top (180px tall)
- A product category label in orange below the image
- A bold product title
- A short grey description paragraph
- A divider line above the footer
- The price on the left and an "Add to Cart" button on the right
- The button changes to orange on hover

Open DevTools and click the `.card` element. In the Box Model diagram, verify:
- The content area shows the exact rendered size
- Padding shows `20px` on all sides of `.card-body`
- The border is `1px` on the card outline
- The box-sizing diagram confirms border-box sizing

---

### Stage 5 — Box Model Experiments

Try each of these experiments. Observe, understand, then undo before the next one.

**Experiment A:** Temporarily remove `box-sizing: border-box` from the `*` selector. Reload. Does the card change size? Check in DevTools. Restore `border-box` when done.

**Experiment B:** Change `.card-body` padding from `20px` to `40px`. Does the card get wider? (With `border-box`: No — the content area shrinks. Without `border-box`: Yes — the card grows.) This is the clearest way to feel the difference.

**Experiment C:** Add `border: 10px solid red` to `.card`. Does the card grow? (With `border-box`: No — the red border eats inward. Without `border-box`: Yes — the card grows by 20px total.) Observe in DevTools.

**Experiment D:** Add `margin: 40px` to `.card`. The card moves away from the page centre — but does the card's own size in DevTools change? (No — margin is outside the box.)

---

### Reflection Questions

1. If you had not used `box-sizing: border-box`, and you added `padding: 20px` to `.card-body`, by how much wider would the total card have grown?
2. Look at `.card-button`. It has no explicit `width`. Where does its width come from in the Box Model?
3. What would happen if you added `border: 5px solid black` to `.card-body` without `border-box`? Would the inner content still be exactly 280px wide?
4. The `.card-footer` has `border-top: 1px`. Does this border affect the width of the card? Why or why not?

---

## Common Beginner Mistakes

---

### Mistake 1 — Assuming `width` Is the Total Width

```css
/* WRONG assumption: "this box is 300px wide" */
.box {
  width: 300px;
  padding: 20px;
  border: 5px solid;
}
/* Actual width: 300 + 20 + 20 + 5 + 5 = 350px */

/* RIGHT approach: use border-box */
.box {
  box-sizing: border-box;
  width: 300px;   /* THIS is actually 300px */
  padding: 20px;
  border: 5px solid;
}
```

---

### Mistake 2 — Including Margin in the Size Calculation

```css
.box {
  width: 200px;
  padding: 10px;
  border: 2px solid;
  margin: 30px;
}
/* WRONG: "total size = 200 + 10 + 10 + 2 + 2 + 30 + 30 = 284px" ❌ */
/* RIGHT: total rendered size = 200 + 10 + 10 + 2 + 2 = 224px      ✅ */
/* Margin (30px each side) affects page space, NOT the element's own size */
```

---

### Mistake 3 — Forgetting to Set `box-sizing` Globally

```css
/* INCOMPLETE — only applies to div, not to every element */
div {
  box-sizing: border-box;
}

/* CORRECT — applies to every single element */
* {
  box-sizing: border-box;
}
```

If you only apply `border-box` to some elements, you end up with inconsistent sizing behaviour across your page — some elements use one model, others use another, and layouts become unpredictable.

---

### Mistake 4 — Setting a Width That Leaves No Room for Content

```css
/* PROBLEMATIC with border-box */
.tiny-box {
  box-sizing: border-box;
  width: 50px;
  padding: 30px;   /* 30 + 30 = 60px — more than the total width! */
  border: 5px solid;
}
/* Content area = 50 - 30 - 30 - 5 - 5 = -20px → collapses to 0 */
```

With `border-box`, if your padding and border together exceed the declared width, the content area collapses to zero. Content will overflow or be invisible. Always make sure your `width` is large enough to accommodate your padding and border.

---

### Mistake 5 — Thinking Padding and Margin Do the Same Thing

```css
/* PADDING — space INSIDE the border, fills with background colour */
.card {
  background-color: lightblue;
  padding: 20px;   /* the lightblue area extends 20px around the content */
}

/* MARGIN — space OUTSIDE the border, always transparent */
.card {
  margin: 20px;   /* transparent gap between this card and other elements */
}
```

Use **padding** when you want space between content and border (inner cushion).
Use **margin** when you want space between this element and the elements around it (outer gap).

---

### Mistake 6 — Adding Border Without Accounting for It

```css
/* You want a nav bar that is exactly 960px wide */
.navbar {
  width: 960px;
  padding: 0 20px;
  border: 2px solid #333;  /* often forgotten in the size calculation */
}
/* Actual width (content-box): 960 + 20 + 20 + 2 + 2 = 1004px */
/* The navbar is wider than intended and may overflow the page! */

/* Fix — use border-box */
.navbar {
  box-sizing: border-box;
  width: 960px;   /* total, including border */
  padding: 0 20px;
  border: 2px solid #333;
}
```

---

## Completion Checklist

Before finishing this lesson, confirm you can do all of the following:

- [ ] I can name and describe all four layers of the CSS Box Model (content, padding, border, margin)
- [ ] I understand that `width` and `height` set the **content area** only by default
- [ ] I can use the total width formula: `width + left padding + right padding + left border + right border`
- [ ] I can use the total height formula: `height + top padding + bottom padding + top border + bottom border`
- [ ] I know that margin does NOT affect an element's own size (the box stops at the border)
- [ ] I understand the difference between `box-sizing: content-box` (default) and `box-sizing: border-box`
- [ ] I can explain why `border-box` makes layout maths easier
- [ ] I know how to apply `border-box` to every element using `* { box-sizing: border-box; }`
- [ ] I can open browser DevTools and read the Box Model diagram for any element
- [ ] I completed the total width/height calculation exercises correctly
- [ ] I completed the product card mini project
- [ ] I performed the Box Model experiments and understood each result

---

## Real-World Connections

**Every CSS layout system ever built is grounded in the Box Model.** Flexbox, CSS Grid, Bootstrap's 12-column grid, Tailwind CSS utility classes — all of them are ultimately arranging boxes defined by the Box Model rules you learned in this lesson.

**`box-sizing: border-box` is in every major CSS framework.** Bootstrap resets to `border-box` in its base stylesheet. Tailwind does too. Any professional boilerplate or starter template you encounter in the industry will include `* { box-sizing: border-box; }` at the very top.

**The DevTools Box Model diagram** is one of the first things professional developers open when something in a layout looks wrong. Being fluent with this tool will dramatically reduce your debugging time on every project.

**Precise size calculations** matter enormously in UI components. When building a product card, a modal dialog, a navigation bar, or a form input, you need to know exactly how wide something will be so it aligns correctly with everything around it. The Box Model gives you the formula to always know.

---

## Lesson Summary

In this lesson you mastered the CSS Box Model — the most foundational concept in CSS layout.

**The Four Layers:**
- **Content** — your actual text or image; `width` and `height` set this area
- **Padding** — transparent cushion inside the border; shares the element's background
- **Border** — the visible frame; has a measurable thickness
- **Margin** — transparent gap outside the border; creates distance from other elements

**Total Size Formulas (content-box default):**
- Total width = `width + left padding + right padding + left border + right border`
- Total height = `height + top padding + bottom padding + top border + bottom border`
- Margin is NOT included in the element's own size

**`box-sizing` Property:**
- `content-box` (default) → `width`/`height` apply to content only; padding and border add to the size
- `border-box` → `width`/`height` are the total rendered size; padding and border consume from inside
- Apply globally with `* { box-sizing: border-box; }` — this is a universal professional best practice

**Tools:**
- Browser DevTools Box Model diagram shows every layer in real pixel values
- Double-click any value to experiment live without saving files

---

*End of Lesson 11 — The CSS Box Model*
