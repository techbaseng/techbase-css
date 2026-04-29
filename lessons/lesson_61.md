---
render_with_liquid: false
title: "CSS Buttons — Styling, Hover Effects & Button Groups"
nav_order: 61
---

# Lesson 61: CSS Buttons — Styling, Hover Effects & Button Groups

---

## Lesson Introduction

Buttons are one of the most important interactive elements on any webpage. Every time a user submits a form, downloads a file, adds an item to a cart, or navigates a site, they almost always press a **button**. The problem? The browser's default button style looks plain and very "unfinished".

In this lesson, you will learn how to take that plain, grey, default browser button and transform it into something polished, professional, and interactive — using nothing but CSS.

By the end of this lesson, you will be able to:
- Style buttons with colours, sizes, fonts, borders, and rounded corners
- Build animated hover effects — colour shifts, lift shadows, ripple effects, border sweeps, and more
- Create button groups and navigation bars from sets of buttons
- Understand the difference between full-width buttons, outline buttons, disabled buttons, and icon buttons
- Build a real-world mini-project: a complete action panel with multiple button styles

> **Who is this for?**
> Anyone who knows basic CSS (properties, selectors, colours, and `hover`). No JavaScript knowledge is needed for most of this lesson — the hover effects and transitions are all pure CSS.

---

## Prerequisite Concepts

### What is a `<button>` element?

In HTML, the `<button>` tag creates a clickable button:

```html
<button>Click Me</button>
```

**Expected result:** A plain grey box with the text "Click Me" — functional but visually unappealing.

### What is an `<a>` tag styled as a button?

Links (`<a>` tags) can also be styled to look and behave like buttons. This is common for navigation:

```html
<a href="#" class="btn">Go Home</a>
```

With CSS, you can make this look identical to a `<button>`.

### The `:hover` pseudo-class

`:hover` lets you apply styles that only activate when the user's mouse is over an element:

```css
button:hover {
  background-color: darkblue;
}
```

### The `transition` property

`transition` makes changes happen smoothly over time, instead of snapping instantly:

```css
button {
  transition: background-color 0.3s ease;
}
```

This means "change the background colour smoothly over 0.3 seconds."

---

## Part 1 — Basic Button Styling

### 1.1 The Default Button Problem

Open any browser and drop in a plain `<button>`. You get this:

```html
<button>Click Me</button>
```

**What the browser gives you by default:**
- An ugly grey background
- A square, boxy border from the OS
- A very small font that varies per browser
- No padding — the text is cramped
- No personality whatsoever

CSS lets you override all of this completely.

---

### 1.2 The Essential Button Reset

The first step is to strip away the browser's default styling and take full control:

```css
button {
  background-color: #4CAF50;   /* Green background */
  color: white;                 /* White text */
  padding: 15px 32px;           /* Space inside the button */
  text-align: center;           /* Centre the text */
  font-size: 16px;              /* Readable text size */
  border: none;                 /* Remove default border */
  cursor: pointer;              /* Hand cursor on hover */
  border-radius: 4px;           /* Slightly rounded corners */
  display: inline-block;        /* Sit next to other elements */
}
```

**Line-by-line explanation:**

| Property | Value | What it does |
|----------|-------|--------------|
| `background-color` | `#4CAF50` | Sets a pleasant green background |
| `color` | `white` | Makes the text white so it is readable on green |
| `padding` | `15px 32px` | 15px top/bottom, 32px left/right — creates breathing room |
| `text-align` | `center` | Centres the text inside the button |
| `font-size` | `16px` | Large enough to read comfortably |
| `border` | `none` | Removes the browser's default border box |
| `cursor` | `pointer` | Shows the hand icon — signals "this is clickable" |
| `border-radius` | `4px` | Slightly rounds the corners |
| `display` | `inline-block` | Allows padding and sizing while flowing inline |

**Expected result:** A clean, green button with white text and comfortable padding.

> **Why `cursor: pointer`?** Buttons automatically get the pointer cursor. But `<a>` tags styled as buttons, or `<div>` tags used as buttons, do *not* get it automatically. Always add this so users know the element is clickable.

---

### 1.3 Button Colour Variations

Colour is the fastest way to communicate a button's purpose. Conventions have developed around certain colours:

```css
/* Primary action — Blue */
.btn-primary {
  background-color: #008CBA;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
}

/* Danger / Delete — Red */
.btn-danger {
  background-color: #f44336;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
}

/* Warning — Orange/Yellow */
.btn-warning {
  background-color: #ff9800;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
}

/* Success / Confirm — Green */
.btn-success {
  background-color: #4CAF50;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
}

/* Neutral / Secondary — Grey */
.btn-secondary {
  background-color: #9e9e9e;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
}

/* Dark */
.btn-dark {
  background-color: #555555;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
}
```

```html
<button class="btn-primary">Primary</button>
<button class="btn-danger">Danger</button>
<button class="btn-warning">Warning</button>
<button class="btn-success">Success</button>
<button class="btn-secondary">Secondary</button>
<button class="btn-dark">Dark</button>
```

**Expected result:** A row of colourful buttons, each communicating a different type of action.

> **Real-world use:** Almost every website or app uses this colour coding. Blue = do something, Red = dangerous action, Green = confirm/go, Yellow/Orange = caution. You will see this in Bootstrap, Tailwind, Material UI, and virtually every design system.

---

### 1.4 Button Sizes

You control button size primarily through `padding` and `font-size`:

```css
/* Extra Small */
.btn-xs {
  padding: 4px 8px;
  font-size: 11px;
}

/* Small */
.btn-sm {
  padding: 8px 16px;
  font-size: 13px;
}

/* Medium (default) */
.btn-md {
  padding: 12px 24px;
  font-size: 16px;
}

/* Large */
.btn-lg {
  padding: 18px 36px;
  font-size: 20px;
}

/* Extra Large */
.btn-xl {
  padding: 24px 48px;
  font-size: 24px;
}
```

```html
<button class="btn-xs">Extra Small</button>
<button class="btn-sm">Small</button>
<button class="btn-md">Medium</button>
<button class="btn-lg">Large</button>
<button class="btn-xl">Extra Large</button>
```

**Expected result:** A series of buttons growing progressively larger from left to right.

> **Think about it:** What happens if you increase `font-size` but keep `padding` the same? The button gets taller (text pushes the height up), but the space around the text stays the same. Try it!

---

### 1.5 Full-Width Button

A full-width button stretches across its entire container. This is standard on mobile designs and for primary call-to-action sections:

```css
.btn-full {
  width: 100%;
  padding: 15px;
  font-size: 18px;
  background-color: #008CBA;
  color: white;
  border: none;
  cursor: pointer;
}
```

```html
<button class="btn-full">Subscribe Now</button>
```

**Expected result:** The button stretches to fill the full width of its parent container.

---

### 1.6 Rounded Buttons (Pill Shape)

You can make buttons fully rounded on the ends — called a "pill" button — by setting `border-radius` to a large value:

```css
.btn-pill {
  background-color: #4CAF50;
  color: white;
  padding: 14px 28px;
  border: none;
  cursor: pointer;
  font-size: 16px;
  border-radius: 50px;   /* Very large value → pill shape */
}
```

**Expected result:** A button where the left and right ends are completely semicircular — a pill shape.

> **Why does `50px` (not `50%`) work here?** Because `border-radius` applies to corners. When the radius is larger than half the element's height, the corners are as round as they can be — forming smooth semicircles. For buttons, `999px` also works as a shorthand for "as rounded as possible."

---

### 1.7 Outline / Ghost Buttons

An outline button has a transparent background with only a coloured border and matching text. This is used for secondary actions that should be visible but not as prominent as the primary button:

```css
.btn-outline-blue {
  background-color: transparent;
  color: #008CBA;
  border: 2px solid #008CBA;
  padding: 13px 30px;      /* Slightly less to account for the 2px border */
  font-size: 16px;
  cursor: pointer;
  border-radius: 4px;
}

.btn-outline-green {
  background-color: transparent;
  color: #4CAF50;
  border: 2px solid #4CAF50;
  padding: 13px 30px;
  font-size: 16px;
  cursor: pointer;
  border-radius: 4px;
}

.btn-outline-red {
  background-color: transparent;
  color: #f44336;
  border: 2px solid #f44336;
  padding: 13px 30px;
  font-size: 16px;
  cursor: pointer;
  border-radius: 4px;
}
```

```html
<button class="btn-outline-blue">Blue Outline</button>
<button class="btn-outline-green">Green Outline</button>
<button class="btn-outline-red">Red Outline</button>
```

**Expected result:** Transparent buttons with a coloured border and matching text colour.

> **Real-world use:** Landing pages often pair a solid primary button ("Buy Now") with an outline secondary button ("Learn More"). The solid one draws the eye; the outline one provides an alternative without competing.

---

### 1.8 Disabled Buttons

A disabled button should look visually inactive and should not show the pointer cursor:

```css
.btn-disabled {
  background-color: #cccccc;
  color: #666666;
  padding: 15px 32px;
  font-size: 16px;
  border: none;
  cursor: not-allowed;   /* Shows a "not allowed" cursor */
  border-radius: 4px;
  opacity: 0.65;
}
```

Or using the built-in HTML `disabled` attribute with CSS:

```css
button:disabled,
button[disabled] {
  background-color: #cccccc;
  color: #888888;
  cursor: not-allowed;
  opacity: 0.65;
}
```

```html
<button disabled>I Am Disabled</button>
```

**Expected result:** A greyed-out button with a "not allowed" cursor — visually communicating that the action is currently unavailable.

---

### 1.9 Buttons with Icons

Adding an emoji or icon character to a button makes it more communicative at a glance:

```css
.btn-icon {
  background-color: #4CAF50;
  color: white;
  padding: 12px 20px;
  font-size: 16px;
  border: none;
  cursor: pointer;
  border-radius: 4px;
  display: inline-flex;       /* Aligns icon and text side by side */
  align-items: center;        /* Vertically centres icon with text */
  gap: 8px;                   /* Space between icon and text */
}
```

```html
<button class="btn-icon">
  ✔ Confirm
</button>

<button class="btn-icon" style="background-color:#f44336;">
  ✖ Delete
</button>

<button class="btn-icon" style="background-color:#008CBA;">
  ⬇ Download
</button>
```

**Expected result:** Buttons with symbols and text side by side, nicely aligned.

---

## Part 2 — Hover Effects

### 2.1 Why Hover Effects Matter

A button without a hover effect feels flat and lifeless. When users hover over something and *nothing changes*, they start to wonder: "Is this actually a button? Will it respond if I click it?"

Hover effects:
- Confirm interactivity — "Yes, this will do something."
- Add professionalism and polish
- Delight users with small moments of feedback

The key to great hover effects is combining `:hover` with `transition` for smoothness.

---

### 2.2 Simple Background Colour Change

The most basic hover effect: the background changes colour on hover.

```css
.btn-hover-basic {
  background-color: #4CAF50;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
  border-radius: 4px;
  transition: background-color 0.3s ease;  /* Smooth colour change */
}

.btn-hover-basic:hover {
  background-color: #45a049;   /* A slightly darker green */
}
```

**Expected result:** The button goes from bright green to darker green smoothly when hovered.

> **The rule of thumb:** Make the hover state 15–25% darker (or lighter) than the normal state. This is enough to be clearly noticed without being jarring.

**Darken any colour on hover:**

```css
/* Blue button, darker on hover */
.btn-blue {
  background-color: #008CBA;
  transition: background-color 0.3s;
}
.btn-blue:hover {
  background-color: #006f94;
}

/* Red button, darker on hover */
.btn-red {
  background-color: #f44336;
  transition: background-color 0.3s;
}
.btn-red:hover {
  background-color: #d32f2f;
}
```

---

### 2.3 Shadow Lift Effect

This effect makes the button look like it lifts up off the page, growing a shadow underneath it — like physically pressing or releasing a physical button.

```css
.btn-lift {
  background-color: #4CAF50;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
  border-radius: 4px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);   /* Starting shadow */
  transition: box-shadow 0.3s ease, transform 0.3s ease;
}

.btn-lift:hover {
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);  /* Bigger shadow on hover */
  transform: translateY(-3px);                  /* Moves up 3px */
}
```

**Line-by-line explanation:**

| Property | What it does |
|----------|--------------|
| `box-shadow: 0 4px 6px ...` | Starts with a subtle shadow below the button |
| `transform: translateY(-3px)` | Moves the button 3 pixels upward (negative Y = up) |
| `box-shadow: 0 8px 16px ...` | On hover, shadow grows bigger — as if the button moved away from the surface |

**Expected result:** Hovering makes the button appear to float upward slightly, with a larger shadow beneath it. Very satisfying effect.

---

### 2.4 Press / Click Effect (Active State)

The press effect makes a button look like it physically gets pressed in when clicked. Combine it with the lift effect:

```css
.btn-pressable {
  background-color: #4CAF50;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
  border-radius: 4px;
  box-shadow: 0 6px 0 #2e7d32;  /* "Raised" shadow — like a 3D bottom edge */
  transition: all 0.1s ease;
}

.btn-pressable:hover {
  box-shadow: 0 4px 0 #2e7d32;
  transform: translateY(2px);   /* Moves slightly down on hover */
}

.btn-pressable:active {
  box-shadow: 0 0 0 #2e7d32;    /* Shadow disappears — button is "flat" now */
  transform: translateY(6px);   /* Moves down fully — pressed in */
}
```

**What `:active` does:** `:active` applies styles during the moment a button is being clicked (mouse is held down). This creates a physical "press down" sensation.

**Expected result:** The button looks 3D with a bottom edge shadow. Hovering moves it slightly. Clicking presses it all the way down, removing the shadow.

---

### 2.5 Animated Border / Outline Grow on Hover

This effect adds a border outline that smoothly grows in on hover:

```css
.btn-outline-grow {
  background-color: #4CAF50;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
  border-radius: 4px;
  outline: 2px solid transparent;        /* Invisible outline to start */
  outline-offset: 0px;
  transition: outline-offset 0.3s ease, outline-color 0.3s ease;
}

.btn-outline-grow:hover {
  outline-color: #4CAF50;                /* Green outline appears */
  outline-offset: 5px;                   /* Pushes outline away from button */
}
```

**Expected result:** On hover, a green ring grows outward around the button, separated from its edge by a small gap.

---

### 2.6 Background Colour Sweep / Slide Effect

This advanced effect uses a CSS gradient trick to make colour sweep in from one side on hover:

```css
.btn-sweep {
  position: relative;
  color: #4CAF50;
  background-color: transparent;
  border: 2px solid #4CAF50;
  padding: 13px 30px;
  font-size: 16px;
  cursor: pointer;
  border-radius: 4px;
  overflow: hidden;              /* Clips the sweeping element */
  z-index: 0;
  transition: color 0.4s ease;
}

/* The pseudo-element that sweeps across */
.btn-sweep::before {
  content: "";
  position: absolute;
  top: 0;
  left: -100%;                   /* Starts fully off-screen to the left */
  width: 100%;
  height: 100%;
  background-color: #4CAF50;
  z-index: -1;                   /* Behind the text */
  transition: left 0.4s ease;   /* Animates the left position */
}

.btn-sweep:hover::before {
  left: 0;                       /* Sweeps in from the left */
}

.btn-sweep:hover {
  color: white;                  /* Text becomes white as background arrives */
}
```

**Step-by-step breakdown:**
1. The button starts as a transparent outline button with green text
2. A `::before` pseudo-element sits behind the button content, off-screen to the left
3. On hover, the pseudo-element slides in from left to right (its `left` property animates from `-100%` to `0`)
4. The button text colour transitions from green to white simultaneously
5. Result: a green background sweeps in from the left, "filling" the button

**Expected result:** A smooth colour sweep from left to right when hovered. Looks very sophisticated.

> **What is `::before`?** It is a pseudo-element — an invisible extra "element" that CSS inserts before the content of a real element. It has no HTML tag; it exists purely in CSS. You must always set `content: ""` for it to appear.

---

### 2.7 Glow Effect

A glowing button uses `box-shadow` with a bright, blurred colour:

```css
.btn-glow {
  background-color: #4CAF50;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
  border-radius: 4px;
  box-shadow: none;
  transition: box-shadow 0.3s ease;
}

.btn-glow:hover {
  box-shadow: 0 0 15px 5px rgba(76, 175, 80, 0.7);  /* Coloured glow */
}
```

**`box-shadow` breakdown:** `0 0 15px 5px rgba(76, 175, 80, 0.7)`

| Value | Meaning |
|-------|---------|
| `0` | No horizontal offset (glow is centred) |
| `0` | No vertical offset |
| `15px` | Blur radius (how spread out the glow is) |
| `5px` | Spread radius (how large the glow starts before blurring) |
| `rgba(76,175,80,0.7)` | Semi-transparent green (matches the button) |

**Expected result:** A soft, coloured halo appears around the button on hover.

> **Tip:** Match the glow colour to the button's background colour for the best effect. For a blue button: `rgba(0, 140, 186, 0.7)`. For red: `rgba(244, 67, 54, 0.7)`.

---

### 2.8 Scale / Zoom on Hover

A subtle zoom effect gives a sense of energy:

```css
.btn-zoom {
  background-color: #008CBA;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
  border-radius: 4px;
  transition: transform 0.2s ease;
}

.btn-zoom:hover {
  transform: scale(1.08);   /* Grows to 108% of original size */
}
```

**Expected result:** The button gently grows 8% larger on hover.

> **Warning:** Do not scale too aggressively (e.g., `scale(1.5)`). Subtle changes of 5–10% feel professional. Large changes feel clunky.

---

### 2.9 Rotate Effect

A playful rotate on hover — good for icon buttons or fun, casual UIs:

```css
.btn-rotate {
  background-color: #ff9800;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
  border-radius: 4px;
  transition: transform 0.3s ease;
}

.btn-rotate:hover {
  transform: rotate(5deg);   /* Tilts 5 degrees clockwise */
}
```

**Expected result:** The button tilts slightly on hover — subtle and fun.

---

### 2.10 Opacity Fade on Hover

The simplest possible hover effect — the button becomes slightly transparent:

```css
.btn-fade {
  background-color: #4CAF50;
  color: white;
  padding: 15px 32px;
  border: none;
  cursor: pointer;
  font-size: 16px;
  border-radius: 4px;
  opacity: 1;
  transition: opacity 0.3s ease;
}

.btn-fade:hover {
  opacity: 0.7;   /* 70% opacity — slightly see-through */
}
```

**Expected result:** The button dims slightly on hover.

---

### 2.11 The Full `transition` Shorthand

You can animate multiple properties at once:

```css
button {
  transition: background-color 0.3s ease,
              box-shadow 0.3s ease,
              transform 0.2s ease,
              color 0.3s ease;
}
```

Or use the shorthand `all` to transition every changing property:

```css
button {
  transition: all 0.3s ease;
}
```

> **Caution with `all`:** Using `all` can trigger unwanted transitions on properties you didn't intend (like `width` when the page loads). For precise control, list specific properties separately.

---

## Part 3 — Button Groups

### 3.1 What is a Button Group?

A **button group** is a set of buttons placed together so they appear as a single connected unit — like a row of tabs or a segmented control.

You see these on:
- Alignment tools ("Left | Centre | Right")
- Pagination bars ("← 1 2 3 4 5 →")
- Toolbars and filter selectors
- Social media share button rows

The core technique is to remove the gaps between buttons and handle borders carefully so adjacent buttons share a border rather than doubling up.

---

### 3.2 Basic Horizontal Button Group

```css
.btn-group {
  display: inline-flex;  /* Places buttons in a row */
}

.btn-group button {
  background-color: #4CAF50;
  color: white;
  padding: 10px 20px;
  font-size: 15px;
  cursor: pointer;
  border: 1px solid #3d8b40;  /* Thin green border */
  border-right: none;          /* Removes right border to avoid doubling */
  transition: background-color 0.2s;
}

/* Restore the right border on the last button */
.btn-group button:last-child {
  border-right: 1px solid #3d8b40;
}

/* Round only the outer corners */
.btn-group button:first-child {
  border-radius: 4px 0 0 4px;  /* Top-left, top-right, bottom-right, bottom-left */
}

.btn-group button:last-child {
  border-radius: 0 4px 4px 0;
}

.btn-group button:hover {
  background-color: #3d8b40;
}
```

```html
<div class="btn-group">
  <button>Left</button>
  <button>Centre</button>
  <button>Right</button>
</div>
```

**Expected result:** Three buttons joined as one connected bar. The left button has rounded left corners, the right button has rounded right corners, the middle button has no rounded corners. No double borders.

> **The `border-right: none` trick:** Without this, each button would have a right border AND the next button would have a left border — creating a thick double line between buttons. Removing all right borders except the last one solves this elegantly.

---

### 3.3 Understanding `border-radius` for Groups

The 4-value `border-radius` notation:

```css
border-radius: top-left  top-right  bottom-right  bottom-left;
```

So for the **first** button in a group:

```css
border-radius: 4px 0 0 4px;
/*             TL  TR  BR  BL */
/* Round left corners, square right corners */
```

For the **last** button:

```css
border-radius: 0 4px 4px 0;
/*             TL  TR  BR  BL */
/* Square left corners, round right corners */
```

Middle buttons: `border-radius: 0` (all corners square).

---

### 3.4 Button Group Using `<a>` Tags (Navigation Bar)

Button groups are also commonly built with links styled as buttons — perfect for navigation menus:

```css
.nav-group {
  display: inline-flex;
}

.nav-group a {
  background-color: #555;
  color: white;
  padding: 12px 20px;
  font-size: 15px;
  text-decoration: none;         /* Remove underline from links */
  border-right: 1px solid #777;  /* Divider line between links */
  transition: background-color 0.2s;
}

.nav-group a:last-child {
  border-right: none;
}

.nav-group a:first-child {
  border-radius: 4px 0 0 4px;
}

.nav-group a:last-child {
  border-radius: 0 4px 4px 0;
}

.nav-group a:hover {
  background-color: #333;
}
```

```html
<div class="nav-group">
  <a href="#">Home</a>
  <a href="#">About</a>
  <a href="#">Portfolio</a>
  <a href="#">Contact</a>
</div>
```

**Expected result:** A connected navigation bar with equal-sized link buttons, a divider between each, and a darker hover state.

---

### 3.5 Vertical Button Group

Vertical button groups stack buttons top-to-bottom in a connected column:

```css
.btn-group-vertical {
  display: inline-flex;
  flex-direction: column;   /* Stack vertically instead of horizontally */
}

.btn-group-vertical button {
  background-color: #4CAF50;
  color: white;
  padding: 10px 20px;
  font-size: 15px;
  cursor: pointer;
  border: 1px solid #3d8b40;
  border-bottom: none;       /* Remove bottom border to avoid doubling */
  width: 120px;              /* Give all buttons the same width */
  transition: background-color 0.2s;
}

.btn-group-vertical button:last-child {
  border-bottom: 1px solid #3d8b40;   /* Restore bottom border on last */
}

.btn-group-vertical button:first-child {
  border-radius: 4px 4px 0 0;   /* Round top corners only */
}

.btn-group-vertical button:last-child {
  border-radius: 0 0 4px 4px;   /* Round bottom corners only */
}

.btn-group-vertical button:hover {
  background-color: #3d8b40;
}
```

```html
<div class="btn-group-vertical">
  <button>Top</button>
  <button>Middle</button>
  <button>Bottom</button>
</div>
```

**Expected result:** Three buttons stacked as a connected vertical column, rounded only at the very top and very bottom.

---

### 3.6 Mixed-Colour Button Group

Button groups can use different colours — useful for toggle groups or "like / dislike" controls:

```css
.btn-group-mixed {
  display: inline-flex;
}

.btn-group-mixed button {
  padding: 10px 20px;
  font-size: 15px;
  cursor: pointer;
  border: none;
  color: white;
  transition: opacity 0.2s;
}

.btn-group-mixed button:hover {
  opacity: 0.85;
}

.btn-group-mixed .btn-yes {
  background-color: #4CAF50;
  border-radius: 4px 0 0 4px;
}

.btn-group-mixed .btn-no {
  background-color: #f44336;
  border-radius: 0 4px 4px 0;
}
```

```html
<div class="btn-group-mixed">
  <button class="btn-yes">👍 Yes</button>
  <button class="btn-no">👎 No</button>
</div>
```

**Expected result:** A two-button group — green "Yes" on the left, red "No" on the right.

---

### 3.7 Active State in a Button Group

To show which button in a group is currently selected (like the active tab in a filter):

```css
.btn-group-filter button.active {
  background-color: #2e6da4;    /* Darker, clearly selected */
  box-shadow: inset 0 2px 4px rgba(0,0,0,0.3);  /* Inset shadow = "pressed in" */
  color: white;
}
```

The `inset` keyword on `box-shadow` puts the shadow *inside* the element rather than outside — making it look sunken/pressed.

```html
<div class="btn-group btn-group-filter">
  <button class="active">All</button>
  <button>Active</button>
  <button>Completed</button>
</div>
```

**Expected result:** "All" appears pressed in and darker than the other buttons, indicating it is selected.

---

### 3.8 Button Group with Spacing (Not Connected)

Sometimes you want buttons near each other but with small gaps — not connected as one unit:

```css
.btn-group-spaced {
  display: inline-flex;
  gap: 8px;    /* Space between buttons */
}

.btn-group-spaced button {
  background-color: #008CBA;
  color: white;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  font-size: 15px;
  border-radius: 4px;
  transition: background-color 0.2s;
}

.btn-group-spaced button:hover {
  background-color: #006f94;
}
```

```html
<div class="btn-group-spaced">
  <button>Save</button>
  <button>Preview</button>
  <button>Publish</button>
</div>
```

**Expected result:** Three separate but closely aligned buttons with a small gap between each. No shared borders.

---

## Part 4 — Code Challenge Concepts

The W3Schools challenges for CSS buttons test your ability to combine properties to match a target design. Here are the key challenge patterns and how to approach them.

### Challenge Pattern 1: Recreate a Button Exactly

You are shown a button and must match it precisely. The mental checklist:

1. **Background colour** — Is it solid or transparent?
2. **Text colour** — White, dark, or matching the border?
3. **Padding** — How much breathing room does it have?
4. **Font size** — How large is the text relative to the button?
5. **Border** — Solid? Dashed? What colour and width?
6. **Border-radius** — Pill? Slightly rounded? Squared?
7. **Cursor** — Is `pointer` set?

### Challenge Pattern 2: Hover Behaviour

You click "Run" and hover over the button. Does it:
- Change colour? → `background-color` on `:hover`
- Grow a shadow? → `box-shadow` on `:hover`
- Move? → `transform` on `:hover`
- Add an outline ring? → `outline` on `:hover`

Always check if a `transition` is needed.

### Challenge Pattern 3: Button Group Layout

Key things that must be set for a connected group:
- `display: inline-flex` on the container
- Shared borders (not doubled)
- Rounded corners only on the outer edges
- Hover state per button

---

## Part 5 — Guided Practice Exercises

### Exercise 1: Build All Button Variants

**Objective:** Build a single HTML page that demonstrates all the following button types.

**Requirements:**

```html
<!DOCTYPE html>
<html>
<head>
  <title>Button Library</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    h2 { margin: 20px 0 10px; color: #333; }
    .row { display: flex; gap: 10px; flex-wrap: wrap; margin-bottom: 15px; }

    /* Base button reset */
    .btn {
      padding: 12px 24px;
      font-size: 15px;
      border: none;
      cursor: pointer;
      border-radius: 4px;
      transition: all 0.3s ease;
      display: inline-block;
    }

    /* Colours */
    .btn-green  { background-color: #4CAF50; color: white; }
    .btn-blue   { background-color: #008CBA; color: white; }
    .btn-red    { background-color: #f44336; color: white; }
    .btn-orange { background-color: #ff9800; color: white; }
    .btn-grey   { background-color: #9e9e9e; color: white; }

    /* Hover — darken */
    .btn-green:hover  { background-color: #388e3c; }
    .btn-blue:hover   { background-color: #006f94; }
    .btn-red:hover    { background-color: #d32f2f; }
    .btn-orange:hover { background-color: #e65100; }
    .btn-grey:hover   { background-color: #757575; }

    /* Sizes */
    .btn-sm { padding: 7px 14px; font-size: 12px; }
    .btn-lg { padding: 18px 36px; font-size: 20px; }

    /* Pill */
    .btn-pill { border-radius: 50px; }

    /* Outline */
    .btn-outline {
      background-color: transparent;
      border: 2px solid #4CAF50;
      color: #4CAF50;
      padding: 10px 22px;
    }
    .btn-outline:hover { background-color: #4CAF50; color: white; }

    /* Full width */
    .btn-full { width: 100%; }

    /* Disabled */
    .btn-disabled {
      background-color: #ccc;
      color: #888;
      cursor: not-allowed;
      opacity: 0.65;
    }
  </style>
</head>
<body>

  <h2>Colour Variants</h2>
  <div class="row">
    <button class="btn btn-green">Green</button>
    <button class="btn btn-blue">Blue</button>
    <button class="btn btn-red">Red</button>
    <button class="btn btn-orange">Orange</button>
    <button class="btn btn-grey">Grey</button>
  </div>

  <h2>Sizes</h2>
  <div class="row" style="align-items:center;">
    <button class="btn btn-blue btn-sm">Small</button>
    <button class="btn btn-blue">Medium</button>
    <button class="btn btn-blue btn-lg">Large</button>
  </div>

  <h2>Pill Shape</h2>
  <div class="row">
    <button class="btn btn-green btn-pill">Pill Button</button>
    <button class="btn btn-blue btn-pill">Pill Button</button>
  </div>

  <h2>Outline</h2>
  <div class="row">
    <button class="btn btn-outline">Outline (Hover Me)</button>
  </div>

  <h2>Full Width</h2>
  <button class="btn btn-blue btn-full">Full Width Button</button>

  <h2>Disabled</h2>
  <div class="row">
    <button class="btn btn-disabled">Disabled</button>
  </div>

</body>
</html>
```

**Self-check:**
- Do all hover states work smoothly?
- Does the outline button fill with colour on hover?
- Does the disabled button show `not-allowed` cursor?

---

### Exercise 2: Hover Effect Showcase

**Objective:** Create one button for each of these 5 hover effects, labelled clearly.

| Button Label | Effect to apply |
|---|---|
| "Lift" | Shadow grows + `translateY(-3px)` |
| "Glow" | Green `box-shadow` glow appears |
| "Sweep" | Colour sweeps from left using `::before` |
| "Zoom" | Button scales to 108% |
| "Press" | Button uses `box-shadow` bottom edge, depresses on `:active` |

**Hint for "Sweep":**
```css
.btn-sweep {
  position: relative;
  overflow: hidden;
  z-index: 0;
}
.btn-sweep::before {
  content: "";
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background-color: /* darker shade */;
  z-index: -1;
  transition: left 0.4s ease;
}
.btn-sweep:hover::before {
  left: 0;
}
```

---

### Exercise 3: Build a Button Group Navigation Bar

**Objective:** Build a horizontal navigation bar using a button group with 5 links: Home, About, Services, Portfolio, Contact.

**Requirements:**
- Connected (no gaps between buttons)
- First and last buttons have outer rounded corners
- Hover changes to a darker colour
- One button has class `active` and appears pressed in (darker + inset shadow)

**Expected output:** A professional navigation bar that could be placed on a real website header.

---

### Exercise 4: Filter Toggle Group

**Objective:** Build a "filter" button group with the options: All | Design | Development | Marketing

**Requirements:**
- All four buttons connected in a horizontal group
- "All" is the active/selected button (darker + inset shadow)
- Hover on non-active buttons changes their colour slightly

```html
<div class="btn-group-filter">
  <button class="active">All</button>
  <button>Design</button>
  <button>Development</button>
  <button>Marketing</button>
</div>
```

---

## Part 6 — Mini-Project: Complete Action Panel

### Project Overview

You will build a polished, self-contained **Action Panel** — a section of a page that could appear in a real admin dashboard, a sign-up page, or a product page. It combines all the techniques from this lesson.

### What You Will Build

A card-style panel containing:
1. A title and description
2. A row of primary action buttons (styled, with hover effects)
3. A horizontal button group for filter/tab selection
4. A full-width call-to-action button at the bottom
5. A disabled button to show unavailable state

---

### Stage 1: HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Action Panel</title>
  <link rel="stylesheet" href="action-panel.css">
</head>
<body>

  <div class="panel">
    <h2 class="panel-title">Project Actions</h2>
    <p class="panel-desc">Choose an action to perform on the selected project.</p>

    <!-- Primary Actions -->
    <div class="action-row">
      <button class="btn btn-success btn-lift">✔ Save</button>
      <button class="btn btn-primary btn-glow">👁 Preview</button>
      <button class="btn btn-outline-green btn-sweep-btn">⬇ Export</button>
      <button class="btn btn-danger btn-zoom">✖ Delete</button>
      <button class="btn btn-disabled" disabled>🔒 Archive</button>
    </div>

    <!-- Filter Group -->
    <h3 class="section-label">View by Status</h3>
    <div class="btn-group">
      <button class="active">All</button>
      <button>Active</button>
      <button>Paused</button>
      <button>Completed</button>
    </div>

    <!-- Full Width CTA -->
    <button class="btn btn-cta">🚀 Publish Project</button>
  </div>

</body>
</html>
```

---

### Stage 2: Base CSS (`action-panel.css`)

```css
/* ==========================================
   RESET & PAGE
   ========================================== */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Segoe UI', Arial, sans-serif;
  background: #f0f2f5;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

/* ==========================================
   PANEL CARD
   ========================================== */
.panel {
  background: white;
  padding: 36px 40px;
  border-radius: 12px;
  box-shadow: 0 8px 30px rgba(0,0,0,0.12);
  max-width: 680px;
  width: 100%;
}

.panel-title {
  font-size: 22px;
  color: #222;
  margin-bottom: 6px;
}

.panel-desc {
  font-size: 14px;
  color: #666;
  margin-bottom: 24px;
}

.section-label {
  font-size: 14px;
  color: #888;
  font-weight: normal;
  margin: 24px 0 10px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
```

---

### Stage 3: Button Base Styles

```css
/* ==========================================
   BUTTON BASE
   ========================================== */
.btn {
  padding: 12px 22px;
  font-size: 15px;
  border: none;
  cursor: pointer;
  border-radius: 6px;
  font-family: inherit;
  font-weight: 500;
  transition: all 0.3s ease;
}

.btn-success  { background-color: #4CAF50; color: white; }
.btn-primary  { background-color: #1976d2; color: white; }
.btn-danger   { background-color: #e53935; color: white; }

.btn-outline-green {
  background-color: transparent;
  border: 2px solid #4CAF50;
  color: #4CAF50;
  padding: 10px 20px;
}

.btn-disabled {
  background-color: #ddd;
  color: #aaa;
  cursor: not-allowed;
  opacity: 0.7;
}

/* Action row layout */
.action-row {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}
```

---

### Stage 4: Hover Effects

```css
/* ==========================================
   HOVER EFFECTS
   ========================================== */

/* Lift */
.btn-lift:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 20px rgba(76, 175, 80, 0.4);
}
.btn-lift:active {
  transform: translateY(0);
}

/* Glow */
.btn-glow:hover {
  box-shadow: 0 0 18px 4px rgba(25, 118, 210, 0.55);
}

/* Outline sweep */
.btn-sweep-btn {
  position: relative;
  overflow: hidden;
  z-index: 0;
}
.btn-sweep-btn::before {
  content: "";
  position: absolute;
  top: 0; left: -100%;
  width: 100%; height: 100%;
  background-color: #4CAF50;
  z-index: -1;
  transition: left 0.35s ease;
}
.btn-sweep-btn:hover::before { left: 0; }
.btn-sweep-btn:hover { color: white; }

/* Zoom */
.btn-zoom:hover {
  transform: scale(1.07);
  background-color: #c62828;
}
```

---

### Stage 5: Button Group Styles

```css
/* ==========================================
   BUTTON GROUP
   ========================================== */
.btn-group {
  display: inline-flex;
}

.btn-group button {
  background-color: #e8f4fd;
  color: #1976d2;
  padding: 10px 20px;
  font-size: 14px;
  cursor: pointer;
  border: 1px solid #90caf9;
  border-right: none;
  font-family: inherit;
  transition: background-color 0.2s, color 0.2s;
}

.btn-group button:last-child {
  border-right: 1px solid #90caf9;
}

.btn-group button:first-child {
  border-radius: 6px 0 0 6px;
}

.btn-group button:last-child {
  border-radius: 0 6px 6px 0;
}

.btn-group button:hover {
  background-color: #bbdefb;
}

.btn-group button.active {
  background-color: #1976d2;
  color: white;
  box-shadow: inset 0 2px 5px rgba(0,0,0,0.2);
}
```

---

### Stage 6: Full-Width CTA Button

```css
/* ==========================================
   CALL TO ACTION
   ========================================== */
.btn-cta {
  width: 100%;
  margin-top: 28px;
  padding: 16px;
  font-size: 17px;
  font-weight: bold;
  background: linear-gradient(135deg, #43a047, #1976d2);  /* Green → Blue gradient */
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 8px;
  letter-spacing: 0.5px;
  transition: transform 0.2s ease, box-shadow 0.3s ease;
}

.btn-cta:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(25, 118, 210, 0.4);
}

.btn-cta:active {
  transform: translateY(0);
}
```

---

### Milestone Output Check

Open your `action-panel.html` in a browser and verify:

- ✅ "Save" button lifts upward with a green shadow on hover
- ✅ "Preview" button gets a blue glow on hover
- ✅ "Export" button sweeps in from left on hover, becoming solid green
- ✅ "Delete" button zooms and darkens on hover
- ✅ "Archive" button shows `not-allowed` cursor and cannot be activated
- ✅ Filter group appears as a connected bar; "All" looks selected (darker)
- ✅ Filter buttons highlight on hover
- ✅ "Publish Project" is full-width with gradient, lifts on hover

---

### Optional Enhancements

- Add a dark mode version using CSS custom properties (`--btn-bg: #333;`)
- Make the filter group switch the `active` class with JavaScript (one line: `this.parentElement.querySelectorAll('button').forEach(b=>b.classList.remove('active')); this.classList.add('active');`)
- Add a loading state to the "Publish" button: on click, change text to "Publishing…" and add a spinner animation
- Make the panel responsive — stack buttons vertically on screens under 480px using a media query

---

## Part 7 — Common Beginner Mistakes

### Mistake 1: Forgetting `cursor: pointer`

**Wrong:**
```css
.btn { background-color: blue; color: white; padding: 10px 20px; }
```

**Problem:** The cursor remains an arrow over the button (for `<div>` and `<a>` elements), making it look un-clickable.

**Correct:**
```css
.btn { background-color: blue; color: white; padding: 10px 20px; cursor: pointer; }
```

---

### Mistake 2: Transition on `:hover` only (instead of the base element)

**Wrong:**
```css
button { background-color: green; }
button:hover { background-color: darkgreen; transition: background-color 0.3s; }
```

**Problem:** The transition plays when going *into* hover, but *snaps back* instantly when you move the mouse off.

**Correct:** Always put `transition` on the *base* element, not the `:hover` state:

```css
button { background-color: green; transition: background-color 0.3s; }
button:hover { background-color: darkgreen; }
```

---

### Mistake 3: Double borders in a button group

**Wrong:**
```css
.btn-group button { border: 1px solid grey; }
/* Adjacent buttons each have a border = 2px thick gap between them */
```

**Correct:**
```css
.btn-group button {
  border: 1px solid grey;
  border-right: none;          /* Remove right border */
}
.btn-group button:last-child {
  border-right: 1px solid grey;  /* Restore only on the last one */
}
```

---

### Mistake 4: Rounding all corners on button group buttons

**Wrong:**
```css
.btn-group button { border-radius: 4px; }
/* All four corners of every button are rounded = gaps between buttons */
```

**Correct:**
```css
.btn-group button:first-child { border-radius: 4px 0 0 4px; }
.btn-group button:last-child  { border-radius: 0 4px 4px 0; }
/* Middle buttons: no border-radius at all */
```

---

### Mistake 5: Using `width: 100%` without a block display context

**Wrong:** Setting `width: 100%` on a button inside a flex container often does not give full width across the page as expected.

**Correct:** Make sure the button's parent is `display: block` (or the button itself is `display: block`):
```css
.btn-full {
  display: block;
  width: 100%;
}
```

---

### Mistake 6: Forgetting `overflow: hidden` on the sweep animation container

**Wrong:**
```css
.btn-sweep { position: relative; }  /* Forgot overflow: hidden */
.btn-sweep::before { content:""; position:absolute; left:-100%; width:100%; ... }
```

**Problem:** The `::before` element is visible off to the left of the button before the hover animation. The background bleeds out.

**Correct:**
```css
.btn-sweep { position: relative; overflow: hidden; }
```

---

### Mistake 7: Applying `transform` without `transition`

**Wrong:**
```css
button:hover { transform: scale(1.1); }
/* Snaps to 110% instantly — jarring */
```

**Correct:**
```css
button { transition: transform 0.2s ease; }
button:hover { transform: scale(1.1); }
/* Smoothly grows to 110% over 0.2 seconds */
```

---

### Mistake 8: Using `border: none` then adding `border` on `:hover` without accounting for size shift

**Wrong:**
```css
button { border: none; padding: 12px 24px; }
button:hover { border: 2px solid blue; }
/* The button grows by 4px total on hover (2px each side) — causes layout shift! */
```

**Correct:** Use `outline` for hover borders instead — it does not affect layout:
```css
button { border: none; outline: 2px solid transparent; outline-offset: 0; transition: outline 0.3s; }
button:hover { outline-color: blue; }
```

Or start with the border already present but transparent:
```css
button { border: 2px solid transparent; }
button:hover { border-color: blue; }
```

---

## Part 8 — Reflection Questions

1. **Why is `cursor: pointer` important even on `<button>` elements?** *(Hint: think about browsers, `<a>` tags, and custom elements)*

2. **Why should you put `transition` on the base element instead of the `:hover` state? What visual problem does putting it on `:hover` cause?**

3. **A button group has 5 buttons. Without the `border-right: none` technique, what would the gap between buttons look like, and why?**

4. **What is the difference between `box-shadow` and `filter: drop-shadow()`? Which would you prefer for a button, and why?**

5. **The sweep effect uses a `::before` pseudo-element. What would happen if you removed `z-index: -1` from the `::before` style?**

6. **You want a button that looks "pressed in" when active. What two CSS properties create this sunken/depressed feeling?**

7. **Why does `transform: translateY(-3px)` on `:hover` make a button look like it "lifts"? What physical analogy does this create in the user's mind?**

8. **A designer asks for a button group where the selected button looks "pressed in". Which CSS property creates an inset shadow, and what keyword do you use?**

---

## Part 9 — Completion Checklist

Before moving on, confirm you can do all of the following:

- [ ] Style a plain `<button>` with background colour, text colour, padding, font size, border, and border-radius
- [ ] Set multiple button colour variants (green, blue, red, orange, grey)
- [ ] Control button size through `padding` and `font-size`
- [ ] Create a full-width button with `width: 100%`
- [ ] Create a pill-shaped button with `border-radius: 50px`
- [ ] Create an outline/ghost button with `background: transparent` and `border`
- [ ] Style a disabled button with `cursor: not-allowed` and reduced opacity
- [ ] Add a smooth background colour change on hover using `transition`
- [ ] Create a shadow lift effect using `transform: translateY()` and `box-shadow`
- [ ] Create a 3D press effect using `box-shadow` bottom edge and `:active`
- [ ] Create a glow effect using a coloured, blurred `box-shadow`
- [ ] Create a colour sweep effect using `::before` and `left: -100%` → `left: 0`
- [ ] Add a zoom effect using `transform: scale()`
- [ ] Understand why `transition` belongs on the base element, not `:hover`
- [ ] Build a horizontal button group with `display: inline-flex`, shared borders, and outer rounded corners
- [ ] Build a vertical button group with `flex-direction: column`
- [ ] Add an active/selected state to a button group item using `.active` class and `box-shadow: inset`
- [ ] Recognise and fix the 8 common beginner mistakes

---

## Lesson Summary

In this lesson, you went from understanding a plain grey browser button to being able to create sophisticated, animated, interactive button systems from scratch.

**Part 1 — Basic Styling:** The core recipe for any button is `background-color`, `color`, `padding`, `font-size`, `border: none`, `cursor: pointer`, and `border-radius`. From there, you apply colour semantics (green = success, red = danger, blue = primary), adjust sizes through padding and font size, create pill shapes with large `border-radius`, and build outline buttons with `background: transparent`.

**Part 2 — Hover Effects:** Every good hover effect pairs a CSS property change on `:hover` with `transition` on the base element. You learned eight distinct effects: background colour change, shadow lift with `translateY`, 3D press with `:active`, outline grow, colour sweep with `::before`, glow with coloured `box-shadow`, scale zoom, and opacity fade. Each uses `transition` to make the change smooth and professional.

**Part 3 — Button Groups:** Button groups use `display: inline-flex` on a container. The key technique is removing `border-right` from all buttons except the last one (to avoid double borders), and using the 4-value `border-radius` (`TL TR BR BL`) to round only the outer corners. Vertical groups use `flex-direction: column` and remove `border-bottom` instead. The active/selected state uses `box-shadow: inset` to create a pressed-in appearance.

**Part 4 — Challenges:** The challenges test your ability to read a visual target and replicate it by identifying colour, padding, font size, border, border-radius, cursor, hover state, and transition.

---

> **Next up:** Lesson 62 covers CSS Pagination — how to build numbered page navigation bars using button-group and styling techniques that directly build on what you learned here.
