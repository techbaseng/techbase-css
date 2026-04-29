---
render_with_liquid: false
title: "CSS 2D and 3D Transforms — Moving, Rotating, Scaling, Skewing, and 3D Space"
nav_order: 54
---

# Lesson 54 — CSS 2D and 3D Transforms

---

## Lesson Introduction

Have you ever watched an animation on a website where a card flips over when you hover it, or an icon smoothly spins, or a button gently grows when you mouse over it? These effects are powered by **CSS Transforms**.

CSS Transforms let you **move, rotate, resize, and distort** any HTML element — purely in CSS, without needing JavaScript or images. There are two families of transforms:

- **2D Transforms** — changes that happen on a flat screen (left/right, up/down, rotation, scaling, skewing)
- **3D Transforms** — changes that bring a sense of depth and perspective (rotating into or away from you, moving along a Z-axis)

By the end of this lesson you will be able to:
- Translate (move) elements in 2D and 3D space
- Rotate elements on any axis
- Scale elements up and down
- Skew elements into diagonal shapes
- Apply multiple transforms at once
- Build a real 3D flip card — a staple interactive component in modern web design

> **Real-world relevance:** Transforms are used in image galleries, product cards, loading animations, pricing tables, navigation icons, interactive menus, data visualisation dashboards, and mobile app UIs.

---

## Prerequisite Concepts

### What is a CSS Property?
A **CSS property** is the thing you want to change about an element. `transform` is the property covered in this lesson.

### What is a CSS Value?
The **value** is what you set the property to. For transforms, values are function calls like `rotate(45deg)` or `translateX(50px)`.

### What is the CSS `transform` Property?
The `transform` property applies one or more geometric changes (transformations) to an element. You write `transform:` followed by one or more transform functions.

### What is a Function in CSS?
A CSS function is a special word followed by parentheses that contain a value — for example `rotate(45deg)` or `scale(1.5)`. The word before the brackets is the function name, and what's inside the brackets is the argument (the input it needs to do its job).

### What are Degrees (`deg`)?
Degrees measure rotation, just like on a compass or a clock:
- `0deg` = no rotation (original position)
- `90deg` = a quarter turn clockwise
- `180deg` = half a turn (upside down)
- `360deg` = a full turn (back to where you started)
- Negative degrees (`-45deg`) rotate counter-clockwise

### What is the `perspective` Property?
Perspective is what creates the illusion of depth. Imagine looking down a road — objects further away look smaller. `perspective` in CSS tells the browser how far "away" the viewer is from the 3D scene. We will cover this fully in the 3D section.

### What is `transform-origin`?
By default, transforms happen around the **centre** of the element. `transform-origin` lets you change that pivot point — for example, making a door hinge from its left edge instead of its centre.

---

## Part 1 — CSS 2D Transforms

### What Are 2D Transforms?

2D (two-dimensional) means changes that happen on the flat surface of your screen — left and right (the X-axis), and up and down (the Y-axis). No depth is involved.

> **Analogy:** Think of your screen as a table. 2D transforms slide things around on the table, spin them flat like spinning a coin, stretch or shrink them, or tilt them to one side. Everything still stays on the flat table surface.

The CSS property is:

```css
selector {
  transform: function(value);
}
```

---

### 2D Transform Function 1 — `translate()`

#### What Is Translate?

**Translate** means to **move** an element from its current position to a new one. It does NOT affect the surrounding layout — the space where the element originally was stays empty (other elements do not shift).

> **Analogy:** Imagine your element is a sticky note on a whiteboard. `translate()` lifts it and places it somewhere else on the board — but the original rectangular ghost of it stays pinned where it was. Other sticky notes don't move.

#### Syntax

```css
/* Move right 50px and down 20px */
transform: translate(50px, 20px);

/* Move only horizontally */
transform: translateX(50px);

/* Move only vertically */
transform: translateY(20px);
```

| Value | What It Does |
|---|---|
| `translate(x, y)` | Moves x pixels right and y pixels down |
| `translate(-x, -y)` | Moves x pixels left and y pixels up |
| `translateX(x)` | Moves only horizontally |
| `translateY(y)` | Moves only vertically |

#### Simple Example 1 — Basic translate()

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .box {
      width: 100px;
      height: 100px;
      background-color: coral;
      transform: translate(50px, 30px);
    }
  </style>
</head>
<body>
  <div class="box">Moved!</div>
</body>
</html>
```

**Line-by-line:**
- `width: 100px; height: 100px;` — creates a 100×100 box
- `background-color: coral;` — gives it an orange-coral colour
- `transform: translate(50px, 30px);` — shifts the box 50px to the right and 30px downward from where it would normally sit

**Expected Output:**
A coral square that appears shifted 50px right and 30px down from its normal position. The space where it would have been is left blank.

> **Thinking prompt:** What happens if you use `translate(-50px, -30px)`? (The box moves 50px to the LEFT and 30px UP.)

#### Simple Example 2 — translateX Only

```css
.icon {
  width: 50px;
  height: 50px;
  background-color: steelblue;
  transform: translateX(100px);
}
```

**Expected Output:** A blue box moved 100px to the right, with no vertical movement.

#### Practical use case — Centering with translate

```css
/* A classic CSS centering trick */
.centered {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

**What this does:** Placing the top-left corner of an element at 50%/50% would put it slightly off-center. Moving it back by -50% of its own width and height perfectly centers it. This is a real-world technique used constantly by professional developers.

---

### 2D Transform Function 2 — `rotate()`

#### What Is Rotate?

`rotate()` spins an element clockwise (positive degrees) or counter-clockwise (negative degrees) around its centre point (or a custom origin).

> **Analogy:** Think of a clock hand pivoting around the centre of the clock face.

#### Syntax

```css
transform: rotate(angle);
```

| Value | Effect |
|---|---|
| `rotate(45deg)` | 45° clockwise turn |
| `rotate(-45deg)` | 45° counter-clockwise turn |
| `rotate(180deg)` | Upside down |
| `rotate(360deg)` | Full spin (looks same as 0, but useful in animations) |

#### Simple Example 1 — Basic rotate()

```html
<style>
  .box {
    width: 100px;
    height: 100px;
    background-color: mediumseagreen;
    transform: rotate(45deg);
  }
</style>
<div class="box">Rotated</div>
```

**Expected Output:**
A green square rotated 45 degrees clockwise — it now looks like a diamond shape.

#### Simple Example 2 — Negative Rotation

```css
.arrow {
  font-size: 32px;
  display: inline-block;
  transform: rotate(-90deg);
}
```

**Expected Output:** An element (like an arrow symbol) that points to the right becomes an upward-pointing arrow because it was rotated 90° counter-clockwise.

#### Changing the Pivot Point with `transform-origin`

By default, rotation happens around the centre of the element. You can change this:

```css
.door {
  width: 80px;
  height: 160px;
  background-color: sienna;
  transform-origin: left center;  /* Hinge on the left edge */
  transform: rotate(30deg);
}
```

| transform-origin value | Pivot point |
|---|---|
| `center` (default) | Middle of the element |
| `top left` | Top-left corner |
| `left center` | Middle of the left edge |
| `bottom right` | Bottom-right corner |
| `50% 50%` | Same as center (in percentages) |

**Expected Output:** A brown rectangle that appears to swing open like a door hinged at its left edge.

---

### 2D Transform Function 3 — `scale()`

#### What Is Scale?

`scale()` makes an element **larger or smaller** without affecting the surrounding layout. Think of it like zooming in or out on just that element.

> **Analogy:** Imagine holding a rubber stamp and stretching it — the stamp gets bigger, but the table it's sitting on doesn't move.

#### Syntax

```css
/* Scale both width and height equally */
transform: scale(factor);

/* Scale width and height independently */
transform: scale(xFactor, yFactor);

/* Scale only width */
transform: scaleX(factor);

/* Scale only height */
transform: scaleY(factor);
```

| Factor Value | Effect |
|---|---|
| `scale(1)` | No change (original size) |
| `scale(2)` | Double the size |
| `scale(0.5)` | Half the size |
| `scale(1.5)` | 50% larger |
| `scale(-1)` | Flips the element (mirror image) |

#### Simple Example 1 — Basic scale()

```html
<style>
  .box {
    width: 100px;
    height: 100px;
    background-color: orchid;
    transform: scale(2);
  }
</style>
<div class="box">2× bigger</div>
```

**Expected Output:** A purple box that appears twice as wide and twice as tall as its original 100×100 size. Note it scales FROM the centre — so it expands equally in all directions.

> **Important:** The element still technically occupies its original 100×100 space in the layout. `scale()` is a visual effect only.

#### Simple Example 2 — scale() on Hover (Common Pattern)

```css
.card {
  width: 200px;
  height: 150px;
  background-color: white;
  box-shadow: 0 4px 10px rgba(0,0,0,0.2);
  transition: transform 0.3s ease;
}

.card:hover {
  transform: scale(1.05);
}
```

**Expected Output:** A card that smoothly grows 5% bigger when you hover over it — a very common "zoom in on hover" effect for product images, cards, and thumbnails.

#### Simple Example 3 — scaleX and scaleY Independently

```css
.wide {
  transform: scaleX(3);      /* 3× as wide, same height */
}

.tall {
  transform: scaleY(2);      /* 2× as tall, same width */
}

.mirrored {
  transform: scaleX(-1);     /* Horizontally flipped */
}
```

**Expected Outputs:**
- `.wide` → a horizontally stretched element
- `.tall` → a vertically stretched element
- `.mirrored` → a horizontally mirrored/flipped element (useful for flipping directional icons)

---

### 2D Transform Function 4 — `skew()`

#### What Is Skew?

`skew()` **tilts/slants** an element along the X and/or Y axis. It's like pushing the top of a rectangle to the right while keeping the bottom in place — the result is a parallelogram shape.

> **Analogy:** Imagine writing text on a rubber eraser, then pushing the top of the eraser sideways. The text leans diagonally — that's a skew.

#### Syntax

```css
/* Skew along X axis (tilts left/right) */
transform: skewX(angle);

/* Skew along Y axis (tilts up/down) */
transform: skewY(angle);

/* Skew both axes at once */
transform: skew(xAngle, yAngle);
```

#### Simple Example 1 — skewX

```html
<style>
  .box {
    width: 150px;
    height: 80px;
    background-color: tomato;
    transform: skewX(20deg);
  }
</style>
<div class="box">Skewed!</div>
```

**What `skewX(20deg)` does:** The top edge of the box shifts 20° to the right while the bottom stays put, turning the rectangle into a slanted parallelogram shape.

**Expected Output:** A red box that looks like it's leaning/italicised to the right.

#### Simple Example 2 — skewY

```css
.box {
  transform: skewY(10deg);
}
```

**Expected Output:** A box where the left edge tilts, making the shape lean diagonally from left-bottom to right-top.

#### Simple Example 3 — Both Axes

```css
.box {
  transform: skew(20deg, 10deg);
}
```

**Expected Output:** A box skewed along both axes simultaneously, creating a double-slanted parallelogram.

#### Real-world use — Skewed section dividers

Skew is commonly used on website sections to create diagonal/angled transitions between sections:

```css
.hero-section {
  background-color: #4A90E2;
  padding: 60px;
  transform: skewY(-3deg);
  margin-bottom: -20px;
}
```

**Expected Output:** A section whose top and bottom edges are diagonally slanted instead of perfectly horizontal — a very trendy design technique seen on marketing and SaaS websites.

---

### 2D Transform Function 5 — `matrix()`

#### What Is matrix()?

`matrix()` is a single function that **combines** all 2D transforms into one. It is a compact shorthand used internally by browsers and sometimes in animation libraries. It uses 6 values from a mathematical concept called a **transformation matrix**.

> **You don't need to memorise matrix() values** — but you should know it exists and what it can do.

#### Syntax

```css
transform: matrix(scaleX, skewY, skewX, scaleY, translateX, translateY);
```

| Position | What It Controls |
|---|---|
| 1st (a) | scaleX — horizontal scale |
| 2nd (b) | skewY — Y-axis skew |
| 3rd (c) | skewX — X-axis skew |
| 4th (d) | scaleY — vertical scale |
| 5th (e) | translateX — horizontal move |
| 6th (f) | translateY — vertical move |

#### Example — matrix() replicating a combination

```css
/* This matrix() is equivalent to: scale(1) + no skew + translate(50px, 30px) */
transform: matrix(1, 0, 0, 1, 50, 30);

/* This produces the same result as: translate(50px, 30px) */
```

**When is this used?**
Browsers often convert your separate transforms into a matrix internally for performance. Animation libraries like GSAP also output matrix values. Understanding its structure helps you read browser debug tools.

---

### Combining Multiple 2D Transforms

You can apply **multiple transform functions** to one element by listing them separated by spaces:

```css
/* Rotate AND translate at the same time */
.element {
  transform: rotate(45deg) translate(50px, 0);
}

/* Scale AND rotate */
.element {
  transform: scale(1.2) rotate(10deg);
}

/* Translate, rotate, and scale together */
.element {
  transform: translate(30px, 20px) rotate(30deg) scale(0.8);
}
```

> **Important:** The ORDER of transforms matters! `rotate(45deg) translate(50px, 0)` is NOT the same as `translate(50px, 0) rotate(45deg)`. The first rotates the element and then translates along the rotated axis. The second translates and then rotates around the translated position.

#### Example — Combining rotate and translate

```html
<style>
  .box-a {
    transform: rotate(45deg) translate(80px, 0);
    /* Rotates first, then moves 80px along the ROTATED X-axis (diagonally) */
  }

  .box-b {
    transform: translate(80px, 0) rotate(45deg);
    /* Moves 80px RIGHT first, then rotates in place */
  }
</style>
```

**Expected Output:** The two boxes end up in different positions and orientations — visually demonstrating that transform order matters.

---

### 2D Transforms — Complete Reference Table

| Function | Syntax | What It Does |
|---|---|---|
| `translate()` | `translate(x, y)` | Moves element x right and y down |
| `translateX()` | `translateX(x)` | Moves element horizontally only |
| `translateY()` | `translateY(y)` | Moves element vertically only |
| `rotate()` | `rotate(angle)` | Rotates element clockwise |
| `scale()` | `scale(x, y)` | Resizes element (1 = normal, 2 = double) |
| `scaleX()` | `scaleX(x)` | Resizes width only |
| `scaleY()` | `scaleY(y)` | Resizes height only |
| `skewX()` | `skewX(angle)` | Slants element along X axis |
| `skewY()` | `skewY(angle)` | Slants element along Y axis |
| `skew()` | `skew(xAngle, yAngle)` | Slants element on both axes |
| `matrix()` | `matrix(a,b,c,d,e,f)` | Combines all transforms in one function |

---

## Part 2 — 2D Transform Code Challenges

### Challenge 1 — Centred Diagonal Banner

**Task:** Create a div that is rotated -45 degrees and translated 30px to the right and 10px up.

```html
<style>
  .banner {
    width: 200px;
    height: 50px;
    background-color: #e74c3c;
    color: white;
    text-align: center;
    line-height: 50px;
    font-weight: bold;
    /* ADD TRANSFORM HERE */
  }
</style>
<div class="banner">SALE</div>
```

**Solution:**
```css
.banner {
  transform: rotate(-45deg) translate(30px, -10px);
}
```

**Expected Output:** A red "SALE" banner tilted counter-clockwise diagonally — the kind you often see in the corner of product images.

---

### Challenge 2 — Mirrored Icon

**Task:** Flip an arrow element horizontally using scale.

```html
<style>
  .arrow {
    font-size: 40px;
    display: inline-block;
    /* ADD TRANSFORM HERE */
  }
</style>
<span class="arrow">➜</span>
```

**Solution:**
```css
.arrow {
  transform: scaleX(-1);
}
```

**Expected Output:** The right-pointing arrow now points left — achieved by horizontally mirroring with `scaleX(-1)`.

---

### Challenge 3 — Hover Zoom Card

**Task:** Make a card smoothly grow 10% on hover.

```html
<style>
  .card {
    width: 200px;
    padding: 20px;
    background: white;
    border-radius: 8px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    transition: transform 0.3s ease;
  }
  /* ADD HOVER RULE HERE */
</style>
<div class="card">
  <h3>Product</h3>
  <p>$29.99</p>
</div>
```

**Solution:**
```css
.card:hover {
  transform: scale(1.1);
}
```

**Expected Output:** A card that smoothly zooms 10% larger when you hover over it, returning to normal when the mouse leaves.

---

### Challenge 4 — Skewed Heading

**Task:** Create a heading with a skewX of -15deg to give it a dynamic, italicised parallelogram feel.

```html
<style>
  h1 {
    display: inline-block;
    background-color: #3498db;
    color: white;
    padding: 10px 20px;
    /* ADD TRANSFORM HERE */
  }
</style>
<h1>Fast. Modern. Bold.</h1>
```

**Solution:**
```css
h1 {
  transform: skewX(-15deg);
}
```

**Expected Output:** A blue heading with the background slanted diagonally — as if it's leaning forward aggressively.

---

## Part 3 — CSS 3D Transforms

### What Are 3D Transforms?

So far, all our transforms happened on a flat surface — left/right (X) and up/down (Y). **3D transforms** add a third dimension: **Z** — which represents depth — things coming toward you or going away from you.

> **Analogy:** Imagine your screen is a window looking into a room. X moves things left and right across the room. Y moves things up and down. Z moves things closer to the window (toward you) or further into the room (away from you).

### The Three Axes in 3D

```
        Y (up/down)
        |
        |
        |_________ X (left/right)
       /
      /
     Z (toward/away from viewer)
```

| Axis | Direction |
|---|---|
| X | Left (negative) / Right (positive) |
| Y | Up (negative) / Down (positive) |
| Z | Away from viewer (negative) / Toward viewer (positive) |

---

### Prerequisites for 3D: `perspective`

Before 3D transforms look like 3D, you need to set a **perspective** on the parent container.

#### What Is Perspective?

Perspective creates the **illusion of depth**. Without it, a 3D rotation looks flat — it just squishes. With perspective, elements further away look smaller and closer elements look larger, just like in real life.

> **Analogy:** Perspective is like the distance between you and a painting. Stand 5cm away from a painting and the perspective is extreme — things look wildly distorted. Stand 5 metres away and everything looks more normal. In CSS: a small perspective value = dramatic 3D effect. A large value = subtle 3D effect.

#### Syntax: Two Ways to Set Perspective

**Method 1: `perspective` property on the PARENT element (most common)**

```css
.container {
  perspective: 500px;
}
```

This applies perspective to ALL children of `.container` as if they're in the same 3D scene together.

**Method 2: `perspective()` function in the child's `transform`**

```css
.child {
  transform: perspective(500px) rotateY(45deg);
}
```

This applies perspective to ONE specific element only.

| Perspective Value | Visual Effect |
|---|---|
| `100px` | Very strong, dramatic 3D effect |
| `500px` | Moderate, natural 3D effect |
| `1000px` | Subtle 3D effect |
| `none` | No perspective — flat appearance |

---

### 3D Transform Function 1 — `rotateX()`, `rotateY()`, `rotateZ()`

#### What Are 3D Rotations?

In 3D, you can rotate an element around any of the three axes:

- `rotateX(angle)` — tilts element forward/backward (like a page turning toward you)
- `rotateY(angle)` — spins element left/right (like a revolving door)
- `rotateZ(angle)` — spins flat on screen (same as 2D `rotate()`)

#### Simple Example 1 — rotateY (Revolving Door)

```html
<style>
  .container {
    perspective: 600px;
  }

  .box {
    width: 150px;
    height: 100px;
    background-color: #3498db;
    color: white;
    text-align: center;
    line-height: 100px;
    transform: rotateY(45deg);
  }
</style>
<div class="container">
  <div class="box">rotateY(45deg)</div>
</div>
```

**Line-by-line:**
- `perspective: 600px` on the container — sets up the 3D viewing distance
- `rotateY(45deg)` on the box — rotates it 45° around the vertical (Y) axis

**Expected Output:**
A blue box that appears to be turning away from you like a revolving door that's 45° open. The left side appears further away (smaller) and the right side appears closer (larger).

#### Simple Example 2 — rotateX (Page Flip Forward)

```css
.container {
  perspective: 400px;
}

.box {
  transform: rotateX(45deg);
}
```

**Expected Output:** The box appears to tilt forward at the bottom — like a book cover opening toward you, with the top going away and the bottom coming closer.

#### Simple Example 3 — All Three Axes Compared

```html
<style>
  .scene {
    perspective: 600px;
    display: flex;
    gap: 40px;
  }

  .box {
    width: 100px;
    height: 100px;
    background-color: coral;
    color: white;
    text-align: center;
    line-height: 100px;
  }

  .rx { transform: rotateX(45deg); }
  .ry { transform: rotateY(45deg); }
  .rz { transform: rotateZ(45deg); }
</style>

<div class="scene">
  <div class="box rx">rotateX</div>
  <div class="box ry">rotateY</div>
  <div class="box rz">rotateZ</div>
</div>
```

**Expected Output:** Three boxes in a row — first tilted forward (X-axis), second spinning sideways (Y-axis), third rotated flat (Z-axis, like 2D rotate).

---

### 3D Transform Function 2 — `rotate3d()`

`rotate3d()` lets you define a **custom rotation axis** — a combination of X, Y, and Z — and then specify the angle.

#### Syntax

```css
transform: rotate3d(x, y, z, angle);
```

| Parameter | Meaning |
|---|---|
| `x` | How much the X axis contributes (0 to 1) |
| `y` | How much the Y axis contributes (0 to 1) |
| `z` | How much the Z axis contributes (0 to 1) |
| `angle` | The degree of rotation |

#### Examples

```css
/* Pure X rotation (same as rotateX(45deg)) */
transform: rotate3d(1, 0, 0, 45deg);

/* Pure Y rotation (same as rotateY(45deg)) */
transform: rotate3d(0, 1, 0, 45deg);

/* Diagonal axis (mix of X and Y) */
transform: rotate3d(1, 1, 0, 45deg);
```

---

### 3D Transform Function 3 — `translateZ()` and `translate3d()`

`translateZ()` moves an element **toward or away from the viewer** along the Z-axis.

> **Analogy:** `translateZ(100px)` is like picking up an object and moving it 100px closer to your face. `translateZ(-100px)` pushes it 100px further away.

#### Syntax

```css
/* Move 100px toward the viewer */
transform: translateZ(100px);

/* Move 100px away from the viewer */
transform: translateZ(-100px);

/* Move on all three axes at once */
transform: translate3d(x, y, z);
```

#### Example — translateZ with perspective

```html
<style>
  .scene {
    perspective: 400px;
    display: flex;
    gap: 30px;
    align-items: center;
  }

  .far   { transform: translateZ(-100px); background: #e74c3c; }
  .near  { transform: translateZ(100px);  background: #2ecc71; }
  .box {
    width: 100px;
    height: 100px;
    color: white;
    text-align: center;
    line-height: 100px;
  }
</style>

<div class="scene">
  <div class="box far">Far</div>
  <div class="box near">Near</div>
</div>
```

**Expected Output:** Two boxes — the red one appears smaller (pushed away) and the green one appears larger (pulled forward) — demonstrating depth perception through translateZ.

---

### 3D Transform Function 4 — `scaleZ()` and `scale3d()`

`scaleZ()` scales an element along the Z-axis (depth). On its own, this has no visual effect unless combined with another 3D transform that uses depth.

```css
/* Scale in all three dimensions */
transform: scale3d(scaleX, scaleY, scaleZ);
```

**Example:**
```css
transform: scale3d(1.5, 1.5, 1);
/* Same as: scale(1.5) — no Z scaling needed for a flat element */
```

---

### The `transform-style` Property

When you build 3D scenes with nested elements (like a 3D flip card where the front and back faces are children), you need to tell CSS to **preserve the 3D positions** of child elements.

```css
.parent {
  transform-style: flat;          /* Default — children are flattened */
  transform-style: preserve-3d;   /* Children keep their 3D positions */
}
```

> **Rule of thumb:** Any container that is being 3D-transformed AND has children that should also appear in 3D space needs `transform-style: preserve-3d`.

---

### The `backface-visibility` Property

When you rotate an element 180 degrees, you are looking at its **back face**. By default the back face is visible (you see a mirrored version of the front). You can hide it:

```css
.card-face {
  backface-visibility: hidden;   /* Hides the element when facing away */
  backface-visibility: visible;  /* Default — always visible */
}
```

**Why is this important?**
In a 3D flip card, you have two faces (front and back). When the front is visible, the back should be hidden, and vice versa. `backface-visibility: hidden` makes this work correctly.

---

### 3D CSS Transforms — Complete Reference

| Function | Description |
|---|---|
| `rotateX(angle)` | Rotates around horizontal axis (forward/backward tilt) |
| `rotateY(angle)` | Rotates around vertical axis (left/right spin) |
| `rotateZ(angle)` | Rotates around depth axis (same as 2D rotate) |
| `rotate3d(x,y,z,angle)` | Rotates around a custom 3D axis |
| `translateZ(z)` | Moves along depth axis (toward/away from viewer) |
| `translate3d(x,y,z)` | Moves in all three directions at once |
| `scaleZ(z)` | Scales depth axis |
| `scale3d(x,y,z)` | Scales all three axes at once |
| `perspective(n)` | Sets perspective depth for one element |
| `matrix3d(16 values)` | Full 3D transformation matrix (16 values) |

| Property | Description |
|---|---|
| `perspective` | Distance from the viewer (on parent element) |
| `perspective-origin` | Position of the viewer's eye (default: center center) |
| `transform-style` | `flat` or `preserve-3d` for child elements |
| `backface-visibility` | `hidden` or `visible` for back face |

---

## Part 4 — Guided Practice Exercises

### Exercise 1 — Rotating Badge

**Objective:** Use rotate and translate to create a corner badge.

**Scenario:** You are styling a product card and need a "NEW" badge in the top-right corner, tilted diagonally.

```html
<style>
  .product {
    position: relative;
    width: 200px;
    height: 250px;
    background: #f8f9fa;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 4px 15px rgba(0,0,0,0.15);
  }

  .badge {
    position: absolute;
    top: 20px;
    right: -30px;
    background-color: #e74c3c;
    color: white;
    padding: 5px 40px;
    font-size: 12px;
    font-weight: bold;
    /* ADD TRANSFORM HERE */
  }
</style>

<div class="product">
  <div class="badge">NEW</div>
  <div style="padding: 20px;">
    <h3>Sneaker Pro X</h3>
    <p>$89.99</p>
  </div>
</div>
```

**Task:** Add `transform: rotate(45deg)` to `.badge`.

**Expected Output:** A product card with a red diagonal "NEW" ribbon in the top-right corner — identical to the badges you see on e-commerce product cards.

---

### Exercise 2 — 3D Perspective Box

**Objective:** Use `rotateY` with `perspective` to make a box appear 3D.

```html
<style>
  .scene {
    perspective: 500px;
    margin: 80px auto;
    width: 200px;
  }

  .box-3d {
    width: 200px;
    height: 150px;
    background: linear-gradient(135deg, #667eea, #764ba2);
    color: white;
    text-align: center;
    line-height: 150px;
    font-size: 18px;
    font-weight: bold;
    border-radius: 8px;
    /* ADD TRANSFORM HERE */
    transition: transform 0.5s ease;
  }

  .box-3d:hover {
    /* ADD HOVER TRANSFORM HERE */
  }
</style>

<div class="scene">
  <div class="box-3d">Hover Me!</div>
</div>
```

**Task:**
1. Add `transform: rotateY(20deg)` to the normal state
2. Add `transform: rotateY(-20deg)` to the hover state

**Expected Output:** A purple gradient box slightly turned to one side. When you hover it, it smoothly swings to the other side — creating a rocking 3D animation.

---

### Exercise 3 — Zoom Gallery

**Objective:** Apply scale and transition to create an image zoom gallery effect.

```html
<style>
  .gallery {
    display: flex;
    gap: 15px;
    flex-wrap: wrap;
  }

  .gallery-item {
    width: 150px;
    height: 100px;
    overflow: hidden;
    border-radius: 8px;
    cursor: pointer;
  }

  .gallery-item div {
    width: 100%;
    height: 100%;
    background-color: #3498db;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-weight: bold;
    transition: transform 0.4s ease;
  }

  /* ADD HOVER RULE HERE */
</style>

<div class="gallery">
  <div class="gallery-item"><div>Photo 1</div></div>
  <div class="gallery-item"><div>Photo 2</div></div>
  <div class="gallery-item"><div>Photo 3</div></div>
</div>
```

**Task:** Add a hover rule: `.gallery-item:hover div { transform: scale(1.2); }`

**Expected Output:** Each gallery card smoothly zooms in when hovered. Because `overflow: hidden` is on the container, the zoom stays contained — content that grows beyond the boundary is clipped. This is the classic image gallery hover zoom pattern.

---

## Part 5 — Mini Project: 3D Flip Card

This is the signature 3D CSS project — a card that flips over when you hover it, revealing a back face. This technique is used on business card websites, flashcard apps, team member profiles, and product feature reveals.

### How a 3D Flip Card Works

The structure is:
1. **Outer container** — the fixed-size window. Has `perspective`.
2. **Inner wrapper** — does the rotating. Has `transform-style: preserve-3d` and `transition`.
3. **Front face** — visible by default. Has `backface-visibility: hidden`.
4. **Back face** — hidden by default (rotated 180° away). Has `backface-visibility: hidden` and `transform: rotateY(180deg)`.

When you hover, the inner wrapper rotates 180°. The front goes away, the back comes forward.

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>3D Flip Card</title>
  <link rel="stylesheet" href="flip.css">
</head>
<body>
  <div class="flip-container">
    <div class="flipper">

      <!-- FRONT FACE -->
      <div class="face front">
        <div class="face-content">
          <div class="avatar">TK</div>
          <h2>Temi Kola</h2>
          <p class="role">Frontend Developer</p>
          <p class="hint">Hover to see more →</p>
        </div>
      </div>

      <!-- BACK FACE -->
      <div class="face back">
        <div class="face-content">
          <h2>Contact</h2>
          <p>📧 temi@example.com</p>
          <p>🐦 @temi_codes</p>
          <p>💼 Lagos, Nigeria</p>
          <button class="connect-btn">Connect</button>
        </div>
      </div>

    </div>
  </div>
</body>
</html>
```

**Milestone 1 Output:** Two sections of content stacked on top of each other — messy, but the HTML structure is in place.

---

### Stage 2 — Container and Flipper Styles

Create `flip.css`:

```css
/* ========================
   RESET AND BODY
   ======================== */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background: linear-gradient(135deg, #1a1a2e, #16213e);
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Arial, sans-serif;
}

/* ========================
   THE 3D FLIP MECHANISM
   ======================== */

/* Step 1: Outer container — fixed size + perspective */
.flip-container {
  width: 300px;
  height: 380px;
  perspective: 1000px;       /* 3D viewing distance */
  cursor: pointer;
}

/* Step 2: Inner wrapper — this is what rotates */
.flipper {
  position: relative;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;    /* Critical: preserves 3D positions of children */
  transition: transform 0.7s ease; /* Smooth 0.7s flip animation */
}

/* Step 3: Trigger the flip on hover */
.flip-container:hover .flipper {
  transform: rotateY(180deg);
}

/* ========================
   SHARED FACE STYLES
   ======================== */
.face {
  position: absolute;   /* Both faces sit in exact same position */
  width: 100%;
  height: 100%;
  border-radius: 20px;
  backface-visibility: hidden;   /* Critical: hide face when facing away */
  overflow: hidden;
}

.face-content {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 30px;
  text-align: center;
  gap: 12px;
}
```

**Milestone 2 Output:** The card container is set up. Both faces are layered on top of each other but neither is visible yet (they're both hidden by `backface-visibility`). The 3D scene is ready.

---

### Stage 3 — Front Face Styles

```css
/* ========================
   FRONT FACE
   ======================== */
.front {
  background: linear-gradient(160deg, #ffffff 0%, #f0f4ff 100%);
  box-shadow:
    0 20px 60px rgba(0, 0, 0, 0.3),
    0 6px 20px rgba(0, 0, 0, 0.2);
  /* Front face is already at 0deg — visible by default */
}

.avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
  font-size: 28px;
  font-weight: bold;
  line-height: 80px;
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.5);
}

.front h2 {
  font-size: 22px;
  color: #1a1a2e;
}

.front .role {
  font-size: 14px;
  color: #667eea;
  text-transform: uppercase;
  letter-spacing: 1.5px;
}

.front .hint {
  font-size: 12px;
  color: #aaa;
  margin-top: 8px;
}
```

**Milestone 3 Output:** Hovering now shows a white card with a purple gradient avatar, name, and role title — the front face is fully styled.

---

### Stage 4 — Back Face Styles

```css
/* ========================
   BACK FACE
   ======================== */
.back {
  background: linear-gradient(160deg, #667eea 0%, #764ba2 100%);
  color: white;
  /* Critical: rotate back face 180deg so it starts hidden */
  transform: rotateY(180deg);
  box-shadow:
    0 20px 60px rgba(0, 0, 0, 0.3),
    0 6px 20px rgba(102, 126, 234, 0.3);
}

.back h2 {
  font-size: 22px;
  margin-bottom: 10px;
}

.back p {
  font-size: 15px;
  line-height: 1.8;
  opacity: 0.9;
}

.connect-btn {
  margin-top: 16px;
  padding: 10px 28px;
  background: white;
  color: #667eea;
  border: none;
  border-radius: 25px;
  font-size: 14px;
  font-weight: bold;
  cursor: pointer;
  box-shadow: 0 4px 12px rgba(0,0,0,0.2);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.connect-btn:hover {
  transform: scale(1.05);
  box-shadow: 0 6px 20px rgba(0,0,0,0.3);
}
```

**Milestone 4 — Final Output:**

A stunning flip card effect:
- **Default state:** White card showing avatar, name, and role — professional and clean
- **On hover:** The card smoothly rotates 180° over 0.7 seconds to reveal a purple gradient back face with contact details and a Connect button
- The flip feels physical and three-dimensional, thanks to `perspective: 1000px`
- The front hides as it turns away and the back appears as it faces the viewer
- The Connect button has its own scale hover effect on top of the flip

---

### Stage 5 — Complete Final File

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>3D Flip Card</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      background: linear-gradient(135deg, #1a1a2e, #16213e);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: Arial, sans-serif;
    }

    .flip-container {
      width: 300px;
      height: 380px;
      perspective: 1000px;
      cursor: pointer;
    }

    .flipper {
      position: relative;
      width: 100%;
      height: 100%;
      transform-style: preserve-3d;
      transition: transform 0.7s ease;
    }

    .flip-container:hover .flipper {
      transform: rotateY(180deg);
    }

    .face {
      position: absolute;
      width: 100%;
      height: 100%;
      border-radius: 20px;
      backface-visibility: hidden;
      overflow: hidden;
    }

    .face-content {
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 30px;
      text-align: center;
      gap: 12px;
    }

    /* FRONT */
    .front {
      background: linear-gradient(160deg, #ffffff, #f0f4ff);
      box-shadow: 0 20px 60px rgba(0,0,0,0.3), 0 6px 20px rgba(0,0,0,0.2);
    }

    .avatar {
      width: 80px;
      height: 80px;
      border-radius: 50%;
      background: linear-gradient(135deg, #667eea, #764ba2);
      color: white;
      font-size: 28px;
      font-weight: bold;
      line-height: 80px;
      box-shadow: 0 4px 15px rgba(102,126,234,0.5);
    }

    .front h2 { font-size: 22px; color: #1a1a2e; }
    .front .role { font-size: 14px; color: #667eea; text-transform: uppercase; letter-spacing: 1.5px; }
    .front .hint { font-size: 12px; color: #aaa; margin-top: 8px; }

    /* BACK */
    .back {
      background: linear-gradient(160deg, #667eea, #764ba2);
      color: white;
      transform: rotateY(180deg);
      box-shadow: 0 20px 60px rgba(0,0,0,0.3), 0 6px 20px rgba(102,126,234,0.3);
    }

    .back h2 { font-size: 22px; margin-bottom: 10px; }
    .back p { font-size: 15px; line-height: 1.8; opacity: 0.9; }

    .connect-btn {
      margin-top: 16px;
      padding: 10px 28px;
      background: white;
      color: #667eea;
      border: none;
      border-radius: 25px;
      font-size: 14px;
      font-weight: bold;
      cursor: pointer;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
      transition: transform 0.2s ease, box-shadow 0.2s ease;
    }

    .connect-btn:hover {
      transform: scale(1.05);
      box-shadow: 0 6px 20px rgba(0,0,0,0.3);
    }
  </style>
</head>
<body>
  <div class="flip-container">
    <div class="flipper">
      <div class="face front">
        <div class="face-content">
          <div class="avatar">TK</div>
          <h2>Temi Kola</h2>
          <p class="role">Frontend Developer</p>
          <p class="hint">Hover to see more →</p>
        </div>
      </div>
      <div class="face back">
        <div class="face-content">
          <h2>Contact</h2>
          <p>📧 temi@example.com</p>
          <p>🐦 @temi_codes</p>
          <p>💼 Lagos, Nigeria</p>
          <button class="connect-btn">Connect</button>
        </div>
      </div>
    </div>
  </div>
</body>
</html>
```

**Reflection Questions:**
1. Why does the `.back` face need `transform: rotateY(180deg)` in its default state?
2. What would happen if you removed `transform-style: preserve-3d` from `.flipper`?
3. What does `backface-visibility: hidden` do and why is it necessary?
4. How would you make the card flip vertically (top to bottom) instead of horizontally (left to right)?
5. How would you trigger the flip with a click instead of a hover?

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting `perspective` for 3D Transforms

```css
/* ❌ WRONG — no perspective means 3D looks flat */
.box {
  transform: rotateY(45deg);
  /* Without perspective, this just looks like the box got narrower */
}

/* ✅ CORRECT — perspective on the parent brings 3D to life */
.parent {
  perspective: 600px;
}
.box {
  transform: rotateY(45deg);
}
```

**Without `perspective`**, a 3D rotation just looks like the element squishing. Perspective is what creates the depth illusion.

---

### Mistake 2 — Forgetting `transform-style: preserve-3d`

```css
/* ❌ WRONG — children collapse flat */
.flipper {
  transform: rotateY(180deg);
  /* Children of flipper won't be in 3D space */
}

/* ✅ CORRECT */
.flipper {
  transform-style: preserve-3d;
  transform: rotateY(180deg);
}
```

Without `preserve-3d`, child elements are flattened onto the parent's plane and 3D positioning is lost.

---

### Mistake 3 — Wrong Transform Order

```css
/* ❌ These produce different results — don't mix them up */
transform: rotate(45deg) translate(100px, 0);
/* Rotates element, THEN moves it along the rotated axis (diagonal) */

transform: translate(100px, 0) rotate(45deg);
/* Moves element right 100px, THEN rotates it in place */
```

Always think about which operation needs to happen first. When in doubt, test both orders.

---

### Mistake 4 — Using `translate` Without Units on Non-Percentage Values

```css
/* ❌ WRONG — no units */
transform: translate(50, 30);

/* ✅ CORRECT */
transform: translate(50px, 30px);
/* OR using percentages (relative to element's own size): */
transform: translate(50%, 30%);
```

CSS values that are not `0` require units. `50` means nothing — `50px` is a valid pixel offset.

---

### Mistake 5 — Applying Multiple Transforms with Multiple `transform:` Lines

```css
/* ❌ WRONG — second transform overrides the first */
.box {
  transform: rotate(45deg);
  transform: translate(50px, 0);    /* This REPLACES the rotate — not adds to it */
}

/* ✅ CORRECT — combine them in one transform declaration */
.box {
  transform: rotate(45deg) translate(50px, 0);
}
```

CSS properties are overwritten when declared twice. Always put all transforms in a single `transform:` declaration.

---

### Mistake 6 — Forgetting `backface-visibility: hidden` in Flip Cards

```css
/* ❌ WRONG — without this, the back of the front face shows through */
.face {
  position: absolute;
}

/* ✅ CORRECT */
.face {
  position: absolute;
  backface-visibility: hidden;
}
```

Without `backface-visibility: hidden`, when the card flips, you see a mirrored ghost of the front face through the back, ruining the effect.

---

### Mistake 7 — Using `scale(0)` Instead of `display: none` to Hide

```css
/* ⚠️ scale(0) makes element invisible but it still takes up space and is clickable */
.hidden {
  transform: scale(0);
}

/* ✅ Better for truly hiding */
.hidden {
  display: none;
}
/* OR for animations, keep scale(0) but be aware the space remains */
```

`scale(0)` collapses the visual size to zero but the element still occupies layout space and can receive pointer events.

---

## Reflection Questions

1. What is the difference between 2D and 3D transforms?
2. What does `translate(50px, -30px)` do to an element?
3. What does `rotate(-90deg)` mean — which direction does it spin?
4. If you use `scale(2)`, does the surrounding layout shift? Why or why not?
5. What is `skewX` and what shape does it create?
6. Why does the ORDER of multiple transforms matter?
7. What is the `perspective` property and why is it needed for 3D transforms?
8. What does `transform-style: preserve-3d` do?
9. What does `backface-visibility: hidden` do and when do you need it?
10. What are the three axes in 3D transforms and what direction does each one go?
11. What is the difference between `rotateX()`, `rotateY()`, and `rotateZ()`?
12. How is `translateZ(100px)` different from `translateY(-100px)`?

---

## Completion Checklist

- [ ] I understand what CSS transforms are and why they are used
- [ ] I can use `translate()` to move elements without affecting layout
- [ ] I can use `rotate()` with positive and negative degree values
- [ ] I can use `scale()` to resize elements visually
- [ ] I can use `skewX()` and `skewY()` to slant elements
- [ ] I understand `matrix()` as a shorthand for all 2D transforms
- [ ] I know that transform ORDER matters
- [ ] I can combine multiple transforms in one `transform:` declaration
- [ ] I can change the pivot point with `transform-origin`
- [ ] I understand the three axes (X, Y, Z) in 3D space
- [ ] I know why `perspective` is needed for 3D transforms to look correct
- [ ] I can use `rotateX()`, `rotateY()`, and `rotateZ()`
- [ ] I understand `translateZ()` and how it creates depth
- [ ] I understand `transform-style: preserve-3d`
- [ ] I understand `backface-visibility: hidden`
- [ ] I completed the 2D code challenges (rotate badge, mirrored icon, zoom card, skewed heading)
- [ ] I completed the guided practice exercises
- [ ] I built the 3D Flip Card mini-project
- [ ] I understand all 7 common beginner mistakes and how to avoid them

---

## Lesson Summary

In this lesson you mastered **CSS 2D and 3D Transforms** — the tools that make webpages feel alive and interactive.

**2D Transforms:**
`translate()` moves elements without disturbing layout. `rotate()` spins them clockwise or counter-clockwise. `scale()` zooms them in or out visually. `skew()` slants them into parallelogram shapes. `matrix()` combines all of these into one compact six-value function. Multiple transforms can be chained in a single `transform:` declaration — and their ORDER affects the final result.

**3D Transforms:**
3D extends 2D by adding the Z-axis (depth). `perspective` on the parent container creates the illusion of 3D depth. `rotateX()`, `rotateY()`, and `rotateZ()` spin elements around each axis. `translateZ()` moves elements toward or away from the viewer. `transform-style: preserve-3d` ensures children stay in 3D space. `backface-visibility: hidden` hides the back of an element when it faces away — essential for flip card effects.

**Key professional applications you can now build:**
- Diagonal ribbon/badge overlays on product cards
- Hover-zoom galleries
- Rotating icon animations
- Skewed section dividers
- 3D perspective boxes and panels
- Full 3D flip cards for portfolios, flashcard apps, and profile pages

> Transforms are at the heart of almost every CSS animation and interactive UI component. In the next lesson, you will combine transforms with CSS Transitions and Animations to create smooth, time-based motion effects.

---

*Sources: W3Schools CSS 2D Transforms (https://www.w3schools.com/css/css3_2dtransforms.asp), CSS Scale (https://www.w3schools.com/css/css3_2dtransforms_scale.asp), CSS Skew/Matrix (https://www.w3schools.com/css/css3_2dtransforms_skew.asp), CSS 3D Transforms (https://www.w3schools.com/css/css3_3dtransforms.asp)*
