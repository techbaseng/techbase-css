---
render_with_liquid: false
title: "CSS Selectors — Targeting Elements Like a Pro"
nav_order: 2
---

# Lesson 02 — CSS Selectors: Targeting Elements Like a Pro

---

## Lesson Introduction

Welcome to one of the most important lessons in all of CSS!

Imagine you are in a large classroom. The teacher wants to give instructions — but not to everyone. Sometimes she says **"everyone with a red shirt, stand up."** Other times she says **"John, come to the board."** And sometimes she says **"everyone, be quiet."**

CSS works exactly the same way. You have a webpage full of HTML elements — paragraphs, headings, buttons, images — and CSS needs a way to **pick which ones to style**. That picking mechanism is called a **selector**.

Without selectors, CSS would be useless. You could write the most beautiful styling rules in the world, but without a selector, CSS would not know *who* to apply them to.

By the end of this lesson you will:

- Understand what a CSS selector is and why it exists
- Use the **element selector** to style HTML tags by name
- Use the **id selector** to style one unique element
- Use the **class selector** to style groups of elements
- Use the **universal selector** to style everything at once
- Use the **grouping selector** to write cleaner, shorter CSS
- Recognise common beginner mistakes and know how to fix them
- Complete guided practice exercises and a mini-project

---

## Prerequisite Concepts

Before we start, make sure you understand these two things. If they are new to you, read this section carefully before moving on.

### What is HTML?

HTML (HyperText Markup Language) is the language used to build the structure of a webpage. It uses **tags** like `<p>`, `<h1>`, `<div>`, and `<button>` to create different kinds of content.

```html
<!-- This is a paragraph in HTML -->
<p>Hello, world!</p>

<!-- This is a heading -->
<h1>Welcome to My Page</h1>
```

Each of these tags creates an **element** — a piece of content on the page.

### What is CSS?

CSS (Cascading Style Sheets) is the language used to **decorate** that HTML. It controls colours, fonts, sizes, spacing, and layout.

A CSS rule looks like this:

```css
/* Syntax: selector { property: value; } */
p {
  color: red;
}
```

- `p` — the **selector** (which element to style)
- `color` — the **property** (what aspect to change)
- `red` — the **value** (what to change it to)
- The whole block `{ color: red; }` is called a **declaration block**

> **Analogy:** Think of HTML as the skeleton of a body, and CSS as the clothing, makeup, and accessories. The selector is what tells CSS *which body part* to dress.

---

## Part 1 — What Is a CSS Selector?

A **CSS selector** is the part of a CSS rule that identifies **which HTML element(s)** the rule applies to.

```css
h1 {              /* ← This is the selector */
  color: blue;
}
```

The selector `h1` tells the browser: *"Find every `<h1>` element on this page, and make its text blue."*

CSS selectors can be divided into five main categories. This lesson focuses on the most fundamental ones — called **simple selectors**:

1. **Element selector** — selects by tag name (e.g., `p`, `h1`, `div`)
2. **ID selector** — selects one unique element by its `id` attribute
3. **Class selector** — selects any element with a matching `class` attribute
4. **Universal selector** — selects every element on the page
5. **Grouping selector** — applies the same style to multiple selectors at once

---

## Part 2 — The Element Selector

### What is it?

The **element selector** (also called the **type selector**) selects HTML elements based on their **tag name**.

### Why does it exist?

Suppose you want every single paragraph on your page to use a specific font. Writing a rule for each paragraph individually would be tedious and impractical. The element selector lets you target *all* paragraphs with one rule.

### How it works

Simply write the tag name, followed by your style rules in curly braces:

```css
tagname {
  property: value;
}
```

### Simple Example 1 — Style all paragraphs

**HTML:**
```html
<p>This is the first paragraph.</p>
<p>This is the second paragraph.</p>
<p>This is the third paragraph.</p>
```

**CSS:**
```css
p {
  color: red;
  text-align: center;
}
```

**Expected Output:**
All three paragraphs will appear with **red text**, and each will be **centred** on the page.

**Line-by-line explanation:**
- `p` — the selector. This targets *every* `<p>` element on the page.
- `{` — opens the declaration block (the list of styling rules).
- `color: red;` — sets the text colour to red.
- `text-align: center;` — aligns the text to the centre of its container.
- `}` — closes the declaration block.

> **Thinking Prompt:** What would happen if you changed `p` to `h1`? Try to predict the answer before testing it.

---

### Simple Example 2 — Style all headings

**HTML:**
```html
<h1>Main Title</h1>
<h2>Sub-Title</h2>
<p>Some introductory text here.</p>
```

**CSS:**
```css
h1 {
  color: navy;
}
```

**Expected Output:**
Only the `<h1>` element "Main Title" will turn navy blue. The `<h2>` and `<p>` are NOT affected.

> **Key insight:** The element selector is broad but precise at the same time — it targets *all* elements of that type, but only that type.

---

### Real-World Use Case

In a news website, a developer might write:

```css
p {
  font-size: 16px;
  line-height: 1.6;
  color: #333;
}
```

This ensures every article paragraph has a comfortable, readable style — without having to repeat the code hundreds of times.

---

## Part 3 — The ID Selector

### What is it?

The **ID selector** targets **one specific, unique element** on the page using its `id` attribute.

### Why does it exist?

Sometimes you have one special element that needs a completely different style from everything else. For example, you might have a hero banner, a top navigation bar, or a modal popup that needs its own unique look.

### The `id` attribute — a quick explanation

In HTML, you can give any element a unique label called an `id`:

```html
<p id="intro">This is a special paragraph.</p>
<p>This is a normal paragraph.</p>
```

- `id="intro"` — gives this element the unique identifier "intro"
- **Every `id` on a page must be unique** — no two elements should share the same id

### How the ID selector works in CSS

To target an element by its id, write a **hash symbol `#`** followed by the id name:

```css
#idname {
  property: value;
}
```

### Simple Example 1 — Style one specific paragraph

**HTML:**
```html
<p id="para1">This paragraph has a special style.</p>
<p>This paragraph is completely normal.</p>
```

**CSS:**
```css
#para1 {
  text-align: center;
  color: red;
}
```

**Expected Output:**
- The first paragraph (with `id="para1"`) will be **red and centred**.
- The second paragraph is **completely unaffected** — it keeps its default styling.

**Line-by-line explanation:**
- `#para1` — the `#` symbol signals "this is an ID selector". `para1` is the id name to look for.
- `text-align: center;` — centres the text.
- `color: red;` — makes the text red.

---

### Simple Example 2 — Style a navigation bar

**HTML:**
```html
<div id="navbar">Home | About | Contact</div>
<p>Welcome to our website!</p>
```

**CSS:**
```css
#navbar {
  background-color: black;
  color: white;
  padding: 10px;
}
```

**Expected Output:**
The navigation `div` will have a **black background** with **white text**, while the paragraph is unaffected.

---

### Important Rules for IDs

> ⚠️ **Rules you must follow:**
> - An `id` name **cannot start with a number**. `id="1intro"` is invalid; `id="intro1"` is fine.
> - An `id` should not contain spaces. Use hyphens or camelCase instead: `id="main-header"` or `id="mainHeader"`.
> - Each `id` must be **unique on the page**. Using the same id on two elements is invalid HTML and causes unpredictable CSS behaviour.

---

### Real-World Use Case

In almost every website, the main page header gets a unique id:

```html
<header id="site-header">
  <h1>My Blog</h1>
</header>
```

```css
#site-header {
  background-color: #2c3e50;
  color: white;
  padding: 20px 40px;
}
```

This targets only that one header element — leaving all other elements alone.

---

## Part 4 — The Class Selector

### What is it?

The **class selector** targets **any element** that has been assigned a particular `class` attribute. Unlike an id (which is unique), many elements can share the same class.

### Why does it exist?

Imagine you are building a product catalogue. Some product cards should be highlighted in yellow — maybe the best-sellers. Others are normal. You can assign a class `"highlight"` to any product that needs the yellow treatment, then write one CSS rule for `.highlight`.

### The `class` attribute — a quick explanation

```html
<p class="highlight">Best Seller!</p>
<p>Regular product.</p>
<h2 class="highlight">Featured Category</h2>
```

- `class="highlight"` — marks these elements as belonging to the "highlight" group
- **Multiple elements CAN share the same class** — that is the whole point
- An element **can have multiple classes**: `class="highlight bold large"`

### How the class selector works in CSS

Write a **period (dot) `.`** followed by the class name:

```css
.classname {
  property: value;
}
```

### Simple Example 1 — Style a group of elements

**HTML:**
```html
<h1 class="highlight">Top Product</h1>
<p class="highlight">This item is on sale!</p>
<p>This item is not on sale.</p>
```

**CSS:**
```css
.highlight {
  background-color: yellow;
  color: black;
}
```

**Expected Output:**
- The `<h1>` "Top Product" will have a **yellow background**.
- The first `<p>` "This item is on sale!" will also have a **yellow background**.
- The second `<p>` "This item is not on sale." is **completely unaffected**.

**Line-by-line explanation:**
- `.highlight` — the `.` signals "this is a class selector". `highlight` is the class name.
- `background-color: yellow;` — sets the background colour to yellow.
- `color: black;` — sets the text colour to black.

---

### Simple Example 2 — Target a specific tag that has a class

You can combine a tag name with a class to be even more specific. This is called a **qualified class selector**:

```css
p.highlight {
  background-color: yellow;
}
```

This means: *"Only target `<p>` elements that have the class `highlight`."* A `<h1 class="highlight">` would NOT be styled by this rule.

**HTML:**
```html
<h1 class="highlight">I am a heading with the class.</h1>
<p class="highlight">I am a paragraph with the class.</p>
<p>I have no class at all.</p>
```

**CSS:**
```css
p.highlight {
  background-color: yellow;
}
```

**Expected Output:**
- Only the `<p class="highlight">` gets the yellow background.
- The `<h1 class="highlight">` is **NOT** styled — because the rule is limited to `p` elements only.

---

### Simple Example 3 — Multiple classes on one element

An element can belong to more than one class at once. Separate class names with a **space** inside the `class` attribute:

**HTML:**
```html
<p class="large bold">This text is large AND bold.</p>
```

**CSS:**
```css
.large {
  font-size: 24px;
}

.bold {
  font-weight: bold;
}
```

**Expected Output:**
The paragraph will be displayed with a **24px font size AND bold weight** — because both classes apply to it simultaneously.

> **Thinking Prompt:** What would happen if you wrote `class="large bold extra"` but there was no `.extra` rule in your CSS? Would it cause an error?
> *(Answer: No error. CSS simply ignores class names it has no rules for.)*

---

### ID vs Class — When to use which?

| Feature | ID (`#`) | Class (`.`) |
|---|---|---|
| Uniqueness | Must be unique (one per page) | Can be reused on many elements |
| Symbol in CSS | `#` | `.` |
| Best used for | One-of-a-kind elements (logo, main nav) | Groups of similar elements (buttons, cards, alerts) |
| Multiple per element | No — one id per element | Yes — many classes per element |

> **Analogy:** An id is like a national ID card — one person, one number. A class is like a school uniform — many students wear it, and one student can wear multiple items (blazer *and* tie *and* school shoes).

---

## Part 5 — The Universal Selector

### What is it?

The **universal selector** is written as a single asterisk `*` and it targets **every single HTML element** on the page — headings, paragraphs, divs, spans, buttons, images, everything.

### Why does it exist?

It is most commonly used to apply a global reset or baseline style. For example, some browsers add default padding and margins to elements. Web developers use `*` to remove all those defaults and start with a clean slate.

### How it works

```css
* {
  property: value;
}
```

### Simple Example 1 — Colour everything blue

**HTML:**
```html
<h1>Heading</h1>
<p>Paragraph</p>
<a href="#">Link</a>
```

**CSS:**
```css
* {
  text-align: center;
  color: blue;
}
```

**Expected Output:**
Every element on the page — the heading, the paragraph, and the link — will have **centred, blue text**.

---

### Simple Example 2 — The CSS Reset (most common real-world use)

This is the most important practical use of the universal selector:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

**What this does:**
- `margin: 0;` — removes all default outer spacing from every element
- `padding: 0;` — removes all default inner spacing from every element
- `box-sizing: border-box;` — changes how element sizes are calculated (more predictable)

> **Real-World Insight:** Almost every professional CSS stylesheet starts with a universal reset like this. It eliminates browser inconsistencies so your layout behaves the same in Chrome, Firefox, Safari, and Edge.

---

> ⚠️ **Performance Note:** Because `*` targets every element, it can slow down very large, complex pages if overused with expensive properties. For simple properties like `margin` and `padding`, it is perfectly fine.

---

## Part 6 — The Grouping Selector

### The Problem It Solves

Imagine you have three different elements — `h1`, `h2`, and `p` — and you want them all to have the same text colour and alignment. Without the grouping selector, you would write this:

```css
h1 {
  text-align: center;
  color: red;
}

h2 {
  text-align: center;
  color: red;
}

p {
  text-align: center;
  color: red;
}
```

This works, but it is **repetitive and inefficient**. If you later decide to change `red` to `navy`, you have to change it in **three places**. If you miss one, your page will look inconsistent.

### What is the Grouping Selector?

The **grouping selector** lets you apply the same style rules to **multiple selectors at once**. You simply list the selectors separated by **commas**.

### How it works

```css
selector1, selector2, selector3 {
  property: value;
}
```

### Simple Example 1 — Group three elements

**CSS (before grouping — the problem):**
```css
h1 {
  text-align: center;
  color: red;
}

h2 {
  text-align: center;
  color: red;
}

p {
  text-align: center;
  color: red;
}
```

**CSS (after grouping — the solution):**
```css
h1, h2, p {
  text-align: center;
  color: red;
}
```

**Expected Output:**
Exactly the same result — all `<h1>`, `<h2>`, and `<p>` elements will have **red, centred text** — but the code is now much shorter and easier to maintain.

---

### Simple Example 2 — Grouping class and element selectors together

You can group any mix of selector types — elements, ids, and classes — as long as they need the same style:

**HTML:**
```html
<h1>Main Heading</h1>
<p class="intro">Introduction paragraph.</p>
<span id="tagline">Our tagline here.</span>
```

**CSS:**
```css
h1, .intro, #tagline {
  font-family: Arial, sans-serif;
  color: #333;
}
```

**Expected Output:**
All three elements — the `<h1>`, the `.intro` paragraph, and the `#tagline` span — will use the Arial font with dark grey text.

---

### Real-World Use Case

In real projects, grouping selectors are used extensively to maintain consistent typography across a page:

```css
h1, h2, h3, h4, h5, h6 {
  font-family: 'Georgia', serif;
  color: #1a1a2e;
  line-height: 1.3;
}
```

This ensures all six heading levels share the same font, colour, and line spacing — a fundamental part of consistent web design.

---

## Part 7 — All Five Simple Selectors at a Glance

Here is a complete summary table of everything covered so far:

| Selector | Syntax | What It Targets | Example |
|---|---|---|---|
| Element | `p` | All `<p>` elements | `p { color: red; }` |
| ID | `#myId` | One element with `id="myId"` | `#logo { width: 200px; }` |
| Class | `.myClass` | All elements with `class="myClass"` | `.btn { background: blue; }` |
| Universal | `*` | Every element on the page | `* { box-sizing: border-box; }` |
| Grouping | `h1, h2, p` | All listed selectors | `h1, h2 { font-family: Arial; }` |

---

## Part 8 — Guided Practice Exercises

### Exercise 1 — Styling a Simple Blog Page

**Objective:** Practice using the element, id, and class selectors together.

**Scenario:** You are building the HTML and CSS for a simple blog post page.

**HTML (given — do not change this):**
```html
<!DOCTYPE html>
<html>
<head>
  <title>My Blog Post</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <h1 id="post-title">My First Blog Post</h1>

  <p class="intro-text">Welcome to my blog! I write about technology and design.</p>

  <h2>Why I Started This Blog</h2>
  <p>I started this blog because I love sharing what I learn.</p>

  <h2>What I Write About</h2>
  <p class="intro-text">Mostly CSS, HTML, and design principles.</p>

</body>
</html>
```

**Your Task (write the CSS in `style.css`):**

1. Make all `<h2>` elements dark blue (`color: darkblue`).
2. Make the element with `id="post-title"` use a font size of 36px (`font-size: 36px`) and the colour `#c0392b` (a deep red).
3. Make all elements with `class="intro-text"` have an italic style (`font-style: italic`) and a light grey background (`background-color: #f0f0f0`).
4. Use a **grouping selector** to centre-align both `h1` and `h2` elements.

**Hints:**
- Use `h2 { }` for task 1
- Use `#post-title { }` for task 2
- Use `.intro-text { }` for task 3
- Use `h1, h2 { }` for task 4

**Expected Output:**
- The main title "My First Blog Post" should be large, dark red, and centred.
- The two `<h2>` subheadings should be dark blue and centred.
- The two `.intro-text` paragraphs should be italic with a light grey background.
- The normal `<p>` "I started this blog..." should have default styling.

**Solution:**
```css
/* Task 1 — Element selector */
h2 {
  color: darkblue;
}

/* Task 2 — ID selector */
#post-title {
  font-size: 36px;
  color: #c0392b;
}

/* Task 3 — Class selector */
.intro-text {
  font-style: italic;
  background-color: #f0f0f0;
}

/* Task 4 — Grouping selector */
h1, h2 {
  text-align: center;
}
```

**Self-check Questions:**
- Which paragraphs got the grey background — all of them, or only some?
- Is the main title centred because of the `#post-title` rule or the `h1, h2` rule?
- What would happen if you removed the grouping selector but kept the `#post-title` rule?

---

### Exercise 2 — Product Cards

**Objective:** Practice using multiple classes and the universal selector.

**Scenario:** You are styling a simple product listing page for a small shop.

**HTML (given):**
```html
<div class="card">
  <h3 class="product-name">Running Shoes</h3>
  <p class="price">₦15,000</p>
</div>

<div class="card featured">
  <h3 class="product-name">Premium Sneakers</h3>
  <p class="price special-price">₦25,000</p>
</div>

<div class="card">
  <h3 class="product-name">Sandals</h3>
  <p class="price">₦8,000</p>
</div>
```

**Your Task (write the CSS):**

1. Use `*` to remove all default margin and padding.
2. Style `.card` with a border, padding, and a small bottom margin.
3. Style `.product-name` to be dark green.
4. Style `.price` to be bold.
5. Style `.special-price` to be red.
6. Style `.featured` cards to have a light gold background (`background-color: #fff9c4`).

**Solution:**
```css
/* Task 1 — Universal selector reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Task 2 — Card base style */
.card {
  border: 1px solid #ccc;
  padding: 16px;
  margin-bottom: 12px;
}

/* Task 3 — Product name */
.product-name {
  color: darkgreen;
}

/* Task 4 — Price base */
.price {
  font-weight: bold;
}

/* Task 5 — Special price */
.special-price {
  color: red;
}

/* Task 6 — Featured card */
.featured {
  background-color: #fff9c4;
}
```

**Expected Output:**
- All three cards will have borders and padding.
- The "Premium Sneakers" card will have a yellow background (featured).
- Its price "₦25,000" will be both bold AND red (it has both `.price` and `.special-price` classes).
- Regular prices will be bold only.

> **What-If Challenge:** What happens if you add the class `featured` to the Sandals card too? Try it!

---

## Part 9 — Mini Project: Personal Profile Card

Build a complete, styled personal profile card page from scratch using all the selectors you have learned.

### Project Brief

You are building a simple personal profile page for a fictional person named "Amara Okafor." The page should look clean, organised, and styled using only the selectors from this lesson.

---

### Stage 1 — Setup: HTML Structure

Create a file called `index.html` with this content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Amara Okafor — Profile</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <header id="page-header">
    <h1>Amara Okafor</h1>
    <p class="tagline">Software Developer · Lagos, Nigeria</p>
  </header>

  <main id="main-content">

    <section class="card">
      <h2>About Me</h2>
      <p>I am a passionate software developer with a love for building clean, accessible web applications.</p>
    </section>

    <section class="card featured">
      <h2>Featured Project</h2>
      <p class="highlight">Budget Tracker App — built with HTML, CSS, and JavaScript.</p>
      <p>This app helps families manage monthly expenses with a simple, visual dashboard.</p>
    </section>

    <section class="card">
      <h2>Skills</h2>
      <p>HTML · CSS · JavaScript · Python · Git</p>
    </section>

  </main>

  <footer id="page-footer">
    <p>© 2025 Amara Okafor. All rights reserved.</p>
  </footer>

</body>
</html>
```

---

### Stage 2 — Core Styling: `style.css`

```css
/* ===== STAGE 2: CORE STYLES ===== */

/* Universal Reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Body base */
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  color: #333;
  padding: 20px;
}
```

**Milestone Output:** The page should now have a grey background, dark text, and Arial font everywhere. All default browser spacing has been removed.

---

### Stage 3 — Selectors in Action

Add these rules to your `style.css`:

```css
/* ===== STAGE 3: SELECTORS ===== */

/* ID selectors — unique sections */
#page-header {
  background-color: #2c3e50;
  color: white;
  padding: 30px;
  text-align: center;
  border-radius: 8px;
  margin-bottom: 20px;
}

#page-footer {
  background-color: #2c3e50;
  color: white;
  text-align: center;
  padding: 15px;
  border-radius: 8px;
  margin-top: 20px;
}

/* Class selector — card styling */
.card {
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 16px;
}

/* Class selector — featured card */
.featured {
  background-color: #eaf4fb;
  border-color: #3498db;
}

/* Class selector — highlighted text */
.highlight {
  color: #2980b9;
  font-weight: bold;
}

/* Class selector — tagline */
.tagline {
  font-size: 14px;
  color: #bdc3c7;
  margin-top: 6px;
}

/* Element selectors — headings inside cards */
h2 {
  color: #2c3e50;
  margin-bottom: 10px;
}

/* Element selector — paragraphs inside cards */
p {
  line-height: 1.6;
}

/* Grouping selector — all headings */
h1, h2 {
  font-family: Georgia, serif;
}
```

**Milestone Output:**
- A dark navy header with Amara's name and tagline
- Three white cards
- The "Featured Project" card has a light blue tint and blue border
- The "Budget Tracker App" text is bold and blue
- All headings use Georgia font

---

### Stage 4 — Reflection Questions

After completing the project, answer these questions in your own words:

1. Which selector did you use the most? Why do you think that is?
2. What is the difference between how `#page-header` and `.card` target elements?
3. If you wanted to add a fourth card AND make it look like a warning (red background), what CSS would you write?
4. Why did the grouping selector `h1, h2` make the code more efficient?
5. What would break if you accidentally gave two elements `id="page-header"`?

---

### Optional Extension Challenges

- Add a `<nav>` element inside the header with links, and style it using an id
- Create a `.warning` class and apply it to a new section
- Add a `.skills-list` class to the Skills section and change the colour of its paragraph

---

## Part 10 — Common Beginner Mistakes

### Mistake 1 — Forgetting the `#` for IDs

**Wrong:**
```css
para1 {
  color: red;
}
```

**Why it's wrong:** Without `#`, CSS treats `para1` as an element selector — it looks for an HTML tag called `<para1>`, which doesn't exist. Nothing will be styled.

**Correct:**
```css
#para1 {
  color: red;
}
```

---

### Mistake 2 — Forgetting the `.` for Classes

**Wrong:**
```css
highlight {
  background-color: yellow;
}
```

**Why it's wrong:** CSS will look for an HTML tag called `<highlight>`, which doesn't exist.

**Correct:**
```css
.highlight {
  background-color: yellow;
}
```

---

### Mistake 3 — Using Spaces in Class Names in CSS

**Wrong:**
```css
.my class {    /* THIS IS TWO SELECTORS, NOT ONE! */
  color: red;
}
```

**Why it's wrong:** A space in CSS between two selectors means "an element INSIDE another element" — this is called a descendant combinator. `.my class` means "a `class` element *inside* something with class `my`."

**Correct:**
```css
.my-class {
  color: red;
}
```

In HTML, use a hyphen in the class name: `class="my-class"`.

---

### Mistake 4 — Repeating the Same Styles Instead of Grouping

**Wrong (repetitive):**
```css
h1 { color: navy; }
h2 { color: navy; }
h3 { color: navy; }
```

**Correct (grouped):**
```css
h1, h2, h3 {
  color: navy;
}
```

---

### Mistake 5 — Using the Same ID Twice

**Wrong:**
```html
<div id="box">First</div>
<div id="box">Second</div>  <!-- INVALID HTML! -->
```

**Why it's wrong:** HTML IDs must be unique. If you use the same id twice, your CSS may only style the first one (browser behaviour is unpredictable), and your HTML fails validation.

**Correct:** Use a class instead when multiple elements need the same style:
```html
<div class="box">First</div>
<div class="box">Second</div>
```

---

### Mistake 6 — Missing the Comma in Grouping Selectors

**Wrong:**
```css
h1 h2 {    /* This means: h2 INSIDE an h1 — probably not what you want! */
  color: red;
}
```

**Why it's wrong:** Without the comma, `h1 h2` becomes a **descendant selector** — it means "any `h2` that is nested inside an `h1`."

**Correct:**
```css
h1, h2 {    /* Comma = grouping = BOTH h1 AND h2 get styled */
  color: red;
}
```

---

## Part 11 — Reflection Questions

Before moving on to the next lesson, take a moment to answer these:

1. What is a CSS selector? Explain it in your own words without using technical jargon.
2. You have a webpage with 50 paragraphs. You want only 3 of them to have a yellow background. Would you use an element selector, id selector, or class selector? Why?
3. What is the difference between `.card` and `#card` in CSS?
4. You notice your universal selector `*` is making all images disappear. What might have gone wrong?
5. If `h1`, `h2`, `h3`, and `p` all need `color: #444`, what is the cleanest way to write that CSS?
6. Can one HTML element have both an `id` and a `class` at the same time? What would that look like?

---

## Completion Checklist

Use this checklist to confirm you are ready to move to the next lesson:

- [ ] I can explain what a CSS selector is and why it is needed
- [ ] I can write a CSS rule using the **element selector** to target HTML tags
- [ ] I can write a CSS rule using the **id selector** (`#`) to target one unique element
- [ ] I can write a CSS rule using the **class selector** (`.`) to target a group of elements
- [ ] I can write a CSS rule using the **universal selector** (`*`) to target all elements
- [ ] I can use the **grouping selector** (comma-separated) to apply the same style to multiple selectors
- [ ] I understand that `id` must be unique, while `class` can be reused
- [ ] I understand the difference between `h1 h2` (descendant) and `h1, h2` (grouping)
- [ ] I completed Exercise 1 (Blog Page)
- [ ] I completed Exercise 2 (Product Cards)
- [ ] I completed the Mini Project (Profile Card)
- [ ] I can identify and fix the 6 common beginner mistakes

---

## Lesson Summary

In this lesson, you learned how CSS **selectors** act as the targeting system that tells CSS *which elements to style*. Here is a recap of everything covered:

**The five simple selectors:**

The **element selector** (`p`, `h1`, `div`) targets all elements of a given HTML tag type — useful for setting site-wide base styles. The **id selector** (`#myId`) targets exactly one unique element — ideal for headers, footers, and other one-of-a-kind components. The **class selector** (`.myClass`) targets any element bearing that class name — the most flexible and widely-used selector in real projects. The **universal selector** (`*`) targets every element simultaneously — most commonly used for CSS resets at the top of a stylesheet. The **grouping selector** (`h1, h2, p`) lists multiple selectors separated by commas so they all share the same style rules — an essential tool for writing clean, maintainable code.

**Key principles to remember:**

An id must be unique — use it for elements that appear only once. A class is reusable — use it for components that repeat. A space between selectors means "descendant", while a comma means "grouping". The universal selector is powerful but should be used deliberately.

In the next lesson, you will learn how to **add CSS to your HTML document** — inline, internal, and external stylesheets — so your selectors can actually be applied to real pages.

---

*Sources: W3Schools CSS Selectors (https://www.w3schools.com/css/css_selectors.asp) and CSS Grouping Selectors (https://www.w3schools.com/css/css_selectors_grouping.asp)*
