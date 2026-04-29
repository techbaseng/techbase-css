---
render_with_liquid: false
title: "CSS Rounded Corners"
nav_order: 46
---

# Lesson 46 — CSS Rounded Corners

---

## Lesson Introduction

Have you ever noticed how buttons on apps, profile pictures on social media, and notification cards on websites all have soft, smooth, rounded edges instead of harsh, sharp corners? That polished look comes from a single, powerful CSS property: **`border-radius`**.

In this lesson you will learn exactly what `border-radius` is, why it exists, how it works, and how to use it with complete control — from making one corner round to creating a perfect circle out of a square, to making fancy asymmetrical "pill" shapes.

By the end of this lesson, you will be able to:

- Understand what `border-radius` does and why designers love it
- Apply rounded corners to any HTML element
- Control each corner individually
- Use the shorthand to write compact code
- Create circles, pills, and ellipses with only CSS
- Solve code challenges using `border-radius`
- Build a mini profile card mini-project

No prior CSS experience with rounded corners is needed — we will build from zero.

---

## Prerequisite Concepts

Before jumping in, make sure you understand these basic ideas. If any of them are new to you, read the short explanation provided before continuing.

### What is an HTML element?

An HTML element is anything you put on a webpage — a box of text (`<div>`), a paragraph (`<p>`), an image (`<img>`), a button (`<button>`), and so on. Every element takes up a rectangular space on the page.

### What is CSS?

CSS stands for **Cascading Style Sheets**. It is the language you use to control how HTML elements look — their colours, sizes, fonts, spacing, and shape.

### What is a CSS property?

A CSS property is an instruction you give to the browser. For example:

```css
color: red;
```

This tells the browser: "Make the text colour red."

### What is a CSS value?

A value is the *specific setting* you give to a property. In `color: red`, the value is `red`. Values can be colours, numbers, percentages, keywords, and more.

### What is a pixel (px)?

A pixel is a tiny unit of measurement on screens. `25px` means "25 pixels." The more pixels, the bigger the size. A typical laptop screen is about 1920 pixels wide.

---

## Part 1 — Conceptual Understanding

### What is `border-radius`?

Imagine taking a plain rectangular piece of cardboard. The corners are sharp 90-degree points. Now imagine using scissors to clip each corner into a smooth curve. That is *exactly* what `border-radius` does in CSS — it clips the corners of an element's box to make them curved.

**`border-radius`** is a CSS property that defines the **radius of the curves** at the corners of an element.

> 📐 **Analogy:** Think of a circle. The "radius" of a circle is the distance from its centre to its edge. When you set `border-radius: 25px`, you are telling the browser to place an imaginary circle of radius 25px at each corner, and curve the corner to match that circle.

### Why does `border-radius` exist?

Before CSS3 (an upgrade to CSS released around 2011), creating rounded corners on a webpage required very complex tricks — developers had to use separate corner images, slice pictures, or write JavaScript. This was slow, hard to maintain, and fragile.

`border-radius` was introduced in CSS3 to solve this problem cleanly. With just one line of code, any element can have rounded corners.

### What elements can use `border-radius`?

`border-radius` works on any element that has one of the following:

- A **`background-color`** (a filled background)
- A **`border`** (a visible edge/stroke)
- A **`background-image`** (a picture as the background)

> 💡 **Think about it:** If an element has no visible background or border, `border-radius` still works but you may not be able to see the effect, because there is nothing being clipped visually.

### How does it work internally?

When you write:

```css
border-radius: 25px;
```

The browser draws an arc (a curved segment from a circle of radius 25px) at all four corners of the element's box. The greater the value, the more dramatic the curve.

---

## Part 2 — The `border-radius` Property in Detail

### Syntax

```css
selector {
  border-radius: value;
}
```

The `value` can be written as:

- **Pixels** — `10px`, `25px`, `50px`
- **Percentage** — `10%`, `25%`, `50%`

### Simple Example — One Value, All Four Corners

When you give `border-radius` a **single value**, it applies the same curve to **all four corners**.

```html
<!-- HTML -->
<div id="box1">Hello!</div>
```

```css
/* CSS */
#box1 {
  border-radius: 25px;
  background-color: #73AD21;
  width: 200px;
  height: 100px;
  padding: 20px;
}
```

**What this does:**
- `border-radius: 25px` — clips all four corners with a 25px curve
- `background-color: #73AD21` — gives the box a green background so you can see the shape
- `width` and `height` — define the box size
- `padding` — adds space between the text and the edge

**Expected visual output:**
```
╭──────────────────╮
│                  │
│      Hello!      │
│                  │
╰──────────────────╯
```
A green box with smooth rounded corners.

---

### The Property Works on Any Background Type

You do not need a solid colour background. `border-radius` also works on elements with:

**A border only (no fill):**

```html
<div id="box2">Rounded border!</div>
```

```css
#box2 {
  border-radius: 25px;
  border: 2px solid #73AD21;
  width: 200px;
  height: 100px;
  padding: 20px;
}
```

**Expected visual output:** A box with NO fill colour, only a visible green curved border/stroke around it.

---

**A background image:**

```html
<div id="box3">Image box!</div>
```

```css
#box3 {
  border-radius: 25px;
  background-image: url("paper.jpg");
  width: 200px;
  height: 100px;
  padding: 20px;
}
```

**Expected visual output:** The image inside the box is clipped so the corners are rounded — the image itself appears to have rounded corners.

> 💡 **Key insight:** `border-radius` clips the *visible boundary* of the element. Whatever is inside (colour, image, text) gets clipped at the rounded corners.

---

## Part 3 — Controlling Each Corner Individually

This is where `border-radius` becomes really powerful. You can round each corner by a *different amount*, which lets you create unique, custom shapes.

### The Four Corner Properties

Each corner of an element has its own property name:

| Property | Corner It Controls |
|---|---|
| `border-top-left-radius` | Top-left corner |
| `border-top-right-radius` | Top-right corner |
| `border-bottom-right-radius` | Bottom-right corner |
| `border-bottom-left-radius` | Bottom-left corner |

> 🗺️ **Corner map:**
> ```
> top-left ──────────── top-right
>    │                      │
>    │         BOX           │
>    │                      │
> bottom-left ──────── bottom-right
> ```

### Example — Different Radius Per Corner

```html
<div id="custom">Unique shape!</div>
```

```css
#custom {
  border-top-left-radius: 50px;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 50px;
  border-bottom-left-radius: 10px;
  background-color: #3498DB;
  width: 200px;
  height: 100px;
  padding: 20px;
  color: white;
}
```

**Line-by-line breakdown:**

- `border-top-left-radius: 50px` → Top-left corner gets a big, dramatic curve (50px)
- `border-top-right-radius: 10px` → Top-right corner gets a small, subtle curve (10px)
- `border-bottom-right-radius: 50px` → Bottom-right gets the same big curve
- `border-bottom-left-radius: 10px` → Bottom-left gets the small curve
- `background-color: #3498DB` → Blue background
- `color: white` → White text so it's readable on blue

**Expected visual output:**
```
╭────────────────────╮
│                    │
│   Unique shape!    │
│                    │
╰────────────────────╯
(left sides heavily curved, right sides slightly curved)
```

> 🤔 **Think about it:** What would happen if you set `border-top-left-radius: 0px`? The top-left corner would be a sharp 90-degree point while the others remain rounded.

---

## Part 4 — The `border-radius` Shorthand

Writing four separate properties every time would be tedious. CSS provides a **shorthand** — a way to write all four values in one line.

### Shorthand with 4 Values

```css
border-radius: top-left  top-right  bottom-right  bottom-left;
```

The values go **clockwise** starting from the **top-left** corner. Think of a clock: start at 10 o'clock (top-left), go to 2 o'clock (top-right), then 4 o'clock (bottom-right), then 8 o'clock (bottom-left).

```css
/* These two are exactly the same: */

/* Long version */
border-top-left-radius: 15px;
border-top-right-radius: 50px;
border-bottom-right-radius: 30px;
border-bottom-left-radius: 5px;

/* Shorthand version */
border-radius: 15px 50px 30px 5px;
```

> 🧠 **Memory trick:** **T**op-**L**eft → **T**op-**R**ight → **B**ottom-**R**ight → **B**ottom-**L**eft. You can remember this as "TL → TR → BR → BL" going clockwise.

### Full Example with 4-Value Shorthand

```html
<div id="shorthand-box">Shorthand!</div>
```

```css
#shorthand-box {
  border-radius: 15px 50px 30px 5px;
  background-color: #E74C3C;
  width: 200px;
  height: 100px;
  padding: 15px;
  color: white;
}
```

**Expected visual output:**
A red box where:
- Top-left: small curve (15px)
- Top-right: large curve (50px)
- Bottom-right: medium curve (30px)
- Bottom-left: very small curve (5px)

---

### Shorthand with 3 Values

```css
border-radius: top-left  top-right-AND-bottom-left  bottom-right;
```

Example:
```css
border-radius: 10px 25px 40px;
/* 
  top-left        = 10px
  top-right       = 25px (also applies to bottom-left)
  bottom-right    = 40px
  bottom-left     = 25px (same as top-right)
*/
```

---

### Shorthand with 2 Values

```css
border-radius: top-left-AND-bottom-right  top-right-AND-bottom-left;
```

Example:
```css
border-radius: 10px 40px;
/*
  top-left = bottom-right = 10px
  top-right = bottom-left = 40px
*/
```

This creates a shape that looks like it's tilted — the diagonal corners match.

---

### Shorthand with 1 Value

```css
border-radius: 25px;
/* All four corners = 25px */
```

This is the most common usage. All four corners get the same curve.

---

## Part 5 — Special Shapes with `border-radius`

One of the most exciting things about `border-radius` is that you can use it to create circles and "pill" shapes — without any images!

### How to Make a Perfect Circle

To make a circle, you need:
1. An element where `width` equals `height` (a square)
2. `border-radius: 50%`

Using 50% means the radius equals half of the element's size — which turns a square into a perfect circle.

```html
<div id="circle">Circle!</div>
```

```css
#circle {
  border-radius: 50%;
  background-color: #9B59B6;
  width: 150px;
  height: 150px;
  color: white;
  text-align: center;
  line-height: 150px; /* vertically centers text */
}
```

**Line-by-line:**
- `border-radius: 50%` → Rounds every corner by 50% of the element's size — creating a full circle
- `width: 150px; height: 150px` → Must be equal to make a circle (not oval)
- `line-height: 150px` → A trick to vertically center text by matching line height to box height

**Expected visual output:**
```
   ╭──────╮
  ╱        ╲
 │  Circle!  │
  ╲        ╱
   ╰──────╯
```
A perfect purple circle.

> 🌟 **Real-world use:** Profile pictures on social media (Twitter, LinkedIn, Facebook) are squares in the code, made to look circular using `border-radius: 50%`.

---

### How to Make a Pill Shape (Ellipse / Capsule)

A pill shape (also called a capsule) is a rectangle with fully rounded left and right sides. You often see this on buttons.

```html
<div id="pill">I am a pill!</div>
```

```css
#pill {
  border-radius: 50px;  /* Large enough to fully round short sides */
  background-color: #1ABC9C;
  width: 250px;
  height: 60px;
  color: white;
  text-align: center;
  line-height: 60px;
  padding: 0 20px;
}
```

**Expected visual output:**
```
╭─────────────────────────╮
│       I am a pill!       │
╰─────────────────────────╯
```

The trick: the height is `60px` and the `border-radius` is `50px` — since the radius is close to or greater than half the height, the short ends become fully curved into semicircles.

> 💡 **Tip:** You can also use `border-radius: 999px` for a guaranteed pill shape at any size, because an extremely large radius will always create full semicircle ends on shorter sides.

---

### Creating an Ellipse (Oval)

If you use `border-radius: 50%` on a **non-square** element (where width ≠ height), you get an oval/ellipse.

```html
<div id="ellipse">Oval</div>
```

```css
#ellipse {
  border-radius: 50%;
  background-color: #E67E22;
  width: 300px;
  height: 100px;
  color: white;
  text-align: center;
  line-height: 100px;
}
```

**Expected visual output:**
```
   ╭─────────────────────╮
  ╱                        ╲
 │          Oval             │
  ╲                        ╱
   ╰─────────────────────╯
```
A wide, flat orange oval.

> 🤔 **Think about it:** What happens to the shape if you change `height` from 100px to 200px while keeping `width: 300px`? The oval becomes more circular as the aspect ratio approaches 1:1.

---

## Part 6 — Percentage Values vs. Pixel Values

`border-radius` accepts both `px` (pixel) values and `%` (percentage) values. Understanding the difference is important.

### Pixel values (`px`)

Fixed and absolute. `border-radius: 20px` always creates a curve with a 20px radius, no matter how big or small the element is.

```css
/* A small box and a large box both get a 20px curve */
.small-box { width: 50px; height: 50px; border-radius: 20px; }
.large-box { width: 500px; height: 500px; border-radius: 20px; }
```

On the small box, 20px is a large fraction of its size — it will look very round. On the large box, 20px is a tiny fraction — it will look almost square with just slightly clipped corners.

### Percentage values (`%`)

Relative to the element's size. `border-radius: 50%` always creates a curve equal to 50% of the element's dimensions — so it scales perfectly with the element.

```css
/* Both boxes become perfect circles */
.small-box { width: 50px; height: 50px; border-radius: 50%; }
.large-box { width: 500px; height: 500px; border-radius: 50%; }
```

> 📏 **Rule of thumb:**
> - Use `%` when you want the rounding to **scale** with the element (e.g., circles, responsive designs)
> - Use `px` when you want the rounding to stay a **fixed size** regardless of element dimensions (e.g., button corners, card corners)

---

## Part 7 — The `border-radius` CSS Reference Table

Here is a complete reference for everything you can do with `border-radius`:

| Property | Description | Example |
|---|---|---|
| `border-radius` | Shorthand for all corners | `border-radius: 10px 25px 10px 25px` |
| `border-top-left-radius` | Top-left corner only | `border-top-left-radius: 20px` |
| `border-top-right-radius` | Top-right corner only | `border-top-right-radius: 5px` |
| `border-bottom-right-radius` | Bottom-right corner only | `border-bottom-right-radius: 20px` |
| `border-bottom-left-radius` | Bottom-left corner only | `border-bottom-left-radius: 5px` |

---

## Part 8 — Guided Practice Exercises

### Exercise 1 — Warm-Up: Simple Rounded Box

**Objective:** Apply `border-radius` to a simple div.

**Scenario:** You are styling a notification banner for a website. The banner must have a green background with rounded corners.

**Steps:**

1. Create an HTML file.
2. Add a `<div>` with the id `"notification"` and the text "You have a new message!".
3. In CSS, set:
   - `border-radius: 15px`
   - `background-color: #2ECC71` (a green colour)
   - `padding: 20px`
   - `width: 300px`
   - `color: white`

**Starter code:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    #notification {
      /* Add your styles here */
    }
  </style>
</head>
<body>
  <div id="notification">You have a new message!</div>
</body>
</html>
```

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    #notification {
      border-radius: 15px;
      background-color: #2ECC71;
      padding: 20px;
      width: 300px;
      color: white;
    }
  </style>
</head>
<body>
  <div id="notification">You have a new message!</div>
</body>
</html>
```

**Expected output:**
```
╭────────────────────────────╮
│  You have a new message!   │
╰────────────────────────────╯
```
A green box with smooth rounded corners and white text inside.

**Self-check questions:**
- What would happen if you changed `border-radius: 15px` to `border-radius: 100px`?
- What if you removed the `background-color`? Would you still see the rounded shape?

---

### Exercise 2 — Individual Corners

**Objective:** Round different corners by different amounts.

**Scenario:** You are creating a stylised "speech bubble" shape. The box should have one very sharp corner (pointing at the speaker) and three rounded corners.

**Steps:**

1. Create a div with id `"bubble"` and text `"Hello there!"`.
2. Apply these individual corner radii:
   - Top-left: `30px`
   - Top-right: `30px`
   - Bottom-right: `30px`
   - Bottom-left: `0px` (sharp — the "tail" of the bubble)
3. Add `background-color: #3498DB`, `color: white`, `padding: 20px`, `width: 200px`.

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    #bubble {
      border-top-left-radius: 30px;
      border-top-right-radius: 30px;
      border-bottom-right-radius: 30px;
      border-bottom-left-radius: 0px;
      background-color: #3498DB;
      color: white;
      padding: 20px;
      width: 200px;
    }
  </style>
</head>
<body>
  <div id="bubble">Hello there!</div>
</body>
</html>
```

**Expected output:**
```
╭──────────────────╮
│                  │
│   Hello there!   │
│                  │
└──────────────────╯
```
(Top and bottom-right corners curved; bottom-left is a sharp point)

**Self-check questions:**
- Can you rewrite this using the shorthand `border-radius` with 4 values?
- What values would you use?

> **Hint:** `border-radius: 30px 30px 30px 0px;`

---

### Exercise 3 — The Shorthand Challenge

**Objective:** Read shorthand values and predict the shape.

**Scenario:** A colleague gave you this CSS. Before testing it in the browser, predict what each corner looks like.

```css
#mystery-box {
  border-radius: 10px 60px 10px 60px;
  background-color: #E74C3C;
  width: 200px;
  height: 100px;
}
```

**Your predictions:**
- Top-left corner: `___px`
- Top-right corner: `___px`
- Bottom-right corner: `___px`
- Bottom-left corner: `___px`

**Answers:**
- Top-left: `10px` (small curve)
- Top-right: `60px` (large curve)
- Bottom-right: `10px` (small curve)
- Bottom-left: `60px` (large curve)

The box will have a distinctive "wave-like" or "S-curve" appearance because the opposing diagonal corners alternate between small and large curves.

---

### Exercise 4 — Create a Circle Button

**Objective:** Use `border-radius: 50%` with a perfect square to create a circular button.

**Scenario:** You are building a floating action button (FAB) like the round "+" buttons in mobile apps.

**Steps:**

1. Create a `<button>` element with the text `"+"`.
2. Set:
   - `width: 60px`
   - `height: 60px`
   - `border-radius: 50%`
   - `background-color: #E74C3C`
   - `color: white`
   - `font-size: 30px`
   - `border: none`
   - `cursor: pointer`

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    #fab-button {
      width: 60px;
      height: 60px;
      border-radius: 50%;
      background-color: #E74C3C;
      color: white;
      font-size: 30px;
      border: none;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <button id="fab-button">+</button>
</body>
</html>
```

**Expected output:** A perfectly circular red button with a white "+" symbol in the centre.

**Professional use case:** This exact pattern is used in Google Material Design for the "Floating Action Button" seen in Android apps and web apps like Gmail, Google Drive, and Google Maps.

---

## Part 9 — Code Challenges (Based on W3Schools Challenges)

These challenges directly reflect the types of exercises from the W3Schools CSS Rounded Corners Code Challenge page. Try each one, then check the solution.

### Challenge 1 — Add Rounded Corners

**Task:** Give the `<div>` below a `border-radius` of `25px`.

```html
<div style="background-color:#73AD21; width:200px; height:100px; padding:20px;">
  I am a div element.
</div>
```

**Your job:** Add one CSS property to this div.

**Solution:**

```html
<div style="background-color:#73AD21; width:200px; height:100px; padding:20px; border-radius:25px;">
  I am a div element.
</div>
```

**Expected output:** A green box with all four corners rounded by 25 pixels.

---

### Challenge 2 — Only Top-Left Corner

**Task:** Make only the **top-left** corner of a div rounded with a value of `25px`. All other corners must stay sharp.

**Solution:**

```css
div {
  border-top-left-radius: 25px;
  background-color: #73AD21;
  width: 200px;
  height: 100px;
  padding: 20px;
}
```

**Expected output:**
```
╭────────────────────
│
│   I am a div.
│
└────────────────────
```
Only the top-left corner is rounded.

---

### Challenge 3 — Make an Ellipse

**Task:** Use `border-radius` to turn the div below into an ellipse (oval shape).

```html
<div style="background-color:#73AD21; width:300px; height:100px;">
</div>
```

**Solution:**

```html
<div style="background-color:#73AD21; width:300px; height:100px; border-radius:50%;">
</div>
```

**Expected output:** A wide green oval shape.

> 🔑 **Key:** `50%` applied to a non-square element always creates an oval. The wider the element, the more "stretched" the oval.

---

### Challenge 4 — Shorthand 4 Values

**Task:** Use the `border-radius` shorthand to set:
- Top-left: `15px`
- Top-right: `50px`
- Bottom-right: `30px`
- Bottom-left: `5px`

**Solution:**

```css
div {
  border-radius: 15px 50px 30px 5px;
  background-color: #73AD21;
  width: 200px;
  height: 100px;
  padding: 20px;
}
```

**Expected output:** A green box with four distinctly different corner curves. Top-right has the most dramatic curve (50px), bottom-left has the subtlest (5px).

---

## Part 10 — Mini-Project: Profile Card

Now let's combine everything you have learned into a realistic, professional-looking mini-project: a **profile card**.

Profile cards appear everywhere — on team pages, apps, dashboards, social media. They typically have a circular avatar, a name, a job title, and rounded card edges.

### Stage 1 — Setup: Basic Card Structure

**Preview:**

```html
<!DOCTYPE html>
<html>
<head>
  <title>Profile Card</title>
</head>
<body>
  <div class="card">
    <div class="avatar">AB</div>
    <h2>Ada Babbage</h2>
    <p>Frontend Developer</p>
    <button class="follow-btn">Follow</button>
  </div>
</body>
</html>
```

**Milestone output (no CSS yet):** Plain text content stacked vertically, no styling.

---

### Stage 2 — Card Container Styling

Now we style the card itself using `border-radius` to give it rounded corners.

```css
body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #F0F4F8;
  font-family: Arial, sans-serif;
}

.card {
  background-color: white;
  border-radius: 20px;          /* Rounded card corners */
  padding: 40px 30px;
  width: 260px;
  text-align: center;
  box-shadow: 0 4px 15px rgba(0,0,0,0.1);  /* subtle shadow */
}
```

**Line-by-line explanation of `.card`:**
- `background-color: white` → Card has a clean white background
- `border-radius: 20px` → All four corners of the card are rounded by 20px
- `padding: 40px 30px` → Space of 40px top/bottom, 30px left/right inside the card
- `width: 260px` → Fixed card width
- `text-align: center` → All text and elements centre-aligned
- `box-shadow` → A soft, blurry drop shadow below the card for depth

**Milestone output:** A white rounded card centred on a light grey page background.

---

### Stage 3 — Circular Avatar

```css
.avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;             /* Makes it a circle */
  background-color: #3498DB;
  color: white;
  font-size: 36px;
  font-weight: bold;
  line-height: 100px;             /* Vertically centres text */
  margin: 0 auto 20px auto;      /* Centres horizontally, adds space below */
}
```

**Line-by-line explanation:**
- `width: 100px; height: 100px` → Equal width and height = square
- `border-radius: 50%` → Turns the square into a **perfect circle**
- `background-color: #3498DB` → Blue background for the avatar
- `line-height: 100px` → Equals the height, centres "AB" text vertically
- `margin: 0 auto 20px auto` → `0` top, `auto` left and right (centres block), `20px` bottom gap

**Milestone output:** A circular blue avatar with initials "AB" inside, centred above the name.

---

### Stage 4 — Text Styling and Follow Button

```css
h2 {
  margin: 0 0 5px 0;
  font-size: 22px;
  color: #2C3E50;
}

p {
  color: #7F8C8D;
  font-size: 14px;
  margin: 0 0 20px 0;
}

.follow-btn {
  border-radius: 999px;           /* Pill shape button */
  background-color: #3498DB;
  color: white;
  border: none;
  padding: 10px 30px;
  font-size: 15px;
  cursor: pointer;
  font-weight: bold;
}

.follow-btn:hover {
  background-color: #2980B9;     /* Slightly darker on hover */
}
```

**Line-by-line explanation of `.follow-btn`:**
- `border-radius: 999px` → An extremely large value that always creates a full pill/capsule shape regardless of button size
- `background-color: #3498DB` → Blue button
- `border: none` → Removes the default button border
- `padding: 10px 30px` → Comfortable click area
- `cursor: pointer` → Shows a hand cursor on hover, signalling it's clickable

---

### Stage 5 — Final Complete Code

Put it all together:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Profile Card</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      background-color: #F0F4F8;
      font-family: Arial, sans-serif;
    }

    .card {
      background-color: white;
      border-radius: 20px;
      padding: 40px 30px;
      width: 260px;
      text-align: center;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
    }

    .avatar {
      width: 100px;
      height: 100px;
      border-radius: 50%;
      background-color: #3498DB;
      color: white;
      font-size: 36px;
      font-weight: bold;
      line-height: 100px;
      margin: 0 auto 20px auto;
    }

    h2 {
      margin: 0 0 5px 0;
      font-size: 22px;
      color: #2C3E50;
    }

    p {
      color: #7F8C8D;
      font-size: 14px;
      margin: 0 0 20px 0;
    }

    .follow-btn {
      border-radius: 999px;
      background-color: #3498DB;
      color: white;
      border: none;
      padding: 10px 30px;
      font-size: 15px;
      cursor: pointer;
      font-weight: bold;
    }

    .follow-btn:hover {
      background-color: #2980B9;
    }
  </style>
</head>
<body>
  <div class="card">
    <div class="avatar">AB</div>
    <h2>Ada Babbage</h2>
    <p>Frontend Developer</p>
    <button class="follow-btn">Follow</button>
  </div>
</body>
</html>
```

**Expected final visual output:**
```
  ┌─────────────────────────────┐
  │                             │
  │          ╭──────╮           │
  │         │  AB  │           │
  │          ╰──────╯           │
  │                             │
  │       Ada Babbage           │
  │    Frontend Developer       │
  │                             │
  │    ╭──────────────────╮     │
  │    │     Follow       │     │
  │    ╰──────────────────╯     │
  │                             │
  └─────────────────────────────┘
```
A polished profile card with:
- Rounded card corners (20px)
- Circular avatar (border-radius: 50%)
- Pill-shaped follow button (border-radius: 999px)

---

### Reflection Questions for the Mini-Project

1. What would happen to the avatar if you changed `width` to `150px` but kept `height: 100px`? (Hint: it would no longer be a circle...)
2. How would you change the card to have sharp corners on the bottom and rounded corners only on the top?
3. Can you change the card to have a blue gradient background instead of white?
4. What value of `border-radius` would turn the "Follow" button into a rectangle?

> **Optional extension:** Add a second card for another person. Try giving the second card a `border-radius: 0` to see the contrast between rounded and sharp corners side by side.

---

## Part 11 — Common Beginner Mistakes

### Mistake 1 — Forgetting to set equal width and height for circles

❌ **Wrong:**
```css
.circle {
  border-radius: 50%;
  width: 200px;
  height: 100px; /* not equal to width! */
}
```

**Result:** An oval, not a circle. CSS cannot create a circle if the element is not square.

✅ **Correct:**
```css
.circle {
  border-radius: 50%;
  width: 150px;
  height: 150px; /* equal to width */
}
```

---

### Mistake 2 — Wrong shorthand order

❌ **Wrong (assuming clockwise but starting wrong):**
```css
/* Intended: top-right=50px, others=10px */
border-radius: 50px 10px 10px 10px; /* This makes TOP-LEFT=50px */
```

✅ **Correct:**
```css
/* Shorthand order: top-left, top-right, bottom-right, bottom-left */
border-radius: 10px 50px 10px 10px; /* NOW top-right=50px */
```

> 🔑 **Reminder:** The order is always **clockwise starting from top-left**.

---

### Mistake 3 — Using `border-radius` without a visible background or border

❌ **Wrong:**
```css
p {
  border-radius: 20px;
  /* No background-color, no border — nothing to round! */
}
```

**Result:** No visible change because there is nothing to clip.

✅ **Correct:**
```css
p {
  border-radius: 20px;
  background-color: #ECF0F1; /* Now there's something to round */
  padding: 10px;
}
```

---

### Mistake 4 — Typos in the property name

❌ **Common typos:**
```css
border-radius-top: 10px;    /* WRONG - property doesn't exist */
top-left-radius: 10px;      /* WRONG - incorrect syntax */
```

✅ **Correct:**
```css
border-top-left-radius: 10px;   /* CORRECT - always "border-" first */
```

---

### Mistake 5 — Using percentage on a non-square for a circle

❌ **Wrong (expecting a circle):**
```css
.avatar {
  border-radius: 50%;
  width: 200px;
  height: 80px; /* Different from width */
}
```

**Result:** An oval/ellipse, not a circle.

✅ **Correct:**
```css
.avatar {
  border-radius: 50%;
  width: 100px;
  height: 100px; /* Width = Height = Square → Circle */
}
```

---

## Part 12 — Real-World Use Cases

`border-radius` is one of the most frequently used CSS properties in professional web development:

**Profile pictures:** Social platforms use `border-radius: 50%` to turn square profile images into circles.

**Buttons:** Most modern UI buttons use `border-radius: 4px` to `border-radius: 999px` for a friendly, approachable look. Google's Material Design recommends `border-radius: 4px` for standard buttons.

**Cards and panels:** Dashboard panels, notification cards, and content cards typically use `border-radius: 8px` to `border-radius: 16px` for a modern, clean feel.

**Badges and tags:** Pill-shaped badges showing categories, statuses, or labels use `border-radius: 999px` for the capsule shape.

**Modal dialogs:** Popup windows and modals often use `border-radius: 12px` on the container for a friendly appearance.

**Input fields:** Form inputs sometimes use `border-radius: 4px` or `border-radius: 8px` for a softer look.

**Avatars in chat apps:** WhatsApp, Slack, and Teams use circular avatars created with `border-radius: 50%`.

---

## Reflection Questions

Take a moment to think through these questions. They will reinforce your understanding.

1. What is the difference between `border-radius: 50px` and `border-radius: 50%`?
2. If you wanted only the top two corners to be rounded and the bottom two sharp, what CSS would you write?
3. What value of `border-radius` would you use to make a perfect circle? What two conditions must the element meet?
4. In the shorthand `border-radius: 10px 20px`, which corners get `10px` and which get `20px`?
5. Why does `border-radius: 50%` on a `300px × 100px` div produce an oval instead of a circle?
6. If a button has `border-radius: 999px`, what shape does it become?
7. What is the shorthand to set all four corners individually using only one `border-radius` declaration?
8. Can you use `border-radius` on an element that has no background colour? What would happen?

---

## Completion Checklist

Before moving on to the next lesson, confirm you can do all of the following:

- [ ] Explain what `border-radius` does in plain language
- [ ] Apply a simple `border-radius` to any element using a pixel value
- [ ] Apply `border-radius` using a percentage value
- [ ] Set individual corners using the four individual corner properties
- [ ] Use the shorthand `border-radius` with 1, 2, 3, and 4 values correctly
- [ ] Create a perfect circle using `border-radius: 50%` on a square
- [ ] Create a pill/capsule shape button using `border-radius: 999px`
- [ ] Explain the difference between `px` values and `%` values for this property
- [ ] Identify and correct the most common `border-radius` mistakes
- [ ] Build a profile card using `border-radius` on the card, avatar, and button

---

## Lesson Summary

In this lesson, you mastered CSS Rounded Corners using the `border-radius` property.

Here is a quick recap of everything covered:

**The property:** `border-radius` curves the corners of any HTML element that has a visible background colour, border, or background image.

**Single value — all corners equal:**
```css
border-radius: 25px;
```

**Four individual corner properties:**
```css
border-top-left-radius: 10px;
border-top-right-radius: 20px;
border-bottom-right-radius: 30px;
border-bottom-left-radius: 40px;
```

**Shorthand (clockwise from top-left):**
```css
border-radius: 10px 20px 30px 40px;
```

**Make a circle (requires equal width and height):**
```css
border-radius: 50%;
```

**Make an oval (on a non-square element):**
```css
border-radius: 50%;
```

**Make a pill/capsule shape:**
```css
border-radius: 999px;
```

`border-radius` is a foundational CSS3 feature used in virtually every modern website and app. Mastering it gives you the power to create polished, professional UI elements with nothing but code — no images required.

---

*End of Lesson 46 — CSS Rounded Corners*
