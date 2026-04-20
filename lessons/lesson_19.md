---
render_with_liquid: false
title: "CSS Display — Block, Inline, Inline-Block, None & Visibility"
nav_order: 19
---

# Lesson 19: CSS Display — Block, Inline, Inline-Block, None & Visibility

---

## Lesson Introduction

Welcome to Lesson 19! This lesson is about one of the **most fundamental and powerful** properties in all of CSS — the `display` property.

Every single element on a webpage has a display type. It controls **how elements sit on the page** — whether they stack on top of each other, sit side by side, or disappear from the page entirely.

Understanding `display` is the key that unlocks almost all layout work in CSS. When something looks wrong on your page — an element wrapping unexpectedly, two things not sitting next to each other, a gap where you don't want one — the `display` property is almost always involved.

By the end of this lesson, you will be able to:
- Explain what the `display` property does and why it exists
- Understand the difference between **block** and **inline** elements
- Use `display: block`, `display: inline`, and `display: inline-block`
- Use `display: none` to completely remove elements from the page
- Use `visibility: hidden` to hide elements while keeping their space
- Know when to use `display: none` vs `visibility: hidden`
- Build a real-world navigation bar using display manipulation
- Apply display changes to show and hide content dynamically

---

## Prerequisite Concepts

### What Is an HTML Element?

An **HTML element** is a piece of content on a webpage wrapped in tags. For example:

```html
<p>This is a paragraph.</p>
<span>This is a span.</span>
<div>This is a div.</div>
```

Each of these elements has a **default display type** built into the browser. You didn't have to write any CSS — the browser already decided whether it stacks vertically or sits inline. The `display` property lets you **override** that default.

### What Does "Layout" Mean?

**Layout** is how elements are positioned and sized on the page. When you load a webpage, the browser reads your HTML and CSS from top to bottom, then decides:
- Where does each element start?
- How wide is it?
- Does it force the next element onto a new line?

The `display` property is the #1 tool that controls all of these decisions.

---

## Part 1: The `display` Property — What It Is and Why It Exists

### The Core Idea

Think of a webpage like a newspaper. Some content is laid out in **big full-width blocks** (like article headlines — they take the whole row). Other content **flows within a line of text** (like bold words or hyperlinks — they sit inside a sentence without breaking it).

CSS uses the same two ideas:
- **Block** — like a paragraph. Takes the full width. Starts on a new line.
- **Inline** — like a bold word. Only takes as much space as it needs. Sits inside a line.

The `display` property is how CSS controls this.

### Every HTML Element Has a Default Display Value

The browser has built-in defaults for every HTML element. You can see this clearly:

**Elements that default to `block`:**
`<div>`, `<p>`, `<h1>` through `<h6>`, `<ul>`, `<ol>`, `<li>`, `<form>`, `<header>`, `<footer>`, `<section>`, `<article>`, `<nav>`, `<main>`, `<aside>`, `<blockquote>`, `<hr>`, `<table>`

**Elements that default to `inline`:**
`<span>`, `<a>`, `<strong>`, `<em>`, `<b>`, `<i>`, `<u>`, `<img>`, `<input>`, `<button>`, `<label>`, `<code>`, `<abbr>`

You can completely change an element's default behaviour using the `display` property.

---

## Part 2: `display: block`

### What Is a Block Element?

A **block element** behaves like a full-width bar. Here is exactly what it does:

1. It **starts on a new line** — nothing can sit to its left or right
2. It **stretches to fill the full available width** (unless you set a specific width)
3. It **respects `width`, `height`, `padding`, `margin`, and `border`** in all directions

**Analogy:** Imagine laying bricks in a single column. Each brick takes the full width of the wall and the next brick always goes below the previous one. That is how block elements work.

### Quick Visual Demo

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .box {
      background-color: steelblue;
      color: white;
      padding: 10px;
      margin: 5px 0;
    }
  </style>
</head>
<body>
  <div class="box">Block 1</div>
  <div class="box">Block 2</div>
  <div class="box">Block 3</div>
</body>
</html>
```

**Expected Visual Output:**
Three full-width blue bars stacked vertically, each on its own line:

```
[========== Block 1 ==========]
[========== Block 2 ==========]
[========== Block 3 ==========]
```

### Forcing an Inline Element to Become Block

By default, `<a>` (links) are inline. You can force them to be block-level with `display: block`:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    a {
      display: block;
      background-color: #e8f0fe;
      padding: 10px 15px;
      margin: 5px 0;
      text-decoration: none;
      color: #333;
      border: 1px solid #ccc;
    }
  </style>
</head>
<body>
  <a href="#">Home</a>
  <a href="#">About</a>
  <a href="#">Contact</a>
</body>
</html>
```

**Expected Visual Output:**
Three links stacked vertically, each taking the full width — like a vertical menu.

```
[Home        ]
[About       ]
[Contact     ]
```

> **Why is this useful?** Navigation menus, buttons that span the full width, and list items in a sidebar are all built this way.

### Line-by-Line Explanation

- `display: block;` — This tells the browser: "treat this `<a>` tag as if it were a `<div>`." It now starts on its own line and expands to full width.
- `padding: 10px 15px;` — Adds space inside the link so it looks like a proper button/menu item.
- `margin: 5px 0;` — Adds a small gap between each link vertically.

> **Thinking Prompt:** What happens if you remove `display: block` from these links? They will all collapse onto one line next to each other, as inline elements do by default.

---

## Part 3: `display: inline`

### What Is an Inline Element?

An **inline element** flows within text. Here is exactly what it does:

1. It **does NOT start on a new line** — it sits next to other inline elements
2. It **only takes up as much width as its content** — no more
3. It **ignores `width` and `height`** settings
4. It **respects horizontal padding and margin** but vertical padding/margin is unreliable

**Analogy:** Think of words in a sentence. The word "hello" does not start a new line — it just sits next to the words before and after it. Inline elements work the same way.

### Quick Visual Demo — Default Inline Behaviour

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    span {
      background-color: #ffe57f;
      padding: 4px;
    }
  </style>
</head>
<body>
  <p>
    This is a sentence with a
    <span>highlighted word</span>
    right in the middle of it.
  </p>
</body>
</html>
```

**Expected Visual Output:**
The `<span>` sits inside the sentence, highlighted in yellow — it does NOT break onto its own line.

```
This is a sentence with a [highlighted word] right in the middle of it.
```

### Forcing a Block Element to Become Inline

By default, `<li>` (list items) are block-level. You can make them sit side by side with `display: inline`:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    li {
      display: inline;
      padding: 0 15px;
      list-style: none;
      background-color: #3366cc;
      color: white;
    }
  </style>
</head>
<body>
  <ul>
    <li>Home</li>
    <li>Products</li>
    <li>Services</li>
    <li>Contact</li>
  </ul>
</body>
</html>
```

**Expected Visual Output:**
All four list items appear on the same horizontal line:

```
[Home] [Products] [Services] [Contact]
```

> **Real-world use:** This is exactly how horizontal navigation bars are built! Making `<li>` items `display: inline` is a classic and fundamental technique.

### The Limitation of `display: inline`

A key limitation: **you cannot control `width` or `height` on inline elements**. If you set `width: 200px` on a `<span>`, it is simply ignored.

```css
span {
  display: inline;
  width: 200px;  /* This will be IGNORED */
  height: 50px;  /* This will also be IGNORED */
}
```

This is where `display: inline-block` saves the day.

---

## Part 4: `display: inline-block`

### The Best of Both Worlds

`display: inline-block` is a hybrid. It gives you:
- **Inline behaviour:** Elements sit next to each other on the same line
- **Block behaviour:** You CAN set `width`, `height`, `padding`, and `margin` in all directions

**Analogy:** Think of `inline-block` like stamps in a row. Each stamp has a fixed, controlled size, but they all sit side by side without stacking vertically.

### Comparison: `inline` vs `inline-block` vs `block`

| Property | `inline` | `inline-block` | `block` |
|---|---|---|---|
| Starts on new line? | No | No | Yes |
| Sits next to others? | Yes | Yes | No |
| Respects `width`/`height`? | No | **Yes** | Yes |
| Respects all margins? | Partially | Yes | Yes |
| Takes full width by default? | No | No | Yes |

### Simple Example — Inline Elements With Dimensions

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .box {
      display: inline-block;
      width: 120px;
      height: 80px;
      background-color: coral;
      color: white;
      text-align: center;
      line-height: 80px; /* vertically centres text */
      margin: 5px;
    }
  </style>
</head>
<body>
  <div class="box">Box 1</div>
  <div class="box">Box 2</div>
  <div class="box">Box 3</div>
</body>
</html>
```

**Expected Visual Output:**
Three equal-sized coral coloured squares sitting side by side on the same row:

```
[  Box 1  ] [  Box 2  ] [  Box 3  ]
(120x80px)  (120x80px)  (120x80px)
```

Without `display: inline-block`, these `<div>` elements would stack vertically (because `<div>` is block by default). With `inline-block`, they sit side by side and still respect their fixed dimensions.

### Real-World Example — A Navigation Bar with `inline-block`

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    nav ul {
      list-style: none;
      padding: 0;
      margin: 0;
      background-color: #222;
    }

    nav ul li {
      display: inline-block;
    }

    nav ul li a {
      display: block;
      padding: 14px 20px;
      color: white;
      text-decoration: none;
    }

    nav ul li a:hover {
      background-color: #555;
    }
  </style>
</head>
<body>
  <nav>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">About</a></li>
      <li><a href="#">Services</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  </nav>
</body>
</html>
```

**Expected Visual Output:**
A dark horizontal navigation bar with four clickable links side by side. Each link lights up grey on hover.

```
[Home]  [About]  [Services]  [Contact]     (dark background)
```

> **Thinking Prompt:** Why do we set `display: inline-block` on the `<li>` AND `display: block` on the `<a>` inside it? The `<li>` goes inline so items sit side by side. The `<a>` goes block so its click area fills the entire `<li>` space — making the whole box clickable, not just the text.

### `inline-block` for Card Grids

`inline-block` is also used to create grid-like card layouts:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .card {
      display: inline-block;
      width: 180px;
      padding: 15px;
      margin: 10px;
      border: 1px solid #ccc;
      border-radius: 6px;
      vertical-align: top; /* aligns cards by their top edges */
      background-color: #f9f9f9;
    }

    .card h3 {
      margin: 0 0 8px 0;
      font-size: 16px;
    }

    .card p {
      margin: 0;
      font-size: 13px;
      color: #666;
    }
  </style>
</head>
<body>
  <div class="card">
    <h3>Card A</h3>
    <p>Short description for this card.</p>
  </div>
  <div class="card">
    <h3>Card B</h3>
    <p>A slightly longer description that wraps over two lines.</p>
  </div>
  <div class="card">
    <h3>Card C</h3>
    <p>Another description here.</p>
  </div>
</body>
</html>
```

**Expected Visual Output:**
Three card boxes sitting side by side, each 180px wide, aligned by their top edges.

> **Note on `vertical-align: top`:** When `inline-block` elements have different heights, they align at their bottom edges by default. Adding `vertical-align: top` aligns them at the top — much better for cards.

---

## Part 5: `display: none` — Completely Removing Elements

### What Does `display: none` Do?

`display: none` **completely removes an element from the page**. It is as if the element does not exist at all:
- It takes up **no space**
- It is **invisible**
- Other elements move in to fill the space it would have occupied
- The HTML code is still there in the file — it just is not rendered

**Analogy:** Imagine you wrote a word on a piece of paper and then used correction fluid (whiteout) to cover it. The underlying word is still there on the paper — but visually it is gone and the words after it have moved to fill the gap.

### Simple Example — Hiding a Paragraph

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      background-color: #dff0d8;
      padding: 10px;
      margin: 5px 0;
      border: 1px solid #ccc;
    }

    .hidden {
      display: none;
    }
  </style>
</head>
<body>
  <p>Paragraph 1 — I am visible.</p>
  <p class="hidden">Paragraph 2 — I am HIDDEN! (display: none)</p>
  <p>Paragraph 3 — I am visible.</p>
</body>
</html>
```

**Expected Visual Output:**
Only paragraphs 1 and 3 appear. Paragraph 2 is completely gone — paragraph 3 moves up as if paragraph 2 was never there.

```
[Paragraph 1 — I am visible.  ]
[Paragraph 3 — I am visible.  ]
```

### Real-World Use: Toggling Content with JavaScript

The most common real-world use of `display: none` is toggling content visibility with JavaScript. Here is a complete working example:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    #secret-message {
      display: none; /* hidden by default */
      background-color: #fff3cd;
      border: 1px solid #ffc107;
      padding: 15px;
      margin-top: 10px;
      border-radius: 4px;
    }

    button {
      padding: 10px 20px;
      background-color: #3366cc;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 14px;
    }

    button:hover {
      background-color: #254ea6;
    }
  </style>
</head>
<body>
  <button onclick="toggleMessage()">Show / Hide Message</button>

  <div id="secret-message">
    <strong>Surprise!</strong> This message was hidden. Now you can see it!
  </div>

  <script>
    function toggleMessage() {
      var msg = document.getElementById("secret-message");
      if (msg.style.display === "none" || msg.style.display === "") {
        msg.style.display = "block";
      } else {
        msg.style.display = "none";
      }
    }
  </script>
</body>
</html>
```

**Expected Visual Output:**
- On page load: Only the button is visible
- After clicking the button: A yellow message box appears below
- After clicking again: The message disappears

> **Don't worry if the JavaScript is new to you!** The CSS part (`display: none` / `display: block`) is what matters here. JavaScript is just flipping the display value back and forth. This pattern is used on almost every modern website.

### `display: none` vs. `display: block` Toggling Pattern

This is the core pattern used by accordions, dropdowns, modals, and tabs on real websites:

```css
/* Default: element is hidden */
.panel {
  display: none;
}

/* When "active" class is added by JavaScript */
.panel.active {
  display: block;
}
```

---

## Part 6: `visibility: hidden` — Hiding Without Removing Space

### What Does `visibility: hidden` Do?

`visibility: hidden` makes an element **invisible** but it **still takes up its original space on the page**. Other elements do NOT move to fill its gap.

| Property | Element Visible? | Takes Up Space? |
|---|---|---|
| `display: none` | No | **No** — space is removed |
| `visibility: hidden` | No | **Yes** — space remains |

**Analogy:** Imagine a reserved seat at a cinema. `display: none` is like removing the seat entirely — the row gets shorter. `visibility: hidden` is like the seat being there but draped with a cloth — you can't see it, but it still occupies space. Nobody sits in it.

### Direct Side-by-Side Comparison

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .box {
      display: inline-block;
      width: 100px;
      height: 60px;
      background-color: steelblue;
      color: white;
      text-align: center;
      line-height: 60px;
      margin: 5px;
    }

    .display-none {
      display: none;
    }

    .vis-hidden {
      visibility: hidden;
    }
  </style>
</head>
<body>
  <h3>With display: none (Box 2 removed):</h3>
  <div class="box">Box 1</div>
  <div class="box display-none">Box 2</div>
  <div class="box">Box 3</div>

  <h3>With visibility: hidden (Box 2 invisible but space kept):</h3>
  <div class="box">Box 1</div>
  <div class="box vis-hidden">Box 2</div>
  <div class="box">Box 3</div>
</body>
</html>
```

**Expected Visual Output:**

First row — `display: none`:
```
[Box 1]         [Box 3]
       ^ gap closed — Box 3 moved left
```

Second row — `visibility: hidden`:
```
[Box 1]  [     ]  [Box 3]
          ^ Box 2 is invisible but its space is still reserved
```

This is the key visual difference between the two techniques.

### When to Use Each

**Use `display: none` when:**
- You want the element completely gone from the layout
- You are toggling menus, modals, tabs, or accordions
- You want surrounding elements to fill in the space
- You are making a responsive layout where certain elements don't exist on mobile

**Use `visibility: hidden` when:**
- You want to hide an element but preserve the layout spacing around it
- You have a table or grid where removing cells would break alignment
- You want a "placeholder" element that keeps its space but is temporarily invisible
- Animating opacity (combined with `opacity: 0` for smooth transitions)

### `visibility` Values

The `visibility` property has three values:

| Value | Effect |
|---|---|
| `visible` | The element is visible (this is the default) |
| `hidden` | The element is invisible but still takes up space |
| `collapse` | For table rows/columns: removes them without affecting table layout |

```css
.element { visibility: visible; }  /* Default — visible */
.element { visibility: hidden; }   /* Invisible but space preserved */
```

### Combining `display: none` with Responsive Design

A very common real-world pattern is hiding navigation menus on mobile:

```css
/* Mobile: hide the desktop nav */
.desktop-nav {
  display: none;
}

/* On screens wider than 768px: show the desktop nav */
@media (min-width: 768px) {
  .desktop-nav {
    display: block;
  }
}
```

This is how websites show a hamburger menu on phones but a full navigation bar on desktops.

---

## Part 7: Other `display` Values (Quick Overview)

The `display` property has several more values worth knowing. These will each get their own detailed lessons, but here is a quick introduction so nothing surprises you:

### `display: flex`

Turns an element into a **flex container**. All its children can be arranged in rows or columns with powerful alignment tools.

```css
.container {
  display: flex;
  justify-content: space-between; /* distributes children evenly */
}
```

### `display: grid`

Turns an element into a **grid container**. Children can be arranged in both rows AND columns simultaneously.

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* 3 equal columns */
}
```

### `display: table`

Makes a non-table element behave like a `<table>`.

```css
.fake-table {
  display: table;
}
```

### `display: list-item`

Makes an element behave like a `<li>` — adds a bullet point marker.

```css
span {
  display: list-item;
  margin-left: 20px;
}
```

> **Focus for this lesson:** `block`, `inline`, `inline-block`, and `none`. These are the four you will use daily. `flex` and `grid` are covered in depth in their own lessons.

---

## Guided Practice Exercises

### Exercise 1 — Block vs Inline Observation

**Objective:** See and feel the difference between block and inline behaviour.

**Scenario:** You are building a simple recipe page. Ingredients are listed with `<span>` elements but they need to stack vertically for readability on mobile.

**Steps:**

1. Create an HTML file with five `<span>` elements, each containing an ingredient name.
2. Style them with a light background and padding.
3. Notice how they all sit on one line (inline default).
4. Now add `display: block;` to the span style.
5. Notice how they now each take their own line.

**Starting code:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    span.ingredient {
      background-color: #e8f5e9;
      padding: 6px 12px;
      border: 1px solid #a5d6a7;
      border-radius: 4px;
      margin: 4px;
      /* Try adding display: block; here */
    }
  </style>
</head>
<body>
  <h2>Ingredients</h2>
  <span class="ingredient">2 cups flour</span>
  <span class="ingredient">1 tsp salt</span>
  <span class="ingredient">3 eggs</span>
  <span class="ingredient">1 cup milk</span>
  <span class="ingredient">2 tbsp butter</span>
</body>
</html>
```

**Step A — Expected output (no `display: block`):**
All ingredients on one line (may wrap if the screen is narrow).

**Step B — Expected output (with `display: block`):**
```
[2 cups flour  ]
[1 tsp salt    ]
[3 eggs        ]
[1 cup milk    ]
[2 tbsp butter ]
```

**Self-check Questions:**
- Why do `<span>` elements sit on one line without `display: block`?
- What happened to the spacing when you added `display: block`?
- Can you set `width: 300px` on a `<span>` with and without `display: block`? What changes?

---

### Exercise 2 — Building a Horizontal Navigation

**Objective:** Use `display: inline` to convert a vertical list into a horizontal nav bar.

**Scenario:** Your website has a list of navigation links. By default the `<li>` items stack vertically. You want them side by side.

**Steps:**

1. Create an unordered list with 4 navigation links.
2. Remove the bullet points with `list-style: none`.
3. Add `display: inline` to the `<li>` elements.
4. Style the links to look like nav items.

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
    }

    ul.nav {
      list-style: none;
      padding: 0;
      margin: 0;
      background-color: #2c3e50;
    }

    ul.nav li {
      display: inline;  /* KEY CHANGE: list items go horizontal */
    }

    ul.nav li a {
      display: inline-block;
      padding: 14px 22px;
      color: #ecf0f1;
      text-decoration: none;
      font-size: 14px;
    }

    ul.nav li a:hover {
      background-color: #34495e;
    }
  </style>
</head>
<body>
  <ul class="nav">
    <li><a href="#">Home</a></li>
    <li><a href="#">Portfolio</a></li>
    <li><a href="#">Blog</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</body>
</html>
```

**Expected Visual Output:**
A dark horizontal navigation bar with four links side by side.

```
[Home]  [Portfolio]  [Blog]  [Contact]     (dark background)
```

**Self-check Questions:**
- What happens if you remove `display: inline` from the `<li>` elements?
- Why did we use `display: inline-block` on the `<a>` tags instead of `display: inline`?
- What would happen if you gave `<a>` a width setting but it was `display: inline`?

---

### Exercise 3 — Show and Hide a Panel

**Objective:** Use `display: none` and `display: block` to toggle a content panel.

**Scenario:** You are building an FAQ section. Each answer should be hidden by default and revealed when clicked.

**Steps:**

1. Create a question heading and an answer paragraph.
2. Set the answer to `display: none` initially.
3. Add a button that toggles the answer's visibility using JavaScript.

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .faq-item {
      border: 1px solid #ddd;
      border-radius: 6px;
      margin: 10px 0;
      overflow: hidden;
    }

    .faq-question {
      background-color: #f7f7f7;
      padding: 14px 16px;
      cursor: pointer;
      font-weight: bold;
      display: flex;
      justify-content: space-between;
    }

    .faq-question:hover {
      background-color: #eaeaea;
    }

    .faq-answer {
      display: none; /* hidden by default */
      padding: 14px 16px;
      background-color: #fff;
      color: #444;
      border-top: 1px solid #ddd;
      line-height: 1.6;
    }
  </style>
</head>
<body>
  <h2>Frequently Asked Questions</h2>

  <div class="faq-item">
    <div class="faq-question" onclick="toggleAnswer(this)">
      What is CSS? <span>+</span>
    </div>
    <div class="faq-answer">
      CSS stands for Cascading Style Sheets. It is used to control the
      visual appearance of HTML elements — things like colour, font size,
      spacing, and layout.
    </div>
  </div>

  <div class="faq-item">
    <div class="faq-question" onclick="toggleAnswer(this)">
      Why is the display property important? <span>+</span>
    </div>
    <div class="faq-answer">
      The display property controls how elements are arranged on the page.
      It determines whether an element takes a full row (block), sits inline
      with text, or is removed from the layout entirely.
    </div>
  </div>

  <script>
    function toggleAnswer(questionElement) {
      var answer = questionElement.nextElementSibling;
      if (answer.style.display === "block") {
        answer.style.display = "none";
      } else {
        answer.style.display = "block";
      }
    }
  </script>
</body>
</html>
```

**Expected Visual Output:**
- On load: Two FAQ question bars visible; answers hidden
- After clicking a question: Its answer slides open below
- After clicking again: Answer hides

**Self-check Questions:**
- What property starts each answer as invisible?
- If you replaced `display: none` with `visibility: hidden`, would the answers still appear to "collapse"? What would change?

**What-if challenge:** Can you make both answers open at the same time? (Yes — each button controls its own sibling answer independently.)

---

## Mini Project: "Interactive Profile Page with Show/Hide Sections"

### Project Goal

Build a profile page that uses all the display techniques from this lesson:
- A horizontal nav bar using `display: inline-block`
- Profile cards using `display: inline-block`
- Collapsible "bio" sections using `display: none`/`display: block` toggling
- A footer using `display: block` elements

### Stage 1 — Horizontal Navigation

```html
<!DOCTYPE html>
<html>
<head>
  <title>My Profile</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: Arial, sans-serif; background: #f4f4f4; color: #333; }

    /* Navigation */
    nav {
      background-color: #1a1a2e;
    }

    nav ul {
      list-style: none;
      padding: 0;
      margin: 0;
    }

    nav ul li {
      display: inline-block; /* Horizontal layout */
    }

    nav ul li a {
      display: block;
      padding: 16px 24px;
      color: #eee;
      text-decoration: none;
      font-size: 14px;
      letter-spacing: 0.5px;
    }

    nav ul li a:hover {
      background-color: #16213e;
      color: #4fc3f7;
    }
  </style>
</head>
<body>
  <nav>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">Projects</a></li>
      <li><a href="#">Skills</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  </nav>
</body>
</html>
```

**Milestone Output:** A dark professional navigation bar with four horizontally aligned links.

---

### Stage 2 — Profile Cards Using `inline-block`

Add inside `<body>` after the nav:

```html
<section style="padding: 40px; text-align: center;">
  <h1 style="margin-bottom: 30px;">Meet the Team</h1>

  <div class="profile-card">
    <div class="avatar" style="background-color: #4fc3f7;"></div>
    <h3>Alex Kim</h3>
    <p>Lead Developer</p>
    <button onclick="toggleBio('bio1')">View Bio</button>
    <p class="bio" id="bio1">
      Alex has 8 years of experience building scalable web applications.
      Passionate about clean code and great user experiences.
    </p>
  </div>

  <div class="profile-card">
    <div class="avatar" style="background-color: #f48fb1;"></div>
    <h3>Jordan Lee</h3>
    <p>UI/UX Designer</p>
    <button onclick="toggleBio('bio2')">View Bio</button>
    <p class="bio" id="bio2">
      Jordan creates intuitive, beautiful interfaces. Believes that
      great design is invisible — it just works.
    </p>
  </div>

  <div class="profile-card">
    <div class="avatar" style="background-color: #a5d6a7;"></div>
    <h3>Morgan Chen</h3>
    <p>Data Scientist</p>
    <button onclick="toggleBio('bio3')">View Bio</button>
    <p class="bio" id="bio3">
      Morgan transforms raw data into meaningful insights that drive
      product decisions and business strategy.
    </p>
  </div>
</section>
```

Add the card styles:

```css
.profile-card {
  display: inline-block;     /* Cards sit side by side */
  vertical-align: top;
  width: 220px;
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 10px;
  padding: 20px;
  margin: 10px;
  text-align: center;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}

.profile-card .avatar {
  width: 70px;
  height: 70px;
  border-radius: 50%;
  margin: 0 auto 12px;
}

.profile-card h3 {
  margin: 0 0 4px;
  font-size: 16px;
}

.profile-card p {
  color: #777;
  font-size: 13px;
  margin: 0 0 10px;
}

.profile-card button {
  padding: 7px 14px;
  background-color: #1a1a2e;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 12px;
  margin-bottom: 10px;
}

.profile-card button:hover {
  background-color: #16213e;
}

.bio {
  display: none;   /* Hidden by default */
  font-size: 12px;
  color: #555;
  line-height: 1.5;
  text-align: left;
  background-color: #f9f9f9;
  padding: 10px;
  border-radius: 4px;
  margin-top: 8px;
}
```

---

### Stage 3 — The Toggle Script

Add before `</body>`:

```html
<script>
  function toggleBio(id) {
    var bio = document.getElementById(id);
    if (bio.style.display === "block") {
      bio.style.display = "none";
    } else {
      bio.style.display = "block";
    }
  }
</script>
```

---

### Stage 4 — Complete Final Code

```html
<!DOCTYPE html>
<html>
<head>
  <title>Team Profile Page</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: Arial, sans-serif; background: #f4f4f4; color: #333; }

    nav { background-color: #1a1a2e; }
    nav ul { list-style: none; }
    nav ul li { display: inline-block; }
    nav ul li a {
      display: block;
      padding: 16px 24px;
      color: #eee;
      text-decoration: none;
      font-size: 14px;
    }
    nav ul li a:hover { background-color: #16213e; color: #4fc3f7; }

    section { padding: 40px; text-align: center; }
    section h1 { margin-bottom: 30px; font-size: 24px; }

    .profile-card {
      display: inline-block;
      vertical-align: top;
      width: 220px;
      background-color: white;
      border: 1px solid #ddd;
      border-radius: 10px;
      padding: 20px;
      margin: 10px;
      text-align: center;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
    }

    .profile-card .avatar {
      width: 70px;
      height: 70px;
      border-radius: 50%;
      margin: 0 auto 12px;
    }

    .profile-card h3 { margin: 0 0 4px; font-size: 16px; }
    .profile-card > p { color: #777; font-size: 13px; margin: 0 0 10px; }

    .profile-card button {
      padding: 7px 14px;
      background-color: #1a1a2e;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 12px;
      margin-bottom: 10px;
    }
    .profile-card button:hover { background-color: #16213e; }

    .bio {
      display: none;
      font-size: 12px;
      color: #555;
      line-height: 1.5;
      text-align: left;
      background-color: #f9f9f9;
      padding: 10px;
      border-radius: 4px;
      margin-top: 8px;
    }

    footer {
      display: block;
      background-color: #1a1a2e;
      color: #aaa;
      text-align: center;
      padding: 20px;
      font-size: 13px;
      margin-top: 30px;
    }
  </style>
</head>
<body>

  <nav>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">Projects</a></li>
      <li><a href="#">Skills</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  </nav>

  <section>
    <h1>Meet the Team</h1>

    <div class="profile-card">
      <div class="avatar" style="background-color: #4fc3f7;"></div>
      <h3>Alex Kim</h3>
      <p>Lead Developer</p>
      <button onclick="toggleBio('bio1')">View Bio</button>
      <p class="bio" id="bio1">
        Alex has 8 years of experience building scalable web applications.
        Passionate about clean code and great user experiences.
      </p>
    </div>

    <div class="profile-card">
      <div class="avatar" style="background-color: #f48fb1;"></div>
      <h3>Jordan Lee</h3>
      <p>UI/UX Designer</p>
      <button onclick="toggleBio('bio2')">View Bio</button>
      <p class="bio" id="bio2">
        Jordan creates intuitive, beautiful interfaces. Believes that
        great design is invisible — it just works.
      </p>
    </div>

    <div class="profile-card">
      <div class="avatar" style="background-color: #a5d6a7;"></div>
      <h3>Morgan Chen</h3>
      <p>Data Scientist</p>
      <button onclick="toggleBio('bio3')">View Bio</button>
      <p class="bio" id="bio3">
        Morgan transforms raw data into meaningful insights that drive
        product decisions and business strategy.
      </p>
    </div>
  </section>

  <footer>
    &copy; 2025 Team Profile Page. All rights reserved.
  </footer>

  <script>
    function toggleBio(id) {
      var bio = document.getElementById(id);
      if (bio.style.display === "block") {
        bio.style.display = "none";
      } else {
        bio.style.display = "block";
      }
    }
  </script>

</body>
</html>
```

**Final Output:** A complete team profile page with a dark horizontal navigation bar, three profile cards side by side, expandable bio sections, and a footer.

**Reflection Questions:**
- The nav bar uses `display: inline-block` on `<li>` — why not just `display: inline`?
- What happens visually when you click "View Bio" on one card and then another?
- Change `.bio` from `display: none` to `visibility: hidden`. How does the card layout change?
- Why does the footer use `display: block` explicitly even though `<footer>` is already block by default?

**Optional Extensions:**
- Change the "View Bio" button text to "Hide Bio" when the bio is open, and back to "View Bio" when closed
- Add `transition: all 0.3s ease;` to `.bio` — does anything change? (Hint: transitions don't work on `display`. This is a common limitation.)
- Use `visibility: hidden` and `opacity: 0` together with a CSS transition for a smooth fade effect instead

---

## Common Beginner Mistakes

### Mistake 1: Setting `width` or `height` on a pure `inline` element

**Wrong:**

```css
span {
  display: inline;
  width: 200px;   /* IGNORED on inline elements */
  height: 50px;   /* IGNORED on inline elements */
}
```

**Fix:** Use `display: inline-block` if you need dimensions:

```css
span {
  display: inline-block; /* Now width and height work */
  width: 200px;
  height: 50px;
}
```

---

### Mistake 2: Confusing `display: none` with `visibility: hidden`

**Wrong thinking:** "Both hide the element, so they are the same."

**Reality:** They are very different:

```css
/* Removes element completely — other content moves in */
.gone { display: none; }

/* Invisible but the SPACE is still there — other content stays put */
.invisible { visibility: hidden; }
```

---

### Mistake 3: Forgetting that `<li>` items have default `display: list-item`

```css
li {
  display: inline; /* Works, but also removes the bullet point */
}
```

When you change `<li>` to `display: inline`, the bullet marker disappears automatically. If you want the bullet to stay, you cannot use `display: inline`. Use `list-style: none` explicitly when you do not want bullets.

---

### Mistake 4: Not removing bullet points when making horizontal nav

**Wrong (looks messy — bullets appear):**

```css
li {
  display: inline;
  /* Forgot to remove bullets! */
}
```

**Correct:**

```css
ul {
  list-style: none; /* Removes bullets from the whole list */
  padding: 0;
  margin: 0;
}

li {
  display: inline;
}
```

---

### Mistake 5: Using `display: none` to "style" something instead of CSS

**Wrong approach:** Hiding all elements and only showing one — instead of simply writing CSS for the one you want:

```css
/* Don't do this when CSS can solve the visual problem */
.red-version { display: none; }
.blue-version { display: block; }
```

`display: none` is for **dynamic behaviour** (toggling with JavaScript) or **responsive design**, not for choosing between two static designs.

---

### Mistake 6: Expecting `display: none` to remove something from screen readers

**Wrong assumption:** "`display: none` hides content from everyone."

**Reality:** `display: none` does remove content from screen readers too. But if you want content to be **visually hidden but still accessible to screen readers**, use this pattern instead:

```css
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  overflow: hidden;
  clip: rect(0,0,0,0);
  white-space: nowrap;
}
```

This is an accessibility technique used for things like icon button labels that sighted users don't need to see but screen-reader users do.

---

### Mistake 7: The `inline-block` whitespace gap

When you write `inline-block` elements in separate lines of HTML, a small whitespace gap appears between them. This is because the space (or newline) between HTML tags is rendered as a text space character.

**HTML that causes a gap:**

```html
<div class="box">Box 1</div>
<div class="box">Box 2</div>
<div class="box">Box 3</div>
```

**The gap appears because the newline between `</div>` and `<div>` is treated as a space.**

**Quick fixes:**

```css
/* Fix 1: Set font-size to 0 on the parent */
.parent {
  font-size: 0;
}
.box {
  display: inline-block;
  font-size: 16px; /* Reset font size on children */
}

/* Fix 2: Use negative margin (less clean) */
.box {
  display: inline-block;
  margin-right: -4px;
}
```

> **Note:** Flexbox (`display: flex`) does not have this whitespace gap problem, which is one reason modern layouts prefer it over `inline-block` for complex grids.

---

## Reflection Questions

1. What is the fundamental difference between `display: block` and `display: inline`?
2. Why would you use `display: inline-block` instead of just `display: inline`?
3. An element has `display: none`. Does it still exist in the HTML? Can JavaScript still find it?
4. You have a table with 5 columns. You hide one column with `display: none` — the other columns shift left. You hide it with `visibility: hidden` — the columns stay in place. Why?
5. If you want a horizontal navigation bar using `<li>` items, which display value do you set on the `<li>` — `inline` or `block`? Why?
6. Why does `display: none` remove content from screen readers, and what is the alternative if you want to hide something only visually?
7. You set `width: 300px` on a `<span>`. Nothing happens. What do you need to change and why?

---

## Completion Checklist

- [ ] I understand that every HTML element has a default display value
- [ ] I can list at least 5 elements that default to `block` and 5 that default to `inline`
- [ ] I understand what `display: block` does — full width, new line, respects all dimensions
- [ ] I understand what `display: inline` does — flows in text, no forced new line, ignores width/height
- [ ] I understand what `display: inline-block` does — sits inline but respects all dimensions
- [ ] I can use `display: inline` to convert `<li>` items into a horizontal navigation
- [ ] I can use `display: inline-block` to create side-by-side cards with controlled sizes
- [ ] I understand that `display: none` completely removes an element from the layout
- [ ] I understand that `visibility: hidden` hides an element but preserves its space
- [ ] I can explain the exact difference between `display: none` and `visibility: hidden`
- [ ] I have completed all three guided exercises
- [ ] I have built the team profile page mini project
- [ ] I understand why removing focus outlines with `display: none` impacts accessibility
- [ ] I know about the `inline-block` whitespace gap and at least one way to fix it

---

## Lesson Summary

### All Key Display Values at a Glance

| Value | Starts New Line? | Respects Width/Height? | Takes Up Space When Hidden? |
|---|---|---|---|
| `block` | Yes | Yes | Yes |
| `inline` | No | No | Yes |
| `inline-block` | No | **Yes** | Yes |
| `none` | — | — | **No** |

### `display: none` vs `visibility: hidden`

| | `display: none` | `visibility: hidden` |
|---|---|---|
| Visible? | No | No |
| Takes up space? | **No** | **Yes** |
| Other elements move to fill gap? | Yes | No |
| Screen reader? | Removed | Removed |

### The Display Override Pattern

```css
/* Making block elements go inline */
li    { display: inline; }       /* For horizontal nav */
h1    { display: inline; }       /* For inline headings */

/* Making inline elements go block */
a     { display: block; }        /* For full-width links */
span  { display: block; }        /* For stacked spans */
img   { display: block; }        /* For centred images */

/* The hybrid: inline but with dimensions */
div   { display: inline-block; } /* For side-by-side cards */
li    { display: inline-block; } /* For nav items with padding */
```

### The Toggle Pattern (for JavaScript)

```css
/* Default: hidden */
.panel { display: none; }

/* When activated */
.panel.active { display: block; }
```

### Real-World Applications

- **Navigation bars:** `display: inline` or `display: inline-block` on `<li>` elements
- **Card grids:** `display: inline-block` on card containers
- **Dropdowns and modals:** `display: none` toggled to `display: block`
- **Responsive design:** `display: none` to hide content on mobile/desktop
- **Form layouts:** `display: block` on labels and inputs for vertical stacking
- **Horizontal menus from vertical lists:** `display: inline` on `<li>` elements
- **Accessibility labels:** Screen-reader-only classes using `position: absolute` instead of `display: none`

---

*You have completed Lesson 19: CSS Display. In the next lesson, you will explore CSS Max-Width — controlling how wide elements can grow on large screens.*
