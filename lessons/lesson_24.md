---
render_with_liquid: false
title: "CSS Overflow — Controlling What Happens When Content Is Too Big"
nav_order: 24
---

# Lesson 24 — CSS Overflow: Controlling What Happens When Content Is Too Big

---

## Lesson Introduction

Have you ever seen a webpage where text spills out of a box, or where a box has a scrollbar so you can read more content inside it? That is CSS **overflow** at work.

In this lesson you will learn:

- What overflow means in CSS and why it matters
- The five values of the `overflow` property: `visible`, `hidden`, `scroll`, `auto`, and `clip`
- How to control overflow separately on the horizontal axis (`overflow-x`) and the vertical axis (`overflow-y`)
- Real-world situations where each value is the best choice
- How to combine `overflow-x` and `overflow-y` for fine-grained control
- Common beginner mistakes and how to avoid them

By the end of this lesson you will be able to build a polished **mini-profile card widget** that uses overflow correctly, just like a real front-end developer would.

---

## Prerequisite Concepts

Before diving into overflow, make sure you understand these building blocks. If anything below looks unfamiliar, read the short explanation before continuing.

### What is a CSS Box?

Every HTML element on a webpage is treated as a rectangular box. That box has four layers:

```
+----------------------------------+
|           MARGIN                 |
|  +----------------------------+  |
|  |        BORDER              |  |
|  |  +----------------------+  |  |
|  |  |      PADDING         |  |  |
|  |  |  +----------------+  |  |  |
|  |  |  |   CONTENT      |  |  |  |
|  |  |  +----------------+  |  |  |
|  |  +----------------------+  |  |
|  +----------------------------+  |
+----------------------------------+
```

The **content area** is where your text, images, and child elements live. When you set `width` and `height` on an element, you are setting the size of that content area.

### What is Width and Height?

```css
div {
  width: 200px;   /* The box is 200 pixels wide */
  height: 100px;  /* The box is 100 pixels tall */
}
```

These two properties create a fixed-size box. The moment you make a box a fixed size, you create the *possibility* of overflow — because the content inside might be bigger than the box.

### What Are Block Elements?

Block elements (like `<div>`, `<p>`, `<section>`) take up the full width of their parent and stack vertically. The `overflow` property only works on **block elements that have a set height**. Keep this rule in mind — it is very important.

---

## Part 1 — Understanding Overflow

### What Is Overflow?

Think of a box as a glass of water. If you pour too much water in, it spills over the edges. In CSS, when content is too large to fit inside a box, it **overflows** — it spills outside the box's boundaries.

**The problem overflow solves:** Without any overflow rules, content just keeps spilling out, which can break your entire page layout. Overflow gives you control over what happens in that situation.

Real-world analogy: Imagine a receipt printer at a supermarket. The paper has a fixed width. If the product name is too long, should it spill off the edge of the paper? Should it be cut off? Should it wrap? The `overflow` property answers exactly that question for CSS boxes.

### When Does Overflow Happen?

Overflow happens when:

1. You give an element a fixed `height` and the content inside is taller than that height.
2. You give an element a fixed `width` and the content inside is wider than that width.
3. A child element is absolutely positioned outside its parent.
4. You use `white-space: nowrap` and a long line of text cannot wrap.

> **Key Rule to remember:** The `overflow` property only takes effect when the element has a set height. Without a height, block elements simply grow taller to fit their content, so overflow never occurs.

---

## Part 2 — The `overflow` Property and Its Values

The `overflow` property is written like this:

```css
selector {
  overflow: value;
}
```

There are five values you need to know:

| Value     | What it does                                                          |
|-----------|-----------------------------------------------------------------------|
| `visible` | Default. Content spills outside the box. Nothing is hidden.           |
| `hidden`  | Content that overflows is cut off (clipped) and hidden.               |
| `scroll`  | Always shows scrollbars. User scrolls to see hidden content.          |
| `auto`    | Smart — only adds scrollbars when content actually overflows.         |
| `clip`    | Like hidden, but does NOT create a scroll container (advanced).       |

Let's explore each one deeply.

---

### Value 1 — `overflow: visible` (The Default)

#### What Is It?

`visible` is the **default value** of the overflow property. You never need to write it explicitly unless you are overriding a previous setting.

With `overflow: visible`, content that is too large to fit inside the box simply **renders outside the box boundaries**. It is not clipped, not hidden, and no scrollbar appears.

#### Why Does This Exist?

Beginners often wonder: "Why would I want content to spill outside its box?" The answer is that sometimes you do — for example, tooltips, dropdown menus, or decorative elements that extend beyond a container. Also, it is the safe default: your content is never accidentally hidden.

**Important:** Even though the content is visible outside the box, it does **not** affect the flow of the page. Other elements on the page do not move to make room for the overflowing content — they stay exactly where they are.

#### Simple Example

```html
<!-- HTML -->
<div class="box">
  This is a very long paragraph of text that will not fit inside
  this small box. It will just spill outside the box boundaries
  and render over whatever is below it.
</div>
<p>This paragraph is right below the box.</p>
```

```css
/* CSS */
.box {
  width: 200px;
  height: 65px;
  background-color: coral;
  overflow: visible; /* This is the default — you don't need to write it */
}
```

**Expected Output (visual description):**
```
+-----------------------------+
|  This is a very long par... | ← coral box (65px tall)
+-----------------------------+
  ...agraph of text that will  ← content spills out below
  not fit inside this small    ← it overlaps the paragraph below
  box. It will just spill...
This paragraph is right below the box.  ← paragraph does NOT move
```

The overflowing text does not push the paragraph down — it overlaps it. This is the key behaviour of `overflow: visible`.

> 💭 **Think about it:** What would happen if you removed the `height: 65px` property? Try it! The box would simply grow taller to fit all the text, and there would be no overflow at all.

---

### Value 2 — `overflow: hidden`

#### What Is It?

With `overflow: hidden`, any content that goes beyond the box boundaries is **cut off and completely hidden**. It is as if you took scissors to everything outside the box.

#### Why Use It?

- To prevent overflowing content from ruining your layout
- To create clean, cropped image effects
- To hide long text that users do not need to read (for example, a subtitle that is too long for a card component)
- As a technique for clearing floats (covered in a later lesson)

#### Simple Example

```html
<!-- HTML -->
<div class="box">
  This is a very long paragraph of text that will not fit inside
  this small box. Watch what happens to the extra text.
</div>
```

```css
/* CSS */
.box {
  width: 200px;
  height: 65px;
  background-color: lightblue;
  overflow: hidden;
}
```

**Expected Output (visual description):**
```
+-----------------------------+
|  This is a very long par... | ← only 65px of content is visible
+-----------------------------+
                               ← everything below is GONE (hidden)
```

The text is cleanly cut off at the box boundary. No scrollbar appears. The hidden text still exists in the HTML — it is just not rendered on screen.

#### Second Example — Cropping an Image

```html
<!-- HTML -->
<div class="image-frame">
  <img src="large-photo.jpg" alt="Landscape" />
</div>
```

```css
/* CSS */
.image-frame {
  width: 300px;
  height: 200px;
  overflow: hidden;  /* Crops the image to fit the frame exactly */
}

.image-frame img {
  width: 500px;  /* Image is wider than the frame */
}
```

**Expected Output:** The image displays inside the 300×200 frame, and the parts of the image that are wider than 300px are cleanly cropped off. This is exactly how profile picture circles and thumbnail images are made on real websites.

> 💭 **Think about it:** What if you need users to access the hidden content? `overflow: hidden` removes it from view permanently. That is when you need `scroll` or `auto` instead.

---

### Value 3 — `overflow: scroll`

#### What Is It?

With `overflow: scroll`, the browser **always adds scrollbars** to the element — both a vertical scrollbar and a horizontal scrollbar — regardless of whether the content actually overflows. Users can scroll to see all the content.

#### Why Use It?

- For content boxes where users need to read everything (terms and conditions, long descriptions, chat windows, comment sections)
- When you want consistent scrollbar space so your layout does not shift when content changes

#### Simple Example

```html
<!-- HTML -->
<div class="box">
  Chapter 1: The Beginning. Lorem ipsum dolor sit amet, consectetur
  adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore
  magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco.
  Chapter 2: The Middle. Duis aute irure dolor in reprehenderit in
  voluptate velit esse cillum dolore eu fugiat nulla pariatur.
  Chapter 3: The End. Excepteur sint occaecat cupidatat non proident.
</div>
```

```css
/* CSS */
.box {
  width: 300px;
  height: 100px;
  background-color: lightyellow;
  border: 1px solid #ccc;
  overflow: scroll;
}
```

**Expected Output:**
```
+-----------------------------------+  ↑
| Chapter 1: The Beginning. Lorem   |  |
| ipsum dolor sit amet, consectetur |  | 100px
| adipiscing elit. Sed do eiusmod   |  | visible
+-----------------------------------+ ↓|
[=======================]  ← horizontal scrollbar (always shown)
     ↕  ← vertical scrollbar (always shown)
```

Both scrollbars appear even if the content only overflows in one direction. This is a known drawback of `scroll` — the horizontal scrollbar may appear even when it is not needed.

> 💭 **Think about it:** What if the box has very little text and no overflow happens at all? The scrollbars still appear with `overflow: scroll` — they just cannot be scrolled. Is that good design? Usually not. That is why `auto` is often a better choice.

---

### Value 4 — `overflow: auto` ⭐ (Recommended for Most Cases)

#### What Is It?

`overflow: auto` is the **smart version** of `scroll`. The browser checks whether the content actually overflows. If it does, a scrollbar is added only in the direction where overflow occurs. If it does not overflow, no scrollbar appears at all.

#### Why Use It?

- Cleaner design — no unnecessary scrollbars
- Flexible — works correctly whether content is short or long
- The most commonly used overflow value in professional web development

#### Simple Example

```html
<!-- HTML: Example A — content overflows -->
<div class="box">
  This is a long text that exceeds the height of the box.
  More content here. Even more content here.
  And here is some additional text to make it even longer.
</div>
```

```css
/* CSS */
.box {
  width: 300px;
  height: 80px;
  background-color: #f0f0f0;
  border: 1px solid #999;
  overflow: auto;
}
```

**Expected Output (content overflows):**
```
+-----------------------------------+ ↑
| This is a long text that exceeds  | |
| the height of the box. More con...|↕| ← vertical scrollbar appears
+-----------------------------------+ ↓
```

Only the vertical scrollbar appears because the overflow is only vertical. No horizontal scrollbar.

```html
<!-- HTML: Example B — content does NOT overflow -->
<div class="box">Short text.</div>
```

**Expected Output (no overflow):**
```
+-----------------------------------+
| Short text.                       |
+-----------------------------------+
```

No scrollbars at all — the box looks completely clean. This is the difference between `scroll` and `auto`.

#### Comparison Table — `scroll` vs `auto`

| Situation                      | `overflow: scroll`         | `overflow: auto`           |
|-------------------------------|---------------------------|---------------------------|
| Content overflows vertically  | Vertical + horizontal bars | Only vertical scrollbar    |
| Content overflows horizontally| Vertical + horizontal bars | Only horizontal scrollbar  |
| No overflow at all            | Both scrollbars still show | No scrollbars shown        |
| Layout stability               | Consistent (bars always there) | Shifts slightly when bars appear |

> ⭐ **Best practice:** In most situations, prefer `overflow: auto` over `overflow: scroll`. It gives a cleaner appearance and only shows controls when they are actually needed.

---

### Value 5 — `overflow: clip` (Advanced)

#### What Is It?

`overflow: clip` is the newest overflow value. It looks very similar to `overflow: hidden` — it cuts off content that overflows — but with one important technical difference: it does **not** create a scroll container.

#### What Is a Scroll Container?

When you use `hidden`, `scroll`, or `auto`, the browser creates what is called a **scroll container** — a scrollable region, even if no scrollbar is visible. This has a side effect: you cannot have one axis set to `clip`/`hidden` while the other axis is set to `visible`. The scroll container limitation prevents it.

`clip` removes this limitation. It is pure clipping without any scroll container.

#### Why Use `clip`?

- When you want to clip content in one direction while keeping it visible in another direction
- When you specifically do NOT want the element to be programmatically scrollable
- For certain advanced layout techniques

#### Simple Example

```css
/* CSS */
.box {
  width: 300px;
  height: 100px;
  overflow-x: clip;   /* Clip horizontal overflow */
  overflow-y: visible; /* Allow vertical overflow to show */
}
```

With `hidden` instead of `clip`, the above combination would not work as expected. `clip` enables this kind of fine-grained directional control.

> 📝 **Note for beginners:** You will use `clip` rarely. For everyday work, `hidden`, `auto`, and `scroll` are the three values you will reach for most often. Learn `clip` when you encounter a specific layout problem that those three cannot solve.

---

## Part 3 — Controlling Each Direction Separately: `overflow-x` and `overflow-y`

So far you have used the shorthand `overflow` property, which applies the same rule to both horizontal (left/right) and vertical (up/down) overflow. But CSS also gives you two separate properties:

- `overflow-x` — controls what happens to content that overflows **horizontally** (left and right edges)
- `overflow-y` — controls what happens to content that overflows **vertically** (top and bottom edges)

Both properties accept the same values: `visible`, `hidden`, `scroll`, `auto`, and `clip`.

### Why Would You Use These Separately?

Real-world scenario: You are building a **data table** that can have many columns. You want users to be able to scroll horizontally to see all columns, but you do not want a vertical scrollbar — the table should just show all rows. Solution: `overflow-x: auto` + `overflow-y: visible`.

Another scenario: A **chat window** where you always want vertical scrolling for messages, but never horizontal scrolling: `overflow-x: hidden` + `overflow-y: auto`.

---

### `overflow-x` — Controlling Horizontal Overflow

`overflow-x` controls content that overflows on the left or right sides of the box.

#### Simple Example — Horizontal Scrollbar

```html
<!-- HTML -->
<div class="wide-content">
  This sentence is extremely long and will not wrap because we 
  have turned off text wrapping using white-space: nowrap — which 
  forces all text onto one single line no matter how long it gets.
</div>
```

```css
/* CSS */
.wide-content {
  width: 300px;
  height: 60px;
  border: 2px solid steelblue;
  white-space: nowrap;  /* Forces text onto one line — causes horizontal overflow */
  overflow-x: scroll;   /* Adds a horizontal scrollbar */
}
```

**Expected Output:**
```
+--------------------------------------------→ (scroll right)
| This sentence is extremely long and will no|  ← text cut at right edge
+--------------------------------------------+
[========================]  ← horizontal scrollbar
```

Users can scroll right to read the rest of the sentence.

#### `overflow-x: hidden` — Hiding Horizontal Overflow

```css
/* CSS */
.cropped {
  width: 300px;
  overflow-x: hidden;  /* Hide anything that sticks out to the right */
}
```

This is commonly used to prevent a child element (like an animated element that slides in from the right) from causing a horizontal scrollbar on the entire page.

#### All `overflow-x` Values

```css
.box { overflow-x: visible; } /* Default — horizontal overflow shows outside */
.box { overflow-x: hidden;  } /* Horizontal overflow is cut off and hidden */
.box { overflow-x: scroll;  } /* Horizontal scrollbar always shown */
.box { overflow-x: auto;    } /* Horizontal scrollbar only when needed */
```

---

### `overflow-y` — Controlling Vertical Overflow

`overflow-y` controls content that overflows the top or bottom edges of the box.

#### Simple Example — Vertical Scrollbar

```html
<!-- HTML -->
<div class="scrollable-text">
  <p>Paragraph 1: The quick brown fox jumps over the lazy dog.</p>
  <p>Paragraph 2: Pack my box with five dozen liquor jugs.</p>
  <p>Paragraph 3: How vexingly quick daft zebras jump!</p>
  <p>Paragraph 4: The five boxing wizards jump quickly.</p>
  <p>Paragraph 5: Sphinx of black quartz, judge my vow.</p>
</div>
```

```css
/* CSS */
.scrollable-text {
  width: 300px;
  height: 80px;    /* Box is only 80px tall — content is taller */
  border: 2px solid tomato;
  overflow-y: scroll;  /* Always show vertical scrollbar */
}
```

**Expected Output:**
```
+-----------------------------------+ ↑
| Paragraph 1: The quick brown fox  | |
| jumps over the lazy dog.          |↕| ← vertical scrollbar
+-----------------------------------+ ↓
```

Users can scroll up and down to read all five paragraphs.

#### `overflow-y: hidden` — Cutting Off Vertical Content

```css
/* CSS */
.preview-card {
  width: 250px;
  height: 100px;
  overflow-y: hidden;  /* Show only the top 100px of content */
  background: #fff;
  border: 1px solid #ddd;
}
```

This is a classic design pattern: show a preview of an article or blog post, cutting it off at a fixed height, then adding a "Read more" button below.

---

### Combining `overflow-x` and `overflow-y`

The real power comes when you combine both properties. You can set completely different behaviour for each axis.

#### Example — Horizontal Scroll, Vertical Hidden

```css
/* CSS */
.data-table-wrapper {
  width: 500px;
  height: auto;
  overflow-x: auto;    /* Scroll horizontally if table is wider than 500px */
  overflow-y: visible; /* Let height grow as needed — no vertical scroll */
}
```

> **Important rule:** You cannot set one axis to `visible` while the other axis is set to `hidden`, `scroll`, or `auto` — unless you use `clip` for the visible direction. If you try this combination with `hidden`/`scroll`/`auto`, the browser automatically changes the `visible` axis to `auto`. This is a known CSS quirk.

#### Correct Cross-Axis Combination

```css
/* This works correctly */
.element {
  overflow-x: auto;
  overflow-y: hidden;
}

/* This also works */
.element {
  overflow-x: scroll;
  overflow-y: auto;
}

/* This has a quirk — the 'visible' will be converted to 'auto' by the browser */
.element {
  overflow-x: hidden;
  overflow-y: visible;  /* Browser may change this to 'auto' */
}

/* Use 'clip' instead of 'hidden' to avoid the quirk */
.element {
  overflow-x: clip;     /* True clipping — no scroll container created */
  overflow-y: visible;  /* This now works as expected */
}
```

---

### The Shorthand `overflow` with Two Values

You can also write `overflow` with two values in one line. The first value applies to `overflow-x`, the second to `overflow-y`:

```css
/* Syntax: overflow: [x-value] [y-value]; */

.box { overflow: hidden scroll; }
/* Equivalent to: overflow-x: hidden; overflow-y: scroll; */

.box { overflow: auto hidden; }
/* Equivalent to: overflow-x: auto; overflow-y: hidden; */

.box { overflow: scroll auto; }
/* Equivalent to: overflow-x: scroll; overflow-y: auto; */
```

When you write only one value (like `overflow: hidden`), both axes are set to the same value.

---

## Part 4 — Guided Practice Exercises

### Exercise 1 — Identifying Overflow Values (Warm-up)

**Objective:** Match each real-world scenario to the correct overflow value.

**Scenarios:**

1. A news website shows article previews. Each preview card is exactly 120px tall. The article text is always longer than 120px. You want to cut off the extra text — no scrollbar, no spilling.

2. A legal website has a "Terms and Conditions" box. The box is 200px tall. Users must be able to read all the text by scrolling. Show a scrollbar only when needed.

3. A social media post card shows a user's bio. The bio might be short or long. If it is longer than the card, the user should be able to scroll vertically to read it all. If it fits, no scrollbar should appear.

4. A technical documentation site has code examples. The code may be very long horizontally. Users should always see a horizontal scrollbar so they know they can scroll.

**Expected Answers:**

1. `overflow: hidden` — cuts off text with no scrollbar
2. `overflow: auto` — scrollbar appears only when needed
3. `overflow-y: auto` — only vertical scrollbar when needed
4. `overflow-x: scroll` — horizontal scrollbar always visible

---

### Exercise 2 — Building an Article Preview Card

**Objective:** Create a blog article preview card that clips long text.

**Scenario:** You are building a blog homepage. Each article card is 300px wide and 150px tall. The article title and excerpt are inside the card. If the excerpt is too long, clip it cleanly.

**Steps:**

1. Create the HTML structure.
2. Set a fixed width and height on the card.
3. Apply `overflow: hidden` to clip the content.
4. Add a background colour and some padding for appearance.

**Your Code:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .article-card {
      width: 300px;
      height: 150px;
      background-color: #ffffff;
      border: 1px solid #ddd;
      border-radius: 8px;
      padding: 16px;
      overflow: hidden;   /* Clips any content that goes beyond 150px */
      box-sizing: border-box;
    }

    .article-card h2 {
      font-size: 18px;
      margin: 0 0 8px 0;
      color: #333;
    }

    .article-card p {
      font-size: 14px;
      color: #666;
      line-height: 1.5;
      margin: 0;
    }
  </style>
</head>
<body>

  <div class="article-card">
    <h2>Understanding Black Holes</h2>
    <p>
      Black holes are regions of spacetime where gravity is so strong that 
      nothing — not even light or other electromagnetic waves — has enough 
      speed to escape the event horizon. The theory of general relativity 
      predicts that a sufficiently compact mass can deform spacetime to form 
      a black hole. The boundary of no escape is called the event horizon.
    </p>
  </div>

</body>
</html>
```

**Expected Output:** A neat 300×150 card showing the title and the first two or three lines of the paragraph. The rest of the paragraph is cleanly clipped at the bottom of the card. No scrollbar appears.

**Self-check Questions:**
- What happens if you change `overflow: hidden` to `overflow: auto`?
- What happens if you remove the `height: 150px` completely?
- What happens if you change the height to `300px`?

**What-If Challenge:** Add a "Read more →" link below the card (outside the card div). This is exactly how real blog preview cards are built.

---

### Exercise 3 — Building a Scrollable Chat Window

**Objective:** Create a chat message window that scrolls vertically.

**Scenario:** You are building a simple messaging application. The chat box is 350px wide and 200px tall. Messages stack vertically. When there are more messages than fit in 200px, the user should be able to scroll down.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .chat-window {
      width: 350px;
      height: 200px;
      border: 2px solid #4a90d9;
      border-radius: 10px;
      background-color: #f5f5f5;
      overflow-y: auto;    /* Vertical scroll when messages overflow */
      overflow-x: hidden;  /* Never scroll horizontally */
      padding: 10px;
      box-sizing: border-box;
    }

    .message {
      background-color: #fff;
      border: 1px solid #ddd;
      border-radius: 8px;
      padding: 8px 12px;
      margin-bottom: 8px;
      font-size: 14px;
      color: #333;
    }

    .message.sent {
      background-color: #d1e8ff;
      text-align: right;
    }
  </style>
</head>
<body>

  <div class="chat-window">
    <div class="message">Hey! How are you?</div>
    <div class="message sent">I'm great, thanks! Working on a web project.</div>
    <div class="message">Oh cool! What are you building?</div>
    <div class="message sent">A CSS lesson on overflow. It's pretty fun!</div>
    <div class="message">That sounds useful. Overflow trips me up sometimes.</div>
    <div class="message sent">Same! But once you understand it, it all clicks.</div>
    <div class="message">What's the difference between scroll and auto?</div>
    <div class="message sent">Auto only shows scrollbars when needed. Scroll always shows them.</div>
    <div class="message">Got it! Thanks for explaining.</div>
  </div>

</body>
</html>
```

**Expected Output:** A 350×200 chat box. The first few messages are visible. A vertical scrollbar appears on the right side because there are too many messages to fit. No horizontal scrollbar appears.

**Self-check Questions:**
- Why did we use `overflow-y: auto` instead of `overflow-y: scroll`?
- What would happen if we used `overflow: hidden` on the chat window?
- Why is `overflow-x: hidden` a good idea on a chat window?

---

### Exercise 4 — Responsive Data Table Wrapper

**Objective:** Make a wide data table scroll horizontally on small screens.

**Scenario:** You are displaying a sales data table with many columns. On large screens it fits fine, but on small screens the table overflows. Instead of breaking the layout, you want horizontal scrolling.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .table-wrapper {
      width: 100%;
      max-width: 500px;   /* Simulate a smaller screen */
      overflow-x: auto;   /* Horizontal scroll when table is wider */
      overflow-y: visible; /* Let height grow normally */
      border: 1px solid #ccc;
    }

    table {
      width: 800px;        /* Table is wider than the wrapper */
      border-collapse: collapse;
      font-size: 14px;
    }

    th, td {
      border: 1px solid #ddd;
      padding: 8px 16px;
      text-align: left;
      white-space: nowrap;  /* Prevent cells from wrapping */
    }

    th {
      background-color: #4a90d9;
      color: white;
    }

    tr:nth-child(even) {
      background-color: #f2f2f2;
    }
  </style>
</head>
<body>

  <div class="table-wrapper">
    <table>
      <thead>
        <tr>
          <th>Product</th>
          <th>Category</th>
          <th>Q1 Sales</th>
          <th>Q2 Sales</th>
          <th>Q3 Sales</th>
          <th>Q4 Sales</th>
          <th>Total</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Laptop Pro X</td>
          <td>Electronics</td>
          <td>₦1,200,000</td>
          <td>₦980,000</td>
          <td>₦1,500,000</td>
          <td>₦2,100,000</td>
          <td>₦5,780,000</td>
        </tr>
        <tr>
          <td>Office Chair</td>
          <td>Furniture</td>
          <td>₦340,000</td>
          <td>₦420,000</td>
          <td>₦390,000</td>
          <td>₦510,000</td>
          <td>₦1,660,000</td>
        </tr>
        <tr>
          <td>LED Monitor</td>
          <td>Electronics</td>
          <td>₦760,000</td>
          <td>₦820,000</td>
          <td>₦910,000</td>
          <td>₦1,050,000</td>
          <td>₦3,540,000</td>
        </tr>
      </tbody>
    </table>
  </div>

</body>
</html>
```

**Expected Output:** A table wrapper that is at most 500px wide. The table inside is 800px wide, so it overflows horizontally. A horizontal scrollbar appears at the bottom of the wrapper. Users can scroll right to see all seven columns. No vertical scrollbar.

**What-If Challenge:** Try changing `overflow-x: auto` to `overflow-x: hidden`. What happens to the columns that were hidden? Can users still access them? This shows why `hidden` is the wrong choice for data tables.

---

## Part 5 — Mini Project: Scrollable Profile Card Widget

### Project Overview

You will build a complete **Profile Card Widget** that uses overflow correctly in multiple places:

1. A circular avatar image (cropped with overflow)
2. A fixed-height bio section with vertical scroll
3. A horizontal tag list that scrolls if tags overflow
4. A skills table wrapper with horizontal scroll

This is exactly the type of component used on social media platforms, job boards, and portfolio websites.

---

### Stage 1 — Setup and Avatar

**Goal:** Create the card container and the circular avatar image.

**Preview:** A white card with rounded corners. The avatar image is circular and cropped perfectly.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Reset */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: #e8f4f8;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      font-family: Arial, sans-serif;
    }

    /* ---- STAGE 1: Card and Avatar ---- */
    .profile-card {
      width: 360px;
      background-color: #ffffff;
      border-radius: 16px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.12);
      overflow: hidden;  /* Important: clips the header background at rounded corners */
    }

    .card-header {
      background-color: #4a90d9;
      height: 80px;
      position: relative;
    }

    .avatar-wrapper {
      width: 80px;
      height: 80px;
      border-radius: 50%;      /* Makes the wrapper a circle */
      overflow: hidden;         /* Crops the image to the circle shape */
      border: 3px solid #fff;
      position: absolute;
      bottom: -40px;
      left: 20px;
    }

    .avatar-wrapper img {
      width: 100%;
      height: 100%;
      object-fit: cover;        /* Ensures image fills the circle without distortion */
    }
  </style>
</head>
<body>
  <div class="profile-card">
    <div class="card-header">
      <div class="avatar-wrapper">
        <!-- Using a placeholder image service -->
        <img src="https://via.placeholder.com/80x80/6db3d4/ffffff?text=AM" alt="Avatar" />
      </div>
    </div>
    <!-- More sections will be added below -->
  </div>
</body>
</html>
```

**Milestone Output:** A blue header bar with a circular avatar that overlaps the bottom of the header. The avatar is perfectly cropped to a circle due to `border-radius: 50%` + `overflow: hidden`.

---

### Stage 2 — Name, Title, and Bio with Scroll

**Goal:** Add the person's name, job title, and a fixed-height bio section with vertical scroll.

```html
<!-- Add this inside .profile-card, after the .card-header div -->

<div class="card-body">
  <div class="profile-info">
    <h2 class="profile-name">Adaeze Madu</h2>
    <p class="profile-title">Senior Data Analyst · Lagos, Nigeria</p>
  </div>

  <div class="bio-section">
    <h3>About</h3>
    <div class="bio-text">
      <p>
        Passionate data analyst with 6 years of experience turning complex 
        datasets into actionable business insights. I specialise in Python, 
        SQL, and data visualisation tools including Power BI and Tableau.
      </p>
      <p>
        I have worked across fintech, healthcare, and e-commerce sectors, 
        delivering dashboards and predictive models that have directly 
        influenced product and strategy decisions at executive level.
      </p>
      <p>
        Outside of work, I mentor junior analysts through the CodeLagos 
        initiative and write a weekly newsletter on data literacy for 
        non-technical professionals.
      </p>
    </div>
  </div>
</div>
```

```css
/* Add these styles to your existing CSS */

.card-body {
  padding: 50px 20px 20px 20px;  /* Top padding makes room for the avatar */
}

.profile-name {
  font-size: 20px;
  font-weight: bold;
  color: #222;
}

.profile-title {
  font-size: 13px;
  color: #777;
  margin-top: 4px;
}

.bio-section {
  margin-top: 20px;
}

.bio-section h3 {
  font-size: 14px;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #4a90d9;
  margin-bottom: 8px;
}

.bio-text {
  height: 90px;       /* Fixed height — bio text will overflow this */
  overflow-y: auto;   /* Vertical scrollbar when bio is too long */
  overflow-x: hidden; /* Never scroll horizontally in the bio */
  padding-right: 8px; /* Space for scrollbar so it does not overlap text */
}

.bio-text p {
  font-size: 14px;
  color: #555;
  line-height: 1.6;
  margin-bottom: 10px;
}
```

**Milestone Output:** A bio section that is exactly 90px tall. The first paragraph is visible. A vertical scrollbar allows reading the full bio. No horizontal scroll.

---

### Stage 3 — Horizontal Tag List with Scroll

**Goal:** Add a skills tag list that scrolls horizontally if there are too many tags.

```html
<!-- Add this inside .card-body, after the .bio-section div -->

<div class="tags-section">
  <h3>Skills</h3>
  <div class="tags-list">
    <span class="tag">Python</span>
    <span class="tag">SQL</span>
    <span class="tag">Power BI</span>
    <span class="tag">Tableau</span>
    <span class="tag">Excel</span>
    <span class="tag">Machine Learning</span>
    <span class="tag">Statistics</span>
    <span class="tag">R</span>
    <span class="tag">Pandas</span>
    <span class="tag">Data Storytelling</span>
  </div>
</div>
```

```css
/* Add these styles */

.tags-section {
  margin-top: 16px;
}

.tags-section h3 {
  font-size: 14px;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #4a90d9;
  margin-bottom: 8px;
}

.tags-list {
  display: flex;          /* Place tags side by side horizontally */
  gap: 6px;
  overflow-x: auto;       /* Horizontal scroll when tags overflow */
  overflow-y: hidden;     /* No vertical scroll */
  padding-bottom: 6px;    /* Space for the scrollbar */
  white-space: nowrap;    /* Prevent tags from wrapping to the next line */
}

.tag {
  display: inline-block;
  background-color: #e8f4f8;
  color: #4a90d9;
  border: 1px solid #c5dff0;
  border-radius: 20px;
  padding: 4px 12px;
  font-size: 12px;
  font-weight: bold;
  flex-shrink: 0;         /* Prevent tags from shrinking */
}
```

**Milestone Output:** A row of skill tags. On the visible area you see tags like "Python", "SQL", "Power BI" etc. A horizontal scrollbar appears at the bottom of the tag row, allowing the user to scroll right to see all 10 tags.

---

### Stage 4 — Final Card (Put It All Together)

Here is the complete final code for your Profile Card Widget:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Profile Card — CSS Overflow Project</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: #e8f4f8;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      padding: 40px 16px;
      min-height: 100vh;
      font-family: Arial, sans-serif;
    }

    /* ---- CARD CONTAINER ---- */
    .profile-card {
      width: 360px;
      background-color: #ffffff;
      border-radius: 16px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.12);
      overflow: hidden;   /* Clips children at the card's rounded corners */
    }

    /* ---- HEADER ---- */
    .card-header {
      background-color: #4a90d9;
      height: 80px;
      position: relative;
    }

    /* ---- AVATAR (circular crop) ---- */
    .avatar-wrapper {
      width: 80px;
      height: 80px;
      border-radius: 50%;
      overflow: hidden;      /* Crops image to circle */
      border: 3px solid #fff;
      position: absolute;
      bottom: -40px;
      left: 20px;
    }

    .avatar-wrapper img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    /* ---- BODY ---- */
    .card-body {
      padding: 50px 20px 20px 20px;
    }

    .profile-name {
      font-size: 20px;
      font-weight: bold;
      color: #222;
    }

    .profile-title {
      font-size: 13px;
      color: #777;
      margin-top: 4px;
    }

    /* ---- BIO (vertical scroll) ---- */
    .bio-section {
      margin-top: 20px;
    }

    .bio-section h3,
    .tags-section h3,
    .stats-section h3 {
      font-size: 12px;
      text-transform: uppercase;
      letter-spacing: 1px;
      color: #4a90d9;
      margin-bottom: 8px;
    }

    .bio-text {
      height: 90px;
      overflow-y: auto;
      overflow-x: hidden;
      padding-right: 6px;
    }

    .bio-text p {
      font-size: 14px;
      color: #555;
      line-height: 1.6;
      margin-bottom: 10px;
    }

    /* ---- TAGS (horizontal scroll) ---- */
    .tags-section {
      margin-top: 16px;
    }

    .tags-list {
      display: flex;
      gap: 6px;
      overflow-x: auto;
      overflow-y: hidden;
      padding-bottom: 6px;
      white-space: nowrap;
    }

    .tag {
      display: inline-block;
      background-color: #e8f4f8;
      color: #4a90d9;
      border: 1px solid #c5dff0;
      border-radius: 20px;
      padding: 4px 12px;
      font-size: 12px;
      font-weight: bold;
      flex-shrink: 0;
    }

    /* ---- STATS ROW ---- */
    .stats-section {
      margin-top: 16px;
    }

    .stats-row {
      display: flex;
      gap: 12px;
      text-align: center;
    }

    .stat-box {
      flex: 1;
      background-color: #f8f9fa;
      border-radius: 8px;
      padding: 10px 6px;
    }

    .stat-number {
      font-size: 20px;
      font-weight: bold;
      color: #4a90d9;
    }

    .stat-label {
      font-size: 11px;
      color: #999;
      margin-top: 2px;
    }

    /* ---- FOOTER ---- */
    .card-footer {
      border-top: 1px solid #eee;
      margin-top: 16px;
      padding: 12px 20px;
      background-color: #fafafa;
      text-align: center;
    }

    .contact-btn {
      display: inline-block;
      background-color: #4a90d9;
      color: white;
      padding: 8px 24px;
      border-radius: 20px;
      font-size: 14px;
      text-decoration: none;
      font-weight: bold;
    }
  </style>
</head>
<body>

<div class="profile-card">

  <!-- HEADER + AVATAR -->
  <div class="card-header">
    <div class="avatar-wrapper">
      <img src="https://via.placeholder.com/80x80/6db3d4/ffffff?text=AM" alt="Adaeze Madu" />
    </div>
  </div>

  <!-- BODY -->
  <div class="card-body">

    <!-- Name and Title -->
    <h2 class="profile-name">Adaeze Madu</h2>
    <p class="profile-title">Senior Data Analyst · Lagos, Nigeria</p>

    <!-- Bio — vertical scroll -->
    <div class="bio-section">
      <h3>About</h3>
      <div class="bio-text">
        <p>Passionate data analyst with 6 years of experience turning complex 
        datasets into actionable business insights. I specialise in Python, 
        SQL, and data visualisation tools including Power BI and Tableau.</p>
        <p>I have worked across fintech, healthcare, and e-commerce sectors, 
        delivering dashboards and predictive models that have directly 
        influenced product and strategy decisions at executive level.</p>
        <p>Outside of work, I mentor junior analysts through the CodeLagos 
        initiative and write a weekly newsletter on data literacy.</p>
      </div>
    </div>

    <!-- Tags — horizontal scroll -->
    <div class="tags-section">
      <h3>Skills</h3>
      <div class="tags-list">
        <span class="tag">Python</span>
        <span class="tag">SQL</span>
        <span class="tag">Power BI</span>
        <span class="tag">Tableau</span>
        <span class="tag">Excel</span>
        <span class="tag">Machine Learning</span>
        <span class="tag">Statistics</span>
        <span class="tag">R</span>
        <span class="tag">Pandas</span>
        <span class="tag">Data Storytelling</span>
      </div>
    </div>

    <!-- Stats -->
    <div class="stats-section">
      <h3>Highlights</h3>
      <div class="stats-row">
        <div class="stat-box">
          <div class="stat-number">6+</div>
          <div class="stat-label">Years Exp.</div>
        </div>
        <div class="stat-box">
          <div class="stat-number">42</div>
          <div class="stat-label">Projects</div>
        </div>
        <div class="stat-box">
          <div class="stat-number">1.2k</div>
          <div class="stat-label">Followers</div>
        </div>
      </div>
    </div>

  </div><!-- end .card-body -->

  <!-- FOOTER -->
  <div class="card-footer">
    <a href="#" class="contact-btn">Contact Adaeze</a>
  </div>

</div><!-- end .profile-card -->

</body>
</html>
```

**Final Output:** A polished profile card featuring:
- A circular cropped avatar (thanks to `overflow: hidden` on the `.avatar-wrapper`)
- A bio area with a vertical scrollbar that appears when text overflows
- A skills tag list with a horizontal scrollbar for many tags
- Clean rounded card corners maintained by `overflow: hidden` on `.profile-card`

**Reflection Questions:**
- How many places in this project did you use overflow? Count them all.
- Which overflow value did you use most? Why?
- What would break if you removed `overflow: hidden` from `.profile-card`?
- What would happen to the bio if you changed `overflow-y: auto` to `overflow-y: hidden`?

**Optional Advanced Extensions:**
- Add a "Read more" toggle that removes the height limit on the bio when clicked (requires JavaScript)
- Add a photo gallery strip that scrolls horizontally below the stats
- Make the card responsive so it goes full-width on mobile screens

---

## Part 6 — Common Beginner Mistakes

### Mistake 1 — Using `overflow` Without Setting a Height

```css
/* WRONG — overflow has no effect without a height */
.box {
  width: 300px;
  /* No height set! */
  overflow: hidden;   /* This does nothing — content just makes the box taller */
}
```

```css
/* CORRECT */
.box {
  width: 300px;
  height: 150px;      /* Height must be set for overflow to work */
  overflow: hidden;
}
```

**Why this happens:** Without a height, block elements simply grow to fit their content. There is no overflow to manage. The `overflow` property only activates when the content is larger than the fixed box.

---

### Mistake 2 — Choosing `scroll` When `auto` Is Better

```css
/* WRONG — scrollbars always appear even when not needed */
.notification-box {
  height: 200px;
  overflow: scroll;   /* Empty state will show scrollbars — ugly! */
}
```

```css
/* CORRECT — scrollbars only appear when needed */
.notification-box {
  height: 200px;
  overflow: auto;     /* Clean when empty, scrollable when full */
}
```

**Why this matters:** `scroll` shows scrollbars permanently. When the box is empty or has little content, the scrollbars make the UI look cluttered and unprofessional.

---

### Mistake 3 — Trying to Set One Axis to `visible` With the Other to `hidden`

```css
/* PROBLEMATIC — browser will change overflow-y to 'auto' */
.box {
  overflow-x: hidden;
  overflow-y: visible;   /* Browser ignores this and makes it 'auto' */
}
```

```css
/* CORRECT — use 'clip' to achieve true clipping without a scroll container */
.box {
  overflow-x: clip;
  overflow-y: visible;   /* Now this works as expected */
}
```

**Why this happens:** `hidden`, `scroll`, and `auto` all create a scroll container. A scroll container cannot have `visible` overflow on one axis while being limited on the other. The `clip` value does not create a scroll container, so the limitation does not apply.

---

### Mistake 4 — Forgetting `white-space: nowrap` for Horizontal Overflow

```css
/* WRONG — text will wrap instead of overflowing horizontally */
.wide-content {
  width: 300px;
  overflow-x: scroll;   /* Scrollbar appears but content still wraps — no horizontal overflow */
}
```

```css
/* CORRECT — prevent wrapping so content actually overflows horizontally */
.wide-content {
  width: 300px;
  white-space: nowrap;  /* Forces content onto one line */
  overflow-x: scroll;   /* Now the horizontal scrollbar actually works */
}
```

**Why this happens:** Text naturally wraps when it hits the container edge. If it wraps, it overflows vertically (if at all), not horizontally. `white-space: nowrap` prevents wrapping so text can overflow horizontally.

---

### Mistake 5 — Using `overflow: hidden` on the Wrong Element

```css
/* WRONG — hiding overflow on body can prevent page scrolling */
body {
  overflow: hidden;   /* The entire page is now unscrollable! */
}
```

```css
/* CORRECT — apply overflow to the specific element that needs it */
.modal-content {
  overflow: hidden;   /* Only this specific box clips its content */
}
```

**Why this matters:** Applying `overflow: hidden` to `<html>` or `<body>` removes the ability to scroll the entire page. This is sometimes done intentionally (to trap scroll inside a modal dialog) but is a very common accidental mistake.

---

## Part 7 — Reflection Questions

Think carefully about each question. Write your answers in your notes before moving on:

1. What is the default value of the `overflow` property? What does it do?
2. What is the difference between `overflow: scroll` and `overflow: auto`? When would you choose each?
3. You have a `<div>` with `height: 200px` and lots of text. You want users to scroll to read all the text, but no scrollbar should appear when the text is short. Which value would you use?
4. What must be true for the `overflow` property to have any effect on a block element?
5. You are building a wide data table that users need to scroll horizontally. Which property and value combination would you use: `overflow: scroll` or `overflow-x: auto`? What is the advantage of your choice?
6. What is the difference between `overflow: hidden` and `overflow: clip`?
7. A colleague sets `overflow-x: hidden` and `overflow-y: visible` on the same element. They complain it does not work as expected. What is happening and how would you fix it?
8. Name two real-world UI components that rely on `overflow: hidden` for their appearance.
9. What CSS property must you often combine with `overflow-x: scroll` to ensure the content does not just wrap to the next line?
10. Where in the Profile Card mini-project was `overflow: hidden` used for a visual/design purpose (not just content management)? Explain what it achieves.

---

## Lesson Completion Checklist

Before moving to the next lesson, confirm you can answer "yes" to each item:

- [ ] I understand what CSS overflow is and when it occurs
- [ ] I can explain all five `overflow` values: `visible`, `hidden`, `scroll`, `auto`, `clip`
- [ ] I know the difference between `overflow: scroll` and `overflow: auto`
- [ ] I understand that `overflow` requires a set `height` to work on block elements
- [ ] I can use `overflow-x` and `overflow-y` separately
- [ ] I know the quirk about mixing `visible` with `hidden`/`scroll`/`auto` on different axes
- [ ] I know when to use `overflow: clip` instead of `overflow: hidden`
- [ ] I built all four practice exercises successfully
- [ ] I completed the Profile Card mini-project
- [ ] I can name at least three common beginner mistakes and how to avoid them
- [ ] I can answer the reflection questions above

---

## Lesson Summary

The CSS `overflow` property gives you full control over what happens when content is too large to fit inside an element's box.

The five values are:

- **`visible`** — the default; content spills outside the box and is fully visible but does not affect page flow
- **`hidden`** — content is cleanly clipped at the box edge; nothing shows outside; no scrollbar
- **`scroll`** — scrollbars are always added (both horizontal and vertical) regardless of whether content overflows
- **`auto`** — the smart choice; scrollbars only appear in the direction where content actually overflows
- **`clip`** — clips content like `hidden` but does not create a scroll container, enabling advanced directional control

The individual properties `overflow-x` and `overflow-y` let you control each axis independently — a powerful technique for data tables, tag lists, and chat windows.

The shorthand `overflow` accepts two values (e.g., `overflow: hidden auto`) where the first applies to the horizontal axis and the second to the vertical axis.

Remember these rules:
- `overflow` only works on block elements with a set `height`
- Prefer `auto` over `scroll` in most real-world situations
- Use `clip` when you need true directional clipping without a scroll container
- Combine `white-space: nowrap` with `overflow-x` to enable horizontal scrolling for text content

In the next lesson, you will study **CSS Float** — another important layout property that controls how elements position themselves alongside other content.

---

*Sources: W3Schools CSS Overflow Tutorial, W3Schools CSS Overflow-X and Overflow-Y Reference, MDN Web Docs CSS Overflow, CSS-Tricks Overflow Almanac, freeCodeCamp CSS Overflow Guide, Kilian Valkhof — Do you know about overflow: clip?*
