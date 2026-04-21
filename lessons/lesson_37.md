---
render_with_liquid: false
title: "CSS Counters & Nested Counters"
nav_order: 37
---

# Lesson 37 — CSS Counters & Nested Counters

---

## Lesson Introduction

Have you ever looked at a legal document, a textbook, a formal report, or an instruction manual and noticed beautifully organised numbering like **"1.1", "1.2", "2.1", "2.2"**? Or maybe a webpage where every heading is automatically numbered — and if you add a new section, all the numbers update by themselves?

That automatic numbering is done with **CSS Counters**.

In this lesson you will learn exactly what CSS counters are, why they are incredibly useful, how they work step by step, and how to use them — from simple single-level numbering all the way to multi-level nested numbering (like a book with chapters and sub-chapters). You will also practise with exercises and build a mini-project.

By the end of this lesson you will be able to:
- Create automatic numbering on any HTML element using only CSS
- Build single-level counters for headings, steps, or list items
- Build multi-level nested counters for structured documents
- Style and format counter output (adding text before or after the number)
- Avoid all common beginner mistakes with counters

---

## Prerequisite Concepts

Before diving in, make sure you are comfortable with these ideas. If any of them are unfamiliar, read the short explanation provided below each.

### What is a CSS Property?

A CSS **property** is an instruction you write in CSS to control how something looks or behaves. For example, `color: red;` is a property that makes text red.

### What is `::before` and `::after`?

These are **CSS pseudo-elements**. Think of them as invisible "attachment zones" that exist just before or just after the content of an HTML element. You can insert generated text or symbols into those zones using the `content` property in CSS.

```css
/* This inserts the word "Note: " before every paragraph */
p::before {
  content: "Note: ";
  color: blue;
}
```

**Expected output in the browser:**
> Note: This is my paragraph text.

CSS counters use `::before` and `::after` to inject counter numbers into your page.

### What is the `content` Property?

The `content` property only works inside `::before` and `::after`. It tells CSS what text or value to insert into that pseudo-element slot.

```css
h2::before {
  content: "★ ";
}
```

This would place a star before every `<h2>` heading on the page.

---

## Part 1 — What Are CSS Counters?

### The Big Idea

A **CSS counter** is like an invisible variable that CSS manages for you. You give it a name, tell it where to start, tell it when to count up, and then display its current value wherever you want.

**Analogy:** Imagine a sports scorekeeper. The scorekeeper starts at 0, adds 1 point every time a team scores, and shows the current total on a scoreboard. A CSS counter works the same way — it starts at a value you set, increases every time it encounters a matching HTML element, and displays the total at that element.

### Why Do CSS Counters Exist? What Problem Do They Solve?

Without CSS counters, if you want numbered headings on a webpage, you have to type the numbers manually into your HTML:

```html
<h2>1. Introduction</h2>
<h2>2. Setup</h2>
<h2>3. Usage</h2>
<h2>4. Advanced</h2>
```

The problem? If you later add a new section between "1. Introduction" and "2. Setup", you have to manually renumber every single heading after it. That is time-consuming, error-prone, and completely unnecessary.

With CSS counters, the browser handles ALL the numbering automatically. You just add or remove headings and the numbers update themselves.

### The Four Key CSS Counter Tools

There are exactly four things you need to understand to use counters:

| Tool | What It Does |
|------|-------------|
| `counter-reset` | **Creates** a counter and sets its starting value (default: 0) |
| `counter-increment` | **Increases** the counter's value each time an element is found |
| `counter()` | **Displays** the current counter value (used inside `content:`) |
| `counters()` | **Displays** nested counter values with a separator (e.g., "1.2.3") |

Let's explore each one in depth.

---

## Part 2 — `counter-reset`: Creating a Counter

### What It Does

`counter-reset` is how you **declare** (create) a counter. You write it on a parent element, and it resets (or initialises) the counter to a value you choose.

**Syntax:**

```css
selector {
  counter-reset: counter-name starting-value;
}
```

- `counter-name` — You choose any name you like (no spaces). Examples: `section`, `myCounter`, `chapter`, `step`.
- `starting-value` — Optional. The number the counter begins at **before** it is first incremented. Default is `0`.

### Simple Example

```css
body {
  counter-reset: section;
}
```

This creates a counter called `section` that starts at `0`. It is placed on `body` so it applies to the whole page.

> **Thinking prompt:** Why do we place `counter-reset` on the **parent** element rather than the element being counted? Because the parent is where the counter "lives". Child elements then increment it as the browser scans through them.

---

## Part 3 — `counter-increment`: Counting Up

### What It Does

`counter-increment` **increases** the counter's value. You place it on the element that you want to "trigger" a count increase.

**Syntax:**

```css
selector {
  counter-increment: counter-name amount;
}
```

- `counter-name` — The same name you used in `counter-reset`.
- `amount` — Optional. How much to increase by. Default is `1`. You can use negative values to count down.

### Simple Example

```css
h2 {
  counter-increment: section;
}
```

Every time the browser finds an `<h2>` element on the page, it increases the `section` counter by 1.

> **What happens if you do NOT use `counter-increment`?** Nothing counts. The counter stays at 0 forever.

---

## Part 4 — `counter()`: Displaying the Counter

### What It Does

`counter()` is a CSS **function** that reads the current value of a named counter and returns it as text. You use it inside the `content` property of a `::before` or `::after` pseudo-element.

**Syntax:**

```css
selector::before {
  content: counter(counter-name);
}
```

You can also add text around it:

```css
selector::before {
  content: "Section " counter(section) ": ";
}
```

---

## Part 5 — Putting It All Together: Your First Counter

Now let's combine all three tools into a complete working example.

### Example 1 — Auto-Numbering Headings (Simplest Possible)

**HTML:**

```html
<body>
  <h2>Introduction</h2>
  <h2>Setup</h2>
  <h2>Usage</h2>
  <h2>Advanced Topics</h2>
</body>
```

**CSS:**

```css
/* Step 1: Create the counter on the parent element */
body {
  counter-reset: section;
}

/* Step 2: Increment the counter each time an h2 is found */
h2 {
  counter-increment: section;
}

/* Step 3: Display the counter value before each h2 */
h2::before {
  content: "Section " counter(section) " — ";
}
```

**Expected Output in Browser:**

```
Section 1 — Introduction
Section 2 — Setup
Section 3 — Usage
Section 4 — Advanced Topics
```

#### Line-By-Line Explanation

| Line | What It Does |
|------|-------------|
| `counter-reset: section;` | Creates a counter named `section`, starting at 0 |
| `counter-increment: section;` | Each `<h2>` adds 1 to the `section` counter |
| `content: "Section " counter(section) " — ";` | Inserts the text "Section", then the number, then " — " before each heading |

> **Thinking prompt:** What would happen if we put `counter-reset` on `h2` instead of `body`? The counter would reset to 0 every time a new `<h2>` is found — so every heading would show "Section 1". Try it and see!

---

### Example 2 — Auto-Numbering with Custom Start Value

What if you want numbering to start at 5 instead of 1?

```css
body {
  counter-reset: section 4;  /* Start at 4, so first increment gives 5 */
}

h2 {
  counter-increment: section;
}

h2::before {
  content: "Step " counter(section) ": ";
}
```

**Expected Output:**

```
Step 5: First heading
Step 6: Second heading
Step 7: Third heading
```

> **Why `4` not `5`?** Because `counter-reset` sets the value BEFORE the first increment. When the browser hits the first `<h2>`, it increments from 4 to 5, so the display starts at 5.

---

### Example 3 — Counting by 2 (Increment Amount)

```css
body {
  counter-reset: even;
}

p {
  counter-increment: even 2;
}

p::before {
  content: counter(even) ". ";
}
```

**HTML:**
```html
<p>First paragraph</p>
<p>Second paragraph</p>
<p>Third paragraph</p>
```

**Expected Output:**

```
2. First paragraph
4. Second paragraph
6. Third paragraph
```

---

## Part 6 — Counter Display Types

By default, counters display as decimal numbers (1, 2, 3...). But you can change this!

**Syntax:**

```css
content: counter(counter-name, list-style-type);
```

| List Style Type | Output Example |
|----------------|---------------|
| `decimal` | 1, 2, 3 (default) |
| `upper-roman` | I, II, III |
| `lower-roman` | i, ii, iii |
| `upper-alpha` | A, B, C |
| `lower-alpha` | a, b, c |

### Example — Roman Numeral Sections

```css
body {
  counter-reset: chapter;
}

h2 {
  counter-increment: chapter;
}

h2::before {
  content: counter(chapter, upper-roman) ". ";
}
```

**Expected Output:**

```
I. Introduction
II. Setup
III. Usage
IV. Advanced Topics
```

---

## Part 7 — Nested Counters

### The Concept

In a book, you have chapters and within each chapter you have sections:

```
Chapter 1
  1.1 First Section
  1.2 Second Section
Chapter 2
  2.1 First Section
  2.2 Second Section
```

This is called **nested numbering**. CSS counters can do this with multiple counter instances — one for the top level and one for the sub-level.

### The Key Insight: `counter-reset` on a Child Resets for Each Parent

When you put `counter-reset` on an element, it creates a **fresh instance** of the counter each time that element appears. So if chapters reset the section counter, each new chapter gets its own section count starting from 0.

### Example 4 — Two-Level Nested Counter (Chapter → Section)

**HTML:**

```html
<body>
  <h1>Introduction</h1>
    <h2>What is CSS?</h2>
    <h2>Why CSS Matters</h2>
  <h1>Fundamentals</h1>
    <h2>Selectors</h2>
    <h2>Properties</h2>
    <h2>Values</h2>
  <h1>Advanced</h1>
    <h2>Flexbox</h2>
    <h2>Grid</h2>
</body>
```

**CSS:**

```css
/* Level 1: Chapter counter on body */
body {
  counter-reset: chapter;
}

h1 {
  counter-increment: chapter;
  counter-reset: section;    /* Reset section counter for each new chapter */
}

h1::before {
  content: counter(chapter) ". ";
}

/* Level 2: Section counter */
h2 {
  counter-increment: section;
}

h2::before {
  content: counter(chapter) "." counter(section) " ";
  margin-left: 20px;
}
```

**Expected Output:**

```
1. Introduction
    1.1 What is CSS?
    1.2 Why CSS Matters
2. Fundamentals
    2.1 Selectors
    2.2 Properties
    2.3 Values
3. Advanced
    3.1 Flexbox
    3.2 Grid
```

#### Step-By-Step Breakdown

1. `body { counter-reset: chapter; }` — Creates the `chapter` counter (starts at 0)
2. `h1 { counter-increment: chapter; }` — Each `<h1>` adds 1 to `chapter`
3. `h1 { counter-reset: section; }` — Each `<h1>` ALSO resets `section` back to 0, so sections restart for every new chapter
4. `h2 { counter-increment: section; }` — Each `<h2>` adds 1 to `section`
5. `h2::before { content: counter(chapter) "." counter(section) " "; }` — Displays "chapter.section" format

> **This is the key to nested counters:** you put BOTH `counter-increment` and `counter-reset` on the parent-level element. That parent counts itself UP, while also resetting the child counter.

---

## Part 8 — The `counters()` Function for Deeply Nested Lists

### When to Use `counters()` Instead of `counter()`

When your list items can be **arbitrarily deeply nested** (like an outline that could go 3, 4, or 5 levels deep), using multiple separate counter names becomes complex. The `counters()` function handles this elegantly by automatically tracking ALL levels of nesting and joining them with a separator you provide.

**Syntax:**

```css
content: counters(counter-name, "separator");
```

- `counter-name` — The same counter name used at every level
- `"separator"` — The character(s) between each level (e.g., `"."` or `" - "`)

### How It Works

The magic is that CSS creates a **new scope** of the same-named counter for each nested list. `counters()` collects all the values from the outermost to the innermost scope and joins them with your separator.

### Example 5 — Deeply Nested Outline List

**HTML:**

```html
<ol>
  <li>First item
    <ol>
      <li>Sub item A</li>
      <li>Sub item B
        <ol>
          <li>Deep item i</li>
          <li>Deep item ii</li>
        </ol>
      </li>
      <li>Sub item C</li>
    </ol>
  </li>
  <li>Second item</li>
  <li>Third item
    <ol>
      <li>Sub item A</li>
      <li>Sub item B</li>
    </ol>
  </li>
</ol>
```

**CSS:**

```css
/* Remove default list numbering */
ol {
  list-style: none;
  counter-reset: outline;
}

li {
  counter-increment: outline;
}

li::before {
  content: counters(outline, ".") " ";
}
```

**Expected Output:**

```
1 First item
  1.1 Sub item A
  1.2 Sub item B
    1.2.1 Deep item i
    1.2.2 Deep item ii
  1.3 Sub item C
2 Second item
3 Third item
  3.1 Sub item A
  3.2 Sub item B
```

#### Why This Works

- Each `<ol>` element triggers a `counter-reset: outline` (because every `ol` has that rule)
- This creates a **new, fresh scope** of the `outline` counter
- Each `<li>` increments the `outline` counter **in its own scope**
- `counters(outline, ".")` reads all the nested scope values from outside to inside and joins them with `"."`

> **Thinking prompt:** What would change if you used `"/"` as the separator instead of `"."`? The output would be `1/2/3` style numbering instead of `1.2.3`. Try it!

---

## Part 9 — `counter()` vs `counters()` — Key Differences

| Feature | `counter()` | `counters()` |
|---------|------------|-------------|
| **Levels** | Works for a single counter level | Works across all nested levels |
| **Separator** | No separator (just shows the current count) | You define a separator string |
| **Best for** | Simple headings, steps, sections | Nested outlines, numbered lists |
| **Syntax** | `counter(name)` | `counters(name, ".")` |
| **Display type** | Optional: `counter(name, upper-roman)` | Optional: `counters(name, ".", lower-alpha)` |

---

## Part 10 — Complete CSS Counter Properties Reference

| Property / Function | Where Used | Purpose |
|--------------------|-----------|---------|
| `counter-reset: name value` | On parent element | Creates the counter and sets start value |
| `counter-reset: name` | On parent element | Creates the counter, start value = 0 |
| `counter-reset: a b c` | On parent element | Creates multiple counters at once |
| `counter-increment: name` | On counted elements | Increments by 1 |
| `counter-increment: name 3` | On counted elements | Increments by 3 |
| `counter-increment: name -1` | On counted elements | Decrements (counts down) |
| `counter()` | Inside `content:` | Displays single counter value |
| `counters()` | Inside `content:` | Displays all nested counter values |

---

## Part 11 — Guided Practice Exercises

### Exercise 1 — Warm-Up: Step Counter

**Objective:** Create a numbered list of steps for making tea using CSS counters (not HTML `<ol>`).

**Scenario:** You are building a recipe website. The steps should be auto-numbered: "Step 1:", "Step 2:", etc.

**HTML to use:**

```html
<div class="steps">
  <p>Boil water in a kettle</p>
  <p>Place a tea bag in a mug</p>
  <p>Pour hot water into the mug</p>
  <p>Wait 3 minutes</p>
  <p>Remove the tea bag</p>
  <p>Add milk or sugar if desired</p>
  <p>Enjoy your tea!</p>
</div>
```

**Steps to solve:**
1. Add `counter-reset: step;` to `.steps` to create the counter
2. Add `counter-increment: step;` to `p` to count each paragraph
3. Add `p::before { content: "Step " counter(step) ": "; }` to display the count

**Hints:**
- Don't forget the space after the colon in the content string
- You may also add `font-weight: bold;` to `p::before` to make step labels stand out

**Expected Output:**

```
Step 1: Boil water in a kettle
Step 2: Place a tea bag in a mug
Step 3: Pour hot water into the mug
Step 4: Wait 3 minutes
Step 5: Remove the tea bag
Step 6: Add milk or sugar if desired
Step 7: Enjoy your tea!
```

**Self-check questions:**
- What happens if you remove `counter-reset`?
- What happens if you change `counter-increment: step;` to `counter-increment: step 2;`?

---

### Exercise 2 — Roman Numeral Chapter List

**Objective:** Create a table of contents with Roman numeral chapters.

**HTML:**

```html
<div class="toc">
  <h2>History</h2>
  <h2>Theory</h2>
  <h2>Practice</h2>
  <h2>Conclusion</h2>
</div>
```

**Steps to solve:**
1. Reset a counter called `chapter` on `.toc`
2. Increment `chapter` on `h2`
3. Display using `counter(chapter, upper-roman)` in `h2::before`
4. Add `"Chapter "` before and `" — "` after the number in the content string

**Expected Output:**

```
Chapter I — History
Chapter II — Theory
Chapter III — Practice
Chapter IV — Conclusion
```

---

### Exercise 3 — Nested Sections (Intermediate)

**Objective:** Build a two-level document with chapters and sub-sections numbered `1`, `1.1`, `1.2`, `2`, `2.1`, etc.

**HTML:**

```html
<div class="document">
  <h2>Planning</h2>
    <h3>Define goals</h3>
    <h3>Research</h3>
  <h2>Execution</h2>
    <h3>Build</h3>
    <h3>Test</h3>
    <h3>Deploy</h3>
  <h2>Review</h2>
    <h3>Collect feedback</h3>
</div>
```

**Steps to solve:**
1. On `.document`: `counter-reset: chapter;`
2. On `h2`: `counter-increment: chapter;` AND `counter-reset: section;`
3. On `h2::before`: `content: counter(chapter) ". ";`
4. On `h3`: `counter-increment: section;`
5. On `h3::before`: `content: counter(chapter) "." counter(section) " ";`
6. Add some left padding to `h3` so it looks indented

**Expected Output:**

```
1. Planning
    1.1 Define goals
    1.2 Research
2. Execution
    2.1 Build
    2.2 Test
    2.3 Deploy
3. Review
    3.1 Collect feedback
```

**What-if challenges:**
- What happens if you remove `counter-reset: section;` from `h2`? (The section numbers keep incrementing across chapters!)
- What if you want chapters as letters (A, B, C)? Change `counter(chapter)` to `counter(chapter, upper-alpha)`.

---

### Exercise 4 — Nested `<ol>` with `counters()`

**Objective:** Create a deeply nested outline using `counters()`.

**HTML:**

```html
<ol>
  <li>Animals
    <ol>
      <li>Mammals
        <ol>
          <li>Dogs</li>
          <li>Cats</li>
        </ol>
      </li>
      <li>Birds</li>
    </ol>
  </li>
  <li>Plants
    <ol>
      <li>Trees</li>
      <li>Flowers</li>
    </ol>
  </li>
</ol>
```

**CSS to write:**

```css
ol {
  list-style: none;
  counter-reset: items;
}

li {
  counter-increment: items;
}

li::before {
  content: counters(items, ".") ". ";
}
```

**Expected Output:**

```
1. Animals
  1.1. Mammals
    1.1.1. Dogs
    1.1.2. Cats
  1.2. Birds
2. Plants
  2.1. Trees
  2.2. Flowers
```

---

## Part 12 — Mini Project: Automated Course Syllabus

### Project Overview

You are building an automated course syllabus page for an online learning platform. The page must show:
- Module numbers (1, 2, 3...)
- Lesson numbers within each module (1.1, 1.2, 2.1, 2.2...)
- A "Total Lessons" count at the end, all using CSS counters.

### Stage 1 — Basic HTML Structure

Set up the HTML:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>CSS Course Syllabus</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <h1>CSS Mastery Course — Syllabus</h1>

  <div class="syllabus">

    <div class="module">
      <h2>Introduction to CSS</h2>
      <p class="lesson">What is CSS?</p>
      <p class="lesson">CSS Syntax and Selectors</p>
      <p class="lesson">Colours and Backgrounds</p>
    </div>

    <div class="module">
      <h2>Box Model and Layout</h2>
      <p class="lesson">The Box Model</p>
      <p class="lesson">Margins and Padding</p>
      <p class="lesson">Display and Position</p>
      <p class="lesson">Flexbox Basics</p>
    </div>

    <div class="module">
      <h2>Advanced CSS</h2>
      <p class="lesson">CSS Grid</p>
      <p class="lesson">Animations and Transitions</p>
      <p class="lesson">CSS Variables</p>
      <p class="lesson">CSS Counters</p>
    </div>

  </div>

</body>
</html>
```

**Expected milestone:** Plain text headings and paragraphs — no numbering yet.

---

### Stage 2 — Add Module Counter

Add CSS for module numbering:

```css
/* style.css */

body {
  font-family: Arial, sans-serif;
  max-width: 700px;
  margin: 40px auto;
  padding: 0 20px;
  background: #f5f5f5;
}

h1 {
  text-align: center;
  color: #2c3e50;
}

/* Counter for modules */
.syllabus {
  counter-reset: module;
}

.module {
  background: white;
  border-left: 4px solid #3498db;
  margin-bottom: 20px;
  padding: 15px 20px;
  border-radius: 4px;
  counter-increment: module;
  counter-reset: lesson;
}

.module h2::before {
  content: "Module " counter(module) " — ";
  color: #3498db;
}
```

**Expected milestone output:**

```
Module 1 — Introduction to CSS
Module 2 — Box Model and Layout
Module 3 — Advanced CSS
```

---

### Stage 3 — Add Lesson Counter with Nested Numbering

```css
/* Add to style.css */

.lesson {
  counter-increment: lesson;
  padding: 5px 0 5px 20px;
  border-bottom: 1px solid #eee;
  color: #555;
}

.lesson::before {
  content: counter(module) "." counter(lesson) "  ";
  font-weight: bold;
  color: #2c3e50;
  margin-right: 8px;
}
```

**Expected milestone output:**

```
Module 1 — Introduction to CSS
    1.1  What is CSS?
    1.2  CSS Syntax and Selectors
    1.3  Colours and Backgrounds

Module 2 — Box Model and Layout
    2.1  The Box Model
    2.2  Margins and Padding
    2.3  Display and Position
    2.4  Flexbox Basics

Module 3 — Advanced CSS
    3.1  CSS Grid
    3.2  Animations and Transitions
    3.3  CSS Variables
    3.4  CSS Counters
```

---

### Stage 4 — Show Total Lesson Count

After the `.syllabus` div, add a total:

```html
<div class="total">Total Lessons in this Course</div>
```

```css
/* Add to style.css */

.syllabus {
  counter-reset: module total-lessons;  /* Reset both counters */
}

/* Modify lesson rule to also increment total */
.lesson {
  counter-increment: lesson total-lessons;
}

/* Display the total */
.total {
  text-align: center;
  font-size: 1.1em;
  color: #2c3e50;
  margin-top: 20px;
}

.total::after {
  content: ": " counter(total-lessons) " lessons";
  font-weight: bold;
  color: #3498db;
}
```

**Expected milestone output:**
> Total Lessons in this Course: 11 lessons

---

### Stage 5 — Final Full CSS File

Here is the complete combined CSS:

```css
body {
  font-family: Arial, sans-serif;
  max-width: 700px;
  margin: 40px auto;
  padding: 0 20px;
  background: #f5f5f5;
}

h1 {
  text-align: center;
  color: #2c3e50;
}

.syllabus {
  counter-reset: module total-lessons;
}

.module {
  background: white;
  border-left: 4px solid #3498db;
  margin-bottom: 20px;
  padding: 15px 20px;
  border-radius: 4px;
  counter-increment: module;
  counter-reset: lesson;
}

.module h2::before {
  content: "Module " counter(module) " — ";
  color: #3498db;
}

.lesson {
  counter-increment: lesson total-lessons;
  padding: 5px 0 5px 20px;
  border-bottom: 1px solid #eee;
  color: #555;
}

.lesson::before {
  content: counter(module) "." counter(lesson) "  ";
  font-weight: bold;
  color: #2c3e50;
  margin-right: 8px;
}

.total {
  text-align: center;
  font-size: 1.1em;
  color: #2c3e50;
  margin-top: 20px;
}

.total::after {
  content: ": " counter(total-lessons) " lessons";
  font-weight: bold;
  color: #3498db;
}
```

**Reflection questions:**
- What would happen if you removed `counter-reset: lesson;` from `.module`?
- How would you add a 4th level of nesting (Module → Section → Lesson → Sub-Lesson)?
- How could you make the module count use Roman numerals?

**Optional extensions:**
- Add a "difficulty level" using `upper-alpha` counters (A=Beginner, B=Intermediate, C=Advanced)
- Add a `counter(module)` to the page title dynamically
- Build a table of contents using `counters()` at the top of the page

---

## Part 13 — Common Beginner Mistakes

### Mistake 1 — Forgetting `counter-reset`

```css
/* WRONG — counter was never created */
h2 {
  counter-increment: section;
}
h2::before {
  content: counter(section);
}
```

**Problem:** Without `counter-reset`, the counter does not exist. The browser may still try to display something, but the behaviour is undefined.

**Fix:** Always declare the counter with `counter-reset` on a parent element first.

```css
/* CORRECT */
body {
  counter-reset: section;   /* Create it here */
}
h2 {
  counter-increment: section;
}
h2::before {
  content: counter(section);
}
```

---

### Mistake 2 — Using `content` Without `::before` or `::after`

```css
/* WRONG — content only works in pseudo-elements */
h2 {
  content: counter(section);
}
```

**Problem:** The `content` property has no effect on regular HTML elements. It only works inside `::before` and `::after`.

**Fix:** Always use `::before` or `::after`:

```css
h2::before {
  content: counter(section) ". ";
}
```

---

### Mistake 3 — Forgetting to Reset the Child Counter in Nested Counters

```css
/* WRONG — sections never reset between chapters */
body { counter-reset: chapter; }
h1 { counter-increment: chapter; }
h2 { counter-increment: section; }   /* <-- section never resets! */
```

**Problem:** The `section` counter keeps going up across all chapters (1, 2, 3, 4, 5...) instead of resetting for each chapter (1.1, 1.2, 2.1, 2.2...).

**Fix:** Reset the child counter on the parent element:

```css
h1 {
  counter-increment: chapter;
  counter-reset: section;    /* Reset sections for every new chapter */
}
```

---

### Mistake 4 — Using `counter()` Instead of `counters()` for Nested Lists

```css
/* WRONG — only shows the current level number */
ol { counter-reset: item; }
li { counter-increment: item; }
li::before {
  content: counter(item) ". ";
}
```

**Problem:** This only shows the number at the current nesting level (1, 2, 3 everywhere) — it does NOT show the full path like "1.2.3".

**Fix:** Use `counters()` with a separator:

```css
li::before {
  content: counters(item, ".") ". ";
}
```

---

### Mistake 5 — Confusing Start Value in `counter-reset`

```css
/* WRONG — if you want to start at 1, don't set reset to 1 */
body {
  counter-reset: section 1;
}
h2 {
  counter-increment: section;
}
```

**Problem:** The first `<h2>` will display **2** because the counter starts at 1 and then gets incremented to 2.

**Fix:** Set `counter-reset` to one LESS than your desired start number:

```css
/* To start at 1: reset to 0 (the default) */
body {
  counter-reset: section;   /* starts at 0, first increment = 1 */
}

/* To start at 5: reset to 4 */
body {
  counter-reset: section 4;  /* starts at 4, first increment = 5 */
}
```

---

### Mistake 6 — Forgetting `list-style: none` When Replacing `<ol>` Numbering

```css
/* PROBLEM — browser shows both default numbers AND your counter */
ol {
  counter-reset: item;
}
li::before {
  content: counter(item) ". ";
  counter-increment: item;
}
```

**Problem:** The `<ol>` still shows its built-in 1, 2, 3 numbering, AND your custom counter also shows. You get double numbers.

**Fix:** Remove the default list numbering:

```css
ol {
  list-style: none;
  counter-reset: item;
}
```

---

## Part 14 — Real-World Use Cases

CSS counters are used widely in professional web development:

**Documentation sites** — Technical documentation like developer guides, API references, and user manuals use counters to auto-number sections and API endpoints.

**Legal and contract documents** — Law firms and contract template platforms use counters for clause numbering (1, 1.1, 1.1.1).

**Academic papers and theses** — Research platforms use counters to number figures, tables, equations, and sections.

**E-learning platforms** — Course outlines, lesson numbering, and progress tracking on sites like Coursera use counter-like systems.

**Recipe sites** — Step-by-step cooking instructions with auto-numbered steps.

**Terms and conditions pages** — Large legal T&C pages with numbered clauses and sub-clauses.

**Print stylesheets** — When printing webpages, CSS counters are used to add page numbers and section references in print media queries.

---

## Part 15 — Reflection Questions

Think through these questions to solidify your understanding:

1. What is the difference between `counter-reset` and `counter-increment`? Can you have one without the other?
2. Why must `counter()` be used inside the `content` property, and only inside `::before` or `::after`?
3. What is the fundamental difference between `counter()` and `counters()`? When would you choose one over the other?
4. If you want chapter sections to restart at 1 for each new chapter, which CSS property do you add to the chapter heading, and what value do you give it?
5. How would you create a counter that counts **down** from 10 to 1?
6. If you have three levels of nesting (part → chapter → section), how many `counter-reset` declarations do you need and where do they go?
7. Can two different counters be reset at the same time on one element? How?
8. What would happen if you put `counter-reset` on the **same element** as `counter-increment` for the same counter name?

---

## Part 16 — Completion Checklist

Before moving to the next lesson, check off each item:

- [ ] I understand what a CSS counter is and what problem it solves
- [ ] I can use `counter-reset` to create and initialise a counter
- [ ] I can use `counter-increment` to count elements as the browser reads them
- [ ] I can use `counter()` inside `content` to display a counter value
- [ ] I can set a custom start value using `counter-reset: name value`
- [ ] I can change the display type (decimal, roman, alpha) of a counter
- [ ] I understand how `counter-reset` on a child element creates nested counter scopes
- [ ] I can build a two-level nested counter (e.g., chapter.section)
- [ ] I can use `counters()` with a separator for deep list nesting
- [ ] I know the difference between `counter()` and `counters()`
- [ ] I have identified and can fix all 6 common mistakes
- [ ] I completed at least 2 of the 4 practice exercises
- [ ] I completed the mini-project syllabus page
- [ ] I can name at least 3 real-world applications for CSS counters

---

## Lesson Summary

CSS counters are a powerful pure-CSS mechanism for automatic numbering. Here is what you learned:

**The four tools:**
- `counter-reset` — Creates a counter and sets its starting value (place on a parent element)
- `counter-increment` — Increases the counter each time a matching element is found
- `counter()` — Displays a single counter value (use inside `content:` in `::before`/`::after`)
- `counters()` — Displays full nested path values joined by a separator

**Single-level pattern:**
```css
parent  { counter-reset: name; }
element { counter-increment: name; }
element::before { content: counter(name) ". "; }
```

**Nested counter pattern:**
```css
body    { counter-reset: chap; }
h1      { counter-increment: chap; counter-reset: sec; }
h1::before { content: counter(chap) ". "; }
h2      { counter-increment: sec; }
h2::before { content: counter(chap) "." counter(sec) " "; }
```

**Deep nested list pattern:**
```css
ol      { list-style: none; counter-reset: item; }
li      { counter-increment: item; }
li::before { content: counters(item, ".") ". "; }
```

CSS counters are supported in all modern browsers and are actively used in documentation systems, e-learning platforms, legal documents, and anywhere structured, auto-numbered content is needed.

---

*End of Lesson 37 — CSS Counters & Nested Counters*
