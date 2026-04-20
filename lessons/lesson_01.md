---
render_with_liquid: false
title: "Introduction to CSS — What It Is, Why It Exists, and How It Works"
nav_order: 1
---

# Lesson 01 — Introduction to CSS: What It Is, Why It Exists, and How It Works

---

## Lesson Introduction

Welcome! In this lesson, you will take your very first steps into the world of **CSS** — one of the most important technologies used to build websites and web applications.

By the time you finish this lesson, you will be able to:

- Explain what CSS is and why it was created
- Understand how CSS and HTML work together
- Write a complete, correct CSS rule from memory
- Know the names and roles of every part of a CSS rule
- Spot and fix common CSS mistakes
- Apply CSS to a real mini-project

You do not need any previous knowledge to start. This lesson will teach you everything from the ground up. Even if you have never written a single line of code before, you are in the right place.

---

## Prerequisite Concepts — Things You Need to Know First

Before we dive into CSS, we need to briefly explain one idea that CSS depends on: **HTML**.

### What is HTML?

**HTML** stands for **HyperText Markup Language**. It is the language used to build the *structure* of a web page — like the skeleton of a building. It defines things like headings, paragraphs, images, and links.

Here is a simple HTML example:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My First Page</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
    <p>This is a paragraph of text.</p>
  </body>
</html>
```

**What does this produce?**

```
Hello, World!
This is a paragraph of text.
```

The page appears plain and unstyled — just raw black text on a white background. It has structure, but no design. That is where CSS comes in.

> 💡 **Analogy:** Think of HTML as the bricks and concrete of a building (structure), and CSS as the paint, wallpaper, and furniture (appearance).

---

## Section 1 — What Is CSS?

### The Simple Definition

**CSS** stands for **Cascading Style Sheets**.

CSS is the language used to control how HTML elements *look* on a screen, on a printed page, or in any other display medium.

Without CSS, every webpage would look like a plain, unstyled document — like a Word document with no formatting. CSS is what makes websites look colourful, professional, and beautiful.

### Breaking Down the Name

Let us look at each word in "Cascading Style Sheets" so you understand exactly what it means:

- **Cascading** — CSS rules can come from multiple places (your file, the browser's defaults, inline styles). The word "cascading" describes how these rules flow together and how conflicts between them are resolved. We will learn more about this later.
- **Style** — CSS controls the visual style: colours, fonts, sizes, spacing, layout, and more.
- **Sheets** — CSS rules are usually written in a separate file (a "sheet"), though they can also appear inside an HTML file.

### What Can CSS Control?

CSS can control almost every visual aspect of a webpage, including:

- **Colours** — background colour, text colour, border colour
- **Fonts** — font family, font size, bold, italic
- **Layout** — where elements sit on the page, how wide they are, how much space surrounds them
- **Spacing** — the gap inside an element (padding) and outside an element (margin)
- **Borders** — lines drawn around elements
- **Animations** — moving and transitioning elements smoothly
- **Responsive design** — making pages look good on phones, tablets, and desktops

### CSS Saves a Huge Amount of Work

Here is one of the most important things to understand about CSS: **a single CSS file can control the appearance of an entire website** — dozens or hundreds of pages at once.

Imagine you have a website with 100 pages and you want to change the colour of all your headings from black to blue. Without CSS, you would need to open every single page and change each heading individually. With CSS, you open *one* CSS file, change one line, and every page on your website updates automatically.

This is why CSS exists. It separates the *content* (HTML) from the *design* (CSS), making large websites much easier to manage.

---

## Section 2 — CSS and HTML: How They Work Together

Think of building a webpage like decorating a room:

- **HTML** = the walls, furniture, and objects in the room
- **CSS** = the paint on the walls, the colour of the furniture, the size of the windows

HTML creates the *things* on the page. CSS decides how those *things look*.

### A Real-World Analogy

Imagine a restaurant menu. The words on the menu (dish names, descriptions, prices) are like **HTML** — they are the content. But whether those words appear in a fancy gold font on dark paper, or in plain black on white paper, or in a big red title — that is like **CSS**. The content is the same; only the presentation changes.

### Seeing CSS In Action

Look at the same HTML page below, first without CSS and then with CSS applied:

**HTML only (no CSS):**

```html
<h1>Welcome to My Bakery</h1>
<p>We bake fresh bread every morning.</p>
```

**Output (no CSS):**

```
Welcome to My Bakery
We bake fresh bread every morning.
```

Plain, black text. No colour. No personality.

**Same HTML with CSS applied:**

```css
h1 {
  color: darkred;
  font-size: 36px;
  text-align: center;
}

p {
  color: gray;
  font-size: 18px;
  font-family: Georgia, serif;
}
```

**Output (with CSS):**

The heading appears large, dark red, and centred. The paragraph appears smaller, grey, and in an elegant serif font. Same HTML content — completely different visual experience.

> 💡 **Thinking Prompt:** What would happen if you changed `color: darkred` to `color: blue`? The heading would appear blue instead. CSS gives you that kind of control instantly.

---

## Section 3 — CSS Syntax: The Grammar of CSS

Every programming language or styling language has a **syntax** — a set of rules about how you must write your code so the computer understands it. CSS syntax is very simple and follows a consistent pattern.

### The Three Parts of a CSS Rule

A complete CSS instruction is called a **CSS rule**. Every CSS rule is made up of exactly three parts:

1. **Selector** — tells CSS *which* HTML element to style
2. **Property** — tells CSS *what* aspect to change (colour, size, font, etc.)
3. **Value** — tells CSS *how* to change it (red, 20px, bold, etc.)

Here is the pattern:

```
selector {
  property: value;
}
```

And here is a real example:

```css
p {
  color: red;
}
```

Let us break every character down:

| Part | What it is | What it does |
|------|-----------|--------------|
| `p` | Selector | Targets all `<p>` (paragraph) HTML elements |
| `{` | Opening curly brace | Opens the "instruction block" — everything inside applies to the selector |
| `color` | Property | The visual aspect we want to change — in this case, the text colour |
| `:` | Colon | Separates the property name from its value |
| `red` | Value | The specific setting for the property — make the text red |
| `;` | Semicolon | Marks the end of this one declaration. Required if there are more below it. |
| `}` | Closing curly brace | Closes the instruction block |

### The Correct Terms to Know

CSS professionals use specific words for these parts:

- The `selector + { ... }` together is called a **CSS rule** (or "rule set")
- The part inside the curly braces is called the **declaration block**
- Each single `property: value;` line inside the block is called a **declaration**
- The word on the left of the colon (`:`) is the **property**
- The word on the right of the colon (`:`) is the **value**

```css
/* Full structure labelled: */

p              /* ← SELECTOR */
{              /* ← Opening brace of DECLARATION BLOCK */
  color: red;  /* ← DECLARATION (property: value;) */
}              /* ← Closing brace of DECLARATION BLOCK */
```

### Multiple Declarations in One Rule

You can write as many declarations as you want inside one rule block. Each declaration must end with a semicolon (`;`).

**Example with three declarations:**

```css
p {
  color: red;
  text-align: center;
  font-size: 20px;
}
```

**What this does:**

- `color: red;` — makes the text red
- `text-align: center;` — centres the text horizontally
- `font-size: 20px;` — makes the text 20 pixels tall

**Expected Output:** All paragraphs (`<p>` elements) on the page appear with red text, centred, at a size of 20 pixels.

> 💡 **Thinking Prompt:** What would happen if you removed the semicolon after `color: red`? Many browsers will still understand it if it is the last declaration, but it is considered bad practice and can cause bugs when you add more declarations later. Always use semicolons.

### Multiple Rules for Different Selectors

You can write as many CSS rules as you need — one for each type of HTML element you want to style:

```css
body {
  background-color: lightblue;
}

h1 {
  color: white;
  text-align: center;
}

p {
  font-family: verdana;
  font-size: 20px;
}
```

**Breaking this down line by line:**

- `body { background-color: lightblue; }` — The `body` selector targets the entire webpage. This makes the whole page background light blue.
- `h1 { color: white; text-align: center; }` — Targets all `<h1>` (biggest heading) elements. Makes them white and centred.
- `p { font-family: verdana; font-size: 20px; }` — Targets all `<p>` (paragraph) elements. Sets their font to Verdana and their size to 20px.

**Expected Output:** A webpage with a light blue background, white centred headings, and paragraphs in Verdana at 20px.

---

## Section 4 — Understanding Each Part in Depth

### 4.1 — The Selector

The **selector** is the part of a CSS rule that says "which HTML element should this rule apply to?"

Think of it like the name tag at a job site. If you want all the painters to wear blue uniforms, you write a rule targeted at "painters". If you want all the electricians to wear yellow uniforms, you write a separate rule for "electricians".

The most basic type of selector is the **element selector** — it simply names the HTML tag you want to style.

**Simple element selectors:**

```css
/* Target all <h1> elements */
h1 {
  color: navy;
}

/* Target all <p> elements */
p {
  color: darkgray;
}

/* Target all <body> elements (the whole page) */
body {
  background-color: ivory;
}
```

> 📌 **Important:** In the CSS selector, you do NOT include the angle brackets (`<` and `>`). You write `p`, not `<p>`. You write `h1`, not `<h1>`.

**What happens with an element selector?**

When you write `h1 { color: blue; }`, CSS finds *every single* `<h1>` element in your entire HTML document and makes all of them blue. One rule, multiple elements — that is the power of CSS.

### 4.2 — The Property

The **property** is the name of the visual aspect you want to change.

CSS has hundreds of properties. Here are some of the most common ones you will use:

| Property | What it controls | Example value |
|----------|-----------------|---------------|
| `color` | Text colour | `red`, `blue`, `#ff0000` |
| `background-color` | Background colour | `lightblue`, `white` |
| `font-size` | How large the text is | `16px`, `2em` |
| `font-family` | Which font to use | `Arial`, `Georgia` |
| `text-align` | Left, centre, or right alignment | `center`, `left`, `right` |
| `border` | Line around an element | `1px solid black` |
| `margin` | Space *outside* an element | `20px`, `auto` |
| `padding` | Space *inside* an element | `10px` |
| `width` | How wide the element is | `300px`, `50%` |
| `height` | How tall the element is | `200px` |

Properties always go on the **left side** of the colon (`:`).

### 4.3 — The Value

The **value** tells CSS exactly how to apply the property. It always goes on the **right side** of the colon (`:`).

Different properties accept different types of values:

- **Colour values:** `red`, `blue`, `lightblue`, `#ff0000`, `rgb(255, 0, 0)`
- **Size values:** `20px`, `1.5em`, `50%`, `2rem`
- **Text values:** `center`, `left`, `bold`, `italic`
- **Font values:** `Arial`, `Georgia`, `sans-serif`

**Example — showing different value types:**

```css
h2 {
  color: navy;           /* colour keyword */
  font-size: 24px;       /* pixel size */
  text-align: center;    /* alignment keyword */
  font-family: Arial;    /* font name */
}
```

**Expected Output:** All `<h2>` headings appear navy blue, 24px tall, centred, in the Arial font.

### 4.4 — Curly Braces `{ }`

The curly braces `{` and `}` are like a container or a box. Everything you put inside them belongs to the selector above them.

- `{` opens the container
- `}` closes the container

**Never forget to close your curly brace!** A missing `}` is one of the most common CSS mistakes and can break every rule below it.

### 4.5 — The Colon `:`

The colon separates the **property name** from its **value**. There must always be a colon between them.

```css
/* Correct */
color: red;

/* Wrong - no colon */
color red;

/* Wrong - semicolon instead of colon */
color; red;
```

### 4.6 — The Semicolon `;`

The semicolon marks the end of each declaration. It acts like a full stop in a sentence. Without it, CSS does not know where one declaration ends and the next one begins.

```css
p {
  color: red;       /* ← semicolon here */
  font-size: 18px;  /* ← semicolon here */
  text-align: left; /* ← semicolon here (good habit, even on the last line) */
}
```

> 💡 **Best Practice:** Always put a semicolon after every declaration, including the last one. It is technically optional on the last one, but if you always do it, you will never accidentally introduce a bug when you add another line later.

---

## Section 5 — Simple Standalone Examples

Let us look at several complete, working examples from the very simplest to slightly more complex.

### Example 1 — Styling a Heading (Most Basic Possible)

**CSS:**

```css
h1 {
  color: blue;
}
```

**HTML:**

```html
<h1>Hello, World!</h1>
```

**Expected Output:** The text "Hello, World!" appears in blue.

**What happened?**
- Selector: `h1` — targets the `<h1>` element
- Property: `color` — controls the text colour
- Value: `blue` — makes it blue

---

### Example 2 — Changing the Background

**CSS:**

```css
body {
  background-color: lightyellow;
}
```

**HTML:**

```html
<body>
  <p>This page has a light yellow background.</p>
</body>
```

**Expected Output:** The entire webpage background becomes light yellow.

**What happened?**
- `body` is the selector — it targets the `<body>` tag which wraps the entire page
- `background-color` is the property — controls the background
- `lightyellow` is the value — a pale yellow colour

---

### Example 3 — Styling a Paragraph

**CSS:**

```css
p {
  font-size: 20px;
  color: darkgreen;
  text-align: center;
}
```

**HTML:**

```html
<p>This paragraph is styled with CSS.</p>
```

**Expected Output:** The paragraph text appears dark green, 20 pixels tall, and centred.

**Line-by-line explanation:**
- `font-size: 20px;` — makes the text 20 pixels high. `px` stands for "pixels" — tiny dots on your screen.
- `color: darkgreen;` — sets the text colour to dark green
- `text-align: center;` — centres the text horizontally within the page

---

### Example 4 — Multiple Rules for Multiple Elements

**CSS:**

```css
body {
  background-color: lightblue;
}

h1 {
  color: white;
  text-align: center;
}

p {
  font-family: verdana;
  font-size: 20px;
}
```

**HTML:**

```html
<body>
  <h1>My Website</h1>
  <p>Welcome to my page. This text is in Verdana font.</p>
</body>
```

**Expected Output:**
- The whole page background is light blue
- The heading "My Website" is white and centred
- The paragraph uses Verdana font at 20px

> 💡 **Thinking Prompt:** Can you predict what would happen if you added `color: navy;` as a new declaration inside the `p { }` rule? The paragraph text would appear navy blue.

---

## Section 6 — Guided Practice Exercises

These exercises will help you build confidence by writing real CSS rules.

---

### Exercise 1 — Warm-Up: Your First CSS Rule

**Objective:** Write a CSS rule that makes all `<h1>` headings appear in the colour `coral`.

**Scenario:** You are building a webpage for a surf shop. The owner wants the main heading to stand out in a vibrant colour.

**Steps:**

1. Identify the selector. Which HTML element are we targeting? → `h1`
2. Identify the property. What aspect are we changing? → `color`
3. Identify the value. What colour do we want? → `coral`
4. Write the rule using correct CSS syntax.

**Your Answer Should Look Like:**

```css
h1 {
  color: coral;
}
```

**Expected Output:** All `<h1>` elements on the page appear in the colour coral (a warm pinkish-orange).

**Self-Check Questions:**
- Did you use curly braces `{ }`?
- Did you use a colon `:` between the property and value?
- Did you end the declaration with a semicolon `;`?

---

### Exercise 2 — Multiple Declarations

**Objective:** Style a paragraph so it uses the Georgia font, has a font size of 18px, and dark gray text colour.

**Scenario:** You are designing a blog post page. The reading text needs to be elegant and easy to read.

**Steps:**

1. Selector → `p`
2. You need three declarations:
   - Font family → `font-family: Georgia;`
   - Font size → `font-size: 18px;`
   - Text colour → `color: darkgray;`

**Your Answer Should Look Like:**

```css
p {
  font-family: Georgia;
  font-size: 18px;
  color: darkgray;
}
```

**Expected Output:** All paragraphs use the Georgia font, are 18 pixels tall, and appear in dark gray.

**Self-Check Questions:**
- Does each declaration end with a semicolon?
- Is the entire block wrapped in curly braces?

---

### Exercise 3 — Page Background and Heading Together

**Objective:** Create two CSS rules: one that gives the whole page a `lightgray` background, and one that makes `<h2>` headings appear `darkblue` and centred.

**Scenario:** You are creating a simple company profile page and want a clean, professional look.

**Steps:**

1. Write a rule for `body` → `background-color: lightgray;`
2. Write a second rule for `h2` → `color: darkblue;` and `text-align: center;`

**Your Answer Should Look Like:**

```css
body {
  background-color: lightgray;
}

h2 {
  color: darkblue;
  text-align: center;
}
```

**Expected Output:** The whole page has a light gray background. All `<h2>` headings are dark blue and centred.

**What-If Challenge:** What would happen if you changed `text-align: center;` to `text-align: right;`? The headings would shift to the right side of the page.

---

### Exercise 4 — Build a Full Simple Stylesheet

**Objective:** Write a complete stylesheet with rules for `body`, `h1`, `h2`, and `p`.

**Scenario:** You are building a simple recipe page. Use this specification:

- Page background: `#fff5e6` (a warm cream colour)
- `h1`: colour `saddlebrown`, centred
- `h2`: colour `sienna`, font size `22px`
- `p`: font family `Arial`, font size `16px`, colour `#333`

**Your Answer Should Look Like:**

```css
body {
  background-color: #fff5e6;
}

h1 {
  color: saddlebrown;
  text-align: center;
}

h2 {
  color: sienna;
  font-size: 22px;
}

p {
  font-family: Arial;
  font-size: 16px;
  color: #333;
}
```

**Expected Output:** A warm cream-coloured page with brown headings and dark gray body text — perfect for a recipe page.

> 📌 **Note about `#333`:** This is a colour written in **hexadecimal format** — a way of describing colours using numbers and letters. `#333` is a very dark gray. You do not need to fully understand hex colours yet — just know they are another valid way to specify a colour in CSS.

---

## Section 7 — Common Beginner Mistakes (and How to Fix Them)

These are the mistakes that almost every beginner makes at least once. Knowing them in advance will save you a lot of frustration.

---

### Mistake 1 — Missing Curly Braces

**Wrong:**

```css
p
  color: red;
  font-size: 18px;
```

**Problem:** There are no curly braces `{ }`. CSS cannot tell where the declarations belong.

**Correct:**

```css
p {
  color: red;
  font-size: 18px;
}
```

---

### Mistake 2 — Missing Colon

**Wrong:**

```css
p {
  color red;
}
```

**Problem:** There is no colon `:` between the property (`color`) and the value (`red`). CSS cannot understand this.

**Correct:**

```css
p {
  color: red;
}
```

---

### Mistake 3 — Missing Semicolons Between Declarations

**Wrong:**

```css
p {
  color: red
  font-size: 18px
}
```

**Problem:** There are no semicolons after each declaration. CSS might misread these as one broken declaration.

**Correct:**

```css
p {
  color: red;
  font-size: 18px;
}
```

---

### Mistake 4 — Writing the Selector as an HTML Tag

**Wrong:**

```css
<p> {
  color: blue;
}
```

**Problem:** CSS selectors do NOT use angle brackets. Those are only for HTML.

**Correct:**

```css
p {
  color: blue;
}
```

---

### Mistake 5 — Confusing the Colon and Semicolon

**Wrong:**

```css
p {
  color; red:
}
```

**Problem:** The colon and semicolon are swapped. Colon always goes *between* property and value. Semicolon always goes *at the end* of a declaration.

**Correct:**

```css
p {
  color: red;
}
```

---

### Mistake 6 — Forgetting to Close the Curly Brace

**Wrong:**

```css
h1 {
  color: navy;

p {
  font-size: 16px;
}
```

**Problem:** The `h1` rule is never closed. CSS gets confused about where `h1`'s declarations end and where `p`'s begin. This can break *everything* below the missing brace.

**Correct:**

```css
h1 {
  color: navy;
}

p {
  font-size: 16px;
}
```

---

### Mistake 7 — Misspelling a Property or Value

**Wrong:**

```css
p {
  colour: red;       /* British spelling — not valid in CSS */
  tekst-align: center; /* typo in property name */
}
```

**Problem:** CSS uses American English. `colour` is wrong; it must be `color`. And `tekst-align` is a typo; it must be `text-align`.

**Correct:**

```css
p {
  color: red;
  text-align: center;
}
```

> 💡 **Tip:** CSS silently ignores rules it cannot understand. If a style is not working, check for spelling mistakes first!

---

## Section 8 — Mini Project: Style a Personal Profile Page

Let us put everything together in a small but complete project. You will write a full CSS stylesheet for a simple personal profile webpage.

### Project Brief

You are building a simple personal profile page for someone named "Amara Johnson". The page already has HTML written. Your job is to write all the CSS.

### Stage 1 — The HTML (Already Written for You)

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Amara's Profile</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <h1>Amara Johnson</h1>
    <h2>Web Developer & Designer</h2>
    <p>Hello! I am a passionate web developer based in Lagos. I love building
    clean, user-friendly websites that make a difference.</p>
    <h2>My Skills</h2>
    <p>HTML, CSS, JavaScript, Python, UI Design</p>
    <h2>Contact</h2>
    <p>Email: amara@example.com</p>
  </body>
</html>
```

### Stage 2 — Setup: Plan Before You Code

Before writing CSS, plan what you want:

- The page should have a clean white background
- The main name (`h1`) should be large, dark, and centred
- The sub-headings (`h2`) should be a medium purple colour
- The paragraphs should be a readable dark gray with a nice font
- A comfortable font size throughout

### Stage 3 — Core CSS (Write Your Stylesheet)

Create a file called `style.css` and write the following:

```css
/* === Page Base === */
body {
  background-color: #ffffff;
  font-family: Arial, sans-serif;
  margin: 40px;
}

/* === Main Name === */
h1 {
  color: #1a1a2e;
  font-size: 36px;
  text-align: center;
}

/* === Sub-Headings === */
h2 {
  color: #6a0dad;
  font-size: 22px;
}

/* === Body Text === */
p {
  color: #444444;
  font-size: 16px;
}
```

**Milestone Output — What the Page Should Look Like:**

- White background
- "Amara Johnson" appears large (36px), very dark navy (`#1a1a2e`), and centred
- "Web Developer & Designer", "My Skills", and "Contact" appear in purple (`#6a0dad`) at 22px
- All paragraph text appears dark gray (`#444444`) at 16px
- The whole page uses Arial font

### Stage 4 — Enhancements (Optional Extra Styling)

Try adding these extra styles to make the page even better:

```css
/* Make the whole content area centred and limited in width */
body {
  background-color: #f4f4f4;
  font-family: Arial, sans-serif;
  max-width: 700px;
  margin: 40px auto;
  padding: 30px;
  background-color: #ffffff;
}

/* Add a subtle underline styling to sub-headings */
h2 {
  color: #6a0dad;
  font-size: 22px;
  border-bottom: 2px solid #6a0dad;
  padding-bottom: 4px;
}
```

> 📌 **New properties introduced here:**
> - `max-width: 700px;` — limits the content area to 700px wide so it does not stretch too wide on large screens
> - `margin: 40px auto;` — `auto` on left and right margins automatically centres the element on the page
> - `padding: 30px;` — adds 30px of breathing space *inside* the body box
> - `border-bottom: 2px solid #6a0dad;` — draws a 2-pixel solid purple line under each `h2`
> - `padding-bottom: 4px;` — adds a small gap between the text and the underline

### Reflection Questions

After completing the mini-project, ask yourself:

1. What is the difference between `color` and `background-color`?
2. Why do we write `body { }` to style the entire page, and not `html { }`?
3. If you wanted all three headings (`h1`, `h2`, and `h3`) to be the same purple colour, how many CSS rules would you need?
4. What would happen if you deleted the `font-family: Arial, sans-serif;` from the body rule?

---

## Section 9 — Real-World Use Cases

Understanding CSS is not just academic — it is directly used in:

- **Web development jobs:** Every frontend developer writes CSS daily
- **Marketing and branding:** Companies use CSS to ensure their brand colours, fonts, and layouts appear consistently across their website
- **Journalism and publishing:** News sites like BBC or CNN use CSS to make articles readable and attractive
- **E-commerce:** Online stores like Amazon use CSS to highlight prices, buttons, and product layouts
- **Mobile apps:** Many mobile apps are built with web technologies that include CSS
- **Data dashboards:** Scientists and data analysts who build web-based data visualisation tools use CSS to style charts and reports

Even if you never become a professional developer, understanding CSS helps you communicate with designers and developers, customise website templates, and troubleshoot why something looks wrong on your screen.

---

## Section 10 — Reflection Questions

Test your understanding by answering these questions:

1. What does CSS stand for? What does each word mean?
2. Why was CSS created? What problem does it solve?
3. In the rule `h1 { color: blue; }`, what are the selector, the property, and the value?
4. What is the difference between a CSS *property* and a CSS *value*?
5. What is the purpose of the curly braces `{ }` in a CSS rule?
6. What is the purpose of the colon `:` inside a CSS declaration?
7. What is the purpose of the semicolon `;` at the end of a CSS declaration?
8. You write `<p> { color: red; }` but nothing happens. What is the mistake?
9. If you have a website with 200 pages and you want to change the font of all body text, how many files would you need to edit if you were using an external CSS file?
10. Write a CSS rule from memory that makes all `<h3>` elements appear in the colour `tomato` with a font size of `28px` and centred alignment.

---

## Completion Checklist

Before moving to Lesson 02, make sure you can honestly tick every item:

- [ ] I can explain what CSS is in simple language
- [ ] I understand why CSS was created and what problem it solves
- [ ] I know what CSS stands for and what each word means
- [ ] I can identify the selector, property, and value in any CSS rule
- [ ] I know what a declaration block is
- [ ] I know what a declaration is
- [ ] I understand the role of `{ }`, `:`, and `;` in CSS
- [ ] I can write a CSS rule from memory without looking
- [ ] I can write multiple declarations in one CSS rule
- [ ] I can write multiple CSS rules for different elements
- [ ] I know at least 5 common CSS properties and what they do
- [ ] I can recognise and fix the 7 common CSS mistakes listed in this lesson
- [ ] I have completed all 4 guided exercises
- [ ] I have completed the mini-project CSS stylesheet for Amara's profile page

---

## Lesson Summary

Here is everything this lesson covered, summarised for quick reference:

**What is CSS?**
CSS stands for Cascading Style Sheets. It is the language used to control the visual appearance of HTML elements — colours, fonts, sizes, layout, and more.

**Why does CSS exist?**
CSS separates content (HTML) from design. One CSS file can control the appearance of an entire website, making it much easier to update and maintain.

**The structure of a CSS rule:**

```css
selector {
  property: value;
  property: value;
}
```

**Key vocabulary:**
- **Rule (rule set):** The complete `selector { declarations }` block
- **Selector:** Points to the HTML element to style
- **Declaration block:** Everything inside `{ }`
- **Declaration:** One `property: value;` line
- **Property:** What aspect to style (colour, size, font, etc.)
- **Value:** How to style it (red, 20px, Arial, etc.)

**Key punctuation:**
- `{ }` — wraps the declaration block
- `:` — separates property from value
- `;` — ends each declaration

**Always remember:**
- CSS selectors do NOT use angle brackets (`<` `>`)
- Always close your curly braces
- Always use colons between property and value
- Always use semicolons after each declaration
- CSS uses American English spelling (e.g., `color` not `colour`)

---

*End of Lesson 01 — You are now ready to move on to Lesson 02: CSS Selectors*
