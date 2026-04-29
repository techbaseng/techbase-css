---
render_with_liquid: false
title: "CSS Multiple Columns — Building Newspaper-Style Layouts from Scratch"
nav_order: 63
---

# Lesson 63 — CSS Multiple Columns: Building Newspaper-Style Layouts from Scratch

---

## Lesson Introduction

Have you ever opened a newspaper, a printed magazine, or a Wikipedia article and noticed the text flows in neat side-by-side vertical strips — like this?

```
┌──────────────────────────────────────────────────────┐
│           ARTICLE HEADING ACROSS THE TOP             │
├─────────────────┬──────────────┬─────────────────────┤
│ Lorem ipsum     │ sed diam     │ Ut wisi enim ad     │
│ dolor sit amet, │ nonummy nibh │ minim veniam, quis  │
│ consectetuer    │ euismod      │ nostrud exerci...   │
│ adipiscing...   │ tincidunt... │                     │
└─────────────────┴──────────────┴─────────────────────┘
```

That is called a **multi-column layout**. Before CSS had a built-in way to do this, web developers had to use complicated tricks with floats and tables to fake it. Today, CSS gives us a dedicated set of **column properties** that make this effortless.

In this lesson you will learn:

- What multi-column layout is and why it exists
- How to split content into columns with just one CSS property
- How to control the gap (space) between columns
- How to draw decorative lines (called "rules") between columns
- How to control rule style, width, and colour individually and with a shorthand
- How to make a heading or element span across ALL columns
- How to set column width instead of column count
- How to use the `columns` shorthand property
- Real-world use cases for multi-column layout
- How to build a full magazine-style article page as a mini-project

---

## Prerequisite Concepts

Before we start, let's make sure you understand the building blocks this lesson depends on.

### What Is a Block-Level Container?

A **block-level element** is an element that takes up the full width of its parent and starts on a new line. The most common one is `<div>`. When we apply column properties, we apply them to a container like `<div>` and the content inside automatically flows into columns.

```html
<div class="article">
  <p>This is a paragraph of text.</p>
  <p>This is another paragraph.</p>
</div>
```

The `<div class="article">` is our **multi-column container**. Everything inside it — paragraphs, headings, lists — flows through the columns.

---

### What Is the CSS `border` Property?

The `column-rule` property (which we will learn in detail) works almost identically to `border`. If you know how to write `border: 2px solid red`, you already know the pattern for `column-rule`.

```css
/* border shorthand: width style color */
border: 2px solid red;

/* column-rule shorthand: width style color (same pattern!) */
column-rule: 2px solid red;
```

---

### What Is `px` vs `em`?

Throughout this lesson we use two length units:

- `px` (pixels) — a fixed, absolute size. `40px` is always 40 pixels, regardless of font size.
- `em` — a relative size. `1em` equals the current font size of the element. If the font is `16px`, then `1em = 16px`.

The default gap between columns is `1em` (roughly equal to the font size).

---

## Part 1 — What Is CSS Multi-Column Layout?

### The Problem It Solves

A normal webpage shows text in one long column that fills the entire width of the page. This works fine for short content, but for long articles on a wide screen, reading becomes tiring — your eyes have to travel the full width of the screen and then jump back to the left to find the next line.

Newspapers discovered centuries ago that **narrower columns are easier to read** because your eyes don't have to travel as far. The CSS Multi-column Layout Module brings this same principle to the web.

### Real-World Uses

- **News websites** — articles split into 2 or 3 columns
- **Wikipedia** — reference lists displayed in multiple columns
- **Online magazines** — editorial feature articles
- **Product documentation** — side-by-side comparison of options
- **Dictionary / glossary pages** — two columns of terms

### The Key Properties at a Glance

| Property | What It Does |
|---|---|
| `column-count` | Sets how many columns |
| `column-gap` | Sets the space between columns |
| `column-rule-style` | Sets the style of the line between columns |
| `column-rule-width` | Sets the thickness of the line |
| `column-rule-color` | Sets the colour of the line |
| `column-rule` | Shorthand for all three rule properties |
| `column-span` | Makes an element stretch across all columns |
| `column-width` | Sets a suggested optimal width per column |
| `columns` | Shorthand for `column-width` and `column-count` |

---

## Part 2 — `column-count`: Splitting Content into Columns

### What It Is

`column-count` is the most fundamental multi-column property. It tells the browser: "Take the content inside this element and split it into **N** equal columns."

The browser then automatically:
1. Calculates how wide each column should be (based on the container width)
2. Distributes the text evenly across all columns
3. Balances the columns so they are roughly the same height

### Syntax

```css
div {
  column-count: 3;
}
```

- `3` — the number of columns. You can use any whole number.
- `auto` — the default value, which means "no columns" (just the normal single-column layout).

### Simple Isolated Example — 2 Columns

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .two-col {
      column-count: 2;
    }
  </style>
</head>
<body>
  <div class="two-col">
    <p>
      Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam
      nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat
      volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation
      ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
      Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse
      molestie consequat, vel illum dolore eu feugiat nulla facilisis at
      vero eros et accumsan et iusto odio dignissim qui blandit praesent.
    </p>
  </div>
</body>
</html>
```

**Expected output:**
```
┌──────────────────────────────────────────────┐
│  Lorem ipsum dolor sit  │  aliquip ex ea     │
│  amet, consectetuer     │  commodo consequat.│
│  adipiscing elit, sed   │  Duis autem vel    │
│  diam nonummy nibh...   │  eum iriure...     │
└──────────────────────────────────────────────┘
```

The paragraph flows through two equal-width columns side by side. The browser automatically decided where each column ends and the next begins.

> **Thinking Prompt:** What do you think happens if you have very short text — only one sentence — and you set `column-count: 4`? Try it! Does the browser still create 4 columns?

---

### Example — 3 Columns (Classic Newspaper Style)

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .three-col {
      column-count: 3;
    }
  </style>
</head>
<body>
  <div class="three-col">
    <p>
      Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam
      nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat
      volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation
      ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
      Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse
      molestie consequat, vel illum dolore eu feugiat nulla facilisis.
    </p>
  </div>
</body>
</html>
```

**Expected output:**
```
┌────────────────────────────────────────────────────────┐
│  Lorem ipsum   │  Ut wisi enim  │  Duis autem vel     │
│  dolor sit     │  ad minim      │  eum iriure dolor   │
│  amet...       │  veniam...     │  in hendrerit...    │
└────────────────────────────────────────────────────────┘
```

Three equal columns. The content flows: left column fills first, then middle, then right.

> **Analogy:** Think of `column-count` like pouring water into a tray with dividers. The water fills the first section, spills over to the second, then the third. The text works the same way — it fills the first column, then overflows into the second, and so on.

---

## Part 3 — `column-gap`: Space Between Columns

### What It Is

`column-gap` controls the **white space between adjacent columns**. Without enough gap, columns look cramped and text from neighbouring columns blurs together visually.

### Default Value

The default gap is `normal`, which the browser interprets as `1em` (roughly the size of one character). This is a sensible default, but you can increase or decrease it.

### Syntax

```css
div {
  column-count: 3;
  column-gap: 40px;   /* 40 pixels of space between each column */
}
```

### Micro Demo — Comparing No Gap vs Large Gap

**No gap (tight):**
```css
.tight {
  column-count: 3;
  column-gap: 0;
}
```
Result: Columns are jammed together — hard to read.

**Comfortable gap:**
```css
.comfortable {
  column-count: 3;
  column-gap: 40px;
}
```
Result: Clear visual separation between columns.

### Full Example with column-count and column-gap:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .article {
      column-count: 3;
      column-gap: 40px;
    }
  </style>
</head>
<body>
  <div class="article">
    <p>
      Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam
      nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat
      volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation
      ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
      Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse
      molestie consequat, vel illum dolore eu feugiat nulla facilisis at
      vero eros et accumsan et iusto odio dignissim qui blandit praesent.
    </p>
  </div>
</body>
</html>
```

**Expected output:**
```
┌───────────────────────────────────────────────────────────┐
│  Lorem ipsum   ←40px→  Ut wisi enim   ←40px→  Duis autem │
│  dolor sit...          ad minim...             vel eum... │
└───────────────────────────────────────────────────────────┘
```

> **Thinking Prompt:** What would happen if you set `column-gap` to `0`? What about `200px`? Is there a point where the gap becomes too large and makes reading harder?

---

## Part 4 — Column Rules: Drawing Lines Between Columns

### What Is a Column Rule?

A **column rule** is a vertical line drawn between adjacent columns — similar to the dividing lines you see between columns in a printed newspaper. It is a purely decorative element that helps readers visually separate one column from another.

> **Important:** The column rule lives **inside** the column gap and takes up no extra space. If the rule is wider than the gap, the rule extends underneath the adjacent columns rather than pushing them apart.

The column rule is controlled by three individual properties or one shorthand:

```
column-rule-style    ← what kind of line? (solid, dashed, dotted...)
column-rule-width    ← how thick? (in pixels)
column-rule-color    ← what colour?
column-rule          ← shorthand for all three at once
```

---

### Property 1 — `column-rule-style`

This sets the **style (appearance) of the line**. It accepts the exact same values as the CSS `border-style` property.

**Possible values:**

| Value | What it looks like |
|---|---|
| `none` | No line (default) |
| `solid` | ──────── (a plain continuous line) |
| `dashed` | - - - - - (broken dashes) |
| `dotted` | · · · · · (small dots) |
| `double` | ════════ (two parallel lines) |
| `groove` | A 3D grooved effect (appears sunken) |
| `ridge` | A 3D ridged effect (appears raised) |
| `inset` | Top-left sides darker (appears pressed in) |
| `outset` | Bottom-right sides darker (appears popped out) |
| `hidden` | Invisible (same as none for columns) |

**Simple Example:**

```css
div {
  column-count: 3;
  column-rule-style: solid;
}
```

**Expected output:** A thin solid black line appears between each column. The browser sets the default width and colour automatically (usually 1px and the text colour).

---

### Property 2 — `column-rule-width`

This sets the **thickness of the line**. You can use pixel values or the keyword values `thin`, `medium`, and `thick`.

```css
div {
  column-count: 3;
  column-rule-style: dotted;
  column-rule-width: 5px;
}
```

**Expected output:** A 5-pixel-wide dotted line between each column.

| Value | Approximate thickness |
|---|---|
| `thin` | 1px |
| `medium` | 3px |
| `thick` | 5px |
| `5px` | Exactly 5 pixels |

> **Note:** `column-rule-width` on its own does **nothing** if `column-rule-style` is not set or is `none`. The style must be set first for the line to appear.

---

### Property 3 — `column-rule-color`

This sets the **colour of the line**. It accepts any valid CSS colour — colour names, hex codes, RGB, HSL.

```css
div {
  column-count: 3;
  column-rule-style: solid;
  column-rule-width: 3px;
  column-rule-color: lightblue;
}
```

**Expected output:** A 3-pixel-wide solid light-blue line between each column.

> **Default:** If you set `column-rule-style` and `column-rule-width` but leave out `column-rule-color`, the line colour automatically matches the text colour of the container.

---

### The Three Properties Together — Full Example:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .ruled {
      column-count: 3;
      column-gap: 40px;
      column-rule-style: solid;
      column-rule-width: 3px;
      column-rule-color: lightblue;
    }
  </style>
</head>
<body>
  <div class="ruled">
    <p>
      Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam
      nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat
      volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation
      ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
      Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse
      molestie consequat, vel illum dolore eu feugiat nulla facilisis.
    </p>
  </div>
</body>
</html>
```

**Expected output:**
```
┌────────────────────────────────────────────────────────┐
│  Lorem ipsum   ┊   Ut wisi enim  ┊   Duis autem vel   │
│  dolor sit...  ┊   ad minim...   ┊   eum iriure...    │
└────────────────────────────────────────────────────────┘
       ↑ light-blue solid 3px rule between each column
```

> **Thinking Prompt:** What if `column-rule-width` is set to `60px` but `column-gap` is only `40px`? Try it — the rule will extend under the text of adjacent columns because the rule does not push the columns apart.

---

## Part 5 — `column-rule`: The Shorthand

### Why Use a Shorthand?

Writing three separate properties every time you want a column rule is verbose. The `column-rule` shorthand lets you set all three values in a single line — just like `border`.

### Syntax

```css
div {
  column-rule: width style color;
}
```

The order is the same as `border`: **width → style → color**.

### Examples

```css
/* 1px wide, solid style, light-blue colour */
div {
  column-rule: 1px solid lightblue;
}

/* 4px wide, dashed style, red colour */
div {
  column-rule: 4px dashed red;
}

/* 2px wide, dotted style, dark-grey colour */
div {
  column-rule: 2px dotted #333;
}
```

### Full Shorthand Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .shorthand-rule {
      column-count: 3;
      column-gap: 30px;
      column-rule: 1px solid lightblue;
    }
  </style>
</head>
<body>
  <div class="shorthand-rule">
    <p>
      Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam
      nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat
      volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation
      ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
    </p>
  </div>
</body>
</html>
```

**Expected output:** Three columns with a thin solid light-blue vertical line between them.

> **Memory Trick:** Both `border` and `column-rule` follow the same pattern: **width style color**. Learn it once, use it for both!

---

### Comparing Individual Properties vs Shorthand

```css
/* LONG WAY — three separate declarations */
div {
  column-rule-style: dashed;
  column-rule-width: 3px;
  column-rule-color: tomato;
}

/* SHORT WAY — one declaration, same result */
div {
  column-rule: 3px dashed tomato;
}
```

Both produce identical results. The shorthand is preferred for clean, concise CSS.

---

## Part 6 — `column-span`: Making Elements Stretch Across All Columns

### What It Is

By default, every element inside a multi-column container — including headings — flows through the columns just like text. So an `<h2>` would only appear inside one narrow column, not across the full width.

`column-span` lets you pull an element **out of the column flow** so it stretches across all columns — perfect for article titles, section headings, or images that should be full-width.

### Values

```css
h2 {
  column-span: all;   /* span across ALL columns */
}

h2 {
  column-span: none;  /* default — stay inside one column */
}
```

- `all` — The element expands to fill the full width of the multi-column container.
- `none` — The default. The element stays confined to its current column.

### Why This Matters

Imagine a newspaper where the main headline at the top spans the full page width, but the article text below is in three columns. That's exactly what `column-span: all` lets you recreate on a webpage.

### Example — Heading Spans All Columns

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .article {
      column-count: 3;
      column-gap: 30px;
      column-rule: 1px solid #ccc;
    }
    /* The heading spans the full width of all columns */
    .article h2 {
      column-span: all;
      background-color: #f0f0f0;
      padding: 8px;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="article">
    <h2>Breaking News: CSS Layout Gets Even Better</h2>
    <p>
      Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam
      nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat
      volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation
      ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
      Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse
      molestie consequat, vel illum dolore eu feugiat nulla facilisis.
    </p>
  </div>
</body>
</html>
```

**Expected output:**
```
┌──────────────────────────────────────────────────────────┐
│       Breaking News: CSS Layout Gets Even Better         │
│              ← heading spans ALL 3 columns →             │
├──────────────┬───────────────┬──────────────────────────┤
│  Lorem ipsum │  Ut wisi enim │  Duis autem vel eum      │
│  dolor sit   │  ad minim     │  iriure dolor in         │
│  amet...     │  veniam...    │  hendrerit...            │
└──────────────┴───────────────┴──────────────────────────┘
```

The heading appears above all three columns, full-width. The article text flows beneath it in three columns.

> **Thinking Prompt:** What happens to the column rules when a spanning element is present? The rules are drawn only between columns in the same row — they stop before the spanning element and start again after it.

---

### Example — `column-span: none` (Default Behaviour)

```html
<style>
  .article {
    column-count: 3;
    column-rule: 1px solid gray;
  }
  .article h2 {
    column-span: none; /* stays confined to one column — DEFAULT */
  }
</style>
```

**Expected output:** The `<h2>` appears only inside the first column, taking up only its narrow column width. The text continues in the same column after it.

---

## Part 7 — `column-width`: Setting a Suggested Column Width

### What It Is

Instead of telling the browser "I want exactly 3 columns", `column-width` says: "I want columns that are approximately this wide — create as many as will fit in the container."

This is especially powerful for **responsive design** — on a wide desktop screen you get many columns, on a narrow mobile screen you might get just one.

### Syntax

```css
div {
  column-width: 150px;
}
```

- `150px` — The browser will try to make columns approximately 150px wide.
- `auto` — Default. The browser decides the width based on `column-count`.

### How the Browser Decides the Column Count

If the container is `600px` wide and `column-width: 150px`, the browser calculates: `600 ÷ 150 = 4 columns`. It creates as many 150px-ish columns as will fit.

If the container is `900px` wide, it creates 6 columns. If it's `300px` wide, it creates 2 columns. The layout adapts automatically!

### Example — Responsive Column Width

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .flexible {
      column-width: 150px;
      column-gap: 20px;
    }
  </style>
</head>
<body>
  <div class="flexible">
    <p>
      Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam
      nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat
      volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation
      ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
    </p>
  </div>
</body>
</html>
```

**Expected output (on a wide screen):**
```
│ ~150px col │ ~150px col │ ~150px col │ ~150px col │
```

**Expected output (on a narrow screen):**
```
│ ~150px col │ ~150px col │
```

The number of columns automatically adjusts to the screen width.

> **Analogy:** `column-width` is like telling workers: "Set up tables that are about 150cm wide each." On a huge ballroom floor, you'd fit many tables. In a small room, only two or three. The size of each table stays roughly constant — only the count changes.

---

## Part 8 — `columns`: The Shorthand for Width and Count

### What It Is

The `columns` shorthand combines `column-width` and `column-count` into a single declaration.

### Syntax

```css
div {
  columns: column-width column-count;
}
```

Or just one value if you only need to set one of them:

```css
/* Just set the count */
div {
  columns: 3;
}

/* Just set the width */
div {
  columns: 200px;
}

/* Set both: suggested width of 200px, maximum of 3 columns */
div {
  columns: 200px 3;
}
```

### How the Two Values Work Together

When you write `columns: 200px 3`:

- `column-width: 200px` — Each column should be approximately 200px wide.
- `column-count: 3` — Never create more than 3 columns.

This means: "Create columns of about 200px each, but cap it at 3 maximum."

- On a wide screen (800px): the browser would create 4 columns at 200px, BUT because of the count limit, it stops at 3. Each column becomes `800px ÷ 3 ≈ 267px`.
- On a narrow screen (300px): the browser creates only 1 column at ~300px (since 200px fits only 1.5 times).

The layout **automatically breaks down to a single column at narrow widths** — no media queries needed!

### Full `columns` Shorthand Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .news-article {
      columns: 200px 3;        /* ~200px wide, max 3 columns */
      column-gap: 40px;
      column-rule: 1px solid lightblue;
    }
  </style>
</head>
<body>
  <div class="news-article">
    <p>
      Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam
      nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat
      volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation
      ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
      Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse
      molestie consequat, vel illum dolore eu feugiat nulla facilisis.
    </p>
  </div>
</body>
</html>
```

**Expected output (wide screen):** 3 columns of ~200px each, with a light-blue rule between them.

**Expected output (mobile phone):** 1 or 2 columns, no media queries needed.

---

## Part 9 — All Column Properties Reference Table

Here is a complete summary of every multi-column property covered in this lesson:

| Property | Values | What It Does |
|---|---|---|
| `column-count` | number, `auto` | Sets the exact number of columns |
| `column-gap` | length (px, em), `normal` | Sets the space between columns |
| `column-rule-style` | `none`, `solid`, `dashed`, `dotted`, `double`, `groove`, `ridge`, `inset`, `outset`, `hidden` | Sets the line style between columns |
| `column-rule-width` | length (px), `thin`, `medium`, `thick` | Sets the line thickness |
| `column-rule-color` | any CSS colour | Sets the line colour |
| `column-rule` | `width style color` | Shorthand for all three rule properties |
| `column-span` | `none`, `all` | Makes an element span across all columns |
| `column-width` | length (px, em), `auto` | Sets the suggested optimal column width |
| `columns` | `column-width column-count` | Shorthand for width and count together |

---

## Guided Practice Exercises

### Exercise 1 — Simple 3-Column Article

**Objective:** Create a 3-column text layout using `column-count`.

**Scenario:** You are building a news website. A long article needs to be split into 3 columns for readability.

**Steps:**
1. Create `exercise1.html`.
2. Add a `<div class="news">` containing at least 3 paragraphs of text.
3. Apply `column-count: 3` to `.news`.
4. Add `column-gap: 30px` for comfortable spacing.

**Expected output:**
```
┌──────────────────────────────────────────────────┐
│  Paragraph   │  text cont-  │  text cont-        │
│  text...     │  inues...    │  inues here...     │
└──────────────────────────────────────────────────┘
```

**Self-check questions:**
- Does the text flow across all 3 columns?
- Is there visible spacing between columns?
- Do all 3 columns appear to be roughly equal in height?

---

### Exercise 2 — Column Rules Practice

**Objective:** Add decorative rules between columns using individual rule properties.

**Scenario:** A magazine wants a visible dividing line between its columns.

**Steps:**
1. Start with your Exercise 1 layout.
2. Add `column-rule-style: dashed`.
3. Add `column-rule-width: 2px`.
4. Add `column-rule-color: tomato`.
5. Then refactor those 3 lines into a single `column-rule` shorthand.

**Hint:** The shorthand order is: `width style color`.

**Expected output:** Dashed red lines separating the three columns.

**What-if challenge:** Change the rule style to `double` with a width of `6px` and a colour of `steelblue`. What does a double rule look like?

---

### Exercise 3 — Spanning Heading

**Objective:** Add a full-width heading that spans all three columns.

**Scenario:** The news article needs a headline above the columns.

**Steps:**
1. Start with your Exercise 2 layout.
2. Add an `<h2>` inside the `<div>` as the **very first element** (before the paragraphs).
3. Apply `column-span: all` to the `h2`.
4. Style it with a background colour and centred text to make it stand out.

**Expected output:**
```
┌──────────────────────────────────────────────────────┐
│        Full-Width Headline Across All Columns        │
├────────────────┬─────────────────┬───────────────────┤
│  Article text  │  continues in   │  three columns    │
│  here...       │  the middle...  │  here...          │
└────────────────┴─────────────────┴───────────────────┘
```

**Self-check questions:**
- Does the heading stretch the full width of the container?
- Does the text continue in 3 columns beneath the heading?
- Do the column rules stop at the heading and restart after it?

---

### Exercise 4 — Flexible Columns with `column-width`

**Objective:** Use `column-width` for a responsive multi-column layout.

**Scenario:** A blog needs to look good on both desktop and mobile without writing media queries.

**Steps:**
1. Create a new `<div class="blog-post">` with 2–3 paragraphs of text.
2. Apply `column-width: 200px`.
3. Add `column-gap: 25px` and `column-rule: 1px solid #ddd`.
4. Resize your browser window and watch the column count change automatically.

**Self-check questions:**
- On a wide window, how many columns do you see?
- On a very narrow window, how many columns appear?
- Did you write any media queries? (You shouldn't need to!)

---

### Exercise 5 — Full Columns Shorthand

**Objective:** Rewrite a multi-column layout using the `columns` shorthand.

**Starting code (long way):**
```css
.article {
  column-width: 150px;
  column-count: 4;
  column-gap: 20px;
  column-rule-style: solid;
  column-rule-width: 1px;
  column-rule-color: gray;
}
```

**Your task:** Refactor this into the shortest possible CSS using the `columns` shorthand and `column-rule` shorthand. The output must look identical.

**Expected result:**
```css
.article {
  columns: 150px 4;
  column-gap: 20px;
  column-rule: 1px solid gray;
}
```

---

## Mini Project — Magazine-Style Article Page

### Project Goal

Build a fully styled magazine-style article page that demonstrates every multi-column property from this lesson.

The page will have:
- A full-width page header
- A multi-column article section with a spanning headline
- A visible column rule
- A mid-article pull-quote that spans all columns
- Comfortable gaps and styling

---

### Stage 1: Setup — HTML Structure

Create `magazine_article.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>The Daily Reader</title>
  <style>
    /* CSS goes here */
  </style>
</head>
<body>

  <!-- Page Header -->
  <header>
    <h1>The Daily Reader</h1>
    <p>Technology · Science · Culture</p>
  </header>

  <!-- Multi-column Article -->
  <div class="article">

    <!-- Spanning headline -->
    <h2>The Future of Web Layout: CSS Multi-Column Explained</h2>

    <p>
      Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam
      nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat
      volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation
      ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
    </p>

    <p>
      Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse
      molestie consequat, vel illum dolore eu feugiat nulla facilisis at
      vero eros et accumsan et iusto odio dignissim qui blandit praesent
      luptatum zzril delenit augue duis dolore te feugait nulla facilisi.
    </p>

    <!-- Pull-quote spanning all columns -->
    <blockquote class="pull-quote">
      "CSS Multi-Column Layout brings the elegance of print directly to the web."
    </blockquote>

    <p>
      Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam
      nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat
      volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation
      ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
    </p>

    <p>
      Nam liber tempor cum soluta nobis eligend optio congue nihil quod doming
      id quod mazim placerat facer possim assum. Typi non habent claritatem
      insitam, est usus legentis in iis qui facit eorum claritatem.
    </p>

  </div>

  <!-- Footer -->
  <footer>
    <p>© 2026 The Daily Reader. All rights reserved.</p>
  </footer>

</body>
</html>
```

**Milestone 1:** Plain, unstyled HTML — all content in one column. This is expected.

---

### Stage 2: Core Multi-Column Styles

Inside `<style>`, add:

```css
/* ---- RESET & BASE ---- */
* {
  box-sizing: border-box;
}

body {
  font-family: Georgia, serif;
  font-size: 16px;
  line-height: 1.7;
  color: #222;
  background-color: #fdfdfd;
  max-width: 960px;
  margin: 0 auto;
  padding: 20px;
}

/* ---- PAGE HEADER ---- */
header {
  text-align: center;
  border-bottom: 3px double #333;
  padding-bottom: 12px;
  margin-bottom: 24px;
}

header h1 {
  font-size: 2.5em;
  letter-spacing: 3px;
  text-transform: uppercase;
  margin-bottom: 4px;
}

header p {
  color: #666;
  font-style: italic;
  font-size: 0.9em;
}

/* ---- MULTI-COLUMN ARTICLE ---- */
.article {
  columns: 200px 3;       /* ~200px wide, max 3 columns */
  column-gap: 40px;       /* comfortable spacing */
  column-rule: 1px solid #ccc;  /* subtle grey divider */
}

/* ---- SPANNING HEADLINE ---- */
.article h2 {
  column-span: all;        /* stretch across all 3 columns */
  font-size: 1.6em;
  text-align: center;
  border-bottom: 2px solid #333;
  padding-bottom: 10px;
  margin-bottom: 20px;
}

/* ---- SPANNING PULL-QUOTE ---- */
.article .pull-quote {
  column-span: all;        /* full-width pull quote */
  background-color: #f5f5f5;
  border-left: 4px solid #333;
  padding: 16px 24px;
  margin: 20px 0;
  font-size: 1.15em;
  font-style: italic;
  color: #444;
}

/* ---- FOOTER ---- */
footer {
  text-align: center;
  border-top: 1px solid #ccc;
  margin-top: 30px;
  padding-top: 12px;
  font-size: 0.85em;
  color: #999;
}
```

**Milestone 2 output:**
```
┌──────────────────────────────────────────────────────────────────┐
│                       THE DAILY READER                           │
│                  Technology · Science · Culture                  │
├──────────────────────────────────────────────────────────────────┤
│          The Future of Web Layout: CSS Multi-Column Explained    │
│─────────────────────────────────────────────────────────────────│
│  Lorem ipsum   │   Duis autem   │  Nam liber tem  │             │
│  dolor sit...  │   vel eum...   │  por cum...     │             │
│─────────────────────────────────────────────────────────────────│
│  "CSS Multi-Column Layout brings the elegance of print to web." │
│─────────────────────────────────────────────────────────────────│
│  Lorem ipsum   │   Duis autem   │  Nam liber      │             │
│  continues...  │   continues... │  continues...   │             │
└──────────────────────────────────────────────────────────────────┘
```

---

### Stage 3: Enhancements — Typography & Polish

Add these styles to make it look genuinely magazine-quality:

```css
/* First paragraph — drop the first letter (drop cap) */
.article p:first-of-type::first-letter {
  font-size: 3em;
  font-weight: bold;
  float: left;
  line-height: 1;
  margin-right: 6px;
  color: #333;
}

/* Justify text like a real newspaper */
.article p {
  text-align: justify;
}
```

**Milestone 3:** The first letter of the first paragraph is large and decorative (a "drop cap" effect). All text is fully justified across each column — exactly like a real printed newspaper.

---

### Stage 4: Final Complete Code

Here is the entire finished article page in one file:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>The Daily Reader</title>
  <style>
    * { box-sizing: border-box; }

    body {
      font-family: Georgia, serif;
      font-size: 16px;
      line-height: 1.7;
      color: #222;
      background-color: #fdfdfd;
      max-width: 960px;
      margin: 0 auto;
      padding: 20px;
    }

    header {
      text-align: center;
      border-bottom: 3px double #333;
      padding-bottom: 12px;
      margin-bottom: 24px;
    }
    header h1 {
      font-size: 2.5em;
      letter-spacing: 3px;
      text-transform: uppercase;
      margin-bottom: 4px;
    }
    header p {
      color: #666;
      font-style: italic;
      font-size: 0.9em;
    }

    .article {
      columns: 200px 3;
      column-gap: 40px;
      column-rule: 1px solid #ccc;
    }

    .article h2 {
      column-span: all;
      font-size: 1.6em;
      text-align: center;
      border-bottom: 2px solid #333;
      padding-bottom: 10px;
      margin-bottom: 20px;
    }

    .article .pull-quote {
      column-span: all;
      background-color: #f5f5f5;
      border-left: 4px solid #333;
      padding: 16px 24px;
      margin: 20px 0;
      font-size: 1.15em;
      font-style: italic;
      color: #444;
    }

    .article p {
      text-align: justify;
    }

    .article p:first-of-type::first-letter {
      font-size: 3em;
      font-weight: bold;
      float: left;
      line-height: 1;
      margin-right: 6px;
      color: #333;
    }

    footer {
      text-align: center;
      border-top: 1px solid #ccc;
      margin-top: 30px;
      padding-top: 12px;
      font-size: 0.85em;
      color: #999;
    }
  </style>
</head>
<body>

  <header>
    <h1>The Daily Reader</h1>
    <p>Technology · Science · Culture</p>
  </header>

  <div class="article">

    <h2>The Future of Web Layout: CSS Multi-Column Explained</h2>

    <p>
      Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam
      nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat
      volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation
      ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
    </p>

    <p>
      Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse
      molestie consequat, vel illum dolore eu feugiat nulla facilisis at
      vero eros et accumsan et iusto odio dignissim qui blandit praesent
      luptatum zzril delenit augue duis dolore te feugait nulla facilisi.
    </p>

    <blockquote class="pull-quote">
      "CSS Multi-Column Layout brings the elegance of print directly to the web."
    </blockquote>

    <p>
      Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam
      nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat
      volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation
      ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat.
    </p>

    <p>
      Nam liber tempor cum soluta nobis eligend optio congue nihil quod doming
      id quod mazim placerat facer possim assum. Typi non habent claritatem
      insitam, est usus legentis in iis qui facit eorum claritatem.
    </p>

  </div>

  <footer>
    <p>© 2026 The Daily Reader. All rights reserved.</p>
  </footer>

</body>
</html>
```

**Final Milestone Output:**
- Professional newspaper-style header with double border underline
- Full-width article headline spanning all three columns
- Three justified columns of text with subtle grey rule dividers
- A pull-quote spanning all columns mid-article
- A large drop cap on the first letter of the article
- Clean footer

### Reflection Questions

- Which property controls the number of columns: `column-count` or `column-width`? When would you use each?
- What makes `column-span: all` useful? What would happen without it?
- Why is the `columns` shorthand helpful compared to writing `column-width` and `column-count` separately?
- How would you update this page to show only 2 columns on a narrow screen? (Hint: you could use a media query, but `column-width` handles it automatically!)

### Optional Extensions

- Try changing `column-rule: 1px solid #ccc` to `column-rule: 4px double steelblue`.
- Try `column-rule-style: groove` or `ridge` — what do they look like?
- Add a second `<h2>` in the middle of the article body with `column-span: all` for a mid-article section break.
- Try wrapping the whole `.article` in a `max-width: 700px` container and resize — watch how columns change with `column-width` set.

---

## Common Beginner Mistakes

### Mistake 1 — Applying Column Properties to the Wrong Element

Column properties go on the **container** (`<div>`, `<article>`, `<section>`) — NOT on individual paragraphs or headings.

```css
/* WRONG — applied to each paragraph */
p {
  column-count: 3;
}

/* CORRECT — applied to the container holding the paragraphs */
.article {
  column-count: 3;
}
```

---

### Mistake 2 — `column-rule-width` Without `column-rule-style`

Setting only `column-rule-width` produces no visible line. The rule only appears when `column-rule-style` is set to something other than `none`.

```css
/* WRONG — rule is invisible */
.article {
  column-count: 3;
  column-rule-width: 4px;
  column-rule-color: red;
}

/* CORRECT — rule is now visible */
.article {
  column-count: 3;
  column-rule-style: solid;  /* This must be set! */
  column-rule-width: 4px;
  column-rule-color: red;
}
```

---

### Mistake 3 — Confusing `column-gap` and `column-rule`

Beginners sometimes think column-rule adds extra width. It does NOT. The rule lives **inside** the gap. If your rule is wider than the gap, it overlaps under the text — it doesn't push the columns apart.

```css
/* Potential issue: rule is 60px but gap is only 20px */
.article {
  column-count: 3;
  column-gap: 20px;
  column-rule: 60px solid red;   /* rule wider than gap — overlaps text */
}

/* CORRECT: rule width should be smaller than gap */
.article {
  column-count: 3;
  column-gap: 40px;
  column-rule: 2px solid red;    /* rule much thinner than gap */
}
```

---

### Mistake 4 — Putting `column-span` on the Container

`column-span` should be applied to an **element inside** the multi-column container — such as a heading `<h2>` or a `<blockquote>` — not to the container itself.

```css
/* WRONG — column-span on the container itself */
.article {
  column-count: 3;
  column-span: all;   /* meaningless here */
}

/* CORRECT — column-span on a child element inside the container */
.article h2 {
  column-span: all;   /* makes the h2 span all columns */
}
```

---

### Mistake 5 — Expecting `column-width` to Set an Exact Width

`column-width` is a **suggestion**, not a strict rule. The browser uses it as a guide to calculate how many columns to create, but the actual column width may differ.

```css
/* This means "try for ~150px columns" — not "make every column exactly 150px" */
.article {
  column-width: 150px;
}
```

If you need exact column widths, use CSS Grid instead.

---

### Mistake 6 — Short Text with Many Columns

If there isn't enough text to fill all the specified columns, you get empty columns at the end. This looks awkward.

```css
/* PROBLEM: only 1 sentence of text split into 5 columns looks strange */
.article {
  column-count: 5;
}
```

**Tip:** Only use as many columns as your content comfortably fills. 2–3 columns work well for most text content.

---

## Reflection Questions

1. What does `column-count` do, and what happens when you set it to `auto`?
2. What is `column-gap` and what is its default value?
3. Why must `column-rule-style` be set before `column-rule-width` and `column-rule-color` have any effect?
4. Write the `column-rule` shorthand for: 3px wide, dashed style, colour `#666`.
5. What are the two values accepted by `column-span`? What does each one do?
6. What is the difference between `column-count` and `column-width`? When would you prefer one over the other?
7. Write the `columns` shorthand that sets a suggested width of `200px` and a maximum of 3 columns.
8. Why does `column-rule` not take up space in the layout?
9. What happens to column rules when a `column-span: all` element appears mid-article?
10. How does using `column-width` instead of `column-count` make a layout automatically responsive?

---

## Completion Checklist

Check each item off as you complete it:

- [ ] I can explain what CSS multi-column layout is and why it's useful
- [ ] I can apply `column-count` to split content into N columns
- [ ] I can apply `column-gap` to control spacing between columns
- [ ] I understand that `column-rule-style` must be set for a rule to appear
- [ ] I can use `column-rule-style`, `column-rule-width`, and `column-rule-color` separately
- [ ] I can use the `column-rule` shorthand (width style color) to replace all three
- [ ] I know all valid values for `column-rule-style` (solid, dashed, dotted, double, groove, ridge, etc.)
- [ ] I can apply `column-span: all` to make an element stretch across all columns
- [ ] I can use `column-width` for a flexible, responsive column layout
- [ ] I can use the `columns` shorthand to set both width and count together
- [ ] I have completed all 5 guided exercises
- [ ] I have built the magazine-style article mini-project from scratch

---

## Lesson Summary

In this lesson you explored the **CSS Multi-column Layout Module** — a set of properties that let you split content into newspaper-style columns with just a few lines of CSS.

You started with `column-count`, the core property that divides a container's content into a specified number of equal columns. You then used `column-gap` to add comfortable whitespace between those columns so readers can distinguish them clearly.

Next you learned the column rule system — three individual properties that draw a decorative vertical line between columns: `column-rule-style` for the line appearance (solid, dashed, dotted, etc.), `column-rule-width` for the thickness, and `column-rule-color` for the colour. You then simplified all three into the `column-rule` shorthand, which follows the same `width style color` pattern as the `border` property.

You used `column-span: all` to make headings and pull-quotes break out of the column flow and stretch across the full container width — essential for newspaper-style article headers. You then compared `column-count` with `column-width`, understanding that `column-width` creates responsive layouts that automatically adjust the number of columns based on available space. Finally, the `columns` shorthand combined both width and count into a single declaration.

All these skills came together in the magazine-style article mini-project, where you built a professionally styled, multi-column news article page complete with a spanning headline, a mid-article pull-quote, a decorative drop cap, and subtle column dividers — all using only HTML and CSS.

---

*Lesson 63 — CSS Multiple Columns | Source: W3Schools CSS Multiple Columns & Column Rules Tutorials*
