---
render_with_liquid: false
title: "CSS Combinators — Targeting Elements by Their Relationships"
nav_order: 28
---

# Lesson 28 — CSS Combinators

---

## Lesson Introduction

So far you have learned to target HTML elements using simple selectors like `p`, `.classname`, and `#id`. But what if you only want to style a `<p>` that is **inside** a specific `<div>`? Or only the `<p>` that comes **immediately after** an `<h2>`? Or only the **direct children** of a sidebar?

This is exactly what **CSS combinators** solve. A combinator is a symbol you place **between two selectors** to describe a **relationship** between them. Instead of targeting every `<p>` on the page, you can target a `<p>` only when it appears in a specific place in your HTML structure.

In this lesson you will learn:
- What a combinator is and why it exists
- All four CSS combinators: descendant (` `), child (`>`), adjacent sibling (`+`), and general sibling (`~`)
- How to read, write, and apply each combinator with working code examples
- How to combine multiple combinators to write powerful, precise selectors
- How to build a real-world styled article page using all four combinators together

By the end of this lesson, you will be able to write CSS selectors that are surgical — targeting exactly the right element in exactly the right context, without needing extra classes or IDs.

---

## Prerequisite Concepts

Before learning combinators, you need to understand two ideas: CSS selectors and the HTML family-tree structure.

### 1. What is a CSS Selector?

A CSS **selector** is the part of a CSS rule that identifies which HTML element(s) you want to style.

```css
/* Selector → Style rule */
p {
  color: blue;
}
```

Here, `p` is the selector — it targets every `<p>` element on the page.

You already know simple selectors:
- `p` — selects all paragraph elements
- `.highlight` — selects all elements with class "highlight"
- `#header` — selects the element with id "header"

But sometimes you need to target an element **only when it has a specific relationship to another element**.

### 2. The HTML Tree — Parents, Children, Descendants, and Siblings

HTML elements are nested inside each other, forming a structure like a **family tree**. Understanding this tree is the key to understanding combinators.

Consider this HTML:

```html
<div>               ← parent
  <p>First</p>      ← child of div, sibling of Second and Third
  <p>Second</p>     ← child of div, sibling of First and Third
  <span>
    <p>Third</p>    ← child of span, grandchild of div (descendant)
  </span>
</div>
<p>Outside</p>      ← NOT inside div at all
```

**Vocabulary you need:**

- **Parent** — the element directly containing another element. In the example above, `<div>` is the parent of the first two `<p>` tags.
- **Child** — an element directly inside a parent. The two `<p>` tags and the `<span>` are **direct children** of `<div>`.
- **Descendant** — any element inside another element, no matter how deeply nested. The third `<p>` (inside `<span>` inside `<div>`) is a **descendant** of `<div>`, even though it is not a direct child.
- **Sibling** — two elements that share the same parent. The two `<p>` tags inside `<div>` are siblings of each other.
- **Adjacent sibling** — a sibling that comes **immediately after** another in the HTML code.

**Analogy:** Think of it like a real family. Your parent is one level above you. Your siblings share the same parent. Your descendants are your children, grandchildren, great-grandchildren, etc.

---

## Conceptual Understanding

### What is a CSS Combinator?

A **combinator** is a special character placed **between two selectors** that tells the browser about the **relationship** required between those two elements for the style to apply.

```css
/* General pattern */
selector1 COMBINATOR selector2 {
  /* styles apply to selector2 when it has the right relationship to selector1 */
}
```

There are **four CSS combinators**:

| Name | Symbol | Meaning |
|---|---|---|
| Descendant | ` ` (a space) | Any matching element anywhere inside the first |
| Child | `>` | Only direct children of the first |
| Adjacent Sibling | `+` | Only the immediately following sibling |
| General Sibling | `~` | All following siblings |

> **💡 Key insight:** Combinators do NOT style the first selector — they style the **second** selector, but only when the first selector's relationship condition is met. The first selector sets the context; the second is what actually gets styled.

---

## The Four Combinators — Full Detailed Explanations

---

### Combinator 1 — The Descendant Selector (space)

**Symbol:** A single space between two selectors: `A B`

**What it does:** Selects **every** element matching `B` that is located **anywhere inside** element `A` — whether it is a direct child, grandchild, great-grandchild, or even deeper.

**Think of it like:** "Give me all the `<p>` tags that live inside this `<div>`, no matter how deep they are buried."

**Syntax:**
```css
ancestor descendant {
  /* styles */
}
```

#### Simple Example 1 — Descendant Selector

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div p {
      background-color: yellow;
    }
  </style>
</head>
<body>

  <div>
    <p>Paragraph 1 — inside div (styled ✅)</p>
    <p>Paragraph 2 — inside div (styled ✅)</p>
    <section>
      <p>Paragraph 3 — inside section inside div (styled ✅)</p>
    </section>
  </div>

  <p>Paragraph 4 — OUTSIDE div (NOT styled ❌)</p>

</body>
</html>
```

**Expected Output (visually):**
```
[yellow background] Paragraph 1 — inside div
[yellow background] Paragraph 2 — inside div
[yellow background] Paragraph 3 — inside section inside div
Paragraph 4 — OUTSIDE div     ← no yellow background
```

**Breaking down the code:**

`div p` — The space between `div` and `p` is the **descendant combinator**. It tells the browser: "Find all `<p>` elements that exist anywhere inside a `<div>`."

Notice that Paragraph 3 is inside `<section>` which is inside `<div>`. Even though there is an extra layer (`section`) between `div` and `p`, the descendant selector still finds it because it searches all levels down.

Paragraph 4 is **outside** the `<div>`, so it is NOT styled.

> **🤔 Thinking prompt:** What if you added another `<p>` inside a `<span>` inside the `<div>`? Would it get styled? Yes! The descendant selector goes as deep as needed.

---

### Combinator 2 — The Child Selector (`>`)

**Symbol:** `>` (greater-than sign): `A > B`

**What it does:** Selects **only** elements matching `B` that are **direct children** of `A`. Grandchildren and deeper descendants are NOT selected.

**Think of it like:** "Only style my immediate children — not my grandchildren."

**Syntax:**
```css
parent > direct-child {
  /* styles */
}
```

#### Simple Example 2 — Child Selector

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div > p {
      background-color: lightblue;
    }
  </style>
</head>
<body>

  <div>
    <p>Paragraph 1 — direct child of div (styled ✅)</p>
    <p>Paragraph 2 — direct child of div (styled ✅)</p>
    <section>
      <p>Paragraph 3 — child of section, NOT direct child of div (NOT styled ❌)</p>
    </section>
  </div>

  <p>Paragraph 4 — outside div (NOT styled ❌)</p>

</body>
</html>
```

**Expected Output (visually):**
```
[light blue] Paragraph 1 — direct child of div
[light blue] Paragraph 2 — direct child of div
Paragraph 3 — child of section, NOT direct child of div     ← no styling
Paragraph 4 — outside div                                   ← no styling
```

**Breaking down the code:**

`div > p` — The `>` means "direct child only." Paragraphs 1 and 2 are **direct children** of `<div>`, so they are styled. Paragraph 3 is a direct child of `<section>`, not of `<div>` — so it is **not** styled by this rule.

**Descendant vs. Child — The Key Difference:**

| Selector | Selects Paragraph 3 inside `<section>` inside `<div>`? |
|---|---|
| `div p` (descendant) | ✅ Yes — selects all levels deep |
| `div > p` (child) | ❌ No — only direct children |

> **🤔 Thinking prompt:** When would you want to use `>` instead of ` ` (space)? Use `>` when you have nested structures and only want to style one specific level — for example, styling only the top-level menu items in a nav bar, but not items inside sub-menus.

---

### Combinator 3 — The Adjacent Sibling Selector (`+`)

**Symbol:** `+` (plus sign): `A + B`

**What it does:** Selects the **single** element matching `B` that comes **immediately after** element `A`, AND both must share the **same parent**.

**Think of it like:** "Style only my next-door neighbour — the one who comes right after me."

**Key rules:**
- Both `A` and `B` must share the same parent
- `B` must appear **directly after** `A` in the HTML — no other elements between them
- Only **one** element is selected (the immediate next sibling), not multiple

**Syntax:**
```css
element + immediately-following-sibling {
  /* styles */
}
```

#### Simple Example 3 — Adjacent Sibling Selector

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    h2 + p {
      background-color: lightgreen;
    }
  </style>
</head>
<body>

  <h2>A Heading</h2>
  <p>This paragraph is right after h2 (styled ✅)</p>
  <p>This paragraph is NOT right after h2 (NOT styled ❌)</p>

  <h2>Another Heading</h2>
  <p>This paragraph is right after h2 again (styled ✅)</p>
  <p>This one is not right after h2 (NOT styled ❌)</p>

</body>
</html>
```

**Expected Output (visually):**
```
A Heading
[light green] This paragraph is right after h2
This paragraph is NOT right after h2

Another Heading
[light green] This paragraph is right after h2 again
This one is not right after h2
```

**Breaking down the code:**

`h2 + p` — "Find a `<p>` that comes **immediately** after an `<h2>`."

The **first** `<p>` after each `<h2>` is styled. The second, third, or any further `<p>` after the heading is not styled — only the immediately adjacent one.

> **🌍 Real-World Use:** This pattern is extremely common for styling the paragraph that follows a section heading differently — for example, making the first paragraph after a heading slightly larger (a "lead paragraph" or "drop cap" effect).

#### Second Example — What Happens When Another Element Is Between Them?

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    h2 + p {
      color: red;
    }
  </style>
</head>
<body>

  <h2>Heading</h2>
  <span>I am between the h2 and the p!</span>
  <p>This p is NOT right after h2 — a span is in the way (NOT styled ❌)</p>

</body>
</html>
```

**Expected Output:**
```
Heading
I am between the h2 and the p!
This p is NOT right after h2 — a span is in the way    ← NOT red
```

Because the `<span>` is between the `<h2>` and the `<p>`, the `<p>` is no longer the **immediate** sibling of `<h2>`. The `+` combinator is not applied.

> **💡 Important:** The `+` combinator is very strict — there must be **zero** other elements between `A` and `B`. Even a single `<br>` or `<span>` in between will break the match.

---

### Combinator 4 — The General Sibling Selector (`~`)

**Symbol:** `~` (tilde): `A ~ B`

**What it does:** Selects **all** elements matching `B` that come **after** element `A`, as long as they share the **same parent**. They do not need to be immediately adjacent — there can be other elements between them.

**Think of it like:** "Style all of my younger siblings — not just the one right next to me, but all of them who come after me."

**Key differences from `+`:**
- `+` selects only the **one** immediately following sibling
- `~` selects **all** following siblings that match

**Syntax:**
```css
element ~ all-following-siblings {
  /* styles */
}
```

#### Simple Example 4 — General Sibling Selector

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    h2 ~ p {
      background-color: lightyellow;
    }
  </style>
</head>
<body>

  <p>This p comes BEFORE h2 (NOT styled ❌)</p>

  <h2>The Heading</h2>

  <p>Paragraph 1 after h2 (styled ✅)</p>
  <p>Paragraph 2 after h2 (styled ✅)</p>
  <span>I am a span — not a p, so not styled</span>
  <p>Paragraph 3 after h2 (still styled ✅)</p>

</body>
</html>
```

**Expected Output (visually):**
```
This p comes BEFORE h2                   ← NOT styled

The Heading

[light yellow] Paragraph 1 after h2
[light yellow] Paragraph 2 after h2
I am a span — not a p, so not styled
[light yellow] Paragraph 3 after h2
```

**Breaking down the code:**

`h2 ~ p` — "Find all `<p>` elements that come after an `<h2>`, anywhere after it, as long as they share the same parent."

Notice:
- The `<p>` **before** the `<h2>` is NOT styled — the `~` combinator only looks forward, never backward.
- The `<span>` is ignored — it is not a `<p>` so the selector doesn't match it.
- The third `<p>` after the `<span>` is still styled — unlike `+`, the `~` selector doesn't care about other elements in between, as long as the `<p>` comes after the `<h2>`.

---

## All Four Combinators — Visual Summary

Here is a diagram to show the structure and what each combinator selects:

```
HTML Structure:
<div>
  <p>A</p>          ← direct child of div
  <section>
    <p>B</p>        ← grandchild of div, child of section
  </section>
  <p>C</p>          ← direct child of div
  <p>D</p>          ← direct child of div
</div>
<p>E</p>            ← outside div entirely
```

| Selector | What gets styled |
|---|---|
| `div p` (descendant) | A, B, C, D — all p's inside div at any depth |
| `div > p` (child) | A, C, D — only direct children of div |
| `section + p` | C — the p immediately after section |
| `section ~ p` | C, D — all p's that come after section |

---

## Simple Standalone Examples (Second Set)

### Example 5 — Descendant Selector in a Navigation Menu

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Style ALL links that are anywhere inside the nav element */
    nav a {
      color: white;
      text-decoration: none;
      font-weight: bold;
    }

    nav {
      background-color: #333;
      padding: 10px;
    }
  </style>
</head>
<body>

  <nav>
    <a href="#">Home</a>
    <div>
      <a href="#">Products</a>   <!-- nested inside a div, but still inside nav -->
      <a href="#">Services</a>
    </div>
  </nav>

  <a href="#">This link is outside nav — not styled</a>

</body>
</html>
```

**Expected Output:**
```
[dark bar with white bold links] Home  Products  Services

This link is outside nav — not styled   ← default blue underlined link
```

The `nav a` selector styles ALL anchor tags anywhere inside `<nav>`, regardless of whether they are direct children or inside nested `<div>` elements.

---

### Example 6 — Child Selector for a List Menu (Avoids Deep Nesting)

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Style only DIRECT children of ul.menu — not nested sub-menu items */
    ul.menu > li {
      list-style-type: none;
      display: inline-block;
      padding: 10px 20px;
      background-color: #4a90d9;
      color: white;
      margin: 2px;
    }
  </style>
</head>
<body>

  <ul class="menu">
    <li>Home</li>
    <li>About
      <ul>
        <li>Team</li>      <!-- NOT styled — this is a child of inner ul, not menu -->
        <li>History</li>   <!-- NOT styled -->
      </ul>
    </li>
    <li>Contact</li>
  </ul>

</body>
</html>
```

**Expected Output (visually):**
```
[blue box: Home]  [blue box: About]  [blue box: Contact]
                     Team               ← plain text, no blue box
                     History            ← plain text, no blue box
```

Using `ul.menu > li` instead of `ul.menu li` (descendant) means only the top-level list items get the blue button styling — the nested sub-menu items are left unstyled.

> **🌍 Real-World Connection:** This exact pattern — `nav ul > li` — is used in almost every multi-level navigation menu on the web to style top-level items differently from sub-menu items.

---

### Example 7 — Adjacent Sibling for a Lead Paragraph

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Style only the first paragraph after each section heading */
    h2 + p {
      font-size: 18px;
      font-style: italic;
      color: #555;
    }

    p {
      font-size: 14px;
      color: #333;
    }
  </style>
</head>
<body>

  <h2>Introduction</h2>
  <p>This is the lead paragraph — larger and italic.</p>
  <p>This is a regular paragraph — smaller and normal.</p>
  <p>Another regular paragraph.</p>

  <h2>Chapter One</h2>
  <p>This is the lead paragraph for Chapter One — larger and italic.</p>
  <p>Back to regular size.</p>

</body>
</html>
```

**Expected Output:**
```
Introduction
  [18px italic grey] This is the lead paragraph — larger and italic.
  [14px normal] This is a regular paragraph — smaller and normal.
  [14px normal] Another regular paragraph.

Chapter One
  [18px italic grey] This is the lead paragraph for Chapter One — larger and italic.
  [14px normal] Back to regular size.
```

The `h2 + p` rule fires once per heading — only the paragraph immediately following the `<h2>` gets the special treatment.

---

### Example 8 — General Sibling for a "Selected" State Effect

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* When a radio button is selected, style all p siblings after it */
    input[type="radio"]:checked ~ p {
      color: green;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <input type="radio" name="demo" id="on">
  <label for="on">Toggle on</label>

  <p>This paragraph changes when the radio is checked!</p>
  <p>So does this one!</p>

</body>
</html>
```

**Expected Output:**
- Before clicking: both paragraphs appear in normal black text.
- After clicking the radio button: both paragraphs turn green and bold.

This uses the `~` combinator with `:checked` pseudo-class to create a CSS-only toggle effect — no JavaScript needed!

---

## Guided Practice Exercises

### Exercise 1 — Warm-Up: Descendant vs. Child

**Objective:** Understand the visual difference between descendant and child combinators.

**Scenario:** You are building a content page with a main article and a sidebar. You want to colour the paragraphs in the article but NOT the paragraphs in the sidebar.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* YOUR TASK: Write a selector here that colours ONLY the
       paragraphs inside #article, NOT those inside #sidebar */

    #article p {
      color: darkblue;
    }
  </style>
</head>
<body>

  <div id="article">
    <p>Article paragraph 1</p>
    <p>Article paragraph 2</p>
    <div class="pull-quote">
      <p>Quoted text inside article</p>
    </div>
  </div>

  <div id="sidebar">
    <p>Sidebar paragraph — should NOT be blue</p>
  </div>

</body>
</html>
```

**Expected Output:**
```
[dark blue] Article paragraph 1
[dark blue] Article paragraph 2
[dark blue] Quoted text inside article   ← styled because it's a DESCENDANT of #article
Sidebar paragraph — should NOT be blue   ← normal black text
```

**Self-check Questions:**
1. The "Quoted text inside article" is inside a `<div class="pull-quote">` which is inside `#article`. Is it styled? Why?
2. What would you change to make `#article > p` instead? Which paragraph would then NOT be styled?
3. Try it: change `#article p` to `#article > p`. What changes?

---

### Exercise 2 — Building a Table of Contents with Sibling Selectors

**Objective:** Use sibling selectors to style headings and the content that follows them.

**Scenario:** You are formatting a recipe page. Each recipe section has an `<h3>` title followed by several elements. You want to:
- Make the first paragraph after each `<h3>` (the description) appear in italic
- Make ALL paragraphs after each `<h3>` have a slightly indented left margin

**Starter Code:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: Georgia, serif;
      max-width: 600px;
      margin: 30px auto;
    }

    /* Adjacent sibling: first p right after h3 — the recipe description */
    h3 + p {
      font-style: italic;
      color: #666;
    }

    /* General sibling: ALL p after h3 — indent them all */
    h3 ~ p {
      margin-left: 20px;
    }
  </style>
</head>
<body>

  <h3>Jollof Rice</h3>
  <p>A rich, smoky one-pot rice dish loved across West Africa.</p>
  <p>Prep time: 20 minutes. Cook time: 45 minutes. Serves: 6.</p>
  <p>Pairs well with fried plantain and grilled chicken.</p>

  <h3>Egusi Soup</h3>
  <p>A hearty melon seed soup with leafy greens and meat or fish.</p>
  <p>Prep time: 30 minutes. Cook time: 1 hour. Serves: 8.</p>

</body>
</html>
```

**Expected Output:**
```
Jollof Rice
  [italic grey indented] A rich, smoky one-pot rice dish loved across West Africa.
  [indented] Prep time: 20 minutes. Cook time: 45 minutes. Serves: 6.
  [indented] Pairs well with fried plantain and grilled chicken.

Egusi Soup
  [italic grey indented] A hearty melon seed soup with leafy greens and meat or fish.
  [indented] Prep time: 30 minutes. Cook time: 1 hour. Serves: 8.
```

**Note:** The first paragraph after each `<h3>` gets BOTH the `h3 + p` style (italic, grey) AND the `h3 ~ p` style (margin-left). This is because it matches both selectors — CSS applies them both!

**Self-check Questions:**
1. Why does the first paragraph get both `font-style: italic` and `margin-left: 20px`?
2. Do the second and third paragraphs get `font-style: italic`? Why or why not?
3. If you added a `<hr>` line between the `<h3>` and the first `<p>`, would the `h3 + p` rule still match? Why or why not?

---

### Exercise 3 — Navigation Menu with Child Combinator

**Objective:** Build a two-level navigation menu where only the top-level items are styled as tab buttons.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Reset */
    * { box-sizing: border-box; margin: 0; padding: 0; }

    .navbar {
      background-color: #2c3e50;
    }

    /* Style ONLY direct children of .navbar > ul — the top-level items */
    .navbar > ul > li {
      display: inline-block;
      padding: 14px 20px;
      color: white;
      font-family: Arial, sans-serif;
      font-size: 15px;
      cursor: pointer;
      position: relative;
    }

    .navbar > ul > li:hover {
      background-color: #e74c3c;
    }

    /* Sub-menu styling — nested uls */
    .navbar ul {
      list-style: none;
    }

    .navbar > ul > li > ul {
      display: none;
      position: absolute;
      background-color: #34495e;
      top: 100%;
      left: 0;
      min-width: 150px;
    }

    .navbar > ul > li:hover > ul {
      display: block;
    }

    .navbar > ul > li > ul > li {
      display: block;
      padding: 10px 15px;
      color: #ccc;
      font-size: 14px;
    }

    .navbar > ul > li > ul > li:hover {
      background-color: #e74c3c;
      color: white;
    }
  </style>
</head>
<body>

  <nav class="navbar">
    <ul>
      <li>Home</li>
      <li>Products
        <ul>
          <li>Laptops</li>
          <li>Tablets</li>
          <li>Phones</li>
        </ul>
      </li>
      <li>About</li>
      <li>Contact</li>
    </ul>
  </nav>

  <p style="padding: 20px;">Hover over "Products" to see the sub-menu.</p>

</body>
</html>
```

**Expected Output:**
```
[dark bar] Home  Products  About  Contact

(On hover over Products, a dropdown appears:)
  Laptops
  Tablets
  Phones
```

**Self-check Questions:**
1. Why do we use `.navbar > ul > li` instead of `.navbar li`? What would break if we used the descendant combinator instead?
2. What does `position: relative` on the parent `<li>` and `position: absolute` on the sub-menu `<ul>` achieve?
3. Can you add another top-level item called "Blog" with two sub-items: "News" and "Tutorials"?

---

## Mini Project — Styled Article Page Using All Four Combinators

In this project, you will style a complete news article page using all four CSS combinators in a meaningful, practical way.

### Project Overview

You are building the article detail page for a fictional online magazine called **"The Codebreaker"**. The article page needs:
- Body text paragraphs styled in dark grey
- The first paragraph after each section heading styled as a "lead paragraph" (larger, italic)
- All paragraphs following section headings indented
- Navigation links styled using descendant combinator
- Section headings and their direct content styled differently from the main body

---

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html>
<head>
  <title>The Codebreaker — Article</title>
  <link rel="stylesheet" href="article.css">
</head>
<body>

  <!-- Navigation using descendant combinator -->
  <nav id="top-nav">
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">Tech</a></li>
      <li><a href="#">Science</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  </nav>

  <!-- Article content using all combinators -->
  <article id="main-article">

    <h1>How CSS Changed the Web Forever</h1>
    <p class="meta">Published by Ada Okafor · April 2026</p>

    <h2>The Beginning</h2>
    <p>Before CSS, all styling was done inline or with HTML attributes. Pages were messy, hard to maintain, and looked identical everywhere.</p>
    <p>CSS was introduced to separate structure from presentation, making web development cleaner and more powerful.</p>
    <p>Today, CSS is used by millions of developers worldwide to build beautiful, responsive interfaces.</p>

    <h2>The Revolution</h2>
    <p>When CSS2 arrived, developers gained new tools for layout, positioning, and more expressive typography.</p>
    <p>It allowed a single stylesheet to control the appearance of hundreds of pages simultaneously.</p>

    <h2>What Comes Next</h2>
    <p>CSS continues to evolve with features like Grid, Flexbox, custom properties, and container queries.</p>
    <p>The future is bright for web designers and developers who invest time in mastering this language.</p>

  </article>

  <!-- Sidebar using child combinator -->
  <aside id="sidebar">
    <h3>Related Articles</h3>
    <ul>
      <li><a href="#">Understanding Flexbox</a></li>
      <li><a href="#">CSS Grid Complete Guide</a></li>
      <li><a href="#">The History of HTML</a></li>
    </ul>
  </aside>

</body>
</html>
```

---

### Stage 2 — CSS Using All Four Combinators

Create `article.css`:

```css
/* --- Base Reset --- */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Georgia, serif;
  background-color: #f9f9f9;
  color: #333;
  padding: 20px;
  max-width: 900px;
  margin: 0 auto;
}

/* ====================================
   COMBINATOR 1: DESCENDANT SELECTOR
   Selects all <a> links anywhere inside #top-nav
   ==================================== */
#top-nav a {
  color: white;
  text-decoration: none;
  padding: 0 15px;
  font-family: Arial, sans-serif;
  font-size: 15px;
}

#top-nav {
  background-color: #1a1a2e;
  padding: 12px 0;
  margin-bottom: 30px;
}

#top-nav ul {
  list-style: none;
}

#top-nav ul li {
  display: inline-block;
}

#top-nav a:hover {
  color: #e94560;
}


/* ====================================
   COMBINATOR 2: CHILD SELECTOR
   Selects only DIRECT <p> children of #main-article
   This does NOT affect .meta which is also a <p>
   ==================================== */
#main-article > p {
  font-size: 13px;
  color: #888;
  margin-bottom: 20px;
  font-family: Arial, sans-serif;
}

/* ====================================
   COMBINATOR 3: ADJACENT SIBLING SELECTOR
   The FIRST paragraph right after any h2 — lead paragraph
   ==================================== */
h2 + p {
  font-size: 18px;
  font-style: italic;
  color: #444;
  line-height: 1.7;
  margin-bottom: 12px;
}

/* ====================================
   COMBINATOR 4: GENERAL SIBLING SELECTOR
   ALL paragraphs after any h2 — general article body text
   ==================================== */
h2 ~ p {
  font-size: 15px;
  color: #555;
  line-height: 1.8;
  margin-bottom: 12px;
  margin-left: 10px;
}

/* Headings */
h1 {
  font-size: 32px;
  color: #1a1a2e;
  margin-bottom: 5px;
}

h2 {
  font-size: 22px;
  color: #e94560;
  margin-top: 30px;
  margin-bottom: 10px;
  border-bottom: 2px solid #e94560;
  padding-bottom: 5px;
}

h3 {
  font-size: 18px;
  color: #333;
  margin-bottom: 10px;
}

/* Sidebar */
#sidebar {
  margin-top: 40px;
  padding: 20px;
  background-color: #eef2ff;
  border-left: 4px solid #4a90d9;
}

#sidebar ul {
  list-style: none;
  margin-top: 10px;
}

#sidebar ul li {
  margin-bottom: 8px;
}

/* Descendant combinator — all links in sidebar */
#sidebar a {
  color: #4a90d9;
  text-decoration: none;
  font-family: Arial, sans-serif;
  font-size: 14px;
}

#sidebar a:hover {
  text-decoration: underline;
}
```

---

### Stage 3 — Full Combined File (All-in-One Version)

```html
<!DOCTYPE html>
<html>
<head>
  <title>The Codebreaker — Article</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: Georgia, serif;
      background-color: #f9f9f9;
      color: #333;
      padding: 20px;
      max-width: 860px;
      margin: 0 auto;
    }

    /* DESCENDANT: all links in nav */
    #top-nav a {
      color: white;
      text-decoration: none;
      padding: 0 15px;
      font-family: Arial, sans-serif;
      font-size: 15px;
    }
    #top-nav { background-color: #1a1a2e; padding: 12px 0; margin-bottom: 30px; }
    #top-nav ul { list-style: none; }
    #top-nav ul li { display: inline-block; }
    #top-nav a:hover { color: #e94560; }

    /* CHILD: direct p child of article (the .meta line only) */
    #main-article > p {
      font-size: 13px;
      color: #888;
      margin-bottom: 20px;
      font-family: Arial, sans-serif;
    }

    /* ADJACENT SIBLING: first p after h2 = lead paragraph */
    h2 + p {
      font-size: 18px;
      font-style: italic;
      color: #444;
      line-height: 1.7;
      margin-bottom: 12px;
    }

    /* GENERAL SIBLING: all p after h2 = body text */
    h2 ~ p {
      font-size: 15px;
      color: #555;
      line-height: 1.8;
      margin-bottom: 12px;
      margin-left: 10px;
    }

    h1 { font-size: 32px; color: #1a1a2e; margin-bottom: 5px; }
    h2 { font-size: 22px; color: #e94560; margin-top: 30px; margin-bottom: 10px; border-bottom: 2px solid #e94560; padding-bottom: 5px; }
    h3 { font-size: 18px; color: #333; margin-bottom: 10px; }

    #sidebar { margin-top: 40px; padding: 20px; background-color: #eef2ff; border-left: 4px solid #4a90d9; }
    #sidebar ul { list-style: none; margin-top: 10px; }
    #sidebar ul li { margin-bottom: 8px; }

    /* DESCENDANT: all links in sidebar */
    #sidebar a { color: #4a90d9; text-decoration: none; font-family: Arial, sans-serif; font-size: 14px; }
    #sidebar a:hover { text-decoration: underline; }
  </style>
</head>
<body>

  <nav id="top-nav">
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">Tech</a></li>
      <li><a href="#">Science</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  </nav>

  <article id="main-article">
    <h1>How CSS Changed the Web Forever</h1>
    <p class="meta">Published by Ada Okafor · April 2026</p>

    <h2>The Beginning</h2>
    <p>Before CSS, all styling was done inline or with HTML attributes. Pages were messy and hard to maintain.</p>
    <p>CSS was introduced to separate structure from presentation, making web development cleaner and more powerful.</p>
    <p>Today, CSS is used by millions of developers worldwide to build beautiful, responsive interfaces.</p>

    <h2>The Revolution</h2>
    <p>When CSS2 arrived, developers gained new tools for layout, positioning, and expressive typography.</p>
    <p>It allowed a single stylesheet to control the appearance of hundreds of pages simultaneously.</p>

    <h2>What Comes Next</h2>
    <p>CSS continues to evolve with Grid, Flexbox, custom properties, and container queries.</p>
    <p>The future is bright for developers who invest in mastering this language.</p>
  </article>

  <aside id="sidebar">
    <h3>Related Articles</h3>
    <ul>
      <li><a href="#">Understanding Flexbox</a></li>
      <li><a href="#">CSS Grid Complete Guide</a></li>
      <li><a href="#">The History of HTML</a></li>
    </ul>
  </aside>

</body>
</html>
```

**Milestone Output:**
```
[dark nav bar] Home  Tech  Science  Contact

How CSS Changed the Web Forever
[small grey] Published by Ada Okafor · April 2026

[red underline] The Beginning
  [18px italic] Before CSS, all styling was done inline or with HTML attributes...
  [15px indented] CSS was introduced to separate...
  [15px indented] Today, CSS is used by...

[red underline] The Revolution
  [18px italic] When CSS2 arrived...
  [15px indented] It allowed a single stylesheet...

[blue sidebar]
  Related Articles
  Understanding Flexbox
  CSS Grid Complete Guide
  The History of HTML
```

**Reflection Questions:**
1. Which combinator made the `.meta` paragraph (the "Published by..." line) look different from the section paragraphs?
2. The `h2 + p` rule and `h2 ~ p` rule both match the first paragraph after `h2`. Which styles win for each property?
3. If you moved the `<p class="meta">` line to be after the `<h1>`, would `h2 + p` still match it? Why or why not?

**Optional advanced extensions:**
- Add a `blockquote` inside one section. Use a sibling combinator to style the paragraph immediately after the blockquote differently.
- Use `article > h2` to style only the `h2` elements that are direct children of `<article>`.
- Add a second-level `<ul>` inside the sidebar's `<ul>` and use `.sidebar > ul > li` to style only the top-level items.

---

## Common Beginner Mistakes

### Mistake 1 — Confusing Descendant (space) with Child (`>`)

```css
/* WRONG intent: want to style only direct children */
div p {    /* ← This styles ALL p descendants, not just direct children */
  color: red;
}

/* CORRECT: use > for direct children only */
div > p {
  color: red;
}
```

**When this bites you:** You style a nav bar's top-level items, but the nested sub-menu items also get the same style unexpectedly.

---

### Mistake 2 — Expecting `+` to Match When There Is an Element In Between

```html
<h2>Title</h2>
<span>Some note</span>   <!-- ← This breaks the adjacency! -->
<p>Lead paragraph</p>   <!-- h2 + p will NOT match this -->
```

```css
/* This will NOT work because span is between h2 and p */
h2 + p {
  font-style: italic;
}
```

**Fix:** Either remove the element in between, or use `h2 ~ p` if you don't need strict adjacency.

---

### Mistake 3 — Expecting `~` to Work Backwards

```html
<p>This comes BEFORE h2</p>
<h2>Heading</h2>
<p>This comes AFTER h2</p>
```

```css
/* h2 ~ p only styles p that come AFTER h2, never before */
h2 ~ p {
  color: green;
}
/* Result: only the SECOND <p> is green — the first <p> is NOT affected */
```

**Why this happens:** All sibling combinators (`+` and `~`) only look **forward** in the document — they never look backward.

---

### Mistake 4 — Confusing `+` (one sibling) with `~` (all siblings)

```css
/* Styles only the FIRST p after h2 */
h2 + p { font-size: 20px; }

/* Styles ALL p elements after h2 */
h2 ~ p { font-size: 20px; }
```

Beginners often write `h2 + p` when they mean "all paragraphs after a heading." If you want all of them, use `~`.

---

### Mistake 5 — Forgetting That Combinators Style the SECOND Element

```css
/* This does NOT change the div — it changes the p */
div p {
  color: red;
}
```

The `div` is used to **set the context** (the p must be inside a div). The `div` itself is not styled by this rule. Only the `<p>` gets `color: red`.

---

### Mistake 6 — Writing Extra Spaces Where They Change Meaning

```css
div>p { ... }    /* Valid — same as div > p */
div > p { ... }  /* Valid — spaces around > are optional */
divp { ... }     /* INVALID — this reads as a selector for <divp> element! */
```

Always make sure there is either a proper combinator symbol (`>`, `+`, `~`) or a clear space between selectors. No space and no symbol means the browser treats it as one single selector name.

---

## Reflection Questions

1. **What is a combinator?** Write a one-sentence definition in your own words.

2. **You have this HTML:** `<div><p>Hello</p></div>`. Write a selector that targets the `<p>` using the descendant combinator. Then write one using the child combinator. What is the difference?

3. **Which combinator would you use** if you want to style only the `<p>` immediately after an `<h3>`?

4. **Which combinator would you use** if you want to style all the `<li>` items that appear after a `<hr>` inside the same `<ul>`?

5. **You write `nav > a` but the links are not being styled.** You look at the HTML and find `<nav><ul><li><a>Link</a></li></ul></nav>`. Why doesn't the selector work, and how would you fix it?

6. **Both `h2 + p` and `h2 ~ p` match the first paragraph after an `<h2>`.** If `h2 + p` sets `font-size: 20px` and `h2 ~ p` sets `font-size: 16px`, which `font-size` wins for the first paragraph? Why? (Hint: think about specificity and order of rules.)

7. **Name a real-world scenario** where the child combinator (`>`) is more useful than the descendant combinator (` `).

---

## Completion Checklist

Before moving on to the next lesson, confirm you can do all of the following:

- [ ] Explain what a combinator is and why it is useful
- [ ] Understand the HTML tree (parent, child, descendant, sibling concepts)
- [ ] Write and explain the descendant selector (space) and know it selects at ALL depth levels
- [ ] Write and explain the child selector (`>`) and know it selects ONLY direct children
- [ ] Write and explain the adjacent sibling selector (`+`) and know it selects the ONE immediately following sibling
- [ ] Write and explain the general sibling selector (`~`) and know it selects ALL following siblings
- [ ] Know the critical difference between `+` (one) and `~` (all)
- [ ] Know that sibling combinators only look **forward**, not backward
- [ ] Build a styled navigation menu using the child combinator to differentiate levels
- [ ] Build an article page that uses all four combinators together
- [ ] Identify and fix the six common mistakes described in this lesson

---

## Lesson Summary

In this lesson, you mastered all four CSS combinators — the tools that let you target elements based on their **relationship** to other elements in the HTML structure.

**The Four Combinators at a Glance:**

| Combinator | Symbol | Selects | Example |
|---|---|---|---|
| Descendant | ` ` (space) | Any matching element inside the first, at any depth | `div p` |
| Child | `>` | Only direct children of the first | `ul > li` |
| Adjacent Sibling | `+` | The one immediately following sibling | `h2 + p` |
| General Sibling | `~` | All following siblings | `h2 ~ p` |

**The big idea:** Instead of adding a class to every element you want to style, combinators let you describe **where** an element is in relation to another element, and CSS handles the targeting automatically. This keeps your HTML cleaner and your CSS smarter.

**Critical rules to remember:**
- `div p` (space) goes **as deep as needed** — it finds p tags no matter how many levels down
- `div > p` stops at **one level** — it only finds direct children
- `h2 + p` matches **only one** element — the immediately following sibling
- `h2 ~ p` matches **all elements** — every following sibling of the right type
- Both `+` and `~` only look **forward** — they never match elements that come before

**Real-world significance:** Combinators are used in virtually every serious CSS file — for styling navigation menus, article typography, form layouts, table structures, and interactive widget states. Mastering them means you can write precise, efficient CSS without cluttering your HTML with extra classes.

---

*End of Lesson 28 — You are now ready to move on to CSS Pseudo-classes in Lesson 29!*
