---
render_with_liquid: false
title: "CSS Box Sizing"
nav_order: 67
---

# CSS Box Sizing

## Lesson Introduction

Have you ever set the width of a box on a webpage and then been confused because it turned out **much bigger** than you expected? You set it to `300px`, but it came out looking like `360px`? You are not alone — this is one of the most common surprises beginners face in CSS. The reason is how CSS calculates the **actual size** of an element by default.

In this lesson, you will learn:

- What the **CSS Box Model** is (a quick recap to set the foundation)
- Why elements often appear **bigger than you set** them
- What the `box-sizing` property is and how it solves this problem
- How to use `box-sizing: border-box` to write **predictable, clean layouts**
- A professional trick used by almost every real-world website today
- Hands-on exercises and a mini-project to practise everything

No prior knowledge of `box-sizing` is needed. If you know basic HTML and CSS (how to write selectors and properties), you are ready to begin.

---

## Prerequisite Concepts

Before we dive in, let us make sure you understand two foundational ideas: the **Box Model** and what **padding** and **border** mean in CSS.

### What Is the CSS Box Model?

Every single HTML element — a heading, a paragraph, a `<div>`, a button — is treated by the browser as a **rectangular box**. This box has four layers, like the layers of a picture frame:

```
+-----------------------------+
|         MARGIN              |  ← Space OUTSIDE the element
|  +-----------------------+  |
|  |       BORDER          |  |  ← The visible outline/frame
|  |  +-----------------+  |  |
|  |  |    PADDING      |  |  |  ← Space INSIDE, between border and content
|  |  |  +-----------+  |  |  |
|  |  |  |  CONTENT  |  |  |  |  ← Your actual text, image, etc.
|  |  |  +-----------+  |  |  |
|  |  +-----------------+  |  |
|  +-----------------------+  |
+-----------------------------+
```

- **Content** — The actual text, image, or child elements inside
- **Padding** — The breathing room between the content and the border
- **Border** — A visible (or invisible) frame around the element
- **Margin** — Space outside the border that separates this element from its neighbours

### What Are Width and Height in CSS?

When you write `width: 300px;` in CSS, you are telling the browser: *"Make the content area of this element 300 pixels wide."*

Notice the key phrase: **content area**. By default, CSS does NOT include padding and border in that `300px`. It only applies to the inner content area.

This means the element's **actual visible size on screen** is:

```
Actual width  = width + left padding + right padding + left border + right border
Actual height = height + top padding + bottom padding + top border + bottom border
```

This is the **root cause** of elements appearing bigger than expected.

---

## Conceptual Understanding

### The Problem: Default Box Sizing

Let us build an intuition with a real-world analogy before we look at code.

**Analogy: Ordering a Pizza Box**

Imagine you order a pizza and ask for a **30 cm box**. The restaurant gives you a box where the pizza itself is 30 cm — but then they add a 5 cm thick foam lining on each side (padding) and a 1 cm cardboard frame (border). The final box you receive is actually:

```
30 cm (pizza) + 5 cm (foam left) + 5 cm (foam right) + 1 cm (frame left) + 1 cm (frame right)
= 42 cm total
```

You asked for 30 cm but got 42 cm! That is exactly what CSS does by default.

In CSS terms, the default behaviour is called **`box-sizing: content-box`**. The `width` you set only applies to the content — not the padding or border.

### Example 1 — Seeing the Problem

Here are two `<div>` elements. Both have `width: 300px` and `height: 100px`. The first has no padding. The second has `padding: 50px`. Watch what happens to the actual size:

```html
<!DOCTYPE html>
<html>
<head>
<style>
  /* Both divs are declared at the SAME size */
  .div1 {
    width: 300px;
    height: 100px;
    border: 1px solid blue;
    background-color: lightblue;
  }

  .div2 {
    width: 300px;
    height: 100px;
    padding: 50px;          /* 50px on all 4 sides */
    border: 1px solid red;
    background-color: lightsalmon;
  }
</style>
</head>
<body>
  <div class="div1">I am div1. Width declared: 300px</div>
  <div class="div2">I am div2. Width declared: 300px but padding: 50px</div>
</body>
</html>
```

**Expected output (what you see on screen):**

```
div1 → Actual width = 300px + 1px + 1px (borders) = 302px wide
div2 → Actual width = 300px + 50px + 50px (padding) + 1px + 1px (borders) = 402px wide
```

Even though BOTH divs say `width: 300px`, div2 is **100 pixels wider** on screen because its padding is added on top of the declared width.

> 💡 **Think about it:** What would happen if you had four of these `div2` boxes side by side in a row, expecting them all to fit in a 1200px container? They would overflow and break your layout!

---

### The Solution: `box-sizing: border-box`

The CSS property `box-sizing` was introduced to fix exactly this problem. It controls how the browser **calculates** the total width and height of an element.

There are two possible values:

| Value | What It Means |
|---|---|
| `content-box` | Default. Width/height apply to the CONTENT only. Padding and border are added on top. |
| `border-box` | Width/height include padding and border. The content shrinks to fit inside. |

**The key insight about `border-box`:**

When you set `box-sizing: border-box;`, the browser keeps the element at exactly the width/height you declare. If there is padding or a border, the browser **shrinks the content area** to make room for them — so the total stays exactly the declared size.

Using the pizza analogy again: with `border-box`, you get a box that is exactly 30 cm total. The pizza inside gets smaller to make room for the foam and cardboard, but the box itself is exactly 30 cm as requested.

---

### Example 2 — Applying `border-box` to Both Divs

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .div1 {
    width: 300px;
    height: 100px;
    border: 1px solid blue;
    background-color: lightblue;
    box-sizing: border-box;   /* ← Added this line */
  }

  .div2 {
    width: 300px;
    height: 100px;
    padding: 50px;
    border: 1px solid red;
    background-color: lightsalmon;
    box-sizing: border-box;   /* ← Added this line */
  }
</style>
</head>
<body>
  <div class="div1">Div1: width 300px, border-box</div>
  <div class="div2">Div2: width 300px, padding 50px, border-box</div>
</body>
</html>
```

**Expected output:**

```
div1 → Actual width on screen = exactly 300px
div2 → Actual width on screen = exactly 300px ✅
```

Both divs are now the **same width** on screen. The padding in div2 is now contained *inside* the 300px. The content area becomes 300 - 50 - 50 - 1 - 1 = 198px, but that is handled automatically by the browser. You just work with 300px and it stays 300px. 

> 💡 **Think about it:** Why is this so powerful for layout? If you are building a two-column layout and want each column to be exactly 50% wide, `border-box` ensures that even if you add padding to each column, they still fit perfectly side by side.

---

### The Universal `border-box` Reset

Since `box-sizing: border-box` is almost always more intuitive and useful, professional developers apply it to **every element** on the page using the universal CSS selector `*`:

```css
* {
  box-sizing: border-box;
}
```

**Line-by-line explanation:**

- `*` — This is the **universal selector**. It targets every single HTML element on the page — every div, paragraph, heading, input, button, image — everything.
- `{` — Opens the rule block
- `box-sizing: border-box;` — Sets the box-sizing model to `border-box` for all elements
- `}` — Closes the rule block

**Why use this?**

When you apply `border-box` universally, you can confidently set widths and heights knowing they will never surprise you with extra pixels from padding or borders. Many browsers already use `border-box` for some form elements (like `<input>` and `<textarea>`), so applying it universally also ensures **consistency** across all elements.

> ✅ **Real World Fact:** Almost every professional CSS framework, including Bootstrap and Tailwind CSS, applies `box-sizing: border-box` globally as a reset. When you see `* { box-sizing: border-box; }` at the top of a CSS file, you know the developer cares about clean, predictable layouts.

---

### Example 3 — Universal Reset in Action

```html
<!DOCTYPE html>
<html>
<head>
<style>
  /* Apply border-box to EVERYTHING on the page */
  * {
    box-sizing: border-box;
  }

  /* Now ALL elements follow border-box rules automatically */
  .container {
    width: 600px;
    padding: 20px;
    border: 2px solid black;
    background-color: #f0f0f0;
  }

  .column {
    width: 50%;        /* Exactly half of 600px = 300px */
    padding: 15px;
    border: 1px solid grey;
    background-color: white;
    display: inline-block;
  }
</style>
</head>
<body>
  <div class="container">
    <div class="column">Column 1 — exactly 50% wide</div><div class="column">Column 2 — exactly 50% wide</div>
  </div>
</body>
</html>
```

**Expected output:**

```
Container: 600px wide with 20px inner padding
Column 1:  300px wide (50%) with 15px padding and 1px border — all contained within 300px
Column 2:  300px wide (50%) with 15px padding and 1px border — all contained within 300px
Both columns sit perfectly side by side inside the 600px container ✅
```

Without `border-box`, the columns would overflow the container because their padding (15px × 2 = 30px) would be added to their 50% width.

---

## Simple Standalone Examples

### Example A — Same Width, Different Padding (No `border-box`)

```css
/* WITHOUT border-box — default content-box behaviour */
.box-a {
  width: 200px;
  padding: 0px;
  border: 2px solid navy;
}

.box-b {
  width: 200px;
  padding: 20px;
  border: 2px solid navy;
}
```

**Calculating actual sizes:**

```
box-a actual width = 200 + 0 + 0 + 2 + 2 = 204px
box-b actual width = 200 + 20 + 20 + 2 + 2 = 244px
```

They look different on screen even though both declare `width: 200px`.

---

### Example B — Same Width, Different Padding (WITH `border-box`)

```css
/* WITH border-box */
.box-a {
  width: 200px;
  padding: 0px;
  border: 2px solid navy;
  box-sizing: border-box;
}

.box-b {
  width: 200px;
  padding: 20px;
  border: 2px solid navy;
  box-sizing: border-box;
}
```

**Calculating actual sizes:**

```
box-a actual width = exactly 200px ✅
box-b actual width = exactly 200px ✅  (content shrinks to 200 - 20 - 20 - 2 - 2 = 156px internally)
```

Both boxes look the same width on screen.

---

### Example C — Understanding the Content Shrinkage

This example helps you see how the content area shrinks when `border-box` is used:

```css
* {
  box-sizing: border-box;
}

.card {
  width: 400px;
  padding: 40px;
  border: 5px solid darkgreen;
  background-color: lightgreen;
}
```

**What the browser calculates internally:**

```
Total declared width:  400px
Left border:            -5px
Right border:           -5px
Left padding:          -40px
Right padding:         -40px
─────────────────────────────
Content area width:    310px  ← Browser auto-adjusts this
```

The element still appears exactly 400px wide on screen. The browser just arranges the internal layers to fit within that budget.

---

## The `box-sizing` Property Reference

| Property | Values | What It Does |
|---|---|---|
| `box-sizing` | `content-box` | Default. `width`/`height` = content only. Padding + border are extra. |
| `box-sizing` | `border-box` | `width`/`height` = content + padding + border. Element stays exactly declared size. |

---

## Guided Practice Exercises

### Exercise 1 — Spot the Size Difference

**Objective:** Observe how padding changes the actual size of an element without `border-box`.

**Scenario:** You are building a product card for an online shop. Each card should be 250px wide. You add padding for spacing.

**Steps:**

1. Create an HTML file with the code below
2. Open it in a browser
3. Observe that both cards declare `width: 250px` but look different sizes

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .card {
    width: 250px;
    border: 2px solid #333;
    background-color: #fafafa;
    margin: 10px;
    display: inline-block;
    vertical-align: top;
  }

  .card-no-padding {
    /* No padding — card stays close to 250px */
  }

  .card-with-padding {
    padding: 20px; /* Adds 40px total to width! */
  }
</style>
</head>
<body>
  <div class="card card-no-padding">
    <p>Card A — No padding. Width: 250px declared.</p>
  </div>
  <div class="card card-with-padding">
    <p>Card B — Padding: 20px. Width: 250px declared.</p>
  </div>
</body>
</html>
```

**Expected output:** Card B is visibly wider than Card A on screen.

**Self-check questions:**
- How many extra pixels wide is Card B compared to Card A?
- If you put four of these cards side by side expecting 1000px total, what would actually happen?

**Hints:**
- Card B actual width = 250 + 20 + 20 + 2 + 2 = 294px
- Four Card B elements = 4 × 294 = 1176px — that is 176px too wide for a 1000px container!

---

### Exercise 2 — Applying the Fix

**Objective:** Add `box-sizing: border-box` to fix the layout from Exercise 1.

**Steps:**

1. Take the code from Exercise 1
2. Add `* { box-sizing: border-box; }` at the top of your CSS
3. Observe that both cards are now the same width

```html
<!DOCTYPE html>
<html>
<head>
<style>
  /* THE FIX */
  * {
    box-sizing: border-box;
  }

  .card {
    width: 250px;
    border: 2px solid #333;
    background-color: #fafafa;
    margin: 10px;
    display: inline-block;
    vertical-align: top;
  }

  .card-no-padding {
    /* No padding */
  }

  .card-with-padding {
    padding: 20px;
  }
</style>
</head>
<body>
  <div class="card card-no-padding">
    <p>Card A — No padding.</p>
  </div>
  <div class="card card-with-padding">
    <p>Card B — Padding: 20px.</p>
  </div>
</body>
</html>
```

**Expected output:** Both cards appear exactly 250px wide. ✅

**What-if challenge:** What happens if you change `padding: 20px` to `padding: 100px`? Try it and see — does the element stay 250px wide? What happens to the text inside?

---

### Exercise 3 — Two-Column Layout

**Objective:** Build a clean two-column layout using percentages and `border-box`.

**Scenario:** You are building a blog page with a main content area (70% wide) and a sidebar (30% wide). They must sit side by side.

```html
<!DOCTYPE html>
<html>
<head>
<style>
  * {
    box-sizing: border-box;
  }

  .layout {
    width: 900px;
    background-color: #eee;
    overflow: hidden; /* Clear floats */
  }

  .main-content {
    width: 70%;
    padding: 20px;
    border: 1px solid #999;
    background-color: white;
    float: left;
  }

  .sidebar {
    width: 30%;
    padding: 20px;
    border: 1px solid #999;
    background-color: #f9f9f9;
    float: left;
  }
</style>
</head>
<body>
  <div class="layout">
    <div class="main-content">
      <h2>Main Article</h2>
      <p>This is the main content area. It takes up 70% of the layout.</p>
    </div>
    <div class="sidebar">
      <h2>Sidebar</h2>
      <p>This is the sidebar. It takes up 30%.</p>
    </div>
  </div>
</body>
</html>
```

**Expected output:** Both columns sit perfectly side by side inside the 900px layout. Total = 70% + 30% = 100% ✅

**Self-check questions:**
- What would happen without `box-sizing: border-box`?
- Remove the `* { box-sizing: border-box; }` line and reload. What do you observe?

---

## Mini-Project: Product Card Grid

Let us build a realistic mini-project: a 3-card product grid for an online shop. Each card will have an image placeholder, a product name, a price, and a button — and all three cards must be exactly the same width with consistent padding.

### Stage 1 — Setup

Create an HTML file. Set up the page structure with a heading and a container:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Product Grid</title>
  <style>
    /* STAGE 1: Global reset */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      padding: 30px;
    }

    h1 {
      text-align: center;
      margin-bottom: 30px;
      color: #333;
    }
  </style>
</head>
<body>
  <h1>Our Products</h1>
  <!-- Cards will go here -->
</body>
</html>
```

**Milestone output:** Page loads with a heading "Our Products" on a light grey background.

---

### Stage 2 — Card Grid Container

Add the grid container and card base styles:

```html
<style>
  /* STAGE 2: Grid container */
  .product-grid {
    display: flex;
    gap: 20px;                 /* Space between cards */
    justify-content: center;
    flex-wrap: wrap;           /* Cards wrap on small screens */
    max-width: 1000px;
    margin: 0 auto;            /* Centre the grid */
  }

  .product-card {
    width: 300px;              /* Each card is exactly 300px */
    padding: 20px;             /* Inner breathing room */
    border: 1px solid #ddd;
    border-radius: 8px;
    background-color: white;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    /* box-sizing: border-box is already applied via * selector */
  }
</style>
```

**Key point:** Because we used `* { box-sizing: border-box; }` in Stage 1, the `padding: 20px` on each card is included within its 300px — the cards will not overflow!

---

### Stage 3 — Card Content

Now add the internal card elements:

```html
<style>
  /* STAGE 3: Card internals */
  .product-image {
    width: 100%;               /* Fill the full card width */
    height: 180px;
    background-color: #c8e6c9; /* Placeholder colour */
    border-radius: 4px;
    margin-bottom: 15px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #555;
    font-size: 14px;
  }

  .product-name {
    font-size: 18px;
    font-weight: bold;
    color: #222;
    margin-bottom: 8px;
  }

  .product-price {
    font-size: 22px;
    color: #e74c3c;
    margin-bottom: 15px;
  }

  .buy-button {
    display: block;
    width: 100%;               /* Full width of card — works perfectly with border-box */
    padding: 12px;
    background-color: #27ae60;
    color: white;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    text-align: center;
  }

  .buy-button:hover {
    background-color: #219a52;
  }
</style>
```

---

### Stage 4 — Final HTML with All Three Cards

Put everything together:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Product Grid</title>
  <style>
    /* Global reset with border-box */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      padding: 30px;
    }

    h1 {
      text-align: center;
      margin-bottom: 30px;
      color: #333;
    }

    .product-grid {
      display: flex;
      gap: 20px;
      justify-content: center;
      flex-wrap: wrap;
      max-width: 1000px;
      margin: 0 auto;
    }

    .product-card {
      width: 300px;
      padding: 20px;
      border: 1px solid #ddd;
      border-radius: 8px;
      background-color: white;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .product-image {
      width: 100%;
      height: 180px;
      background-color: #c8e6c9;
      border-radius: 4px;
      margin-bottom: 15px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #555;
      font-size: 14px;
    }

    .product-name {
      font-size: 18px;
      font-weight: bold;
      color: #222;
      margin-bottom: 8px;
    }

    .product-price {
      font-size: 22px;
      color: #e74c3c;
      margin-bottom: 15px;
    }

    .buy-button {
      display: block;
      width: 100%;
      padding: 12px;
      background-color: #27ae60;
      color: white;
      border: none;
      border-radius: 4px;
      font-size: 16px;
      cursor: pointer;
      text-align: center;
    }

    .buy-button:hover {
      background-color: #219a52;
    }
  </style>
</head>
<body>

  <h1>Our Products</h1>

  <div class="product-grid">

    <div class="product-card">
      <div class="product-image">[ Product Image ]</div>
      <p class="product-name">Wireless Headphones</p>
      <p class="product-price">₦45,000</p>
      <button class="buy-button">Add to Cart</button>
    </div>

    <div class="product-card">
      <div class="product-image">[ Product Image ]</div>
      <p class="product-name">Bluetooth Speaker</p>
      <p class="product-price">₦28,500</p>
      <button class="buy-button">Add to Cart</button>
    </div>

    <div class="product-card">
      <div class="product-image">[ Product Image ]</div>
      <p class="product-name">Smart Watch</p>
      <p class="product-price">₦72,000</p>
      <button class="buy-button">Add to Cart</button>
    </div>

  </div>

</body>
</html>
```

**Final expected output:**

```
Page shows "Our Products" heading at the top.

Three cards sit side by side, each exactly 300px wide.
Each card has:
  - A green image placeholder (180px tall)
  - A product name in bold
  - A price in red
  - A green "Add to Cart" button that fills the card width

All three cards are perfectly aligned and evenly spaced.
The 20px inner padding on each card is included WITHIN the 300px — not added on top. ✅
```

**Reflection questions:**
- Remove `* { box-sizing: border-box; }` and reload. What breaks?
- Try changing `padding: 20px` to `padding: 40px` on the cards. With `border-box`, do the cards still stay 300px wide?
- What would you need to add to make this layout stack vertically on mobile screens?

**Optional advanced extension:** Add a `border: 3px solid green` to just one card and observe that it stays exactly 300px wide because of `border-box`. Without `border-box`, it would grow by 6 extra pixels.

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting `box-sizing` and wondering why things overflow

**Wrong approach (default content-box):**

```css
.sidebar {
  width: 30%;
  padding: 20px;
  border: 2px solid grey;
  float: left;
}

.main {
  width: 70%;
  padding: 20px;
  border: 2px solid grey;
  float: left;
}
```

**Problem:** 30% + 70% = 100%, which seems right. But padding and border add extra pixels, making the total width MORE than 100%. The second column drops below the first.

**Correct approach:**

```css
* {
  box-sizing: border-box;  /* Add this first! */
}

.sidebar {
  width: 30%;
  padding: 20px;
  border: 2px solid grey;
  float: left;
}

.main {
  width: 70%;
  padding: 20px;
  border: 2px solid grey;
  float: left;
}
```

Now 30% + 70% truly = 100% because padding and border are contained within each percentage. ✅

---

### Mistake 2 — Applying `border-box` to only one element in a pair

```css
/* Mistake: Only one element gets border-box */
.div1 {
  width: 300px;
  /* Uses default content-box */
}

.div2 {
  width: 300px;
  padding: 20px;
  box-sizing: border-box;  /* Only div2 has border-box */
}
```

**Problem:** The two elements calculate their sizes differently, leading to inconsistent layouts that are hard to debug.

**Fix:** Always apply `border-box` universally:

```css
* {
  box-sizing: border-box;
}
```

---

### Mistake 3 — Confusing `margin` with `padding` in the context of `box-sizing`

**Important:** `box-sizing: border-box` only includes **padding** and **border** within the declared width. It does **NOT** include **margin**.

```css
* {
  box-sizing: border-box;
}

.box {
  width: 200px;
  padding: 20px;   /* Included in 200px ✅ */
  border: 2px solid;  /* Included in 200px ✅ */
  margin: 30px;    /* NOT included — adds space OUTSIDE the 200px ⚠️ */
}
```

**The element on screen:**
- The box itself = exactly 200px wide ✅
- There is 30px of invisible space around the outside of the box (margin)
- The total space the element occupies in the flow = 200px + 30px + 30px = 260px

Margin is always external. `border-box` does not change this behaviour.

---

### Mistake 4 — Setting padding larger than width

```css
* {
  box-sizing: border-box;
}

.tiny-box {
  width: 50px;
  padding: 40px;  /* 40 + 40 = 80px padding — more than the width! */
}
```

**Problem:** The padding alone exceeds the declared width. The browser cannot make the content area negative. It will set the content area to 0 (or a very small value) and the box may not behave as expected.

**Fix:** Keep padding smaller than the total width it is being applied to. A good rule of thumb: padding should not exceed 40% of the element's width.

---

## Reflection Questions

Take a moment to think through these questions. They will solidify your understanding:

1. You set `width: 400px` on a div with `padding: 30px` and `border: 5px solid`. Without `border-box`, what is the actual rendered width of the div?

2. You add `box-sizing: border-box` to the same div above. Now what is the actual rendered width?

3. Why do professional developers write `* { box-sizing: border-box; }` instead of only adding it to specific elements?

4. Does `box-sizing: border-box` affect margin? Why or why not?

5. You have a layout where two columns should each be 50% wide. You add 15px padding and a 1px border to each. Without `border-box`, will the columns fit side by side? What about with `border-box`?

6. You see a website where the sidebar is falling below the main content instead of sitting beside it. What might `box-sizing` have to do with this bug?

**Answers:**

1. 400 + 30 + 30 + 5 + 5 = **470px**
2. Exactly **400px** (padding and border are included within the 400px)
3. Because applying it universally ensures every element — including ones added later — uses the same predictable model. If you apply it only to some elements, inconsistencies arise.
4. No. `border-box` only controls how padding and border relate to the declared width/height. Margin sits entirely outside and is not affected.
5. Without `border-box`: No — each column would be 50% + 32px wide (padding + border), causing overflow. With `border-box`: Yes — they fit perfectly because padding and border are within the 50%.
6. The sidebar and main content likely have padding or borders that cause their combined width to exceed 100%, pushing the sidebar to a new line. Adding `box-sizing: border-box` globally would fix it.

---

## Completion Checklist

Before moving to the next lesson, confirm you have achieved the following:

- [ ] I understand what the CSS Box Model is (content, padding, border, margin)
- [ ] I can explain why elements appear bigger than their declared width by default
- [ ] I know what `box-sizing: content-box` means (the default browser behaviour)
- [ ] I know what `box-sizing: border-box` does and how it solves the sizing problem
- [ ] I can apply `box-sizing: border-box` to a single element
- [ ] I can apply the universal `* { box-sizing: border-box; }` reset
- [ ] I understand that `border-box` does NOT include margin in the width calculation
- [ ] I completed the two-column layout exercise successfully
- [ ] I built the product card mini-project and observed that all cards stayed 300px wide
- [ ] I can explain at least two common mistakes related to `box-sizing`

---

## Lesson Summary

The CSS `box-sizing` property controls **how the browser calculates the total width and height of an element**.

By default, CSS uses `box-sizing: content-box`, which means the `width` and `height` you set only apply to the **content area**. Padding and border are then added on top, making elements appear larger than declared. This leads to layout bugs, overflowing containers, and misaligned columns.

The fix is `box-sizing: border-box`. When applied, the padding and border are included **within** the declared width and height. The element stays exactly the size you set. The content area shrinks internally to accommodate padding and border, but from the outside, the element is exactly as wide and tall as you declared.

Because this behaviour is almost universally preferred, the standard professional practice is to apply it globally:

```css
* {
  box-sizing: border-box;
}
```

This simple three-line rule eliminates an entire category of CSS layout bugs and is found at the top of nearly every professional stylesheet, CSS framework, and modern web project. Learning it early — as you have done in this lesson — gives you a strong foundation for building clean, reliable web layouts.

| Property | Value | Behaviour |
|---|---|---|
| `box-sizing` | `content-box` | Default. Width = content only. Padding + border are extra. |
| `box-sizing` | `border-box` | Width = content + padding + border. Element stays declared size. |
