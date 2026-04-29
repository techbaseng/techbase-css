---
render_with_liquid: false
title: "CSS Flexbox — Flexible Box Layout Complete Guide"
nav_order: 69
---

# Lesson 69 — CSS Flexbox: Flexible Box Layout, Containers, Items, and Responsive Design

---

## Lesson Introduction

Have you ever tried to centre something perfectly on a webpage and ended up fighting with `margin: auto`, `float`, and endless guessing? Or built a row of cards that looked fine on a big screen but collapsed into a mess on a phone? For years, web developers struggled with these exact problems using old layout tools that were never really designed for the job.

**CSS Flexbox** (short for Flexible Box Layout) was built specifically to solve those problems. It gives you a powerful, intuitive system for arranging elements in rows or columns — aligning them, distributing space between them, and making them adapt to different screen sizes — all with just a handful of well-named CSS properties.

In this lesson you will learn:

- What Flexbox is, why it exists, and how it thinks about layout
- How to turn any element into a **flex container**
- How to control direction, wrapping, and the main axis with container properties
- How to align items along both axes (`justify-content`, `align-items`, `align-content`)
- How to control individual **flex items** — their size, order, growth, and shrinkage
- How to build fully **responsive layouts** using Flexbox and media queries
- How to apply everything in a real mini-project

No prior Flexbox knowledge is required. A basic understanding of HTML and CSS (selectors, properties, values) is enough to follow along.

---

## Prerequisite Concepts

### What is "layout" in CSS?

Layout means deciding how elements are positioned and sized on the page — how they sit next to each other, how much space they take, and where they appear when the screen is resized.

### The Problem with Old Layout Methods

Before Flexbox, layout was done with:

- **`float`** — originally for wrapping text around images, awkwardly repurposed for columns
- **`position: absolute/relative`** — powerful but fragile; elements fall out of the normal flow
- **`display: inline-block`** — creates strange gaps between elements

These tools were unpredictable, required hacks, and did not handle varying content sizes or different screen sizes gracefully.

### What Flexbox Offers

Flexbox introduces a **parent-child relationship** for layout:

- The **parent** element is called the **flex container**. You set rules on it that control how its children are arranged.
- The **children** inside it are called **flex items**. They automatically respond to the container's rules, and you can also give them individual rules.

Think of a flex container like a **tray** holding items. The tray decides whether items line up left-to-right or top-to-bottom, how much space sits between them, and whether they wrap onto new lines. Each item on the tray can also have its own rules about how big it should be.

---

## Part 1 — What is Flexbox and How Do You Activate It?

### Activating Flexbox

You turn any HTML element into a flex container by writing one line of CSS:

```css
display: flex;
```

That is it. Once you do this, all **direct children** of that element automatically become flex items and are arranged according to flexbox rules.

**Before Flexbox (block layout):**

```html
<div class="container">
  <div class="box">Box 1</div>
  <div class="box">Box 2</div>
  <div class="box">Box 3</div>
</div>
```

```css
.container {
  /* No display: flex — default block layout */
}
.box {
  background-color: #4CAF50;
  color: white;
  padding: 20px;
  margin: 5px;
}
```

**Expected result without Flexbox:** Each `.box` is a block element and stacks vertically — one box per line.

---

**After adding Flexbox:**

```css
.container {
  display: flex;   /* ← This one line changes everything */
}
.box {
  background-color: #4CAF50;
  color: white;
  padding: 20px;
  margin: 5px;
}
```

**Expected result WITH Flexbox:** All three boxes appear in a **row** side by side, left to right.

> 🤔 **Think About This:** You only changed the container, not the boxes themselves. Yet the boxes changed how they look. This is the parent-child power of Flexbox — the container decides how its children behave.

---

### The Two Axes of Flexbox

Flexbox works along **two axes**. Understanding these axes is the key to understanding every property that follows.

```
MAIN AXIS (default: horizontal → left to right)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━►

  ┌─────────┐  ┌─────────┐  ┌─────────┐
  │  Item 1 │  │  Item 2 │  │  Item 3 │      ▲
  └─────────┘  └─────────┘  └─────────┘      │
                                              CROSS AXIS
                                          (default: vertical ↓)
```

- The **main axis** runs in the direction items are placed (default: left to right)
- The **cross axis** runs perpendicular to the main axis (default: top to bottom)

When you change the direction, the axes rotate. This is critical — keep it in mind throughout the lesson.

---

### `display: inline-flex`

There is also `display: inline-flex`. The difference:

- `display: flex` — the container itself becomes a block-level element (takes full row width)
- `display: inline-flex` — the container becomes inline (sits alongside other inline content)

```css
/* The container takes full width */
.container { display: flex; }

/* The container is only as wide as its content */
.container { display: inline-flex; }
```

Most of the time you will use `display: flex`.

---

## Part 2 — Flex Container Properties

These are properties you set **on the parent/container** to control how all its children are arranged.

---

### `flex-direction` — Which Way Do Items Go?

`flex-direction` controls the direction of the **main axis** — the direction items are placed.

**Syntax:**
```css
.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
```

| Value | What it does |
|-------|-------------|
| `row` | Items placed left to right (default) |
| `row-reverse` | Items placed right to left |
| `column` | Items placed top to bottom |
| `column-reverse` | Items placed bottom to top |

**Example 1 — `flex-direction: row` (default):**

```css
.container {
  display: flex;
  flex-direction: row;
}
```

```
[ Item 1 ] [ Item 2 ] [ Item 3 ]
→ left to right
```

---

**Example 2 — `flex-direction: column`:**

```css
.container {
  display: flex;
  flex-direction: column;
}
```

```
[ Item 1 ]
[ Item 2 ]   ↓ top to bottom
[ Item 3 ]
```

> 💡 **Important:** When you switch to `column`, the **main axis is now vertical** and the **cross axis is now horizontal**. This affects how `justify-content` and `align-items` behave — something beginners often find confusing!

---

**Example 3 — `flex-direction: row-reverse`:**

```css
.container {
  display: flex;
  flex-direction: row-reverse;
}
```

```
[ Item 3 ] [ Item 2 ] [ Item 1 ]
← right to left
```

---

### `flex-wrap` — What Happens When There Is No Room?

By default, flex items all try to fit on one line. If there are too many items to fit, they **shrink** rather than wrap. `flex-wrap` changes this behaviour.

**Syntax:**
```css
.container {
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

| Value | What it does |
|-------|-------------|
| `nowrap` | All items on one line, shrink to fit (default) |
| `wrap` | Items wrap onto new lines as needed |
| `wrap-reverse` | Items wrap in reverse — new lines appear above |

**Example — `flex-wrap: nowrap` (default):**

```css
.container {
  display: flex;
  flex-wrap: nowrap;
  width: 300px;   /* too narrow for 6 items */
}
```

```
[I1][I2][I3][I4][I5][I6]   ← all squashed on one line
```

---

**Example — `flex-wrap: wrap`:**

```css
.container {
  display: flex;
  flex-wrap: wrap;
  width: 300px;
}
```

```
[Item 1][Item 2][Item 3]
[Item 4][Item 5][Item 6]   ← overflow wraps to next line
```

> 💡 **Real-world use:** `flex-wrap: wrap` is essential for responsive card grids. When the screen gets narrow, cards naturally wrap to new rows instead of becoming tiny.

---

**Example — `flex-wrap: wrap-reverse`:**

```css
.container {
  display: flex;
  flex-wrap: wrap-reverse;
}
```

```
[Item 4][Item 5][Item 6]   ← last row appears at TOP
[Item 1][Item 2][Item 3]
```

---

### `flex-flow` — Shorthand for direction + wrap

`flex-flow` combines `flex-direction` and `flex-wrap` in one line:

```css
/* Long form */
.container {
  flex-direction: row;
  flex-wrap: wrap;
}

/* Shorthand — exactly equivalent */
.container {
  flex-flow: row wrap;
}
```

**More examples:**

```css
flex-flow: column nowrap;      /* column direction, no wrapping */
flex-flow: row-reverse wrap;   /* right-to-left with wrapping */
```

---

## Part 3 — Justifying Content Along the Main Axis

### `justify-content` — Space Distribution on the Main Axis

`justify-content` controls how flex items are positioned and spaced **along the main axis** (the direction they are flowing in).

**Syntax:**
```css
.container {
  justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
}
```

To understand each value, imagine 3 boxes inside a wide container. The container has leftover space on the right.

---

**`justify-content: flex-start` (default):**

```
[Box1][Box2][Box3]                    (empty space)
← items packed to the START of the main axis
```

```css
.container {
  display: flex;
  justify-content: flex-start;
}
```

---

**`justify-content: flex-end`:**

```
                    (empty space)[Box1][Box2][Box3]
                                 items packed to the END →
```

```css
.container {
  display: flex;
  justify-content: flex-end;
}
```

---

**`justify-content: center`:**

```
         (space)[Box1][Box2][Box3](space)
                  items centred
```

```css
.container {
  display: flex;
  justify-content: center;
}
```

> 💡 **This is how you centre things horizontally in a row container with one line of CSS!**

---

**`justify-content: space-between`:**

```
[Box1]         [Box2]         [Box3]
  no gap at edges; equal gap BETWEEN items
```

```css
.container {
  display: flex;
  justify-content: space-between;
}
```

This is extremely common for navigation bars — logo on the left, links on the right.

---

**`justify-content: space-around`:**

```
  (half)[Box1](full)(Box2)(full)[Box3](half)
  equal space on EACH SIDE of every item
  (edge gaps are half the size of middle gaps)
```

```css
.container {
  display: flex;
  justify-content: space-around;
}
```

---

**`justify-content: space-evenly`:**

```
  (gap)[Box1](gap)[Box2](gap)[Box3](gap)
  perfectly EQUAL gaps everywhere including edges
```

```css
.container {
  display: flex;
  justify-content: space-evenly;
}
```

> 🤔 **Think About This:** What is the difference between `space-around` and `space-evenly`? In `space-around`, the edge gaps are half the size of middle gaps. In `space-evenly`, ALL gaps are identical.

---

### Remembering `justify-content`

A simple memory trick: **"justify" = along the main axis**. Just like text justification in a word processor adjusts text along the horizontal line, `justify-content` adjusts items along the flex direction.

---

## Part 4 — Aligning Items Along the Cross Axis

### `align-items` — Alignment on the Cross Axis (Single Line)

`align-items` controls how flex items are positioned **along the cross axis** (perpendicular to the direction they flow). For a `row` container, this means vertical alignment.

**Syntax:**
```css
.container {
  align-items: stretch | flex-start | flex-end | center | baseline;
}
```

Imagine 3 boxes in a row inside a tall container. The cross axis runs vertically.

---

**`align-items: stretch` (default):**

```
┌────────────────────────────────┐
│ [Box1] [Box2] [Box3]           │
│                                │
│  items stretch to fill the     │
│  full height of the container  │
└────────────────────────────────┘
```

```css
.container {
  display: flex;
  align-items: stretch;
  height: 200px;
}
```

**Expected result:** All items grow to the container's full height, even if their content is short.

---

**`align-items: flex-start`:**

```
┌────────────────────────────────┐
│ [Box1] [Box2] [Box3]           │  ← items at TOP (cross-axis start)
│                                │
│                                │
│                                │
└────────────────────────────────┘
```

---

**`align-items: flex-end`:**

```
┌────────────────────────────────┐
│                                │
│                                │
│                                │
│ [Box1] [Box2] [Box3]           │  ← items at BOTTOM (cross-axis end)
└────────────────────────────────┘
```

---

**`align-items: center`:**

```
┌────────────────────────────────┐
│                                │
│ [Box1] [Box2] [Box3]           │  ← items CENTRED vertically
│                                │
└────────────────────────────────┘
```

```css
.container {
  display: flex;
  align-items: center;
  height: 200px;
}
```

> 💡 **The famous centring trick:** Combine `justify-content: center` + `align-items: center` to perfectly centre one or more items both horizontally AND vertically inside their container — something that was notoriously difficult before Flexbox!

```css
.container {
  display: flex;
  justify-content: center;   /* centre along main axis (horizontal) */
  align-items: center;       /* centre along cross axis (vertical) */
  height: 300px;
}
```

---

**`align-items: baseline`:**

Items are aligned so their **text baselines** line up — useful when items have different font sizes and you want the text to sit on the same invisible line.

```css
.container {
  display: flex;
  align-items: baseline;
}
```

```
[small text] [BIG TEXT] [medium]
      ↑           ↑        ↑
      All text baselines aligned on same horizontal line
```

---

### `align-content` — Alignment When There Are Multiple Lines

`align-content` only takes effect when items **wrap onto multiple lines** (i.e., when `flex-wrap: wrap` is set and there actually IS wrapping). It controls how the **lines themselves** are distributed along the cross axis.

Think of it as `justify-content` but for the lines/rows rather than for individual items.

**Syntax:**
```css
.container {
  align-content: flex-start | flex-end | center | space-between | space-around | space-evenly | stretch;
}
```

| Value | What it does |
|-------|-------------|
| `flex-start` | Lines packed at the start of the cross axis |
| `flex-end` | Lines packed at the end |
| `center` | Lines centred on the cross axis |
| `space-between` | Equal space between lines, no space at edges |
| `space-around` | Equal space around each line |
| `space-evenly` | Equal space between all lines and edges |
| `stretch` | Lines stretch to fill available space (default) |

**Example:**

```css
.container {
  display: flex;
  flex-wrap: wrap;
  align-content: space-between;
  height: 400px;
}
```

```
┌────────────────────────────────┐
│ [Item1][Item2][Item3]          │  ← Row 1 at top
│                                │
│                                │  ← space between rows
│                                │
│ [Item4][Item5][Item6]          │  ← Row 2 at bottom
└────────────────────────────────┘
```

> ⚠️ **Common confusion:** `align-items` vs `align-content`
> - `align-items` — aligns items **within** a single line (works even without wrapping)
> - `align-content` — aligns the **lines themselves** (only works when there are multiple lines)

---

### Quick Reference: Container Properties Summary

| Property | Controls | Axis |
|----------|---------|------|
| `flex-direction` | Direction items flow | Sets main axis |
| `flex-wrap` | Whether items wrap to new lines | Cross axis |
| `flex-flow` | Shorthand: direction + wrap | Both |
| `justify-content` | Space/position along main axis | Main |
| `align-items` | Position along cross axis (single line) | Cross |
| `align-content` | Position of multiple lines | Cross |

---

## Part 5 — Flex Item Properties

So far we have only set properties on the **container**. Now we look at properties you set on **individual items** to control their own size and behaviour.

---

### `order` — Change the Visual Order of Items

By default, flex items appear in the same order as they appear in the HTML. `order` lets you change the visual order without changing the HTML.

**Syntax:**
```css
.item {
  order: integer;   /* default is 0 */
}
```

Items are sorted from lowest to highest `order` value. Items with the same `order` appear in HTML order.

**Example:**

```html
<div class="container">
  <div class="item" id="a">A</div>   <!-- HTML order: 1st -->
  <div class="item" id="b">B</div>   <!-- HTML order: 2nd -->
  <div class="item" id="c">C</div>   <!-- HTML order: 3rd -->
</div>
```

```css
.container { display: flex; }

#a { order: 3; }   /* A displayed last */
#b { order: 1; }   /* B displayed first */
#c { order: 2; }   /* C displayed second */
```

**Expected result (visual display):** `B → C → A`

Even though in HTML the order is A, B, C — visually they appear as B, C, A.

> 💡 **Real-world use:** You can reorder elements for mobile vs desktop using media queries + `order`, without moving HTML around. For example, show a sidebar before the main content on desktop, but after it on mobile.

---

### `flex-grow` — How Much Should an Item Grow?

`flex-grow` controls how much extra space an item takes up relative to other items, when the container has leftover space.

**Syntax:**
```css
.item {
  flex-grow: number;   /* default is 0 — do not grow */
}
```

The value is a **ratio** (not a percentage or pixel amount). The browser calculates how much free space exists, then divides it among items proportionally to their `flex-grow` values.

**Example 1 — No growing (default):**

```css
.item { flex-grow: 0; }   /* items stay their natural size */
```

```
[Item1][Item2][Item3]                  (leftover space unused)
```

---

**Example 2 — All items grow equally:**

```css
.item { flex-grow: 1; }   /* each item gets 1 share of free space */
```

```
[──── Item1 ────][──── Item2 ────][──── Item3 ────]
All three items grow equally to fill the container
```

---

**Example 3 — One item grows more:**

```css
.item-a { flex-grow: 1; }
.item-b { flex-grow: 2; }   /* gets TWICE as much free space */
.item-c { flex-grow: 1; }
```

If there is 60px of free space, item-a gets 15px, item-b gets 30px, item-c gets 15px (ratios 1:2:1).

```
[─ Item A ─][──── Item B ────][─ Item C ─]
```

> 🤔 **Think About This:** If every item has `flex-grow: 1`, do they all end up the same size? Not necessarily — they start at their natural size and then share the FREE space. If they started at different sizes they will end at different sizes but each absorbed the same amount of extra space.

---

### `flex-shrink` — How Much Should an Item Shrink?

`flex-shrink` is the opposite of `flex-grow`. It controls how much an item shrinks relative to others when the container is **too small** to fit everything at natural size.

**Syntax:**
```css
.item {
  flex-shrink: number;   /* default is 1 — shrink proportionally */
}
```

**Example:**

```css
.item-a { flex-shrink: 1; }   /* shrinks normally */
.item-b { flex-shrink: 3; }   /* shrinks 3x as much as item-a */
.item-c { flex-shrink: 1; }
```

When the container runs out of space, item-b gives up three times more width than item-a or item-c.

**To prevent shrinking:**

```css
.item { flex-shrink: 0; }   /* item will never shrink below its natural size */
```

> 💡 **Real-world use:** A navigation logo should never shrink while links can. Set `flex-shrink: 0` on the logo item.

---

### `flex-basis` — The Starting Size of an Item

`flex-basis` sets the **initial/base size** of a flex item before any growing or shrinking happens. Think of it as setting the "starting point" size.

**Syntax:**
```css
.item {
  flex-basis: auto | length | percentage;
}
```

| Value | Meaning |
|-------|---------|
| `auto` | Use the item's content size (default) |
| `200px` | Start at exactly 200px |
| `30%` | Start at 30% of the container's size |
| `0` | Start with no assumed size (grow from scratch) |

**Example:**

```css
.item-a { flex-basis: 200px; }   /* starts at 200px, then grows/shrinks from there */
.item-b { flex-basis: 100px; }   /* starts at 100px */
.item-c { flex-basis: auto; }    /* starts at natural content size */
```

---

### `flex` — The Powerful Shorthand

`flex` is a shorthand that combines `flex-grow`, `flex-shrink`, and `flex-basis` in one declaration:

```css
.item {
  flex: flex-grow  flex-shrink  flex-basis;
}
```

**Common patterns:**

```css
flex: 1;            /* grow: 1, shrink: 1, basis: 0  → items share space equally */
flex: 1 1 auto;     /* same as above but starts from natural size */
flex: 0 0 200px;    /* fixed 200px — never grows, never shrinks */
flex: 2 1 150px;    /* starts at 150px, grows at 2x rate, shrinks at 1x rate */
flex: none;         /* fully inflexible: 0 0 auto — stays natural size */
flex: auto;         /* fully flexible: 1 1 auto */
```

> 💡 **Best practice:** Use the shorthand `flex` rather than the three separate properties. It also sets sensible defaults for the properties you don't specify.

**Equal-width columns with `flex: 1`:**

```css
.container {
  display: flex;
}

.column {
  flex: 1;   /* every column shares space equally */
}
```

```
[── Column 1 ──][── Column 2 ──][── Column 3 ──]
All three columns are exactly equal width
```

**Sidebar + main content layout:**

```css
.sidebar {
  flex: 0 0 250px;   /* fixed 250px sidebar, never grows or shrinks */
}

.main-content {
  flex: 1;           /* takes all remaining space */
}
```

```
[── Sidebar 250px ──][──────────── Main Content ────────────]
```

---

### `align-self` — Override Alignment for One Item

`align-self` lets a **single item** override the container's `align-items` setting for itself only.

**Syntax:**
```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

These values work exactly like `align-items` but apply to just one item.

**Example:**

```css
.container {
  display: flex;
  align-items: flex-start;   /* all items start at the top */
  height: 200px;
}

.special-item {
  align-self: center;   /* THIS item centres itself vertically, overriding the container rule */
}
```

```
┌─────────────────────────────────────────┐
│ [Item1]  [Item2]       [Item3]          │
│           ↑ starts at top               │
│         [Special]                       │
│           ↑ centred (overrides rule)    │
│                                         │
└─────────────────────────────────────────┘
```

---

### `gap`, `row-gap`, `column-gap` — Space Between Items

`gap` (previously called `grid-gap`) adds space between flex items without affecting the outer edges of the container. This is cleaner than using `margin` on every item.

**Syntax:**
```css
.container {
  gap: 20px;              /* equal gap in both directions */
  row-gap: 10px;          /* gap between rows only */
  column-gap: 20px;       /* gap between columns only */
  gap: 10px 20px;         /* row-gap then column-gap */
}
```

**Example:**

```css
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}
```

```
[Item1]  [Item2]  [Item3]
  16px     16px
[Item4]  [Item5]
  ↑ 16px between rows too
```

> 💡 **Much better than margins:** With `margin`, the outer items have an unwanted margin on the container edge. `gap` only creates space BETWEEN items, not outside them.

---

### Flex Item Properties Summary

| Property | Controls | Default |
|----------|---------|---------|
| `order` | Visual order of this item | `0` |
| `flex-grow` | How much this item grows | `0` |
| `flex-shrink` | How much this item shrinks | `1` |
| `flex-basis` | Starting size before grow/shrink | `auto` |
| `flex` | Shorthand: grow + shrink + basis | `0 1 auto` |
| `align-self` | This item's cross-axis alignment | `auto` |

---

## Part 6 — Responsive Flexbox Layouts

### What is Responsive Design?

Responsive design means your layout adapts gracefully to different screen sizes — desktop, tablet, and mobile — without building separate websites. Flexbox is perfectly suited for this because flex items can grow, shrink, and wrap automatically.

The two main tools for responsive Flexbox are:

1. **`flex-wrap: wrap`** — items wrap naturally when the container is too narrow
2. **Media queries** — override Flexbox properties at specific screen widths

---

### Technique 1 — Natural Wrapping with `flex-wrap`

The simplest responsive pattern: set items to a minimum width and let them wrap.

```css
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.card {
  flex: 1 1 300px;   /* grow: 1, shrink: 1, basis: 300px minimum */
}
```

**What happens at different screen sizes:**

- **Wide screen (1200px):** Four `300px` cards fit in one row → four columns
- **Medium screen (800px):** Two cards per row (each about 380px after growing)
- **Narrow screen (400px):** One card per row (fills full width)

No media queries needed at all — the wrapping is completely automatic! This is the most elegant responsive pattern.

> 🤔 **Think About This:** What does `flex: 1 1 300px` mean exactly? It says: "Start at 300px. Grow to fill extra space. Shrink if needed. But never let wrapping happen if 300px fits."

---

### Technique 2 — Responsive Navigation Bar

A navigation bar that is horizontal on desktop but stacks vertically on mobile:

```css
/* Base styles (mobile first — stack vertically) */
.nav {
  display: flex;
  flex-direction: column;
  background-color: #333;
}

.nav a {
  color: white;
  padding: 12px 20px;
  text-decoration: none;
}

/* Desktop (wider than 600px) — switch to horizontal row */
@media (min-width: 600px) {
  .nav {
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }
}
```

**Expected result:**

- Mobile: Links stack vertically in a column
- Desktop (600px+): Links sit side by side in a row, spread across the nav bar

---

### Technique 3 — Responsive Two-Column Layout

A sidebar + main content layout that collapses to a single column on mobile:

```css
/* Base: single column for mobile */
.page-layout {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

/* Desktop: two-column sidebar + content */
@media (min-width: 768px) {
  .page-layout {
    flex-direction: row;
  }

  .sidebar {
    flex: 0 0 240px;   /* fixed 240px sidebar */
  }

  .main-content {
    flex: 1;           /* takes remaining space */
  }
}
```

**Expected result:**

- Mobile: Sidebar and main content stack vertically
- Desktop (768px+): Sidebar fixed at 240px on the left, main content fills the right

---

### Technique 4 — Responsive Card Grid

A classic card grid that adjusts columns automatically:

```css
.card-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 24px;
}

.card {
  background: white;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);

  /* 3 cards per row on desktop, wraps on smaller screens */
  flex: 1 1 calc(33% - 24px);
  min-width: 200px;   /* never smaller than 200px */
}
```

**Expected result:**

- Wide screens: 3 cards per row
- Medium screens: 2 cards per row (when 3 don't fit at 200px minimum)
- Narrow screens: 1 card per row

---

### Technique 5 — Mobile-First with Media Queries

The professional approach: start with mobile styles, then add desktop styles in media queries.

```css
/* ===== MOBILE FIRST ===== */
.features {
  display: flex;
  flex-direction: column;   /* stack on mobile */
  gap: 16px;
}

.feature-item {
  flex: 1;                  /* full width on mobile */
  padding: 20px;
  background: #f5f5f5;
  border-radius: 8px;
}

/* ===== TABLET (600px+) ===== */
@media (min-width: 600px) {
  .features {
    flex-direction: row;    /* side by side on tablet */
    flex-wrap: wrap;
  }

  .feature-item {
    flex: 1 1 calc(50% - 8px);   /* 2 per row */
  }
}

/* ===== DESKTOP (900px+) ===== */
@media (min-width: 900px) {
  .feature-item {
    flex: 1 1 calc(33% - 16px);  /* 3 per row */
  }
}
```

**Expected result:**

- Mobile: Items in a column (one per row)
- Tablet: Two items per row
- Desktop: Three items per row

---

### `order` for Responsive Reordering

You can also use `order` to change the visual sequence between mobile and desktop — without touching HTML.

```css
/* Mobile: natural HTML order — content first, sidebar second */
.sidebar    { order: 2; }
.main-content { order: 1; }

/* Desktop: sidebar goes before content visually */
@media (min-width: 768px) {
  .sidebar    { order: 1; }   /* sidebar appears first on desktop */
  .main-content { order: 2; }
}
```

---

## Part 7 — Guided Practice Exercises

### Exercise 1 — Your First Flex Container (Beginner)

**Objective:** Activate Flexbox and control direction.

**Scenario:** You have a row of navigation links that should display horizontally, centred, with even spacing.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    nav {
      background-color: #2c3e50;
      padding: 15px;
      /* TODO: Make this a flex container */
      /* TODO: Centre items horizontally */
      /* TODO: Add 30px gap between items */
    }

    nav a {
      color: white;
      text-decoration: none;
      font-size: 18px;
      padding: 8px 16px;
    }
  </style>
</head>
<body>
  <nav>
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Projects</a>
    <a href="#">Contact</a>
  </nav>
</body>
</html>
```

**Steps:**
1. Add `display: flex` to `nav`
2. Add `justify-content: center` to centre the links
3. Add `gap: 30px` for spacing between links

**Expected Result:** Four white nav links sit in a centred horizontal row on a dark background with 30px gaps between them.

**Self-Check:** Can you change it to spread the links evenly edge-to-edge using `justify-content: space-between`?

---

### Exercise 2 — Perfect Centring (Beginner)

**Objective:** Centre content both vertically and horizontally.

**Scenario:** A hero section that should display its text perfectly centred in the middle of a 400px tall box.

```css
.hero {
  height: 400px;
  background-color: #3498db;
  /* TODO: Use Flexbox to centre .hero-content both ways */
}

.hero-content {
  color: white;
  text-align: center;
}
```

**Solution — fill in the blanks:**

```css
.hero {
  height: 400px;
  background-color: #3498db;
  display: _______;           /* activate Flexbox */
  justify-content: _______;   /* centre on main axis */
  align-items: _______;       /* centre on cross axis */
}
```

**Expected Result:** The `.hero-content` div appears perfectly centred inside the blue hero box.

---

### Exercise 3 — Sidebar Layout (Intermediate)

**Objective:** Build a two-column page layout.

**Task:** Using Flexbox, create a layout with:
- A sidebar that is always 220px wide and never shrinks or grows
- A main content area that fills all remaining space

```html
<div class="page">
  <aside class="sidebar">Sidebar</aside>
  <main class="content">Main Content</main>
</div>
```

```css
.page {
  display: flex;
  min-height: 100vh;
  gap: 0;
}

/* Add your flex item rules below */
.sidebar {
  background: #ecf0f1;
  padding: 20px;
  /* TODO: Fixed 220px, never grows, never shrinks */
}

.content {
  background: #ffffff;
  padding: 20px;
  /* TODO: Takes all remaining space */
}
```

**Hints:**
- Use `flex: 0 0 220px` on the sidebar
- Use `flex: 1` on the content

---

### Exercise 4 — Responsive Card Grid (Intermediate)

**Objective:** Build a card grid that wraps responsively without any media queries.

```css
.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  padding: 20px;
}

.card {
  background: white;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 24px;
  /* TODO: Set flex so cards start at 280px and grow to fill space */
}
```

**Task:** Write the `flex` shorthand for `.card` so that:
- Cards start at `280px` wide
- Cards grow to fill available space
- Cards shrink if needed
- Cards wrap when they can't fit at `280px`

**Expected Behaviour:**
- Wide screen → 3 or more cards per row
- Medium screen → 2 per row
- Narrow screen → 1 per row, full width

**Answer:** `flex: 1 1 280px;`

---

### Exercise 5 — Item Order and Alignment (Advanced)

**Objective:** Use `order` and `align-self`.

**Scenario:** A three-card row where:
- The second card should appear first
- The first card should appear last
- The third card should be aligned to the bottom of the row (while others stretch to full height)

```css
.container {
  display: flex;
  align-items: stretch;
  height: 250px;
  gap: 16px;
}

.card-1 { order: ___; }   /* appears last */
.card-2 { order: ___; }   /* appears first */
.card-3 {
  order: ___;
  align-self: ___;        /* pinned to bottom */
}
```

**Answer:**
```css
.card-1 { order: 3; }
.card-2 { order: 1; }
.card-3 { order: 2; align-self: flex-end; }
```

---

## Part 8 — Mini Project: "FlexFolio" — A Responsive Portfolio Page

Build a complete responsive portfolio page for a fictional web developer called "Jordan Lee". The page uses Flexbox for every layout decision.

### Stage 1 — Navigation Bar

```html
<nav class="navbar">
  <div class="logo">Jordan Lee</div>
  <ul class="nav-links">
    <li><a href="#">Home</a></li>
    <li><a href="#">Work</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

```css
/* Reset */
* { margin: 0; padding: 0; box-sizing: border-box; }
ul { list-style: none; }
a { text-decoration: none; }

.navbar {
  display: flex;
  justify-content: space-between;   /* logo left, links right */
  align-items: center;              /* vertically centred */
  background-color: #1a1a2e;
  padding: 16px 40px;
}

.logo {
  color: #e94560;
  font-size: 22px;
  font-weight: bold;
}

.nav-links {
  display: flex;        /* links in a row */
  gap: 30px;
}

.nav-links a {
  color: #ffffff;
  font-size: 16px;
  transition: color 0.2s;
}

.nav-links a:hover {
  color: #e94560;
}
```

**Milestone 1 Output:** Dark navbar with logo on the left and four nav links on the right, all vertically centred.

---

### Stage 2 — Hero Section

```html
<section class="hero">
  <div class="hero-content">
    <h1>Hi, I'm Jordan Lee</h1>
    <p>Frontend Developer & UI Designer</p>
    <a href="#" class="cta-button">View My Work</a>
  </div>
</section>
```

```css
.hero {
  display: flex;
  justify-content: center;     /* centre horizontally */
  align-items: center;         /* centre vertically */
  min-height: 80vh;
  background: linear-gradient(135deg, #1a1a2e, #16213e);
  text-align: center;
}

.hero-content {
  color: white;
  display: flex;
  flex-direction: column;      /* stack h1, p, button vertically */
  align-items: center;         /* centre each child horizontally */
  gap: 20px;
}

.hero-content h1 { font-size: 52px; }
.hero-content p  { font-size: 22px; color: #aaaaaa; }

.cta-button {
  background-color: #e94560;
  color: white;
  padding: 14px 36px;
  border-radius: 30px;
  font-size: 16px;
  transition: background 0.2s;
}

.cta-button:hover {
  background-color: #c73652;
}
```

**Milestone 2 Output:** Dark gradient hero section with name, tagline, and button all perfectly centred both ways. The hero-content itself is a flex column so the three children stack neatly.

---

### Stage 3 — Projects Card Grid

```html
<section class="projects">
  <h2 class="section-title">My Work</h2>
  <div class="project-grid">
    <div class="project-card">
      <div class="card-tag">React</div>
      <h3>E-Commerce Store</h3>
      <p>A fully responsive online shop with cart functionality.</p>
    </div>
    <div class="project-card">
      <div class="card-tag">CSS</div>
      <h3>Portfolio Generator</h3>
      <p>A drag-and-drop tool for building portfolio pages.</p>
    </div>
    <div class="project-card">
      <div class="card-tag">JavaScript</div>
      <h3>Weather Dashboard</h3>
      <p>Real-time weather data with charts and forecasts.</p>
    </div>
    <div class="project-card">
      <div class="card-tag">Node.js</div>
      <h3>Task Manager API</h3>
      <p>A REST API for managing tasks with authentication.</p>
    </div>
    <div class="project-card">
      <div class="card-tag">Python</div>
      <h3>Data Visualiser</h3>
      <p>Interactive charts from uploaded CSV files.</p>
    </div>
    <div class="project-card">
      <div class="card-tag">Vue.js</div>
      <h3>Recipe Book App</h3>
      <p>Search, save and share recipes with friends.</p>
    </div>
  </div>
</section>
```

```css
.projects {
  padding: 80px 40px;
  background-color: #f8f9fa;
}

.section-title {
  text-align: center;
  font-size: 36px;
  margin-bottom: 48px;
  color: #1a1a2e;
}

.project-grid {
  display: flex;
  flex-wrap: wrap;           /* wrap to new rows */
  gap: 24px;
  justify-content: center;
}

.project-card {
  background: white;
  border-radius: 12px;
  padding: 28px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.08);
  flex: 1 1 280px;           /* start at 280px, grow, wrap naturally */
  max-width: 360px;          /* don't let them get too wide */
  display: flex;
  flex-direction: column;    /* inner content stacks vertically */
  gap: 12px;
}

.card-tag {
  display: inline-block;
  background-color: #e94560;
  color: white;
  font-size: 12px;
  padding: 4px 12px;
  border-radius: 20px;
  align-self: flex-start;    /* tag only as wide as its text */
}

.project-card h3 {
  font-size: 20px;
  color: #1a1a2e;
}

.project-card p {
  color: #666;
  line-height: 1.6;
  flex: 1;    /* pushes anything after it to the bottom */
}
```

**Milestone 3 Output:** Six project cards that automatically flow into rows: 3-per-row on wide screens, 2-per-row on medium, 1-per-row on narrow — all without a single media query.

---

### Stage 4 — Footer + Responsive Navigation

```css
footer {
  background-color: #1a1a2e;
  color: #aaa;
  padding: 30px 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;      /* wraps on small screens */
  gap: 16px;
}

footer .footer-links {
  display: flex;
  gap: 20px;
}

footer a {
  color: #e94560;
}

/* ===== RESPONSIVE ===== */
@media (max-width: 768px) {
  .navbar {
    flex-direction: column;     /* stack logo above links on mobile */
    gap: 16px;
    padding: 20px;
  }

  .nav-links {
    gap: 16px;
  }

  .hero-content h1 {
    font-size: 34px;
  }

  .projects {
    padding: 50px 16px;
  }

  footer {
    flex-direction: column;
    text-align: center;
  }
}
```

**Milestone 4 Output:** On mobile (under 768px), the navbar stacks logo above links, the hero heading shrinks, and the footer stacks its content. The card grid adapts automatically (no extra media query needed).

---

### Final Project Reflection Questions

1. What single Flexbox property automatically makes the card grid responsive without any media query?
2. How does `flex: 1 1 280px` differ from `width: 280px`?
3. Why does the `.card-tag` use `align-self: flex-start` — what would happen without it?
4. The footer uses `flex-wrap: wrap`. When would this wrapping actually kick in?
5. How could you add a "featured" project card that is twice as wide as the others?

---

## Part 9 — Common Beginner Mistakes

### Mistake 1: Setting Flex Properties on the Wrong Element

```css
/* ❌ WRONG — setting container properties on an item */
.item {
  justify-content: center;   /* this does nothing on an item */
}

/* ✅ CORRECT — justify-content goes on the container */
.container {
  display: flex;
  justify-content: center;
}
```

**Why:** `justify-content`, `align-items`, `flex-direction`, and `flex-wrap` are **container properties**. `order`, `flex-grow`, `flex-shrink`, `flex-basis`, `flex`, and `align-self` are **item properties**.

---

### Mistake 2: Forgetting `display: flex`

```css
/* ❌ WRONG — nothing works without activating Flexbox */
.container {
  justify-content: center;   /* has zero effect */
}

/* ✅ CORRECT */
.container {
  display: flex;
  justify-content: center;
}
```

---

### Mistake 3: Confusing `align-items` with `justify-content`

Many beginners mix up which property controls which axis. The mnemonic:

- **`justify-content`** → **J**ust like text **J**ustification → works along the **main axis** (same direction as the text/flow)
- **`align-items`** → **A**cross → works across on the **cross axis** (perpendicular)

```css
/* For a row container (flex-direction: row): */
justify-content: center;   /* centres LEFT-RIGHT */
align-items: center;       /* centres UP-DOWN */

/* For a column container (flex-direction: column): */
justify-content: center;   /* centres UP-DOWN (main axis is now vertical) */
align-items: center;       /* centres LEFT-RIGHT (cross axis is now horizontal) */
```

---

### Mistake 4: Using `align-content` When You Mean `align-items`

```css
/* ❌ WRONG — align-content has no effect on a single-line flex container */
.container {
  display: flex;
  /* NO flex-wrap, so only one line */
  align-content: center;   /* does nothing! */
}

/* ✅ CORRECT for single-line containers */
.container {
  display: flex;
  align-items: center;   /* this is the right property for single line */
}

/* align-content only works WITH flex-wrap: wrap AND actual wrapping */
.container {
  display: flex;
  flex-wrap: wrap;
  align-content: center;   /* ✅ now it works — there are multiple lines */
}
```

---

### Mistake 5: Expecting `flex-grow` to Set a Percentage

```css
/* ❌ COMMON MISUNDERSTANDING */
.item { flex-grow: 50; }   /* this does NOT mean 50% width */

/* flex-grow is a RATIO — items share free space in proportion */
.item-a { flex-grow: 1; }
.item-b { flex-grow: 1; }   /* item-a and item-b each get 50% of FREE space */
```

If you want exactly 50% width, use `flex: 0 0 50%` or `flex-basis: 50%`.

---

### Mistake 6: Adding `flex-wrap` Without Enough Min-Width

```css
/* ❌ PROBLEM — items wrap immediately if they have no natural or set minimum size */
.container {
  display: flex;
  flex-wrap: wrap;
}

.item { }   /* no width/basis set — items might wrap at 1px wide */

/* ✅ CORRECT — give items a minimum size to control when they wrap */
.item {
  flex: 1 1 200px;   /* wraps only when 200px won't fit */
}
```

---

### Mistake 7: Assuming Flex Children Are Still Block Elements

```css
/* ❌ MISUNDERSTANDING */
/* Flex items do NOT stack vertically by default, they go horizontal */
/* And they do NOT respect margin: auto the same way block elements do */
/* BUT margin: auto DOES work for centering one item in Flexbox! */

.container {
  display: flex;
}

.push-right {
  margin-left: auto;   /* ✅ This DOES work — pushes item to the far right! */
}
```

---

## Reflection Questions

Test your understanding:

1. You have a flex container with `flex-direction: column`. Which axis is now the main axis? Which axis does `justify-content` control in this case?

2. You set `align-items: center` on a flex container but the items don't centre vertically. What is the most likely cause?

3. What is the difference between `flex: 1` and `flex: 1 0 auto`? When would this difference matter?

4. You have four items with `flex-grow: 1, 2, 1, 2`. The container has 120px of free space. How many pixels does each item get?

5. Why does `gap: 20px` behave better than `margin: 10px` on flex items for creating spacing between cards?

6. What is the minimum CSS needed to perfectly centre a single `<div>` both horizontally and vertically inside its parent?

7. You want a flex container where items wrap, and you want the wrapped rows to be evenly spaced top-to-bottom inside a fixed-height container. Which property do you use: `align-items` or `align-content`?

---

## Completion Checklist

Before moving on, confirm you can answer "yes" to each:

- [ ] I can activate Flexbox with `display: flex`
- [ ] I understand what a flex container and flex item are
- [ ] I can change direction with `flex-direction`
- [ ] I can allow wrapping with `flex-wrap`
- [ ] I can distribute space along the main axis with `justify-content` (all 6 values)
- [ ] I can align items on the cross axis with `align-items` (all 5 values)
- [ ] I can align multiple wrapped lines with `align-content`
- [ ] I can use `order` to change an item's visual position
- [ ] I can control item sizing with `flex-grow`, `flex-shrink`, and `flex-basis`
- [ ] I can write the `flex` shorthand confidently
- [ ] I can override one item's alignment with `align-self`
- [ ] I can use `gap` to space items cleanly
- [ ] I can build a naturally responsive card grid using `flex-wrap` + `flex-basis`
- [ ] I can combine Flexbox with media queries for a fully responsive layout
- [ ] I completed the mini-project (or am confident I could)
- [ ] I can identify and fix at least 5 common Flexbox mistakes

---

## Lesson Summary

CSS Flexbox is a one-dimensional layout system — it arranges elements in either a row or a column (but not both at once; that is CSS Grid's job). You activate it with `display: flex` on a parent element, which makes all direct children into flex items.

**Container properties** control the overall arrangement:
- `flex-direction` sets the main axis (row, column, and reversed variants)
- `flex-wrap` allows items to wrap to new lines instead of shrinking
- `justify-content` spaces and positions items along the main axis (flex-start, flex-end, center, space-between, space-around, space-evenly)
- `align-items` aligns items along the cross axis for a single line
- `align-content` aligns multiple lines when wrapping occurs
- `gap` adds clean space between items

**Item properties** give individual control:
- `order` changes visual order without touching HTML
- `flex-grow` determines how much an item expands when there is extra space
- `flex-shrink` determines how much an item contracts when space is tight
- `flex-basis` sets the starting size before grow/shrink
- `flex` is the shorthand combining all three (`flex: 1` is the most common)
- `align-self` overrides the container's `align-items` for one specific item

**Responsive Flexbox** is built on two techniques: `flex-wrap: wrap` with `flex-basis` values that control natural breakpoints, and media queries that override `flex-direction` or other container properties at specific widths. The combination of `flex: 1 1 Xpx` with `flex-wrap: wrap` creates fully adaptive card grids that need zero media queries.

Mastering these properties gives you the ability to build virtually any web layout — navigation bars, hero sections, card grids, sidebars, footers, and full responsive page structures — using clean, readable, maintainable CSS.

---

*End of Lesson 69 — CSS Flexbox: Flexible Box Layout, Containers, Items, and Responsive Design*
