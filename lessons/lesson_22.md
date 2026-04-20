---
render_with_liquid: false
title: "CSS Position Offsets – top, right, bottom, left"
nav_order: 22
---

# Lesson 22: CSS Position Offsets — `top`, `right`, `bottom`, `left`

---

## Lesson Introduction

Imagine you are arranging furniture in a room. The sofa goes against the left wall, the lamp sits 30 centimetres from the right corner, and the coffee table is exactly in the middle. To describe each item's location, you always measure from something: from a wall, from a corner, from the edge of another piece of furniture.

CSS position offsets work exactly the same way. The four properties — `top`, `right`, `bottom`, and `left` — let you move a positioned element by pushing it away from a specific edge. They are the coordinates system of CSS layout.

In this lesson you will learn:

- What the offset properties `top`, `right`, `bottom`, and `left` actually do
- Why offsets do **nothing** without a `position` value first
- How offsets behave differently for `relative`, `absolute`, `fixed`, and `sticky` positioned elements
- How each offset direction works — and the common misconception beginners have about them
- How to use multiple offsets together to place elements precisely
- The full range of values offsets accept (pixels, percentages, negative values, `auto`)
- How `inset` shorthand combines all four offsets in one line
- Real-world patterns: tooltips, badges, overlays, sticky headers, back-to-top buttons

By the end of this lesson, you will be able to place any element exactly where you want it on a page — and understand precisely why it lands there.

> **Prerequisite check:** You should be comfortable with the `position` property and its five values (`static`, `relative`, `absolute`, `fixed`, `sticky`). You should also know basic CSS selectors, `width`/`height`, and the box model. If you completed the previous CSS position lesson, you are ready.

---

## Prerequisite Concepts

### Quick Recap: The `position` Property

Before offsets make sense, you must understand that they are completely **inactive** unless the element has a non-static `position` value. This is the single most important prerequisite for this lesson.

The five `position` values:

| Value | What it means |
|---|---|
| `static` | Default. Normal flow. **Offsets have NO effect here.** |
| `relative` | Moved from its own normal-flow position. Leaves a ghost in the flow. |
| `absolute` | Removed from flow. Positioned relative to its nearest positioned ancestor. |
| `fixed` | Removed from flow. Positioned relative to the **viewport** (browser window). |
| `sticky` | Normal flow until a scroll threshold, then sticks to the viewport. |

> **The golden rule:** `top`, `right`, `bottom`, and `left` only work on elements whose `position` is set to `relative`, `absolute`, `fixed`, or `sticky`. On `static` elements, they are completely ignored.

### What Is a "Positioned Ancestor"?

For `absolute` positioned elements, offsets are measured from the element's **nearest positioned ancestor** — the closest parent element in the HTML tree that has `position` set to anything other than `static`.

If no such ancestor exists, the offsets are measured from the `<html>` element (effectively, the page itself).

---

## Part 1: What Are the Offset Properties?

### The Four Offset Properties

| Property | What it means | Direction of push |
|---|---|---|
| `top` | Distance from the top edge | Pushes element **downward** |
| `right` | Distance from the right edge | Pushes element **leftward** |
| `bottom` | Distance from the bottom edge | Pushes element **upward** |
| `left` | Distance from the left edge | Pushes element **rightward** |

> **The most important insight about offsets:** Each property names the edge it is measured **from**, not the direction the element moves. `top: 20px` means "20px away from the top edge" — so the element moves **down**. `right: 20px` means "20px away from the right edge" — so the element moves **left**. Beginners often get confused here, so read this paragraph twice.

### The Compass Analogy

Imagine a rectangular area (a parent box, or the viewport). Each wall has a name: top wall, right wall, bottom wall, left wall.

Offset properties measure the distance between the **element's nearest edge** and the **named wall**:

```
┌───────────────────────────────┐
│         top: 30px             │
│    ┌──────────────┐           │
│    │              │           │
│    │   element    │  right:   │
│    │              │   20px    │
│    └──────────────┘           │
│                               │
└───────────────────────────────┘
```

`top: 30px` → there are 30px between the element's top edge and the container's top wall.
`right: 20px` → there are 20px between the element's right edge and the container's right wall.

---

## Part 2: Offsets with `position: relative`

### How Relative Offsets Work

When an element has `position: relative`, offsets move the element away from **where it would normally be** in the document flow. The original space the element occupied in the layout is **preserved** — like a ghost remains in the spot it came from.

Think of it like sliding a piece of paper on your desk without removing it from the pile — the empty space it left behind is still there.

### First Example — Moving Relative to Normal Position

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Relative Offsets</title>
  <style>
    .box {
      width: 120px;
      height: 60px;
      padding: 10px;
      font-family: Arial, sans-serif;
      font-size: 13px;
      text-align: center;
      line-height: 60px;
    }

    .box-normal {
      background-color: #b5e48c;
      border: 2px solid #52b788;
    }

    .box-moved {
      background-color: #90e0ef;
      border: 2px solid #0077b6;
      position: relative;
      top: 20px;      /* Move 20px DOWN from its normal top position */
      left: 40px;     /* Move 40px RIGHT from its normal left position */
    }

    .box-ghost {
      background-color: transparent;
      border: 2px dashed #aaa;
    }
  </style>
</head>
<body>

  <div class="box box-normal">Box 1 (normal)</div>
  <div class="box box-moved">Box 2 (moved)</div>
  <div class="box box-normal">Box 3 (normal)</div>

</body>
</html>
```

**Expected Output:**
- Box 1 appears in its normal position.
- Box 2 is visually shifted 20px downward and 40px to the right compared to where it normally would sit. Crucially, **the space where Box 2 would normally be is still reserved** — Box 3 sits below that empty space, not where Box 2 is visually shown.
- Box 3 appears below the empty "ghost" space left by Box 2.

**Line-by-line explanation:**

- `position: relative;` — Activates offset positioning. Without this line, `top` and `left` would do nothing.
- `top: 20px;` — Moves Box 2 **20 pixels downward** from where it would naturally sit. ("20 pixels away from where its top edge was.")
- `left: 40px;` — Moves Box 2 **40 pixels to the right** from where it would naturally sit. ("40 pixels away from where its left edge was.")
- Box 3 is not affected at all — it still sees Box 2's ghost occupying its original space.

> **Thinking prompt:** What happens if you change `top: 20px` to `bottom: 20px`? Instead of moving downward, the element would move **upward** (20px away from its bottom edge). Try it and observe the difference.

### Relative Offset with All Four Directions

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Relative Offset Directions</title>
  <style>
    .container {
      display: flex;
      gap: 30px;
      padding: 40px;
      background: #f5f5f5;
      font-family: Arial, sans-serif;
    }

    .base {
      width: 80px;
      height: 80px;
      background: #dee2e6;
      border: 2px dashed #aaa;
      font-size: 11px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #888;
    }

    .demo {
      width: 80px;
      height: 80px;
      font-size: 11px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-weight: bold;
      position: relative;
    }

    .move-top    { background: #e63946; top: -20px;  }   /* Moves UP    */
    .move-right  { background: #2a9d8f; left: 20px;  }   /* Moves RIGHT */
    .move-bottom { background: #e9c46a; bottom: -20px; color: #333; } /* Moves DOWN */
    .move-left   { background: #457b9d; right: 20px; }   /* Moves LEFT  */
  </style>
</head>
<body>

  <div class="container">
    <div>
      <div class="base">original</div>
      <div class="demo move-top">top: -20px</div>
    </div>
    <div>
      <div class="base">original</div>
      <div class="demo move-right">left: 20px</div>
    </div>
    <div>
      <div class="base">original</div>
      <div class="demo move-bottom">bottom: -20px</div>
    </div>
    <div>
      <div class="base">original</div>
      <div class="demo move-left">right: 20px</div>
    </div>
  </div>

</body>
</html>
```

**Expected Output:**
Four pairs of boxes. In each pair, the grey dashed box shows the original position, and the coloured box shows the offset result:
- Red box: shifted 20px **upward** (negative `top` = moves up).
- Green box: shifted 20px **to the right** (`left: 20px` = moves right).
- Yellow box: shifted 20px **downward** (negative `bottom` = moves down).
- Blue box: shifted 20px **to the left** (`right: 20px` = moves left).

> **Key insight on negative values:** A negative value reverses the direction. `top: -20px` means "negative 20 pixels from the top" — the element moves **upward**, not downward. This is very commonly used in real layouts.

---

## Part 3: Offsets with `position: absolute`

### How Absolute Offsets Work

When an element has `position: absolute`, it is **completely removed from the document flow** — it leaves no ghost space behind. Offsets then measure its position from the **nearest positioned ancestor** (any ancestor with `position` other than `static`).

This is the position type used most often for precise, intentional placement — badges on images, tooltips, dropdown menus, overlays.

### The Containing Block

The element that an absolutely positioned child measures its offsets from is called the **containing block**. Setting `position: relative` on a parent (without any offsets) is the standard technique for making it the containing block for its absolutely positioned children.

```css
/* Standard pattern: parent as containing block */
.parent {
  position: relative;    /* Makes this the measuring reference for children */
  /* No top/left/etc needed — we don't want to MOVE the parent */
}

.child {
  position: absolute;    /* Removed from flow */
  top: 10px;             /* 10px from the parent's TOP edge */
  right: 10px;           /* 10px from the parent's RIGHT edge */
}
```

### First Absolute Example — Corner Placement

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Absolute Positioning</title>
  <style>
    .card {
      position: relative;      /* Containing block for the badge */
      width: 250px;
      height: 180px;
      background-color: #e9ecef;
      border: 2px solid #ced4da;
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: Arial, sans-serif;
      font-size: 16px;
      color: #495057;
    }

    .badge {
      position: absolute;      /* Removed from flow, measures from .card */
      top: 10px;               /* 10px from card's top edge */
      right: 10px;             /* 10px from card's right edge */
      background-color: #e63946;
      color: white;
      font-size: 12px;
      font-weight: bold;
      padding: 4px 10px;
      border-radius: 20px;
    }
  </style>
</head>
<body>

  <div class="card">
    Product Card
    <span class="badge">NEW</span>
  </div>

</body>
</html>
```

**Expected Output:**
A grey rounded card with the text "Product Card" centred inside it. A small red pill-shaped badge labelled "NEW" sits precisely in the top-right corner of the card, 10px from the top and 10px from the right.

**Line-by-line explanation:**

- `position: relative` on `.card` — Makes the card the measuring reference (containing block). No visual change to the card itself.
- `position: absolute` on `.badge` — Removes the badge from normal flow. It no longer takes up space in the card's content.
- `top: 10px` — Places the badge 10px from the card's top inner edge.
- `right: 10px` — Places the badge 10px from the card's right inner edge.
- The badge "sticks" to the top-right corner of the card. If the card were repositioned on the page, the badge would move with it because its reference point is the card.

### All Four Corners — Absolute Placement Demo

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Four Corners</title>
  <style>
    .frame {
      position: relative;
      width: 300px;
      height: 200px;
      background-color: #f8f9fa;
      border: 2px solid #343a40;
      margin: 40px auto;
    }

    .dot {
      position: absolute;
      width: 50px;
      height: 50px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 10px;
      font-weight: bold;
      color: white;
      border-radius: 6px;
      font-family: Arial, sans-serif;
    }

    .top-left     { top: 0;    left: 0;    background: #e63946; }
    .top-right    { top: 0;    right: 0;   background: #2a9d8f; }
    .bottom-left  { bottom: 0; left: 0;    background: #e9c46a; color: #333; }
    .bottom-right { bottom: 0; right: 0;   background: #457b9d; }
  </style>
</head>
<body>

  <div class="frame">
    <div class="dot top-left">TL</div>
    <div class="dot top-right">TR</div>
    <div class="dot bottom-left">BL</div>
    <div class="dot bottom-right">BR</div>
  </div>

</body>
</html>
```

**Expected Output:**
A rectangular bordered frame. Inside, four coloured boxes sit precisely at each corner: red (top-left), green (top-right), yellow (bottom-left), and blue (bottom-right). Each box hugs its respective corner with zero gap.

**The corner placement patterns:**

```
top-left:     top: 0;    left: 0;
top-right:    top: 0;    right: 0;
bottom-left:  bottom: 0; left: 0;
bottom-right: bottom: 0; right: 0;
```

These four combinations are worth memorising — they appear constantly in real web projects.

### Centring with `top`, `left`, and `transform`

A classic technique for centring an absolutely positioned element inside its container uses offsets combined with `transform: translate`:

```css
.centred-element {
  position: absolute;
  top: 50%;           /* Move top edge to 50% of container height */
  left: 50%;          /* Move left edge to 50% of container width  */
  transform: translate(-50%, -50%);
  /* Pull element back by half ITS OWN width and height */
}
```

**Why the `transform` is needed:**
`top: 50%; left: 50%` places the element's **top-left corner** at the centre of the container. But you want the element's **centre** to be at the container's centre. `transform: translate(-50%, -50%)` shifts the element back by half its own width and height, achieving true centring.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Absolute Centering</title>
  <style>
    .container {
      position: relative;
      width: 320px;
      height: 200px;
      background-color: #dee2e6;
      border: 2px solid #6c757d;
      margin: 40px auto;
    }

    .centred {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background-color: #0d6efd;
      color: white;
      padding: 12px 24px;
      border-radius: 8px;
      font-family: Arial, sans-serif;
      font-size: 14px;
      white-space: nowrap;
    }
  </style>
</head>
<body>

  <div class="container">
    <div class="centred">Perfectly Centred</div>
  </div>

</body>
</html>
```

**Expected Output:**
A grey rectangle with a blue button visually centred both horizontally and vertically inside it.

> **Thinking prompt:** What would happen if you used `top: 50%; left: 50%` without the `transform`? The top-left corner of the blue box would be at the container's centre — the box would appear in the bottom-right quadrant instead of being centred.

---

## Part 4: Offsets with `position: fixed`

### How Fixed Offsets Work

`position: fixed` removes the element from the document flow and positions it relative to the **viewport** — the visible browser window. It stays locked to that position **even when the user scrolls**.

Offsets for `fixed` elements measure from the **edges of the browser window**:

- `top: 0` → element sits at the very top of the browser window
- `bottom: 20px` → element sits 20px above the bottom of the browser window
- `right: 20px` → element sits 20px from the right edge of the browser window

### Fixed Header Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Fixed Header</title>
  <style>
    /* Fixed header — always visible at top of viewport */
    .fixed-header {
      position: fixed;
      top: 0;          /* Pinned to top of viewport */
      left: 0;         /* Starts at left edge */
      right: 0;        /* Stretches to right edge — full width */
      height: 60px;
      background-color: #1a1a2e;
      color: white;
      display: flex;
      align-items: center;
      padding: 0 30px;
      font-family: Arial, sans-serif;
      font-size: 18px;
      font-weight: bold;
      z-index: 1000;   /* Stays above all other content */
    }

    /* Push content down so it is not hidden behind the fixed header */
    body {
      margin-top: 60px;
      font-family: Arial, sans-serif;
      padding: 20px;
    }

    p { margin-bottom: 16px; line-height: 1.7; }
  </style>
</head>
<body>

  <header class="fixed-header">My Website</header>

  <p>Scroll down to see the fixed header stay in place.</p>
  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>
  <p>More content here...</p>
  <!-- Add many paragraphs to make the page scrollable -->

</body>
</html>
```

**Expected Output:**
A dark fixed navigation header is always visible at the top of the browser window. As you scroll down, the header remains — the page content scrolls beneath it.

**Key details:**

- `top: 0; left: 0; right: 0;` — Three offsets together make the header span the full width of the viewport and sit flush at the top. Using `left: 0` and `right: 0` simultaneously stretches the element edge-to-edge (a very common professional pattern).
- `z-index: 1000` — Ensures the header stays visually above all other content when scrolling.
- `margin-top: 60px` on `body` — Compensates for the space the header "takes" from the viewport. Without this, the first 60px of page content would be hidden under the header.

### Fixed Back-to-Top Button

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Back to Top Button</title>
  <style>
    .back-to-top {
      position: fixed;
      bottom: 30px;       /* 30px from the bottom of the viewport */
      right: 30px;        /* 30px from the right of the viewport */
      width: 48px;
      height: 48px;
      background-color: #0d6efd;
      color: white;
      border: none;
      border-radius: 50%;
      font-size: 22px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }

    .back-to-top:hover {
      background-color: #0b5ed7;
    }
  </style>
</head>
<body>

  <!-- Page content goes here -->

  <button class="back-to-top" onclick="window.scrollTo(0,0)" title="Back to top">
    ↑
  </button>

</body>
</html>
```

**Expected Output:**
A circular blue button with an upward arrow sits permanently in the bottom-right corner of the viewport, 30px from both the bottom and right edges. It stays in place as the user scrolls.

---

## Part 5: Offsets with `position: sticky`

### How Sticky Offsets Work

A `sticky` element behaves like a `relative` element (in normal flow) until the user scrolls to a point where the element would scroll off the screen. At that moment, it "sticks" to the position defined by its offset, staying visible while the rest of the page continues to scroll.

The most common sticky offset:

```css
.sticky-header {
  position: sticky;
  top: 0;    /* Stick to the very top of the viewport when scrolled to */
}
```

`top: 0` means: "Once the element reaches the top edge of the viewport during scrolling, lock it there."

You can also use other offsets:

```css
.sticky-sidebar {
  position: sticky;
  top: 20px;    /* Stick 20px below the top of the viewport */
}
```

### Sticky Section Headers Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Sticky Headers</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #f8f9fa;
    }

    .section-header {
      position: sticky;
      top: 0;                    /* Sticks at top of viewport */
      background-color: #343a40;
      color: white;
      padding: 12px 24px;
      font-size: 16px;
      font-weight: bold;
      z-index: 10;
    }

    .section-content {
      padding: 20px 24px;
      background: white;
      border-bottom: 1px solid #dee2e6;
    }

    .section-content p {
      margin: 8px 0;
      color: #555;
      line-height: 1.6;
    }
  </style>
</head>
<body>

  <div class="section-header">Section A — Introduction</div>
  <div class="section-content">
    <p>Content for Section A. Scroll down to see Section B's header stick.</p>
    <p>More content...</p>
    <p>More content...</p>
    <p>More content...</p>
    <p>More content...</p>
  </div>

  <div class="section-header">Section B — Methods</div>
  <div class="section-content">
    <p>Content for Section B.</p>
    <p>More content...</p>
    <p>More content...</p>
    <p>More content...</p>
    <p>More content...</p>
  </div>

  <div class="section-header">Section C — Results</div>
  <div class="section-content">
    <p>Content for Section C.</p>
    <p>More content...</p>
    <p>More content...</p>
    <p>More content...</p>
    <p>More content...</p>
  </div>

</body>
</html>
```

**Expected Output:**
Three sections, each with a dark header. As you scroll, the current section's header sticks at the top of the viewport. When you scroll far enough to reach the next section, its header takes over the sticky position. This is a common pattern in FAQ pages, data tables, and long-form content.

> **Important sticky requirement:** A `sticky` element only sticks within the bounds of its **parent container**. Once the parent has fully scrolled out of the viewport, the sticky element disappears with it. This is why sticky works so well for section headers — each header sticks while its own section is visible.

---

## Part 6: Offset Values — The Complete Reference

Offset properties accept a wide range of value types. Understanding each one gives you precise control.

### 1. Pixel Values (`px`)

The most common. Exact, predictable distances:

```css
.element {
  position: absolute;
  top: 15px;      /* Exactly 15 pixels from the top */
  left: 30px;     /* Exactly 30 pixels from the left */
}
```

### 2. Percentage Values (`%`)

Percentages for `top` and `bottom` are calculated as a percentage of the **containing block's height**. Percentages for `left` and `right` are calculated as a percentage of the **containing block's width**.

```css
.element {
  position: absolute;
  top: 25%;       /* 25% of the containing block's height */
  left: 10%;      /* 10% of the containing block's width  */
}
```

```html
<!-- Example: element 25% down and 10% in from left -->
<div style="position: relative; width: 400px; height: 200px; background: #eee;">
  <div style="position: absolute; top: 25%; left: 10%;
              width: 80px; height: 40px; background: #0d6efd; color: white;
              display: flex; align-items: center; justify-content: center;">
    25%, 10%
  </div>
</div>
```

**Expected Output:**
Inside a 400×200px grey box, a small blue box appears with its top edge at 50px from the top (25% of 200px) and its left edge at 40px from the left (10% of 400px).

### 3. Negative Values

Negative offsets push elements in the **opposite** direction to what the positive value would do:

```css
/* Positive top: moves element down */
top: 20px;     /* Element top edge is 20px below the reference */

/* Negative top: moves element UP, partially outside the container */
top: -20px;    /* Element top edge is 20px ABOVE the reference */
```

```css
/* Useful for overlapping effects */
.overlap-badge {
  position: absolute;
  top: -10px;     /* Sticks up 10px above the top of its container */
  left: -10px;    /* Sticks out 10px to the left of its container */
}
```

Negative offsets are frequently used for:
- Making elements partially stick out of their parent
- Creating overlapping card effects
- Fine-tuning element positions in complex layouts

### 4. `auto` — The Default

`auto` is the default value for all four offset properties. When set to `auto`, the browser calculates the position naturally.

```css
.element {
  position: relative;
  top: auto;    /* Default — no offset applied */
}
```

`auto` becomes meaningful when you want to explicitly remove an offset that was set elsewhere, or when working with the `inset` shorthand.

### 5. `em` and `rem` Values

Offsets can use font-relative units, which scale with text size:

```css
.tooltip {
  position: absolute;
  top: -2.5em;    /* 2.5× the current font size above the element */
}
```

### 6. `vw` and `vh` — Viewport Units

Offset distances relative to the viewport dimensions:

```css
.centred-overlay {
  position: fixed;
  top: 10vh;     /* 10% of viewport height from the top */
  left: 10vw;    /* 10% of viewport width from the left */
}
```

---

## Part 7: The `inset` Shorthand Property

### What Is `inset`?

`inset` is a modern CSS shorthand that sets `top`, `right`, `bottom`, and `left` all in one declaration. It follows the same four-value shorthand pattern as `padding` and `margin`:

```css
/* Long form */
top: 10px;
right: 20px;
bottom: 10px;
left: 20px;

/* Shorthand with inset */
inset: 10px 20px 10px 20px;
/* Order: top  right  bottom  left */
```

### `inset` Value Patterns

```css
/* One value — all four sides the same */
inset: 20px;
/* = top: 20px; right: 20px; bottom: 20px; left: 20px; */

/* Two values — top/bottom | left/right */
inset: 10px 30px;
/* = top: 10px; right: 30px; bottom: 10px; left: 30px; */

/* Three values — top | left/right | bottom */
inset: 5px 15px 25px;
/* = top: 5px; right: 15px; bottom: 25px; left: 15px; */

/* Four values — top | right | bottom | left */
inset: 0 20px 0 20px;
/* = top: 0; right: 20px; bottom: 0; left: 20px; */
```

### The Most Powerful Use of `inset: 0`

`inset: 0` is a single-line shorthand for making an absolutely positioned element **fill its entire containing block** perfectly:

```css
/* Long form — makes element fill its parent completely */
.overlay {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}

/* Shorthand — exactly the same result */
.overlay {
  position: absolute;
  inset: 0;
}
```

### Full Overlay Example Using `inset: 0`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Image Overlay with inset: 0</title>
  <style>
    .image-card {
      position: relative;
      width: 300px;
      height: 200px;
      border-radius: 10px;
      overflow: hidden;   /* Clips the overlay to the card's rounded corners */
      display: block;
    }

    .image-card img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
    }

    /* Gradient overlay covers the entire image */
    .overlay {
      position: absolute;
      inset: 0;            /* = top:0; right:0; bottom:0; left:0 */
      background: linear-gradient(
        to top,
        rgba(0, 0, 0, 0.75) 0%,
        transparent 50%
      );
    }

    /* Text sits on top of the overlay */
    .caption {
      position: absolute;
      bottom: 14px;
      left: 16px;
      right: 16px;
      color: white;
      font-family: Arial, sans-serif;
      font-size: 16px;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <div class="image-card">
    <img src="https://via.placeholder.com/300x200/4a90d9/ffffff?text=Photo" alt="Example photo">
    <div class="overlay"></div>
    <div class="caption">Mountain Sunrise, 2026</div>
  </div>

</body>
</html>
```

**Expected Output:**
A rounded card containing a placeholder image. A dark-to-transparent gradient overlays the bottom half of the image. White bold text reading "Mountain Sunrise, 2026" sits near the bottom-left of the card.

**Why each offset is used:**

- `.overlay` with `inset: 0` — The gradient overlay stretches to every edge of the `.image-card`, covering it completely.
- `.caption` with `bottom: 14px; left: 16px; right: 16px;` — The text sits 14px above the card's bottom and has 16px of horizontal breathing room on both sides. Setting both `left` and `right` makes the text region the full width of the card minus the side padding.

---

## Part 8: Combining Multiple Offsets

### Using Two Offsets to Define Horizontal Stretch

When you set both `left` and `right` on an element with `position: absolute` or `fixed`, the element's width is determined by how much space remains between those offsets:

```css
.full-width-bar {
  position: absolute;
  left: 20px;
  right: 20px;   /* Element stretches from 20px inside left to 20px inside right */
  /* Width is automatically: parent_width - 20px - 20px */
}
```

```html
<div style="position: relative; width: 400px; height: 100px; background: #eee;">
  <div style="position: absolute; left: 20px; right: 20px;
              height: 30px; background: #0d6efd; top: 35px;">
  </div>
</div>
```

**Expected Output:**
Inside a 400px wide grey box, a blue bar stretches across it, starting 20px from the left and ending 20px from the right. The bar is effectively 360px wide (400 - 20 - 20).

### Using All Four Offsets to Fill Space (Without `inset`)

```css
.fill-parent {
  position: absolute;
  top: 10px;
  right: 10px;
  bottom: 10px;
  left: 10px;
  /* Creates a 10px inset inside the parent on all sides */
}
```

This is equivalent to `inset: 10px` and is a common pattern for creating inner frames, overlays with margins, or inset highlights.

### Offset Conflict: Using Opposite Sides Together

When you set `top` AND `bottom`, or `left` AND `right`, the element's size is determined by the remaining space. However, if `height` or `width` is also explicitly set, a conflict arises and the browser uses priority rules:

```css
/* If height is set AND top AND bottom are set: */
.element {
  position: absolute;
  top: 20px;
  bottom: 20px;
  height: 100px;    /* Conflict! Which wins? */
}
```

In this conflict, `top` and `height` take priority over `bottom` (for top-to-bottom). The `bottom` value is ignored and recalculated. To avoid confusion, beginners should use either opposing offsets (to let the browser determine size) OR one offset plus explicit `width`/`height`.

---

## Part 9: Guided Practice Exercises

### Exercise 1 — Notification Badge

**Objective:** Add a red notification count badge to a navigation icon using absolute positioning and offsets.

**Scenario:** You are building a top navigation bar. The bell icon needs a small red circular badge showing the number of unread notifications, positioned at its top-right corner.

**Steps:**
1. Create a wrapper `<div>` with `position: relative`.
2. Place a bell emoji or icon character inside.
3. Add an absolutely positioned `<span>` badge.
4. Use `top` and `right` with negative values so the badge partially overlaps the icon corner.

**Solution:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Notification Badge</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f4f8;
      display: flex;
      justify-content: center;
      padding: 60px;
    }

    .nav-icon-wrapper {
      position: relative;   /* Containing block for the badge */
      display: inline-block;
    }

    .nav-icon {
      font-size: 36px;
      color: #343a40;
      cursor: pointer;
      display: block;
    }

    .badge {
      position: absolute;
      top: -6px;           /* Overlap 6px above the icon's top edge */
      right: -8px;         /* Overlap 8px past the icon's right edge */
      min-width: 20px;
      height: 20px;
      background-color: #e63946;
      color: white;
      font-size: 11px;
      font-weight: bold;
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 0 5px;
      border: 2px solid white;  /* White ring separates badge from icon */
    }
  </style>
</head>
<body>

  <div class="nav-icon-wrapper">
    <span class="nav-icon">🔔</span>
    <span class="badge">5</span>
  </div>

</body>
</html>
```

**Expected Output:**
A bell icon with a red circular badge showing "5" positioned at its top-right, partially overlapping the icon corner. A white ring separates the badge from the icon for visual clarity.

**Self-check Questions:**
- Why do we use negative values for `top` and `right` on the badge? *(Answer: Negative values push the badge outside/above the reference point, making it overlap the corner rather than sit inside the icon.)*
- What does `position: relative` on the wrapper do — but NOT do? *(Answer: It makes the wrapper the containing block. It does NOT visually move the wrapper.)*
- If you change `right: -8px` to `left: -8px`, where does the badge go? *(Answer: It moves to the top-left corner of the icon.)*

---

### Exercise 2 — Tooltip on Hover

**Objective:** Build a tooltip that appears above a button when hovered, using absolute positioning.

**Scenario:** A "Help" button needs a tooltip that explains what it does. The tooltip should appear above the button and be centred over it.

**Solution:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>CSS Tooltip</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 200px;
      background: #f5f5f5;
    }

    /* Wrapper acts as containing block */
    .tooltip-wrapper {
      position: relative;
      display: inline-block;
    }

    .help-button {
      background-color: #6c757d;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 6px;
      font-size: 14px;
      cursor: pointer;
    }

    /* Tooltip — hidden by default */
    .tooltip-text {
      position: absolute;
      bottom: calc(100% + 10px);
      /* 100% = height of the button, +10px = 10px gap above button */
      left: 50%;
      transform: translateX(-50%);
      /* Centres the tooltip over the button */
      background-color: #212529;
      color: white;
      font-size: 13px;
      padding: 8px 14px;
      border-radius: 6px;
      white-space: nowrap;
      opacity: 0;              /* Hidden by default */
      pointer-events: none;
      transition: opacity 0.2s ease;
    }

    /* Small triangle pointer */
    .tooltip-text::after {
      content: '';
      position: absolute;
      top: 100%;               /* Below the tooltip box */
      left: 50%;
      transform: translateX(-50%);
      border: 6px solid transparent;
      border-top-color: #212529;
    }

    /* Show tooltip on hover */
    .tooltip-wrapper:hover .tooltip-text {
      opacity: 1;
    }
  </style>
</head>
<body>

  <div class="tooltip-wrapper">
    <button class="help-button">? Help</button>
    <div class="tooltip-text">Click for detailed documentation</div>
  </div>

</body>
</html>
```

**Expected Output:**
A grey help button. When hovered, a dark tooltip with the text "Click for detailed documentation" appears above the button with a small downward-pointing triangle connecting them.

**Offset breakdown:**

- `bottom: calc(100% + 10px)` — Places the tooltip above the button. `100%` equals the button's full height, and `+10px` adds a gap. So the tooltip's bottom edge sits 10px above the button's top edge.
- `left: 50%` — Moves the tooltip's left edge to the button's horizontal midpoint.
- `transform: translateX(-50%)` — Shifts the tooltip left by half its own width, perfectly centring it over the button.
- `position: absolute` on `.tooltip-text::after` — The triangle arrow is also absolutely positioned relative to the tooltip box itself.
- `top: 100%` on the arrow — Places it just below the tooltip box.

---

### Exercise 3 — Image Cards with Hover Overlay

**Objective:** Create a photo card where a description overlay slides in from the bottom on hover, using absolute positioning and `inset`.

**Solution:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Image Card Overlay</title>
  <style>
    body {
      background: #e9ecef;
      display: flex;
      justify-content: center;
      gap: 24px;
      padding: 40px;
      font-family: Arial, sans-serif;
    }

    .photo-card {
      position: relative;
      width: 240px;
      height: 180px;
      border-radius: 10px;
      overflow: hidden;
      cursor: pointer;
    }

    .photo-card img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
      transition: transform 0.3s ease;
    }

    .photo-card:hover img {
      transform: scale(1.05);  /* Subtle zoom on hover */
    }

    /* Overlay starts hidden below the card */
    .photo-overlay {
      position: absolute;
      left: 0;
      right: 0;
      bottom: -100%;          /* Hidden below card initially */
      background: rgba(13, 27, 62, 0.88);
      color: white;
      padding: 16px;
      transition: bottom 0.3s ease;
    }

    /* Slide up on hover */
    .photo-card:hover .photo-overlay {
      bottom: 0;              /* Slides up to cover bottom of card */
    }

    .photo-overlay h4 {
      margin: 0 0 6px;
      font-size: 14px;
    }

    .photo-overlay p {
      margin: 0;
      font-size: 12px;
      color: #b0c4de;
      line-height: 1.4;
    }
  </style>
</head>
<body>

  <div class="photo-card">
    <img src="https://via.placeholder.com/240x180/4a90d9/fff?text=Photo+1" alt="City">
    <div class="photo-overlay">
      <h4>City Lights</h4>
      <p>Downtown at dusk, captured from the observation deck.</p>
    </div>
  </div>

  <div class="photo-card">
    <img src="https://via.placeholder.com/240x180/52b788/fff?text=Photo+2" alt="Forest">
    <div class="photo-overlay">
      <h4>Morning Forest</h4>
      <p>Mist between the pine trees at sunrise.</p>
    </div>
  </div>

  <div class="photo-card">
    <img src="https://via.placeholder.com/240x180/e63946/fff?text=Photo+3" alt="Desert">
    <div class="photo-overlay">
      <h4>Desert Dunes</h4>
      <p>The shifting sands of the Sahara at golden hour.</p>
    </div>
  </div>

</body>
</html>
```

**Expected Output:**
Three photo cards side by side. On hover over any card, a dark overlay panel slides up from the bottom, revealing a title and description. The image also subtly zooms in.

**How the slide animation works:**

- `.photo-overlay` starts at `bottom: -100%` — completely hidden below the card's bottom edge. Because the parent has `overflow: hidden`, anything below the card's boundary is invisible.
- On hover, `bottom: 0` slides it into view.
- `transition: bottom 0.3s ease` — Animates the `bottom` value change over 0.3 seconds.

---

## Part 10: Mini Project — Dashboard Notification System

### Project Goal

Build a user dashboard card that uses offsets throughout: a sticky header, an absolutely positioned user avatar with a status badge, a fixed "help" button, and a tooltip.

### Stage 1 — Page Shell and Sticky Bar

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dashboard</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      background: #f0f2f5;
      min-height: 200vh;   /* Tall enough to scroll */
    }

    /* FIXED — stays at top when scrolling */
    .top-bar {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      height: 56px;
      background: #1a1a2e;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 24px;
      z-index: 100;
    }

    .top-bar .logo {
      color: white;
      font-size: 18px;
      font-weight: bold;
      letter-spacing: -0.5px;
    }

    .top-bar .nav-links a {
      color: #adb5bd;
      text-decoration: none;
      font-size: 14px;
      margin-left: 20px;
    }

    .top-bar .nav-links a:hover { color: white; }

    .page-content {
      margin-top: 56px;    /* Offset for fixed top bar */
      padding: 32px 24px;
      max-width: 900px;
      margin-left: auto;
      margin-right: auto;
      margin-top: 88px;    /* 56px bar + 32px breathing room */
    }
  </style>
</head>
<body>

  <header class="top-bar">
    <div class="logo">Dashboard</div>
    <nav class="nav-links">
      <a href="#">Overview</a>
      <a href="#">Reports</a>
      <a href="#">Settings</a>
    </nav>
  </header>

  <div class="page-content">
    <!-- Cards go here next -->
  </div>

</body>
</html>
```

**Milestone 1 Output:** A dark fixed navigation bar always visible at the top. The page content starts below it with comfortable spacing.

### Stage 2 — Profile Card with Avatar Badge

```html
<!-- Add inside .page-content -->
<div class="profile-card">

  <!-- Avatar with online status badge -->
  <div class="avatar-wrapper">
    <div class="avatar">AJ</div>
    <span class="status-dot"></span>
  </div>

  <div class="profile-info">
    <h2>Alex Johnson</h2>
    <p class="role">Senior Developer</p>
    <p class="email">alex.johnson@company.com</p>
  </div>

  <!-- Corner label -->
  <span class="card-label">PRO</span>

</div>
```

```css
/* Add to <style> */

.profile-card {
  position: relative;       /* Containing block for .card-label */
  background: white;
  border-radius: 14px;
  padding: 28px;
  display: flex;
  align-items: center;
  gap: 20px;
  box-shadow: 0 2px 12px rgba(0,0,0,0.07);
  margin-bottom: 24px;
}

/* Avatar wrapper is containing block for the status dot */
.avatar-wrapper {
  position: relative;
  flex-shrink: 0;
}

.avatar {
  width: 68px;
  height: 68px;
  border-radius: 50%;
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
  font-size: 22px;
  font-weight: bold;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Green online dot — bottom-right of avatar */
.status-dot {
  position: absolute;
  bottom: 2px;
  right: 2px;
  width: 16px;
  height: 16px;
  background: #2dc653;
  border-radius: 50%;
  border: 2.5px solid white;
}

.profile-info h2 {
  font-size: 20px;
  color: #1a1a2e;
  margin-bottom: 4px;
}

.profile-info .role {
  font-size: 14px;
  color: #6c757d;
  margin-bottom: 2px;
}

.profile-info .email {
  font-size: 13px;
  color: #adb5bd;
}

/* PRO badge — top-right corner of the card */
.card-label {
  position: absolute;
  top: 16px;
  right: 16px;
  background: #f7b731;
  color: #7d5a00;
  font-size: 11px;
  font-weight: bold;
  padding: 3px 10px;
  border-radius: 20px;
  letter-spacing: 0.5px;
}
```

**Milestone 2 Output:** A white profile card with a gradient avatar showing initials "AJ". A green dot sits at the bottom-right of the avatar (online indicator). A gold "PRO" pill badge is pinned to the top-right corner of the entire card.

### Stage 3 — Stats Row with Sticky Section Label

```html
<!-- Add after .profile-card inside .page-content -->

<div class="section-label sticky-label">This Month's Stats</div>

<div class="stats-row">
  <div class="stat-card">
    <div class="stat-number">142</div>
    <div class="stat-title">Commits</div>
  </div>
  <div class="stat-card">
    <div class="stat-number">28</div>
    <div class="stat-title">Pull Requests</div>
  </div>
  <div class="stat-card">
    <div class="stat-number">99%</div>
    <div class="stat-title">Uptime</div>
  </div>
  <div class="stat-card">
    <span class="stat-badge new">NEW</span>
    <div class="stat-number">7</div>
    <div class="stat-title">Deployments</div>
  </div>
</div>
```

```css
.section-label {
  font-size: 13px;
  font-weight: 700;
  color: #6c757d;
  letter-spacing: 0.8px;
  text-transform: uppercase;
  margin-bottom: 12px;
  padding: 8px 0;
  background: #f0f2f5;
}

/* STICKY — label sticks just below the fixed top bar */
.sticky-label {
  position: sticky;
  top: 56px;   /* Offset equals the height of the fixed top-bar */
  z-index: 50;
}

.stats-row {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
  margin-bottom: 24px;
}

.stat-card {
  position: relative;   /* Containing block for .stat-badge */
  background: white;
  border-radius: 12px;
  padding: 20px 16px;
  text-align: center;
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
}

.stat-number {
  font-size: 32px;
  font-weight: bold;
  color: #1a1a2e;
  margin-bottom: 4px;
}

.stat-title {
  font-size: 13px;
  color: #6c757d;
}

/* Badge pinned to top-right of stat card */
.stat-badge {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 10px;
  font-weight: bold;
  padding: 2px 7px;
  border-radius: 20px;
}

.stat-badge.new {
  background: #d0f4de;
  color: #1e7e34;
}
```

**Milestone 3 Output:** A sticky section label reading "THIS MONTH'S STATS" (sticks just below the fixed top bar on scroll) followed by four white stat cards in a grid. The "Deployments" card has a small green "NEW" badge in its top-right corner.

### Stage 4 — Fixed Help Button with Tooltip (Final Stage)

```html
<!-- Add just before </body> -->

<div class="help-btn-wrapper">
  <button class="help-btn">?</button>
  <div class="help-tooltip">Need help? View our docs →</div>
</div>
```

```css
/* FIXED — always visible in the bottom-left of the viewport */
.help-btn-wrapper {
  position: fixed;
  bottom: 28px;
  left: 28px;
  z-index: 200;
}

.help-btn {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: #0d6efd;
  color: white;
  font-size: 20px;
  font-weight: bold;
  border: none;
  cursor: pointer;
  box-shadow: 0 4px 14px rgba(13,110,253,0.4);
  transition: transform 0.2s ease;
}

.help-btn:hover {
  transform: scale(1.1);
}

/* Tooltip — appears to the right of the help button */
.help-tooltip {
  position: absolute;
  bottom: 50%;               /* Vertically align with button centre */
  left: calc(100% + 12px);   /* 12px to the right of the button */
  transform: translateY(50%);
  background: #212529;
  color: white;
  font-size: 13px;
  font-family: Arial, sans-serif;
  padding: 8px 14px;
  border-radius: 8px;
  white-space: nowrap;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.2s ease;
}

.help-btn-wrapper:hover .help-tooltip {
  opacity: 1;
}
```

**Final Milestone Output:**
A complete dashboard with:
- A **fixed** top navigation bar (`top: 0; left: 0; right: 0`)
- A profile card with a **relative** containing block holding an **absolute** status dot (`bottom: 2px; right: 2px`) and an **absolute** PRO badge (`top: 16px; right: 16px`)
- A **sticky** section label (`top: 56px`) that sticks below the top bar
- **Absolute** NEW badge on a stat card (`top: 10px; right: 10px`)
- A **fixed** help button (`bottom: 28px; left: 28px`) with a tooltip using `left: calc(100% + 12px)`

Every single offset technique from this lesson is demonstrated in one cohesive, real-world project.

---

## Part 11: The Position Offset Code Challenges

These challenges match the W3Schools CSS position offset code challenges format.

### Challenge 1 — Move a Relative Element Down and Right

**Task:** Move a `<div>` with `id="myDIV"` 30px down and 50px to the right from its normal position using relative positioning.

```html
<style>
  #myDIV {
    /* Your code here */
    width: 200px;
    height: 80px;
    background-color: lightblue;
    padding: 10px;
  }
</style>
<div id="myDIV">I am moved from my normal position.</div>
```

**Solution:**

```css
#myDIV {
  position: relative;
  top: 30px;
  left: 50px;
  width: 200px;
  height: 80px;
  background-color: lightblue;
  padding: 10px;
}
```

---

### Challenge 2 — Pin an Element to the Top-Right Corner

**Task:** Position a child `<div>` in the **top-right corner** of its parent, 10px from the top and 10px from the right.

```html
<style>
  .parent {
    position: relative;
    width: 300px;
    height: 200px;
    background-color: lightgrey;
  }

  .child {
    /* Your code here */
    width: 60px;
    height: 30px;
    background-color: coral;
  }
</style>

<div class="parent">
  <div class="child">TOP RIGHT</div>
</div>
```

**Solution:**

```css
.child {
  position: absolute;
  top: 10px;
  right: 10px;
  width: 60px;
  height: 30px;
  background-color: coral;
}
```

---

### Challenge 3 — Fix an Element to the Bottom of the Viewport

**Task:** Make a `<div>` stick permanently to the **bottom-centre** of the browser window using fixed positioning.

```html
<style>
  .bottom-bar {
    /* Your code here */
    width: 300px;
    padding: 14px;
    background-color: #333;
    color: white;
    text-align: center;
    border-radius: 8px 8px 0 0;
  }
</style>

<div class="bottom-bar">Fixed Bottom Bar</div>
```

**Solution:**

```css
.bottom-bar {
  position: fixed;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 300px;
  padding: 14px;
  background-color: #333;
  color: white;
  text-align: center;
  border-radius: 8px 8px 0 0;
}
```

---

### Challenge 4 — Centre an Element Absolutely Inside Its Parent

**Task:** Absolutely centre a `<div>` both horizontally and vertically inside its parent.

```html
<style>
  .parent {
    position: relative;
    width: 350px;
    height: 250px;
    background-color: #e0e0e0;
    border: 2px solid #999;
  }

  .centred {
    /* Your code here */
    width: 120px;
    height: 60px;
    background-color: #0d6efd;
    color: white;
    text-align: center;
    line-height: 60px;
  }
</style>

<div class="parent">
  <div class="centred">Centred!</div>
</div>
```

**Solution:**

```css
.centred {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 120px;
  height: 60px;
  background-color: #0d6efd;
  color: white;
  text-align: center;
  line-height: 60px;
}
```

---

### Challenge 5 — Full-Cover Overlay Using `inset`

**Task:** Make an overlay `<div>` cover its parent **completely** on all sides using the `inset` shorthand.

```html
<style>
  .parent {
    position: relative;
    width: 300px;
    height: 200px;
    background-color: lightblue;
  }

  .overlay {
    /* Your code here — use inset shorthand */
    background-color: rgba(0, 0, 0, 0.5);
  }
</style>

<div class="parent">
  <div class="overlay"></div>
</div>
```

**Solution:**

```css
.overlay {
  position: absolute;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.5);
}
```

---

### Challenge 6 — Sticky Sidebar Label

**Task:** Make a section label inside a scrollable container stick to the top of the container when scrolled.

```html
<style>
  .scroll-container {
    height: 200px;
    overflow-y: scroll;
    border: 1px solid #ccc;
    padding: 0 16px;
  }

  .sticky-title {
    /* Your code here */
    background-color: white;
    padding: 8px 0;
    font-weight: bold;
    border-bottom: 1px solid #ddd;
  }
</style>

<div class="scroll-container">
  <div class="sticky-title">Section Title</div>
  <p>Item 1</p><p>Item 2</p><p>Item 3</p>
  <p>Item 4</p><p>Item 5</p><p>Item 6</p>
  <p>Item 7</p><p>Item 8</p><p>Item 9</p>
</div>
```

**Solution:**

```css
.sticky-title {
  position: sticky;
  top: 0;
  background-color: white;
  padding: 8px 0;
  font-weight: bold;
  border-bottom: 1px solid #ddd;
}
```

---

## Part 12: Common Beginner Mistakes

### Mistake 1 — Using Offsets Without Setting `position`

```css
/* WRONG: position is still 'static' by default. top and left do nothing. */
.box {
  top: 20px;
  left: 30px;
}

/* CORRECT: Always set position first */
.box {
  position: relative;   /* or absolute, fixed, sticky */
  top: 20px;
  left: 30px;
}
```

**Visual result of the mistake:** The element stays exactly in its normal flow position. The offset declarations are silently ignored. This is the number one source of confusion for beginners using offsets.

---

### Mistake 2 — Thinking `top` Moves an Element Up

```css
/* WRONG thinking: "top: 20px will move it toward the top of the page" */
.element {
  position: relative;
  top: 20px;    /* This actually moves it DOWN (away from the top) */
}

/* To move it UP, use a negative value: */
.element {
  position: relative;
  top: -20px;   /* This moves it UP (reduces distance from top) */
}
```

**Correct mental model:** `top: 20px` means "set the distance between this element's top edge and its reference point's top edge to 20px." Adding distance from the top means the element moves downward.

---

### Mistake 3 — Forgetting `position: relative` on the Parent for `absolute` Children

```css
/* WRONG: No positioned ancestor — .badge measures from <html> element */
.card {
  /* No position set */
  width: 200px;
}

.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  /* This badge will fly to the top-right of the ENTIRE PAGE, not the card */
}

/* CORRECT: Make the parent the containing block */
.card {
  position: relative;   /* Now .badge measures from .card */
  width: 200px;
}

.badge {
  position: absolute;
  top: 10px;
  right: 10px;
}
```

**Visual result of the mistake:** The absolutely positioned child ends up somewhere completely unexpected — usually at a corner of the entire page instead of inside its parent.

---

### Mistake 4 — Using `margin` When `offset` Is Needed (or Vice Versa)

```css
/* WRONG for precise overlay positioning — margin pushes all siblings too */
.badge {
  margin-top: -10px;
  margin-right: -10px;
}

/* CORRECT — absolute offset only moves THIS element */
.badge {
  position: absolute;
  top: -10px;
  right: -10px;
}
```

**When to use which:**
- Use `margin` for spacing between elements in normal flow.
- Use offset properties (`top`, `right`, etc.) for intentional precise placement with `position: relative/absolute/fixed/sticky`.

---

### Mistake 5 — Forgetting `margin-top` Compensation for a Fixed Header

```css
/* Fixed header — 60px tall */
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 60px;
}

/* WRONG: First 60px of body content hidden under the header */
body {
  /* No compensation */
}

/* CORRECT: Push body content below the header */
body {
  margin-top: 60px;   /* Same as the header height */
  /* Or use padding-top: 60px; */
}
```

**Visual result:** The beginning of the page content is hidden beneath the fixed header. Users cannot see the first section of the page without scrolling up — but they are already at the top.

---

### Mistake 6 — `inset: 0` Without `position: absolute`

```css
/* WRONG: inset is an offset property — needs position set */
.overlay {
  inset: 0;    /* Does nothing without position */
  background: rgba(0,0,0,0.5);
}

/* CORRECT */
.overlay {
  position: absolute;
  inset: 0;
  background: rgba(0,0,0,0.5);
}
```

---

### Mistake 7 — Confusing `sticky` Not Working

```css
/* STICKY DOES NOT WORK in these situations: */

/* 1. No offset value specified */
.sticky-nav {
  position: sticky;
  /* No top/bottom — browser doesn't know WHEN to stick. Always set top: Npx */
}

/* 2. Parent has overflow: hidden or overflow: auto */
.container {
  overflow: hidden;   /* This breaks sticky positioning of children */
}

/* CORRECT sticky setup */
.sticky-nav {
  position: sticky;
  top: 0;    /* Required — defines the sticking threshold */
}
```

---

## Part 13: Reflection Questions

Think through each question to deepen your understanding:

1. **An element has `position: relative; top: 40px; left: 20px`. Describe in plain English exactly where it ends up relative to its normal position.**

2. **Why does setting `position: relative` on a parent container (without any offset values) not visually move the parent — yet it changes the behaviour of absolutely positioned children inside it?**

3. **You place a badge using `position: absolute; top: -8px; right: -8px`. What does the negative value on each offset actually do, and why is it commonly used for badges?**

4. **What is the difference between `position: fixed; top: 0` and `position: sticky; top: 0`? In what scenario would each one be the right choice?**

5. **An absolutely positioned element has `left: 0` and `right: 0` set simultaneously. What does this do to its width, and why?**

6. **Why must a `sticky` element always have an offset (like `top: 0`) for it to actually stick? What happens if `position: sticky` is set but no offset is provided?**

7. **You write `inset: 0` on an element. Write out the four equivalent individual offset properties this shorthand replaces. What is this pattern commonly used for?**

8. **The tooltip in Exercise 2 uses `bottom: calc(100% + 10px)`. Break this down: what does `100%` refer to, and what does the `+ 10px` achieve?**

---

## Completion Checklist

Before moving to the next lesson, confirm you can check off every item:

- [ ] I understand that `top`, `right`, `bottom`, and `left` do nothing on `position: static` elements.
- [ ] I know that each offset names the edge it is **measured from**, not the direction the element moves.
- [ ] I can use offsets with `position: relative` to nudge an element from its normal flow position.
- [ ] I understand that `relative` offsets leave a "ghost" space in the original flow position.
- [ ] I can set `position: relative` on a parent to make it the containing block for absolutely positioned children.
- [ ] I can use `position: absolute` with offsets to precisely place elements inside a container.
- [ ] I know the four corner placement patterns using combinations of `top`, `right`, `bottom`, `left`.
- [ ] I can use `top: 50%; left: 50%; transform: translate(-50%, -50%)` to perfectly centre an absolute element.
- [ ] I can use offsets with `position: fixed` to pin elements to the viewport.
- [ ] I know to add `margin-top` compensation on `body` to account for a fixed header.
- [ ] I can use `position: sticky` with `top: N` to make elements stick at a scroll threshold.
- [ ] I understand that `sticky` only sticks within the bounds of its parent container.
- [ ] I know all offset value types: `px`, `%`, negative values, `auto`, `em`, `vw`/`vh`.
- [ ] I can use the `inset` shorthand and understand its value patterns.
- [ ] I understand what `inset: 0` does and when to use it.
- [ ] I know that `left: 0` and `right: 0` together stretch an element horizontally.
- [ ] I completed all three guided practice exercises (badge, tooltip, image overlay).
- [ ] I completed all six code challenges.
- [ ] I completed the dashboard mini-project.
- [ ] I can identify and fix all seven common beginner mistakes.

---

## Lesson Summary

In this lesson you mastered the four CSS offset properties — `top`, `right`, `bottom`, and `left` — which work together with the `position` property to place elements precisely anywhere on a page.

The core insight: each offset names the **edge it measures from**, not the direction of movement. `top: 20px` means "20 pixels away from the top edge" — the element moves downward. Negative values reverse the direction. This is the single most important concept to internalise.

Offsets behave differently depending on the `position` value:

With **`relative`**, offsets move an element from its own normal-flow position while leaving a ghost space behind. This is useful for subtle fine-tuning and for establishing a containing block.

With **`absolute`**, offsets position the element inside its nearest positioned ancestor. Setting `position: relative` on a parent (with no offsets) is the standard way to create a precise, self-contained positioning context — essential for badges, labels, tooltips, and overlays.

With **`fixed`**, offsets anchor the element to the viewport — always visible regardless of scrolling. Essential for navigation bars, floating action buttons, and chat widgets.

With **`sticky`**, offsets define the scroll threshold at which the element locks in place — perfect for section headers and persistent navigation within scrollable containers.

The `inset` shorthand elegantly combines all four offsets. Its most powerful form, `inset: 0`, fills an element to every edge of its containing block in a single declaration — the foundation of every full-cover overlay in web design.

Together, these tools let you build every UI pattern that requires precise placement: hover tooltips, notification badges, image overlays, sticky navigation, and fixed utility buttons. They are among the most frequently used properties in professional CSS.

---

*Continue to Lesson 23 to learn about CSS Z-index — controlling which elements appear in front of or behind others when they overlap.*
