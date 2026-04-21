---
render_with_liquid: false
title: "CSS Inheritance"
nav_order: 39
---

# Lesson 39: CSS Inheritance

---

## Lesson Introduction

Have you ever wondered why, when you set a font colour on a big container, all the text inside it automatically picks up that same colour — even though you never said anything about colour for the smaller elements inside?

That is **CSS inheritance** at work.

In this lesson, you will learn exactly what inheritance is, why it exists, which CSS properties are inherited by default, which are not, and how you can take full control using the special keyword values `inherit`, `initial`, `unset`, and `revert`. By the end, you will build a mini-project — a styled blog-post card — that demonstrates everything in action.

> **No prior knowledge of inheritance is needed.** If you know basic HTML structure (parent and child elements) and can write simple CSS rules, you are ready.

---

## Prerequisite Concepts

Before diving into inheritance, make sure you are comfortable with these ideas. If anything here is new, read it carefully — you will need it throughout the lesson.

### What is a Parent Element and a Child Element?

In HTML, elements are **nested** inside each other. The outer element is the **parent**. The element inside it is the **child**.

```html
<div>           <!-- parent -->
  <p>Hello</p>  <!-- child of div -->
</div>
```

Think of a folder on your computer. The folder is the parent. The files inside are the children.

### What is a CSS Property?

A CSS property is a style instruction, like `color`, `font-size`, `border`, or `background-color`. You write it in a CSS rule like this:

```css
selector {
  property: value;
}
```

For example:

```css
p {
  color: red;
}
```

This sets the text colour of every `<p>` element to red.

### What is the Document Tree (DOM)?

The HTML page is organised as a tree. The `<html>` element is the root. Inside it is `<body>`. Inside `<body>` are your headings, paragraphs, divs, and so on. Each element can have children, and each child can have its own children.

```
html
└── body
    ├── h1
    └── div
        ├── p
        │   └── span
        └── ul
            ├── li
            └── li
```

Understanding this tree is the key to understanding inheritance, because styles travel **down** the tree from parent to child.

---

## Part 1: Conceptual Understanding — What Is CSS Inheritance?

### The Big Idea

**CSS inheritance is the mechanism by which some CSS property values set on a parent element are automatically passed down to child elements — unless the child has its own rule that overrides it.**

Imagine a family. A parent has blue eyes. Their child might inherit those blue eyes automatically without any extra effort. But if the child has brown eyes, that overrides the inherited trait.

CSS works the same way.

### Why Does Inheritance Exist?

Inheritance exists to save you from writing the same styles over and over again. Without it, you would have to manually write `font-family: Arial` on every single element on your page — every heading, paragraph, list item, span, and button. That would be incredibly tedious.

With inheritance, you write it **once on a parent**, and all the children automatically pick it up.

> **Real-world analogy:** Think of a company-wide memo that says "All employee emails must use Arial font, size 12." Every employee follows this rule without needing their own individual memo — unless a specific team has their own overriding instruction.

### How Does It Work? The Three-Step Process

When the browser needs to decide what value a CSS property has on an element, it follows this logic:

**Step 1 — Does the element have its own rule?**
If yes, use that value.

**Step 2 — Is the property inherited?**
If the element has no rule, and the property is an *inherited property*, the browser looks at the element's parent. If the parent has a value, the child uses that value.

**Step 3 — Use the initial value.**
If the property is *not inherited* and the element has no rule, the browser uses the property's default "initial" value (defined in the CSS specification).

---

## Part 2: Inherited vs. Non-Inherited Properties

Not every CSS property is inherited. The CSS language decides which ones are.

### Properties That ARE Inherited by Default

These are mostly **text-related** properties. It makes sense — if you set a font for a section, you want everything inside that section to use the same font.

Here are the most common inherited properties:

- `color`
- `font-family`
- `font-size`
- `font-style` (normal, italic)
- `font-weight` (normal, bold)
- `font-variant`
- `font` (shorthand)
- `letter-spacing`
- `line-height`
- `text-align`
- `text-indent`
- `text-transform`
- `visibility`
- `word-spacing`
- `list-style` (and its sub-properties)
- `cursor`

> **Memory tip:** If it affects how **text looks or behaves**, it is probably inherited.

### Properties That Are NOT Inherited by Default

These are mostly **layout and box** properties. It would cause chaos if every child automatically had the same border or margin as its parent.

Here are common non-inherited properties:

- `border`
- `margin`
- `padding`
- `background-color`
- `background-image`
- `width`
- `height`
- `position`
- `display`
- `float`
- `overflow`
- `box-shadow`
- `opacity` *(special — see note below)*

> **Note on `opacity`:** `opacity` is technically *not* inherited, but it visually affects children because children are painted *inside* the parent. If a parent has `opacity: 0.5`, the children will appear at 50% opacity too — even though they did not inherit the `opacity` property. This is different from true inheritance.

---

## Part 3: Simple Examples of Inheritance in Action

### Example 1 — `color` Is Inherited

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      color: blue;
    }
  </style>
</head>
<body>
  <div>
    <p>This paragraph is inside the div.</p>
    <span>This span is also inside the div.</span>
  </div>
</body>
</html>
```

**What happens?**

The `<div>` is set to `color: blue`. The `<p>` and `<span>` are children of the `<div>`. They have no `color` rule of their own. Because `color` is an inherited property, they inherit the blue colour from the `<div>`.

**Expected output in the browser:**
- "This paragraph is inside the div." — displayed in **blue**
- "This span is also inside the div." — displayed in **blue**

> **Ask yourself:** What would happen if you added `color: red` directly to the `<p>`? The `<p>` would show red, because its own rule overrides the inherited blue. Try it!

---

### Example 2 — `border` Is NOT Inherited

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      border: 2px solid black;
    }
  </style>
</head>
<body>
  <div>
    <p>This paragraph is inside the div.</p>
  </div>
</body>
</html>
```

**What happens?**

The `<div>` has a black border. The `<p>` inside it has no `border` rule. Because `border` is **not** an inherited property, the `<p>` does **not** get a border.

**Expected output in the browser:**
- The `<div>` has a black border around it.
- The `<p>` inside has **no** border.

> **Ask yourself:** Why is this a good thing? Imagine if every `<span>` and `<p>` automatically got the same border as its parent container — pages would look cluttered and uncontrollable!

---

### Example 3 — Inheritance Travels Multiple Levels

Inheritance passes down the entire family tree, not just one level.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: Georgia, serif;
      font-size: 18px;
      color: #333;
    }
  </style>
</head>
<body>
  <div>
    <p>This is a paragraph. <span>This is a span inside the paragraph.</span></p>
  </div>
</body>
</html>
```

**The family tree here:**
`body` → `div` → `p` → `span`

**What happens?**

The `body` has `font-family: Georgia`, `font-size: 18px`, and `color: #333`. None of the child elements (`div`, `p`, `span`) have their own font or colour rules. They all inherit from `body`.

**Expected output in the browser:**
- All text on the page appears in Georgia font, 18px, dark grey colour.
- This includes the text in `<p>` and the nested `<span>`.

> **Real-world use:** Web developers almost always set a base `font-family`, `font-size`, and `color` on `body` or a root element, and let all children inherit those values. This creates consistent typography with minimal code.

---

## Part 4: The Four Special Keyword Values That Control Inheritance

CSS gives you four powerful keywords that let you **take control** of what value an element uses. You can use these as the value for any property.

---

### Keyword 1: `inherit`

**What it does:** Forces the element to use the **inherited value** from its parent, even for properties that are not normally inherited.

**When to use it:** When a property is not inherited by default (like `border` or `background-color`), but you *want* a child to copy its parent's value.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      border: 3px dashed purple;
    }
    p {
      border: inherit;  /* Force the p to inherit the border from div */
    }
  </style>
</head>
<body>
  <div>
    <p>This paragraph inherits the border from its parent div.</p>
  </div>
</body>
</html>
```

**Expected output:**
- The `<div>` has a 3px dashed purple border.
- The `<p>` inside **also** has a 3px dashed purple border (because of `border: inherit`).

> **Think about it:** Without `border: inherit`, the `<p>` would have no border. The keyword forces it to copy the parent's value.

---

### Keyword 2: `initial`

**What it does:** Resets the property to its **original default value** as defined by the CSS specification — ignoring anything inherited from a parent.

**When to use it:** When you want to remove an inherited or explicitly-set value and go back to square one.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      color: red;
    }
    p {
      color: initial;  /* Reset color back to the CSS default (black) */
    }
  </style>
</head>
<body>
  <p>This paragraph's color is reset to the initial value.</p>
  <span>This span still inherits red from body.</span>
</body>
</html>
```

**Expected output:**
- The `<span>` text appears in **red** (inherited from `body`).
- The `<p>` text appears in the browser's default colour, which is **black** (reset to initial).

> **Important:** `initial` does not mean "the browser's default style". It means "the CSS specification's initial value for this property". For `color`, the CSS initial value is `CanvasText` (which renders as black in most browsers). For `display`, the initial value is `inline`, not `block` — which can surprise you if you use `display: initial` on a `<div>`.

---

### Keyword 3: `unset`

**What it does:** Works like a smart combination of `inherit` and `initial`:
- If the property is naturally **inherited**, `unset` acts like `inherit`.
- If the property is naturally **not inherited**, `unset` acts like `initial`.

**When to use it:** When you want to completely remove your custom styling and let the property fall back to its natural behaviour — without having to know whether it is inherited or not.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      color: navy;
    }
    div {
      color: green;
      border: 2px solid orange;
    }
    p {
      color: unset;   /* color IS inherited, so acts like inherit → uses navy from body */
      border: unset;  /* border is NOT inherited, so acts like initial → no border */
    }
  </style>
</head>
<body>
  <div>
    <p>This paragraph uses unset for both color and border.</p>
  </div>
</body>
</html>
```

**Expected output:**
- The `<div>` has green text and an orange border.
- The `<p>` has **navy** text (unset on an inherited property → inherits from `body`, skipping the `div`'s green).
- The `<p>` has **no border** (unset on a non-inherited property → initial = no border).

> **Why is this useful?** `unset` is particularly powerful in CSS resets and when overriding third-party CSS. You can use `all: unset` to wipe all styles from an element at once.

---

### Keyword 4: `revert`

**What it does:** Reverts the property value to the **browser's default stylesheet** value (what the browser would normally apply without any author CSS).

**The difference from `initial`:** `initial` goes back to the CSS specification default. `revert` goes back to what the browser itself would apply (the user-agent stylesheet). For most elements, this is very similar, but for elements like `<h1>` and `<p>`, the browser has its own default sizes and margins that `initial` would remove but `revert` would restore.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    h1 {
      font-size: 14px;   /* We made h1 tiny */
      font-weight: normal;
    }
    h1.restore {
      font-size: revert;      /* Go back to browser's default for h1 (usually ~2em or 32px) */
      font-weight: revert;    /* Go back to browser's default (bold) */
    }
  </style>
</head>
<body>
  <h1>This h1 is styled tiny and non-bold.</h1>
  <h1 class="restore">This h1 is reverted to browser defaults.</h1>
</body>
</html>
```

**Expected output:**
- First `<h1>`: tiny text, not bold.
- Second `<h1>`: large and bold — back to how the browser would normally render it.

---

### Quick Summary Table of the Four Keywords

| Keyword   | What it Does                                                  | Use Case                                         |
|-----------|---------------------------------------------------------------|--------------------------------------------------|
| `inherit` | Forces the element to use its parent's computed value         | Make non-inherited properties behave as inherited|
| `initial` | Resets to CSS specification default value                     | Strip all custom styling back to spec default    |
| `unset`   | `inherit` if the property is inherited, `initial` if not      | Smart reset that respects natural inheritance    |
| `revert`  | Reverts to browser (user-agent) stylesheet default            | Undo your custom styles, keep browser defaults  |

---

## Part 5: The `all` Shorthand Property

CSS provides a special shorthand property called `all` that lets you apply one of the four keywords to **every single CSS property** of an element at once.

### What is `all`?

`all` is a CSS property that represents every other CSS property (except `unicode-bidi` and `direction`). You can only give it one of the four values: `inherit`, `initial`, `unset`, or `revert`.

### Example: `all: unset`

This is commonly used to create a completely unstyled element — useful for custom components where you want to start fresh.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: Arial;
      color: darkred;
      font-size: 20px;
    }
    button {
      all: unset; /* Strip every browser and inherited style from the button */
      cursor: pointer;
    }
  </style>
</head>
<body>
  <p>This text inherits font and color from body.</p>
  <button>This button has all styles unset.</button>
</body>
</html>
```

**Expected output:**
- The `<p>` appears in Arial, darkred, 20px.
- The `<button>` has no browser default button styling (no border, no background, no padding) because all styles are unset. It displays as plain text.

> **Real-world use:** `all: unset` is widely used in UI component libraries when building custom buttons, inputs, and interactive elements where you want zero inherited or browser-default styling as your starting point.

---

## Part 6: Guided Practice Exercises

Work through each exercise carefully. Read the objective, write the code, check your output.

---

### Exercise 1 — Warm-Up: Let Inheritance Do the Work

**Objective:** Understand that a single style on a parent can style all its children automatically.

**Scenario:** You are building a blog post. You want all text inside the article to use a comfortable reading font and a soft dark colour.

**Instructions:**
1. Create an HTML file with an `<article>` element.
2. Inside the article, put an `<h2>`, two `<p>` elements, and a `<ul>` with three `<li>` elements.
3. Write a CSS rule that sets `font-family: Georgia, serif`, `font-size: 17px`, and `color: #444` **only on the `article` element**.
4. Open the file in a browser and observe.

**Expected output:**
All text inside the article — the heading, paragraphs, and list items — should appear in Georgia font, 17px, dark grey colour. You wrote the style only once.

**Self-check questions:**
- Did the `<li>` elements also get the Georgia font, even though you didn't style them directly?
- What would happen if you added `color: crimson` to just the `<h2>`?

**Hint:** Think about which element is the parent and which are the children.

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    article {
      font-family: Georgia, serif;
      font-size: 17px;
      color: #444;
    }
  </style>
</head>
<body>
  <article>
    <h2>The Power of Inheritance</h2>
    <p>CSS inheritance lets you write less code and maintain consistency.</p>
    <p>Once you understand it, styling pages becomes much faster.</p>
    <ul>
      <li>Reduces repetition</li>
      <li>Creates consistent design</li>
      <li>Easy to override when needed</li>
    </ul>
  </article>
</body>
</html>
```

**Expected output:** All text inside `<article>` appears in Georgia, 17px, #444 — including the `<li>` items and the `<h2>`.

---

### Exercise 2 — Overriding Inheritance

**Objective:** Understand that a child's own rule overrides what it would inherit from a parent.

**Scenario:** You have a section with a default text colour, but one paragraph should stand out in a different colour.

**Instructions:**
1. Create a `<section>` with `color: steelblue`.
2. Inside the section, add three `<p>` elements.
3. Give the second `<p>` a class of `highlight` and set `color: darkorange` on it.
4. Observe which paragraphs are blue and which is orange.

**Expected output:**
- Paragraph 1: **steel blue** (inherited)
- Paragraph 2: **dark orange** (own rule overrides inheritance)
- Paragraph 3: **steel blue** (inherited)

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    section {
      color: steelblue;
    }
    .highlight {
      color: darkorange;
    }
  </style>
</head>
<body>
  <section>
    <p>Paragraph one — inherited blue.</p>
    <p class="highlight">Paragraph two — own rule: orange.</p>
    <p>Paragraph three — inherited blue again.</p>
  </section>
</body>
</html>
```

> **Thinking prompt:** What happens if you remove the `.highlight` rule? All three paragraphs become blue. What if you also set `color: inherit` on `.highlight` explicitly?

---

### Exercise 3 — Using `inherit` to Force Non-Inherited Properties

**Objective:** Practice using the `inherit` keyword on a property that is not naturally inherited.

**Scenario:** You want all direct links inside a navigation bar to match the nav bar's text colour, even though `color` on `<a>` tags is overridden by the browser's default link styling.

**Background to know:** By default, browser stylesheets make `<a>` tags blue and underlined. When you set `color` on a parent, links inside it will **not** automatically pick up that colour — because the browser's default style for `<a>` overrides inheritance.

**Instructions:**
1. Create a `<nav>` element with `color: white` and `background-color: #222`.
2. Inside the nav, add three `<a>` links.
3. First, check what the links look like without any `<a>` styling (they will be blue — browser default wins).
4. Then add `color: inherit` to your `<a>` selector.
5. Observe the difference.

**Expected output:**
- Without `color: inherit`: links appear blue (browser default).
- With `color: inherit`: links appear **white** (inherited from the `<nav>`).

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    nav {
      background-color: #222;
      color: white;
      padding: 10px;
    }
    nav a {
      color: inherit; /* Force link to inherit white from nav */
      margin-right: 20px;
      text-decoration: none;
    }
  </style>
</head>
<body>
  <nav>
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Contact</a>
  </nav>
</body>
</html>
```

**Expected output:** All three links appear in white text on a dark background, matching the nav's colour.

---

### Exercise 4 — Using `initial` to Reset a Property

**Objective:** Practice using `initial` to completely strip an inherited value.

**Scenario:** Your entire page uses dark green text. You have a warning box that must use the browser's default text colour (black), regardless of what is inherited.

**Instructions:**
1. Set `color: darkgreen` on `<body>`.
2. Create a `<div class="warning">` with a yellow background.
3. Inside the warning, add a `<p>`.
4. Use `color: initial` on the `.warning` class.
5. Observe the result.

**Expected output:**
- All other text on the page: **dark green** (inherited from body)
- Text inside `.warning`: **black** (reset to CSS initial value for `color`)

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      color: darkgreen;
      font-size: 16px;
    }
    .warning {
      background-color: #fffacd;
      border: 1px solid #f0c040;
      padding: 10px;
      color: initial; /* Reset to CSS default: black */
    }
  </style>
</head>
<body>
  <p>This text inherits dark green from body.</p>
  <div class="warning">
    <p>Warning: this text is reset to the initial color (black).</p>
  </div>
  <p>Back to dark green again.</p>
</body>
</html>
```

---

### Exercise 5 — Using `unset` in Practice

**Objective:** See how `unset` adapts to whether a property is inherited or not.

**Instructions:**
1. Set `color: purple` on `<body>`.
2. Create a `<div>` with `color: teal` and `border: 3px solid red`.
3. Inside the `<div>`, add a `<p>` with `color: unset` and `border: unset`.
4. Observe what the paragraph's colour and border end up being.

**Expected output:**
- The `<p>` colour: **purple** (unset on `color` → acts like inherit → skips div's teal → gets body's purple)
- The `<p>` border: **none** (unset on `border` → acts like initial → initial value of border is none)

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      color: purple;
    }
    div {
      color: teal;
      border: 3px solid red;
    }
    p {
      color: unset;   /* Inherited property → behaves like inherit → gets purple from body */
      border: unset;  /* Non-inherited property → behaves like initial → no border */
    }
  </style>
</head>
<body>
  <div>
    <p>What color am I? What border do I have?</p>
  </div>
</body>
</html>
```

> **Challenge:** Change `color: unset` to `color: inherit`. Does the result change? (Yes — `inherit` would grab teal from the immediate parent `<div>`, not purple from `<body>`. `unset` goes to the natural inherited value which follows the full cascade.)

---

## Part 7: Common Beginner Mistakes

These are the mistakes that beginners almost always make when learning CSS inheritance. Study them carefully so you can avoid them.

---

### Mistake 1 — Assuming ALL Properties Are Inherited

**Wrong thinking:** "I set `border: 2px solid black` on my `<div>`, so all the `<p>` elements inside should also have that border."

**What actually happens:** `border` is not inherited. Child elements will have no border.

**Fix:** If you want children to have the same border, you must either write a CSS rule targeting them directly, or use `border: inherit` on the children.

```css
/* Wrong assumption — border does NOT automatically pass to children */
div {
  border: 2px solid black;
}

/* Fix option 1: Target children directly */
div p {
  border: 2px solid black;
}

/* Fix option 2: Force inheritance */
div p {
  border: inherit;
}
```

---

### Mistake 2 — Confusing `initial` with "Browser Default"

**Wrong thinking:** "`initial` gives me the browser's default style for this element."

**What actually happens:** `initial` gives you the **CSS specification's** initial value, not the browser's. For `font-size`, the CSS initial value is `medium` (not the browser's 16px rendering of it). For `display`, initial is `inline` — so `display: initial` on a `<div>` makes it inline, which might surprise you.

**Fix:** If you want the browser's default styling for an element, use `revert`, not `initial`.

```css
/* Wrong: This makes the h1 display inline (CSS spec initial for display) */
h1 {
  display: initial;
}

/* Correct: This restores the browser's default display for h1 (block) */
h1 {
  display: revert;
}
```

---

### Mistake 3 — Forgetting That `<a>` Tags Override Colour Inheritance

**Wrong thinking:** "I set `color: white` on my navigation. All text inside, including links, will be white."

**What actually happens:** The browser's built-in stylesheet sets `<a>` colour to blue (or purple for visited). This overrides the inherited colour. You must explicitly set `color: inherit` (or a specific colour) on `<a>` elements.

```css
/* Wrong — links will still be blue despite the parent having white */
nav {
  color: white;
}

/* Correct — explicitly force links to use the parent's colour */
nav a {
  color: inherit;
}
```

---

### Mistake 4 — Using `all: unset` and Losing Important Behaviour

**Wrong thinking:** "I'll use `all: unset` on my button to strip all styles."

**What actually happens:** `all: unset` removes everything — including `cursor: pointer`, `display`, and focus outlines. Your element may become inaccessible or behave unexpectedly.

**Fix:** After `all: unset`, add back the essential properties you need:

```css
button {
  all: unset;
  cursor: pointer;       /* Restore pointer cursor */
  display: inline-block; /* Restore sensible display */
}

button:focus {
  outline: 2px solid blue; /* Restore focus indicator for accessibility */
}
```

---

### Mistake 5 — Expecting Inheritance Across Unrelated Elements

**Wrong thinking:** "My `<h1>` has red text. My `<p>` should also get red text from it."

**What actually happens:** Inheritance only travels **down** the document tree — from parent to child. Sibling elements (elements at the same level) do not inherit from each other. A `<p>` after an `<h1>` is not the `<h1>`'s child; they are siblings. Only a common ancestor can pass styles to both.

```html
<!-- Wrong: thinking h1's color passes to p (they are siblings, not parent/child) -->
<h1 style="color: red;">Title</h1>
<p>Does this get red? NO — it is a sibling, not a child.</p>

<!-- Correct: wrap them in a parent and set color on the parent -->
<div style="color: red;">
  <h1>Title</h1>   <!-- inherits red -->
  <p>Paragraph</p> <!-- inherits red -->
</div>
```

---

## Part 8: Mini Project — Styled Blog Post Card

In this project, you will build a **blog post card** that uses CSS inheritance cleverly. You will set styles on parent elements and let children inherit them — then override only where needed. You will also use `inherit` and `initial` in context.

### Project Goal

Create a blog post card that looks like a simple article preview — with a heading, author name, paragraph text, a tag list, and a "Read More" link — all styled primarily through inheritance from a parent container.

---

### Stage 1 — HTML Setup

**Objective:** Build the HTML structure first.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Blog Post Card</title>
  <link rel="stylesheet" href="card.css">
</head>
<body>

  <div class="card">
    <h2 class="card-title">Understanding CSS Inheritance</h2>
    <p class="card-author">By Alex Johnson &bull; April 2026</p>
    <p class="card-excerpt">
      CSS inheritance is one of the most powerful but misunderstood features of 
      the language. Once you master it, you will write far less CSS and maintain 
      your stylesheets much more easily.
    </p>
    <ul class="card-tags">
      <li>CSS</li>
      <li>Web Design</li>
      <li>Beginner</li>
    </ul>
    <a href="#" class="card-link">Read More &rarr;</a>
  </div>

</body>
</html>
```

**Milestone output:** Plain, unstyled HTML rendered in the browser's defaults.

---

### Stage 2 — Set Up Inheritance on the Card Container

**Objective:** Use the `.card` as the parent. Set font, colour, and size there so all children inherit.

Create `card.css`:

```css
/* Stage 2: Inheritance base on .card */
body {
  background-color: #f0f4f8;
  margin: 40px;
}

.card {
  background-color: white;
  padding: 30px;
  border-radius: 8px;
  max-width: 500px;

  /* These will be inherited by all children */
  font-family: Georgia, "Times New Roman", serif;
  font-size: 16px;
  color: #2d2d2d;
  line-height: 1.7;
}
```

**Milestone output:** The card appears as a white rounded box. All text inside — title, author, excerpt, tags, link — automatically uses Georgia, 16px, dark grey, because they inherit from `.card`.

---

### Stage 3 — Override Specific Children

**Objective:** Now override only the things that need to look different from the inherited defaults.

Add to `card.css`:

```css
/* Stage 3: Override specific elements */

/* Title needs to be bigger and bolder */
.card-title {
  font-size: 1.5em;    /* 1.5 × the inherited 16px = 24px */
  font-weight: bold;
  color: #1a3a5c;      /* Override to a dark blue */
  margin-bottom: 6px;
}

/* Author line should be smaller and softer */
.card-author {
  font-size: 0.85em;   /* Smaller than inherited */
  color: #888;          /* Override to grey */
  font-style: italic;
}

/* Excerpt: uses inherited size and colour — no override needed */

/* Remove default list styling from tags */
.card-tags {
  list-style: none;
  padding: 0;
  display: flex;
  gap: 8px;
  margin: 14px 0;
}

.card-tags li {
  background-color: #e8f0fe;
  color: #1a3a5c;      /* Override to dark blue */
  padding: 3px 10px;
  border-radius: 20px;
  font-size: 0.8em;    /* Smaller than inherited */
}

/* Link: force it to inherit the parent's color (not browser blue) */
.card-link {
  color: inherit;      /* <-- inherit keyword in action */
  font-weight: bold;
  text-decoration: none;
  border-bottom: 2px solid currentColor;
}
```

**Milestone output:** The card now shows a clearly styled title in blue, a small grey italic author line, a clean excerpt in inherited dark grey, soft blue tags, and a bold "Read More" link that matches the card's text colour.

---

### Stage 4 — Using `initial` to Demonstrate Reset

Add one more rule to show how `initial` works in context:

```css
/* Stage 4: A reset demonstration */

/* If we ever need to show a "plain" version of a tag */
.card-tags li.plain-tag {
  color: initial;           /* Reset to CSS spec default (black) */
  background-color: initial; /* Reset to transparent */
  border: 1px solid #ccc;
}
```

In your HTML, add `class="plain-tag"` to the last `<li>`:

```html
<ul class="card-tags">
  <li>CSS</li>
  <li>Web Design</li>
  <li class="plain-tag">Beginner</li>
</ul>
```

**Milestone output:** The first two tags appear styled in blue. The last tag appears with no background colour and black text — because `initial` reset those properties.

---

### Final Complete CSS File

```css
body {
  background-color: #f0f4f8;
  margin: 40px;
}

.card {
  background-color: white;
  padding: 30px;
  border-radius: 8px;
  max-width: 500px;
  font-family: Georgia, "Times New Roman", serif;
  font-size: 16px;
  color: #2d2d2d;
  line-height: 1.7;
}

.card-title {
  font-size: 1.5em;
  font-weight: bold;
  color: #1a3a5c;
  margin-bottom: 6px;
}

.card-author {
  font-size: 0.85em;
  color: #888;
  font-style: italic;
}

.card-tags {
  list-style: none;
  padding: 0;
  display: flex;
  gap: 8px;
  margin: 14px 0;
}

.card-tags li {
  background-color: #e8f0fe;
  color: #1a3a5c;
  padding: 3px 10px;
  border-radius: 20px;
  font-size: 0.8em;
}

.card-tags li.plain-tag {
  color: initial;
  background-color: initial;
  border: 1px solid #ccc;
}

.card-link {
  color: inherit;
  font-weight: bold;
  text-decoration: none;
  border-bottom: 2px solid currentColor;
}
```

---

### Reflection Questions

1. How many times did you write `font-family: Georgia` in your CSS? Why did it only need to appear once?
2. The `.card-author` changed `color` to `#888`. Is this overriding inheritance or using it?
3. The `.card-link` uses `color: inherit`. What would the link look like without that rule?
4. Why does the `.plain-tag` use `color: initial` instead of `color: black`?
5. Optional extension: What would happen if you added `color: red` to the `body`? Which elements would be affected and which would not?

---

## Part 9: Reflection Questions for the Full Lesson

Answer these questions in your own words to test your understanding:

1. What is CSS inheritance in one sentence?
2. Name three CSS properties that are inherited by default.
3. Name three CSS properties that are NOT inherited by default.
4. What is the difference between `inherit` and `initial`?
5. What is the difference between `initial` and `revert`?
6. When would you use `all: unset`? What extra steps should you take after using it?
7. Why do `<a>` links often need `color: inherit` even when the parent has a colour set?
8. Inheritance travels in which direction — up the tree, down the tree, or sideways?
9. What does `unset` do for a property that is not naturally inherited?
10. How is `opacity` different from a truly inherited property, even though children visually appear to share the parent's opacity?

---

## Completion Checklist

Before you move on, confirm you can tick each item:

- [ ] I can explain what CSS inheritance is in plain language
- [ ] I know the difference between inherited and non-inherited CSS properties
- [ ] I can give at least three examples of each type
- [ ] I understand what `inherit` does and when to use it
- [ ] I understand what `initial` does and the difference from browser defaults
- [ ] I understand what `unset` does for inherited vs. non-inherited properties
- [ ] I understand what `revert` does and when it differs from `initial`
- [ ] I know what `all: unset` does and the caution needed after using it
- [ ] I completed all five guided exercises and checked the outputs
- [ ] I built the blog card mini-project and can explain each CSS decision
- [ ] I know the five common beginner mistakes and how to avoid them
- [ ] I answered the reflection questions in my own words

---

## Lesson Summary

CSS inheritance is the automatic passing of certain CSS property values from a **parent element** down to its **child elements**. It exists to reduce repetition and create consistent styling with minimal code.

**Key points to remember:**

Text-related properties — like `color`, `font-family`, `font-size`, `line-height`, and `text-align` — are inherited by default. Layout and box properties — like `border`, `margin`, `padding`, `background-color`, and `width` — are not inherited.

When an element has no explicit value for an inherited property, it uses its parent's computed value. When an element has no explicit value for a non-inherited property, it uses the CSS specification's initial value.

You have four keywords to take full control:

- **`inherit`** — force any property to use the parent's value
- **`initial`** — reset any property to the CSS specification's default
- **`unset`** — smart reset: inherits if the property is naturally inherited; uses initial if not
- **`revert`** — restore the browser's (user-agent) default styling

The shorthand **`all`** applies one of these keywords to every CSS property at once (`all: unset` is commonly used to create zero-styling starting points for components).

In professional web development, inheritance is leveraged constantly: a base `font-family`, `color`, and `font-size` are set once on `body` or a wrapper element, and the entire page's typography is established through inheritance. Targeted overrides handle the exceptions — not the rule.

---

*End of Lesson 39: CSS Inheritance*
