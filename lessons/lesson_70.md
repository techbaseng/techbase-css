---
render_with_liquid: false
title: "CSS Grid Layout – Complete Guide from Intro to @supports"
nav_order: 70
---

# Lesson 70 – CSS Grid Layout: Building Two-Dimensional Page Structures

---

## Lesson Introduction

Every modern website you visit — news portals, dashboards, image galleries, e-commerce stores, blog layouts — uses a grid to organise content. Before CSS Grid existed, developers struggled with complicated float hacks, negative margins, and fragile table layouts just to place a sidebar beside a main article. It was messy, hard to maintain, and broke constantly on different screen sizes.

**CSS Grid** is a purpose-built, two-dimensional layout system that lets you design rows AND columns simultaneously — like the ruled squares in a notebook. You decide exactly how many rows and columns exist, how wide and tall each one is, and which cell each piece of content occupies. It is the most powerful layout tool in CSS.

This lesson is comprehensive and covers every major aspect of CSS Grid:
- What Grid is and how it works conceptually.
- Creating a grid container and defining tracks.
- Gaps, alignment, and justification.
- Placing grid items precisely using line numbers, spans, and named areas.
- Aligning individual items within their cells.
- Controlling item order.
- Building a professional 12-column layout.
- Using `@supports` to write safe, progressive-enhancement CSS.

By the end, you will be able to build any real-world webpage layout using CSS Grid from scratch.

---

## Prerequisite Concepts

### What is a CSS Layout?

A layout is the arrangement of elements on a web page — where the header sits, how the sidebar lines up with the main content, how wide the footer is. By default, HTML elements stack vertically (block elements like `div`, `p`, `h1`) or sit side-by-side horizontally (inline elements like `span`, `a`). CSS layouts give you full control over this arrangement.

### What is `display`?

The `display` property changes how an element behaves in the page flow. You already know `display: block` and `display: inline`. Grid introduces:
- `display: grid` — makes an element a **block-level grid container**.
- `display: inline-grid` — makes an element an **inline-level grid container**.

### What is a Parent/Child Relationship?

In HTML, elements nest inside each other:

```html
<div class="container">   <!-- PARENT (becomes the grid) -->
  <div class="item">A</div>  <!-- CHILD (becomes a grid item) -->
  <div class="item">B</div>
  <div class="item">C</div>
</div>
```

Grid rules on the **parent** control the overall layout. Grid rules on the **children** control where each individual item is placed.

### What is a Unit of Measurement in CSS?

You already know `px` (pixels) and `%` (percentage). Grid introduces a new unit: **`fr`** (fraction). We will explain this fully when we first use it.

---

## Part 1 — CSS Grid Introduction

### What is CSS Grid Layout?

CSS Grid Layout is a **two-dimensional layout system** for the web. It handles both columns AND rows simultaneously — unlike Flexbox, which is primarily one-dimensional (either a row OR a column).

**The newspaper analogy:** Think of a newspaper front page. It has a large banner headline spanning the full width, a main story in the left two-thirds, a sidebar in the right third, smaller stories below in three columns, and a full-width advertisement at the bottom. CSS Grid lets you build exactly this kind of complex, multi-zone layout with just a few lines of CSS.

### The Two Roles: Grid Container and Grid Items

CSS Grid works through two types of elements:

**The Grid Container** — the parent element you turn into a grid by writing `display: grid`. It owns all the layout rules: how many columns, how many rows, and how big each one is.

**Grid Items** — the direct children of the grid container. They automatically become grid items and can be placed in specific grid cells.

```html
<div class="grid-container">   <!-- Grid Container -->
  <div>Item 1</div>            <!-- Grid Item -->
  <div>Item 2</div>            <!-- Grid Item -->
  <div>Item 3</div>            <!-- Grid Item -->
  <div>Item 4</div>            <!-- Grid Item -->
</div>
```

```css
.grid-container {
  display: grid;
}
```

**Expected output:** At this stage, the items stack vertically — just one column, same as before. Grid is active but we haven't defined any columns yet.

> **Key rule:** Only **direct children** become grid items. Grandchildren do not automatically participate in the grid.

### Grid Lines, Tracks, and Cells — The Vocabulary

Before writing any code, you must understand the vocabulary. These terms appear everywhere in the Grid specification.

**Grid Line:** The dividing lines that form the grid structure. They run horizontally (row lines) and vertically (column lines). Lines are numbered starting from 1 at the left and top. If you have 3 columns, you have 4 vertical grid lines (line 1, 2, 3, 4).

```
|   col 1   |   col 2   |   col 3   |
1           2           3           4   ← Column line numbers
```

**Grid Track:** The space between two adjacent grid lines — in other words, a single column or a single row.

**Grid Cell:** The intersection of one row track and one column track — a single "square" in the grid.

**Grid Area:** One or more grid cells grouped together as a rectangular region.

**Visual diagram:**

```
     Line 1   Line 2   Line 3   Line 4
        |        |        |        |
Line 1 -+--------+--------+--------+
        | Cell   | Cell   | Cell   |  ← Row Track 1
Line 2 -+--------+--------+--------+
        | Cell   | Cell   | Cell   |  ← Row Track 2
Line 3 -+--------+--------+--------+
```

---

## Part 2 — The Grid Container

### Creating a Grid Container

Apply `display: grid` to any element to make it a grid container.

```css
.container {
  display: grid;
}
```

All direct children of `.container` are now grid items. But without column definitions, all items just stack in a single column.

### Defining Columns: `grid-template-columns`

This is the most important property. It defines how many columns the grid has and how wide each column is.

**Syntax:**
```css
grid-template-columns: value1 value2 value3 ...;
```

Each value defines one column's width. The number of values equals the number of columns.

**Example — 3 equal columns using pixels:**

```css
.container {
  display: grid;
  grid-template-columns: 200px 200px 200px;
}
```

**Expected output:** Three equal columns, each 200px wide. Items fill left to right, wrapping to the next row after 3.

**Example — 3 unequal columns:**

```css
.container {
  display: grid;
  grid-template-columns: 100px 300px 150px;
}
```

**Expected output:** Three columns of different widths: narrow, wide, medium.

### The `fr` Unit — Fractional Units

`fr` is a new CSS unit introduced specifically for Grid. It represents a **fraction of the available free space** in the grid container.

**Analogy:** Imagine splitting a pizza. If you have 3 people and the pizza is divided into `1fr 1fr 1fr`, everyone gets an equal third. If it's divided `1fr 2fr 1fr`, the middle person gets twice as much as the others.

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
```

**Expected output:** Three columns, each taking up exactly one-third of the available width. If the container is 900px, each column is 300px. If the container is 600px, each column is 200px. They always adjust proportionally.

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
}
```

**Expected output:** The middle column is twice as wide as the side columns. In a 900px container: side columns = 225px each, middle = 450px.

> **Why `fr` is powerful:** It automatically fills available space and adapts to container resizing. No need to manually calculate percentages.

### Defining Rows: `grid-template-rows`

Just like columns, you define row heights explicitly.

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 100px 200px;
}
```

**Expected output:** Two rows — first row is 100px tall, second row is 200px tall. A third row (if items overflow) uses auto height.

If you do not define `grid-template-rows`, all rows are automatically sized to fit their content (`auto`).

### The `repeat()` Function

When you want multiple equal tracks, typing the same value multiple times is tedious. The `repeat()` function is shorthand.

**Syntax:**
```css
repeat(number-of-times, track-size)
```

```css
/* These two are identical: */
grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
grid-template-columns: repeat(5, 1fr);
```

```css
/* 12 equal columns: */
grid-template-columns: repeat(12, 1fr);

/* 3 columns, alternating widths: */
grid-template-columns: repeat(3, 100px 200px);
/* = 100px 200px 100px 200px 100px 200px */
```

### The `minmax()` Function

`minmax(min, max)` defines a track size range — the track is at least `min` wide/tall but no more than `max`.

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, minmax(150px, 1fr));
}
```

**Expected output:** Three columns that are at least 150px wide but grow equally to fill available space. This is very useful for responsive layouts.

### `auto-fill` and `auto-fit` — Responsive Column Counts

These special keywords inside `repeat()` let the grid automatically decide how many columns fit.

```css
/* auto-fill: Creates as many columns as fit, keeping empty columns */
grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));

/* auto-fit: Creates as many columns as fit, collapsing empty ones */
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
```

**Expected output:** With `auto-fit, minmax(200px, 1fr)` — on a wide screen, you get 4–5 columns. On a narrow screen (mobile), items drop to 1 or 2 columns. All automatically, with no media queries needed.

> **Thinking prompt:** What is the difference between `auto-fill` and `auto-fit`? With `auto-fill`, even empty column tracks occupy space. With `auto-fit`, empty column tracks collapse to 0 width, letting filled columns expand further.

### Grid Shorthand: `grid-template`

Combine rows and columns in one declaration:

```css
.container {
  grid-template: 100px 200px / 1fr 1fr 1fr;
  /* rows: 100px 200px | columns: 1fr 1fr 1fr */
}
```

---

## Part 3 — Grid Tracks (Column and Row Track Sizing)

### Track Sizing Options

Every column and row track can use any of these sizing values:

| Value | Meaning | Example |
|---|---|---|
| `px` | Fixed pixel size | `200px` |
| `%` | Percentage of container | `33%` |
| `fr` | Fraction of free space | `1fr`, `2fr` |
| `auto` | Size based on content | `auto` |
| `minmax(min, max)` | Range between min and max | `minmax(100px, 1fr)` |
| `repeat(n, size)` | Repeat a track n times | `repeat(3, 1fr)` |
| `min-content` | Minimum content size | `min-content` |
| `max-content` | Maximum content size | `max-content` |

### Mixing Track Sizes

You can mix any of these freely:

```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr auto;
}
```

**Expected output:**
- Column 1: Fixed 200px.
- Column 2: Takes up the remaining free space after columns 1 and 3 are sized.
- Column 3: As wide as its content needs.

```css
.container {
  display: grid;
  grid-template-columns: minmax(100px, 300px) 1fr 1fr;
}
```

**Expected output:** Column 1 grows from 100px minimum to 300px maximum; columns 2 and 3 share the rest equally.

### Named Grid Lines

You can give grid lines custom names to make placement code more readable:

```css
.container {
  display: grid;
  grid-template-columns: [sidebar-start] 250px [sidebar-end content-start] 1fr [content-end];
}
```

The names go in square brackets before each track size. A line can have multiple names (space-separated inside the brackets). You can then use these names when placing items.

---

## Part 4 — Grid Gaps

### What is a Gap?

A gap is the empty space between grid tracks (rows and columns). Think of it like the gutters between tiles on a floor — the tiles themselves (grid cells) do not touch; there is a small gap between them.

### The `gap` Property (and its long forms)

```css
/* Gap between rows AND columns: */
.container {
  gap: 20px;
}

/* Different row and column gaps: */
.container {
  gap: 20px 40px;   /* row-gap  column-gap */
}

/* Individual gap properties: */
.container {
  row-gap: 20px;
  column-gap: 40px;
}
```

**Example with visual output:**

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 15px;
  padding: 15px;
  background: lightgrey;
}

.container div {
  background: steelblue;
  color: white;
  padding: 20px;
  text-align: center;
}
```

**Expected output:** A 3-column grid where every item has a 15px gap on all four sides between its neighbours. The light grey background shows through the gaps.

> **Historical note:** The original property names were `grid-row-gap` and `grid-column-gap`. These were later renamed to `row-gap` and `column-gap` (without the `grid-` prefix) to work with both Grid and Flexbox. Most modern browsers support both, but use the newer versions.

---

## Part 5 — Grid Container Alignment

Grid provides powerful alignment tools for positioning content both horizontally (along the row axis = inline axis) and vertically (along the column axis = block axis).

### Aligning All Items: `justify-items` and `align-items`

These properties control how **all grid items** are positioned inside their individual grid cells.

**`justify-items`** — horizontal positioning of items within their cells (along the inline/row axis):

| Value | Effect |
|---|---|
| `stretch` (default) | Item stretches to fill the full cell width |
| `start` | Item is placed at the left edge of the cell |
| `end` | Item is placed at the right edge of the cell |
| `center` | Item is horizontally centred in the cell |

**`align-items`** — vertical positioning of items within their cells (along the block/column axis):

| Value | Effect |
|---|---|
| `stretch` (default) | Item stretches to fill the full cell height |
| `start` | Item is placed at the top of the cell |
| `end` | Item is placed at the bottom of the cell |
| `center` | Item is vertically centred in the cell |

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 200px);
  grid-template-rows: 150px 150px;
  justify-items: center;
  align-items: center;
}
```

**Expected output:** All items are perfectly centred — both horizontally and vertically — inside their 200px × 150px cells.

**Shorthand — `place-items`:**

```css
place-items: align-items-value justify-items-value;

/* Example: */
place-items: center center;
/* or just: */
place-items: center;  /* same value applied to both */
```

### Aligning the Entire Grid: `justify-content` and `align-content`

These properties control how the **grid itself** is positioned within the container — useful when the grid tracks are smaller than the container.

**`justify-content`** — horizontal positioning of the grid within the container:

| Value | Effect |
|---|---|
| `start` | Grid aligns to the left of the container |
| `end` | Grid aligns to the right |
| `center` | Grid is centred |
| `stretch` | Grid expands to fill container width |
| `space-between` | Equal gaps between columns; no gap at edges |
| `space-around` | Equal space around each column |
| `space-evenly` | Perfectly equal space everywhere |

**`align-content`** — vertical positioning of the grid within the container (same values as `justify-content` but vertically).

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(2, 80px);
  justify-content: space-between;
  align-content: center;
  height: 400px;
  width: 600px;
}
```

**Expected output:** Three 100px columns with equal gaps between them (space-between horizontally), and the two rows vertically centred in the 400px container.

**Shorthand — `place-content`:**

```css
place-content: align-content justify-content;
place-content: center space-between;
```

---

## Part 6 — Grid Items

Now we move from the container to the **individual items** themselves. Grid items can be positioned precisely anywhere in the grid, can span multiple cells, and can be aligned independently.

### How Items Are Placed by Default

By default, grid items fill cells from left to right, top to bottom, in document order (the order they appear in the HTML). This is called **auto-placement**.

```html
<div class="grid">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
  <div>5</div>
  <div>6</div>
</div>
```

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

**Expected output:**

```
| 1 | 2 | 3 |
| 4 | 5 | 6 |
```

### Placing Items with Line Numbers

Every grid line has a number. Use `grid-column` and `grid-row` to tell an item exactly which lines to start and end at.

**Syntax:**
```css
grid-column: start-line / end-line;
grid-row: start-line / end-line;
```

**Example:**

```css
.grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(3, 100px);
}

.item-a {
  grid-column: 1 / 3;  /* Start at line 1, end at line 3 = spans 2 columns */
  grid-row: 1 / 2;     /* First row only */
}
```

**Expected output:**
```
| A  |  A  | 2 | 3 |   ← item A spans columns 1 and 2
| 4  |  5  | 6 | 7 |
| 8  |  9  |10 |11 |
```

### Using `span` Keyword

Instead of specifying the end line, you can say how many tracks the item should span:

```css
/* These are equivalent: */
grid-column: 1 / 3;
grid-column: 1 / span 2;   /* Start at line 1, span 2 columns */

/* Start from wherever auto-placement puts it, span 3 columns: */
grid-column: span 3;
```

### Long-form Properties

`grid-column` and `grid-row` are shorthand. The individual properties are:

```css
grid-column-start: 1;
grid-column-end: 4;

grid-row-start: 2;
grid-row-end: 4;
```

### Negative Line Numbers

You can count grid lines from the right/bottom using negative numbers. `-1` is always the last line.

```css
/* Span from the first column line to the very last: */
grid-column: 1 / -1;

/* Full-width element regardless of how many columns exist: */
grid-column: 1 / -1;
```

### Complete Placement Example

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 80px 80px 80px;
  gap: 10px;
}

.header  { grid-column: 1 / -1; }           /* Full width */
.sidebar { grid-column: 1 / 2; grid-row: 2 / 4; }  /* Left, spans 2 rows */
.main    { grid-column: 2 / -1; grid-row: 2 / 3; } /* Right of sidebar */
.footer  { grid-column: 2 / -1; grid-row: 3 / 4; } /* Bottom right */
```

```html
<div class="grid">
  <div class="header">Header</div>
  <div class="sidebar">Sidebar</div>
  <div class="main">Main</div>
  <div class="footer">Footer</div>
</div>
```

**Expected layout:**
```
| Header  | Header  | Header  |
| Sidebar | Main    | Main    |
| Sidebar | Footer  | Footer  |
```

> **Thinking prompt:** What happens if you use `grid-column: 2 / 5` on a 3-column grid? The item would extend beyond the defined grid, and the browser would implicitly create a 4th column track to accommodate it.

---

## Part 7 — Named Grid Areas

Placing items with line numbers works, but reading `grid-column: 2 / 4` isn't very descriptive. CSS Grid offers an elegant alternative: **named grid areas**. You literally draw your layout as an ASCII-art map.

### `grid-template-areas` on the Container

```css
.container {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: 80px 1fr 60px;
  grid-template-areas:
    "header  header"
    "sidebar main"
    "footer  footer";
}
```

**How to read this:** You write the area name in each cell of the grid. Use the same name in adjacent cells to make an area span multiple cells. Use a dot `.` for an empty cell.

Rules for named areas:
- A named area must form a **rectangle** — you cannot have an L-shape or T-shape area.
- All rows must have the same number of cells.
- Each name must be a single word (no spaces).

### Placing Items into Named Areas

On each grid item, use `grid-area: name` to assign it to a named region:

```css
.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.footer  { grid-area: footer; }
```

**Full working example:**

```css
.page {
  display: grid;
  grid-template-columns: 200px 1fr;
  grid-template-rows: 70px auto 50px;
  grid-template-areas:
    "header  header"
    "sidebar content"
    "footer  footer";
  min-height: 100vh;
  gap: 10px;
}

.header  { grid-area: header;  background: #2c3e50; color: white; }
.sidebar { grid-area: sidebar; background: #ecf0f1; }
.content { grid-area: content; background: white; }
.footer  { grid-area: footer;  background: #2c3e50; color: white; }
```

```html
<div class="page">
  <header class="header">My Website</header>
  <nav class="sidebar">Navigation</nav>
  <main class="content">Main Content</main>
  <footer class="footer">Copyright 2025</footer>
</div>
```

**Expected layout:**
```
|   My Website (header, full width)   |
| Navigation  |  Main Content         |
| (sidebar)   |                       |
|   Copyright 2025 (footer, full width)|
```

### Empty Cells with Dots

```css
grid-template-areas:
  "header header header"
  "sidebar . main"    /* Middle cell is empty */
  "footer footer footer";
```

The dot `.` creates an empty cell with no grid item assigned to it.

### Named Lines Generated by `grid-template-areas`

When you define named areas, CSS Grid automatically generates named lines too. For an area named `header`, the browser creates `header-start` and `header-end` lines on both the column and row axes. This means you can use `grid-column: header-start / header-end` for even more explicit control.

---

## Part 8 — Aligning Individual Grid Items

While `justify-items` and `align-items` on the container affect ALL items, you can override alignment for any single item using properties on the item itself.

### `justify-self` — Horizontal Alignment of One Item

```css
.item {
  justify-self: start | end | center | stretch;
}
```

```css
.item-1 { justify-self: start; }   /* Item sticks to left of cell */
.item-2 { justify-self: end; }     /* Item sticks to right of cell */
.item-3 { justify-self: center; }  /* Item centred horizontally */
.item-4 { justify-self: stretch; } /* Item fills full cell width (default) */
```

**Expected output:** Four items in cells of the same width, but each positioned differently within its cell.

### `align-self` — Vertical Alignment of One Item

```css
.item {
  align-self: start | end | center | stretch;
}
```

```css
.item-1 { align-self: start; }   /* Item at top of cell */
.item-2 { align-self: end; }     /* Item at bottom of cell */
.item-3 { align-self: center; }  /* Item centred vertically */
.item-4 { align-self: stretch; } /* Item fills full cell height (default) */
```

### Shorthand: `place-self`

```css
place-self: align-self justify-self;
place-self: center end;   /* vertical: center, horizontal: end */
place-self: center;       /* both axes: center */
```

---

## Part 9 — Grid Item Order

By default, grid items are placed in their HTML source order. But CSS Grid lets you change the visual order without changing the HTML — using the `order` property.

### The `order` Property

```css
.item {
  order: number;
}
```

- The default `order` is `0` for all items.
- Items with a lower `order` value appear first (further left/up).
- Items with a higher `order` value appear last (further right/down).
- Negative values are allowed — they appear before items with `order: 0`.

**Example:**

```html
<div class="grid">
  <div class="a">A</div>
  <div class="b">B</div>
  <div class="c">C</div>
  <div class="d">D</div>
</div>
```

```css
.grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
}

.a { order: 3; }
.b { order: 1; }
.c { order: 4; }
.d { order: 2; }
```

**Expected output:** The items appear in order B, D, A, C — sorted by their `order` values (1, 2, 3, 4), not their HTML position.

**Real-world use case:** On mobile, you might want the sidebar to appear after the main content even though it is placed before it in the HTML (for accessibility reasons). Use `order` to change the visual position on small screens without touching the HTML.

> **Important warning:** Changing visual order with `order` does NOT change the tab order or screen reader order — those follow the HTML source order. Always think about keyboard and accessibility users when using `order`.

---

## Part 10 — The CSS Grid 12-Column Layout System

### Why 12 Columns?

The number 12 is mathematically elegant for layout design. It divides evenly into halves (6), thirds (4), quarters (3), sixths (2), and twelfths (1). This flexibility is why nearly every professional design framework — Bootstrap, Foundation, Material Design — uses a 12-column grid as its foundation.

With a 12-column grid, you can express any layout fraction as a number of columns:
- Full width = 12 columns
- Half width = 6 columns
- One third = 4 columns
- One quarter = 3 columns
- Two thirds = 8 columns
- Three quarters = 9 columns

### Setting Up the 12-Column Grid

```css
.grid-12 {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px;
}
```

That is all you need for the container. Every item can then specify how many of the 12 columns it occupies using `grid-column: span N`.

### Using the 12-Column System

```html
<div class="grid-12">
  <div class="col-12">Full Width Banner</div>
  <div class="col-6">Left Half</div>
  <div class="col-6">Right Half</div>
  <div class="col-4">One Third</div>
  <div class="col-4">One Third</div>
  <div class="col-4">One Third</div>
  <div class="col-3">Quarter</div>
  <div class="col-3">Quarter</div>
  <div class="col-3">Quarter</div>
  <div class="col-3">Quarter</div>
</div>
```

```css
.grid-12 {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 16px;
}

.col-12 { grid-column: span 12; }
.col-9  { grid-column: span 9; }
.col-8  { grid-column: span 8; }
.col-6  { grid-column: span 6; }
.col-4  { grid-column: span 4; }
.col-3  { grid-column: span 3; }
.col-2  { grid-column: span 2; }
.col-1  { grid-column: span 1; }
```

**Expected output:**
```
|          Full Width Banner (12)          |
|   Left Half (6)    |   Right Half (6)    |
| Third(4) | Third(4)| Third(4)           |
|Q(3)|Q(3) |Q(3)     |Q(3)               |
```

### Sidebar + Main Content Layout with 12 Columns

```css
.layout {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 24px;
}

.sidebar { grid-column: span 3; }  /* 3/12 = 25% */
.main    { grid-column: span 9; }  /* 9/12 = 75% */
```

### Offset Columns

You can leave empty columns before an item to create indentation or centering effects:

```css
/* Start a 6-column item in column 4 (leaving 3 empty columns first) */
.centred-content {
  grid-column: 4 / span 6;
}
```

**Expected output:** A centred block that occupies the middle 6 columns (4 through 9), with 3 empty columns on each side.

### Responsive 12-Column Grid with Media Queries

```css
.grid-12 {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 16px;
}

/* Mobile: everything full width */
@media (max-width: 768px) {
  .col-6,
  .col-4,
  .col-3 {
    grid-column: span 12;
  }
}

/* Tablet: half widths */
@media (min-width: 769px) and (max-width: 1024px) {
  .col-4 { grid-column: span 6; }
  .col-3 { grid-column: span 6; }
}
```

---

## Part 11 — The CSS `@supports` Rule

### What is `@supports`?

`@supports` is a CSS at-rule that lets you write styles that **only apply if the browser supports a specific CSS feature**. It is the CSS equivalent of "if-then" logic.

This is called **feature detection** — checking whether a browser can handle a feature before using it.

**Why it matters:** Not all browsers support every CSS feature. A cutting-edge CSS property might work perfectly in Chrome but not in an older browser used by 10% of your visitors. `@supports` lets you provide a modern experience for capable browsers while ensuring older browsers still get something that works.

**Analogy:** Imagine building a house. You have a smart thermostat that works great in new homes with the right wiring. In older homes without that wiring, the smart thermostat simply does not work. `@supports` lets you say: "If this house has the right wiring, install the smart thermostat. Otherwise, install a basic thermostat." Both homes get a thermostat — just different ones.

### Basic Syntax

```css
@supports (property: value) {
  /* Styles that only apply if the browser supports property: value */
}
```

**Example — Apply Grid only if supported:**

```css
/* Default layout for all browsers (safe fallback) */
.container {
  display: flex;
  flex-wrap: wrap;
}

/* Override with Grid for browsers that support it */
@supports (display: grid) {
  .container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
  }
}
```

**Expected behaviour:**
- Modern browsers (Chrome, Firefox, Edge, Safari): Uses the Grid layout with 3 columns.
- Very old browsers that don't support Grid: Falls back to the Flexbox layout.

### Checking CSS Grid Support

```css
@supports (display: grid) {
  .layout {
    display: grid;
    grid-template-columns: 200px 1fr;
    gap: 20px;
  }
}
```

**Expected output:** Grid layout applies only in browsers that understand `display: grid`. In others, this entire block is ignored.

### The `not` Operator

The `not` operator applies styles when a feature is **NOT** supported:

```css
@supports not (display: grid) {
  /* Styles for browsers WITHOUT Grid support */
  .container {
    float: left;
    width: 33.33%;
  }
}
```

**Expected behaviour:** The float-based layout only applies in browsers where Grid is not supported. Modern browsers with Grid support completely ignore this block.

### The `and` Operator

Apply styles only if **multiple features** are all supported:

```css
@supports (display: grid) and (gap: 20px) {
  .container {
    display: grid;
    gap: 20px;
  }
}
```

**Expected behaviour:** Both `display: grid` AND `gap: 20px` must be supported for these styles to apply.

### The `or` Operator

Apply styles if **at least one** of multiple features is supported:

```css
@supports (display: flex) or (display: grid) {
  .container {
    /* Modern layout styles */
  }
}
```

### Combining Operators

You can combine operators, but use parentheses to make the logic clear:

```css
@supports ((display: grid) and (gap: 1rem)) or (display: flex) {
  .layout {
    /* applies if (grid + gap) OR flex is supported */
  }
}
```

### `@supports selector()` — Testing Selector Support

You can also check if a browser supports a specific selector:

```css
@supports selector(:has(+ div)) {
  /* Only if the :has() selector is supported */
  .parent:has(+ .sibling) {
    background: yellow;
  }
}
```

### Practical `@supports` Pattern: Progressive Enhancement

The most common real-world pattern is the "enhancement layer" approach:

```css
/* ===== LAYER 1: Base styles - work everywhere ===== */
.card-grid {
  /* Simple stacked layout - works in any browser */
}

.card-grid .card {
  margin-bottom: 20px;
  width: 100%;
}

/* ===== LAYER 2: Enhanced Grid - modern browsers only ===== */
@supports (display: grid) {
  .card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 24px;
  }

  .card-grid .card {
    margin-bottom: 0;  /* Remove margin - gap handles spacing now */
    width: auto;
  }
}
```

This guarantees every visitor sees a usable layout, while modern browser users get the polished Grid version.

### `@supports` vs Media Queries

| `@supports` | `@media` |
|---|---|
| Checks browser feature support | Checks device/screen characteristics |
| "Does this browser support Grid?" | "Is the screen wider than 768px?" |
| Feature detection | Responsive design |
| Applied once based on browser capability | Applied dynamically as window resizes |

---

## Simple Standalone Examples — Full Collection

### Example A — A Basic 3-Column Grid

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
```

```html
<div class="grid">
  <div style="background:coral; padding:20px">1</div>
  <div style="background:coral; padding:20px">2</div>
  <div style="background:coral; padding:20px">3</div>
  <div style="background:coral; padding:20px">4</div>
  <div style="background:coral; padding:20px">5</div>
  <div style="background:coral; padding:20px">6</div>
</div>
```

**Expected output:**
```
| 1 | 2 | 3 |
| 4 | 5 | 6 |
```
Six boxes in two equal rows of three, with 10px gaps between them.

---

### Example B — Full-Width Header with Side-by-Side Content

```css
.layout {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-template-rows: 80px auto 60px;
  grid-template-areas:
    "header  header"
    "sidebar content"
    "footer  footer";
  gap: 10px;
  min-height: 100vh;
}

.header  { grid-area: header;  background: #34495e; color: white; padding: 20px; }
.sidebar { grid-area: sidebar; background: #ecf0f1; padding: 20px; }
.content { grid-area: content; background: white;   padding: 20px; }
.footer  { grid-area: footer;  background: #34495e; color: white; padding: 15px; }
```

**Expected output:** A classic two-column webpage layout with full-width header and footer.

---

### Example C — Responsive Card Grid (no media queries!)

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  padding: 20px;
}
```

**Expected output:** On a wide desktop: 4–5 cards per row. On a tablet: 2–3 cards. On mobile: 1 card per row. Fully automatic, no media queries needed.

---

### Example D — Item Spanning Multiple Columns and Rows

```css
.mosaic {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(3, 120px);
  gap: 8px;
}

.big   { grid-column: 1 / 3; grid-row: 1 / 3; }   /* 2×2 block */
.tall  { grid-column: 3; grid-row: 1 / 3; }        /* 1×2 tall */
.wide  { grid-column: 4; grid-row: 1 / 3; }
.strip { grid-column: 1 / -1; }                    /* Full width */
```

**Expected output:** A photo mosaic layout — one large 2×2 featured image, tall images, and a full-width strip at the bottom.

---

### Example E — `@supports` with Grid Fallback

```css
/* All browsers: stack vertically */
.items > * {
  display: block;
  margin-bottom: 16px;
}

/* Modern browsers: use grid */
@supports (display: grid) {
  .items {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
  }
  .items > * {
    margin-bottom: 0;
  }
}
```

**Expected output:**
- Modern browsers: 3-column grid layout.
- Old browsers: stacked single-column layout.

---

## Guided Practice Exercises

### Exercise 1 — Build a Simple Photo Gallery Grid

**Objective:** Practice `grid-template-columns`, `repeat()`, `gap`, and basic item sizing.

**Scenario:** You are building a photo gallery page for a photographer's portfolio. The gallery should show 3 images per row.

**Steps:**
1. Create an HTML file with a `<div class="gallery">` containing 9 `<div>` children labelled "Photo 1" through "Photo 9".
2. Make `.gallery` a grid with 3 equal columns using `repeat()`.
3. Set a `gap` of `12px`.
4. Give each child a background colour, a height of `150px`, centred text, and white text.
5. Add `border-radius: 8px` for style.

**Hint:** Use `display: flex; align-items: center; justify-content: center;` on the children to centre the text inside each photo.

**Expected output:** A 3×3 gallery grid with 12px gaps between photos.

**Solution:**
```css
.gallery {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  padding: 12px;
}

.gallery div {
  background-color: steelblue;
  height: 150px;
  color: white;
  font-weight: bold;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
}
```

**Self-check questions:**
- How would you change it to 4 photos per row? (`repeat(4, 1fr)`)
- How would you make it responsive with no media queries? (`repeat(auto-fit, minmax(200px, 1fr))`)

---

### Exercise 2 — Classic Page Layout with Named Areas

**Objective:** Practice `grid-template-areas` and `grid-area`.

**Scenario:** Build a standard magazine-style layout with header, left nav, main article, and footer.

**Steps:**
1. Create the HTML with `<header>`, `<nav>`, `<main>`, `<footer>` inside a `.page` wrapper.
2. Define a grid with `grid-template-areas` showing header full-width, nav on left (25%), main on right (75%), footer full-width.
3. Set `grid-template-rows: 70px auto 60px`.
4. Assign each element to its area with `grid-area`.
5. Style each area with a distinct background colour.

**Expected output:** A complete webpage layout using only CSS Grid named areas.

**Solution:**
```css
.page {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-template-rows: 70px auto 60px;
  grid-template-areas:
    "header  header"
    "nav     main"
    "footer  footer";
  min-height: 100vh;
  gap: 8px;
}

header { grid-area: header; background: #2ecc71; color: white; padding: 20px; }
nav    { grid-area: nav;    background: #3498db; color: white; padding: 20px; }
main   { grid-area: main;   background: #ecf0f1; padding: 20px; }
footer { grid-area: footer; background: #2ecc71; color: white; padding: 15px; }
```

**Self-check questions:**
- How would you add a right sidebar? (Add a 3rd column and a 3rd column name in the template areas.)
- How would you make the nav appear after the main on mobile? (Use `order` property in a media query.)

---

### Exercise 3 — Precise Item Placement with Line Numbers

**Objective:** Practice `grid-column`, `grid-row`, and `span`.

**Scenario:** Build a dashboard with one wide analytics panel, two medium stat boxes, and one tall activity feed.

**Steps:**
1. Create a 4-column, 3-row grid.
2. Make the `.analytics` panel span all 4 columns in row 1.
3. Make `.stats-1` span 2 columns, row 2.
4. Make `.stats-2` span 2 columns (the right half), row 2.
5. Make `.activity` span all 4 columns in row 3.

**Expected output:**
```
| Analytics (spans all 4 columns)         |
| Stats-1 (cols 1-2) | Stats-2 (cols 3-4) |
| Activity (spans all 4 columns)          |
```

**Solution:**
```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: 80px 200px 150px;
  gap: 12px;
}

.analytics { grid-column: 1 / -1; background: #9b59b6; color: white; }
.stats-1   { grid-column: 1 / 3; background: #3498db; color: white; }
.stats-2   { grid-column: 3 / 5; background: #e74c3c; color: white; }
.activity  { grid-column: 1 / -1; background: #27ae60; color: white; }

.dashboard > div {
  padding: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  border-radius: 6px;
}
```

**Self-check questions:**
- How do you use `span` instead of end-line numbers for `.stats-1`? (`grid-column: 1 / span 2`)
- What does `1 / -1` mean? (Start at line 1, end at the last line — span all columns.)

---

### Exercise 4 — Build a 12-Column Responsive Layout

**Objective:** Practice the 12-column grid system.

**Steps:**
1. Create a `.grid-12` container with `repeat(12, 1fr)` and `gap: 16px`.
2. Add these items: a full-width hero, two half-width feature boxes, three equal third-width cards, a 9-column content area + 3-column sidebar.
3. Use `grid-column: span N` classes.

**Solution:**
```css
.grid-12 {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 16px;
  padding: 16px;
}

.span-12 { grid-column: span 12; }
.span-9  { grid-column: span 9; }
.span-6  { grid-column: span 6; }
.span-4  { grid-column: span 4; }
.span-3  { grid-column: span 3; }

/* Style each box for visibility */
.grid-12 > div {
  background: #3498db;
  color: white;
  padding: 20px;
  min-height: 80px;
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
}
```

```html
<div class="grid-12">
  <div class="span-12">Hero (12)</div>
  <div class="span-6">Feature A (6)</div>
  <div class="span-6">Feature B (6)</div>
  <div class="span-4">Card 1 (4)</div>
  <div class="span-4">Card 2 (4)</div>
  <div class="span-4">Card 3 (4)</div>
  <div class="span-9">Main Content (9)</div>
  <div class="span-3">Sidebar (3)</div>
</div>
```

---

### Exercise 5 — `@supports` Progressive Enhancement

**Objective:** Write a layout that works in all browsers and adds Grid as an enhancement.

**Steps:**
1. Start with a simple stacked (block) layout for `.product-grid`.
2. Wrap Grid styles in `@supports (display: grid)`.
3. Inside the `@supports` block, apply `auto-fit, minmax(200px, 1fr)`.
4. Add a second `@supports not (display: grid)` block for old-browser float fallbacks.

**Solution:**
```css
/* Base: works everywhere */
.product-grid {
  padding: 16px;
}

.product-grid .product {
  display: block;
  width: 100%;
  margin-bottom: 20px;
  background: #f0f0f0;
  padding: 20px;
  box-sizing: border-box;
}

/* Enhancement: Grid for modern browsers */
@supports (display: grid) {
  .product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
  }

  .product-grid .product {
    margin-bottom: 0;
    width: auto;
  }
}

/* Fallback: Float for very old browsers */
@supports not (display: grid) {
  .product-grid::after {
    content: '';
    display: table;
    clear: both;
  }

  .product-grid .product {
    float: left;
    width: calc(33.33% - 16px);
    margin-right: 16px;
  }
}
```

---

## Mini Project — Complete News Website Layout

**Goal:** Build a fully functional news website layout using every concept from this lesson: Grid container, tracks, gaps, named areas, item placement with line numbers, item alignment, order, 12-column system, and `@supports`.

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Daily Grid News</title>
  <link rel="stylesheet" href="news.css">
</head>
<body>
  <div class="site-wrapper">

    <header class="site-header">
      <h1>📰 Daily Grid News</h1>
      <nav>Home | World | Tech | Sports</nav>
    </header>

    <main class="news-grid">
      <article class="featured">
        <h2>Breaking: CSS Grid Changes Web Development Forever</h2>
        <p>Developers worldwide celebrate the power of two-dimensional layouts...</p>
      </article>

      <aside class="sidebar">
        <h3>Trending</h3>
        <ul>
          <li>Story 1</li>
          <li>Story 2</li>
          <li>Story 3</li>
        </ul>
      </aside>

      <section class="secondary-stories">
        <article class="card">Tech Update</article>
        <article class="card">Science News</article>
        <article class="card">Business Report</article>
        <article class="card">Culture Today</article>
      </section>

      <section class="ad-banner">Advertisement</section>
    </main>

    <footer class="site-footer">
      <p>&copy; 2025 Daily Grid News</p>
    </footer>

  </div>
</body>
</html>
```

**Milestone output:** Plain unstyled HTML — all content visible but stacked vertically.

---

### Stage 2 — Grid Container and Named Areas

```css
/* ===== RESET & BASE ===== */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: Georgia, serif;
  background: #f5f5f0;
  color: #222;
}

/* ===== SITE WRAPPER ===== */
.site-wrapper {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 16px;
}
```

**Milestone output:** Content is now contained within a max-width wrapper.

---

### Stage 3 — Header

```css
.site-header {
  display: grid;
  grid-template-columns: 1fr auto;
  align-items: center;
  padding: 16px 0;
  border-bottom: 3px solid #c0392b;
  margin-bottom: 20px;
}

.site-header h1 {
  font-size: 2rem;
  color: #c0392b;
}

.site-header nav {
  font-size: 0.9rem;
  color: #555;
}
```

**Milestone output:** Header with newspaper title on the left and navigation links on the right, separated by a red rule.

---

### Stage 4 — Main News Grid with Named Areas

```css
.news-grid {
  display: grid;
  grid-template-columns: 1fr 280px;
  grid-template-rows: auto auto auto;
  grid-template-areas:
    "featured   sidebar"
    "secondary  sidebar"
    "ad-banner  ad-banner";
  gap: 20px;
  margin-bottom: 20px;
}

.featured  { grid-area: featured; }
.sidebar   { grid-area: sidebar; }
.secondary-stories { grid-area: secondary; }
.ad-banner { grid-area: ad-banner; }
```

**Milestone output:** The featured story sits beside the sidebar. Secondary stories are below the featured area. The ad banner spans the full width at the bottom.

---

### Stage 5 — Styling Each Zone

```css
/* FEATURED STORY */
.featured {
  background: white;
  padding: 24px;
  border-radius: 4px;
  border-left: 5px solid #c0392b;
}

.featured h2 {
  font-size: 1.6rem;
  margin-bottom: 12px;
  line-height: 1.3;
}

/* SIDEBAR */
.sidebar {
  background: #2c3e50;
  color: white;
  padding: 20px;
  border-radius: 4px;
}

.sidebar h3 {
  margin-bottom: 12px;
  color: #e74c3c;
  text-transform: uppercase;
  font-size: 0.85rem;
  letter-spacing: 2px;
}

.sidebar li {
  padding: 8px 0;
  border-bottom: 1px solid #3d5166;
  list-style: none;
}

/* SECONDARY STORIES — 12 COLUMN SUB-GRID */
.secondary-stories {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 12px;
}

.card {
  grid-column: span 6;   /* 2 cards per row (6/12 = 50%) */
  background: white;
  padding: 20px;
  border-radius: 4px;
  border-top: 3px solid #3498db;
  min-height: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
}

/* AD BANNER */
.ad-banner {
  background: repeating-linear-gradient(
    45deg,
    #ffeaa7,
    #ffeaa7 10px,
    #fdcb6e 10px,
    #fdcb6e 20px
  );
  padding: 20px;
  text-align: center;
  border-radius: 4px;
  font-style: italic;
  color: #636e72;
}

/* FOOTER */
.site-footer {
  border-top: 2px solid #ddd;
  padding: 16px 0;
  text-align: center;
  color: #888;
  font-size: 0.9rem;
}
```

**Milestone output:** A complete, professionally styled news website layout.

---

### Stage 6 — Responsive with Media Query + `@supports`

```css
/* @supports — Grid progressive enhancement */
@supports not (display: grid) {
  .news-grid {
    display: block;
  }
  .featured, .sidebar, .secondary-stories, .ad-banner {
    display: block;
    width: 100%;
    margin-bottom: 20px;
  }
}

/* Responsive: Stack on mobile */
@media (max-width: 768px) {
  .news-grid {
    grid-template-columns: 1fr;
    grid-template-areas:
      "featured"
      "secondary"
      "sidebar"
      "ad-banner";
  }

  /* Reorder sidebar to appear after stories on mobile */
  .sidebar { order: 1; }

  .card { grid-column: span 12; } /* Full width cards on mobile */

  .site-header {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 8px;
  }
}
```

**Final milestone output:** On desktop, a full newspaper-style two-column grid layout. On mobile, everything stacks into a single column with the sidebar moved below the stories.

---

### Reflection Questions

1. Why are named grid areas easier to maintain than line-number placement for a full page layout?
2. How does `repeat(auto-fit, minmax(250px, 1fr))` eliminate the need for media queries in a card grid?
3. What is the difference between `justify-items` (on the container) and `justify-self` (on an item)?
4. Why do professional grid systems use 12 columns instead of 10 or 8?
5. In what situation would you use `@supports not (display: grid)` instead of `@supports (display: grid)`?
6. What is the accessibility risk of using the `order` property?

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting `display: grid` on the Container

**Wrong:**
```css
.container {
  grid-template-columns: repeat(3, 1fr);  /* Grid rules but no display: grid! */
}
```

**Problem:** Without `display: grid`, no grid is created and all grid properties are ignored.

**Correct:**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

---

### Mistake 2 — Applying Grid Properties to Items Instead of Container

**Wrong:**
```css
.item {
  grid-template-columns: repeat(3, 1fr);  /* This belongs on the PARENT */
}
```

**Problem:** `grid-template-columns` belongs on the **grid container**, not on the items. Items use `grid-column`, `grid-row`, `grid-area`.

**Container properties:** `grid-template-columns`, `grid-template-rows`, `grid-template-areas`, `gap`, `justify-items`, `align-items`, `justify-content`, `align-content`.

**Item properties:** `grid-column`, `grid-row`, `grid-area`, `justify-self`, `align-self`, `order`.

---

### Mistake 3 — Using `grid-gap` Instead of `gap`

**Outdated (but still works in most browsers):**
```css
.container {
  grid-gap: 20px;       /* Old name */
  grid-row-gap: 10px;   /* Old name */
  grid-column-gap: 20px; /* Old name */
}
```

**Modern (preferred):**
```css
.container {
  gap: 20px;
  row-gap: 10px;
  column-gap: 20px;
}
```

---

### Mistake 4 — Non-Rectangular Named Areas

**Wrong:**
```css
grid-template-areas:
  "header header"
  "header content"  /* 'header' appears in row 2, column 1 - forms an L-shape! */
  "footer footer";
```

**Problem:** A named grid area must form a complete rectangle. An L-shape or T-shape is invalid and the entire `grid-template-areas` declaration is ignored.

**Correct:**
```css
grid-template-areas:
  "header  header"
  "sidebar content"
  "footer  footer";
```

---

### Mistake 5 — Overlapping Items Without Intending To

**Wrong (accidental overlap):**
```css
.item-1 { grid-column: 1 / 3; }
.item-2 { grid-column: 2 / 4; }
/* Both items include column 2 — they overlap! */
```

**Problem:** Item 1 spans columns 1–2. Item 2 spans columns 2–3. They share column 2, so they visually overlap (item 2 sits on top of item 1 in column 2).

**Correct (no overlap):**
```css
.item-1 { grid-column: 1 / 3; }   /* columns 1 and 2 */
.item-2 { grid-column: 3 / 5; }   /* columns 3 and 4 */
```

> **Note:** Intentional overlap is a valid technique — you can layer items on top of each other using z-index for creative designs. The key word is *intentional*.

---

### Mistake 6 — Wrong Number of Areas in `grid-template-areas` Rows

**Wrong:**
```css
grid-template-areas:
  "header header header"
  "sidebar content"        /* Only 2 cells — but 3 columns defined! */
  "footer footer footer";
```

**Problem:** Every row in `grid-template-areas` must have the same number of area cells as there are columns. A row with 2 area names in a 3-column grid is invalid.

**Correct:**
```css
grid-template-areas:
  "header  header  header"
  "sidebar content content"  /* 3 names, one per column */
  "footer  footer  footer";
```

---

### Mistake 7 — Confusing `justify-content` with `justify-items`

- `justify-items`: positions **items inside their cells** (affects cell contents).
- `justify-content`: positions **the entire grid** within the container (affects the grid as a whole).

**Analogy:** `justify-items` is like telling people where to stand within their own room. `justify-content` is like deciding which rooms in the house get space.

---

### Mistake 8 — Incorrect `@supports` Syntax (Missing Parentheses)

**Wrong:**
```css
@supports display: grid {    /* Missing parentheses! */
  .container { display: grid; }
}
```

**Correct:**
```css
@supports (display: grid) {   /* Property: value wrapped in parentheses */
  .container { display: grid; }
}
```

---

## Complete Property Reference Tables

### Grid Container Properties

| Property | Values | Purpose |
|---|---|---|
| `display` | `grid`, `inline-grid` | Activates grid layout |
| `grid-template-columns` | lengths, fr, %, repeat(), minmax() | Defines column tracks |
| `grid-template-rows` | lengths, fr, %, repeat(), minmax() | Defines row tracks |
| `grid-template-areas` | quoted area name strings | Defines named grid areas |
| `grid-template` | rows / columns shorthand | Shorthand for rows, columns, areas |
| `grid-auto-columns` | any track size | Size of implicitly created columns |
| `grid-auto-rows` | any track size | Size of implicitly created rows |
| `grid-auto-flow` | `row`, `column`, `dense` | Auto-placement algorithm |
| `gap` | length | Sets both row and column gap |
| `row-gap` | length | Gap between rows |
| `column-gap` | length | Gap between columns |
| `justify-items` | `start`, `end`, `center`, `stretch` | Horizontal alignment of ALL items in cells |
| `align-items` | `start`, `end`, `center`, `stretch` | Vertical alignment of ALL items in cells |
| `place-items` | align justify shorthand | Shorthand for align-items + justify-items |
| `justify-content` | `start`, `end`, `center`, `stretch`, `space-between`, `space-around`, `space-evenly` | Horizontal positioning of the grid |
| `align-content` | same as justify-content | Vertical positioning of the grid |
| `place-content` | align justify shorthand | Shorthand for align-content + justify-content |

### Grid Item Properties

| Property | Values | Purpose |
|---|---|---|
| `grid-column` | `start / end` or `start / span n` | Column placement shorthand |
| `grid-column-start` | line number, name, span | Where the item starts (column) |
| `grid-column-end` | line number, name, span | Where the item ends (column) |
| `grid-row` | `start / end` or `start / span n` | Row placement shorthand |
| `grid-row-start` | line number, name, span | Where the item starts (row) |
| `grid-row-end` | line number, name, span | Where the item ends (row) |
| `grid-area` | area name or `row-start / col-start / row-end / col-end` | Assign to named area or full placement shorthand |
| `justify-self` | `start`, `end`, `center`, `stretch` | Horizontal alignment of THIS item |
| `align-self` | `start`, `end`, `center`, `stretch` | Vertical alignment of THIS item |
| `place-self` | align justify shorthand | Shorthand for align-self + justify-self |
| `order` | integer | Visual order of the item |

---

## Reflection Questions

1. What is the fundamental difference between CSS Grid and CSS Flexbox? When would you choose one over the other?
2. Explain what `1fr` means. If a grid has `grid-template-columns: 1fr 2fr 1fr` and the container is 800px wide, how wide is each column?
3. What is the visual result of `grid-template-columns: repeat(auto-fit, minmax(200px, 1fr))` on screens of different widths?
4. Why must named areas in `grid-template-areas` always form rectangles?
5. What is the difference between `grid-column: 1 / 4` and `grid-column: 1 / span 3`? Are they always equivalent?
6. When would you use `align-self` on an item instead of `align-items` on the container?
7. What does `@supports (display: grid)` do, and why is it good practice to use it?
8. What is the accessibility concern with using the CSS `order` property?
9. Why does a 12-column grid give more layout flexibility than an 8-column or 10-column grid?
10. What does `grid-column: 1 / -1` do, and why is it useful?

---

## Completion Checklist

Before moving on, make sure you can do all of the following:

- [ ] Explain what a Grid Container and Grid Item are.
- [ ] Activate CSS Grid with `display: grid`.
- [ ] Define columns with `grid-template-columns` using `px`, `fr`, `%`, `auto`.
- [ ] Define rows with `grid-template-rows`.
- [ ] Use `repeat()` to create multiple equal tracks.
- [ ] Use `minmax()` to create tracks with flexible size ranges.
- [ ] Use `auto-fit` and `auto-fill` with `minmax()` for responsive grids.
- [ ] Set row and column gaps with `gap`, `row-gap`, `column-gap`.
- [ ] Use `justify-items`, `align-items`, `justify-content`, `align-content` on a container.
- [ ] Use `place-items` and `place-content` shorthand.
- [ ] Place items precisely with `grid-column` and `grid-row` line numbers.
- [ ] Use the `span` keyword for item sizing.
- [ ] Use negative line numbers (e.g. `1 / -1`).
- [ ] Define and assign named grid areas with `grid-template-areas` and `grid-area`.
- [ ] Use `justify-self` and `align-self` on individual items.
- [ ] Control visual order with the `order` property.
- [ ] Build a 12-column grid layout using `repeat(12, 1fr)` and `span` classes.
- [ ] Write a `@supports (display: grid)` block with a CSS Grid enhancement.
- [ ] Write a `@supports not (display: grid)` fallback.
- [ ] Use `@supports` with `and`, `or`, and `not` operators.
- [ ] Build a complete page layout using named areas.
- [ ] Identify and fix all 8 common Grid mistakes.

---

## Lesson Summary

CSS Grid is a **two-dimensional layout system** that handles rows and columns simultaneously. It is the most powerful layout tool in CSS.

**Setting up a grid:** Apply `display: grid` to a container. Define columns with `grid-template-columns` and rows with `grid-template-rows`. Use `fr` units (fractions of available space), `repeat()` for multiple equal tracks, and `minmax()` for flexible size ranges.

**Tracks** are the row and column spaces between grid lines. **Gaps** (`gap`, `row-gap`, `column-gap`) create gutters between tracks.

**Container alignment:** `justify-items` and `align-items` control how all items sit within their cells. `justify-content` and `align-content` control where the grid itself sits within the container.

**Grid items** can be placed precisely using `grid-column` and `grid-row` with line numbers (`1 / 3`), spans (`1 / span 2`), or negative numbers (`1 / -1`). Named areas (`grid-template-areas` + `grid-area`) provide a descriptive, visual way to design layouts.

**Item-level alignment** uses `justify-self` and `align-self` to override the container defaults for individual items. The `order` property changes visual order independently of HTML source order.

**The 12-column layout** is a professional grid system using `repeat(12, 1fr)` where items span a number of columns (`span 6` = half width, `span 4` = one third, etc.) — the foundation of most design frameworks.

**`@supports`** is the feature-detection at-rule that applies CSS only when a browser supports a given feature. Use `@supports (display: grid)` to enhance a base layout for modern browsers, and `@supports not (display: grid)` to write fallbacks for older browsers. Combine conditions with `and`, `or`, and `not`.

Together, these tools give you complete, professional-grade control over every layout in modern web development.

---

*Sources: W3Schools CSS Grid Introduction, Grid Container, Grid Tracks, Grid Gaps, Grid Alignment, Grid Items, Named Grid Items, Grid Item Alignment, Grid Item Order, 12-Column Grid, and CSS @supports Rule tutorials and code challenges.*
