---
render_with_liquid: false
title: "Lesson 21: CSS Position — Static, Relative, Fixed, Absolute, and Sticky"
nav_order: 21
---

# Lesson 21: CSS Position — Static, Relative, Fixed, Absolute, and Sticky

---

## Lesson Introduction

Up until now, every element you have placed on a page has followed the same rule: elements stack from top to bottom, one after the other, in the order you wrote them in the HTML. This is called the **normal document flow**.

But look at any real website and you will immediately see elements that break this rule. A navigation bar that stays at the top of the screen even when you scroll. A tooltip that hovers just above a button. A banner image with a text label pinned to its bottom-left corner. A sidebar that scrolls with you until it reaches the top, then locks in place.

All of this is achieved with a single CSS property: `position`.

The `position` property is one of the most powerful and most misunderstood concepts in CSS. When you truly understand it, you gain the ability to place any element anywhere on the page — and keep it there through scrolling, resizing, and user interaction.

This lesson covers all five position values — `static`, `relative`, `fixed`, `absolute`, and `sticky` — fully and from scratch, progressively building toward a real-world project you can use immediately.

---

## Prerequisite Concepts

### What is the Normal Document Flow?

When a browser renders a page, it places every element in sequence, from top to bottom, following the HTML order. Block elements like `<div>`, `<p>`, `<h1>` take up the full width and stack vertically. Inline elements like `<span>`, `<a>` sit side by side in a line.

This default stacking is called the **normal document flow** or **normal flow**.

```html
<div>Box One</div>
<div>Box Two</div>
<div>Box Three</div>
```

**Expected output in browser:**
```
┌──────────────────────┐
│ Box One              │
└──────────────────────┘
┌──────────────────────┐
│ Box Two              │
└──────────────────────┘
┌──────────────────────┐
│ Box Three            │
└──────────────────────┘
```

They stack vertically because that is normal flow.

### What are the Offset Properties?

When you take an element out of normal flow and position it, you control its location using four **offset properties**:

| Property | Meaning |
|---|---|
| `top` | Distance from the top edge of the reference point |
| `bottom` | Distance from the bottom edge of the reference point |
| `left` | Distance from the left edge of the reference point |
| `right` | Distance from the right edge of the reference point |

These properties do **nothing** unless `position` is set to something other than `static`. They always work together with the `position` property.

> **Important:** The "reference point" changes depending on which position value you use. This is the key concept to understand in this lesson.

---

## Part 1 — `position: static` (The Default)

### What is `position: static`?

Every HTML element has `position: static` by default. It means the element follows normal document flow and is **not** positioned by offset properties.

You almost never write `position: static` yourself. It is the starting state of every element unless you change it.

```css
div {
  position: static;   /* This is the default — no change */
  top: 50px;          /* This does NOTHING when position is static */
  left: 50px;         /* This also does NOTHING */
}
```

**Expected output:** The `top` and `left` values are completely ignored. The element sits exactly where it would in normal flow.

> **Key rule:** Offset properties (`top`, `bottom`, `left`, `right`) only work when `position` is `relative`, `absolute`, `fixed`, or `sticky`. They are ignored on `static` elements.

**Example — static in action:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div.static-box {
      position: static;
      background-color: lightblue;
      padding: 20px;
      width: 200px;
    }
  </style>
</head>
<body>
  <div class="static-box">I am static (default)</div>
  <div class="static-box">I follow normal flow</div>
</body>
</html>
```

**Expected output:** Two light blue boxes stacked vertically, exactly as they appear in the HTML — no special positioning applied.

---

## Part 2 — `position: relative`

### What is `position: relative`?

`position: relative` means the element is positioned **relative to where it would normally be** in the document flow.

Think of it this way: the element is placed in the page as normal, and then you can nudge it from that original position using offset properties. The original space it occupied **remains reserved** — no other element fills in the gap.

> **Analogy:** Imagine you are standing in a queue. `position: relative` means you can lean forward or sideways, but your spot in the queue is still reserved for you. Nobody moves in to take your place.

### Syntax

```css
div.moved {
  position: relative;
  top: 20px;    /* Move DOWN 20px from its normal position */
  left: 40px;   /* Move RIGHT 40px from its normal position */
}
```

> **Confusing but important:** `top: 20px` pushes the element DOWN (away from the top). `left: 40px` pushes the element RIGHT (away from the left). Think of the offset as the amount of space pushed in from that edge.

### Simple Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      width: 180px;
      padding: 16px;
      font-family: Arial, sans-serif;
    }

    div.normal {
      background-color: #cfe2ff;
    }

    div.shifted {
      position: relative;
      top: 20px;
      left: 40px;
      background-color: #ffcdd2;
    }

    div.after {
      background-color: #c8e6c9;
    }
  </style>
</head>
<body>
  <div class="normal">Box 1 (normal)</div>
  <div class="shifted">Box 2 (relative — shifted 20px down, 40px right)</div>
  <div class="after">Box 3 (normal — notice it does NOT move up)</div>
</body>
</html>
```

**Expected output:**
- Box 1: sits in normal flow
- Box 2: visually shifted — it appears 20px lower and 40px to the right compared to where it would normally be. **But the gap where it would have been is still there.** Box 3 does not move up to fill the gap.
- Box 3: sits right where it always would — it does not know Box 2 moved.

> **Thinking prompt:** What happens if you change `top: 20px` to `top: -20px`? The element moves UP — because negative values reverse direction.

### Using Negative Offsets

```css
div.up-and-left {
  position: relative;
  top: -10px;    /* Moves 10px UPWARD */
  left: -20px;   /* Moves 20px to the LEFT */
}
```

Negative values pull the element in the opposite direction from the named edge.

### Why `position: relative` Matters Beyond Moving

`position: relative` has a second very important purpose: **it creates a positioning context for child elements with `position: absolute`**. You will see this in Part 4. This is often the main reason developers use `relative` — not to move the element at all, but purely to set up a container that `absolute` children can be placed inside.

---

## Part 3 — `position: fixed`

### What is `position: fixed`?

`position: fixed` takes the element completely **out of the normal document flow** and fixes it to a position relative to the **browser viewport** (the visible window area). It stays in that exact spot even when the user scrolls.

> **Analogy:** Imagine a sticky note on your screen. No matter how much you scroll the document behind it, the sticky note never moves. That is `position: fixed`.

The reference point for `fixed` is always the **viewport** — the browser window itself.

### Syntax

```css
div.fixed-navbar {
  position: fixed;
  top: 0;       /* Pinned to the very top of the viewport */
  left: 0;      /* Pinned to the very left edge */
  width: 100%;  /* Stretches across the full width of the viewport */
}
```

### Simple Example — Fixed Top Navigation Bar

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
    }

    nav.fixed-nav {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      background-color: #1a237e;
      color: white;
      padding: 16px 24px;
      z-index: 1000;   /* Ensures it sits on top of other content */
    }

    main {
      margin-top: 60px;  /* Prevents content hiding under the fixed nav */
      padding: 20px;
    }

    p {
      margin-bottom: 20px;
    }
  </style>
</head>
<body>

  <nav class="fixed-nav">My Fixed Navigation Bar</nav>

  <main>
    <p>Scroll down to see the navigation bar stay fixed at the top.</p>
    <p>Paragraph 2. Keep scrolling.</p>
    <p>Paragraph 3. The nav doesn't move!</p>
    <p>Paragraph 4.</p>
    <p>Paragraph 5.</p>
    <p>Paragraph 6.</p>
    <p>Paragraph 7.</p>
    <p>Paragraph 8.</p>
  </main>

</body>
</html>
```

**Line by line — new properties:**
- `position: fixed` — removes the nav from normal flow and locks it to the viewport
- `top: 0; left: 0;` — pins it to the top-left corner of the window
- `width: 100%;` — stretches across the full browser width
- `z-index: 1000;` — ensures it renders on top of all other content when things overlap. We cover z-index in a later lesson; for now, just know that higher numbers sit on top.
- `margin-top: 60px;` on `<main>` — because fixed elements are removed from flow, the main content would slide up underneath the nav. We push it down 60px (the height of the nav) to prevent overlap.

**Expected output:** A dark navy bar stays pinned at the top of the viewport while all the paragraphs scroll behind it.

> **Thinking prompt:** What would happen if you removed `margin-top: 60px` from `<main>`? The first paragraph would be hidden behind the nav bar. This is a very common beginner mistake.

### Fixed Bottom — A Cookie Banner / Footer Bar

```css
div.cookie-banner {
  position: fixed;
  bottom: 0;      /* Pinned to the bottom of the viewport */
  left: 0;
  width: 100%;
  background-color: #333;
  color: white;
  padding: 14px 24px;
  text-align: center;
}
```

**Expected output:** A dark bar locked to the bottom of the browser window — exactly like a cookie consent banner.

### Fixed Corner Button — "Back to Top"

```css
a.back-to-top {
  position: fixed;
  bottom: 30px;     /* 30px from the bottom of the viewport */
  right: 30px;      /* 30px from the right edge of the viewport */
  background-color: #e94560;
  color: white;
  padding: 12px 16px;
  border-radius: 50%;
  text-decoration: none;
  font-size: 18px;
}
```

**Expected output:** A circular button pinned to the bottom-right corner of the screen — a pattern seen on nearly every long-scrolling website.

---

## Part 4 — `position: absolute`

### What is `position: absolute`?

`position: absolute` is where CSS positioning becomes truly powerful — and truly confusing if you do not understand the key rule.

`position: absolute` takes the element **completely out of normal flow** (like `fixed`) and positions it relative to its **nearest positioned ancestor**.

**What is a "positioned ancestor"?** An ancestor element (any parent, grandparent, or great-grandparent in the HTML tree) that has a `position` value other than `static`. This means `relative`, `absolute`, `fixed`, or `sticky`.

**If no positioned ancestor exists**, the element is positioned relative to the **initial containing block** — which is effectively the `<html>` element (the entire page).

> **The golden rule of `position: absolute`:**  
> "Absolute elements look UP the HTML tree to find their nearest non-static positioned ancestor. That ancestor becomes their reference box."

> **Analogy:** Imagine you are inside a framed picture on a wall. You can move anywhere inside the frame. But if there is no frame, you can move anywhere on the entire wall. The frame is the "positioned ancestor." `position: relative` on a parent creates that frame.

### Simple Example — No Positioned Ancestor

When no parent has `position: relative` (or any non-static position), the `absolute` element positions itself relative to the whole page:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div.absolute-box {
      position: absolute;
      top: 80px;
      right: 20px;
      background-color: #ffcdd2;
      padding: 16px;
      width: 180px;
    }
  </style>
</head>
<body>
  <p>This paragraph is in normal flow.</p>
  <div class="absolute-box">I am absolutely positioned from the page edge</div>
  <p>This paragraph also ignores the absolute box — they do not interact.</p>
</body>
</html>
```

**Expected output:** The red box appears 80px from the top and 20px from the right edge of the **entire page**. The paragraphs flow normally beneath it, completely unaware the box exists in flow (because it has been removed from it).

---

### The Most Important Pattern — `relative` Parent + `absolute` Child

This is the most commonly used positioning pattern in all of web development. You set `position: relative` on a parent container (often with no offsets — just the keyword), and then place `position: absolute` children inside it, using offsets that are measured from the parent's edges.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div.card {
      position: relative;    /* Creates the positioning context */
      width: 300px;
      height: 200px;
      background-color: #e3f2fd;
      border: 1px solid #90caf9;
      border-radius: 8px;
    }

    div.badge {
      position: absolute;    /* Positions relative to .card */
      top: 10px;             /* 10px from the TOP of .card */
      right: 10px;           /* 10px from the RIGHT of .card */
      background-color: #e53935;
      color: white;
      padding: 4px 10px;
      border-radius: 20px;
      font-size: 12px;
      font-weight: bold;
      font-family: Arial, sans-serif;
    }
  </style>
</head>
<body>

  <div class="card">
    <div class="badge">NEW</div>
    <p style="padding: 16px;">A product card with a badge pinned to the top-right corner.</p>
  </div>

</body>
</html>
```

**Expected output:** A blue card with a small red "NEW" badge locked to the top-right corner inside the card — no matter how wide or narrow the viewport is, the badge stays pinned to the card's corner.

> **Why `relative` on `.card` with no offsets?** Writing `position: relative` without `top`/`left`/`right`/`bottom` does not move the element at all. It only establishes a positioning context for absolute children. This is intentional and very common.

### More Absolute Use Cases

#### Centred Overlay Text on an Image

```html
<div class="image-container">
  <img src="photo.jpg" alt="City" width="400" height="250">
  <div class="overlay-text">Paris, France</div>
</div>
```

```css
div.image-container {
  position: relative;   /* context for overlay */
  display: inline-block;
  width: 400px;
}

div.image-container img {
  display: block;
  width: 100%;
}

div.overlay-text {
  position: absolute;
  bottom: 16px;          /* 16px from the bottom of the container */
  left: 0;
  right: 0;
  text-align: center;
  background-color: rgba(0, 0, 0, 0.55);
  color: white;
  padding: 10px;
  font-size: 18px;
  font-family: Arial, sans-serif;
}
```

**Expected output:** A photo with a semi-transparent dark caption bar pinned to the bottom. This pattern is used on every photo gallery, travel website, and news card on the internet.

#### Tooltip Positioned Above a Button

```html
<div class="tooltip-wrapper">
  <button>Hover me</button>
  <div class="tooltip">This is a tooltip!</div>
</div>
```

```css
div.tooltip-wrapper {
  position: relative;
  display: inline-block;
}

div.tooltip {
  position: absolute;
  bottom: 110%;        /* Positions above the button */
  left: 50%;
  transform: translateX(-50%);   /* Centres the tooltip horizontally */
  background-color: #333;
  color: white;
  padding: 6px 12px;
  border-radius: 4px;
  font-size: 13px;
  white-space: nowrap;
  pointer-events: none;
}
```

**`bottom: 110%` explained:** This sets the bottom edge of the tooltip to 110% of the parent's height above the parent's bottom edge. In practice: it floats the tooltip just above the button with a small gap.

**`left: 50%` + `transform: translateX(-50%)` explained:** `left: 50%` moves the tooltip's left edge to the midpoint of the parent. `translateX(-50%)` then shifts it back half of its own width — perfectly centring it over the parent. This is a classic CSS centring technique.

---

### `absolute` vs `fixed` — Key Difference

| Feature | `position: absolute` | `position: fixed` |
|---|---|---|
| Reference point | Nearest positioned ancestor | Browser viewport |
| Scrolls with page? | Yes, it moves with the page | No, it stays in view |
| Taken out of flow? | Yes | Yes |
| Common use | Badges, tooltips, overlays | Navbars, floating buttons, banners |

---

## Part 5 — `position: sticky`

### What is `position: sticky`?

`position: sticky` is a hybrid between `relative` and `fixed`. An element with `position: sticky` behaves like a **relatively positioned element** while it is within the visible scroll area, and then **becomes fixed** when it reaches a defined scroll threshold.

> **Analogy:** Imagine a sticky note inside a long document. As you scroll down, it scrolls with you normally. But when it reaches the top of the visible window, it sticks there — refusing to scroll further until you reach the end of its parent container.

### The Critical Rule for `sticky`

**You must specify at least one offset property** (`top`, `bottom`, `left`, or `right`) for `sticky` to work. The most common is `top: 0` — which means "stick when you reach the top of the viewport."

```css
div.sticky-header {
  position: sticky;
  top: 0;   /* Stick when the element reaches 0px from the top of the viewport */
  background-color: #fffde7;
  padding: 10px 20px;
  border-bottom: 2px solid #f9a825;
}
```

### Full Sticky Demonstration

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
    }

    /* The sticky element */
    div.section-header {
      position: sticky;
      top: 0;
      background-color: #1565c0;
      color: white;
      padding: 12px 20px;
      font-size: 18px;
      font-weight: bold;
      z-index: 10;
    }

    div.section-content {
      padding: 20px;
      background-color: #e3f2fd;
      height: 300px;   /* Tall enough to force scrolling */
    }
  </style>
</head>
<body>

  <!-- Section 1 -->
  <div class="section-header">Section 1: Introduction</div>
  <div class="section-content">
    <p>Lots of content in Section 1. Scroll down...</p>
  </div>

  <!-- Section 2 -->
  <div class="section-header">Section 2: Methods</div>
  <div class="section-content">
    <p>Lots of content in Section 2. Keep scrolling...</p>
  </div>

  <!-- Section 3 -->
  <div class="section-header">Section 3: Results</div>
  <div class="section-content">
    <p>Lots of content in Section 3.</p>
  </div>

</body>
</html>
```

**Expected output:** As you scroll down, each section header sticks to the top of the viewport while you scroll through that section's content. When the next section header arrives, it pushes the previous one off the top and takes its place. This is used on: alphabet index bars in contact lists, table headers in long data tables, progress indicators, and chapter navigation on long articles.

> **Thinking prompt:** What happens if you change `top: 0` to `top: 60px`? The element will only stick when it is 60px from the top — leaving 60px of space between the sticky element and the top of the viewport (useful if you have a fixed navbar that is 60px tall).

### Sticky vs Fixed — Key Difference

| Feature | `position: sticky` | `position: fixed` |
|---|---|---|
| Taken out of flow? | **No** — still occupies original space | **Yes** — removed from flow |
| Scrolls with page? | Yes, until threshold | No, always fixed |
| Reference for offsets | Scroll container | Browser viewport |
| Content pushes down? | Yes — other content flows around it | No — must add margin manually |

### Common `sticky` Gotcha — The Parent Must Be Tall Enough

A sticky element will only stick as long as it is within the bounds of its **parent container**. The moment the parent's bottom edge scrolls past the viewport, the sticky element unsticks and disappears with the parent.

```html
<!-- BAD: parent is too short — sticky never works -->
<div style="height: 60px;">
  <div style="position: sticky; top: 0;">Header</div>
  <p>Short content</p>
</div>

<!-- GOOD: parent is tall enough for sticky to matter -->
<div style="height: 800px;">
  <div style="position: sticky; top: 0;">Header</div>
  <p>Lots of content here...</p>
</div>
```

---

## Part 6 — Offset Properties Deep Dive

### How `top`, `bottom`, `left`, `right` Work Together

You can use any combination of offset properties. Here is how each one behaves:

| Property | Direction | Example |
|---|---|---|
| `top: 20px` | Pushes element 20px DOWN from its reference top edge | Down |
| `top: -20px` | Pulls element 20px UPWARD | Up |
| `bottom: 20px` | Positions element so its bottom is 20px from the reference bottom | Up |
| `left: 30px` | Pushes element 30px to the RIGHT | Right |
| `left: -30px` | Pulls element 30px to the LEFT | Left |
| `right: 30px` | Positions element so its right is 30px from the reference right | Left |

### Centring with `absolute` — Classic Technique

To centre an absolute element both horizontally and vertically inside its positioned parent:

```css
div.parent {
  position: relative;
  width: 400px;
  height: 300px;
  background-color: #e8f5e9;
}

div.centred-child {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #43a047;
  color: white;
  padding: 16px 24px;
  border-radius: 6px;
}
```

**How it works:**
- `top: 50%; left: 50%;` — moves the element's **top-left corner** to the exact centre of the parent
- `transform: translate(-50%, -50%)` — shifts the element back by half its own width and height, perfectly centring it

**Expected output:** The green box appears exactly centred within the parent container regardless of how big either element is.

---

## Part 7 — The `z-index` Connection

When positioned elements overlap each other, CSS needs to decide which one appears on top. This is controlled by `z-index`. The element with the higher `z-index` appears in front.

```css
div.layer-1 {
  position: absolute;
  top: 20px;
  left: 20px;
  z-index: 1;           /* Lower — appears behind */
  background-color: lightblue;
}

div.layer-2 {
  position: absolute;
  top: 40px;
  left: 40px;
  z-index: 2;           /* Higher — appears in front */
  background-color: lightyellow;
}
```

> **Key rule:** `z-index` only works on **positioned elements** (anything except `position: static`). It has no effect on static elements.

---

## Part 8 — Code Challenge Walkthroughs

The W3Schools CSS position code challenges test your understanding of all five position values and their offset properties. Here are the core types:

### Challenge Type 1: Set an Element to Relative and Offset It

**Task:** Move the element 15px down and 10px right from its normal position.

```css
/* Solution */
div {
  position: relative;
  top: 15px;
  left: 10px;
}
```

---

### Challenge Type 2: Create a Fixed Header

**Task:** Fix a header element to the top of the viewport, full width.

```css
/* Solution */
header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
}
```

---

### Challenge Type 3: Absolute Inside Relative Container

**Task:** Place a `.label` element at the bottom-right corner of its `.container` parent.

```css
/* Solution */
.container {
  position: relative;
}

.label {
  position: absolute;
  bottom: 0;
  right: 0;
}
```

---

### Challenge Type 4: Sticky Section Header

**Task:** Make a header stick to the top of the viewport when scrolled.

```css
/* Solution */
h2 {
  position: sticky;
  top: 0;
}
```

---

### Challenge Type 5: Centre an Absolute Element

**Task:** Centre a `.popup` box inside a `.wrapper` both horizontally and vertically.

```css
/* Solution */
.wrapper {
  position: relative;
}

.popup {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

---

## Guided Practice Exercises

### Exercise 1 — Profile Card with Absolute Badge

**Objective:** Build a profile card where a "VERIFIED" badge is pinned to the top-right corner using `position: absolute` on a `position: relative` container.

**Scenario:** You are building a user profile card for a social platform. Users who have verified their email get a badge pinned to the card corner.

**Starter HTML:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Write your CSS here */
  </style>
</head>
<body>

  <div class="profile-card">
    <div class="badge">✓ VERIFIED</div>
    <div class="avatar">👤</div>
    <h3>Alex Johnson</h3>
    <p>Frontend Developer</p>
  </div>

</body>
</html>
```

**Target styling:**
- `.profile-card`: `position: relative`, white background, `width: 240px`, `padding: 30px 20px`, `border-radius: 12px`, box shadow, `text-align: center`
- `.badge`: `position: absolute`, `top: 12px`, `right: 12px`, green background (`#2e7d32`), white text, small font, rounded pill shape

**Solution:**

```css
* { box-sizing: border-box; margin: 0; padding: 0; }
body { background-color: #f0f2f5; display: flex; justify-content: center; padding: 60px 20px; font-family: Arial, sans-serif; }

.profile-card {
  position: relative;       /* Establishes context for .badge */
  background-color: white;
  width: 240px;
  padding: 30px 20px;
  border-radius: 12px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.1);
  text-align: center;
}

.badge {
  position: absolute;       /* Positioned relative to .profile-card */
  top: 12px;
  right: 12px;
  background-color: #2e7d32;
  color: white;
  font-size: 11px;
  font-weight: bold;
  padding: 4px 10px;
  border-radius: 20px;
}

.avatar {
  font-size: 52px;
  margin-bottom: 12px;
}

h3 { font-size: 18px; color: #222; margin-bottom: 4px; }
p  { font-size: 14px; color: #777; }
```

**Expected output:** A white profile card centred on a grey background, with a small green "✓ VERIFIED" pill badge locked to the top-right corner.

**Self-check questions:**
- Does the badge stay in the corner even if you change the card's width?
- What happens if you remove `position: relative` from `.profile-card`? (The badge jumps to the corner of the whole page.)

---

### Exercise 2 — Fixed Navigation + Sticky Section Headers

**Objective:** Build a page with a fixed top navigation bar and sticky section headers that lock at the viewport top as you scroll.

**Scenario:** You are building a long documentation page with a fixed navbar and sticky chapter headers.

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body { font-family: Arial, sans-serif; }

    /* Fixed navbar — always at top of viewport */
    nav.topbar {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      background-color: #0d47a1;
      color: white;
      padding: 16px 24px;
      font-size: 18px;
      font-weight: bold;
      z-index: 1000;
    }

    /* Push content below the fixed navbar */
    main {
      margin-top: 54px;
    }

    /* Sticky chapter header */
    h2.chapter {
      position: sticky;
      top: 54px;    /* sticks just below the fixed navbar (54px = navbar height) */
      background-color: #e8eaf6;
      color: #283593;
      padding: 10px 24px;
      font-size: 17px;
      border-left: 4px solid #3949ab;
      z-index: 100;
    }

    div.chapter-content {
      padding: 30px 24px;
      background-color: white;
      min-height: 320px;
      border-bottom: 1px solid #e0e0e0;
    }

    p { margin-bottom: 14px; color: #444; line-height: 1.7; }
  </style>
</head>
<body>

  <nav class="topbar">📘 CSS Documentation</nav>

  <main>

    <h2 class="chapter">Chapter 1: Introduction to CSS</h2>
    <div class="chapter-content">
      <p>CSS stands for Cascading Style Sheets. It describes how HTML elements are displayed on screen. Scroll down to continue reading about CSS fundamentals.</p>
      <p>With CSS, you control the layout, colour, spacing, fonts, and visual effects of every element on your web page.</p>
      <p>CSS can be added inline, internally, or via an external stylesheet.</p>
    </div>

    <h2 class="chapter">Chapter 2: Selectors</h2>
    <div class="chapter-content">
      <p>Selectors are patterns used to target HTML elements you want to style.</p>
      <p>Types include element selectors, class selectors, ID selectors, attribute selectors, and pseudo-class selectors.</p>
      <p>Understanding selector specificity is crucial for writing predictable, maintainable CSS.</p>
    </div>

    <h2 class="chapter">Chapter 3: The Box Model</h2>
    <div class="chapter-content">
      <p>Every HTML element is a rectangular box with content, padding, border, and margin.</p>
      <p>The box model determines how space is calculated and distributed around elements.</p>
      <p>Use `box-sizing: border-box` to include padding and border in the element's total width.</p>
    </div>

    <h2 class="chapter">Chapter 4: Positioning</h2>
    <div class="chapter-content">
      <p>CSS positioning includes static, relative, fixed, absolute, and sticky.</p>
      <p>Understanding positioning is one of the most powerful skills in CSS layout design.</p>
      <p>The `position: relative` + `position: absolute` pattern is used on almost every production website.</p>
    </div>

  </main>

</body>
</html>
```

**Expected output:**
- A fixed dark blue navbar always visible at the top
- Each chapter header sticks just below the navbar as you scroll through that chapter's content
- As the next chapter arrives, its header pushes the previous one up and takes its sticky position

---

### Exercise 3 — Image Card with Overlay Text

**Objective:** Build an image card where text overlays the bottom of the image using `position: absolute` on a `position: relative` wrapper.

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body { font-family: Arial, sans-serif; background: #f5f5f5; padding: 40px; }

    .photo-card {
      position: relative;
      width: 340px;
      border-radius: 10px;
      overflow: hidden;       /* clips the overlay to the card's rounded corners */
      box-shadow: 0 6px 20px rgba(0,0,0,0.15);
    }

    .photo-card img {
      display: block;
      width: 100%;
      height: 220px;
      object-fit: cover;      /* fills the space without distortion */
      background-color: #90caf9;  /* placeholder if no actual image */
    }

    /* Simulated image using a div (for demo without real image file) */
    .fake-image {
      display: block;
      width: 100%;
      height: 220px;
      background: linear-gradient(135deg, #1565c0, #42a5f5);
    }

    .caption {
      position: absolute;
      bottom: 0;              /* Pinned to the bottom of .photo-card */
      left: 0;
      right: 0;
      background: linear-gradient(transparent, rgba(0,0,0,0.75));
      color: white;
      padding: 24px 16px 16px;
    }

    .caption h3 { font-size: 17px; margin-bottom: 4px; }
    .caption p  { font-size: 13px; opacity: 0.85; }
  </style>
</head>
<body>

  <div class="photo-card">
    <div class="fake-image"></div>
    <div class="caption">
      <h3>Mountain Sunrise</h3>
      <p>Swiss Alps · Photography by Sarah K.</p>
    </div>
  </div>

</body>
</html>
```

**Expected output:** A rounded photo card with a gradient-fading dark overlay at the bottom containing a title and description. The gradient fades from transparent at the top to semi-black at the bottom — a technique used on every photo card on Instagram, Unsplash, and news sites.

---

## Mini Project — Personal Portfolio Hero Section

### Project Overview

You will build a complete **hero section** for a personal portfolio website. It includes: a fixed navigation bar at the top, a hero background with absolutely positioned text and a call-to-action button, and a sticky section label that locks when you scroll into the about section.

This project uses `fixed`, `absolute`, `relative`, and `sticky` all in one cohesive page.

---

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Alex Chen — Portfolio</title>
  <style>
    /* CSS added stage by stage below */
  </style>
</head>
<body>

  <!-- Fixed navigation -->
  <nav class="main-nav">
    <span class="logo">Alex Chen</span>
    <div class="nav-links">
      <a href="#hero">Home</a>
      <a href="#about">About</a>
      <a href="#work">Work</a>
      <a href="#contact">Contact</a>
    </div>
  </nav>

  <!-- Hero section with absolute overlay text -->
  <section id="hero" class="hero-section">
    <div class="hero-content">
      <span class="tag">Full-Stack Developer</span>
      <h1>Building the Web,<br>One Line at a Time.</h1>
      <p>I create clean, fast, and accessible web experiences.</p>
      <a href="#work" class="cta-btn">View My Work →</a>
    </div>

    <!-- Absolutely positioned decorative badge -->
    <div class="scroll-hint">↓ Scroll</div>
  </section>

  <!-- About section with sticky header -->
  <section id="about" class="about-section">
    <h2 class="sticky-label">About Me</h2>
    <div class="about-content">
      <p>I am a passionate developer with 5 years of experience building modern web applications using HTML, CSS, JavaScript, and React.</p>
      <p>I care deeply about performance, accessibility, and writing code that other developers enjoy reading.</p>
      <p>When I am not coding, I am hiking, reading, or experimenting with new technologies.</p>
      <p>I believe great software starts with clear thinking and a genuine understanding of user needs.</p>
    </div>
  </section>

  <!-- Work section placeholder -->
  <section id="work" class="work-section">
    <h2 class="sticky-label">My Work</h2>
    <div class="about-content">
      <p>Project cards will go here in a future lesson on CSS Grid and Flexbox.</p>
      <p>For now, imagine three beautiful project cards displayed side by side.</p>
      <p>Each one showcases a different type of project — web app, mobile UI, and data dashboard.</p>
      <p>Every card uses the `position: relative` + `position: absolute` badge pattern you learned today.</p>
    </div>
  </section>

</body>
</html>
```

**Milestone output:** Plain, unstyled HTML with navigation, hero, and content sections.

---

### Stage 2 — Global Styles and Fixed Navigation

```css
/* Global Reset */
*, *::before, *::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Arial', sans-serif;
  color: #222;
  background-color: #ffffff;
}

/* ===== FIXED NAVIGATION ===== */
nav.main-nav {
  position: fixed;         /* Locked to viewport — stays on scroll */
  top: 0;
  left: 0;
  width: 100%;
  background-color: rgba(10, 10, 20, 0.92);
  backdrop-filter: blur(8px);     /* Frosted glass effect */
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 40px;
  height: 60px;
  z-index: 9999;
}

.logo {
  color: white;
  font-size: 20px;
  font-weight: bold;
  letter-spacing: 1px;
}

.nav-links a {
  color: #cccccc;
  text-decoration: none;
  margin-left: 28px;
  font-size: 14px;
  transition: color 0.2s ease;
}

.nav-links a:hover {
  color: #64b5f6;
}
```

**Milestone output:** A dark semi-transparent navigation bar with a frosted blur effect, fixed to the top of the viewport. Navigation links turn blue on hover.

---

### Stage 3 — Hero Section with Absolute Positioning

```css
/* ===== HERO SECTION ===== */
section.hero-section {
  position: relative;          /* Context for .hero-content and .scroll-hint */
  height: 100vh;               /* Full viewport height */
  background: linear-gradient(135deg, #0d1b2a 0%, #1b3a5e 50%, #0d47a1 100%);
  display: flex;
  align-items: center;
  padding: 0 60px;
  margin-top: 60px;            /* Offset for fixed nav height */
  overflow: hidden;
}

/* Hero text block — absolutely centred-left in the hero */
div.hero-content {
  position: relative;          /* Stays in flex flow but can contain absolutes */
  max-width: 620px;
}

span.tag {
  display: inline-block;
  background-color: rgba(100, 181, 246, 0.15);
  color: #64b5f6;
  border: 1px solid #64b5f6;
  padding: 5px 14px;
  border-radius: 20px;
  font-size: 13px;
  margin-bottom: 20px;
  letter-spacing: 0.5px;
}

.hero-content h1 {
  font-size: 52px;
  color: white;
  line-height: 1.2;
  margin-bottom: 18px;
  font-weight: 800;
}

.hero-content p {
  font-size: 18px;
  color: #90caf9;
  margin-bottom: 32px;
  line-height: 1.6;
}

a.cta-btn {
  display: inline-block;
  background-color: #1565c0;
  color: white;
  padding: 14px 32px;
  border-radius: 6px;
  text-decoration: none;
  font-size: 16px;
  font-weight: bold;
  transition: background-color 0.25s ease, transform 0.2s ease;
}

a.cta-btn:hover {
  background-color: #0d47a1;
  transform: translateY(-2px);     /* Subtle lift on hover */
}

/* Absolutely positioned scroll hint at bottom-centre of hero */
div.scroll-hint {
  position: absolute;       /* Positioned within .hero-section */
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);    /* Centre it horizontally */
  color: rgba(255, 255, 255, 0.5);
  font-size: 14px;
  letter-spacing: 2px;
  animation: bounce 1.6s infinite;
}

@keyframes bounce {
  0%, 100% { transform: translateX(-50%) translateY(0); }
  50%       { transform: translateX(-50%) translateY(8px); }
}
```

**Milestone output:** A full-screen dark blue gradient hero with a white heading, blue tag badge, subtitle, CTA button, and a gently bouncing "↓ Scroll" hint pinned to the bottom centre.

---

### Stage 4 — About Section with Sticky Headers

```css
/* ===== ABOUT + WORK SECTIONS ===== */
section.about-section,
section.work-section {
  background-color: white;
  min-height: 80vh;
}

/* Sticky section label — sticks below the fixed navbar */
h2.sticky-label {
  position: sticky;
  top: 60px;               /* Sticks 60px from top — right below the fixed nav */
  background-color: #f8f9ff;
  color: #1a237e;
  padding: 14px 40px;
  font-size: 22px;
  border-bottom: 2px solid #e8eaf6;
  border-left: 5px solid #3949ab;
  z-index: 100;
}

div.about-content {
  padding: 40px 60px;
  max-width: 720px;
}

div.about-content p {
  font-size: 16px;
  line-height: 1.85;
  color: #444;
  margin-bottom: 20px;
}
```

**Milestone output:** Each section has a sticky heading that locks just below the fixed navigation bar while you scroll through the section's content.

---

### Stage 5 — Completed Full Project

Combine all stages. The final working page demonstrates every position value working harmoniously:
- `fixed` — navigation bar permanently locked to the top
- `absolute` — scroll hint pinned to the bottom-centre of the hero section
- `relative` — hero section acts as the positioning container
- `sticky` — section headers lock below the nav as you scroll

**Reflection Questions:**
1. Why does `margin-top: 60px` appear on the hero section? What would happen without it?
2. Why is `top: 60px` used on the sticky headers instead of `top: 0`?
3. The `.scroll-hint` uses `left: 50%` + `transform: translateX(-50%)`. Explain in your own words why both are needed.
4. What is `z-index: 9999` on the navbar preventing?

**Optional Extensions:**
- Add a "Back to Top" button using `position: fixed; bottom: 30px; right: 30px`
- Add a notification dot to the navbar logo using `position: absolute` within a `position: relative` wrapper
- Try changing the `sticky` label's `top` value to `0` — what visual problem does this cause?

---

## Common Beginner Mistakes

### Mistake 1: Using Offsets on a Static Element

**Wrong:**
```css
div {
  top: 50px;    /* Does nothing! */
  left: 30px;   /* Does nothing! */
}
```

**Problem:** No `position` property was set. Default is `static`. Offset properties are completely ignored on static elements.

**Correct:**
```css
div {
  position: relative;  /* or absolute, fixed, sticky */
  top: 50px;
  left: 30px;
}
```

---

### Mistake 2: Forgetting to Compensate for Fixed Elements

**Wrong:**
```css
nav { position: fixed; top: 0; height: 60px; }
/* No margin-top on body or main content */
```

**Problem:** Fixed elements are removed from document flow. The content behind them starts at the very top — hidden beneath the fixed nav.

**Correct:**
```css
nav { position: fixed; top: 0; height: 60px; }
main { margin-top: 60px; }   /* Push content below the fixed nav */
```

---

### Mistake 3: Expecting `absolute` to Position Inside the Wrong Parent

**Wrong:**
```html
<div class="wrapper">         <!-- no position set -->
  <div class="parent">        <!-- no position set -->
    <div class="child" style="position: absolute; top: 0; right: 0;">Badge</div>
  </div>
</div>
```

**Problem:** The badge positions relative to the nearest positioned ancestor — but neither `.parent` nor `.wrapper` has a non-static position. The badge jumps to the corner of the entire page.

**Correct:**
```css
.parent {
  position: relative;   /* Now .child positions inside .parent */
}
```

---

### Mistake 4: `sticky` Not Working — Forgetting the Offset

**Wrong:**
```css
div.header {
  position: sticky;    /* sticky without an offset does nothing */
}
```

**Problem:** Without specifying `top`, `bottom`, `left`, or `right`, the browser does not know at what scroll point to make it stick.

**Correct:**
```css
div.header {
  position: sticky;
  top: 0;   /* Stick when element reaches 0px from top of viewport */
}
```

---

### Mistake 5: `sticky` Not Working — Parent Is Too Short or Has `overflow: hidden`

**Wrong setup:**
```css
.section {
  overflow: hidden;   /* This BREAKS sticky positioning */
}
.section h2 {
  position: sticky;
  top: 0;
}
```

**Problem 1:** If the parent container has `overflow: hidden` or `overflow: auto`, `sticky` cannot work — it needs a scroll container, and setting overflow on the parent prevents the sticky behaviour.

**Problem 2:** If the parent is too short (the sticky element fills most of its height), there is nothing to scroll through, so sticky never activates.

**Correct:** Ensure the sticky element's parent does not have `overflow: hidden/auto` and is taller than the sticky element.

---

### Mistake 6: `z-index` Not Working on Static Elements

**Wrong:**
```css
div.overlay {
  z-index: 999;   /* Does nothing — div is position: static */
}
```

**Problem:** `z-index` only works on positioned elements (non-static). On a static element, it is completely ignored.

**Correct:**
```css
div.overlay {
  position: relative;   /* or absolute, fixed, sticky */
  z-index: 999;         /* Now works */
}
```

---

## Reflection Questions

1. What is "normal document flow"? Which `position` values keep an element in normal flow, and which ones remove it?

2. `position: relative` with no offset properties does not visually move an element at all. So why would a developer ever write it?

3. What is the difference between `position: fixed` and `position: sticky` when the user scrolls the page?

4. An element with `position: absolute` can have two different reference points depending on the HTML. What are these two cases, and what determines which one applies?

5. If you have a fixed navbar that is 70px tall, what value should you use for `top` on a sticky element that should stick just below the navbar?

6. You want a "SALE" badge to always appear in the top-right corner of a product image card. What `position` value do you give the card container? What `position` value do you give the badge?

7. Explain in plain words what `left: 50%; transform: translateX(-50%)` does and why both are needed to horizontally centre an absolute element.

8. A colleague says their `position: sticky` element is not working. What are the three most common reasons this happens, and how would you diagnose each one?

---

## Completion Checklist

Before moving to the next lesson, confirm you can do all of the following:

- [ ] I can explain what "normal document flow" is and how `position` interacts with it
- [ ] I understand that `position: static` is the default and that offsets do nothing on static elements
- [ ] I can use `position: relative` to nudge an element from its normal position using `top`, `left`, `right`, `bottom`
- [ ] I understand that `position: relative` reserves the original space even when the element is visually moved
- [ ] I can use `position: fixed` to lock an element to the viewport during scrolling
- [ ] I know to add a `margin-top` to body content to compensate for fixed headers
- [ ] I understand the "nearest positioned ancestor" rule for `position: absolute`
- [ ] I can create the `relative` parent + `absolute` child pattern to pin badges, labels, and overlays inside containers
- [ ] I can use `position: sticky` with `top` offset to create scroll-locking elements
- [ ] I know the common reasons `sticky` fails (missing offset, `overflow: hidden` on parent, parent too short)
- [ ] I can use `left: 50%; transform: translateX(-50%)` to horizontally centre an absolute element
- [ ] I understand that `z-index` only works on positioned (non-static) elements
- [ ] I can identify the right position value for: fixed navbars, sticky headers, corner badges, overlay captions, and back-to-top buttons
- [ ] I have completed the mini-project using all four non-static position values together

---

## Lesson Summary

In this lesson, you mastered one of the most transformative properties in all of CSS — `position`.

You learned that every element starts as `position: static`, following normal document flow. `position: relative` lets you nudge an element from its natural spot while keeping its original space reserved — and more importantly, it creates a positioning context that `absolute` children rely on. `position: fixed` tears an element out of flow entirely and anchors it to the browser viewport, making it immune to scrolling. `position: absolute` also leaves flow but positions relative to the nearest non-static ancestor, enabling the powerful and ubiquitous "relative container + absolute child" pattern used for badges, overlays, tooltips, and captions on virtually every professional website. Finally, `position: sticky` gives you the best of both worlds — scrolling with content until a threshold, then locking — perfect for navigation labels, table headers, and section anchors.

The offset properties (`top`, `right`, `bottom`, `left`) are the coordinates you use with all non-static positions, and you saw how combining them with `transform: translate(-50%, -50%)` achieves perfect centring. You also learned that `z-index` — the stacking controller — only works on positioned elements.

In the next lesson, you will explore **CSS Position Offsets** in more detail, then move on to `z-index` and how layering contexts are created and managed.

---

*Sources: W3Schools CSS Position Tutorial (https://www.w3schools.com/css/css_position.asp), CSS Fixed/Absolute Positioning (https://www.w3schools.com/css/css_positioning_fixed_absolute.asp), CSS Sticky Positioning (https://www.w3schools.com/css/css_positioning_sticky.asp), CSS Position Code Challenges (https://www.w3schools.com/css/css_challenges_position.asp)*
