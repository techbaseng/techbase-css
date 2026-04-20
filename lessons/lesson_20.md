---
render_with_liquid: false
title: "CSS max-width – Controlling How Wide Elements Can Grow"
nav_order: 20
---

# Lesson 20: CSS `max-width` — Controlling How Wide Elements Can Grow

---

## Lesson Introduction

Imagine you are reading an article on a large desktop monitor. Without any limits, the text would stretch from the far left edge of your screen all the way to the far right — one enormous, hard-to-read line. Your eyes would have to travel a huge distance to get from the end of one line to the beginning of the next. That is exhausting and uncomfortable.

Now imagine the same article with text that only takes up a comfortable central column, even on a wide screen. Your eyes barely move. Reading feels effortless.

That comfort is what `max-width` creates.

In this lesson you will learn:

- What `max-width` is and the exact problem it solves
- How `max-width` differs from `width`
- How to combine `max-width` with `margin: auto` to centre elements
- The difference between `max-width` and `min-width`
- How to use `max-width` with images so they never overflow their containers
- How `max-width` supports responsive design
- All the values `max-width` accepts
- How to use `max-width` in real-world page layouts

By the end, you will understand one of the most-used properties in professional CSS and will be able to apply it confidently in your own projects.

> **Prerequisite check:** You should be comfortable with the CSS `width` and `height` properties, basic CSS selectors, and the concept of block-level elements (like `<div>`, `<p>`, `<h1>`). If you have completed the earlier lessons in this series, you are fully prepared.

---

## Prerequisite Concepts

### What Is a Block-Level Element?

A **block-level element** is an HTML element that, by default, takes up the **full width of its parent container**. It also starts on a new line and pushes everything after it onto a new line.

Common block-level elements:

```html
<div>, <p>, <h1>, <h2>, <h3>, <article>, <section>, <main>, <header>, <footer>
```

Because block-level elements naturally stretch to fill their full parent width, they can become **very wide** on large screens if nothing tells them to stop growing. `max-width` is the tool that controls that growth.

### Quick Reminder: What Does `width` Do?

The `width` property sets a **fixed, exact width** for an element:

```css
div {
  width: 500px;
}
```

This makes the `<div>` exactly 500 pixels wide — always. Even if the screen is only 300 pixels wide (like a small phone), the element still tries to be 500 pixels wide, causing the user to scroll sideways. That is a serious problem on mobile devices.

`max-width` solves this problem elegantly.

---

## Part 1: Understanding `max-width`

### What Is `max-width`?

`max-width` sets the **maximum** width an element is allowed to reach. It says: "You can be as wide as your content or container allows, but never wider than this limit."

Think of it like a speed limit sign. A car can go slower than the speed limit — it can crawl, idle, or drive at any speed below it. But it may not exceed the posted limit.

Similarly, an element with `max-width: 800px` can be 200px wide, 500px wide, or 800px wide — but it will **never exceed 800px**, no matter how wide the screen is.

```
Screen width:  400px  → Element width: 400px   (fills available space, under the limit)
Screen width:  800px  → Element width: 800px   (exactly at the limit)
Screen width: 1200px  → Element width: 800px   (capped at max-width)
Screen width: 1920px  → Element width: 800px   (still capped)
```

### Why Is This So Useful?

Without `max-width`, block-level elements stretch to fill their entire container. On a huge widescreen monitor, a paragraph of text would span the full width of the screen — perhaps 1,500 or 1,900 pixels wide. Readable line length for comfortable reading is roughly 600–900 pixels (about 60–80 characters per line). `max-width` enforces that comfortable limit automatically.

### The Key Difference: `width` vs `max-width`

This is the most important concept in this lesson:

| Property | Behaviour | Mobile result |
|---|---|---|
| `width: 800px` | Always exactly 800px, even on a 320px phone screen | Forces horizontal scrolling — bad! |
| `max-width: 800px` | Up to 800px wide, but shrinks on smaller screens | Naturally fits any screen — good! |

```css
/* RIGID — Breaks on small screens */
.box-fixed {
  width: 800px;
}

/* FLEXIBLE — Works on all screen sizes */
.box-flexible {
  max-width: 800px;
}
```

> **Analogy:** `width` is like a wooden plank — it has one fixed length and cannot bend. `max-width` is like a rubber band — it can stretch up to its maximum length, but it also contracts naturally when there is less space.

### Your First `max-width` Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>max-width Basics</title>
  <style>
    .box-no-limit {
      background-color: #f0a500;
      padding: 20px;
      margin-bottom: 20px;
    }

    .box-with-limit {
      background-color: #3a86ff;
      padding: 20px;
      max-width: 500px;
    }
  </style>
</head>
<body>

  <div class="box-no-limit">
    I have NO max-width. I stretch to fill the entire page width.
  </div>

  <div class="box-with-limit">
    I have max-width: 500px. I never grow wider than 500px, but I can be narrower on small screens.
  </div>

</body>
</html>
```

**Expected Output:**

On a wide screen (e.g. 1200px wide):
- The orange box stretches the full 1200px width.
- The blue box is exactly 500px wide (capped by `max-width`).

On a narrow screen (e.g. 350px wide):
- The orange box stretches the full 350px width.
- The blue box is also 350px wide — it shrank naturally below its `max-width` limit to fit the screen.

> **Thinking prompt:** What would happen to the blue box if you resized your browser window to be narrower than 500px? It would shrink to fit the window. What would happen if you had used `width: 500px` instead? The box would overflow and cause horizontal scrollbars.

---

## Part 2: `max-width` with `margin: auto` — Centring Elements

### The Problem: Left-Aligned by Default

When you apply `max-width` to a block-level element, it caps the width — but the element stays aligned to the **left** by default.

```css
.container {
  max-width: 700px;
  background-color: #e0e0e0;
  padding: 20px;
}
```

On a 1200px screen, this creates a 700px grey box stuck to the left side of the page. It works, but it looks unbalanced.

### The Solution: `margin: auto`

Adding `margin: auto` to a block element with a defined (or max) width makes the browser **automatically distribute the remaining space equally** on the left and right sides, which centres the element.

```css
.container {
  max-width: 700px;
  margin: auto;           /* or: margin: 0 auto; */
  background-color: #e0e0e0;
  padding: 20px;
}
```

How `margin: auto` calculates the centering:

```
Page width:     1200px
Element width:   700px
Leftover space:  500px

margin: auto → left margin = 250px, right margin = 250px
Result: element is perfectly centred.
```

### Full Example — Centred Content Container

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Centred Container</title>
  <style>
    body {
      background-color: #f5f5f5;
      margin: 0;
      padding: 20px;
    }

    .container {
      max-width: 700px;
      margin: 0 auto;          /* 0 = top/bottom margin, auto = left/right */
      background-color: white;
      padding: 30px 40px;
      border: 1px solid #ddd;
      border-radius: 8px;
    }

    h1 {
      color: #333;
    }

    p {
      color: #555;
      line-height: 1.7;
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>Welcome to My Article</h1>
    <p>
      This container has a max-width of 700px. On wide screens it appears as
      a centred column. On narrow screens it shrinks to fill the available
      space. This is a very common pattern used on almost every modern website.
    </p>
    <p>
      Notice how the text never stretches uncomfortably wide. This makes it
      much easier to read on large desktop monitors.
    </p>
  </div>

</body>
</html>
```

**Expected Output:**
A white, centred card with a subtle border and rounded corners sits on a light grey background. On a wide screen, the card is 700px wide with equal grey space on both sides. On a narrow screen, the card fills the available width.

**Line-by-line explanation:**

- `max-width: 700px;` — Caps the container width at 700 pixels.
- `margin: 0 auto;` — The `0` sets zero margin on the top and bottom. The `auto` sets equal, automatic margins on the left and right, which centres the box.
- `padding: 30px 40px;` — 30px of breathing room on top/bottom, 40px on left/right, so text does not press against the edges.
- `border-radius: 8px;` — Softly rounds the corners of the container.

> **Important note:** `margin: auto` only works for centring **block-level elements** that have a defined width or `max-width`. It does not work for centring inline elements or elements without a width constraint.

---

## Part 3: How `max-width` Compares to `width` in Detail

Let's put both properties side by side in a real demonstration to feel the difference clearly:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>width vs max-width</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }

    /* Box 1: Fixed width — WILL overflow on small screens */
    .box-fixed {
      width: 600px;
      background-color: #ffadad;
      padding: 20px;
      margin-bottom: 15px;
    }

    /* Box 2: max-width — adapts gracefully */
    .box-max {
      max-width: 600px;
      background-color: #caffbf;
      padding: 20px;
      margin-bottom: 15px;
    }

    /* Box 3: max-width + centred */
    .box-max-centred {
      max-width: 600px;
      margin: 0 auto 15px auto;
      background-color: #9bf6ff;
      padding: 20px;
    }
  </style>
</head>
<body>

  <div class="box-fixed">
    Box 1 — width: 600px (always 600px — overflows small screens)
  </div>

  <div class="box-max">
    Box 2 — max-width: 600px (up to 600px — shrinks on small screens)
  </div>

  <div class="box-max-centred">
    Box 3 — max-width: 600px + margin: auto (centred on wide screens)
  </div>

</body>
</html>
```

**Expected Output (on a 1000px screen):**
- Red box: stretches to exactly 600px, aligned left.
- Green box: stretches to exactly 600px, aligned left.
- Blue box: stretches to exactly 600px, **centred** on the page.

**Expected Output (on a 400px screen):**
- Red box: 600px wide — overflows off the right side of the screen, creating a horizontal scrollbar. ❌
- Green box: 400px wide — naturally shrinks to fit the screen. ✅
- Blue box: 400px wide — naturally shrinks to fit, still centred. ✅

---

## Part 4: Understanding `max-width` Values

`max-width` accepts several types of values. Each has a specific use:

### 1. Pixel Values (`px`)

A fixed pixel cap. The element will never exceed this many pixels.

```css
.article {
  max-width: 800px;
}
```

Use when: You know the exact maximum size you want, such as a readable article column.

### 2. Percentage Values (`%`)

A percentage of the **parent element's** width. As the parent grows or shrinks, the max-width adjusts proportionally.

```css
.sidebar {
  max-width: 30%;
}
```

Use when: You want the max-width to be relative to the surrounding layout.

### 3. `none` (the default)

`max-width: none` means there is **no maximum width limit**. The element can grow as wide as its container allows. This is the default value for every element.

```css
.full-width {
  max-width: none;   /* No limit — this is the default */
}
```

Use when: You want to remove a previously set `max-width`, such as overriding a general rule for a specific element.

### 4. `fit-content`

The element sizes itself to fit its content, but will not exceed its parent's width.

```css
.badge {
  max-width: fit-content;
  background-color: #0070f3;
  color: white;
  padding: 6px 14px;
  border-radius: 20px;
}
```

### 5. `min-content` and `max-content`

These are advanced values that size the element based on its content's minimum or maximum natural width. We will cover them fully in later lessons.

### 6. Viewport Width (`vw`)

`vw` stands for **viewport width**. `1vw` equals 1% of the viewport (browser window) width.

```css
.hero-section {
  max-width: 90vw;   /* Never wider than 90% of the browser window */
}
```

---

## Part 5: `max-width` with Images

### The Problem: Images Overflow Their Containers

By default, images display at their natural (original) size. If you have a 1200px wide image inside a 400px container, the image overflows way beyond the container's edge.

```html
<!-- Without max-width — image overflows! -->
<div style="width: 400px; border: 2px solid red;">
  <img src="photo.jpg">
  <!-- If photo.jpg is 1200px wide, it overflows 800px beyond the box -->
</div>
```

### The Solution: `max-width: 100%` on Images

The single most important CSS rule you can apply to images for responsive design:

```css
img {
  max-width: 100%;
}
```

This single line means: "The image can be as wide as its natural size, but it must never exceed 100% of its container's width."

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Responsive Images with max-width</title>
  <style>
    .narrow-container {
      width: 300px;
      border: 2px solid #333;
      padding: 10px;
      margin-bottom: 20px;
    }

    /* Without this rule, a large image would overflow */
    img {
      max-width: 100%;
      height: auto;   /* Keeps the image proportions correct */
      display: block;
    }
  </style>
</head>
<body>

  <div class="narrow-container">
    <p>Image constrained to container width:</p>
    <img src="https://via.placeholder.com/800x400" alt="Example wide image">
  </div>

</body>
</html>
```

**Expected Output:**
The image (originally 800px wide) is shown inside a 300px container. Instead of overflowing, it shrinks to exactly 300px wide, maintaining its correct proportions (height adjusts automatically due to `height: auto`).

**Why `height: auto` is important:**
When you shrink an image's width, you must also let the height adjust naturally. If you set `max-width: 100%` but leave `height` at its natural value, the image will appear squashed horizontally. `height: auto` tells the browser: "Recalculate the height proportionally whenever the width changes."

> **This is one of the most universally used CSS rules in professional web development.** Many developers include `img { max-width: 100%; height: auto; }` in every project's base CSS as a default rule.

---

## Part 6: `min-width` vs `max-width`

Now that you understand `max-width`, let us compare it with `min-width` — they are related but solve opposite problems:

| Property | What it controls | Analogy |
|---|---|---|
| `max-width` | The MAXIMUM the element can grow to | Speed limit — "Don't go above this" |
| `min-width` | The MINIMUM the element will shrink to | Height requirement — "You must be at least this tall" |

### `min-width` Example

```css
.button {
  min-width: 150px;    /* Button is never narrower than 150px */
  padding: 10px 20px;
  background-color: #0070f3;
  color: white;
  border: none;
  border-radius: 5px;
}
```

A short button label like "OK" would naturally be tiny. `min-width: 150px` ensures the button always looks like a proper button, even with short text.

### Using Both Together

You can use `min-width` and `max-width` at the same time to create a **flexible range**:

```css
.sidebar {
  min-width: 200px;    /* Never shrinks below 200px */
  max-width: 350px;    /* Never grows beyond 350px */
}
```

This tells the browser: "The sidebar must stay between 200px and 350px wide. Smaller screens can go down to 200px, and larger screens can go up to 350px, but neither beyond their respective limits."

### Full Comparison Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>min-width vs max-width</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }

    .demo-box {
      padding: 20px;
      margin-bottom: 15px;
      color: white;
      font-size: 14px;
    }

    /* Only max-width */
    .only-max {
      max-width: 400px;
      background-color: #e63946;
    }

    /* Only min-width */
    .only-min {
      min-width: 400px;
      background-color: #457b9d;
    }

    /* Both together */
    .both {
      min-width: 200px;
      max-width: 400px;
      background-color: #2a9d8f;
    }
  </style>
</head>
<body>

  <div class="only-max demo-box">
    max-width: 400px only.
    On wide screens I am 400px. On narrow screens I shrink.
  </div>

  <div class="only-min demo-box">
    min-width: 400px only.
    I never shrink below 400px. I can grow wider than 400px.
  </div>

  <div class="both demo-box">
    min-width: 200px AND max-width: 400px.
    I stay within this range on all screens.
  </div>

</body>
</html>
```

**Expected Output (on a 600px screen):**
- Red box: 400px wide (at its maximum).
- Blue box: stretches to 600px (no maximum set).
- Green box: 400px wide (at its maximum, within range).

**Expected Output (on a 250px screen):**
- Red box: 250px wide (shrank to fit).
- Blue box: 400px wide (refuses to shrink below minimum, causes overflow).
- Green box: 250px wide (shrank, still above its 200px minimum — it is within range).

---

## Part 7: `max-width` in Real-World Page Layouts

The `max-width` + `margin: auto` pattern is the foundation of almost every modern website's layout. Let's look at how professionals use it.

### Pattern 1 — The Page Wrapper / Container

The most common use of `max-width` in all of web development:

```css
/* The universal "page wrapper" pattern */
.wrapper {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;     /* Side padding prevents content from touching screen edges on mobile */
}
```

Every major section of the page is wrapped in this class. On a 1440px monitor, content is 1200px wide and centred with 120px of margin on each side. On a 375px phone, content fills the screen width minus the 20px side padding.

```html
<header>
  <div class="wrapper">
    <nav>...</nav>
  </div>
</header>

<main>
  <div class="wrapper">
    <article>...</article>
  </div>
</main>

<footer>
  <div class="wrapper">
    <p>Footer content</p>
  </div>
</footer>
```

### Pattern 2 — The Readable Article Column

Articles and blog posts use a narrower `max-width` for ideal reading comfort (60–80 characters per line):

```css
.article-body {
  max-width: 680px;
  margin: 0 auto;
  font-size: 18px;
  line-height: 1.8;
  color: #333;
}
```

### Pattern 3 — Constrained Form Width

Forms that are too wide look unprofessional and are hard to fill in:

```css
.form-container {
  max-width: 500px;
  margin: 40px auto;
  padding: 30px;
  background: white;
  border-radius: 10px;
  box-shadow: 0 2px 12px rgba(0,0,0,0.1);
}
```

### Pattern 4 — Responsive Card Grid

Individual cards in a grid often use `max-width` to prevent them from growing awkwardly wide in large grid cells:

```css
.card {
  max-width: 380px;
  margin: 0 auto;
  background: white;
  border-radius: 8px;
  overflow: hidden;
}
```

---

## Part 8: Guided Practice Exercises

### Exercise 1 — Fix the Broken Layout

**Objective:** Understand why `max-width` is better than `width` for responsive pages.

**Scenario:** A developer has built a blog post page with `width: 900px` on the article. On mobile, users have to scroll sideways to read. Your job is to fix it.

**The broken code:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Blog Post</title>
  <style>
    body {
      font-family: Georgia, serif;
      background-color: #f9f9f9;
      padding: 20px;
    }

    .article {
      width: 900px;       /* ← This is the problem */
      background: white;
      padding: 40px;
      border: 1px solid #ddd;
    }

    h1 { color: #222; }
    p  { line-height: 1.8; color: #444; }
  </style>
</head>
<body>
  <div class="article">
    <h1>The Art of Slow Travel</h1>
    <p>
      Slow travel is about more than just moving at a leisurely pace.
      It is a philosophy of deep engagement with each place you visit.
      Instead of ticking off landmarks, you sit in a café for hours,
      strike up conversations with locals, and let a city reveal itself
      to you gradually.
    </p>
    <p>
      When you travel slowly, you notice the rhythm of a neighbourhood —
      the morning sounds, the way light falls on a particular street corner
      in the afternoon, the smell of street food in the evening. These are
      the moments that photographs cannot capture.
    </p>
  </div>
</body>
</html>
```

**Your task:** Fix the `.article` CSS so the article:
- Has a maximum width of 900px (not a fixed width)
- Is centred on the page
- Works correctly on both wide and narrow screens

**Solution:**

```css
.article {
  /* OLD (broken): width: 900px; */
  max-width: 900px;     /* Changed: now it can shrink on small screens */
  margin: 0 auto;       /* Added: centres the article on wide screens */
  background: white;
  padding: 40px;
  border: 1px solid #ddd;
}
```

**What changed:**
- `width: 900px` → `max-width: 900px`: Allows the article to shrink below 900px on small screens instead of overflowing.
- `margin: 0 auto`: Centres the article horizontally on screens wider than 900px.

**Self-check Questions:**
- On a 600px screen, what width will the article be now? *(Answer: 600px — it fills the available space, which is under the 900px max.)*
- On a 1400px screen, what width will the article be? *(Answer: 900px — capped at its maximum.)*
- What would happen if you removed `margin: 0 auto`? *(Answer: The article would be 900px wide but left-aligned on wide screens.)*

---

### Exercise 2 — Build a Centred Sign-Up Form

**Objective:** Create a responsive, centred sign-up form using `max-width`.

**Scenario:** You are building a sign-up page for a newsletter. The form should be centred, constrained to a comfortable width, and work well on both mobile and desktop.

**Steps:**
1. Create a page with a light background.
2. Create a `.form-wrapper` div that is centred with `max-width: 480px`.
3. Inside, add a heading, a short description, and input fields for Name and Email.
4. Add a submit button that spans the full width of the form.

**Solution:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Newsletter Sign-Up</title>
  <style>
    * {
      box-sizing: border-box;   /* Makes padding not add to total width */
    }

    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      background-color: #eef2f7;
      margin: 0;
      padding: 40px 16px;      /* 16px side padding prevents edge-hugging on mobile */
    }

    /* THE KEY PATTERN: max-width + margin auto */
    .form-wrapper {
      max-width: 480px;
      margin: 0 auto;
      background-color: white;
      border-radius: 12px;
      padding: 40px 36px;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
    }

    .form-wrapper h2 {
      margin: 0 0 8px 0;
      font-size: 24px;
      color: #1a1a2e;
    }

    .form-wrapper p {
      margin: 0 0 28px 0;
      color: #666;
      font-size: 15px;
      line-height: 1.5;
    }

    label {
      display: block;
      font-size: 14px;
      font-weight: 600;
      color: #333;
      margin-bottom: 6px;
    }

    input {
      width: 100%;             /* Input fills the form wrapper */
      padding: 12px 14px;
      font-size: 15px;
      border: 1.5px solid #ccc;
      border-radius: 7px;
      margin-bottom: 20px;
      outline: none;
    }

    input:focus {
      border-color: #4361ee;
    }

    .btn-submit {
      width: 100%;             /* Button spans full form width */
      padding: 14px;
      background-color: #4361ee;
      color: white;
      font-size: 16px;
      font-weight: 600;
      border: none;
      border-radius: 7px;
      cursor: pointer;
    }

    .btn-submit:hover {
      background-color: #3451d1;
    }
  </style>
</head>
<body>

  <div class="form-wrapper">
    <h2>Join Our Newsletter</h2>
    <p>Get weekly tips on web design and development, delivered to your inbox. No spam, ever.</p>

    <label for="name">Full Name</label>
    <input type="text" id="name" placeholder="e.g. Alex Johnson">

    <label for="email">Email Address</label>
    <input type="email" id="email" placeholder="e.g. alex@example.com">

    <button class="btn-submit">Subscribe Now</button>
  </div>

</body>
</html>
```

**Expected Output:**
A clean white card centred on a blue-grey background. It contains a heading, a description, two input fields (name and email), and a full-width blue button. On mobile, the card fills the width of the screen minus the 16px side padding from the `body`.

**Key concepts demonstrated:**
- `max-width: 480px` + `margin: 0 auto` = centred card that adapts to small screens.
- `padding: 40px 16px` on `body` = prevents content from touching screen edges on small devices.
- `width: 100%` on inputs and button = they fill the card's width regardless of the card's current size.
- `box-sizing: border-box` = ensures `width: 100%` includes padding, not just content area.

**What-if challenges:**
- What happens if you change `max-width: 480px` to `max-width: 700px`? The form gets wider on large screens.
- What happens if you remove `margin: 0 auto`? The form card snaps to the left edge.
- Try adding `min-width: 280px` to `.form-wrapper`. Now the form never gets narrower than 280px.

---

### Exercise 3 — Responsive Image Gallery

**Objective:** Use `max-width: 100%` to make images responsive inside a constrained layout.

**Scenario:** You are building a photo blog post with a text column and images. The images should never overflow their container and should scale naturally.

**Solution:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Photo Blog Post</title>
  <style>
    * { box-sizing: border-box; }

    body {
      font-family: Georgia, serif;
      background-color: #fafafa;
      margin: 0;
      padding: 30px 16px;
    }

    /* Page wrapper — constrains content on wide screens */
    .post-wrapper {
      max-width: 720px;
      margin: 0 auto;
    }

    h1 {
      font-size: 32px;
      color: #222;
      margin-bottom: 8px;
    }

    .post-meta {
      color: #888;
      font-size: 14px;
      margin-bottom: 28px;
    }

    p {
      font-size: 18px;
      line-height: 1.8;
      color: #444;
      margin-bottom: 24px;
    }

    /* THE IMAGE RULE — makes all images responsive */
    img {
      max-width: 100%;
      height: auto;
      display: block;
      border-radius: 8px;
      margin: 24px 0;
    }

    .caption {
      font-size: 13px;
      color: #888;
      text-align: center;
      margin-top: -18px;
      margin-bottom: 28px;
      font-style: italic;
    }
  </style>
</head>
<body>

  <div class="post-wrapper">

    <h1>A Morning in the Mountains</h1>
    <p class="post-meta">By Sarah Okafor · April 20, 2026</p>

    <p>
      There is something particular about mountain mornings. The air has a
      quality you cannot find at sea level — thin, cold, and impossibly clear.
      Every breath feels deliberate.
    </p>

    <img src="https://via.placeholder.com/1200x600/87ceeb/333?text=Mountain+Sunrise" alt="Mountain sunrise">
    <p class="caption">Sunrise at 3,200m elevation. Photographed at 5:47am.</p>

    <p>
      I arrived at the trailhead before dawn, guided only by a headlamp and
      an old map I had printed the night before. By the time I reached the
      ridge, the sky had turned a shade of orange I have no word for in any
      language I speak.
    </p>

    <img src="https://via.placeholder.com/1200x450/f4a261/333?text=Mountain+Ridge" alt="Mountain ridge view">
    <p class="caption">The ridge at golden hour. The valley below was still in shadow.</p>

    <p>
      Walking back down, I passed three other hikers heading up. We exchanged
      the brief, knowing nods of people who had all made the same quiet
      decision to be somewhere beautiful before the rest of the world woke up.
    </p>

  </div>

</body>
</html>
```

**Expected Output:**
A beautiful, readable blog post layout centred on the page. The two placeholder images span the full 720px width of the post wrapper. On a narrow screen (e.g. 400px), the images shrink proportionally to fit, never overflowing their container.

**Self-check Questions:**
- What would happen to the images if you removed `max-width: 100%` from the `img` rule? *(Answer: On screens narrower than the image's natural size, the image would overflow the container and the page.)*
- Why is `height: auto` included alongside `max-width: 100%`? *(Answer: So the image's height adjusts proportionally when the width shrinks, maintaining the correct aspect ratio.)*

---

## Part 9: Mini Project — A Complete Blog Post Page Layout

### Project Goal

Build a professional, fully responsive blog post page that uses `max-width` as the core of its layout strategy. This is a real-world pattern used on sites like Medium, Substack, and every major news outlet.

### Stage 1 — Page Foundation

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Blog Post</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Georgia', serif;
      background-color: #f7f7f7;
      color: #333;
    }
  </style>
</head>
<body>
  <!-- Content coming next -->
</body>
</html>
```

**Milestone 1 Output:** A blank grey page — the clean foundation for our layout.

### Stage 2 — Header with Navigation

```html
<!-- Add inside <body> -->
<header class="site-header">
  <div class="wrapper">
    <div class="site-name">The Daily Read</div>
    <nav class="site-nav">
      <a href="#">Home</a>
      <a href="#">Articles</a>
      <a href="#">About</a>
    </nav>
  </div>
</header>
```

```css
/* Add to <style> */

/* THE WRAPPER — the core max-width pattern */
.wrapper {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 24px;    /* Side padding for mobile breathing room */
}

.site-header {
  background-color: white;
  border-bottom: 1px solid #e5e5e5;
  padding: 16px 0;
}

.wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.site-name {
  font-size: 22px;
  font-weight: bold;
  color: #1a1a1a;
  letter-spacing: -0.5px;
}

.site-nav a {
  text-decoration: none;
  color: #555;
  font-family: Arial, sans-serif;
  font-size: 14px;
  margin-left: 24px;
}

.site-nav a:hover {
  color: #0070f3;
}
```

**Milestone 2 Output:** A white header bar stretching the full page width. Inside it, a centred 1100px wrapper holds the site name on the left and nav links on the right.

### Stage 3 — Article Hero Section

```html
<!-- Add after <header> -->
<div class="hero">
  <div class="hero-wrapper">
    <p class="article-category">TECHNOLOGY</p>
    <h1 class="article-title">Why Every Website Should Embrace Responsive Design</h1>
    <p class="article-subtitle">
      More than half of all web traffic comes from mobile devices.
      Here is why designing for every screen size is no longer optional.
    </p>
    <div class="article-meta">
      <span>By Alex Johnson</span>
      <span>·</span>
      <span>April 20, 2026</span>
      <span>·</span>
      <span>5 min read</span>
    </div>
  </div>
</div>
```

```css
.hero {
  background-color: white;
  padding: 60px 0 40px;
  border-bottom: 1px solid #eee;
}

/* NARROWER max-width for the article — keeps lines readable */
.hero-wrapper {
  max-width: 740px;
  margin: 0 auto;
  padding: 0 24px;
}

.article-category {
  font-family: Arial, sans-serif;
  font-size: 12px;
  font-weight: bold;
  color: #0070f3;
  letter-spacing: 1.5px;
  margin-bottom: 16px;
}

.article-title {
  font-size: 38px;
  line-height: 1.2;
  color: #111;
  margin-bottom: 18px;
}

.article-subtitle {
  font-size: 19px;
  line-height: 1.6;
  color: #555;
  margin-bottom: 20px;
}

.article-meta {
  font-family: Arial, sans-serif;
  font-size: 14px;
  color: #888;
  display: flex;
  gap: 8px;
}
```

**Milestone 3 Output:** Below the header, a white hero section appears with a category label, a large article title, a subtitle, and meta information (author, date, reading time). The hero is constrained to 740px — narrower than the site header's 1100px wrapper.

### Stage 4 — Hero Image

```html
<!-- Add after the hero div -->
<div class="hero-image-wrapper">
  <img
    src="https://via.placeholder.com/1100x500/4361ee/ffffff?text=Article+Hero+Image"
    alt="Article hero image"
    class="hero-image"
  >
</div>
```

```css
.hero-image-wrapper {
  max-width: 1100px;    /* Same as the site wrapper — image goes full content width */
  margin: 0 auto;
  padding: 0 24px;
}

.hero-image {
  max-width: 100%;      /* Image never overflows its wrapper */
  height: auto;
  display: block;
  border-radius: 10px;
  margin: 32px 0;
}
```

**Milestone 4 Output:** A wide, rounded hero image appears below the header section, constrained to 1100px and shrinking naturally on smaller screens.

### Stage 5 — Article Body Content (Final)

```html
<!-- Add after hero-image-wrapper -->
<main class="article-body">
  <div class="article-wrapper">

    <p>
      The web began as a desktop experience. Early designers could safely
      assume that visitors were sitting at a computer with a monitor of
      roughly similar dimensions to their own. Those days are long gone.
    </p>

    <p>
      Today, a single website must look good and work well on a wristwatch,
      a smartphone held in one hand on a bus, a tablet propped on a kitchen
      counter, a laptop on a café table, and a 4K monitor at a standing desk.
      The range of screen sizes in active daily use spans from about 320px wide
      to over 2500px wide — a difference of nearly 8 times.
    </p>

    <h2>The Core Principle: Fluid, Not Fixed</h2>

    <p>
      Responsive design means building layouts that <em>respond</em> to their
      environment rather than imposing a fixed size on every visitor. The
      tools for this are simpler than most beginners expect: relative units,
      flexible images, and — crucially — the <code>max-width</code> property.
    </p>

    <p>
      A container with <code>max-width: 800px</code> and
      <code>margin: 0 auto</code> does something elegant: on a 1400px screen,
      it appears as a comfortable 800px centred column. On a 500px phone screen,
      it fills the available width naturally, without any additional rules needed.
      One property, all screen sizes handled.
    </p>

    <h2>Why Line Length Matters</h2>

    <p>
      Typography researchers and designers broadly agree that the optimal line
      length for comfortable reading is between 60 and 80 characters per line.
      When lines are too long, the eye struggles to find the beginning of the
      next line after finishing the current one. When lines are too short,
      reading becomes choppy and fragmented.
    </p>

    <p>
      For body text set at around 18px in a typical proportional font, 60–80
      characters corresponds to roughly 620–740 pixels. This is precisely why
      many well-designed reading experiences — like Medium, Wikipedia, and
      most professional news sites — constrain their article bodies to
      somewhere between 650px and 760px.
    </p>

  </div>
</main>
```

```css
.article-body {
  padding: 40px 0 80px;
}

/* THE READING COLUMN — optimal reading width */
.article-wrapper {
  max-width: 680px;
  margin: 0 auto;
  padding: 0 24px;
}

.article-wrapper p {
  font-size: 18px;
  line-height: 1.85;
  color: #3a3a3a;
  margin-bottom: 26px;
}

.article-wrapper h2 {
  font-size: 26px;
  color: #111;
  margin: 40px 0 18px;
}

.article-wrapper code {
  background-color: #f0f0f0;
  font-family: 'Courier New', monospace;
  font-size: 15px;
  padding: 2px 6px;
  border-radius: 4px;
  color: #c0392b;
}
```

**Final Milestone Output:**
A complete, publication-quality blog post page with three distinct `max-width` values working together:
- `.wrapper` — `max-width: 1100px` — for the header navigation (wide)
- `.hero-image-wrapper` — `max-width: 1100px` — for the full-width hero image
- `.hero-wrapper` — `max-width: 740px` — for the article title and subtitle (comfortable)
- `.article-wrapper` — `max-width: 680px` — for the body text (optimal reading)

This layered use of different `max-width` values at different levels is exactly how professional web publications like Medium and Substack are structured.

### Optional Advanced Extensions

- Add a sticky header that stays at the top when you scroll (`position: sticky; top: 0;`).
- Add a "Table of Contents" sidebar that only appears on wide screens using a media query (`@media (min-width: 1000px)`).
- Add a footer with the `.wrapper` pattern containing three columns of links.
- Add a "Related Articles" section at the bottom using three cards, each with `max-width: 340px`.

---

## Part 10: The `max-width` Code Challenges

These challenges correspond to the W3Schools CSS code challenges for `max-width`. Work through each one to solidify your understanding.

### Challenge 1 — Set a Max Width on a `<div>`

**Task:** Given a `<div>` with `id="myDIV"`, set its maximum width to 500 pixels.

```html
<style>
  #myDIV {
    /* Your code here */
    background-color: lightblue;
    padding: 20px;
  }
</style>

<div id="myDIV">
  This div has a max-width of 500px.
</div>
```

**Solution:**

```css
#myDIV {
  max-width: 500px;
  background-color: lightblue;
  padding: 20px;
}
```

---

### Challenge 2 — Centre a `<div>` with `max-width`

**Task:** Set the `<div>` to a maximum width of 600px AND centre it horizontally on the page.

```html
<style>
  #myDIV {
    /* Your code here */
    background-color: lightcoral;
    padding: 20px;
  }
</style>

<div id="myDIV">
  This div is max 600px wide and centred.
</div>
```

**Solution:**

```css
#myDIV {
  max-width: 600px;
  margin: 0 auto;
  background-color: lightcoral;
  padding: 20px;
}
```

---

### Challenge 3 — Remove a `max-width` Restriction

**Task:** A `<div>` has been given `max-width: 300px`. Override it so it has no maximum width restriction.

```html
<style>
  #myDIV {
    max-width: 300px;
    /* Add a rule to remove the max-width restriction */
    background-color: lightgreen;
    padding: 20px;
  }
</style>
```

**Solution:**

```css
#myDIV {
  max-width: none;    /* 'none' removes any max-width restriction */
  background-color: lightgreen;
  padding: 20px;
}
```

---

### Challenge 4 — Responsive Image

**Task:** Make an `<img>` element responsive so it never overflows its container, and keeps its proportions.

```html
<style>
  .container {
    width: 300px;
    border: 2px solid black;
    padding: 10px;
  }

  img {
    /* Your code here — make the image responsive */
  }
</style>

<div class="container">
  <img src="https://via.placeholder.com/800x400" alt="wide image">
</div>
```

**Solution:**

```css
img {
  max-width: 100%;
  height: auto;
}
```

---

### Challenge 5 — Combined `min-width` and `max-width`

**Task:** Style a `<div>` so it is never narrower than 200px and never wider than 500px.

```html
<style>
  #myDIV {
    /* Your code here */
    background-color: lightyellow;
    padding: 20px;
  }
</style>

<div id="myDIV">
  I stay between 200px and 500px wide.
</div>
```

**Solution:**

```css
#myDIV {
  min-width: 200px;
  max-width: 500px;
  background-color: lightyellow;
  padding: 20px;
}
```

---

## Part 11: Common Beginner Mistakes

### Mistake 1 — Confusing `max-width` with `width`

```css
/* WRONG: Fixed width — causes horizontal scrolling on small screens */
.article {
  width: 800px;
}

/* CORRECT: Flexible maximum — shrinks on small screens */
.article {
  max-width: 800px;
}
```

**Why it matters:** Using `width` instead of `max-width` is one of the most common causes of mobile layout issues. Always ask yourself: "Do I need this to be *exactly* this wide, or *at most* this wide?"

---

### Mistake 2 — Forgetting `margin: auto` When Centring

```css
/* WRONG: max-width is set, but element stays left-aligned */
.container {
  max-width: 800px;
}

/* CORRECT: max-width + margin: auto = centred */
.container {
  max-width: 800px;
  margin: 0 auto;
}
```

**Visual result of the mistake:** The container is the right width but sits in the top-left corner of the page instead of being centred.

---

### Mistake 3 — Applying `max-width: 100%` to Containers (Redundant)

```css
/* UNNECESSARY: Block elements already use 100% of their parent by default */
.wrapper {
  max-width: 100%;    /* This does nothing useful for a block element */
}

/* USEFUL: max-width: 100% is specifically powerful for images */
img {
  max-width: 100%;    /* This is genuinely important and widely used */
  height: auto;
}
```

---

### Mistake 4 — Forgetting `height: auto` with `max-width: 100%` on Images

```css
/* WRONG: Image width shrinks but height stays original — image looks squashed */
img {
  max-width: 100%;
}

/* CORRECT: Height adjusts proportionally */
img {
  max-width: 100%;
  height: auto;
}
```

**Visual result of the mistake:** When the image is constrained horizontally, it looks squashed or stretched because its height does not adjust to match.

---

### Mistake 5 — `margin: auto` on Inline Elements Does Nothing

```css
/* WRONG: <span> is inline — margin: auto has no centring effect */
span {
  max-width: 300px;
  margin: 0 auto;
}

/* CORRECT: Make it block-level first */
span {
  display: block;
  max-width: 300px;
  margin: 0 auto;
}
```

**Why:** `margin: auto` for horizontal centring only works on **block-level elements** with a defined width or `max-width`. Inline elements ignore these rules.

---

### Mistake 6 — Using `max-width` Without Side Padding on Mobile

```css
/* PROBLEMATIC: On small screens, content touches screen edges exactly */
.wrapper {
  max-width: 900px;
  margin: 0 auto;
  /* No padding — text touches left/right screen edges on mobile */
}

/* BETTER: Add side padding for breathing room */
.wrapper {
  max-width: 900px;
  margin: 0 auto;
  padding: 0 20px;   /* 20px breathing room on left and right */
}
```

**Why it matters:** Even with `max-width`, content on small screens fills the full width. Without side padding, text presses uncomfortably against the very edges of the screen.

---

## Part 12: Reflection Questions

Think carefully through each question. They will deepen your understanding of `max-width`:

1. **A `<div>` has `width: 600px` and another has `max-width: 600px`. On a 400px screen, how does each one behave? Which causes a horizontal scrollbar?**

2. **Why does `margin: 0 auto` only work for centring when combined with a `max-width` (or `width`)?** *(Hint: think about what "auto" means when there is no remaining space to distribute.)*

3. **You are building a website and want the main content column to be readable on all screen sizes — from phones to ultra-wide monitors. Would you use `width`, `max-width`, or both? Explain your reasoning.**

4. **Why is `img { max-width: 100%; height: auto; }` considered one of the most fundamental rules in responsive CSS?**

5. **What is the difference between `max-width: none` and simply not writing a `max-width` rule at all?** *(Hint: When would `max-width: none` actually be needed?)*

6. **A developer sets `max-width: 1200px` on a `.page-wrapper` and `max-width: 700px` on a `.article-body` inside it. On a 1400px screen, what width is the wrapper, and what width is the article body?**

7. **You have a `.card` element inside a grid. The grid cell is 500px wide. You set `max-width: 380px` and `margin: 0 auto` on the card. What happens?**

8. **Why do professional web publications like Medium use a narrow `max-width` (around 680–720px) for article body text, even though their site header spans the full page width?**

---

## Completion Checklist

Before moving to the next lesson, confirm you can check off every item:

- [ ] I understand what `max-width` is and what problem it solves.
- [ ] I can explain the difference between `width` and `max-width` clearly.
- [ ] I know why `max-width` is better than `width` for responsive layouts.
- [ ] I can use `max-width` with `margin: 0 auto` to centre block elements.
- [ ] I understand how `margin: auto` distributes remaining space equally.
- [ ] I know all the value types `max-width` accepts: `px`, `%`, `none`, `vw`, `fit-content`.
- [ ] I can use `max-width: 100%` and `height: auto` to make images responsive.
- [ ] I understand the difference between `max-width` and `min-width`.
- [ ] I can use both `min-width` and `max-width` together to create a flexible range.
- [ ] I know why `margin: auto` does not work on inline elements.
- [ ] I completed Exercise 1 (Fix the Broken Layout).
- [ ] I completed Exercise 2 (Centred Sign-Up Form).
- [ ] I completed Exercise 3 (Responsive Image Gallery).
- [ ] I completed the Mini Project (Blog Post Page Layout).
- [ ] I completed all 5 Code Challenges.
- [ ] I can explain all 6 common beginner mistakes and how to fix them.
- [ ] I understand why professional layouts use different `max-width` values at different levels of the page.

---

## Lesson Summary

In this lesson you learned one of the most fundamental and practical properties in all of CSS: `max-width`.

`max-width` sets a ceiling on how wide an element can grow. Unlike `width`, which locks an element to an exact fixed size (causing overflow and horizontal scrolling on small screens), `max-width` allows an element to be **flexible** — it can be narrower than its maximum on small screens, while never exceeding the limit on large screens.

The combination of `max-width` with `margin: 0 auto` is the most widely used layout pattern in web development. It creates a centred content column that adapts gracefully to every screen size: capped and centred on wide screens, naturally filling the available width on narrow ones.

For images, `max-width: 100%` paired with `height: auto` is the single most important responsive CSS rule — it ensures images never overflow their containers and always maintain their correct proportions when scaled.

You also learned `min-width` — the opposite of `max-width` — and how to combine them to create flexible-but-bounded width ranges.

In the mini project, you saw how professional layouts use **different `max-width` values at different levels**: a wide value for the overall page wrapper, a narrower value for article titles, and an even narrower value for body text — all working together to create a beautifully readable, responsive page.

Mastering `max-width` is a significant step toward building layouts that look professional on every device your visitors use.

---

*Continue to Lesson 21 to learn about CSS Position — how to precisely control where elements appear on a page using `static`, `relative`, `absolute`, `fixed`, and `sticky` positioning.*
