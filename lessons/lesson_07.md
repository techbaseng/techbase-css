---
render_with_liquid: false
title: "CSS Borders — Style, Width, Colour, Sides, Shorthand & Rounded Corners"
nav_order: 7
---

# Lesson 07 — CSS Borders

## Border Style · Border Width · Border Colour · Individual Sides · Shorthand · Rounded Corners

---

## Lesson Introduction

Look at any well-designed webpage — notification boxes, profile cards, data tables, input fields, image frames, buttons. What separates one element visually from another? Very often it is a **border**.

A CSS border is a visible line that wraps around the outside of an HTML element. It sits between the element's **padding** (inner space) and its **margin** (outer space). Borders can be thick or thin, solid or dashed, a single colour or transparent. You can apply them to all four sides of an element at once, or you can style each side completely independently.

This lesson covers **every aspect of CSS borders** from scratch:

1. **Border Style** — what kind of line (solid, dashed, dotted, etc.)
2. **Border Width** — how thick the line is
3. **Border Colour** — what colour the line is
4. **Individual Sides** — targeting top, right, bottom, or left borders separately
5. **Shorthand** — combining all border settings into one compact line
6. **Rounded Corners** — using `border-radius` to create rounded or circular shapes

By the end you will be able to design and style borders for any element on any web page.

---

## What You Need to Know Before Starting

### What is an HTML Element?

An HTML element is a piece of content wrapped in tags. For example:

```html
<p>This is a paragraph.</p>
<div>This is a box.</div>
<h1>This is a heading.</h1>
```

Each of these elements can have a border placed around it using CSS.

### What is a CSS Property and Value?

A CSS declaration has two parts:

```css
property: value;
```

For example: `border-style: solid;` — `border-style` is the property, `solid` is the value.

### What is the CSS Box Model?

Every HTML element is treated by the browser as a rectangular box. That box has four layers from inside to outside:

```
┌───────────────────────────────────────┐
│               MARGIN                  │  ← outermost (space between elements)
│   ┌───────────────────────────────┐   │
│   │           BORDER              │   │  ← the visible line we are studying
│   │   ┌───────────────────────┐   │   │
│   │   │       PADDING         │   │   │  ← inner space between content and border
│   │   │   ┌───────────────┐   │   │   │
│   │   │   │   CONTENT     │   │   │   │  ← the actual text, image, etc.
│   │   │   └───────────────┘   │   │   │
│   │   └───────────────────────┘   │   │
│   └───────────────────────────────┘   │
└───────────────────────────────────────┘
```

In this lesson we focus entirely on the **BORDER** layer.

---

## Section 1 — Border Style (`border-style`)

### Why Border Style Must Come First

This is the most important rule about CSS borders that beginners frequently miss:

> **A border will not appear at all unless you set `border-style`.** Width and colour alone are invisible without a style being defined.

Think of it this way: before you can paint a fence (colour) or make it thick (width), the fence must actually exist (style). `border-style` is what creates the border.

### The `border-style` Property

`border-style` tells the browser what kind of line to draw. Here are all the available values:

| Value | What it draws |
|-------|---------------|
| `dotted` | A series of dots |
| `dashed` | A series of short dashes |
| `solid` | A single continuous straight line |
| `double` | Two parallel solid lines |
| `groove` | A carved-in 3D groove effect |
| `ridge` | The opposite of groove — raised 3D ridge |
| `inset` | Makes the element look sunken into the page |
| `outset` | Makes the element look raised out of the page |
| `none` | No border (default — the starting state of all elements) |
| `hidden` | No border, but reserves the space (used in tables) |

> **Analogy:** Think of these styles like different types of picture frames. A `solid` frame is a plain flat frame. A `double` frame is a double-matted frame. A `dashed` frame would be unusual in real life but common in web design for "drop zone" upload areas.

### Simple Example — All Border Styles Demonstrated

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      padding: 10px;
      margin: 8px 0;
    }

    .dotted  { border-style: dotted; }
    .dashed  { border-style: dashed; }
    .solid   { border-style: solid; }
    .double  { border-style: double; }
    .groove  { border-style: groove; }
    .ridge   { border-style: ridge; }
    .inset   { border-style: inset; }
    .outset  { border-style: outset; }
    .none    { border-style: none; }
    .hidden  { border-style: hidden; }
  </style>
</head>
<body>
  <p class="dotted">I have a dotted border.</p>
  <p class="dashed">I have a dashed border.</p>
  <p class="solid">I have a solid border.</p>
  <p class="double">I have a double border.</p>
  <p class="groove">I have a groove border.</p>
  <p class="ridge">I have a ridge border.</p>
  <p class="inset">I have an inset border.</p>
  <p class="outset">I have an outset border.</p>
  <p class="none">I have no border.</p>
  <p class="hidden">I have a hidden border.</p>
</body>
</html>
```

**Expected Output:**

```
[Paragraph with dotted outline]
[Paragraph with dashed outline]
[Paragraph with solid outline]
[Paragraph with double-line outline]
[Paragraph with sunken groove look]
[Paragraph with raised ridge look]
[Paragraph with sunken inset look]
[Paragraph with raised outset look]
[Paragraph — no visible border]
[Paragraph — no visible border]
```

> **Thinking prompt:** Which style would you use for a drag-and-drop file upload area to signal "drop your file here"? (Hint: dashed borders are the standard industry convention for this.)

---

### Multiple Styles on One Element — Controlling All Four Sides at Once

`border-style` can accept **one, two, three, or four values** at a time. Each number of values has a specific meaning:

#### One value — all four sides get the same style

```css
p { border-style: solid; }
/* Top: solid, Right: solid, Bottom: solid, Left: solid */
```

#### Two values — first applies to top & bottom, second to left & right

```css
p { border-style: dotted solid; }
/* Top: dotted, Bottom: dotted, Left: solid, Right: solid */
```

#### Three values — first=top, second=left & right, third=bottom

```css
p { border-style: dotted solid double; }
/* Top: dotted, Right: solid, Bottom: double, Left: solid */
```

#### Four values — each side gets its own value (top → right → bottom → left, clockwise)

```css
p { border-style: dotted solid double dashed; }
/* Top: dotted, Right: solid, Bottom: double, Left: dashed */
```

> **Memory trick for clockwise order:** Think of a clock — start at 12 (top), go to 3 (right), then 6 (bottom), then 9 (left). **T**op → **R**ight → **B**ottom → **L**eft = "**TRouBLe**" — a famous CSS memory aid!

---

## Section 2 — Border Width (`border-width`)

### What Is Border Width?

Once your border style exists, you can control **how thick or thin** it is using `border-width`. If you do not specify a width, the browser uses a default (usually `medium`, which is about 3px).

### How to Specify Width

Border width can be set in three ways:

**Using keywords:**
- `thin` — approximately 1px
- `medium` — approximately 3px (default)
- `thick` — approximately 5px

**Using pixel values (most precise):**
- `1px`, `2px`, `5px`, `10px`, etc.

**Using other CSS length units:**
- `em` (relative to font size), `rem`, `%`, etc. (less common for borders)

### Simple Example — Border Width Keywords

```css
p.thin   { border-style: solid; border-width: thin; }
p.medium { border-style: solid; border-width: medium; }
p.thick  { border-style: solid; border-width: thick; }
```

**Expected Output:**

```
[Thin solid outline — very fine line]
[Medium solid outline — moderate line]
[Thick solid outline — bold line]
```

### Simple Example — Border Width in Pixels

```css
p.one   { border-style: solid; border-width: 1px; }
p.four  { border-style: solid; border-width: 4px; }
p.ten   { border-style: solid; border-width: 10px; }
```

**Expected Output:**

```
[1px — very fine line, barely visible]
[4px — clearly visible line]
[10px — bold, thick frame around the paragraph]
```

### Multiple Values for Border Width (Same Rules as Style)

Just like `border-style`, `border-width` accepts 1, 2, 3, or 4 values with the same top→right→bottom→left logic:

```css
p { border-style: solid; border-width: 5px 10px; }
/* Top & Bottom: 5px | Left & Right: 10px */
```

```css
p { border-style: solid; border-width: 2px 8px 4px 12px; }
/* Top: 2px | Right: 8px | Bottom: 4px | Left: 12px */
```

> **Thinking prompt:** If you want a paragraph that looks like a card with a stronger emphasis on the left side (like a quotation), which side would you make thicker?

---

## Section 3 — Border Colour (`border-color`)

### What Is Border Colour?

`border-color` sets the colour of the border. You can use any valid CSS colour value:

- **Named colours:** `red`, `blue`, `green`, `navy`, `coral`, etc.
- **HEX codes:** `#ff0000` (red), `#0000ff` (blue), `#333333` (dark grey)
- **RGB values:** `rgb(255, 0, 0)` (red), `rgb(0, 128, 0)` (green)
- **HSL values:** `hsl(0, 100%, 50%)` (red), `hsl(120, 100%, 25%)` (dark green)
- **`transparent`:** Makes the border invisible but still takes up space

> **Important:** If `border-color` is not set, the border colour **inherits from the element's `color` property** (the text colour). This is a useful default — your borders will match your text colour automatically unless you override it.

### Simple Example — Named Colour

```css
p {
  border-style: solid;
  border-width: 3px;
  border-color: red;
}
```

**Expected Output:**

```
[Paragraph with a 3px solid red border on all four sides]
```

### Simple Example — Multiple Colour Values

`border-color` also follows the same 1–4 value rule:

```css
p {
  border-style: solid;
  border-width: 3px;
  border-color: red green blue yellow;
}
/* Top: red | Right: green | Bottom: blue | Left: yellow */
```

**Expected Output:**

```
[Paragraph with a different colour on each side: red top, green right, blue bottom, yellow left]
```

### Simple Example — HEX and RGB Colours

```css
/* Using a HEX colour */
div.hex {
  border-style: solid;
  border-width: 4px;
  border-color: #ff6347; /* tomato red */
}

/* Using an RGB colour */
div.rgb {
  border-style: solid;
  border-width: 4px;
  border-color: rgb(0, 128, 128); /* teal */
}

/* Using HSL */
div.hsl {
  border-style: solid;
  border-width: 4px;
  border-color: hsl(240, 100%, 50%); /* pure blue */
}
```

**Expected Output:**

```
[Box with a tomato-red border]
[Box with a teal border]
[Box with a pure blue border]
```

---

## Section 4 — Individual Border Sides

### The Problem: What If You Only Want One Side?

So far every example has styled all four sides. But in real web design, you often want to style sides independently. For example:

- A "bottom underline" heading: border on the bottom only
- A sidebar element with a coloured left accent: border on the left only
- A table cell with borders only on top and bottom

CSS provides dedicated properties for each side:

| Property | Side affected |
|----------|---------------|
| `border-top-style` | Top border |
| `border-right-style` | Right border |
| `border-bottom-style` | Bottom border |
| `border-left-style` | Left border |
| `border-top-width` | Top border width |
| `border-right-width` | Right border width |
| `border-bottom-width` | Bottom border width |
| `border-left-width` | Left border width |
| `border-top-color` | Top border colour |
| `border-right-color` | Right border colour |
| `border-bottom-color` | Bottom border colour |
| `border-left-color` | Left border colour |

### Example 1 — Bottom Border Only (Heading Underline Style)

```css
h2 {
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: navy;
}
```

**Expected Output:**

```
Heading Text
─────────────  ← navy underline
```

This is a very common, professional-looking design pattern for section headings.

### Example 2 — Left Accent Border (Blockquote Style)

```css
blockquote {
  border-left-style: solid;
  border-left-width: 5px;
  border-left-color: orange;
  padding-left: 15px;
  margin: 10px 0;
}
```

**Expected Output:**

```
│ "Design is not just what it looks like. Design is how it works."
```
(A thick orange bar on the left side with the text indented to the right)

This pattern is used on almost every blog and documentation site for highlighted quotations.

### Example 3 — Different Style on Every Side

```css
p {
  border-top-style: solid;
  border-right-style: dashed;
  border-bottom-style: dotted;
  border-left-style: double;

  border-top-color: red;
  border-right-color: green;
  border-bottom-color: blue;
  border-left-color: purple;

  border-top-width: 3px;
  border-right-width: 5px;
  border-bottom-width: 2px;
  border-left-width: 8px;

  padding: 10px;
}
```

**Expected Output:**

```
[Paragraph with:
  top — 3px solid red
  right — 5px dashed green
  bottom — 2px dotted blue
  left — 8px double purple]
```

> While this example is visually wild, it perfectly demonstrates that every single side can be controlled completely independently. In practice, you would use restraint — but knowing you can is important.

---

## Section 5 — Border Shorthand

### The Problem: Too Much Code

To style a simple solid border, the long way requires three separate declarations:

```css
p {
  border-style: solid;
  border-width: 3px;
  border-color: navy;
}
```

That is three lines for something very simple. CSS provides a **shorthand property** that collapses all three into a single line.

### The `border` Shorthand Property

```css
border: [width] [style] [color];
```

The three values are separated by spaces. Order matters: **width first, then style, then colour**.

```css
p {
  border: 3px solid navy;
}
```

This is exactly equivalent to:

```css
p {
  border-width: 3px;
  border-style: solid;
  border-color: navy;
}
```

> **Important:** `border-style` is the only **required** value in the shorthand. Width and colour are optional (they have defaults). But always include all three for clarity and predictability.

### Shorthand Examples

```css
/* Thin dotted red border */
p.example1 { border: 1px dotted red; }

/* Thick dashed blue border */
p.example2 { border: 6px dashed blue; }

/* Solid dark green border */
p.example3 { border: 2px solid darkgreen; }

/* Double thick orange border */
p.example4 { border: 8px double orange; }
```

**Expected Output:**

```
[Thin dotted red outline]
[Thick dashed blue outline]
[Thin solid dark green outline]
[Very thick double orange outline]
```

### Side-Specific Shorthand Properties

You can also use shorthand for individual sides. This is extremely useful and very common in real projects:

| Shorthand | Equivalent to |
|-----------|---------------|
| `border-top: 2px solid red;` | Sets top style, width, colour |
| `border-right: 4px dashed blue;` | Sets right style, width, colour |
| `border-bottom: 1px solid green;` | Sets bottom style, width, colour |
| `border-left: 5px solid orange;` | Sets left style, width, colour |

### Example — Side Shorthand in Practice

```css
h1 {
  border-bottom: 3px solid #333;
  padding-bottom: 8px;
}
```

**Expected Output:**

```
My Page Title
─────────────────────  ← 3px solid dark grey underline
```

This is one of the most commonly used CSS patterns in professional web development.

### Combining Global and Side-Specific Shorthand

A powerful technique is to set all four borders first, then override specific sides:

```css
div {
  border: 2px solid lightgrey;  /* Set all four sides */
  border-left: 5px solid blue;  /* Override just the left side */
}
```

**Expected Output:**

```
[Box with thin lightgrey border on top, right, and bottom, but a thick blue left border]
```

This pattern is heavily used in dashboards, sidebars, notification cards, and list items.

---

## Section 6 — Rounded Corners (`border-radius`)

### What Are Rounded Corners?

`border-radius` is a CSS property that **curves the corners** of an element's border box. Instead of sharp 90° corners, you get smooth curved corners — or even complete circles and pills.

This property works **even if there is no visible border**. You can use `border-radius` on a `div` with a coloured background and no border at all, and it will still round the corners.

> **Analogy:** Think of cutting the corners off a piece of paper. A small cut makes a slightly rounded corner. A big cut makes a very rounded corner. Cutting halfway through on all sides makes a circle.

### Basic Syntax

```css
element {
  border-radius: [value];
}
```

The value is a length (e.g. `px`, `em`) or a percentage (`%`).

- A **small value** (like `5px`) gives a subtle, gentle curve.
- A **large value** (like `30px`) gives a very pronounced curve.
- `50%` on a square element creates a **perfect circle**.
- Very large values on a rectangle (like `border-radius: 50px`) create a **pill/capsule** shape.

### Example 1 — Gentle Rounded Corners

```css
div.card {
  border: 2px solid navy;
  border-radius: 8px;
  padding: 20px;
  width: 200px;
}
```

**Expected Output:**

```
╭──────────────────────╮
│                      │
│   Some card content  │
│                      │
╰──────────────────────╯
```

(A box with gently rounded corners — very common for card components, modals, tooltips.)

### Example 2 — Highly Rounded (Pill/Capsule Shape)

```css
button.pill {
  border: 2px solid crimson;
  border-radius: 25px;
  padding: 10px 20px;
  background-color: white;
}
```

**Expected Output:**

```
╭──────────────────╮
│  Click Me Here   │
╰──────────────────╯
```

(A button that looks like a capsule — very popular for modern web buttons and tags/badges.)

### Example 3 — Perfect Circle

For a circle, the element must be **square** (equal width and height), and `border-radius` must be set to `50%`:

```css
div.circle {
  width: 100px;
  height: 100px;
  background-color: coral;
  border-radius: 50%;
}
```

**Expected Output:**

```
     ╭───╮
    ╱     ╲
   │       │
    ╲     ╱
     ╰───╯
```

(A solid coral-coloured circle. This pattern is used for profile photo avatars, notification badges, status indicators, and icons.)

### Controlling Each Corner Individually

`border-radius` can also accept multiple values to control each corner separately. The order goes clockwise starting from the **top-left** corner:

| Number of values | Which corners |
|-----------------|---------------|
| 1 value | All four corners equally |
| 2 values | Top-left & bottom-right / Top-right & bottom-left |
| 3 values | Top-left / Top-right & bottom-left / Bottom-right |
| 4 values | Top-left / Top-right / Bottom-right / Bottom-left |

You can also use the individual corner properties:

| Property | Corner |
|----------|--------|
| `border-top-left-radius` | Top-left corner |
| `border-top-right-radius` | Top-right corner |
| `border-bottom-right-radius` | Bottom-right corner |
| `border-bottom-left-radius` | Bottom-left corner |

### Example 4 — Asymmetric Rounded Corners

```css
div.asymmetric {
  border: 3px solid teal;
  border-radius: 50px 10px;
  /* Top-left & bottom-right: 50px (very round) */
  /* Top-right & bottom-left: 10px (slightly round) */
  padding: 15px;
  width: 200px;
}
```

**Expected Output:**

```
[Box with very round top-left and bottom-right corners,
 slightly round top-right and bottom-left corners]
```

### Example 5 — Four Different Corners

```css
div.custom {
  border: 3px solid purple;
  border-top-left-radius: 5px;
  border-top-right-radius: 30px;
  border-bottom-right-radius: 5px;
  border-bottom-left-radius: 30px;
  padding: 15px;
}
```

This creates an interesting wave-like shape — useful for stylistic callout boxes or decorative elements.

---

## Section 7 — Simple Standalone Examples (Progressive)

### Example A — The Classic Card

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .card {
      border: 1px solid #cccccc;
      border-radius: 8px;
      padding: 20px;
      width: 250px;
      margin: 20px;
    }

    .card h3 {
      border-bottom: 2px solid #cccccc;
      padding-bottom: 8px;
      margin-top: 0;
    }
  </style>
</head>
<body>
  <div class="card">
    <h3>Card Title</h3>
    <p>This is a simple card with a full border and rounded corners, plus a bottom border on the heading.</p>
  </div>
</body>
</html>
```

**Expected Output:**

```
╭───────────────────────────╮
│ Card Title                │
│ ──────────────────────── │
│ This is a simple card     │
│ with a full border and    │
│ rounded corners...        │
╰───────────────────────────╯
```

---

### Example B — Alert/Notification Box (Accent Border)

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .alert-info {
      border: 1px solid #b3d7ff;
      border-left: 5px solid #0077cc;
      border-radius: 4px;
      background-color: #e8f4ff;
      padding: 15px 20px;
      margin: 10px 0;
    }

    .alert-success {
      border: 1px solid #b2dfdb;
      border-left: 5px solid #00897b;
      border-radius: 4px;
      background-color: #e8f5e9;
      padding: 15px 20px;
      margin: 10px 0;
    }

    .alert-warning {
      border: 1px solid #ffe082;
      border-left: 5px solid #f9a825;
      border-radius: 4px;
      background-color: #fffde7;
      padding: 15px 20px;
      margin: 10px 0;
    }
  </style>
</head>
<body>
  <div class="alert-info">ℹ️ Your profile was saved successfully.</div>
  <div class="alert-success">✅ Payment completed. Your order is confirmed.</div>
  <div class="alert-warning">⚠️ Your session will expire in 5 minutes.</div>
</body>
</html>
```

**Expected Output:**

```
┃ ℹ️ Your profile was saved successfully.      [blue]
┃ ✅ Payment completed. Your order is confirmed. [teal]
┃ ⚠️ Your session will expire in 5 minutes.    [yellow]
```

This is a real-world UI pattern used across practically every web application.

---

### Example C — Profile Avatar Circle

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .avatar {
      width: 80px;
      height: 80px;
      background-color: #7b68ee;
      border: 3px solid white;
      border-radius: 50%;
      box-shadow: 0 0 0 3px #7b68ee;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-size: 28px;
      font-weight: bold;
      font-family: Arial, sans-serif;
    }
  </style>
</head>
<body>
  <div class="avatar">AO</div>
</body>
</html>
```

**Expected Output:**

```
   ╭────╮
  ╱  AO  ╲    ← A circular avatar with initials (purple)
  ╲      ╱
   ╰────╯
```

---

## Section 8 — Guided Practice Exercises

### Exercise 1 — Style a Product Card

**Objective:** Practise using border shorthand, border-radius, and side-specific borders together.

**Scenario:** You are building a product listing page for an online store. Each product appears in a styled card.

**Steps:**

1. Create a file called `product-card.html`
2. Write the following HTML:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      padding: 30px;
    }

    .product-card {
      /* Step 1: Add a 1px solid border using the shorthand */
      border: 1px solid #dddddd;

      /* Step 2: Make the corners gently rounded */
      border-radius: 10px;

      /* Step 3: Add a blue top accent border */
      border-top: 4px solid #0057b8;

      background-color: white;
      padding: 20px;
      width: 220px;
    }

    .product-card h2 {
      font-size: 18px;
      margin-top: 0;
      /* Step 4: Add a bottom border under the product name */
      border-bottom: 1px dashed #cccccc;
      padding-bottom: 10px;
    }

    .product-card .price {
      color: #0057b8;
      font-size: 22px;
      font-weight: bold;
      /* Step 5: Add a top border above the price */
      border-top: 1px solid #eeeeee;
      padding-top: 10px;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <div class="product-card">
    <h2>Wireless Headphones</h2>
    <p>Premium sound quality. 30hr battery. Foldable design.</p>
    <div class="price">₦24,500</div>
  </div>
</body>
</html>
```

3. Open in a browser and observe the result.

**Expected Output:**

```
╭─────────────────────────╮  ← blue top accent
│ Wireless Headphones     │
│ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ │  ← dashed separator
│ Premium sound quality.  │
│ 30hr battery. Foldable. │
│ ─────────────────────── │  ← solid separator
│ ₦24,500                 │
╰─────────────────────────╯
```

**Self-Check Questions:**
- What happens to the card's appearance if you change `border-radius: 10px` to `border-radius: 0`?
- What happens if you remove `border-top: 4px solid #0057b8;`? Does the general `border: 1px solid #dddddd` take over on the top side?
- What happens if you change `border-bottom: 1px dashed #cccccc` on the `h2` to `border-bottom: 3px solid red`?

---

### Exercise 2 — Build a Testimonial Quote Block

**Objective:** Practise left-side accent borders combined with `border-radius`.

**Scenario:** A client wants quote testimonials styled attractively on their website.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: Georgia, serif;
      padding: 30px;
      background-color: #fafafa;
    }

    .testimonial {
      border-left: 6px solid #e67e22;   /* orange left accent */
      border-radius: 0 8px 8px 0;        /* round only right corners */
      background-color: #fff9f5;
      padding: 20px 25px;
      margin: 20px 0;
      max-width: 500px;
    }

    .testimonial p {
      margin: 0 0 10px 0;
      font-size: 16px;
      color: #333;
      font-style: italic;
    }

    .testimonial .author {
      font-style: normal;
      font-weight: bold;
      color: #e67e22;
      border-top: 1px solid #f0d9c8;
      padding-top: 8px;
      margin-top: 10px;
    }
  </style>
</head>
<body>

  <div class="testimonial">
    <p>"This product changed the way I work completely. I cannot imagine going back to my old setup."</p>
    <div class="author">— Chidi Okonkwo, Software Engineer</div>
  </div>

  <div class="testimonial">
    <p>"Excellent quality and fast delivery. The customer support team was incredibly helpful."</p>
    <div class="author">— Amina Bello, Business Owner</div>
  </div>

</body>
</html>
```

**Expected Output:**

```
┃ "This product changed the way I work completely..."
┃ ────────────────────────────────────────────
┃ — Chidi Okonkwo, Software Engineer

┃ "Excellent quality and fast delivery..."
┃ ────────────────────────────────────────
┃ — Amina Bello, Business Owner
```
(Both with an orange left bar and right-only rounded corners)

**Self-Check Questions:**
- Why is `border-radius: 0 8px 8px 0` used here instead of `border-radius: 8px`? (Hint: which corners should be sharp to connect with the left accent bar?)
- What would happen if you changed the left border colour to `#2ecc71` (green)?
- Try changing the left border width from `6px` to `15px`. How does it affect the visual weight?

---

### Exercise 3 — Circle Badge / Notification Dot

**Objective:** Practise using `border-radius: 50%` to create circular elements.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 30px;
    }

    /* Notification badge */
    .badge {
      display: inline-block;
      width: 30px;
      height: 30px;
      background-color: #e74c3c;
      border: 2px solid white;
      border-radius: 50%;
      color: white;
      font-size: 13px;
      font-weight: bold;
      text-align: center;
      line-height: 26px;
    }

    /* Status dot */
    .status-online {
      display: inline-block;
      width: 12px;
      height: 12px;
      background-color: #2ecc71;
      border: 2px solid white;
      border-radius: 50%;
    }

    /* Large profile avatar */
    .avatar-lg {
      width: 80px;
      height: 80px;
      background-color: #3498db;
      border: 4px solid #2980b9;
      border-radius: 50%;
    }
  </style>
</head>
<body>
  <p>Notifications: <span class="badge">7</span></p>
  <p>Status: <span class="status-online"></span> Online</p>
  <div class="avatar-lg"></div>
</body>
</html>
```

**Expected Output:**

```
Notifications: ● 7        ← small red circle with number
Status: ●  Online         ← tiny green dot
[Large blue circle]       ← avatar placeholder
```

**Optional "What-If" Challenge:**
- What happens if you change the `width` and `height` of `.avatar-lg` to different values (e.g. `width: 120px; height: 80px`) while keeping `border-radius: 50%`? Does it become an oval? Why?
- Try making the badge a `border-radius: 4px` instead of `50%`. What shape does it become?

---

## Section 9 — Mini Project: Student Profile Card

### Project Description

You will build a clean, professional **student profile card** using every border concept from this lesson: border style, width, colour, individual sides, shorthand, and rounded corners.

### Project Structure

```
profile-card/
└── index.html
```

### Stage 1 — Setup: HTML Structure

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Student Profile Card</title>
  <link rel="stylesheet" href="card.css">
</head>
<body>

  <div class="profile-card">

    <div class="card-header">
      <div class="avatar">AN</div>
      <div class="header-info">
        <h2>Adaeze Nwosu</h2>
        <p class="role">Full-Stack Developer Student</p>
      </div>
    </div>

    <div class="card-body">
      <div class="stat-row">
        <div class="stat">
          <span class="stat-number">12</span>
          <span class="stat-label">Lessons Done</span>
        </div>
        <div class="stat">
          <span class="stat-number">8</span>
          <span class="stat-label">Projects Built</span>
        </div>
        <div class="stat">
          <span class="stat-number">94%</span>
          <span class="stat-label">Quiz Score</span>
        </div>
      </div>
    </div>

    <div class="card-footer">
      <p class="status">🟢 Active Learner</p>
    </div>

  </div>

</body>
</html>
```

### Stage 2 — CSS: `card.css`

```css
/* ===== Base Styles ===== */
body {
  font-family: Arial, sans-serif;
  background-color: #f0f2f5;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  margin: 0;
}

/* ===== The Card Container ===== */
.profile-card {
  /* Shorthand border: all four sides */
  border: 1px solid #dde1e7;

  /* Rounded corners */
  border-radius: 12px;

  /* Blue top accent using side-specific shorthand */
  border-top: 5px solid #1a73e8;

  background-color: white;
  width: 320px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}

/* ===== Card Header ===== */
.card-header {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 20px;

  /* Subtle bottom border separating header from body */
  border-bottom: 1px solid #eeeeee;
}

/* ===== Avatar Circle ===== */
.avatar {
  width: 56px;
  height: 56px;
  background-color: #1a73e8;

  /* border-radius: 50% creates a circle */
  border-radius: 50%;

  /* White border around the avatar */
  border: 3px solid #e8f0fe;

  color: white;
  font-size: 20px;
  font-weight: bold;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

/* ===== Header Text ===== */
.header-info h2 {
  margin: 0 0 4px 0;
  font-size: 17px;
  color: #1c1c1c;
}

.header-info .role {
  margin: 0;
  font-size: 13px;
  color: #666;
}

/* ===== Card Body: Stats ===== */
.card-body {
  padding: 20px;
}

.stat-row {
  display: flex;
  justify-content: space-between;
}

.stat {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex: 1;
  padding: 10px 0;
}

/* Add a left border to the middle stat to visually separate the three */
.stat:nth-child(2) {
  border-left: 1px solid #eeeeee;
  border-right: 1px solid #eeeeee;
}

.stat-number {
  font-size: 24px;
  font-weight: bold;
  color: #1a73e8;
}

.stat-label {
  font-size: 11px;
  color: #888;
  margin-top: 4px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* ===== Card Footer ===== */
.card-footer {
  padding: 12px 20px;
  background-color: #f8f9fa;

  /* Top border on footer using individual side */
  border-top: 1px solid #eeeeee;
}

.card-footer .status {
  margin: 0;
  font-size: 13px;
  color: #444;
}
```

### Stage 3 — Milestone Check

After building Stage 2, your card should display as:

```
╭──────────────────────────────╮  ← blue top accent (5px)
│  ╭────╮  Adaeze Nwosu        │
│  │ AN │  Full-Stack Dev...   │
│  ╰────╯                      │
│ ─────────────────────────── │  ← 1px bottom border (header)
│                              │
│   12        8       94%      │
│ Lessons  Projects   Quiz     │
│ Done      Built    Score     │
│       │         │            │  ← left/right borders on middle stat
│ ─────────────────────────── │  ← 1px top border (footer)
│ 🟢 Active Learner            │
╰──────────────────────────────╯  ← rounded corners
```

### Stage 4 — Enhancements

Try adding these improvements:

1. Add a second card for a different student next to the first
2. Add a `border-radius: 20px` to the `.stat` elements and a background colour to see how borders and rounded corners combine
3. Try adding `border-style: dashed` to the avatar's border — how does it look?
4. Change the top accent colour from blue (`#1a73e8`) to your favourite colour

### Stage 4 — Reflection Questions

1. The card uses `border: 1px solid #dde1e7` AND `border-top: 5px solid #1a73e8`. Which property declaration wins on the top side, and why?
2. The avatar uses `border-radius: 50%` and is 56px × 56px. What shape is it? What would happen if you changed it to 56px × 80px (different width and height)?
3. The middle stat has `border-left` and `border-right`. Why were these side-specific borders used instead of just `border`?
4. If you wanted to add a "Premium Student" badge as a small red circle in the top-right corner of the avatar, what `border-radius` value would you use?

---

## Section 10 — Common Beginner Mistakes

### Mistake 1 — Expecting a Border Without `border-style`

```css
/* ❌ WRONG — no style = no visible border */
p {
  border-width: 3px;
  border-color: red;
}

/* ✅ CORRECT — style must be set */
p {
  border-style: solid;
  border-width: 3px;
  border-color: red;
}

/* ✅ ALSO CORRECT — using shorthand */
p {
  border: 3px solid red;
}
```

**Why it happens:** Beginners logically assume that setting a width and colour is enough. But CSS requires a style value before it renders any border at all. No style = no border, regardless of width and colour.

---

### Mistake 2 — Wrong Shorthand Order

```css
/* ❌ WRONG — colour and style are swapped */
p { border: solid red 3px; }

/* ❌ WRONG — style is first but the order is still off */
p { border: red 3px solid; }

/* ✅ CORRECT — width, style, colour */
p { border: 3px solid red; }
```

The correct order is always: **width → style → colour**. The browser is sometimes forgiving, but writing it correctly avoids bugs and improves readability.

---

### Mistake 3 — Forgetting That Shorthand Overrides Individual Side Properties

```css
/* ❌ This is a problem — border-left is set BEFORE border which overrides it */
p {
  border-left: 5px solid blue;
  border: 1px solid grey;  /* This resets ALL sides, including left! */
}

/* ✅ CORRECT — set general border FIRST, then override specific sides */
p {
  border: 1px solid grey;     /* Set all four sides */
  border-left: 5px solid blue; /* Override just the left side */
}
```

This is one of the most common CSS bugs beginners encounter. Always put the more specific rule **after** the general rule.

---

### Mistake 4 — `border-radius: 50%` Not Making a Circle

```css
/* ❌ Will not be a circle — width ≠ height */
div {
  width: 150px;
  height: 80px;
  border-radius: 50%;
}
/* Result: an oval/ellipse, NOT a circle */

/* ✅ Equal width and height = true circle */
div {
  width: 100px;
  height: 100px;
  border-radius: 50%;
}
```

For `border-radius: 50%` to create a circle, the element must have **equal width and height**.

---

### Mistake 5 — Omitting Units

```css
/* ❌ WRONG — "5" without a unit is invalid */
p { border: 5 solid red; }

/* ✅ CORRECT — always include the unit */
p { border: 5px solid red; }
```

---

### Mistake 6 — Putting `border-radius` on an Element With `overflow: hidden` Already Applied

```css
/* ❌ This often breaks rounded corners on child images */
.card {
  border-radius: 12px;
  overflow: hidden; /* This is fine in isolation, but watch for interactions */
}
```

> When you have an image inside a rounded-corner container, the image corners may still appear square. Adding `overflow: hidden` to the container tells the browser to clip any content (including the image's sharp corners) to the rounded box shape. This is actually the *solution*, not the problem — but beginners are often confused why their images are still square. The fix is `overflow: hidden` on the parent container.

---

## Section 11 — Reflection Questions

1. You want to create a paragraph with a dotted border. You write `border-color: blue; border-width: 2px;` but nothing appears. What is missing?

2. What is the difference between `border: none` and `border: 0`?
   > (`border: none` sets `border-style` to none. `border: 0` sets `border-width` to 0. Both make the border invisible, but `border: none` is the more common and explicit approach for removing a border entirely.)

3. Write the CSS shorthand for a 4px dashed orange border on all four sides of a `div`.

4. You want a heading with a border only on the bottom. Write the most efficient CSS to achieve this (use the side-specific shorthand).

5. A square `div` is 120px × 120px. What `border-radius` value turns it into a perfect circle?

6. You have `border: 2px solid black` applied to a `p` tag. You then write `border-top: none`. What does the `p` look like?

7. Explain the "TRouBLe" memory trick. What does each letter stand for?

8. Which has more CSS specificity — `border-left-color: red` or `border-color: blue` — when both appear in the same rule block? (Hint: the more specific property always wins.)

---

## Section 12 — Completion Checklist

Go through this list and confirm you can do or explain each item:

- [ ] I know that `border-style` must be set before any border becomes visible
- [ ] I can name at least 5 different `border-style` values and describe what they look like
- [ ] I understand how 1, 2, 3, and 4 values work with border shorthand properties (top → right → bottom → left)
- [ ] I can set `border-width` using keywords (`thin`, `medium`, `thick`) and pixel values
- [ ] I can set `border-color` using named colours, HEX codes, and RGB values
- [ ] I can style individual sides using `border-top`, `border-right`, `border-bottom`, `border-left`
- [ ] I can use the `border` shorthand: `border: [width] [style] [color]`
- [ ] I understand that in shorthand, order is: **width → style → colour**
- [ ] I know that a general `border` rule must come BEFORE a side-specific override
- [ ] I can use `border-radius` to create gently rounded corners, pill shapes, and circles
- [ ] I know that `border-radius: 50%` only creates a circle on square elements
- [ ] I understand why `overflow: hidden` is sometimes needed alongside `border-radius`
- [ ] I completed at least two of the three guided practice exercises
- [ ] I completed at least Stage 1 and Stage 2 of the Mini Project

---

## Lesson Summary

You have now mastered one of the most versatile and commonly used families of CSS properties — **borders**.

Here is your complete reference summary:

### The Three Core Properties

| Property | Purpose | Example |
|----------|---------|---------|
| `border-style` | Type of line | `solid`, `dashed`, `dotted`, `double` |
| `border-width` | Thickness | `1px`, `3px`, `thin`, `thick` |
| `border-color` | Colour | `red`, `#ff0000`, `rgb(255,0,0)` |

### The Shorthand

```css
/* border: width style color; */
border: 3px solid navy;
```

### Individual Side Shorthands

```css
border-top: 2px dashed red;
border-right: 1px solid blue;
border-bottom: 3px solid green;
border-left: 5px solid orange;
```

### Rounded Corners

```css
border-radius: 8px;       /* gentle rounding */
border-radius: 50px;      /* pill/capsule shape */
border-radius: 50%;       /* perfect circle (square elements only) */
```

### Key Rules to Remember

- **`border-style` must always be defined** — without it, no border renders, regardless of width or colour
- **Shorthand order:** `width → style → colour` (never reversed)
- **Side-specific rules must come AFTER general `border`** rules, not before
- **The `TRouBLe` order:** Top → Right → Bottom → Left (clockwise from 12 o'clock)
- **`border-radius: 50%` requires equal width and height** to produce a circle

### Real-World Applications

- **`solid` borders:** Input fields, table cells, cards, modals
- **`dashed` borders:** File upload drop zones, placeholder regions
- **`dotted` borders:** Subtle separators, decorative elements
- **Left-only borders:** Quotation blocks, notification banners, sidebar highlights
- **`border-radius`:** Buttons, cards, avatars, badges, pill tags, modal dialogs
- **Bottom-only borders:** Heading underlines, tab indicators, form field underlines

---

*End of Lesson 07 — You are now ready to move on to CSS Margins.*
