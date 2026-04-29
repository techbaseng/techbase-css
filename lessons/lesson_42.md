---
render_with_liquid: false
title: "CSS Math Functions: calc(), min(), max(), and clamp()"
nav_order: 42
---

# Lesson 42 — CSS Math Functions: `calc()`, `min()`, `max()`, and `clamp()`

---

## Lesson Introduction

Have you ever wished that CSS could **do maths for you** — automatically? Like saying _"make this box 100% of the screen minus the sidebar width"_ without having to calculate it yourself every time the screen changes?

That is exactly what **CSS math functions** do. They let you write **live calculations directly inside your CSS**. The browser does the maths — you just write the formula.

In this lesson, you will learn four powerful CSS math functions:

- `calc()` — performs arithmetic (add, subtract, multiply, divide) on CSS values
- `min()` — picks the **smallest** value from a list
- `max()` — picks the **largest** value from a list
- `clamp()` — keeps a value **between a minimum and maximum**, with a preferred middle value

By the end of this lesson, you will be able to use these functions to build flexible, responsive, and professional layouts without writing a single line of JavaScript.

> 🎯 **Real-world connection:** Every professional website you see today — from Netflix to Google — uses these functions behind the scenes to make layouts that automatically adapt to different screen sizes, fonts, and devices.

---

## Prerequisite Concepts

Before we dive in, let us quickly review a few ideas you need to understand first. If you already know these, feel free to skim — but if any of them feel unfamiliar, read carefully!

### What is a CSS Property Value?

In CSS, when you write a rule like:

```css
width: 300px;
```

The `300px` is called the **value** of the `width` property. CSS math functions replace that plain value with a **calculated expression** instead.

### What are CSS Units?

CSS uses different types of measurement units:

- `px` — pixels (a fixed, absolute size. Example: `20px`)
- `%` — percentage (relative to the parent element. Example: `50%` = half the parent's size)
- `vw` — viewport width (relative to the browser window. Example: `100vw` = full width of window)
- `vh` — viewport height (full height of browser window)
- `em` — relative to the font size of the current element
- `rem` — relative to the font size of the root (`<html>`) element

**Why does this matter?** CSS math functions are special because they let you **mix different units together** in one calculation. Normally you cannot write `300px + 50%` — but inside `calc()`, you can!

### What is Responsive Design?

Responsive design means making your webpage look good on **all screen sizes** — phones, tablets, laptops, desktops. CSS math functions are one of the most important tools for doing this.

---

## Conceptual Understanding

### What is a CSS Math Function?

Think of a CSS math function like a **calculator built into your CSS**. Instead of writing a fixed number, you write a formula, and the browser calculates the answer automatically — every single time the page loads or the screen resizes.

**Analogy:** Imagine you are painting a room. Instead of measuring the wall and calculating paint manually, you have a magic brush that always knows the wall size and adjusts how much paint it uses automatically. That is what CSS math functions do for sizing elements on a webpage.

### Why Do We Need Them?

Without math functions, you might write:

```css
/* Without math functions — fixed, not flexible */
.sidebar { width: 250px; }
.main-content { width: 750px; } /* You manually calculated 1000 - 250 */
```

The problem: if the total page width changes, your numbers break. You have to go back and recalculate manually.

With math functions:

```css
/* With calc() — flexible and automatic */
.sidebar { width: 250px; }
.main-content { width: calc(100% - 250px); } /* Browser always calculates this */
```

Now, no matter how wide the page is, `.main-content` is always exactly `250px` less than the full width. **The browser does the work.**

---

## Part 1 — The `calc()` Function

### What is `calc()`?

`calc()` stands for **calculate**. It lets you perform arithmetic operations on CSS values using:

- `+` (addition)
- `-` (subtraction)
- `*` (multiplication)
- `/` (division)

### Syntax

```css
property: calc(expression);
```

Where `expression` is a mathematical formula using CSS values and operators.

### Critical Rule — Spaces Around `+` and `-`

> ⚠️ **Important:** When using `+` or `-` in `calc()`, you **MUST** put a space on both sides of the operator. If you forget the spaces, the browser will not understand your formula and will ignore the whole rule!

```css
/* CORRECT — spaces around + and - */
width: calc(100% - 20px);
width: calc(50% + 10px);

/* WRONG — will NOT work! */
width: calc(100%-20px);
width: calc(50%+10px);
```

This rule does **not** apply to `*` and `/`, but it is a good habit to always include spaces for readability.

---

### Simple Example 1 — Subtracting Fixed Pixels from a Percentage

**Scenario:** You want a box to be as wide as its container, but with 40px of padding (20px on each side).

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .container {
    width: 600px;
    background-color: lightgray;
    padding: 0;
  }

  .box {
    width: calc(100% - 40px);  /* Full width minus 40px */
    margin: 20px;
    background-color: coral;
    height: 60px;
  }
</style>
</head>
<body>
  <div class="container">
    <div class="box"></div>
  </div>
</body>
</html>
```

**What happens step by step:**
1. `.container` is 600px wide.
2. `.box` gets `width: calc(100% - 40px)`.
3. `100%` of 600px = 600px.
4. `600px - 40px = 560px`.
5. The browser sets `.box` to exactly **560px wide**.

**Expected Output:** A coral-coloured box that is 560px wide, sitting with 20px of space on either side inside the container.

> 🤔 **Thinking prompt:** What would happen if `.container` were only 400px wide? What would the box width become?
> **Answer:** `calc(100% - 40px)` = `400px - 40px` = **360px**. The browser recalculates automatically!

---

### Simple Example 2 — Adding Different Units

**Scenario:** You want an element's height to be `100vh` (full screen height) minus `80px` (to account for a top navigation bar that is 80px tall).

```css
.page-content {
  height: calc(100vh - 80px);
  background-color: #f0f0f0;
  overflow-y: scroll;
}
```

**Line-by-line explanation:**
- `100vh` = 100% of the browser window's height (this changes with every screen size).
- `80px` = the fixed height of the navigation bar.
- `calc(100vh - 80px)` = the browser window height minus 80px = exactly the remaining space below the navbar.

**Expected Output:** `.page-content` fills the entire screen below the navbar, no matter what screen size.

> 💡 **Why this is powerful:** You could **never** do `100vh - 80px` without `calc()`. These are different types of units — one is relative, one is fixed. `calc()` is the only way to mix them.

---

### Simple Example 3 — Multiplication

**Scenario:** You want a font size to be exactly 5 times a base unit.

```css
h1 {
  font-size: calc(1rem * 5);  /* = 5rem */
}
```

**Expected Output:** The heading will be 5rem in size (5 × the root font size, usually 5 × 16px = 80px).

---

### Simple Example 4 — Division

**Scenario:** You want to divide the full width into 3 equal columns.

```css
.column {
  width: calc(100% / 3);  /* One-third of the parent width */
  float: left;
}
```

**Expected Output:** Each `.column` takes up exactly one-third of the available width.

---

### Real-World `calc()` Usage

Here is a realistic layout where a sidebar and main content area are calculated precisely:

```html
<!DOCTYPE html>
<html>
<head>
<style>
  body {
    margin: 0;
    padding: 0;
  }

  .sidebar {
    width: 200px;
    height: 100vh;
    background-color: #2c3e50;
    color: white;
    float: left;
    padding: 20px;
    box-sizing: border-box;
  }

  .main-content {
    width: calc(100% - 200px);  /* Full page minus sidebar */
    min-height: 100vh;
    background-color: #ecf0f1;
    float: left;
    padding: 30px;
    box-sizing: border-box;
  }
</style>
</head>
<body>
  <div class="sidebar">
    <h3>Sidebar</h3>
    <p>Navigation here</p>
  </div>
  <div class="main-content">
    <h1>Main Content</h1>
    <p>Page content goes here.</p>
  </div>
</body>
</html>
```

**Expected Output:** A two-column layout where the sidebar is always 200px and the main area fills the rest of the screen — regardless of screen width.

---

## Part 2 — The `min()` Function

### What is `min()`?

`min()` takes **two or more values** and returns the **smallest one**.

Think of it like asking: *"Of all these choices, which is the smallest? Use that one."*

**Analogy:** Imagine you can only pick the smallest pizza from a menu. If the menu says "300px or 50%", the browser looks at both and picks whichever is actually smaller on the current screen.

### Syntax

```css
property: min(value1, value2, value3, ...);
```

---

### Simple Example 1 — Limiting Width

**Scenario:** You want an element to be 50% of its parent, but never more than 300px wide.

```css
.box {
  width: min(50%, 300px);
  background-color: steelblue;
  height: 100px;
}
```

**How it works:**
- If the parent is 800px wide: `50% = 400px`. Since `400px > 300px`, the browser picks `300px`.
- If the parent is 400px wide: `50% = 200px`. Since `200px < 300px`, the browser picks `200px`.

| Parent Width | 50% Value | min() picks |
|---|---|---|
| 800px | 400px | 300px (smaller) |
| 400px | 200px | 200px (smaller) |
| 200px | 100px | 100px (smaller) |

**Expected Output:** The box is always as narrow as possible between `50%` and `300px`.

> 🤔 **Thinking prompt:** What if the parent is 600px wide? `50% = 300px`. Both values are equal! The browser picks **300px** — it does not matter which one in a tie.

---

### Simple Example 2 — Responsive Font Size

```css
h2 {
  font-size: min(5vw, 40px);
}
```

**Explanation:**
- `5vw` = 5% of the viewport width. On a 1000px wide screen: `5vw = 50px`. On a 600px screen: `5vw = 30px`.
- `40px` = a fixed maximum.
- `min(5vw, 40px)` means: use `5vw`, but never let it be bigger than `40px`.

**Expected Output:**
- On a large screen: font stays capped at `40px`.
- On a small screen: font shrinks proportionally.

---

### Real-World `min()` Usage — Responsive Card

```css
.card {
  width: min(90%, 500px);  /* Be 90% wide, but never more than 500px */
  margin: 0 auto;
  background: white;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}
```

**Expected Output:** On a large screen the card is 500px wide (centered). On a small phone screen, the card takes up 90% of the width — no awkward overflow or scrollbars!

---

## Part 3 — The `max()` Function

### What is `max()`?

`max()` is the opposite of `min()`. It takes **two or more values** and returns the **largest one**.

Think of it like: *"Of all these choices, which is the biggest? Use that one."*

**Analogy:** You set a minimum wage — no one can be paid less than a certain amount. `max()` works the same way: it ensures a value never falls below a certain floor.

### Syntax

```css
property: max(value1, value2, value3, ...);
```

---

### Simple Example 1 — Minimum Width Guarantee

**Scenario:** You want a button's width to be 10% of the parent, but never narrower than 100px (so the text never overflows).

```css
.button {
  width: max(10%, 100px);
  background-color: royalblue;
  color: white;
  padding: 10px;
  text-align: center;
}
```

**How it works:**
- If the parent is 1500px: `10% = 150px`. Since `150px > 100px`, browser picks `150px`.
- If the parent is 600px: `10% = 60px`. Since `60px < 100px`, browser picks `100px`.

| Parent Width | 10% Value | max() picks |
|---|---|---|
| 1500px | 150px | 150px (larger) |
| 600px | 60px | 100px (larger) |
| 400px | 40px | 100px (larger) |

**Expected Output:** The button is always at least 100px wide — never too small to read.

---

### Simple Example 2 — Minimum Font Size

**Scenario:** You want a font to scale with the viewport but never be smaller than 16px (for readability).

```css
p {
  font-size: max(2vw, 16px);
}
```

**Explanation:**
- `2vw` on a 1200px screen = `24px`. Browser picks `24px` (larger).
- `2vw` on a 400px screen = `8px`. Browser picks `16px` (larger, protects readability).

**Expected Output:** Text always stays readable — never drops below 16px.

---

### min() vs max() — Side by Side Comparison

| Function | Behaviour | Use Case |
|---|---|---|
| `min(a, b)` | Picks the **smaller** value | Set a **maximum** limit (cap) |
| `max(a, b)` | Picks the **larger** value | Set a **minimum** limit (floor) |

> 💡 **Memory trick:** `min()` gives you a ceiling (maximum cap). `max()` gives you a floor (minimum guarantee). It sounds backwards at first — but think of it this way: `min()` makes sure the value is never **too big**, `max()` makes sure it is never **too small**.

---

## Part 4 — The `clamp()` Function

### What is `clamp()`?

`clamp()` is the most powerful of the four functions. It **combines the ideas of `min()` and `max()`** in a single function. It keeps a value **clamped** (trapped) between a minimum and maximum, while allowing it to scale fluidly in between.

`clamp()` takes **exactly three values** in this order:

```css
property: clamp(minimum, preferred, maximum);
```

- **minimum** — the smallest the value can ever be
- **preferred** — the ideal value (usually a flexible unit like `vw` or `%`)
- **maximum** — the largest the value can ever be

**Analogy:** Think of a thermostat. You set a minimum temperature (e.g. 18°C), a maximum temperature (e.g. 26°C), and a preferred temperature that adjusts automatically (e.g. based on time of day). The thermostat will never go below 18°C or above 26°C — but in between, it adjusts smoothly. `clamp()` works the same way.

---

### Simple Example 1 — Clamped Font Size

```css
h1 {
  font-size: clamp(20px, 5vw, 60px);
}
```

**Line-by-line explanation:**
- `20px` — minimum: the font will NEVER be smaller than 20px
- `5vw` — preferred: ideally the font scales with the viewport
- `60px` — maximum: the font will NEVER be bigger than 60px

**How it works across different screen sizes:**

| Screen Width | 5vw Value | clamp result |
|---|---|---|
| 2000px | 100px | **60px** (capped at max) |
| 1000px | 50px | **50px** (within range, uses preferred) |
| 600px | 30px | **30px** (within range, uses preferred) |
| 300px | 15px | **20px** (floored at min) |

**Expected Output:** On huge screens, the heading does not become ridiculously large. On tiny screens, it does not become unreadably small. In between — it scales perfectly.

---

### Simple Example 2 — Clamped Width

```css
.container {
  width: clamp(300px, 50%, 800px);
}
```

**Explanation:**
- Never narrower than `300px`
- Never wider than `800px`
- Prefers to be `50%` of the parent

**Expected Output:** The container is perfectly responsive — small screens get a usable minimum, large screens get a maximum cap, and mid-range screens get a proportional size.

---

### Simple Example 3 — Clamped Padding

**Scenario:** You want padding that scales with the screen, but stays within reasonable bounds.

```css
section {
  padding: clamp(10px, 3vw, 50px);
}
```

**Expected Output:**
- On small screens: minimum `10px` padding (not cramped)
- On large screens: maximum `50px` padding (not excessive)
- In between: `3vw` padding scales smoothly

---

### `clamp()` vs `min()` and `max()`

Here is a key insight: `clamp(min, preferred, max)` is actually equivalent to writing:

```css
/* These two are identical: */
font-size: clamp(20px, 5vw, 60px);
font-size: max(20px, min(5vw, 60px));
```

`clamp()` just makes it much easier to read and write.

---

### All Four Functions — Quick Reference Table

| Function | Syntax | What It Does |
|---|---|---|
| `calc()` | `calc(expression)` | Performs arithmetic on CSS values; can mix units |
| `min()` | `min(a, b, ...)` | Returns the smallest value (sets a ceiling/cap) |
| `max()` | `max(a, b, ...)` | Returns the largest value (sets a floor/minimum) |
| `clamp()` | `clamp(min, preferred, max)` | Keeps value between min and max, using preferred when possible |

---

## Guided Practice Exercises

### Exercise 1 — `calc()` Basics

**Objective:** Use `calc()` to create a centred box with side margins.

**Scenario:** You are building a blog layout. The main content area should always have exactly 40px of horizontal space on each side (total 80px), taking up the remaining width.

**Steps:**
1. Create a `<div>` with the class `blog-post`.
2. Give the container `div` a width of 100%.
3. Use `calc()` to set `.blog-post`'s width.

**Starter Code:**
```html
<!DOCTYPE html>
<html>
<head>
<style>
  .page-wrapper {
    width: 100%;
    background-color: #f5f5f5;
    padding: 20px 0;
  }

  .blog-post {
    /* YOUR CODE HERE: width should be 100% minus 80px */
    margin: 0 auto; /* centres the box */
    background-color: white;
    padding: 30px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  }
</style>
</head>
<body>
  <div class="page-wrapper">
    <div class="blog-post">
      <h2>My Blog Post</h2>
      <p>Some content here...</p>
    </div>
  </div>
</body>
</html>
```

**Hint:** Replace `/* YOUR CODE HERE */` with `width: calc(100% - 80px);`

**Expected Output:** The blog post box has 40px of space on either side.

**Solution:**
```css
.blog-post {
  width: calc(100% - 80px);
  margin: 0 auto;
  background-color: white;
  padding: 30px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}
```

**Self-check questions:**
1. What happens to the box width if you change the page to 500px wide?
2. What would the box width be on a 1200px wide page?
3. What would break if you removed the space around `-` in `calc()`?

---

### Exercise 2 — `min()` for Responsive Images

**Objective:** Use `min()` to make an image responsive but capped at a maximum width.

**Scenario:** You have a product image. It should be 100% wide on small screens (fill the screen) but no more than 400px wide on large screens.

**Starter Code:**
```html
<!DOCTYPE html>
<html>
<head>
<style>
  .product-image {
    /* YOUR CODE HERE: use min() */
    height: auto;
    display: block;
    margin: 20px auto;
    border-radius: 8px;
    background-color: #ddd;
  }
</style>
</head>
<body>
  <div class="product-image" style="height:200px;">Product Image</div>
</body>
</html>
```

**Expected Output:** On a phone, the image fills the screen. On a desktop, it never exceeds 400px.

**Solution:**
```css
.product-image {
  width: min(100%, 400px);
  height: auto;
  display: block;
  margin: 20px auto;
}
```

**What-if challenge:** What would happen if you changed `400px` to `600px`? Would it make the image larger or smaller on a 500px screen?

---

### Exercise 3 — `clamp()` for Responsive Typography

**Objective:** Create a heading that scales fluidly between mobile and desktop.

**Scenario:** You are building a landing page hero section. The main heading should be at least 24px (mobile), scale with the viewport at 4vw, and reach a maximum of 72px (desktop).

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .hero {
    background-color: #1a1a2e;
    color: white;
    padding: 80px 40px;
    text-align: center;
  }

  .hero h1 {
    /* YOUR CODE HERE: use clamp() */
    margin: 0;
    line-height: 1.2;
  }

  .hero p {
    font-size: clamp(14px, 2vw, 20px);  /* Already done as an example! */
    max-width: 600px;
    margin: 20px auto 0;
  }
</style>
</head>
<body>
  <div class="hero">
    <h1>Welcome to My Website</h1>
    <p>A modern, responsive site built with CSS math functions.</p>
  </div>
</body>
</html>
```

**Solution:**
```css
.hero h1 {
  font-size: clamp(24px, 4vw, 72px);
  margin: 0;
  line-height: 1.2;
}
```

**Self-check questions:**
1. At what viewport width would the heading be exactly 40px? (Hint: `4vw = 40px` when `vw = 10px`, meaning the viewport is 1000px wide)
2. Why is it important to have both a minimum AND maximum for font sizes?
3. What would `clamp(16px, 4vw, 16px)` do? (Hint: min and max are the same!)

---

## Mini Project — Responsive Profile Card

Now let us combine everything you have learned into a single, polished, real-world component: a responsive profile card that looks great on any screen size.

### Project Goal

Build a profile card that:
- Has a fluid, responsive width using `min()` and `clamp()`
- Uses `calc()` for internal spacing
- Has a fluid font size using `clamp()`
- Works beautifully on both mobile (320px) and desktop (1440px)

---

### Stage 1: Setup — HTML Structure

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
      <div class="avatar"></div>
      <h2 class="profile-name">Adaeze Okonkwo</h2>
      <p class="profile-role">Frontend Developer</p>
      <p class="profile-bio">
        Passionate about building beautiful, accessible, and responsive web experiences.
      </p>
      <div class="stats-row">
        <div class="stat">
          <span class="stat-number">128</span>
          <span class="stat-label">Projects</span>
        </div>
        <div class="stat">
          <span class="stat-number">4.2k</span>
          <span class="stat-label">Followers</span>
        </div>
        <div class="stat">
          <span class="stat-number">312</span>
          <span class="stat-label">Stars</span>
        </div>
      </div>
      <button class="follow-btn">Follow</button>
    </div>
  </div>
</body>
</html>
```

**Milestone Output:** Open this in a browser — you should see plain unstyled text. That is expected at Stage 1.

---

### Stage 2: Core Layout with Math Functions

Now create a file called `style.css` (or add a `<style>` block in your HTML `<head>`):

```css
/* ===== RESET & BASE ===== */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Segoe UI', Arial, sans-serif;
  background-color: #f0f4f8;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

/* ===== PAGE WRAPPER ===== */
.page-wrapper {
  width: 100%;
  display: flex;
  justify-content: center;
}

/* ===== THE CARD ===== */
.profile-card {
  /* min() ensures it never exceeds 420px on large screens */
  width: min(100%, 420px);

  /* calc() creates internal padding that adjusts with content */
  padding: calc(30px + 1vw);

  background-color: white;
  border-radius: 16px;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
  text-align: center;
}
```

**Milestone Output:** The card should now have a white background, rounded corners, shadow, and be centred on the page. On a phone, it fills the screen. On a desktop, it is capped at 420px.

---

### Stage 3: Fluid Typography and Avatar

Add these CSS rules:

```css
/* ===== AVATAR ===== */
.avatar {
  /* clamp() keeps the avatar between 80px and 130px */
  width: clamp(80px, 20vw, 130px);
  height: clamp(80px, 20vw, 130px);

  background: linear-gradient(135deg, #667eea, #764ba2);
  border-radius: 50%;
  margin: 0 auto 20px auto;
}

/* ===== NAME ===== */
.profile-name {
  /* clamp() scales the name fluidly */
  font-size: clamp(20px, 3.5vw, 28px);
  color: #1a202c;
  margin-bottom: 6px;
}

/* ===== ROLE ===== */
.profile-role {
  font-size: clamp(12px, 2vw, 15px);
  color: #667eea;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 14px;
}

/* ===== BIO ===== */
.profile-bio {
  font-size: clamp(13px, 1.8vw, 15px);
  color: #718096;
  line-height: 1.6;
  /* calc() creates padding relative to card size */
  padding: 0 calc(10px + 1%);
  margin-bottom: 24px;
}
```

**Milestone Output:** The card now has a purple gradient avatar circle, a styled name, role label in purple, and readable bio text.

---

### Stage 4: Stats Row and Button

```css
/* ===== STATS ROW ===== */
.stats-row {
  display: flex;
  justify-content: space-around;
  /* calc() creates a top/bottom border area with balanced spacing */
  padding: 20px calc(100% / 12);
  border-top: 1px solid #e2e8f0;
  border-bottom: 1px solid #e2e8f0;
  margin-bottom: 24px;
}

.stat {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
}

.stat-number {
  font-size: clamp(16px, 2.5vw, 22px);
  font-weight: 700;
  color: #1a202c;
}

.stat-label {
  font-size: clamp(10px, 1.5vw, 12px);
  color: #a0aec0;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* ===== BUTTON ===== */
.follow-btn {
  /* min() controls button width: fills space but maxes at 200px */
  width: min(100%, 200px);
  padding: 12px 0;
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
  border: none;
  border-radius: 30px;
  /* clamp() on font-size keeps button text readable */
  font-size: clamp(13px, 2vw, 16px);
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
}

.follow-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.5);
}
```

**Final Expected Output:** A polished, professional profile card with:
- A purple gradient avatar
- Fluid, scalable name and bio text
- A three-column stats row
- A styled gradient button
- Smooth hover effects
- Perfect sizing on any screen from 320px to 1440px

---

### Reflection Questions for the Mini Project

1. The card uses `min(100%, 420px)`. What would happen if you changed `420px` to `300px`? Would the card look more cramped on desktop?
2. The avatar uses `clamp(80px, 20vw, 130px)`. On a 300px screen, `20vw = 60px`. Since `60px < 80px`, what size would the avatar actually be?
3. The stats row uses `padding: 20px calc(100% / 12)`. What is the horizontal padding on a 420px wide card? (`420 / 12 = 35px`)
4. Could you replace all the `clamp()` calls with just `min()` and `max()` combined? Why might `clamp()` be easier?
5. Why is `width: min(100%, 420px)` a better choice for the card than just `width: 420px`?

---

## Common Beginner Mistakes

### Mistake 1 — Missing Spaces Around `+` and `-` in `calc()`

```css
/* ❌ WRONG — will not work, browser ignores this */
width: calc(100%-20px);
padding: calc(50%+10px);

/* ✅ CORRECT — spaces required around + and - */
width: calc(100% - 20px);
padding: calc(50% + 10px);
```

**Why it breaks:** The browser reads `100%-20px` as an unknown value, not a math expression. The spaces signal to the browser that `+` and `-` are arithmetic operators, not part of a unit name.

---

### Mistake 2 — Forgetting Units

```css
/* ❌ WRONG — 20 has no unit */
width: calc(100% - 20);

/* ✅ CORRECT — every number must have a unit */
width: calc(100% - 20px);
```

**Why it breaks:** CSS requires units on all length values. `20` alone means nothing — `20px`, `20%`, `20vw`, etc. are all valid.

**Exception:** Pure multipliers and divisors do NOT need units:
```css
/* ✅ These are fine — 3 and 4 are pure numbers (no unit needed) */
width: calc(100% / 4);
font-size: calc(1rem * 3);
```

---

### Mistake 3 — Dividing by Zero

```css
/* ❌ WRONG — dividing by zero is undefined */
width: calc(100px / 0);

/* ✅ Make sure the divisor is never zero */
width: calc(100px / 4);
```

---

### Mistake 4 — Wrong Argument Count in `clamp()`

```css
/* ❌ WRONG — clamp() requires exactly 3 values */
font-size: clamp(16px, 20px);  /* Only 2 values */
font-size: clamp(16px, 2vw, 40px, 60px);  /* 4 values */

/* ✅ CORRECT — exactly 3: min, preferred, max */
font-size: clamp(16px, 2vw, 40px);
```

---

### Mistake 5 — min/max Values in Wrong Order in `clamp()`

```css
/* ❌ WRONG — minimum is bigger than maximum! */
font-size: clamp(60px, 4vw, 20px);  /* min=60px > max=20px — nonsensical */

/* ✅ CORRECT — minimum must always be ≤ maximum */
font-size: clamp(20px, 4vw, 60px);
```

**Why it breaks:** If the minimum is bigger than the maximum, the values conflict and the result is undefined/unreliable.

---

### Mistake 6 — Using `min()`/`max()` When You Need `clamp()`

```css
/* ❌ Partially correct but incomplete */
font-size: max(16px, 4vw);  /* No maximum cap — scales infinitely */

/* ✅ Better — use clamp() to set both floor and ceiling */
font-size: clamp(16px, 4vw, 48px);
```

---

### Mistake 7 — Nesting `calc()` unnecessarily

```css
/* ❌ Redundant — not wrong, just unnecessary */
width: calc(calc(100% - 20px) - 10px);

/* ✅ Simpler — one calc() is enough */
width: calc(100% - 30px);
```

---

## Reflection Questions

Work through these questions to test your understanding:

1. **`calc()`:** You have a grid with 3 columns and a 20px gap between each column (so 2 gaps total). Using `calc()`, write the CSS for each column's width so all three columns fit perfectly in a 100%-wide container.
   > Hint: `calc((100% - 40px) / 3)` — Why `40px`? Because there are 2 gaps × 20px each.

2. **`min()`:** A developer writes `width: min(80%, 600px)`. On a screen where 80% = 700px, what width does the element get? On a screen where 80% = 400px?

3. **`max()`:** A developer writes `font-size: max(14px, 1.5vw)`. On a 1200px screen, `1.5vw = 18px`. Which value gets used? On a 600px screen, `1.5vw = 9px`. Which value gets used?

4. **`clamp()`:** Explain in your own words what `padding: clamp(10px, 3%, 40px)` does on a 200px wide element versus a 2000px wide element.

5. **Combined:** Which function would you choose for each scenario?
   - A sidebar that should never be narrower than 150px: `_____`
   - A container that should never be wider than 1200px: `_____`
   - A heading that scales smoothly but stays between 18px and 64px: `_____`
   - Centring a box with exactly 30px margins on each side: `_____`

---

## Completion Checklist

Before moving to the next lesson, make sure you can check off each item:

- [ ] I understand what a CSS math function is and why it is useful
- [ ] I can write `calc()` with `+`, `-`, `*`, and `/` and know to include spaces around `+` and `-`
- [ ] I understand that `calc()` can mix different CSS units (like `%` and `px`)
- [ ] I can use `min()` to cap an element at a maximum size
- [ ] I can use `max()` to guarantee an element a minimum size
- [ ] I understand the difference between `min()` and `max()`
- [ ] I can write `clamp(min, preferred, max)` with exactly three arguments
- [ ] I understand that `clamp()` keeps a value between a floor and a ceiling
- [ ] I have completed at least two of the three exercises
- [ ] I have attempted the mini project profile card
- [ ] I can identify and fix the common mistakes listed above

---

## Lesson Summary

In this lesson, you learned four powerful CSS math functions that allow you to write live, browser-calculated values in your stylesheets:

**`calc(expression)`** performs arithmetic (+, -, *, /) on CSS values and is the only way to mix different unit types (like `%` and `px`) in a single value. Always put spaces around `+` and `-`.

**`min(a, b)`** returns the smallest of the given values. Use it to set a **maximum cap** — the element will be as small as possible between the given choices. Ideal for responsive widths and font sizes that should not exceed a certain size.

**`max(a, b)`** returns the largest of the given values. Use it to guarantee a **minimum floor** — the element will be as large as necessary to meet the minimum. Ideal for ensuring readability and usability on small screens.

**`clamp(min, preferred, max)`** is the most powerful function, keeping a value between a defined minimum and maximum while scaling fluidly using a preferred value (usually a viewport-relative unit like `vw` or `%`). It is the go-to tool for truly fluid, responsive typography and sizing.

Together, these four functions replace the need for many JavaScript-based layout adjustments and media query breakpoints. They are standard, supported in all modern browsers, and are a mark of professional, production-quality CSS.

---

> 🚀 **Next Steps:** Now that you understand CSS math functions, you are ready to explore CSS Custom Properties (variables) — which combine beautifully with these functions to create highly maintainable, themeable design systems.
