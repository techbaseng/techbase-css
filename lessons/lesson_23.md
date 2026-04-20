---
render_with_liquid: false
title: "CSS z-index – Controlling the Stack Order of Elements"
nav_order: 23
---

# Lesson 23: CSS `z-index` — Controlling the Stack Order of Elements

---

## Lesson Introduction

Have you ever noticed how a dropdown menu appears on top of the rest of the page content? Or how a pop-up dialog box sits in front of everything else? Or how a "Back to Top" button floats visibly over images and text without disappearing behind them?

That visual "who is on top" behaviour is controlled by a CSS property called **`z-index`**.

In this lesson you will learn exactly what `z-index` is, why it exists, how it works, what rules control it, and how to use it confidently in real web pages. We will build up from the very basics to a realistic mini-project step by step, with every single concept explained and demonstrated with examples.

By the end of this lesson you will be able to:
- Understand how browsers stack elements on top of each other by default
- Use `z-index` to control which element appears "in front" of another
- Understand exactly when `z-index` works and when it does NOT work (and why)
- Recognise common beginner mistakes and fix them
- Apply `z-index` in realistic layouts like tooltips, overlays, modals, and sticky headers

---

## Prerequisite Concepts

Before we dive into `z-index`, you need to understand a few foundational ideas. If you already know these, feel free to skim — but even a quick refresh is helpful.

### What is CSS Positioning?

By default, HTML elements sit one after another on the page, flowing from top to bottom. This is called **normal document flow**.

But CSS has a property called `position` that lets you take elements out of that normal flow and place them wherever you like on the page. The `position` property has these values:

- `static` — The default. The element stays in normal flow. No special positioning.
- `relative` — The element stays in normal flow, but you can offset it from its original spot using `top`, `right`, `bottom`, `left`.
- `absolute` — The element is removed from normal flow and positioned relative to its nearest *positioned* ancestor (or to the `<body>` if there is none).
- `fixed` — The element is removed from normal flow and positioned relative to the browser window. It stays in place even when you scroll.
- `sticky` — A mix of `relative` and `fixed`. It acts like `relative` until you scroll past a certain point, then it sticks in place.

> **Why does this matter for z-index?** Because `z-index` ONLY works on positioned elements — that is, elements with `position` set to `relative`, `absolute`, `fixed`, or `sticky`. It does NOT work on `position: static` elements (the default).

### What is the Z-Axis?

Your screen has two visible dimensions:
- **X-axis** — going left and right (horizontal)
- **Y-axis** — going up and down (vertical)

But there is also a third dimension:
- **Z-axis** — going toward you and away from you (depth, or "in front of" vs "behind")

Although your screen is flat, browsers simulate this depth using a **stacking order** — deciding which element should appear "on top" when two elements occupy the same space on screen.

Think of it like stacking sheets of paper on a desk. The paper on top covers any paper underneath it. `z-index` lets you choose which "sheet" goes on top.

---

## Part 1: Conceptual Understanding — What is `z-index`?

### The Simple Explanation

`z-index` is a CSS property that controls the **stack order** of a positioned element. An element with a **higher** `z-index` value will appear **in front of** an element with a **lower** `z-index` value when they overlap.

**Syntax:**

```css
selector {
  position: relative; /* z-index requires a position value other than static */
  z-index: 1;         /* any whole number — positive, zero, or negative */
}
```

### The Real-Life Analogy

Imagine you have a stack of papers on a desk:
- Paper at the bottom of the stack is at the lowest level → `z-index: 1`
- Paper in the middle is → `z-index: 2`
- Paper on top, covering everything → `z-index: 3`

The paper with the highest `z-index` number is "closest to you" (on top). The one with the lowest number is "furthest from you" (at the bottom).

### Default Stacking — What Happens Without z-index

Without `z-index`, when two positioned elements overlap, the browser stacks them in the order they appear in the HTML. Elements that come **later** in the HTML sit **on top** of elements that come **earlier**.

**Example — Default HTML stacking order:**

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .box {
    width: 200px;
    height: 200px;
    position: absolute;
  }

  .box-one {
    background-color: coral;
    top: 50px;
    left: 50px;
  }

  .box-two {
    background-color: steelblue;
    top: 100px;   /* overlaps box-one */
    left: 100px;
  }
</style>
</head>
<body>

  <div class="box box-one">Box One (coral)</div>
  <div class="box box-two">Box Two (blue)</div>

</body>
</html>
```

**Expected Output:**
- Box One (coral) is drawn first.
- Box Two (blue) is drawn on top of it, partially covering it.
- The blue box appears "in front" of the coral box simply because it comes later in the HTML.

> **Thinking Prompt:** What would happen if you swapped the order of the two `<div>` elements in the HTML? Which box would appear on top?

---

## Part 2: Using `z-index` to Control Stack Order

### The Basic Rule

To give an element a `z-index`, you must first give it a `position` value that is NOT `static`. Then set `z-index` to any whole number.

```css
.element {
  position: relative; /* or absolute, fixed, or sticky */
  z-index: 10;
}
```

- **Higher number = in front**
- **Lower number = behind**
- **Negative numbers** are allowed — they place the element behind even normal (non-positioned) content

### Simple Example — z-index in action

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .box {
    width: 200px;
    height: 200px;
    position: absolute;
  }

  .box-one {
    background-color: coral;
    top: 50px;
    left: 50px;
    z-index: 2;        /* higher number — this will be ON TOP */
  }

  .box-two {
    background-color: steelblue;
    top: 100px;
    left: 100px;
    z-index: 1;        /* lower number — this will be BEHIND */
  }
</style>
</head>
<body>

  <div class="box box-one">Box One (coral) z-index: 2</div>
  <div class="box box-two">Box Two (blue) z-index: 1</div>

</body>
</html>
```

**Expected Output:**
- Even though Box Two comes AFTER Box One in the HTML (and would normally be on top), the `z-index` values override that default.
- Box One (coral) now appears ON TOP because its `z-index: 2` is greater than `z-index: 1`.

> **Key Insight:** `z-index` overrides the default HTML source-order stacking. Higher number = winner.

### Example 2 — Three Overlapping Elements

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .box {
    width: 150px;
    height: 150px;
    position: absolute;
    color: white;
    font-size: 18px;
    padding: 10px;
  }

  #red {
    background-color: crimson;
    top: 40px;
    left: 40px;
    z-index: 1;
  }

  #green {
    background-color: seagreen;
    top: 80px;
    left: 80px;
    z-index: 3;    /* HIGHEST — will be on top */
  }

  #blue {
    background-color: steelblue;
    top: 120px;
    left: 120px;
    z-index: 2;
  }
</style>
</head>
<body>

  <div id="red">Red (z:1)</div>
  <div id="green">Green (z:3)</div>
  <div id="blue">Blue (z:2)</div>

</body>
</html>
```

**Expected Output:**
- Green box is fully visible on top (z-index: 3 — highest)
- Blue box is in the middle (z-index: 2)
- Red box is at the bottom, mostly covered (z-index: 1 — lowest)

> **Thinking Prompt:** What would happen if you changed the green box's `z-index` from `3` to `-1`? Try to guess before experimenting.

---

## Part 3: The Critical Rule — z-index Only Works with Positioned Elements

This is the most important rule beginners overlook, and it causes a lot of confusion.

### The Rule

`z-index` has **no effect** on an element with `position: static` (the default position value).

```css
/* This does NOTHING — static is the default */
.box {
  z-index: 999;   /* ignored completely because position is static by default */
}

/* This WORKS */
.box {
  position: relative;   /* now z-index is respected */
  z-index: 999;
}
```

### Why Does This Rule Exist?

CSS's stacking mechanism only activates for elements that have been "taken out of" or "placed in" a specific layer context. Elements with `position: static` are just in the normal document flow — they don't participate in the z-axis stacking game at all.

Think of it this way: normal flow elements are like furniture sitting on the floor of a room. Positioned elements are like objects you've picked up and are holding at different heights. Only the objects you're holding can be at different heights — the furniture on the floor is just on the floor.

### Demonstration of the Rule

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .box {
    width: 200px;
    height: 200px;
  }

  .box-a {
    background-color: coral;
    /* position: static is the default — z-index won't work */
    z-index: 999;      /* This is IGNORED */
    margin-bottom: -50px;  /* just to cause overlap for demonstration */
  }

  .box-b {
    background-color: steelblue;
    position: relative;    /* THIS activates z-index */
    z-index: 1;
  }
</style>
</head>
<body>

  <div class="box box-a">Box A (static, z-index: 999 — IGNORED)</div>
  <div class="box box-b">Box B (relative, z-index: 1 — WORKS)</div>

</body>
</html>
```

**Expected Output:**
- Box B (blue) appears ON TOP of Box A (coral) despite Box A having `z-index: 999`.
- This is because Box A's `z-index` is ignored — it has no `position` value.
- Box B has `position: relative` so its `z-index: 1` IS respected.

> **Common Beginner Mistake:** Setting a high `z-index` but forgetting to set a `position` property — and then wondering why it doesn't work!

---

## Part 4: Stacking Context — The Advanced Rule

### What is a Stacking Context?

A **stacking context** is like a self-contained "arena" where elements compete against each other for position on the z-axis. Elements inside one stacking context cannot overlap elements in a different stacking context based on their individual `z-index` values — the entire context is treated as a single unit.

This can be confusing, but the analogy makes it clear:

**The Folder Analogy:**

Imagine you have two physical folders of papers on a desk:
- **Folder A** is the bottom folder.
- **Folder B** is placed on top of Folder A.

Inside Folder A, you can arrange the papers in any order you want using their own numbering system. Inside Folder B, the same. BUT, no matter how high you number a paper inside Folder A, it can NEVER appear above ANY paper inside Folder B — because the entire Folder A is underneath Folder B.

This is exactly how stacking contexts work in CSS.

### What Creates a New Stacking Context?

A new stacking context is created whenever an element has:
- `position` set to `absolute`, `relative`, `fixed`, or `sticky` AND a `z-index` value that is NOT `auto`
- `opacity` less than `1` (e.g., `opacity: 0.9`)
- `transform`, `filter`, `perspective`, or `clip-path` applied
- `will-change` set to certain values
- Being a flex or grid container child with a `z-index` that is not `auto`

For beginners, the most common cause is: **a positioned element with a specific `z-index` value creates a new stacking context for its children.**

### Stacking Context Example — The Trap

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .context-a {
    position: relative;
    z-index: 1;           /* Creates a new stacking context */
    background-color: lightcoral;
    width: 300px;
    height: 200px;
    padding: 10px;
  }

  .context-b {
    position: relative;
    z-index: 2;           /* context-b is ABOVE context-a */
    background-color: lightblue;
    width: 300px;
    height: 200px;
    margin-top: -100px;   /* overlap deliberately */
    padding: 10px;
  }

  .child-of-a {
    position: relative;
    z-index: 9999;        /* VERY high — but trapped inside context-a */
    background-color: gold;
    width: 150px;
    height: 80px;
  }
</style>
</head>
<body>

  <div class="context-a">
    Context A (z-index: 1)
    <div class="child-of-a">Child of A (z-index: 9999)</div>
  </div>

  <div class="context-b">
    Context B (z-index: 2) — I cover everything in Context A
  </div>

</body>
</html>
```

**Expected Output:**
- Context B (blue) covers Context A (coral) completely — including the gold "Child of A" box.
- Even though the child has `z-index: 9999`, it CANNOT escape its parent's stacking context.
- Context A as a whole is at `z-index: 1`, and Context B is at `z-index: 2`. So ALL of Context A's children, regardless of their own z-index values, sit below Context B.

> **Real World Analogy:** No matter how important a piece of paper in Folder A is, if Folder B is placed on top of Folder A on the desk, every piece of paper in Folder A is covered.

---

## Part 5: The `z-index: auto` Value

When you set `z-index: auto` (or don't set `z-index` at all on a positioned element), the element does NOT create a new stacking context. It participates in its parent's stacking context instead.

```css
.element {
  position: relative;
  z-index: auto;   /* same as not setting z-index — does NOT create a new stacking context */
}
```

vs.

```css
.element {
  position: relative;
  z-index: 0;   /* creates a new stacking context, even though the value is 0 */
}
```

This is a subtle difference. `z-index: 0` and `z-index: auto` behave similarly for the element itself, but `z-index: 0` creates a new stacking context while `z-index: auto` does not.

---

## Part 6: Negative z-index Values

You can use negative `z-index` values to push an element **behind** its parent or behind normal document flow content.

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .container {
    position: relative;
    background-color: lightgrey;
    width: 300px;
    height: 200px;
    padding: 20px;
  }

  .behind {
    position: absolute;
    z-index: -1;           /* pushed BEHIND the parent */
    background-color: tomato;
    width: 250px;
    height: 150px;
    top: 30px;
    left: 30px;
  }

  p {
    position: relative;    /* This text is above z-index: -1 */
    z-index: 0;
  }
</style>
</head>
<body>

  <div class="container">
    <p>This text is in normal flow inside the container.</p>
    <div class="behind">I am behind the container background (z-index: -1)</div>
  </div>

</body>
</html>
```

**Expected Output:**
- The red `.behind` box is pushed behind the grey container's background.
- The paragraph text sits in front of everything.
- The red box is barely visible (or not at all) peeking out from behind the grey container.

**Practical Use Case for Negative z-index:**
- Placing a decorative background shape behind the main content
- Creating a "watermark" effect
- Building layered backgrounds without extra wrapper elements

---

## Part 7: CSS `z-index` Property Reference

Here is a complete reference of all valid values for the `z-index` property:

| Value | What It Does |
|---|---|
| `auto` | Default. The element's stack level is 0. Does NOT create a new stacking context. |
| Any positive integer (e.g., `1`, `5`, `100`) | Places the element higher in the stack than elements with lower values. Creates a new stacking context. |
| `0` | Stack level is 0. Creates a new stacking context. |
| Any negative integer (e.g., `-1`, `-5`) | Places the element below elements with a value of 0 or higher. |
| `inherit` | Inherits the `z-index` value from the parent element. |
| `initial` | Resets to the default value (`auto`). |

---

## Part 8: Guided Practice Exercises

### Exercise 1 — Basic Stack Control (Warm-Up)

**Objective:** Make the green box appear on top of the red box.

**Scenario:** You have two overlapping coloured boxes. By default the red one appears on top. Use `z-index` to reverse this so green is on top.

**Starter Code:**

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .box {
    width: 200px;
    height: 200px;
    position: absolute;
  }

  #red-box {
    background-color: crimson;
    top: 20px;
    left: 20px;
    /* Add z-index here */
  }

  #green-box {
    background-color: seagreen;
    top: 70px;
    left: 70px;
    /* Add z-index here */
  }
</style>
</head>
<body>
  <div id="red-box">Red Box</div>
  <div id="green-box">Green Box</div>
</body>
</html>
```

**Steps:**
1. Add `z-index: 1` to `#red-box`.
2. Add `z-index: 2` to `#green-box`.
3. Save and open in a browser.
4. Green should now sit on top of red.

**Expected Output:** Green box fully visible, covering part of the red box.

**Solution:**

```css
#red-box {
  background-color: crimson;
  top: 20px;
  left: 20px;
  z-index: 1;
}

#green-box {
  background-color: seagreen;
  top: 70px;
  left: 70px;
  z-index: 2;  /* higher = on top */
}
```

**Self-Check Questions:**
- What would happen if both boxes had `z-index: 1`? (The HTML source order would decide — green appears on top since it comes later.)
- What would happen if you removed `position: absolute` from both boxes and kept the z-index values? (z-index would stop working — it requires a positioned element.)

---

### Exercise 2 — Tooltip Overlay

**Objective:** Create a tooltip that appears in front of nearby text and images.

**Scenario:** You have a word on a page with a tooltip. When you hover over the word, the tooltip box must appear in front of everything else on the page.

**Starter Code:**

```html
<!DOCTYPE html>
<html>
<head>
<style>
  body {
    font-family: Arial, sans-serif;
    padding: 40px;
  }

  .tooltip-container {
    display: inline-block;
    position: relative;   /* needed so the tooltip can be positioned relative to this */
  }

  .tooltip-trigger {
    background-color: steelblue;
    color: white;
    padding: 5px 10px;
    border-radius: 4px;
    cursor: pointer;
  }

  .tooltip-box {
    display: none;           /* hidden by default */
    position: absolute;
    top: -50px;
    left: 0;
    background-color: #333;
    color: white;
    padding: 8px 12px;
    border-radius: 4px;
    white-space: nowrap;
    /* Add z-index here to ensure it appears over everything */
  }

  .tooltip-container:hover .tooltip-box {
    display: block;          /* show on hover */
  }

  .overlap-box {
    background-color: lightcoral;
    padding: 20px;
    margin-top: -10px;       /* deliberately overlapping to test z-index */
    position: relative;
    z-index: 5;
  }
</style>
</head>
<body>

  <div class="overlap-box">
    This red box has z-index: 5 — it might cover the tooltip if z-index is wrong!
  </div>

  <div class="tooltip-container">
    <span class="tooltip-trigger">Hover over me</span>
    <div class="tooltip-box">I am the tooltip!</div>
  </div>

</body>
</html>
```

**Steps:**
1. Hover over the "Hover over me" button.
2. The tooltip may appear behind the red box.
3. Add `z-index: 10` to `.tooltip-box`.
4. Hover again — the tooltip should now appear in front of the red box.

**Expected Output:** Tooltip box appears clearly in front of the red overlap box.

**Solution Addition:**
```css
.tooltip-box {
  /* ... existing styles ... */
  z-index: 10;   /* higher than the overlap-box's z-index: 5 */
}
```

---

### Exercise 3 — Background Decoration with Negative z-index

**Objective:** Place a large decorative circle BEHIND a content card.

**Scenario:** A profile card has a decorative coloured circle in the background. The circle should sit behind the card text.

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .card {
    position: relative;
    width: 280px;
    background-color: white;
    border-radius: 12px;
    padding: 30px;
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    overflow: hidden;
    margin: 60px auto;
  }

  .card-content {
    position: relative;
    z-index: 1;   /* sits above the decoration */
  }

  .background-circle {
    position: absolute;
    width: 200px;
    height: 200px;
    border-radius: 50%;
    background-color: lightblue;
    top: -60px;
    right: -60px;
    z-index: -1;   /* pushed behind the card content */
  }

  h2 { margin: 0 0 10px 0; }
  p  { color: #555; }
</style>
</head>
<body>

  <div class="card">
    <div class="background-circle"></div>
    <div class="card-content">
      <h2>Jane Doe</h2>
      <p>Web Developer</p>
      <p>Lagos, Nigeria</p>
    </div>
  </div>

</body>
</html>
```

**Expected Output:**
- A white card with text (name, role, location) clearly visible.
- A soft blue decorative circle visible in the top-right corner, sitting BEHIND the text content.

**Self-Check Questions:**
- What happens if you change `.background-circle`'s `z-index` from `-1` to `2`? (It would cover the text.)
- What if you remove the `z-index: 1` from `.card-content`? Would the text still show? (Yes, because the circle is at `-1` which is below everything by default.)

---

## Part 9: Mini Project — Image Gallery with Overlay Caption

In this mini-project you will build a photo gallery card. When a user hovers over an image card, a dark overlay with a caption appears on top of the image. This is a very common design pattern seen on portfolio sites, e-commerce pages, and news sites.

### Stage 1: Setup — The Card Structure

Create the basic HTML structure:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Image Gallery with z-index Overlay</title>
  <link rel="stylesheet" href="gallery.css">
</head>
<body>

  <div class="gallery">

    <div class="card">
      <img src="https://picsum.photos/seed/nature/300/200" alt="Nature">
      <div class="overlay">
        <p class="caption">Beautiful Nature</p>
      </div>
    </div>

    <div class="card">
      <img src="https://picsum.photos/seed/city/300/200" alt="City">
      <div class="overlay">
        <p class="caption">City Lights</p>
      </div>
    </div>

    <div class="card">
      <img src="https://picsum.photos/seed/ocean/300/200" alt="Ocean">
      <div class="overlay">
        <p class="caption">Ocean Views</p>
      </div>
    </div>

  </div>

</body>
</html>
```

**Milestone Output:** Three image cards side by side (no styling yet).

---

### Stage 2: Core CSS — Positioning and z-index

Create `gallery.css`:

```css
/* Reset and body */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #1a1a2e;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  font-family: Arial, sans-serif;
}

/* Gallery layout */
.gallery {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
  justify-content: center;
  padding: 30px;
}

/* Each card */
.card {
  position: relative;       /* REQUIRED — makes this the anchor for absolute children */
  width: 300px;
  height: 200px;
  border-radius: 10px;
  overflow: hidden;          /* clips the overlay to the card shape */
  cursor: pointer;
}

/* The image */
.card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  z-index: 1;               /* image is at layer 1 */
  position: relative;       /* activates z-index for the img */
}

/* The overlay — dark semi-transparent cover */
.overlay {
  position: absolute;        /* positioned inside the card */
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6);  /* semi-transparent black */
  z-index: 2;               /* ABOVE the image (z-index: 1) */
  opacity: 0;               /* invisible by default */
  transition: opacity 0.3s ease;  /* smooth fade in */
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Show overlay on hover */
.card:hover .overlay {
  opacity: 1;               /* becomes visible on hover */
}

/* Caption text */
.caption {
  color: white;
  font-size: 18px;
  font-weight: bold;
  text-align: center;
  z-index: 3;               /* above the overlay */
}
```

**Milestone Output:**
- Three image cards with photos visible.
- When you hover over any card, a dark semi-transparent overlay smoothly fades in on top of the image.
- A white caption text appears on the overlay.

---

### Stage 3: Enhancements — "Featured" Badge

Add a "Featured" badge in the top-right corner of the first card that always stays visible (in front of everything):

**Add to HTML (first card only):**
```html
<div class="card">
  <img src="https://picsum.photos/seed/nature/300/200" alt="Nature">
  <div class="overlay">
    <p class="caption">Beautiful Nature</p>
  </div>
  <span class="badge">Featured</span>   <!-- ADD THIS -->
</div>
```

**Add to CSS:**
```css
/* Featured badge — always visible on top */
.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: gold;
  color: #333;
  font-size: 12px;
  font-weight: bold;
  padding: 4px 10px;
  border-radius: 20px;
  z-index: 4;               /* HIGHEST z-index — above overlay (z:2) and caption (z:3) */
}
```

**Milestone Output:**
- The "Featured" badge is always visible on the first card.
- Even when you hover and the overlay appears, the badge still shows on top of the overlay.
- The z-index hierarchy is: image (1) → overlay (2) → caption (3) → badge (4).

---

### Stage 4: Reflection Questions

After completing the project, think through these questions:

1. Why does the `.card` need `position: relative`? What would happen if you removed it?
2. Why does the `.overlay` need `position: absolute`? What would happen if it were `position: relative`?
3. The badge has `z-index: 4`. What would happen if you gave it `z-index: 0` instead?
4. If you wanted to add a "blur" effect to the image on hover, and the blur was applied using `filter: blur(3px)` on the card — would this create a new stacking context? (Yes — `filter` creates a new stacking context.) How would that affect the overlay?

**Optional Advanced Extension:**
- Add a fourth card with a `z-index: 10` "SOLD OUT" stamp that appears over the entire card even during hover
- Create a lightbox effect: clicking a card makes a full-screen dark overlay appear over the entire page with the caption centred

---

## Part 10: Common Beginner Mistakes

### Mistake 1 — Setting z-index without a position property

**Wrong:**
```css
.my-element {
  z-index: 999;   /* IGNORED — no position set, defaults to static */
}
```

**Correct:**
```css
.my-element {
  position: relative;  /* or absolute, fixed, sticky */
  z-index: 999;        /* NOW it works */
}
```

**Why it happens:** Beginners set a high `z-index` and wonder why nothing changes. They forget that `z-index` has a prerequisite.

---

### Mistake 2 — Confused by stacking contexts (the "trapped child" bug)

**The Symptom:** You set a child element's `z-index` to 9999 but it still appears behind another element on the page.

**The Cause:** The child is inside a parent that has its own stacking context (because the parent has a `z-index` value). The child is "trapped" inside the parent's context and cannot escape above elements outside that context.

**Wrong (assuming child can escape parent):**
```css
.parent {
  position: relative;
  z-index: 1;
}
.child {
  position: relative;
  z-index: 9999; /* still trapped within the parent's z-index: 1 context */
}
.outside-element {
  position: relative;
  z-index: 2;   /* entire parent (with all its children) is BELOW this */
}
```

**Fix Option 1 — Raise the parent's z-index:**
```css
.parent {
  z-index: 3;  /* now parent (and all children) is above outside-element */
}
```

**Fix Option 2 — Move the child out of the parent if it needs to be above outside elements.**

---

### Mistake 3 — Using extremely high z-index values unnecessarily

**Wrong (common pattern):**
```css
.my-modal { z-index: 9999999; }
.my-tooltip { z-index: 99999; }
.my-dropdown { z-index: 9999; }
```

**Why it's a problem:** This becomes very hard to manage. When a new developer joins the project, they set `z-index: 99999999` to beat the existing values, and the numbers spiral out of control.

**Best Practice — Use a z-index scale:**
```css
/* Define a clear, manageable scale */
/* z-index: 1-9     → slightly elevated elements */
/* z-index: 10-99   → dropdowns, tooltips */
/* z-index: 100-999 → modals, overlays */
/* z-index: 1000+   → critical UI (cookie banners, chatbots) */

.dropdown   { z-index: 10;  }
.tooltip    { z-index: 20;  }
.modal      { z-index: 100; }
.modal-overlay { z-index: 99; }
```

---

### Mistake 4 — Forgetting that `opacity`, `transform`, and `filter` create stacking contexts

```css
/* This parent has opacity < 1, which creates a NEW stacking context */
.parent {
  opacity: 0.99;   /* Even 0.99 creates a stacking context! */
  /* No z-index set, but stacking context is still created */
}

.child {
  position: absolute;
  z-index: 999;   /* still trapped inside .parent's stacking context */
}
```

**Fix:** Be aware that `opacity`, `transform`, `filter`, `clip-path`, and `will-change` on a parent can trap children in a stacking context. If the parent doesn't need these on the same element, separate them.

---

### Mistake 5 — Removing `position` accidentally

```css
/* Developer adds z-index */
.header {
  position: fixed;
  z-index: 100;
}

/* Later, someone changes position by mistake */
.header {
  position: static;   /* THIS removes z-index functionality! */
  z-index: 100;       /* now ignored */
}
```

**Fix:** Always check that `position` is set correctly when `z-index` stops working.

---

## Reflection Questions

Take a moment to think through these questions before moving on. They will solidify your understanding.

1. You have an element with `position: absolute` and `z-index: 5`. Its sibling has `position: relative` and `z-index: 3`. Which one appears on top? Why?

2. A `<div>` has `position: relative` and `z-index: 2`. Inside that `<div>`, there is a `<span>` with `position: absolute` and `z-index: 999`. A separate `<div>` on the page has `position: relative` and `z-index: 3`. Will the `<span>` appear above or below the second `<div>`? Explain why.

3. You add `transform: rotate(0deg)` to a container element (a transformation that visually does nothing). But suddenly, all the `z-index` values on children stop working as expected. Why? (Hint: think about what `transform` does to stacking context.)

4. A beginner sets a `<nav>` bar to `z-index: 1` with `position: fixed`. A modal dialog uses `z-index: 100`. But the nav bar appears on top of the modal. What might be causing this?

5. What is the difference between `z-index: 0` and `z-index: auto`?

---

## Completion Checklist

Before you consider this lesson complete, make sure you can honestly tick each item below:

- [ ] I can explain what the z-axis is and what "stack order" means in CSS
- [ ] I know that `z-index` only works on positioned elements (not `position: static`)
- [ ] I can set `z-index` to control which element appears in front of another
- [ ] I understand that higher `z-index` values appear in front of lower values
- [ ] I know that negative `z-index` values push elements behind their parent/normal flow
- [ ] I can explain what a stacking context is and when a new one is created
- [ ] I understand that a child element cannot escape its parent's stacking context
- [ ] I know that `opacity`, `transform`, and `filter` also create new stacking contexts
- [ ] I understand the difference between `z-index: 0` and `z-index: auto`
- [ ] I can identify the "forgot to set position" beginner mistake and fix it
- [ ] I completed the three guided exercises
- [ ] I built the image gallery mini-project using layered z-index values
- [ ] I can explain the z-index hierarchy in the mini-project (image → overlay → caption → badge)

---

## Lesson Summary

The `z-index` property in CSS controls the **depth order** of overlapping positioned elements — determining which element appears visually in front of others.

**The key rules to remember:**

`z-index` only works on elements that have `position` set to `relative`, `absolute`, `fixed`, or `sticky`. It has no effect on `position: static` elements.

Higher `z-index` values appear in front; lower values appear behind. Negative values push elements behind normal content.

Every positioned element with a specific `z-index` value creates a **stacking context** — a self-contained layer arena. Children inside a stacking context cannot escape above or below elements outside that context, regardless of their own `z-index` values.

In addition to `position + z-index`, other CSS properties like `opacity` (less than 1), `transform`, and `filter` also trigger new stacking contexts, which can unexpectedly trap children.

`z-index: auto` does NOT create a new stacking context; `z-index: 0` does.

**Real World Uses of z-index:**
- Dropdown menus appearing over page content
- Modal dialogs sitting above everything else on the page
- Tooltips floating above nearby text and images
- Sticky navigation bars staying above scrolling content
- Cookie consent banners appearing over the entire page
- Image overlay captions (as built in our mini-project)
- "Sold Out" stamps overlaid on product images
- Loading spinners floating above a page while data loads

Mastering `z-index` — especially stacking contexts — is one of the skills that separates a beginner CSS developer from a confident one. Keep practising by inspecting real websites in your browser's developer tools to see how professional developers use `z-index` in their layouts.
