---
render_with_liquid: false
title: "CSS Alignment – Center, Horizontal, and Vertical Alignment"
nav_order: 27
---

# Lesson 27: CSS Alignment — Center, Horizontal, and Vertical Alignment

---

## Lesson Introduction

One of the most common questions in web development — even among experienced developers — is: **"How do I centre this thing?"**

Aligning content perfectly is one of the most important skills in CSS. Whether you are building a personal portfolio, a business landing page, a navigation bar, or a login form, you will constantly need to position elements exactly where you want them — centred on the page, pushed to the right, sitting perfectly in the middle of a box, or lined up neatly side by side.

CSS gives you many tools to control alignment. Some tools are for **horizontal alignment** (left, right, or centre across the page). Others are for **vertical alignment** (top, middle, or bottom within a container). And some powerful tools — like Flexbox — can handle both at once.

In this lesson you will learn all the major techniques for aligning elements in CSS, understand exactly when to use each one, and practice through exercises and a complete mini-project.

By the end of this lesson you will confidently be able to:
- Centre a block element horizontally using `margin: auto`
- Align text left, right, or centre using `text-align`
- Position elements using `float` and `clear`
- Centre elements perfectly using Flexbox
- Vertically centre content using multiple techniques
- Know which technique to choose for any alignment situation

---

## Prerequisite Concepts

Before we begin, let us make sure you understand a few building-block ideas.

### Block vs Inline Elements

HTML elements fall into two main categories:

**Block elements** take up the full width available and always start on a new line. Examples: `<div>`, `<p>`, `<h1>`, `<section>`. You can set a `width` on them.

**Inline elements** only take up as much space as their content needs and do not start a new line. Examples: `<span>`, `<a>`, `<strong>`, `<img>`. Setting `width` and `height` on them has no effect (unless you change their `display` value).

This distinction matters greatly for alignment — many techniques only work on block elements.

### What is a Container?

A **container** is simply the parent element that wraps around the element you want to align. When you centre a `<div>` inside a `<section>`, the `<section>` is the container.

Most alignment techniques work by applying CSS to the **container** (to align all its children), or to the **element itself** (to position it within its container).

### The Box Model Reminder

Every HTML element is a rectangular box with content, padding, border, and margin. Understanding this helps when using `margin: auto` for centring — it is the margin (the outside space) that does the magic.

---

## Part 1: Centring a Block Element Horizontally — `margin: auto`

### What is `margin: auto`?

The most classic way to centre a block element horizontally inside its parent is to set its left and right margins to `auto`.

When you set `margin: auto` on the left and right sides, the browser divides the available horizontal space equally between the two sides — effectively pushing the element to the exact centre.

**Syntax:**

```css
.element {
  width: 300px;       /* REQUIRED — must have a width set */
  margin: 0 auto;     /* 0 = top/bottom margin, auto = left/right margin */
}
```

> **Important Rule:** `margin: auto` for horizontal centring **only works if the element has a defined `width`**. Without a width, a block element stretches to fill 100% of its parent, so there is no leftover space to divide — and `auto` has nothing to work with.

### Simple Example

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .container {
    background-color: lightgrey;
    padding: 20px;
  }

  .box {
    width: 300px;           /* width is required */
    background-color: steelblue;
    color: white;
    padding: 20px;
    margin: 0 auto;         /* centres the box horizontally */
    text-align: center;
  }
</style>
</head>
<body>

  <div class="container">
    <div class="box">I am centred!</div>
  </div>

</body>
</html>
```

**Expected Output:**
- A grey container stretching full width.
- A blue box that is 300px wide, sitting perfectly in the horizontal centre of the grey container.

> **Thinking Prompt:** What happens if you remove `width: 300px` from `.box`? (The box stretches full width and `margin: auto` has no effect — there is nothing to centre.)

### Centring with `max-width`

Using `max-width` instead of a fixed `width` is better for responsive design because the element can shrink on smaller screens but will not grow beyond the `max-width` on larger screens.

```css
.content-wrapper {
  max-width: 960px;   /* never wider than 960px */
  margin: 0 auto;     /* centred on large screens, full-width on small ones */
  padding: 0 20px;    /* a little breathing room on the sides */
}
```

**Expected Output:**
- On a large monitor: the content wrapper is 960px wide and centred.
- On a phone: the content wrapper fills the screen (since the phone is narrower than 960px).

This pattern is used on almost every professional website for the main content area.

---

## Part 2: Aligning Text — `text-align`

### What is `text-align`?

`text-align` controls how **inline content** (text, inline elements, inline-block elements) is positioned horizontally within a block container.

```css
p {
  text-align: left;    /* default — text lines up on the left */
  text-align: right;   /* text lines up on the right */
  text-align: center;  /* text is centred */
  text-align: justify; /* text is spread to fill the full width (like a newspaper) */
}
```

> **Important:** `text-align` is applied to the **container**, and it affects all the inline content inside that container. It does NOT centre a block element — it only aligns text and inline items.

### Example — All Four Values

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .box {
    width: 400px;
    background-color: #f0f0f0;
    padding: 15px;
    margin: 10px auto;
    border: 1px solid #ccc;
  }

  .left    { text-align: left;    }
  .right   { text-align: right;   }
  .centre  { text-align: center;  }
  .justify { text-align: justify; }
</style>
</head>
<body>

  <div class="box left">
    Left aligned text. This is the default. Text starts at the left edge.
  </div>

  <div class="box right">
    Right aligned text. Text starts at the right edge.
  </div>

  <div class="box centre">
    Centre aligned text. Text is centred between the two edges.
  </div>

  <div class="box justify">
    Justified text. Each line is stretched so it touches both the left and right edges. Like a newspaper column. This works best with longer paragraphs.
  </div>

</body>
</html>
```

**Expected Output:** Four boxes, each demonstrating a different text alignment.

### `text-align` also works on inline-block elements

```html
<style>
  .nav {
    text-align: center;   /* centres the inline-block items inside */
    background-color: #333;
    padding: 10px;
  }

  .nav a {
    display: inline-block;
    color: white;
    padding: 8px 16px;
    text-decoration: none;
  }
</style>

<nav class="nav">
  <a href="#">Home</a>
  <a href="#">About</a>
  <a href="#">Contact</a>
</nav>
```

**Expected Output:** A dark navigation bar with three links horizontally centred inside it.

---

## Part 3: Horizontal Alignment with `float`

### What is `float`?

The `float` property was originally designed to allow text to wrap around images (like in a magazine or newspaper). It moves an element to the left or right side of its container, and the content that follows flows around it.

```css
img {
  float: left;    /* image moves to the left, text wraps on the right */
  float: right;   /* image moves to the right, text wraps on the left */
  float: none;    /* default — no floating */
}
```

### Simple Float Example

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .container {
    background-color: #f5f5f5;
    padding: 15px;
    overflow: auto;   /* fixes the collapsing parent problem — explained later */
  }

  .left-box {
    float: left;
    width: 200px;
    background-color: steelblue;
    color: white;
    padding: 15px;
    margin-right: 15px;
  }

  p {
    font-size: 16px;
    line-height: 1.6;
  }
</style>
</head>
<body>

  <div class="container">
    <div class="left-box">I am floated left</div>
    <p>This text wraps around the floated box. In a magazine, you often see images on the left with text flowing to the right of them. This is exactly what float was designed for — allowing content to wrap around another element.</p>
  </div>

</body>
</html>
```

**Expected Output:**
- A blue box on the left.
- The paragraph text flows alongside it on the right.

### Using `float` to push an element to the right

```html
<style>
  .header {
    background-color: #333;
    color: white;
    padding: 15px 20px;
    overflow: auto;
  }

  .logo {
    float: left;
    font-size: 22px;
    font-weight: bold;
  }

  .login-btn {
    float: right;
    background-color: steelblue;
    color: white;
    padding: 8px 16px;
    border-radius: 4px;
    text-decoration: none;
  }
</style>

<header class="header">
  <span class="logo">MyWebsite</span>
  <a class="login-btn" href="#">Login</a>
</header>
```

**Expected Output:**
- A dark header bar.
- "MyWebsite" logo floated to the left.
- "Login" button floated to the right.
- This is a very common header layout pattern.

### The `clear` Property — Stopping Float Effects

Once an element is floated, everything after it tries to wrap around it. To stop this and force an element to appear below all floated elements, use `clear`.

```css
.footer {
  clear: both;   /* do not allow anything floated on either side */
}
```

| Value | What it does |
|---|---|
| `clear: left` | The element moves below any left-floated elements |
| `clear: right` | The element moves below any right-floated elements |
| `clear: both` | The element moves below ALL floated elements on both sides |
| `clear: none` | Default. No clearing happens |

```html
<style>
  .float-left  { float: left;  width: 45%; background-color: coral;     padding: 15px; }
  .float-right { float: right; width: 45%; background-color: steelblue; padding: 15px; color: white; }
  .footer      { clear: both;  background-color: #333; color: white; padding: 15px; }
</style>

<div class="float-left">Left column</div>
<div class="float-right">Right column</div>
<footer class="footer">Footer — appears below both columns because of clear: both</footer>
```

**Expected Output:**
- Two columns side by side (coral on the left, blue on the right).
- A dark footer appearing below both columns (thanks to `clear: both`).

> **When to use float today:** Float is largely replaced by Flexbox and Grid for layout purposes. But it is still useful for making text wrap around images, and you will encounter it frequently in older codebases.

---

## Part 4: The Modern Way — Horizontal Alignment with Flexbox

### What is Flexbox?

Flexbox (Flexible Box Layout) is a modern CSS layout system designed specifically for aligning and distributing elements inside a container. It makes alignment — both horizontal and vertical — extremely simple and powerful.

To activate Flexbox on a container:

```css
.container {
  display: flex;
}
```

This one line turns `.container` into a **flex container**, and all its direct children become **flex items** that can be aligned and distributed easily.

### Horizontal Alignment with `justify-content`

The `justify-content` property controls how flex items are distributed along the **main axis** (by default, horizontally left to right).

```css
.container {
  display: flex;
  justify-content: flex-start;    /* items packed to the left (default) */
  justify-content: flex-end;      /* items packed to the right */
  justify-content: center;        /* items packed to the centre */
  justify-content: space-between; /* first item at left, last at right, equal space between */
  justify-content: space-around;  /* equal space around each item */
  justify-content: space-evenly;  /* equal space between items AND at the edges */
}
```

### Example — All `justify-content` Values

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .flex-container {
    display: flex;
    background-color: #f0f0f0;
    padding: 10px;
    margin: 8px 0;
  }

  .flex-container span {
    background-color: steelblue;
    color: white;
    padding: 10px 20px;
    border-radius: 4px;
    font-size: 14px;
  }

  .start   { justify-content: flex-start;   }
  .end     { justify-content: flex-end;     }
  .centre  { justify-content: center;       }
  .between { justify-content: space-between;}
  .around  { justify-content: space-around; }
  .evenly  { justify-content: space-evenly; }

  label { display: block; font-family: monospace; margin-top: 10px; }
</style>
</head>
<body>

  <label>justify-content: flex-start</label>
  <div class="flex-container start">
    <span>A</span><span>B</span><span>C</span>
  </div>

  <label>justify-content: flex-end</label>
  <div class="flex-container end">
    <span>A</span><span>B</span><span>C</span>
  </div>

  <label>justify-content: center</label>
  <div class="flex-container centre">
    <span>A</span><span>B</span><span>C</span>
  </div>

  <label>justify-content: space-between</label>
  <div class="flex-container between">
    <span>A</span><span>B</span><span>C</span>
  </div>

  <label>justify-content: space-around</label>
  <div class="flex-container around">
    <span>A</span><span>B</span><span>C</span>
  </div>

  <label>justify-content: space-evenly</label>
  <div class="flex-container evenly">
    <span>A</span><span>B</span><span>C</span>
  </div>

</body>
</html>
```

**Expected Output:** Six rows of three blue boxes, each showing a different spacing pattern.

> **Thinking Prompt:** Which value would you use to build a navigation bar with the logo on the far left and the login button on the far right? (`space-between`!)

---

## Part 5: Vertical Alignment — The Techniques

Vertical alignment is historically much harder than horizontal alignment in CSS. Over the years, developers have used many clever workarounds. Today, Flexbox has made it easy. Let us go through all the important techniques.

### Technique 1: `padding` — Simple and Reliable

The simplest way to centre content vertically is to add equal `padding` to the top and bottom of its container.

```css
.card {
  padding: 50px 20px;   /* 50px top/bottom creates equal vertical space */
  background-color: lightblue;
  text-align: center;
}
```

**Expected Output:** Text centred visually in the middle of the box (because equal space above and below pushes it to the visual centre).

**When to use it:** When you just need a comfortable amount of vertical breathing room and do not need pixel-perfect centring. Great for buttons, cards, and banners.

---

### Technique 2: `line-height` — For Single-Line Text

When you have a container with a fixed height and a single line of text, you can make the `line-height` equal to the container's `height`. This pushes the text to the vertical middle.

```html
<style>
  .btn {
    height: 50px;           /* fixed height */
    line-height: 50px;      /* same as height — centres single-line text */
    background-color: steelblue;
    color: white;
    text-align: center;
    width: 200px;
    border-radius: 6px;
    margin: 0 auto;
  }
</style>

<div class="btn">Click Me</div>
```

**Expected Output:** A 50px-tall blue button with the text perfectly vertically centred inside it.

**When to use it:** Only works reliably for single-line text. If the text wraps to a second line, it breaks completely.

---

### Technique 3: `position: absolute` with `transform` — Precise Centring

For absolute positioning, you can push an element 50% down from the top of its parent, then shift it back up by half its own height using `transform: translateY(-50%)`. This works regardless of the element's height.

```html
<style>
  .container {
    position: relative;        /* REQUIRED — makes this the anchor for absolute child */
    height: 300px;
    background-color: #f0f0f0;
  }

  .centred {
    position: absolute;
    top: 50%;                  /* move 50% down from the top of the container */
    left: 50%;                 /* move 50% right from the left of the container */
    transform: translate(-50%, -50%);  /* shift back by 50% of own width and height */
    background-color: steelblue;
    color: white;
    padding: 20px 30px;
    border-radius: 8px;
  }
</style>

<div class="container">
  <div class="centred">I am perfectly centred!</div>
</div>
```

**Expected Output:** The blue box sitting perfectly in both the horizontal AND vertical centre of the grey container, regardless of the box's size.

**How it works step by step:**
1. `top: 50%` — the element's top-left corner is placed at the 50% vertical point of the parent.
2. `left: 50%` — the element's top-left corner is placed at the 50% horizontal point of the parent.
3. At this point, the element is slightly off-centre because its top-left corner (not its centre) is at 50%.
4. `transform: translate(-50%, -50%)` shifts the element LEFT by 50% of its own width and UP by 50% of its own height.
5. Now the element's true centre aligns with the parent's centre. Perfect!

---

### Technique 4: Flexbox — The Modern Best Practice

Flexbox makes vertical AND horizontal centring trivially easy with just three lines:

```css
.container {
  display: flex;
  justify-content: center;   /* horizontal centring */
  align-items: center;       /* vertical centring */
}
```

That is it! The container now perfectly centres all its children both ways.

```html
<style>
  .container {
    display: flex;
    justify-content: center;    /* centres children horizontally */
    align-items: center;        /* centres children vertically */
    height: 300px;
    background-color: #1a1a2e;
  }

  .card {
    background-color: white;
    padding: 30px 40px;
    border-radius: 10px;
    text-align: center;
  }
</style>

<div class="container">
  <div class="card">
    <h2>Perfectly Centred</h2>
    <p>Both horizontally and vertically!</p>
  </div>
</div>
```

**Expected Output:** A white card sitting perfectly in the dead centre of a dark blue container.

### Vertical Alignment with `align-items`

`align-items` controls how flex items are aligned along the **cross axis** (by default, vertically top to bottom).

```css
.flex-container {
  display: flex;
  height: 200px;           /* needs a height to see vertical alignment */
  align-items: stretch;    /* default — items stretch to fill the container height */
  align-items: flex-start; /* items align to the top */
  align-items: flex-end;   /* items align to the bottom */
  align-items: center;     /* items align to the middle */
  align-items: baseline;   /* items align by their text baseline */
}
```

### Example — All `align-items` Values

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .flex-container {
    display: flex;
    height: 120px;
    background-color: #f0f0f0;
    margin: 8px 0;
    gap: 10px;
    padding: 5px;
  }

  .flex-container span {
    background-color: steelblue;
    color: white;
    padding: 10px 15px;
    border-radius: 4px;
  }

  .start    { align-items: flex-start; }
  .end      { align-items: flex-end;   }
  .centre   { align-items: center;     }
  .stretch  { align-items: stretch;    }
  .baseline { align-items: baseline;   }

  .big-font { font-size: 28px; }

  label { display: block; font-family: monospace; margin-top: 10px; }
</style>
</head>
<body>

  <label>align-items: flex-start</label>
  <div class="flex-container start">
    <span>A</span><span class="big-font">B</span><span>C</span>
  </div>

  <label>align-items: flex-end</label>
  <div class="flex-container end">
    <span>A</span><span class="big-font">B</span><span>C</span>
  </div>

  <label>align-items: center</label>
  <div class="flex-container centre">
    <span>A</span><span class="big-font">B</span><span>C</span>
  </div>

  <label>align-items: stretch (default)</label>
  <div class="flex-container stretch">
    <span>A</span><span class="big-font">B</span><span>C</span>
  </div>

  <label>align-items: baseline</label>
  <div class="flex-container baseline">
    <span>A</span><span class="big-font">B</span><span>C</span>
  </div>

</body>
</html>
```

**Expected Output:** Five rows showing the same three items (where B is larger) aligned differently — at the top, bottom, middle, stretched full height, and by their text baseline.

---

## Part 6: Aligning a Single Flex Item — `align-self`

If you want most flex children to have one alignment but a specific child to behave differently, use `align-self` on that individual child.

```css
.container {
  display: flex;
  align-items: flex-start;   /* all children align to the top by default */
  height: 200px;
}

.special-child {
  align-self: flex-end;      /* THIS child aligns to the bottom */
}

/* Other values: align-self: center, stretch, baseline, auto */
```

**Example:**

```html
<style>
  .nav {
    display: flex;
    align-items: flex-start;
    height: 80px;
    background-color: #333;
    padding: 0 20px;
    gap: 15px;
  }

  .nav a {
    color: white;
    text-decoration: none;
    padding: 5px 10px;
    align-self: center;     /* vertically centres the links in the tall nav bar */
  }

  .nav .logo {
    font-size: 24px;
    font-weight: bold;
    color: gold;
    align-self: center;
  }
</style>

<nav class="nav">
  <span class="logo">Brand</span>
  <a href="#">Home</a>
  <a href="#">About</a>
  <a href="#">Contact</a>
</nav>
```

**Expected Output:** A dark nav bar with the logo and links all vertically centred regardless of the bar's height.

---

## Part 7: Centring with CSS Grid

CSS Grid also makes centring extremely straightforward:

```css
.container {
  display: grid;
  place-items: center;   /* shorthand for align-items + justify-items: center */
  height: 300px;
}
```

`place-items: center` is a shorthand that sets both `align-items` and `justify-items` to `center` in one line.

```html
<style>
  .grid-centre {
    display: grid;
    place-items: center;
    height: 300px;
    background-color: #1a1a2e;
  }

  .box {
    background-color: gold;
    padding: 25px 40px;
    border-radius: 10px;
    font-size: 20px;
    font-weight: bold;
  }
</style>

<div class="grid-centre">
  <div class="box">Grid-centred!</div>
</div>
```

**Expected Output:** A gold box sitting perfectly in the centre of the dark container.

---

## Part 8: Horizontal Alignment Quick Reference

Here is a summary of all techniques and when to use each:

| Goal | Technique | When to Use |
|---|---|---|
| Centre a block element horizontally | `margin: 0 auto` + `width` | Centring containers, cards, wrappers |
| Align text left / right / centre | `text-align` | Text, headings, inline content |
| Push element to far left or right | `float: left` / `float: right` | Text wrapping around images; old-school layouts |
| Distribute children horizontally | Flexbox `justify-content` | Navigation bars, button groups, card rows |
| Centre element using position | `position: absolute` + `left: 50%` + `transform` | Overlays, modals, tooltips |

---

## Part 9: Vertical Alignment Quick Reference

| Goal | Technique | When to Use |
|---|---|---|
| Simple vertical space | Equal `padding` top and bottom | Buttons, cards, banners |
| Centre single-line text | `line-height` = `height` | Single-line buttons, list items |
| Centre child in positioned parent | `top: 50%` + `transform: translateY(-50%)` | Overlays, popups |
| Centre children in any container | Flexbox `align-items: center` | Most modern layouts |
| Centre in both directions at once | Flexbox `justify-content: center` + `align-items: center` | Hero sections, splash screens, modals |
| Quick centre with Grid | `display: grid; place-items: center` | Simple centring needs |

---

## Part 10: Guided Practice Exercises

### Exercise 1 — Centre a Card (Warm-Up)

**Objective:** Centre a product card horizontally on the page.

**Scenario:** You are building a single product page. There is one card in the middle of the screen.

**Starter Code:**

```html
<!DOCTYPE html>
<html>
<head>
<style>
  body {
    background-color: #f0f4f8;
    font-family: Arial, sans-serif;
  }

  .product-card {
    /* Add styles here to centre this card */
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  }
</style>
</head>
<body>

  <div class="product-card">
    <h2>Wireless Headphones</h2>
    <p>Premium sound quality. Up to 30 hours battery life.</p>
    <p><strong>₦45,000</strong></p>
  </div>

</body>
</html>
```

**Your Task:**
1. Give `.product-card` a fixed `width` of `400px`.
2. Add `margin: 40px auto` to centre it horizontally and add vertical spacing.

**Expected Output:** A white card 400px wide, centred on the grey background.

**Solution:**
```css
.product-card {
  width: 400px;
  margin: 40px auto;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}
```

**Self-Check Questions:**
- What would happen if you removed `width: 400px`? (The card would stretch full width and `margin: auto` would have no effect.)
- Why did we use `margin: 40px auto` instead of `margin: 0 auto`? (The `40px` adds a comfortable gap above and below the card. `auto` handles the left and right centring.)

---

### Exercise 2 — Navigation Bar with Float

**Objective:** Build a header bar with a logo on the left and navigation links on the right.

**Starter Code:**

```html
<!DOCTYPE html>
<html>
<head>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }

  .header {
    background-color: #2d2d2d;
    padding: 15px 30px;
    overflow: auto;   /* clearfix for floated children */
  }

  .logo {
    /* Float this to the left */
    color: gold;
    font-size: 22px;
    font-weight: bold;
  }

  .nav-links {
    /* Float this to the right */
    list-style: none;
  }

  .nav-links li {
    display: inline-block;
    margin-left: 20px;
  }

  .nav-links a {
    color: white;
    text-decoration: none;
    font-size: 15px;
  }
</style>
</head>
<body>

  <header class="header">
    <div class="logo">TechBrand</div>
    <ul class="nav-links">
      <li><a href="#">Home</a></li>
      <li><a href="#">Products</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  </header>

</body>
</html>
```

**Your Task:**
1. Add `float: left` to `.logo`.
2. Add `float: right` to `.nav-links`.

**Expected Output:** A dark header bar with "TechBrand" on the far left in gold, and the three navigation links on the far right in white.

**What-if Experiment:** What happens if you remove `overflow: auto` from `.header`? (The header collapses to zero height because its children are floated and taken out of normal flow. This is called the "collapsing parent" problem.)

---

### Exercise 3 — Flexbox Centred Hero Section

**Objective:** Build a full-screen hero section with text and a button perfectly centred both horizontally and vertically.

```html
<!DOCTYPE html>
<html>
<head>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: 'Arial', sans-serif;
  }

  .hero {
    /* Make this a flex container that centres its children both ways */
    background: linear-gradient(135deg, #1a1a2e, #16213e, #0f3460);
    height: 100vh;          /* full screen height */
    /* ADD: display, justify-content, align-items */
  }

  .hero-content {
    text-align: center;
    color: white;
  }

  .hero-content h1 {
    font-size: 48px;
    margin-bottom: 20px;
  }

  .hero-content p {
    font-size: 20px;
    margin-bottom: 30px;
    opacity: 0.8;
  }

  .hero-btn {
    display: inline-block;
    background-color: #e94560;
    color: white;
    padding: 14px 32px;
    border-radius: 30px;
    text-decoration: none;
    font-size: 16px;
    font-weight: bold;
    transition: background-color 0.3s;
  }

  .hero-btn:hover {
    background-color: #c73652;
  }
</style>
</head>
<body>

  <section class="hero">
    <div class="hero-content">
      <h1>Welcome to Our Platform</h1>
      <p>Build something amazing today.</p>
      <a class="hero-btn" href="#">Get Started</a>
    </div>
  </section>

</body>
</html>
```

**Your Task:** Add three CSS properties to `.hero`:
1. `display: flex`
2. `justify-content: center`
3. `align-items: center`

**Expected Output:** A full-screen deep blue gradient background with the heading, paragraph, and pink button all perfectly centred in the middle of the screen.

---

### Exercise 4 — Mixed Alignment Card Row

**Objective:** Create a row of three cards where the heading is left-aligned, the price is right-aligned, and a "Buy" button is centred.

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .card-row {
    display: flex;
    gap: 20px;
    padding: 30px;
    background-color: #f0f4f8;
    justify-content: center;
  }

  .card {
    background-color: white;
    border-radius: 10px;
    padding: 20px;
    width: 220px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.08);
  }

  .card h3 {
    text-align: left;         /* heading on the left */
    font-size: 16px;
    margin-bottom: 8px;
  }

  .card .price {
    text-align: right;        /* price on the right */
    font-size: 20px;
    font-weight: bold;
    color: #e94560;
    margin-bottom: 15px;
  }

  .card .btn {
    display: block;
    text-align: center;       /* button text centred */
    background-color: steelblue;
    color: white;
    padding: 10px;
    border-radius: 6px;
    text-decoration: none;
    font-size: 14px;
  }
</style>
</head>
<body>

  <div class="card-row">

    <div class="card">
      <h3>Laptop Stand</h3>
      <p class="price">₦12,500</p>
      <a class="btn" href="#">Buy Now</a>
    </div>

    <div class="card">
      <h3>Wireless Mouse</h3>
      <p class="price">₦8,000</p>
      <a class="btn" href="#">Buy Now</a>
    </div>

    <div class="card">
      <h3>USB-C Hub</h3>
      <p class="price">₦22,000</p>
      <a class="btn" href="#">Buy Now</a>
    </div>

  </div>

</body>
</html>
```

**Expected Output:**
- Three white product cards side by side in a grey row.
- Each card has its heading left-aligned, its price right-aligned, and a blue "Buy Now" button with centred text.

**Self-Check Questions:**
- Why do we use `text-align: center` on the `.btn` instead of `margin: 0 auto`?  
  (Because the button is `display: block` inside the card, but we want the text inside the button centred — `text-align` controls inline content within the block. `margin: 0 auto` would centre the button block itself if it had a fixed width less than the card, but here the button fills the card width, so `text-align` centres the text inside it.)
- What `justify-content` value on `.card-row` centres the three cards horizontally in the row? (`center`)

---

## Part 11: Mini Project — Centred Profile Card

In this mini-project you will build a polished profile card that uses every alignment technique from this lesson: `margin: auto` for page centring, `text-align` for text, Flexbox for internal layout, and `position + transform` for a decorative element.

### Stage 1: Page Setup and Outer Centring

Create `profile.html` and `profile.css`.

**profile.html:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Profile Card</title>
  <link rel="stylesheet" href="profile.css">
</head>
<body>

  <main class="page">

    <div class="profile-card">

      <div class="avatar-wrapper">
        <div class="avatar">JD</div>
      </div>

      <div class="card-body">
        <h1 class="name">Jane Doe</h1>
        <p class="role">Senior Web Developer</p>
        <p class="location">📍 Lagos, Nigeria</p>
      </div>

      <div class="stats">
        <div class="stat">
          <span class="stat-number">128</span>
          <span class="stat-label">Projects</span>
        </div>
        <div class="stat">
          <span class="stat-number">4.9</span>
          <span class="stat-label">Rating</span>
        </div>
        <div class="stat">
          <span class="stat-number">3k</span>
          <span class="stat-label">Followers</span>
        </div>
      </div>

      <div class="card-footer">
        <a class="btn btn-primary" href="#">Hire Me</a>
        <a class="btn btn-secondary" href="#">Portfolio</a>
      </div>

    </div>

  </main>

</body>
</html>
```

**Milestone Output (before CSS):** Plain unstyled text and links stacked vertically.

---

### Stage 2: Core CSS — Centring the Card on the Page

**profile.css:**

```css
/* --- Reset --- */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* --- Page: uses Flexbox to centre the card both ways --- */
.page {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(135deg, #1a1a2e, #16213e, #0f3460);
  font-family: 'Arial', sans-serif;
}

/* --- The Card itself: centred on page via the flex parent --- */
.profile-card {
  background-color: white;
  border-radius: 20px;
  width: 340px;
  overflow: hidden;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4);
  text-align: center;       /* text-align centres all inline content in the card */
}
```

**Milestone Output:** A white card centred perfectly on a dark blue gradient background.

---

### Stage 3: Avatar — Absolute Positioning and Transform Centring

```css
/* --- Avatar wrapper: provides a surface for the avatar to overlap --- */
.avatar-wrapper {
  background: linear-gradient(135deg, #e94560, #c73652);
  height: 100px;
  position: relative;       /* anchor for the absolute avatar circle */
}

/* --- Avatar circle: positioned to overlap the wrapper bottom edge --- */
.avatar {
  position: absolute;
  width: 90px;
  height: 90px;
  border-radius: 50%;
  background-color: #0f3460;
  color: white;
  font-size: 32px;
  font-weight: bold;
  border: 4px solid white;

  /* Centre the avatar circle on the wrapper's bottom edge */
  bottom: -45px;             /* pull half of it below the wrapper */
  left: 50%;                 /* start at horizontal centre */
  transform: translateX(-50%);  /* shift left by half its own width */

  /* Centre the initials text inside the circle */
  display: flex;
  justify-content: center;
  align-items: center;
}
```

**Milestone Output:** A coral/pink header band with a circular avatar overlapping its bottom edge, perfectly centred. The initials "JD" are centred inside the circle.

---

### Stage 4: Card Body Text and Stats

```css
/* --- Card body text --- */
.card-body {
  padding: 60px 30px 20px;  /* 60px top to clear the avatar overlap */
}

.name {
  font-size: 24px;
  color: #1a1a2e;
  margin-bottom: 6px;
  text-align: center;
}

.role {
  color: #555;
  font-size: 15px;
  margin-bottom: 6px;
  text-align: center;
}

.location {
  color: #888;
  font-size: 13px;
  text-align: center;
}

/* --- Stats row: Flexbox distributes the three stats evenly --- */
.stats {
  display: flex;
  justify-content: space-around;  /* equal space between stats */
  align-items: center;
  padding: 20px 30px;
  border-top: 1px solid #f0f0f0;
  border-bottom: 1px solid #f0f0f0;
  margin: 15px 0;
}

.stat {
  display: flex;
  flex-direction: column;   /* stack number above label */
  align-items: center;      /* centre number and label horizontally */
}

.stat-number {
  font-size: 22px;
  font-weight: bold;
  color: #1a1a2e;
}

.stat-label {
  font-size: 12px;
  color: #888;
  margin-top: 3px;
}
```

**Milestone Output:** Name, role, and location text centred. Three stats (Projects, Rating, Followers) evenly spaced in a row below the text.

---

### Stage 5: Buttons — Flex Row, Centred

```css
/* --- Footer buttons --- */
.card-footer {
  display: flex;
  justify-content: center;  /* centre the button group */
  gap: 12px;
  padding: 20px 30px 30px;
}

.btn {
  padding: 10px 24px;
  border-radius: 25px;
  font-size: 14px;
  font-weight: bold;
  text-decoration: none;
  text-align: center;
  cursor: pointer;
  transition: opacity 0.2s;
}

.btn:hover {
  opacity: 0.85;
}

.btn-primary {
  background-color: #e94560;
  color: white;
}

.btn-secondary {
  background-color: transparent;
  color: #e94560;
  border: 2px solid #e94560;
}
```

**Final Output:**
A polished profile card perfectly centred on a deep blue gradient background, containing:
- A coral header band
- A circular avatar overlapping the header bottom edge, centred using `absolute` + `left: 50%` + `transform: translateX(-50%)`
- "JD" initials centred inside the avatar using Flexbox
- Name, role, and location text centred with `text-align: center`
- Three stats distributed evenly using Flexbox `justify-content: space-around`
- Two buttons centred using Flexbox `justify-content: center`

---

### Reflection Questions for the Mini-Project

1. The page uses Flexbox with `justify-content: center` and `align-items: center`. What would happen if you removed `min-height: 100vh` from `.page`? (The page would have no height, so the card would not appear vertically centred — there would be no space to centre it within.)

2. The avatar uses `left: 50%` + `transform: translateX(-50%)`. Why not just use `margin: 0 auto`? (Because the avatar is `position: absolute` — `margin: auto` does not work on absolutely positioned elements the same way. The `transform` technique is the reliable method for absolutely positioned elements.)

3. The stats use `justify-content: space-around`. How would the layout change with `space-between`? (The stats would be pushed to the extreme edges of the container — the first stat would touch the left edge, the last the right edge. `space-around` keeps them more balanced with some space at the edges too.)

4. The card has `text-align: center` set on `.profile-card`. Which child elements benefit from this? Which do NOT? (Text content like `.name`, `.role`, `.location` benefits. The flex children in `.stats` and `.card-footer` are not affected because they use Flexbox alignment instead.)

---

## Part 12: Common Beginner Mistakes

### Mistake 1 — `margin: auto` without a width

**Wrong:**
```css
.box {
  margin: 0 auto;  /* won't work — no width defined */
}
```

**Correct:**
```css
.box {
  width: 500px;    /* or max-width: 500px */
  margin: 0 auto;
}
```

---

### Mistake 2 — Using `text-align: center` to centre a block element

`text-align` only affects inline content. It does NOT centre a block element.

**Wrong (for centring a block):**
```css
.parent {
  text-align: center;  /* this centres the TEXT inside .child, not .child itself */
}

.child {
  width: 200px;
  background: blue;
}
```

**Correct:**
```css
.child {
  width: 200px;
  margin: 0 auto;    /* THIS centres the block element */
}
```

---

### Mistake 3 — Forgetting `height` when vertical centring

```css
/* This won't appear vertically centred — the container has no height! */
.container {
  display: flex;
  align-items: center;
  /* missing: height or min-height */
}
```

**Correct:**
```css
.container {
  display: flex;
  align-items: center;
  min-height: 300px;   /* container needs a height to centre within */
}
```

---

### Mistake 4 — Collapsing float parent

```html
<!-- The container collapses because its only children are floated -->
<div class="container">
  <div style="float: left;">Left</div>
  <div style="float: right;">Right</div>
  <!-- Container height = 0! Nothing to hold it open. -->
</div>
```

**Fix — Add `overflow: auto` to the container:**
```css
.container {
  overflow: auto;   /* forces the container to expand and wrap its floated children */
}
```

---

### Mistake 5 — Using `line-height` for multi-line text centring

```css
/* Only works for exactly one line of text */
.btn {
  height: 50px;
  line-height: 50px;   /* breaks if text wraps to 2 lines */
}
```

**Better for modern layouts:**
```css
.btn {
  height: 50px;
  display: flex;
  align-items: center;    /* works perfectly even if text wraps */
  justify-content: center;
}
```

---

### Mistake 6 — `margin: auto` on a flex item's parent

```css
/* Trying to use margin: auto on a flex item itself */
.flex-container {
  display: flex;
}

.child {
  margin: auto;   /* this actually DOES work in Flexbox — it absorbs free space */
}
```

> **Interesting Note:** `margin: auto` on a flex item actually works inside a flex container! It absorbs all available free space in the specified direction, effectively centring the item. This is a legitimate and useful technique for pushing items to opposite ends.

---

## Reflection Questions

1. You want to centre a `<div>` that contains a paragraph of text both horizontally and vertically on the screen. What is the minimal CSS needed? (Make the body or a wrapper a flex container with `justify-content: center`, `align-items: center`, and `min-height: 100vh`. Give the `<div>` a `width`.)

2. A student sets `text-align: center` on a `<p>` but nothing happens. What could be the reason? (The parent container might be very narrow, or the `<p>` might be inside an element that has overriding alignment. More likely: there is nothing wrong — `text-align: center` on a `<p>` should always work. Check if `width: 0` or `display: none` is accidentally applied.)

3. You are using `float: left` and `float: right` to create a two-column layout. The footer is overlapping the columns instead of sitting below them. What is the fix? (`clear: both` on the footer.)

4. When would you choose `position: absolute` + `transform: translate(-50%, -50%)` over Flexbox for centring? (When you need to centre something inside an element that already has `position: relative` and cannot be changed to a flex container — for example, a label over an image, or a badge on a card corner.)

5. What is `place-items: center` and which layout model uses it? (It is a shorthand for `align-items: center` + `justify-items: center`, used in CSS Grid.)

---

## Completion Checklist

- [ ] I can centre a block element horizontally using `margin: 0 auto` and a defined width
- [ ] I understand why `margin: auto` requires a `width` to work
- [ ] I can align text using `text-align: left`, `right`, `center`, and `justify`
- [ ] I understand the difference between aligning text and aligning a block element
- [ ] I can use `float: left` and `float: right` to push elements to the sides
- [ ] I can use `clear: both` to stop elements from wrapping around floated elements
- [ ] I can fix the "collapsing parent" problem caused by floated children
- [ ] I can create a horizontal flex container and distribute items using `justify-content`
- [ ] I can vertically align flex children using `align-items`
- [ ] I can override vertical alignment for a single item using `align-self`
- [ ] I can centre an element using `position: absolute` + `top: 50%` + `transform: translateY(-50%)`
- [ ] I can centre content in both directions at once using Flexbox
- [ ] I can use CSS Grid `place-items: center` for quick centring
- [ ] I completed all four guided exercises
- [ ] I built the full profile card mini-project
- [ ] I can identify which technique is best for a given alignment scenario

---

## Lesson Summary

CSS alignment is one of the most essential skills in web development. This lesson covered all the major techniques from classic to modern.

**Horizontal alignment** can be achieved by applying `margin: 0 auto` with a `width` on block elements, using `text-align` for inline content and text, using `float: left` or `float: right` to push elements to the sides (with `clear: both` to fix the footer), or using Flexbox `justify-content` to distribute flex children across the horizontal axis.

**Vertical alignment** can be achieved using equal `padding` for simple visual centring, `line-height` equal to height for single-line text, `position: absolute` with `top: 50%` and `transform: translateY(-50%)` for precisely positioned elements, or Flexbox `align-items: center` for the cleanest, most modern approach.

**Centring in both directions simultaneously** is best done with Flexbox (`display: flex` + `justify-content: center` + `align-items: center`) or CSS Grid (`display: grid` + `place-items: center`).

**Real World Uses:**
- `margin: 0 auto` on the main content wrapper of almost every website
- `text-align: center` for hero headings, call-to-action buttons, and cards
- `float` for magazine-style text wrapping around images
- Flexbox for navigation bars, card grids, button groups, and form layouts
- `position + transform` centring for modal dialogs, tooltips, and image overlays
- Flexbox hero sections with perfectly centred content at full viewport height

The ability to control alignment precisely — knowing exactly why something is where it is — is what separates a developer who struggles with CSS from one who builds layouts confidently and quickly.
