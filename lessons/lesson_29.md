---
render_with_liquid: false
title: "CSS Pseudo-classes: Styling Elements by State, Position, and Interaction"
nav_order: 29
---

# Lesson 29 — CSS Pseudo-classes: Styling Elements by State, Position, and Interaction

---

## Lesson Introduction

Have you ever noticed that a link on a website changes colour when you hover over it with your mouse? Or that a text box glows when you click inside it? Or that the first paragraph on a page looks slightly different from the rest?

All of those effects are created using something called **CSS pseudo-classes**.

A **pseudo-class** is a special keyword you add to a CSS selector that lets you style an element **based on its current state or its position** in the document — without changing the HTML at all.

Think of it like a smart rule:
> "Style this button **only when the user is hovering over it**."
> "Style this list item **only if it is the first one**."
> "Style this input **only when it contains invalid data**."

In this lesson you will learn:
- What pseudo-classes are and why they exist
- How to write pseudo-class syntax correctly
- How to style links in all their different states
- How to respond to user interactions like hover, focus, and clicks
- How to target elements by their position in a list or group
- How to style form inputs based on their validation state
- How to combine multiple pseudo-classes for powerful effects

By the end of this lesson you will be able to build interactive, state-aware, and position-based CSS styling — skills used in every modern website and web application.

---

## Prerequisite Concepts

Before diving in, make sure you are comfortable with the following ideas. If anything feels unfamiliar, read the short explanation provided.

### What Is a CSS Selector?

A **CSS selector** is the part of a CSS rule that targets which HTML element to style.

```css
p {
  color: blue;
}
```

In this example, `p` is the selector. It targets all `<p>` (paragraph) elements.

### What Is an HTML Element's "State"?

Elements on a webpage can exist in different **states** depending on what the user is doing or what the HTML structure looks like. For example:

- A link can be **unvisited**, **visited**, **hovered**, or **actively clicked**
- An input field can be **focused** (cursor is inside it) or **blurred** (cursor has moved away)
- An item in a list can be the **first item**, the **last item**, or the **third item**

Pseudo-classes give you a way to target and style those specific states.

---

## Part 1 — What Are CSS Pseudo-classes?

### The Simple Definition

A **CSS pseudo-class** is a keyword added to a selector, preceded by a colon (`:`), that defines a special state or condition of the selected element.

### The Syntax

```css
selector:pseudo-class {
  property: value;
}
```

Let's break this down piece by piece:

| Part | Meaning |
|---|---|
| `selector` | The HTML element you are targeting (e.g., `a`, `p`, `button`) |
| `:` | The colon separates the selector from the pseudo-class |
| `pseudo-class` | The keyword describing the state or condition (e.g., `hover`, `first-child`) |
| `{ property: value; }` | The CSS styles to apply when the condition is true |

### A Real-World Analogy

Imagine a traffic light. The same physical light can be in three different **states**: red, yellow, or green. Depending on its state, it shows a different colour.

A pseudo-class works the same way. The same element (the traffic light) gets different styling depending on its current state.

---

## Part 2 — Link Pseudo-classes

### Why Links Need Special Styling

In HTML, a link (`<a>` element) can be in four distinct states:

| State | Meaning |
|---|---|
| `:link` | The link has never been visited by the user |
| `:visited` | The link has been visited before |
| `:hover` | The user's mouse cursor is currently over the link |
| `:active` | The link is being clicked right now (mouse button is pressed down) |

These four states can all look different, giving users helpful visual feedback.

### Syntax for Link States

```css
/* Unvisited link */
a:link {
  color: blue;
}

/* Visited link */
a:visited {
  color: purple;
}

/* Mouse is hovering over the link */
a:hover {
  color: red;
}

/* Link is being actively clicked */
a:active {
  color: orange;
}
```

**Expected result in the browser:**
- Links you've never clicked: blue
- Links you have clicked before: purple
- When you hover your mouse over any link: it turns red
- When you click and hold the mouse on a link: it turns orange

> **Important Rule — The LVHA Order!**
> When styling all four link states, always write them in this exact order:
> 1. `:link`
> 2. `:visited`
> 3. `:hover`
> 4. `:active`
>
> If you put them in a different order, some states may not work correctly because of CSS specificity and cascade rules. Remember the word **LVHA** to keep this order in mind.

### Simple Example: Basic Link Styling

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    a:link    { color: blue;   text-decoration: none; }
    a:visited { color: gray;   text-decoration: none; }
    a:hover   { color: red;    text-decoration: underline; }
    a:active  { color: orange; }
  </style>
</head>
<body>
  <a href="https://example.com">Visit Example.com</a>
</body>
</html>
```

**What happens:**
- The link appears blue with no underline
- After you visit it, it becomes gray
- Hovering your mouse turns it red and adds an underline
- Clicking and holding turns it orange

> **Thinking prompt:** What would happen if you swapped `:hover` and `:active` in the order? Try it and observe the result.

---

### Using :hover on Non-Link Elements

`:hover` is not limited to links! You can apply it to **any** HTML element.

```css
/* A paragraph that changes background when hovered */
p:hover {
  background-color: lightyellow;
}

/* A button that changes colour when hovered */
button:hover {
  background-color: darkblue;
  color: white;
}

/* A div that grows a border on hover */
div:hover {
  border: 2px solid tomato;
}
```

This is extremely useful for making interactive cards, menus, and buttons.

---

## Part 3 — Interactive Pseudo-classes

Interactive pseudo-classes respond to what the **user is currently doing** with an element.

### :hover

You already met `:hover`. It applies styles when the mouse pointer is positioned over an element.

```css
.card:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  transform: translateY(-2px);
}
```

**Use case:** Card hover effects on product pages, portfolio sites, and dashboards.

---

### :focus

`:focus` applies styles to an element that has received **keyboard focus** — meaning the user has clicked inside it or tabbed into it using the keyboard.

This is most commonly used with **form inputs**.

```css
input:focus {
  border: 2px solid blue;
  outline: none;
  background-color: #f0f8ff;
}
```

**Expected result:** When the user clicks inside the input field, it gets a blue border and a light blue background.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    input {
      border: 1px solid gray;
      padding: 8px;
      font-size: 16px;
    }
    input:focus {
      border: 2px solid royalblue;
      outline: none;
      background-color: #eef4ff;
    }
  </style>
</head>
<body>
  <input type="text" placeholder="Click here to type...">
</body>
</html>
```

> **Real-world use:** Almost every modern form uses `:focus` styling to help users know which field they are currently editing. It also helps users who navigate by keyboard (for accessibility).

---

### :focus-within

`:focus-within` applies to a **parent element** when any of its children are focused.

```css
.form-group:focus-within {
  background-color: #f5f5ff;
  border-radius: 4px;
}
```

**Scenario:** You have a form group with a label and an input. When the user focuses the input, the entire group (including the label) changes background.

```html
<div class="form-group">
  <label>Email Address</label>
  <input type="email" placeholder="you@example.com">
</div>
```

When the input inside `.form-group` is focused, the whole `div` will have a light purple background.

---

### :focus-visible

`:focus-visible` applies focus styles only when the element was focused via **keyboard navigation**, not when clicked with a mouse. This is important for accessibility because keyboard users need visible focus indicators, but mouse users often prefer no outline.

```css
button:focus {
  outline: none;   /* Remove default outline for everyone */
}

button:focus-visible {
  outline: 3px solid royalblue;  /* Show outline only for keyboard users */
}
```

---

### :active

`:active` applies styles to an element **at the exact moment it is being clicked** (the moment the mouse button is pressed down, before it is released).

```css
button:active {
  background-color: darkblue;
  transform: scale(0.97);
}
```

**Use case:** Making buttons appear to "press down" when clicked, giving tactile visual feedback.

---

### :checked

`:checked` applies to **checkboxes** and **radio buttons** that are currently selected/checked.

```css
input[type="checkbox"]:checked {
  accent-color: green;
}

input[type="radio"]:checked + label {
  font-weight: bold;
  color: green;
}
```

> **Tip:** The `+` in the second rule above is the **adjacent sibling combinator** — it targets the `<label>` that comes immediately after the checked radio button.

---

### :enabled and :disabled

`:enabled` targets form elements that are available for interaction.
`:disabled` targets form elements that have been disabled.

```html
<input type="text" placeholder="I am enabled">
<input type="text" placeholder="I am disabled" disabled>
```

```css
input:enabled {
  background-color: white;
  color: black;
}

input:disabled {
  background-color: #e0e0e0;
  color: #999;
  cursor: not-allowed;
}
```

**Expected result:**
- The first input looks normal
- The second input has a gray background, lighter text, and shows a "not allowed" cursor on hover

---

### :read-only and :read-write

`:read-only` targets elements that cannot be edited by the user.
`:read-write` targets elements that can be edited.

```html
<input type="text" value="You can edit this">
<input type="text" value="You cannot edit this" readonly>
```

```css
input:read-write {
  background-color: white;
  border: 1px solid #aaa;
}

input:read-only {
  background-color: #f9f9f9;
  border: 1px dashed #ccc;
  color: #666;
}
```

---

### Form Validation Pseudo-classes

These are incredibly powerful pseudo-classes for giving users instant visual feedback about their form input.

#### :required and :optional

```html
<input type="email" required placeholder="Required email">
<input type="text" placeholder="Optional field">
```

```css
input:required {
  border-left: 4px solid red;
}

input:optional {
  border-left: 4px solid lightgray;
}
```

**Expected result:** Required fields have a red left border; optional ones have a gray border.

---

#### :valid and :invalid

`:valid` applies when a form field contains valid data.
`:invalid` applies when a form field contains invalid data.

```html
<input type="email" placeholder="Enter your email">
```

```css
input:valid {
  border: 2px solid green;
  background-color: #f0fff0;
}

input:invalid {
  border: 2px solid red;
  background-color: #fff0f0;
}
```

**What happens:**
- As soon as you type a valid email address (with `@` and a domain), the border turns green
- If the text is not a valid email, the border stays red

> **Thinking prompt:** What happens to a required field that is empty — is it valid or invalid? Try it!

---

#### :in-range and :out-of-range

These apply to `<input>` elements with `min` and `max` attributes.

```html
<input type="number" min="1" max="10" value="5">
```

```css
input:in-range {
  border: 2px solid green;
}

input:out-of-range {
  border: 2px solid red;
}
```

**Expected result:**
- If the user types `5` (between 1 and 10): green border
- If the user types `15` (above 10): red border

---

#### :placeholder-shown

`:placeholder-shown` applies to an input field **while its placeholder text is visible** (meaning the field is empty).

```css
input:placeholder-shown {
  background-color: #fffde7;
  font-style: italic;
}

input:not(:placeholder-shown) {
  background-color: white;
  font-style: normal;
}
```

**What this means:**
- While the field is empty (placeholder is showing): yellow background and italic style
- Once the user starts typing (placeholder disappears): normal white background

---

## Part 4 — Structural Pseudo-classes

Structural pseudo-classes let you target elements **based on their position or relationship** within their parent element's children.

### Understanding "Parent" and "Children"

In HTML, elements are nested inside each other. The outer element is the **parent** and the inner elements are its **children**.

```html
<ul>          <!-- ul is the parent -->
  <li>Apple</li>    <!-- First child -->
  <li>Banana</li>   <!-- Second child -->
  <li>Cherry</li>   <!-- Third child -->
</ul>
```

Structural pseudo-classes let you say things like: "Style only the first `<li>`" or "Style every second `<li>`."

---

### :first-child

`:first-child` targets an element **only if it is the first child** of its parent.

```css
li:first-child {
  color: tomato;
  font-weight: bold;
}
```

**Expected result:**
- "Apple" (first child) → red and bold
- "Banana" and "Cherry" → default styling

---

### :last-child

`:last-child` targets an element **only if it is the last child** of its parent.

```css
li:last-child {
  color: steelblue;
  border-bottom: none;
}
```

**Expected result:**
- "Cherry" (last child) → blue text, no bottom border
- "Apple" and "Banana" → default styling

---

### :nth-child()

`:nth-child(n)` is the most flexible structural pseudo-class. It lets you target **any child element by its position number**, or by a pattern.

**Syntax:**
```css
selector:nth-child(n)
```

Where `n` can be:
- A specific number: `2` → second child
- A keyword: `odd` → every odd-positioned child (1st, 3rd, 5th...)
- A keyword: `even` → every even-positioned child (2nd, 4th, 6th...)
- A formula: `2n` → every 2nd child (same as `even`)
- A formula: `3n` → every 3rd child
- A formula: `2n+1` → every odd child (same as `odd`)

#### Example 1 — Target the second child

```css
li:nth-child(2) {
  background-color: yellow;
}
```

**Output:** Only "Banana" (2nd child) gets a yellow background.

---

#### Example 2 — Zebra striping a table

```css
tr:nth-child(odd) {
  background-color: #f9f9f9;
}

tr:nth-child(even) {
  background-color: #ffffff;
}
```

**Output:** Alternating light-gray and white rows — a very common table style.

---

#### Example 3 — Every third item

```css
li:nth-child(3n) {
  font-weight: bold;
}
```

**Output:** Items 3, 6, 9, 12... are bolded.

---

### :nth-last-child()

`:nth-last-child(n)` works exactly like `:nth-child()` but counts **from the end** instead of from the beginning.

```css
li:nth-last-child(1) {
  color: purple;
}
```

This targets the **last child**, same as `:last-child`. But it becomes very useful with formulas:

```css
li:nth-last-child(2) {
  color: teal;
}
```

This targets the **second-to-last** child.

---

### :first-of-type

`:first-of-type` targets the **first element of a specific tag type** inside its parent — even if there are other element types before it.

This is different from `:first-child`! Look at this example:

```html
<div>
  <span>I am a span</span>   <!-- First child, but NOT a p -->
  <p>First paragraph</p>     <!-- Second child, but first p -->
  <p>Second paragraph</p>
</div>
```

```css
p:first-child {
  color: red;
}
/* This does NOT work — p is not the first child, span is! */

p:first-of-type {
  color: red;
}
/* This WORKS — it targets the first p regardless of what comes before it */
```

---

### :last-of-type

Targets the **last element of a specific tag type** inside its parent.

```css
p:last-of-type {
  margin-bottom: 0;
}
```

Very useful for removing the bottom margin from the last paragraph in a container.

---

### :nth-of-type()

Works like `:nth-child()` but counts only elements of the **same tag type**.

```css
p:nth-of-type(2) {
  font-style: italic;
}
```

This targets the second `<p>` inside its parent, ignoring any `<h1>`, `<span>`, or other tag types in the count.

---

### :nth-last-of-type()

Counts from the end, filtering by element type.

```css
p:nth-last-of-type(1) {
  color: navy;
}
```

Targets the last `<p>` element.

---

### :only-child

`:only-child` targets an element **only if it is the only child** of its parent (i.e., it has no siblings).

```html
<div class="box">
  <p>I am the only paragraph here.</p>
</div>
```

```css
p:only-child {
  font-size: 1.3em;
  font-style: italic;
}
```

If the `<div>` had more than one child, this rule would not apply.

---

### :only-of-type

`:only-of-type` targets an element if it is the **only element of its type** inside its parent (even if there are other element types).

```html
<div>
  <h2>Title</h2>
  <p>Only one paragraph here.</p>
  <span>A span</span>
</div>
```

```css
p:only-of-type {
  background-color: lightyellow;
}
```

This works because `<p>` is the only paragraph in the div, even though there are other elements.

---

### :empty

`:empty` targets an element that has **no children and no text content at all**.

```css
div:empty {
  display: none;
}

td:empty {
  background-color: #f5f5f5;
}
```

**Use case:** Hiding empty containers, or styling empty table cells with a subtle background.

---

### :root

`:root` targets the **highest-level parent element** in the document — in HTML, that is always the `<html>` element.

It is commonly used to define **CSS custom properties (variables)** that apply globally.

```css
:root {
  --primary-color: #3498db;
  --font-size-base: 16px;
  --max-width: 1200px;
}
```

These variables (prefixed with `--`) can then be reused anywhere in your CSS:

```css
h1 {
  color: var(--primary-color);
}

body {
  font-size: var(--font-size-base);
}
```

---

### :target

`:target` applies to an element whose **ID matches the URL fragment** (the part after the `#` in the URL).

**How it works:**

If your page URL is `mypage.html#section2`, then the element with `id="section2"` is the **target**.

```html
<h2 id="section2">About Us</h2>
```

```css
:target {
  background-color: lightyellow;
  border-left: 4px solid gold;
  padding-left: 12px;
}
```

**Expected result:** When a user navigates to `#section2` (by clicking an anchor link), that heading gets a yellow background and a gold border.

**Real-world use:** Highlighting anchor sections in documentation pages, FAQs, and table-of-contents navigation.

---

### :not() — The Negation Pseudo-class

`:not()` targets every element that does **NOT** match the selector inside the parentheses.

```css
/* Style all paragraphs EXCEPT those with the class "special" */
p:not(.special) {
  color: gray;
}

/* Style all inputs EXCEPT submit buttons */
input:not([type="submit"]) {
  border: 1px solid #ccc;
}
```

This is extremely useful to apply "fallback" or "default" styles to all elements except specific ones.

---

## Part 5 — The :lang Pseudo-class

`:lang()` targets elements based on their **language attribute**.

```html
<p lang="fr">Bonjour le monde.</p>
<p lang="en">Hello, world.</p>
```

```css
p:lang(fr) {
  font-style: italic;
  quotes: "« " " »";
}

p:lang(en) {
  font-style: normal;
}
```

**Use case:** Multilingual websites that need different typographic rules for different languages.

---

## Part 6 — Combining Pseudo-classes

You can chain multiple pseudo-classes together, or combine them with other selectors, to create very precise targeting.

### Chaining Two Pseudo-classes

```css
/* A link that is both visited AND hovered */
a:visited:hover {
  color: darkviolet;
}

/* A list item that is the first child AND hovered */
li:first-child:hover {
  background-color: lightyellow;
}
```

### Combining with Class Selectors

```css
/* Only .btn elements when hovered */
.btn:hover {
  background-color: darkblue;
}

/* Only .required-field inputs that are invalid */
.required-field:invalid {
  border-color: crimson;
}
```

### Combining with Combinators

```css
/* The first paragraph inside an article */
article p:first-of-type {
  font-size: 1.1em;
  font-weight: 500;
}

/* Every odd row in a table body */
tbody tr:nth-child(odd) {
  background-color: #f5f5f5;
}
```

---

## Part 7 — Complete Reference Table of Pseudo-classes

| Pseudo-class | What It Targets |
|---|---|
| `:link` | Unvisited links |
| `:visited` | Visited links |
| `:hover` | Element being hovered by mouse |
| `:active` | Element being actively clicked |
| `:focus` | Element with keyboard/click focus |
| `:focus-within` | Parent when any child is focused |
| `:focus-visible` | Element focused via keyboard (not mouse) |
| `:checked` | Checked checkboxes or radio buttons |
| `:enabled` | Enabled form elements |
| `:disabled` | Disabled form elements |
| `:read-only` | Elements with `readonly` attribute |
| `:read-write` | Editable elements |
| `:required` | Inputs with `required` attribute |
| `:optional` | Inputs without `required` attribute |
| `:valid` | Inputs with valid data |
| `:invalid` | Inputs with invalid data |
| `:in-range` | Number inputs within min/max range |
| `:out-of-range` | Number inputs outside min/max range |
| `:placeholder-shown` | Inputs with visible placeholder |
| `:first-child` | First child of parent |
| `:last-child` | Last child of parent |
| `:nth-child(n)` | Child at position n |
| `:nth-last-child(n)` | Child at position n from end |
| `:first-of-type` | First element of its tag type in parent |
| `:last-of-type` | Last element of its tag type in parent |
| `:nth-of-type(n)` | nth element of its tag type |
| `:nth-last-of-type(n)` | nth element of tag type from end |
| `:only-child` | Element that is the only child |
| `:only-of-type` | Element that is the only one of its type |
| `:empty` | Elements with no children/text |
| `:root` | The root `<html>` element |
| `:target` | Element targeted by URL fragment (#id) |
| `:not(x)` | Elements that do NOT match selector x |
| `:lang(x)` | Elements with a specific language |

---

## Guided Practice Exercises

### Exercise 1 — Style a Navigation Menu

**Objective:** Create a navigation menu where links change appearance based on their state.

**Scenario:** You are building a simple website navigation bar with 4 links.

**HTML to use:**
```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Write your CSS here */
  </style>
</head>
<body>
  <nav>
    <a href="#home">Home</a>
    <a href="#about">About</a>
    <a href="#services">Services</a>
    <a href="#contact">Contact</a>
  </nav>
</body>
</html>
```

**Steps:**
1. Style all unvisited links: `color: #333; text-decoration: none; padding: 8px 16px;`
2. Style visited links: `color: #999;`
3. Style hovered links: `color: white; background-color: #333;`
4. Style actively clicked links: `color: white; background-color: black;`

**Expected output:**
- Links appear dark gray, no underline
- Visited links become light gray
- Hovering turns the link into a white-text, dark-background button-like style
- Clicking turns the background black

**Self-check questions:**
- Did you use the LVHA order?
- What happens if you remove the `padding` from the base style?

---

### Exercise 2 — Accessible Form Inputs

**Objective:** Style form inputs to give users clear visual feedback.

**HTML to use:**
```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Write your CSS here */
  </style>
</head>
<body>
  <form>
    <div>
      <label>Name:</label>
      <input type="text" required placeholder="Your full name">
    </div>
    <div>
      <label>Email:</label>
      <input type="email" required placeholder="your@email.com">
    </div>
    <div>
      <label>Website:</label>
      <input type="url" placeholder="Optional">
    </div>
    <input type="submit" value="Submit">
  </form>
</body>
</html>
```

**Steps:**
1. All inputs: `border: 1px solid #ccc; padding: 8px; width: 200px; font-size: 14px;`
2. `:focus` → `border-color: royalblue; outline: none; background-color: #f0f8ff;`
3. `:valid` → `border-color: green;`
4. `:invalid` → `border-color: red;`
5. `:required` → `border-left: 3px solid crimson;`
6. `:optional` → `border-left: 3px solid lightgray;`
7. `:disabled` → `background-color: #eee; color: #aaa;`

**Expected output:** Inputs change border colour based on validity, show a red/gray left border based on required status, and highlight in blue when focused.

**Optional challenge:** Add `:focus-within` styling to each `<div>` wrapper so the whole label+input group highlights when the input inside is focused.

---

### Exercise 3 — Styled Data Table with Zebra Stripes

**Objective:** Use `:nth-child()` to create a readable striped table.

**HTML to use:**
```html
<table>
  <thead>
    <tr>
      <th>Student</th>
      <th>Score</th>
      <th>Grade</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>Alice</td><td>95</td><td>A</td></tr>
    <tr><td>Bob</td><td>82</td><td>B</td></tr>
    <tr><td>Charlie</td><td>74</td><td>C</td></tr>
    <tr><td>Diana</td><td>91</td><td>A</td></tr>
    <tr><td>Eric</td><td>60</td><td>D</td></tr>
  </tbody>
</table>
```

**Steps:**
1. `table` → `border-collapse: collapse; width: 100%;`
2. `th, td` → `padding: 10px 16px; border: 1px solid #ddd; text-align: left;`
3. `thead tr` → `background-color: #333; color: white;`
4. `tbody tr:nth-child(even)` → `background-color: #f5f5f5;`
5. `tbody tr:nth-child(odd)` → `background-color: white;`
6. `tbody tr:hover` → `background-color: #dbeeff;`

**Expected output:**
- Header row: dark background, white text
- Even rows: light gray background
- Odd rows: white background
- Hovered row: light blue highlight

---

### Exercise 4 — Structural Selectors on a Blog Layout

**Objective:** Use structural pseudo-classes to style a blog article list.

**HTML to use:**
```html
<section>
  <article>
    <h2>Post One</h2>
    <p>Introduction paragraph.</p>
    <p>Body content goes here.</p>
    <p>Final summary paragraph.</p>
  </article>
</section>
```

**Steps:**
1. `article p:first-of-type` → `font-size: 1.15em; font-weight: 500; color: #222;`
2. `article p:last-of-type` → `font-style: italic; color: #555;`
3. `article p:not(:first-of-type):not(:last-of-type)` → `color: #333; line-height: 1.7;`

**Expected output:**
- First paragraph: larger, semi-bold, dark
- Last paragraph: italic, lighter gray
- Middle paragraphs: normal body text

---

## Mini Project — Interactive Pricing Card

This mini-project combines link states, hover effects, structural pseudo-classes, and form pseudo-classes into one realistic component.

### The Goal

Build a pricing card component that includes:
1. A highlighted "most popular" plan style
2. Hover effects on all cards
3. An interactive contact form below with validation styling

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Pricing Plans</title>
  <style>
    /* Your CSS goes here — build it stage by stage below */
  </style>
</head>
<body>

  <h1>Choose Your Plan</h1>

  <!-- Pricing Cards -->
  <div class="plans">

    <div class="card">
      <h2>Starter</h2>
      <p class="price">$9/month</p>
      <ul>
        <li>5 Projects</li>
        <li>10 GB Storage</li>
        <li>Email Support</li>
      </ul>
      <a href="#contact" class="btn">Get Started</a>
    </div>

    <div class="card featured">
      <h2>Pro</h2>
      <p class="price">$29/month</p>
      <ul>
        <li>Unlimited Projects</li>
        <li>100 GB Storage</li>
        <li>Priority Support</li>
      </ul>
      <a href="#contact" class="btn">Get Started</a>
    </div>

    <div class="card">
      <h2>Enterprise</h2>
      <p class="price">$99/month</p>
      <ul>
        <li>Unlimited Everything</li>
        <li>Dedicated Server</li>
        <li>24/7 Phone Support</li>
      </ul>
      <a href="#contact" class="btn">Get Started</a>
    </div>

  </div>

  <!-- Contact Form -->
  <section id="contact">
    <h2>Get In Touch</h2>
    <form>
      <div class="field">
        <label>Your Name</label>
        <input type="text" required placeholder="Full name">
      </div>
      <div class="field">
        <label>Email Address</label>
        <input type="email" required placeholder="you@example.com">
      </div>
      <div class="field">
        <label>Budget (1–500)</label>
        <input type="number" min="1" max="500" placeholder="e.g. 50">
      </div>
      <button type="submit">Send Message</button>
    </form>
  </section>

</body>
</html>
```

---

### Stage 2 — Base Layout CSS

```css
/* Reset and base */
* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: sans-serif;
  background: #f4f6f9;
  padding: 40px 20px;
  color: #333;
}

h1 {
  text-align: center;
  margin-bottom: 32px;
}

/* Plans layout */
.plans {
  display: flex;
  gap: 24px;
  justify-content: center;
  flex-wrap: wrap;
}

/* Pricing card */
.card {
  background: white;
  border: 1px solid #ddd;
  border-radius: 10px;
  padding: 32px 24px;
  width: 220px;
  text-align: center;
}
```

**Milestone checkpoint:** You should see three white cards side by side.

---

### Stage 3 — Pseudo-class Enhancements

```css
/* Hover effect on cards */
.card:hover {
  box-shadow: 0 8px 24px rgba(0,0,0,0.12);
  transform: translateY(-4px);
  transition: all 0.2s ease;
}

/* Featured card styling */
.card.featured {
  background: #1a1a2e;
  color: white;
  border-color: #1a1a2e;
}

/* First list item in each card */
.card ul li:first-child {
  font-weight: bold;
}

/* Last list item in each card */
.card ul li:last-child {
  color: #888;
  font-size: 0.9em;
}

/* Alternate list items in featured card */
.card.featured ul li:nth-child(odd) {
  opacity: 0.85;
}

/* Button link states */
.btn {
  display: inline-block;
  margin-top: 20px;
  padding: 10px 24px;
  background: #1a1a2e;
  color: white;
  border-radius: 6px;
  text-decoration: none;
}

.btn:hover {
  background: #3a3a5e;
  color: white;
}

.btn:active {
  background: #000;
  transform: scale(0.97);
}

.card.featured .btn {
  background: white;
  color: #1a1a2e;
}

.card.featured .btn:hover {
  background: #f0f0f0;
}
```

---

### Stage 4 — Form Validation Styling

```css
/* Contact section */
#contact {
  max-width: 480px;
  margin: 60px auto 0;
  background: white;
  padding: 32px;
  border-radius: 10px;
  border: 1px solid #ddd;
}

#contact:target {
  border-color: gold;
  background-color: #fffef0;
}

/* Field wrapper */
.field {
  margin-bottom: 20px;
}

.field:focus-within label {
  color: royalblue;
  font-weight: bold;
}

label {
  display: block;
  margin-bottom: 6px;
  font-size: 0.9em;
  color: #555;
}

input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 14px;
  transition: border-color 0.2s;
}

input:focus {
  outline: none;
  border-color: royalblue;
  background-color: #f0f5ff;
}

input:required {
  border-left: 3px solid crimson;
}

input:optional {
  border-left: 3px solid lightgray;
}

input:valid:not(:placeholder-shown) {
  border-color: seagreen;
}

input:invalid:not(:placeholder-shown) {
  border-color: crimson;
}

input:in-range {
  background-color: #f0fff0;
}

input:out-of-range:not(:placeholder-shown) {
  background-color: #fff0f0;
}

button[type="submit"] {
  width: 100%;
  padding: 12px;
  background: #1a1a2e;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
}

button[type="submit"]:hover {
  background: #3a3a5e;
}

button[type="submit"]:active {
  background: #000;
  transform: scale(0.98);
}
```

---

### Stage 5 — Final Output Verification

When you open this in a browser, verify:

- [ ] Cards appear side by side
- [ ] Cards lift up with a shadow on hover
- [ ] The "Pro" card has a dark background
- [ ] The "Get Started" button changes colour when hovered and pressed
- [ ] Clicking "Get Started" scrolls to the form and highlights it with a gold border
- [ ] The Name and Email fields have a red left border (required)
- [ ] The Budget field has a gray left border (optional)
- [ ] Focusing a field turns its label blue
- [ ] Typing a valid email turns the border green
- [ ] Typing an invalid email keeps the border red
- [ ] Typing a number above 500 gives a red background

### Reflection Questions

1. Why did we use `:not(:placeholder-shown)` in the valid/invalid rules?
2. What would happen if we removed the `transition` property from the `.card` rule?
3. How does `:target` help users who navigate via anchor links?
4. Can you add a `:nth-child(2)` rule to make the second pricing card item in each list italic?

### Optional Extensions

- Add a `:focus-visible` rule so keyboard users see a clear focus ring on the submit button
- Use `:empty` to hide any `.field` divs that have no content
- Create a fourth "Free" plan card and use `:last-child` to remove its bottom margin

---

## Common Beginner Mistakes

### Mistake 1 — Wrong LVHA Order for Links

**Incorrect:**
```css
a:hover   { color: red; }
a:link    { color: blue; }
a:visited { color: gray; }
a:active  { color: orange; }
```

**Problem:** Because of the CSS cascade, `:link` and `:visited` come after `:hover`, so they override the hover style and the hover colour never shows.

**Correct:**
```css
a:link    { color: blue; }
a:visited { color: gray; }
a:hover   { color: red; }
a:active  { color: orange; }
```

---

### Mistake 2 — Forgetting the Colon

**Incorrect:**
```css
a hover { color: red; }
```

**Correct:**
```css
a:hover { color: red; }
```

The colon is required. Without it, CSS treats `hover` as a separate selector (a tag name) and the rule won't work as intended.

---

### Mistake 3 — Confusing :first-child and :first-of-type

**Incorrect assumption:**
```html
<div>
  <h2>Title</h2>
  <p>First paragraph</p>
</div>
```

```css
p:first-child { color: red; }
/* This does NOT style the paragraph! */
/* Because p is the SECOND child, not the first */
```

**Correct — use :first-of-type:**
```css
p:first-of-type { color: red; }
/* This styles the first p, regardless of what comes before it */
```

---

### Mistake 4 — :nth-child() Counting From Zero

**Incorrect belief:** Many beginners think `:nth-child(0)` targets the first child.

**Fact:** CSS counts from **1**, not 0.

```css
li:nth-child(1) { color: red; }  /* This is the FIRST item */
li:nth-child(0) { color: red; }  /* This matches NOTHING */
```

---

### Mistake 5 — Applying :valid/:invalid Before Any Input

**Problem:** If you use `:valid` and `:invalid` without `:not(:placeholder-shown)`, every empty required input immediately shows as invalid (red) when the page loads, before the user has even touched it.

**Incorrect:**
```css
input:invalid {
  border-color: red;
}
```

**Better:**
```css
input:invalid:not(:placeholder-shown) {
  border-color: red;
}
```

This way, the red border only appears **after the user has started typing** (after the placeholder disappears).

---

### Mistake 6 — Confusing :hover with :focus

`:hover` requires a mouse. `:focus` works for keyboard navigation. If you only style `:hover`, your website becomes inaccessible to keyboard-only users.

**Best practice:** Style both together where relevant:

```css
button:hover,
button:focus {
  background-color: darkblue;
  color: white;
}
```

---

### Mistake 7 — Forgetting :not() Can Only Take Simple Selectors (in CSS3)

In CSS3, `:not()` accepts only **simple selectors** (a tag, class, id, or attribute).

**Incorrect (CSS3):**
```css
p:not(.intro .special) { }   /* :not() with descendant combinator — won't work in CSS3 */
```

**Correct:**
```css
p:not(.special) { }           /* Simple class selector inside :not() */
```

> **Note:** CSS4/Selectors Level 4 does allow complex selectors inside `:not()`, and modern browsers support it, but for maximum compatibility stick to simple selectors.

---

## Reflection Questions

1. What is the difference between a CSS selector and a CSS pseudo-class?
2. Can you use `:hover` on a `<div>`? If yes, give an example of when that would be useful.
3. What does `:nth-child(3n+1)` select?
4. A form input has `type="email"` and `required`. List all the pseudo-classes that could match it at different times.
5. What is the difference between `:first-child` and `:first-of-type`? Give an HTML example where they produce different results.
6. When would you use `:focus-visible` instead of `:focus`?
7. How does `:target` work, and what do you need in the HTML for it to function?
8. What would `:not(p):not(.highlight)` select?

---

## Completion Checklist

Before moving to the next lesson, check that you can do all of the following:

- [ ] I understand what a pseudo-class is and why it exists
- [ ] I can write the correct syntax for a pseudo-class rule
- [ ] I know the four link states and the LVHA order
- [ ] I can apply `:hover` to non-link elements
- [ ] I understand `:focus` and can use it to style form inputs
- [ ] I know the difference between `:focus`, `:focus-within`, and `:focus-visible`
- [ ] I can use `:checked`, `:enabled`, `:disabled`, `:read-only`, and `:read-write`
- [ ] I can style forms using `:required`, `:optional`, `:valid`, `:invalid`, `:in-range`, `:out-of-range`, and `:placeholder-shown`
- [ ] I understand the difference between `:first-child` and `:first-of-type`
- [ ] I can use `:nth-child()` with numbers, keywords (odd/even), and formulas (3n, 2n+1)
- [ ] I know how to use `:empty`, `:root`, `:target`, and `:not()`
- [ ] I can chain pseudo-classes together
- [ ] I have completed all four practice exercises
- [ ] I have built the pricing card mini-project

---

## Lesson Summary

In this lesson you explored the complete world of CSS pseudo-classes — one of the most powerful tools in CSS for creating interactive, state-aware, and position-based styling without any JavaScript.

Here is a summary of the main categories covered:

**Link Pseudo-classes** let you style hyperlinks in their four states: `:link`, `:visited`, `:hover`, and `:active`. Always use the LVHA order to avoid cascade conflicts.

**Interactive Pseudo-classes** respond to user actions: `:hover` for mouse-over effects, `:focus` for when an element receives keyboard/click focus, `:focus-within` for parent elements when any child is focused, `:focus-visible` for keyboard-only focus indicators, `:active` for the exact moment of clicking, and `:checked` for selected checkboxes and radio buttons.

**Form State Pseudo-classes** allow you to style inputs based on their attributes and validity: `:enabled`, `:disabled`, `:read-only`, `:read-write`, `:required`, `:optional`, `:valid`, `:invalid`, `:in-range`, `:out-of-range`, and `:placeholder-shown`.

**Structural Pseudo-classes** target elements by their position in the document tree: `:first-child`, `:last-child`, `:nth-child(n)`, `:nth-last-child(n)`, `:first-of-type`, `:last-of-type`, `:nth-of-type(n)`, `:nth-last-of-type(n)`, `:only-child`, `:only-of-type`, and `:empty`.

**Special Pseudo-classes** serve specific purposes: `:root` for global CSS variables, `:target` for URL fragment highlighting, `:not()` for negative selection, and `:lang()` for language-based styling.

By mastering pseudo-classes you can now create professional-grade interactive UIs, accessible form experiences, styled data tables, and dynamic page components — all using pure CSS, no JavaScript required.
