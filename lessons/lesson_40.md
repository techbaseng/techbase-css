---
render_with_liquid: false
title: "CSS Specificity — Who Wins When Rules Conflict?"
nav_order: 40
---

# Lesson 40 — CSS Specificity: Who Wins When Rules Conflict?

---

## Lesson Introduction

Have you ever written CSS and been confused by why your style didn't seem to work? You set a colour for a paragraph, but something else overrode it. You added a class, but the result was still wrong. This happens because of a concept called **CSS Specificity**.

In this lesson you will learn exactly what specificity is, why it exists, how the browser scores and compares selectors, and how to control which style wins every single time. By the end, you will never be surprised by a style conflict again.

> 💡 **Real-world connection:** In professional front-end development, understanding specificity is essential for debugging layout issues, maintaining large stylesheets, working with CSS frameworks like Bootstrap, and writing clean, predictable code.

---

## Prerequisite Concepts

Before diving in, let's make sure you understand the building blocks used throughout this lesson.

### What Is a CSS Selector?

A **selector** is the part of a CSS rule that identifies which HTML element(s) you want to style.

```css
/* The selector is "p" — it targets all <p> elements */
p {
  color: red;
}
```

### The Three Main Selector Types You Need to Know

**1. Element selector** — targets HTML tags by name.

```css
p { color: red; }    /* styles every <p> */
h1 { color: blue; }  /* styles every <h1> */
```

**2. Class selector** — targets elements that have a specific `class` attribute. Written with a dot (`.`) before the name.

```css
.highlight { color: yellow; }
/* This styles any element with class="highlight" */
```

**3. ID selector** — targets ONE specific element with a matching `id` attribute. Written with a hash (`#`) before the name.

```css
#main-title { color: green; }
/* This styles the element with id="main-title" */
```

> 💡 **Key rule to remember:** An `id` must be unique on a page — only one element should have any given `id`. Classes can be shared by many elements.

### What Is a Style Declaration?

A **declaration** is the `property: value` pair inside curly braces.

```css
p {
  color: blue;       /* This is one declaration */
  font-size: 18px;   /* This is another declaration */
}
```

---

## Conceptual Understanding

### What Is Specificity?

**Specificity** is the scoring system that browsers use to decide which CSS rule "wins" when two or more rules target the same element and set the same property.

Think of it like a competition between your CSS rules. Every selector has a **score** (called its specificity weight). When two rules conflict, the one with the **higher score wins**, and its style gets applied.

### Why Does Specificity Exist?

Imagine you're building a website. You have a general rule that makes all paragraphs grey. Then later you want one special paragraph to be red. Without specificity, the browser wouldn't know which rule to use. Specificity is the tiebreaker.

**Analogy:** Think of specificity like priority lanes at an airport. Economy passengers (element selectors) use the regular queue. Business class passengers (class selectors) get a faster lane. First-class passengers (ID selectors) go straight through. The more specific you are, the faster you get to the front.

### A First Look at the Problem Specificity Solves

```html
<!-- HTML -->
<p class="test" id="demo">Hello World!</p>
```

```css
/* Three rules, all targeting the same paragraph */
p       { color: red; }
.test   { color: green; }
#demo   { color: blue; }
```

**Expected Output:** The text "Hello World!" appears in **blue**.

Why blue? Because `#demo` (an ID selector) has a higher specificity score than `.test` (a class selector), which has a higher score than `p` (an element selector). The browser picks blue.

> 🤔 **Thinking prompt:** What would happen if you removed `#demo { color: blue; }`? Which colour would win then? Think about it before reading on.

---

## The Four Levels of Specificity

CSS organises selectors into four levels, from lowest to highest priority.

### Level 1 — Universal Selector and `:where()`  
**Weight: 0-0-0 (no priority)**

The universal selector `*` matches everything, but it has zero specificity. The `:where()` pseudo-class also carries zero specificity weight.

```css
* { color: grey; }        /* weight: 0-0-0 */
:where(p) { color: grey; } /* weight: 0-0-0 */
```

These are always overridden by any other selector.

---

### Level 2 — Element Selectors and Pseudo-elements  
**Weight: 0-0-1**

Element selectors target HTML tags. Pseudo-elements like `::before` and `::after` also sit at this level.

```css
p      { color: red; }    /* weight: 0-0-1 */
h1     { color: blue; }   /* weight: 0-0-1 */
::before { content: "→"; } /* weight: 0-0-1 */
```

---

### Level 3 — Class Selectors, Attribute Selectors, and Pseudo-classes  
**Weight: 0-1-0**

This level includes classes (`.myclass`), attribute selectors (`[type="text"]`), and pseudo-classes (`:hover`, `:focus`, `:nth-child()`).

```css
.test          { color: green; }   /* weight: 0-1-0 */
[type="text"]  { color: green; }   /* weight: 0-1-0 */
:hover         { color: green; }   /* weight: 0-1-0 */
```

---

### Level 4 — ID Selectors  
**Weight: 1-0-0**

ID selectors are the highest specificity you can normally use in a stylesheet. They always override classes and element selectors.

```css
#demo { color: blue; }   /* weight: 1-0-0 */
```

---

### Level 5 — Inline Styles  
**Weight: Even higher than IDs**

Inline styles are written directly on an HTML element using the `style` attribute. They override all stylesheet rules.

```html
<p style="color: pink;">This is pink no matter what.</p>
```

An inline style beats every other type of CSS selector.

---

## The Specificity Weight Notation: X-Y-Z

Specificity is measured using a three-number notation: **X-Y-Z**

| Position | Counts... | Example |
|----------|-----------|---------|
| **X** (first number) | Number of **ID** selectors | `#header` → X = 1 |
| **Y** (second number) | Number of **class**, **attribute**, and **pseudo-class** selectors | `.nav`, `[href]`, `:hover` → Y = 1 each |
| **Z** (third number) | Number of **element** and **pseudo-element** selectors | `p`, `h1`, `::before` → Z = 1 each |

To compare two selectors, start from the left (X). The selector with the bigger X wins. If X is equal, compare Y. If Y is equal, compare Z. If all three are equal, the rule that appears **later in the stylesheet** wins (this is the cascade rule you may have learned previously).

### Quick Weight Examples

| Selector | X (IDs) | Y (Classes) | Z (Elements) | Notation |
|---|---|---|---|---|
| `p` | 0 | 0 | 1 | 0-0-1 |
| `.test` | 0 | 1 | 0 | 0-1-0 |
| `p.test` | 0 | 1 | 1 | 0-1-1 |
| `#demo` | 1 | 0 | 0 | 1-0-0 |
| `p#demo` | 1 | 0 | 1 | 1-0-1 |
| `#demo.test` | 1 | 1 | 0 | 1-1-0 |

---

## Simple Standalone Examples

### Example 1 — Element Selector Alone

```html
<html>
<head>
  <style>
    p { color: red; }
  </style>
</head>
<body>
  <p>Hello World!</p>
</body>
</html>
```

**Expected Output:** The text "Hello World!" appears in **red**.

**Line-by-line explanation:**
- `p` — This is an element selector targeting all `<p>` tags.
- `{ color: red; }` — This sets the text colour to red.
- Specificity weight: **0-0-1**
- Since there is only one rule, it wins by default.

---

### Example 2 — Class Selector Overrides Element Selector

```html
<html>
<head>
  <style>
    .test { color: green; }  /* weight: 0-1-0 */
    p     { color: red; }    /* weight: 0-0-1 */
  </style>
</head>
<body>
  <p class="test">Hello World!</p>
</body>
</html>
```

**Expected Output:** The text "Hello World!" appears in **green**.

**Why green?**
- Both rules target the same `<p>` element.
- `.test` has weight **0-1-0**.
- `p` has weight **0-0-1**.
- Comparing: 0-1-0 is greater than 0-0-1 (Y column: 1 > 0).
- **Green wins.**

> 🤔 **Thinking prompt:** What if you swap the order of the two rules in the stylesheet? Does the result change? Try it.

---

### Example 3 — ID Selector Overrides Everything

```html
<html>
<head>
  <style>
    #demo  { color: blue; }   /* weight: 1-0-0 */
    .test  { color: green; }  /* weight: 0-1-0 */
    p      { color: red; }    /* weight: 0-0-1 */
  </style>
</head>
<body>
  <p id="demo" class="test">Hello World!</p>
</body>
</html>
```

**Expected Output:** The text "Hello World!" appears in **blue**.

**Why blue?**
- The `<p>` element matches all three selectors.
- `#demo` has the highest weight: **1-0-0**.
- Blue wins, regardless of order in the stylesheet.

---

### Example 4 — Combined Selector with Higher Weight

Now here is where it gets interesting. What if we **combine** selectors? When you write `p#demo`, you are selecting a `<p>` element that also has `id="demo"`. This combination adds up the weights.

```css
#demo   { color: blue; }    /* weight: 1-0-0 */
p#demo  { color: orange; }  /* weight: 1-0-1  ← WINS */
.test   { color: green; }   /* weight: 0-1-0 */
p.test  { color: yellow; }  /* weight: 0-1-1 */
p       { color: red; }     /* weight: 0-0-1 */
```

```html
<p id="demo" class="test">Hello World!</p>
```

**Expected Output:** The text "Hello World!" appears in **orange**.

**Why orange?**
- `p#demo` has weight **1-0-1** (1 ID + 1 element).
- `#demo` alone has weight **1-0-0** (1 ID, no elements).
- Comparing X: both have X=1. Tie. Compare Z: `p#demo` has Z=1, `#demo` has Z=0.
- **1-0-1 > 1-0-0** → orange wins.

> 🤔 **Thinking prompt:** Why does `p.test` (weight 0-1-1) lose to `#demo` (weight 1-0-0)?  
> Because the **X column** (IDs) always overrules the Y and Z columns no matter how many classes or elements you have.

---

### Example 5 — Equal Specificity: Last Rule Wins

When two selectors have **identical weight**, the browser uses the one that appears **later** in the stylesheet. This is called the **cascade**.

```css
p { color: red; }    /* weight: 0-0-1 */
p { color: blue; }   /* weight: 0-0-1 — WINS because it comes last */
```

**Expected Output:** Blue.

---

## Understanding the Specificity Hierarchy Table

Here is the complete picture from highest to lowest priority:

| Rank | Type | Example | Weight |
|------|------|---------|--------|
| 1st (highest) | Inline style | `<h1 style="color:pink">` | Higher than all stylesheet selectors |
| 2nd | ID selector | `#navbar` | 1-0-0 |
| 3rd | Class / Attribute / Pseudo-class | `.test`, `[href]`, `:hover` | 0-1-0 |
| 4th | Element / Pseudo-element | `h1`, `p`, `::before` | 0-0-1 |
| 5th (lowest) | Universal / `:where()` | `*`, `:where(p)` | 0-0-0 |

---

## More Complex Specificity Calculations

Let's practice reading and calculating weights of more complex selectors.

### Worked Calculation 1

```css
div p.highlight { color: purple; }
```

Break it down:
- `div` → element → adds **0-0-1**
- `p` → element → adds **0-0-1**
- `.highlight` → class → adds **0-1-0**
- **Total: 0-1-2**

---

### Worked Calculation 2

```css
#header nav ul li a:hover { color: orange; }
```

Break it down:
- `#header` → ID → adds **1-0-0**
- `nav` → element → adds **0-0-1**
- `ul` → element → adds **0-0-1**
- `li` → element → adds **0-0-1**
- `a` → element → adds **0-0-1**
- `:hover` → pseudo-class → adds **0-1-0**
- **Total: 1-1-4**

---

### Worked Calculation 3

```css
.sidebar .widget h2 { color: teal; }
```

Break it down:
- `.sidebar` → class → adds **0-1-0**
- `.widget` → class → adds **0-1-0**
- `h2` → element → adds **0-0-1**
- **Total: 0-2-1**

---

## Guided Practice Exercises

### Exercise 1 — Predict the Winning Colour

**Objective:** Read the CSS and HTML below, calculate which colour wins, and explain why.

**HTML:**
```html
<p id="intro" class="lead">Welcome to my website.</p>
```

**CSS:**
```css
p        { color: black; }      /* Rule A */
.lead    { color: navy; }       /* Rule B */
#intro   { color: crimson; }    /* Rule C */
p.lead   { color: teal; }       /* Rule D */
```

**Steps:**
1. Calculate the weight of each rule.
2. Identify which rule has the highest weight.
3. State which colour the text will appear.

**Weights:**
- Rule A: `p` → **0-0-1**
- Rule B: `.lead` → **0-1-0**
- Rule C: `#intro` → **1-0-0**
- Rule D: `p.lead` → **0-1-1**

**Expected Output:** Text appears in **crimson**.

**Why?** Rule C (`#intro`) has the highest weight of **1-0-0**. The X column (ID count) immediately beats all other rules regardless of their Y or Z values.

**Self-check questions:**
- Does changing the order of the CSS rules change the result? (No — specificity takes priority over order when weights are different.)
- What would happen if you removed `#intro` from the HTML element? Which colour would win then?

---

### Exercise 2 — Rank These Selectors from Weakest to Strongest

Given the following selectors, rank them from lowest to highest specificity:

```
a) *
b) li
c) ul li
d) .menu
e) .menu li
f) #nav
g) #nav li
h) #nav .menu li
```

**Answers with weights:**

| Selector | Weight | Rank |
|----------|--------|------|
| `*` | 0-0-0 | Weakest |
| `li` | 0-0-1 | 2nd |
| `ul li` | 0-0-2 | 3rd |
| `.menu` | 0-1-0 | 4th |
| `.menu li` | 0-1-1 | 5th |
| `#nav` | 1-0-0 | 6th |
| `#nav li` | 1-0-1 | 7th |
| `#nav .menu li` | 1-1-1 | Strongest |

> 🤔 **Thinking prompt:** Notice that `ul li` (0-0-2) is stronger than `.menu` (0-1-0)? Wait… actually that's wrong! Let's check: 0-0-2 vs 0-1-0. Compare Y column: 0 vs 1. `.menu` wins. Always compare left to right!

---

### Exercise 3 — Fix the Specificity Problem

**Scenario:** A web developer is building a navigation bar. She expects the active link to appear orange, but it keeps appearing blue. Help her fix the issue without changing the HTML.

**HTML:**
```html
<nav id="main-nav">
  <a href="#" class="active">Home</a>
</nav>
```

**CSS (broken):**
```css
#main-nav a   { color: blue; }     /* weight: 1-0-1 */
.active       { color: orange; }   /* weight: 0-1-0 */
```

**Problem:** `.active` (0-1-0) loses to `#main-nav a` (1-0-1) because 1-0-1 > 0-1-0.

**Fix option 1 — increase the specificity of the orange rule:**
```css
#main-nav a      { color: blue; }       /* weight: 1-0-1 */
#main-nav .active { color: orange; }   /* weight: 1-1-0  ← WINS */
```

Now `#main-nav .active` has weight **1-1-0**, which beats `#main-nav a` at **1-0-1** because the Y column (1 vs 0) tips the balance when X is tied.

**Fix option 2 — even more specific:**
```css
#main-nav a.active { color: orange; }  /* weight: 1-1-1  ← also wins */
```

**Expected Output (after fix):** The "Home" link appears in **orange**.

---

## Mini Project — Build a Specificity-Aware Webpage

In this project you will build a small webpage that demonstrates all four levels of specificity working together. Each level will change the appearance of a block of text in a controlled, predictable way.

### Stage 1 — Setup

Create your HTML structure:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Specificity Demo</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div id="page-wrapper" class="container">
    <h1>Welcome to My Page</h1>
    <p>Default paragraph — styled by element selector.</p>
    <p class="featured">Featured paragraph — styled by class selector.</p>
    <p id="hero-text" class="featured">Hero paragraph — styled by ID selector.</p>
    <p style="color: purple; font-weight: bold;">
      Inline-styled paragraph — cannot be overridden by the stylesheet.
    </p>
  </div>
</body>
</html>
```

**Milestone output:** You should see four paragraphs on a white page with no styling yet.

---

### Stage 2 — Add Element-Level Styles

Create `style.css` and add:

```css
/* Element selectors — weight: 0-0-1 */
body {
  font-family: Arial, sans-serif;
  margin: 40px;
  background-color: #f4f4f4;
}

p {
  color: grey;
  font-size: 16px;
}

h1 {
  color: navy;
}
```

**Milestone output:** All paragraphs appear grey. Heading appears navy. This is the base layer.

---

### Stage 3 — Add Class-Level Styles

Add to `style.css`:

```css
/* Class selector — weight: 0-1-0 — overrides element selector */
.featured {
  color: darkgreen;
  font-weight: bold;
}

/* Container class */
.container {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
}
```

**Milestone output:**
- Plain `<p>` → grey (element selector)
- `<p class="featured">` → dark green (class selector wins over element)
- Hero `<p>` → dark green (class wins over element, but ID hasn't been styled yet)

---

### Stage 4 — Add ID-Level Style

Add to `style.css`:

```css
/* ID selector — weight: 1-0-0 — overrides class and element */
#hero-text {
  color: crimson;
  font-size: 20px;
  text-decoration: underline;
}
```

**Milestone output:**
- Plain `<p>` → grey
- `<p class="featured">` → dark green
- `<p id="hero-text" class="featured">` → crimson, larger, underlined (ID wins!)
- Inline paragraph → purple bold (inline style wins over everything)

---

### Stage 5 — Final Reflection

Your completed `style.css` should look like:

```css
body {
  font-family: Arial, sans-serif;
  margin: 40px;
  background-color: #f4f4f4;
}

h1 {
  color: navy;
}

/* Element level: 0-0-1 */
p {
  color: grey;
  font-size: 16px;
}

/* Class level: 0-1-0 */
.featured {
  color: darkgreen;
  font-weight: bold;
}

.container {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
}

/* ID level: 1-0-0 */
#hero-text {
  color: crimson;
  font-size: 20px;
  text-decoration: underline;
}
```

**Reflection questions:**
1. What colour would `#hero-text` be if you removed the `#hero-text` rule? (Answer: dark green — the `.featured` class would take over.)
2. What if you also removed `.featured`? (Answer: grey — the `p` element selector would apply.)
3. Can any stylesheet rule override the inline style on the purple paragraph? (Without `!important`, no.)

---

### Optional Extension Challenge

Add a second ID rule that conflicts with the first:

```css
#hero-text        { color: crimson; }  /* weight: 1-0-0 */
p#hero-text       { color: darkorange; } /* weight: 1-0-1 ← should win */
```

**Expected Output:** "Hero paragraph" appears in **dark orange** because `p#hero-text` (1-0-1) beats `#hero-text` (1-0-0).

---

## Common Beginner Mistakes

### Mistake 1 — Thinking Order Always Matters

**Wrong thinking:** "My rule comes after the other one, so it should win."

**Correction:** Order only matters when specificity weights are **equal**. If they are different, the higher weight always wins regardless of order.

```css
#demo  { color: blue; }    /* weight: 1-0-0 */
p      { color: red; }     /* weight: 0-0-1 — comes after but LOSES */
```

**Output:** Blue. The ID beats the element selector no matter the order.

---

### Mistake 2 — Adding More Classes Does Not Beat an ID

**Wrong thinking:** "I have three classes on my selector, so it must beat an ID."

```css
.a.b.c { color: green; }   /* weight: 0-3-0 */
#demo  { color: blue; }    /* weight: 1-0-0 */
```

**Correction:** No number of class selectors can ever beat a single ID selector. The X column (ID count) is always more powerful than the Y column (class count). **0-3-0** loses to **1-0-0**.

---

### Mistake 3 — Forgetting That Combined Selectors Add Up

**Wrong thinking:** "p#demo is the same as #demo."

```css
#demo   { color: blue; }    /* weight: 1-0-0 */
p#demo  { color: orange; }  /* weight: 1-0-1 — WINS */
```

**Correction:** `p#demo` adds the weight of both `p` (an element) and `#demo` (an ID), giving a total of **1-0-1**, which is more than `#demo` alone at **1-0-0**.

---

### Mistake 4 — Thinking Inline Styles Can Be Overridden Without `!important`

```html
<p style="color: purple;">I am always purple.</p>
```

```css
#demo  { color: blue; }   /* Cannot override the inline style */
```

**Correction:** Inline styles override all stylesheet selectors. The only way to beat an inline style in your CSS is to use `!important` (which is covered in the next lesson).

---

### Mistake 5 — Confusing `:where()` and Regular Pseudo-classes

Regular pseudo-classes like `:hover` or `:focus` have weight **0-1-0**. But the special `:where()` function has weight **0-0-0** — it intentionally carries no specificity so it can be easily overridden. These are not the same.

```css
p:hover  { color: blue; }    /* weight: 0-1-1 */
:where(p) { color: red; }   /* weight: 0-0-0 — always loses */
```

---

## Reflection Questions

Work through these questions to solidify your understanding:

1. What is specificity and why does the browser need it?
2. List the four types of selectors in order from lowest to highest specificity weight.
3. You have the rule `div.sidebar ul li a`. What is its specificity weight?
4. Two rules both have weight **0-2-1**. How does the browser decide which one to apply?
5. Your inline style is setting a background colour, but you want your stylesheet to override it. What would you need to use?
6. Why is it generally considered bad practice to rely on ID selectors for styling?
7. A classmate says "I'll just add five classes to my selector to beat the ID". Why won't this work?

---

## Completion Checklist

Use this to check your understanding before moving on:

- [ ] I can explain what CSS specificity is in my own words.
- [ ] I understand that the browser compares rules and applies the highest-weight rule.
- [ ] I know the four selector types and their X-Y-Z weights: element (0-0-1), class (0-1-0), ID (1-0-0), inline (highest).
- [ ] I understand that inline styles override all stylesheet selectors.
- [ ] I can manually calculate the specificity weight of a complex selector.
- [ ] I know that when weights are equal, the rule that appears last in the stylesheet wins.
- [ ] I can predict which colour will display when multiple conflicting rules target the same element.
- [ ] I completed the mini project and observed the four specificity levels in action.
- [ ] I understand that combining selectors adds their weights together.
- [ ] I know that no number of class selectors can beat a single ID selector.

---

## Lesson Summary

CSS **specificity** is the algorithm browsers use to decide which style rule to apply when more than one rule targets the same element with the same property.

Every CSS selector carries a **weight** expressed as three numbers: **X-Y-Z**.

- **X** counts ID selectors (`#name`) — the most powerful.
- **Y** counts class selectors (`.name`), attribute selectors (`[attr]`), and pseudo-classes (`:hover`).
- **Z** counts element selectors (`p`, `h1`) and pseudo-elements (`::before`).

The browser compares weights from left to right. The rule with the higher weight wins. If weights are equal, the rule written **later** in the stylesheet wins (the cascade).

**Inline styles** (written directly on an HTML element with the `style` attribute) override every stylesheet rule. The only way to beat inline styles in a stylesheet is with `!important`, which you will learn in the next lesson.

**The complete priority order:**
```
Inline styles  >  ID selectors  >  Classes  >  Elements  >  Universal (*)
```

Understanding specificity means you can write confident, predictable CSS — knowing exactly which rule will win without trial and error.

---

*Sources: W3Schools CSS Specificity, W3Schools CSS Specificity Hierarchy, W3Schools CSS Specificity Code Challenge*
