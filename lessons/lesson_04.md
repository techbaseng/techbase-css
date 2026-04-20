---
render_with_liquid: false
title: "CSS Comments and CSS Errors"
nav_order: 4
---

# Lesson 04 — CSS Comments and CSS Errors

---

## Lesson Introduction

Welcome to Lesson 04! In this lesson, you will learn two very important professional skills that every CSS developer uses every single day:

1. **CSS Comments** — How to write notes inside your CSS code that the browser completely ignores, but that make your work much easier to understand and manage.
2. **CSS Errors** — How CSS behaves when something goes wrong, why your styles sometimes silently "disappear," and how to find and fix common mistakes before they ruin your whole page.

These two topics work together perfectly. Once you understand how to write and read CSS clearly (comments), and once you understand how CSS handles mistakes (errors), you will be a much more confident and capable developer.

By the end of this lesson you will be able to:
- Write single-line and multi-line comments in CSS
- Use comments to explain your code and temporarily disable styles
- Understand how CSS silently skips broken rules
- Identify the three most common CSS error types
- Use browser DevTools to find and fix CSS mistakes
- Build a well-commented, error-free style sheet for a mini project

---

## Prerequisite Concepts

Before we go further, let's make sure you are comfortable with a few foundational ideas. If you have done the earlier lessons, you already know most of this — but a quick refresher never hurts.

### What is CSS?

CSS stands for **Cascading Style Sheets**. It is the language you use to style an HTML page — setting colours, sizes, fonts, spacing, and layouts.

### What is a CSS Rule?

A CSS rule has three parts:
- A **selector** — which HTML element to style
- A **property** — what aspect to change (e.g. colour, size)
- A **value** — what to set it to

```css
/* This is the full structure of a CSS rule */
selector {
  property: value;
}
```

**Real example:**

```css
p {
  color: blue;
  font-size: 16px;
}
```

- `p` → targets all `<p>` (paragraph) elements
- `color: blue;` → makes the text blue
- `font-size: 16px;` → sets the text size to 16 pixels

**What the browser shows:**

> All paragraph text on the page turns blue and becomes 16 pixels tall.

---

## Part 1 — CSS Comments

---

### 1.1 What is a Comment?

A **comment** is a piece of text that you write inside your code **for yourself or other developers to read**. The browser sees comments but completely ignores them — they have zero effect on how the page looks or behaves.

Think of a comment like a sticky note on a piece of paper. If you hand someone a report with sticky notes on it, they can read the sticky notes, but the sticky notes are not part of the actual report. They are just helpful reminders and explanations.

**Why do comments exist?**

Because code can become very long and confusing. Imagine coming back to a CSS file you wrote six months ago. Without comments, you might not remember why you made certain choices. Comments solve this problem by letting you leave clear explanations right next to your code.

**Real-world analogy:**
When a doctor writes a prescription, they sometimes add notes like *"take with food"* or *"for allergy treatment"*. Those notes don't change the medicine — they just explain why the medicine is being used. CSS comments work exactly the same way.

---

### 1.2 CSS Comment Syntax

In CSS, a comment always starts with `/*` and ends with `*/`.

```
/* Your comment text goes here */
```

- `/*` = the **opening** of the comment (start ignoring this)
- `*/` = the **closing** of the comment (stop ignoring, back to real CSS)

> ⚠️ **Important:** CSS uses `/* ... */` for comments. This is different from HTML comments (`<!-- ... -->`) and JavaScript single-line comments (`//`). In CSS, `//` does NOT create a comment and will instead cause an error.

---

### 1.3 Single-Line Comments

A single-line comment fits on one line.

**Example 1 — A comment above a rule:**

```css
/* This styles all paragraph text */
p {
  color: navy;
  font-size: 18px;
}
```

**What the browser does:**
- Reads the comment → ignores it completely
- Reads `p { color: navy; font-size: 18px; }` → applies the styles

**Expected result:** All paragraphs have navy-blue text at 18 pixels. The comment has no visual effect.

---

**Example 2 — A comment at the end of a line:**

You can also put a comment at the end of a rule, on the same line as a property.

```css
h1 {
  color: red;        /* Main page heading colour */
  font-size: 32px;   /* Large and easy to read */
}
```

**Expected result:** The `h1` heading is red and 32 pixels. The comments are invisible to the browser.

---

> 💡 **Thinking Prompt:** What happens if you change `color: red;` to `color: green;` and leave the comment unchanged? The heading turns green — but the comment still says "Main page heading colour" (not "green"). This is why it's important to update your comments when you change your code!

---

### 1.4 Multi-Line Comments

A multi-line comment spans several lines. It still starts with `/*` and ends with `*/` — but the content in between can be as many lines as you want.

**Example 3 — Multi-line comment block:**

```css
/*
  ===========================
  TYPOGRAPHY STYLES
  ===========================
  These rules control all
  text appearance across the
  site, including headings
  and body paragraphs.
*/

h1 {
  font-family: Georgia, serif;
  font-size: 36px;
  color: #333333;
}

p {
  font-family: Arial, sans-serif;
  font-size: 16px;
  line-height: 1.6;
}
```

**Expected result:** The `h1` is styled with Georgia font, 36px, dark grey. Paragraphs use Arial, 16px, with comfortable line spacing. All comment text is completely invisible to the browser.

---

**Example 4 — Section dividers using multi-line comments:**

Professional developers often use comments to divide a large CSS file into labelled sections, like chapters in a book:

```css
/* ==============================
   SECTION 1: RESET / BASE STYLES
   ============================== */

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* ==============================
   SECTION 2: NAVIGATION BAR
   ============================== */

nav {
  background-color: #1a1a2e;
  padding: 15px 20px;
}

/* ==============================
   SECTION 3: MAIN CONTENT
   ============================== */

main {
  max-width: 960px;
  margin: 0 auto;
}
```

**Expected result:** The page gets three styled areas — a fully reset base, a dark navy navigation bar, and a centred main content area. All section labels are only visible in the source code, not on the webpage.

---

### 1.5 Using Comments to "Turn Off" CSS Temporarily

One of the most useful tricks in CSS development is **commenting out** a line of code. This means wrapping existing CSS in a comment so the browser skips it — without actually deleting it.

This is incredibly useful when:
- You are testing different style options
- You want to temporarily remove a rule to see how the page looks without it
- You are debugging (finding bugs) and want to isolate which rule is causing a problem

**Example 5 — Commenting out a background colour to test:**

```css
body {
  font-family: Arial, sans-serif;
  /* background-color: yellow; */
  color: #222222;
}
```

**What happens here:**
- `font-family` → applied ✅
- `background-color: yellow;` → **commented out, skipped** ❌
- `color: #222222;` → applied ✅

**Expected result:** The page background stays white (or the browser default). No yellow background appears because that line is inside a comment.

To bring the background back, you simply remove the `/*` and `*/`:

```css
body {
  font-family: Arial, sans-serif;
  background-color: yellow;  /* restored! */
  color: #222222;
}
```

**Expected result now:** The page background turns yellow.

---

**Example 6 — Commenting out an entire rule:**

```css
/* 
h2 {
  color: orange;
  text-transform: uppercase;
}
*/

h2 {
  color: steelblue;
}
```

**What happens here:**
- The entire first `h2` rule block (orange + uppercase) is commented out → skipped
- Only the second `h2` rule applies → `h2` text is steelblue

**Expected result:** All `h2` headings appear in steelblue. They are NOT orange and NOT uppercase.

> 💡 **Thinking Prompt:** Why is commenting out code better than deleting it while testing? Because if you delete it and the page looks wrong, you have to re-type the code from scratch. If you comment it out, you can easily restore it by just removing the `/*` and `*/`.

---

### 1.6 Where Can Comments Go?

Comments can be placed almost anywhere in a CSS file:

- Before a rule
- After a rule
- Inside a rule (between properties)
- At the very top of the file (as a file header)
- At the very end of the file

**Example 7 — Comment used as a file header:**

```css
/*
  style.css
  Author: Amara Okonkwo
  Project: Personal Portfolio Website
  Last Updated: April 2026
  Description: Main stylesheet for all pages.
*/

body {
  margin: 0;
  font-family: "Segoe UI", sans-serif;
}
```

**Expected result:** No visual change — but any developer who opens this file immediately knows who wrote it, what it is for, and when it was last updated. This is considered a professional best practice.

---

### 1.7 What CSS Comments Cannot Do

Here are some important limitations of CSS comments:

1. **Comments do NOT work inside property values.**

```css
/* WRONG - this breaks the rule */
p {
  color: /* why is this blue? */ blue;
}
```

> ⚠️ Do not put comments inside a property value. Keep them on their own line or after the semicolon.

2. **CSS comments cannot be nested.**

```css
/* WRONG - never put one comment inside another */
/* This is the outer comment /* inner comment */ */
```

> ⚠️ The inner `*/` will close the outer comment early, which can cause unexpected behaviour.

3. **CSS `//` is NOT a valid comment.** Unlike JavaScript or many other languages, two forward-slashes do not create a comment in CSS.

```css
// WRONG - this is not a CSS comment
p {
  color: red;  // also wrong
}
```

> ⚠️ Using `//` in CSS is a common beginner mistake. The browser will treat it as an error and skip the property.

---

## Part 2 — CSS Errors

---

### 2.1 Why CSS Errors Are Special

In many programming languages, an error stops the whole program from running. For example, if you make a typo in Python, the whole script crashes and nothing works at all.

**CSS is different. CSS errors are silent and forgiving.**

When CSS encounters something it does not understand or that is invalid, it does NOT crash the browser. It does NOT show an error message on screen. Instead, it simply **skips the broken rule or property** and moves on to the next one.

This is called **CSS error recovery** or **CSS fault tolerance**.

**Real-world analogy:**
Imagine you are reading a book and you reach a sentence that is printed in a language you don't understand. You don't throw the whole book away — you just skip that sentence and continue reading the next one. CSS does exactly this.

**Why this matters:**
- Your page may look wrong and you won't know why
- No red warning messages appear on screen
- You have to be your own detective and look for the problem yourself
- Understanding common error types makes you much faster at finding bugs

---

### 2.2 The Three Main Types of CSS Errors

There are three main categories of mistakes that cause CSS rules to be silently skipped:

---

#### Error Type 1 — Syntax Errors (Wrong Punctuation or Structure)

A **syntax error** means the CSS is not written in the correct format. CSS has very strict punctuation rules: you need colons (`:`) between properties and values, semicolons (`;`) at the end of each declaration, and curly braces (`{` `}`) around the declarations.

**Example of a syntax error — missing colon:**

```css
/* BROKEN - missing colon between property and value */
p {
  color red;   /* Should be: color: red; */
  font-size: 16px;
}
```

**What happens:**
- CSS sees `color red;` — it does not understand this (no `:`) → skips the entire property
- CSS sees `font-size: 16px;` — this is valid → applies it

**Expected result:** The paragraph text is NOT red (the colour was skipped). The font size IS 16px (that rule was fine).

---

**Example of a syntax error — missing semicolon:**

```css
/* BROKEN - missing semicolon after first property */
p {
  color: red          /* no semicolon here! */
  font-size: 16px;
}
```

**What happens:**
CSS tries to parse `color: red font-size: 16px;` as one single declaration. It cannot understand this and skips **both** properties.

**Expected result:** Neither the colour nor the font size is applied. Both rules are lost because of the missing `;`.

> ⚠️ **Key rule:** Always end every CSS declaration with a semicolon `;`. Missing semicolons are one of the most common beginner errors and they can silently break multiple properties at once.

---

**Example of a syntax error — missing closing brace:**

```css
/* BROKEN - missing closing } */
h1 {
  color: purple;
  font-size: 28px;

p {
  color: black;
}
```

**What happens:**
CSS thinks the `p` rule is somehow inside the `h1` rule. It gets confused and may skip both rules or produce unexpected results.

**Correct version:**

```css
h1 {
  color: purple;
  font-size: 28px;
}   /* <-- this closing brace was missing */

p {
  color: black;
}
```

---

#### Error Type 2 — Invalid Values

An **invalid value** means the property name is correct, but the value you gave it does not make sense for that property.

**Example — using a number where a colour is expected:**

```css
/* BROKEN - "big" is not a valid colour */
p {
  color: big;
  font-size: 16px;
}
```

**What happens:**
- `color: big;` → "big" is not a colour → this property is skipped
- `font-size: 16px;` → this is valid → applied

**Expected result:** The paragraph text uses the browser's default colour (usually black). The font size is 16px.

---

**Example — missing unit on a size value:**

```css
/* BROKEN - font-size needs a unit like px, em, or rem */
p {
  color: navy;
  font-size: 16;   /* needs to be 16px or 16em */
}
```

**What happens:**
- `color: navy;` → valid → applied
- `font-size: 16;` → invalid (no unit) → skipped

**Expected result:** The text is navy but uses the browser's default font size (not 16px).

> 💡 **Exception:** The value `0` (zero) does not need a unit. `margin: 0;` is perfectly valid. But `font-size: 16;` is invalid because 16 what? Pixels? Points? The browser needs to know.

---

**Example — using a wrong colour format:**

```css
/* BROKEN - hex colour should have # prefix */
body {
  background-color: FF5733;   /* missing the # */
}

/* CORRECT */
body {
  background-color: #FF5733;
}
```

**What happens with the broken version:**
`FF5733` without `#` is not a recognised colour name or valid value → the background colour property is skipped.

**Expected result (broken):** The body background remains the default white.
**Expected result (correct):** The body background becomes a warm orange-red colour.

---

#### Error Type 3 — Wrong Property Names (Typos)

A **wrong property name** means you misspelled the CSS property. CSS will not recognise the misspelled word and will silently skip it.

**Example — typo in property name:**

```css
/* BROKEN - "colour" is not valid CSS (it's "color") */
p {
  colour: red;        /* British English spelling — NOT valid in CSS */
  font-size: 18px;
}
```

**What happens:**
- `colour: red;` → "colour" is not a CSS property → skipped
- `font-size: 18px;` → valid → applied

**Expected result:** The paragraph text is NOT red. The font size IS 18px.

> ⚠️ CSS always uses American English spellings. The correct property is `color`, not `colour`. This is one of the most famous CSS gotchas for developers from the UK, Nigeria, Australia, and other countries that use British English spelling.

---

**More examples of common typos:**

| What you typed (WRONG) | What it should be (CORRECT) |
|---|---|
| `backround-color` | `background-color` |
| `font-wieght` | `font-weight` |
| `margn-top` | `margin-top` |
| `displya` | `display` |
| `colour` | `color` |
| `boarder` | `border` |

---

### 2.3 How CSS Handles Errors — The Cascade of Skipping

When CSS encounters an error in a rule block, it follows a predictable pattern:

1. **A single invalid property** → only that one property is skipped. Other properties in the same block still work.
2. **A syntax error that breaks the whole block** (like a missing `}`) → the entire block may be skipped, including all valid properties inside it.
3. **An error at the selector level** (like a completely unrecognised selector) → the entire rule block is skipped.

**Example showing property-level skipping:**

```css
div {
  background-color: lightblue;    /* valid ✅ */
  colour: white;                   /* invalid ✅ — skipped */
  padding: 20px;                   /* valid ✅ */
  font-size: 18;                   /* invalid — no unit, skipped */
  border: 1px solid grey;          /* valid ✅ */
}
```

**Expected result:**
- Background is lightblue ✅
- Text colour is NOT white (browser default used instead) ❌
- Padding is 20px ✅
- Font size is NOT 18px (browser default used instead) ❌
- Border is applied ✅

---

### 2.4 How to Find and Fix CSS Errors

Since CSS errors are silent, you need to actively search for them. Here are the three most important tools and methods:

---

#### Method 1 — Read Your Code Carefully

Before anything else, re-read your CSS slowly. Check for:
- Is there a `:` between every property and value?
- Is there a `;` at the end of every declaration?
- Does every opening `{` have a matching closing `}`?
- Is every property name spelled correctly?

---

#### Method 2 — Use Browser Developer Tools (DevTools)

Every modern browser (Chrome, Firefox, Edge) has built-in developer tools that let you inspect CSS in real time. This is the most powerful method available.

**How to open DevTools:**
- On Windows/Linux: Press `F12` or `Ctrl + Shift + I`
- On Mac: Press `Cmd + Option + I`
- Or right-click anywhere on the page and choose **Inspect**

**What you will see in DevTools:**

When you click on an HTML element in DevTools, it shows you all the CSS rules that apply to that element in the **Styles panel** on the right side.

If a CSS property has an error, DevTools shows it with a **strikethrough** (a line through the text) and usually a ⚠️ warning icon. This tells you: "This property was skipped."

**Visual example (what it looks like):**

```
p {
  color: red;           ← shown normally (applied)
  ~~colour: blue;~~     ← shown with strikethrough (skipped - invalid)
  font-size: 16px;      ← shown normally (applied)
}
```

This makes it very easy to find exactly which line is broken without guessing.

---

#### Method 3 — Use the W3C CSS Validator

The **W3C CSS Validator** is a free online tool that checks your CSS for errors and tells you exactly what is wrong and on which line.

You can use it at: `https://jigsaw.w3.org/css-validator/`

Simply paste your CSS code into the validator, click "Check," and it will give you a full list of errors with explanations. This is very useful for catching mistakes you may have missed by reading alone.

---

### 2.5 CSS Validation and Best Practices for Error Prevention

The best way to deal with CSS errors is to prevent them from happening in the first place. Here are habits every professional developer follows:

1. **Always write properties and values on separate lines** — it is much easier to spot a missing `;` when each declaration is on its own line.
2. **Use a code editor with syntax highlighting** — tools like Visual Studio Code colour different parts of CSS differently. An invalid property name will often appear in the wrong colour, which makes typos obvious.
3. **Validate your CSS regularly** using the W3C Validator, especially before publishing a project.
4. **Use CSS comments** to label sections — when something breaks, comments help you narrow down which section to check.
5. **Test in the browser often** — do not write 200 lines of CSS before checking it. Write a few rules, save, refresh, check. This way, if something breaks, you know it happened in the last few lines you wrote.

---

## Part 3 — Guided Practice Exercises

---

### Exercise 1 — Add Comments to Existing CSS

**Objective:** Practise writing single-line and multi-line comments.

**Scenario:** You have just been given this plain CSS file and asked to add comments to explain what each section does.

**Starting code (no comments yet):**

```css
* {
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, sans-serif;
  background-color: #f5f5f5;
  color: #333333;
}

h1 {
  font-size: 36px;
  color: #1a1a2e;
  text-align: center;
}

p {
  font-size: 16px;
  line-height: 1.8;
}

footer {
  background-color: #1a1a2e;
  color: white;
  text-align: center;
  padding: 20px;
}
```

**Your task:**
1. Add a file header comment at the top with a title, author, and description.
2. Add a single-line comment above each rule explaining what it does.
3. Wrap the `h1` rule in a multi-line comment block labelled "HEADING STYLES".
4. Comment out the `background-color` on the `body` rule to test the page without it.

**Expected result after your changes:** The browser still shows the same page (because comments have no effect). But the CSS file is now much more readable and the `background-color` on body is temporarily disabled.

---

**Hints:**
- File header: Use `/* ... */` spanning several lines
- Single-line comment: `/* explains this rule */`
- Multi-line section block: Use `/* ===== HEADING STYLES ===== */` above the `h1` rule
- To comment out `background-color: #f5f5f5;`, change it to `/* background-color: #f5f5f5; */`

---

**Self-check questions:**
- Are all your comments between `/*` and `*/`?
- Did you accidentally use `//` for any comment? (Remember: `//` is NOT valid in CSS)
- Does your page still look the same after adding comments?
- Is the body background gone now that it is commented out?

---

### Exercise 2 — Find and Fix the Errors

**Objective:** Practise identifying and correcting the three types of CSS errors.

**Scenario:** A classmate wrote this CSS but the page looks completely wrong. Find all the errors and fix them.

**Broken code:**

```css
/* Header Styles */
h1 {
  colour: #2c3e50;
  font-size 28px;
  text-align: center
}

/* Paragraph Styles */
p {
  color: navy
  font-size: 16;
  line-height: 1.6;
  margin-bottom: 12px;
}

/* Button Styles */
.button {
  backround-color: steelblue;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
  font-size: 14px;
```

**How many errors can you find? There are 7 total.**

**Steps:**
1. Read each property name carefully — any typos?
2. Check each line for missing colons `:`
3. Check each line for missing semicolons `;`
4. Check for missing closing braces `}`

**Expected result after fixing:** All styles apply correctly — the heading is dark blue and centred, paragraphs are navy with comfortable spacing, and the button is steelblue with white text and rounded corners.

---

**Answer (errors identified):**

| Line | Error Type | What was wrong | Fix |
|---|---|---|---|
| `colour:` | Wrong property name | British spelling | Change to `color:` |
| `font-size 28px;` | Syntax error | Missing colon | Change to `font-size: 28px;` |
| `text-align: center` | Syntax error | Missing semicolon | Add `;` → `text-align: center;` |
| `color: navy` | Syntax error | Missing semicolon | Add `;` → `color: navy;` |
| `font-size: 16;` | Invalid value | Missing unit | Change to `font-size: 16px;` |
| `backround-color:` | Wrong property name | Typo (missing 'g') | Change to `background-color:` |
| `.button { ... ` | Syntax error | Missing closing `}` | Add `}` at the end |

---

**Corrected code:**

```css
/* Header Styles */
h1 {
  color: #2c3e50;           /* fixed: colour → color */
  font-size: 28px;          /* fixed: added colon */
  text-align: center;       /* fixed: added semicolon */
}

/* Paragraph Styles */
p {
  color: navy;              /* fixed: added semicolon */
  font-size: 16px;          /* fixed: added px unit */
  line-height: 1.6;
  margin-bottom: 12px;
}

/* Button Styles */
.button {
  background-color: steelblue;  /* fixed: backround → background */
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
  font-size: 14px;
}                               /* fixed: added closing brace */
```

---

### Exercise 3 — Comment-Out Testing Practice

**Objective:** Use commenting to test different style options without losing your original code.

**Scenario:** You are designing a product card for a store. You want to test two colour options for the card background.

**Starting code:**

```css
.product-card {
  background-color: #ffffff;  /* Option A: clean white */
  border: 1px solid #dddddd;
  border-radius: 8px;
  padding: 20px;
  width: 280px;
}
```

**Your tasks:**
1. Comment out Option A (`background-color: #ffffff;`)
2. Add Option B: `background-color: #fef9e7;` (a warm cream/ivory colour) on the next line
3. Test Option B in your browser
4. Then try Option C: `background-color: #eaf4fb;` (a soft sky blue) by commenting out Option B and adding Option C
5. Keep all three options in the file as comments so you can easily switch between them

**Expected final CSS (all three options, two commented out):**

```css
.product-card {
  /* background-color: #ffffff; */   /* Option A: clean white */
  /* background-color: #fef9e7; */   /* Option B: warm cream */
  background-color: #eaf4fb;         /* Option C: soft sky blue (ACTIVE) */
  border: 1px solid #dddddd;
  border-radius: 8px;
  padding: 20px;
  width: 280px;
}
```

**Expected result:** The product card background is soft sky blue. The other two options are preserved in comments and can be activated at any time.

---

## Part 4 — Mini Project: Commented, Error-Free Profile Card

In this project, you will build a small, well-designed profile card using HTML and CSS. Your CSS must be:
- Fully commented with section headers
- Free of all syntax errors, invalid values, and typos
- Tested using browser DevTools

---

### Stage 1 — HTML Setup

Create a file called `profile.html` and paste this HTML:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Profile Card</title>
  <link rel="stylesheet" href="profile.css">
</head>
<body>

  <div class="card">
    <div class="card-header">
      <h1 class="card-name">Amara Osei</h1>
      <p class="card-title">Frontend Developer</p>
    </div>
    <div class="card-body">
      <p class="card-bio">
        Passionate about building clean, accessible, and beautiful websites.
        Based in Accra, Ghana. Open to freelance and collaboration opportunities.
      </p>
    </div>
    <div class="card-footer">
      <a class="card-link" href="#">GitHub</a>
      <a class="card-link" href="#">LinkedIn</a>
      <a class="card-link" href="#">Portfolio</a>
    </div>
  </div>

</body>
</html>
```

---

### Stage 2 — Core CSS with Comments

Create a file called `profile.css`. Write the following CSS, including every comment shown:

```css
/*
  ============================================
  profile.css
  Project: Developer Profile Card
  Description: Styles for a single profile
               card component.
  ============================================
*/


/* ==============================
   SECTION 1: PAGE BACKGROUND
   ============================== */

body {
  /* Centre the card on the page */
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;

  /* Soft neutral background */
  background-color: #eef2f7;

  /* Remove browser default spacing */
  margin: 0;
  padding: 0;

  font-family: Arial, sans-serif;
}


/* ==============================
   SECTION 2: CARD CONTAINER
   ============================== */

.card {
  background-color: #ffffff;    /* White card surface */
  border-radius: 12px;          /* Rounded corners */
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);  /* Soft shadow */
  width: 340px;
  overflow: hidden;             /* Clip content to card edges */
}


/* ==============================
   SECTION 3: CARD HEADER
   ============================== */

.card-header {
  background-color: #1a1a2e;   /* Dark navy header */
  color: white;
  padding: 30px 20px 20px 20px;
  text-align: center;
}

.card-name {
  font-size: 24px;
  margin-bottom: 6px;
}

.card-title {
  font-size: 14px;
  color: #a0aec0;   /* Muted grey subtitle */
  margin: 0;
}


/* ==============================
   SECTION 4: CARD BODY
   ============================== */

.card-body {
  padding: 20px;
}

.card-bio {
  font-size: 14px;
  line-height: 1.7;
  color: #555555;   /* Readable dark grey */
  margin: 0;
}


/* ==============================
   SECTION 5: CARD FOOTER / LINKS
   ============================== */

.card-footer {
  display: flex;
  justify-content: space-around;  /* Space links evenly */
  padding: 16px 20px;
  border-top: 1px solid #eeeeee;  /* Subtle divider line */
}

.card-link {
  color: #1a1a2e;        /* Match header colour */
  text-decoration: none; /* Remove default underline */
  font-size: 13px;
  font-weight: bold;
  padding: 6px 10px;
  border-radius: 4px;
  transition: background-color 0.2s;  /* Smooth hover effect */
}

.card-link:hover {
  background-color: #eef2f7;  /* Subtle highlight on hover */
}
```

---

### Stage 3 — Milestone Output

Open `profile.html` in your browser. You should see:

- A soft blue-grey page background
- A white card centred on the page with rounded corners and a subtle shadow
- A dark navy header with a name and grey subtitle
- A card body with a biography paragraph in dark grey
- Three navigation links at the bottom spaced evenly

The card should look clean, readable, and professional.

---

### Stage 4 — DevTools Check

1. Open your browser DevTools (`F12` or `Ctrl+Shift+I`)
2. Click the **Inspector/Elements** tab
3. Click on `.card-header` in the HTML panel
4. Look at the **Styles** panel on the right
5. Confirm that all properties are showing normally (no strikethrough text, no ⚠️ warnings)
6. If you see any strikethrough properties, that means there is an error on that line — fix it!

---

### Stage 5 — Enhancement Challenge (Optional)

Try adding these optional enhancements to practise what you have learned:

1. Add a comment-out test: comment out `box-shadow` on `.card` to see the card without a shadow. Then restore it.
2. Test two different header colours: comment out `background-color: #1a1a2e;` and try `background-color: #16213e;` (a slightly different navy) or `background-color: #0f3460;` (a deeper blue).
3. Add an `/* EXPERIMENTAL */` comment before any rule you are testing, so you can find all test code easily with `Ctrl+F`.

---

### Reflection Questions

After completing the project, think about these questions:

1. Open your `profile.css` file. Could another developer understand exactly what each section does just from reading the comments? If not, improve your comments.
2. What would happen if you accidentally deleted the closing `}` from `.card-header`? Try it — what breaks?
3. Open DevTools and deliberately introduce a typo: change `border-radius: 12px;` to `border-radus: 12px;`. Can you spot the strikethrough in DevTools?
4. What is the difference between a comment that explains *what* the code does and a comment that explains *why* a decision was made? Which type is more valuable?

---

## Common Beginner Mistakes

Here is a summary of the most frequent mistakes beginners make with CSS comments and errors, along with the fix for each one:

---

### Mistake 1 — Using `//` for CSS Comments

```css
/* WRONG */
p {
  color: red;  // this is not a CSS comment!
}

/* CORRECT */
p {
  color: red;  /* this is a CSS comment */
}
```

**Why this happens:** Many beginners come from JavaScript or other languages where `//` is a valid comment. In CSS, `//` is not recognised and will be treated as an invalid value or cause the property to be skipped.

---

### Mistake 2 — Forgetting to Close a Comment

```css
/* WRONG - comment never closed!
p {
  color: red;
}

h1 {
  font-size: 24px;
}
```

**What happens:** Everything after `/*` is treated as a comment until the browser finds `*/`. If you forget `*/`, the browser ignores everything from that point to the end of the file.

**Fix:** Always type `/*` and `*/` at the same time before writing your comment text:

```css
/* YOUR COMMENT HERE */
```

---

### Mistake 3 — Trying to Nest Comments

```css
/* WRONG */
/* This is a comment /* with a nested comment */ end of comment */
```

**What happens:** The first `*/` at the end of the inner comment is treated as the end of the whole outer comment. The text `end of comment */` is then read as actual CSS and will cause an error.

**Fix:** CSS comments cannot be nested. Use separate comments instead:

```css
/* This is a comment */
/* with a separate additional note */
```

---

### Mistake 4 — British English Spelling

```css
/* WRONG */
p {
  colour: red;      /* Should be: color */
  grey is invalid? No — but... */
}

/* CORRECT */
p {
  color: red;
}
```

Note: `grey` as a colour name **IS** valid in CSS (both `grey` and `gray` are accepted colour names). But `colour` as a property name is NOT valid. CSS uses `color` (American English) for the property name.

---

### Mistake 5 — Missing Units on Size Values

```css
/* WRONG */
p {
  font-size: 18;     /* browser will skip this */
  margin-top: 10;    /* browser will skip this */
}

/* CORRECT */
p {
  font-size: 18px;
  margin-top: 10px;
}
```

**Exception:** `0` (zero) never needs a unit. `margin: 0;` is perfectly valid.

---

### Mistake 6 — Missing Semicolons Breaking the Next Property

```css
/* WRONG - missing semicolon after color */
p {
  color: red
  font-size: 16px;
}
```

**What happens:** CSS tries to read `color: red font-size: 16px` as one declaration. It fails. Both properties are skipped.

**Fix:** Add the semicolon:

```css
/* CORRECT */
p {
  color: red;
  font-size: 16px;
}
```

---

## Completion Checklist

Before you finish this lesson, confirm you can do everything on this list:

- [ ] I can write a single-line CSS comment using `/* comment */`
- [ ] I can write a multi-line CSS comment spanning several lines
- [ ] I understand that CSS comments are invisible to the browser
- [ ] I know how to comment out a CSS property to temporarily disable it
- [ ] I know that `//` is NOT a valid CSS comment
- [ ] I can explain what "CSS error recovery" means (CSS silently skips broken rules)
- [ ] I can identify a syntax error (missing `:`, `;`, or `}`)
- [ ] I can identify an invalid value error (wrong type or missing unit)
- [ ] I can identify a wrong property name error (typo)
- [ ] I know how to use browser DevTools to find strikethrough (skipped) CSS properties
- [ ] I know about the W3C CSS Validator as a tool for finding errors
- [ ] I completed the profile card mini project with full comments
- [ ] I successfully opened DevTools and confirmed no CSS errors in my project

---

## Real-World Connections

**Professional software teams** rely on comments heavily because many developers work on the same CSS file. Without comments, it is nearly impossible for a new team member to understand why certain style choices were made.

**Front-end developers** use the "comment out to test" technique every single day. When a client reports a visual bug, the first step is usually to comment out rules one by one to identify which one is causing the problem.

**CSS validators** are used in automated deployment pipelines (systems that automatically publish websites). Before code goes live, the validator checks for errors and blocks the deployment if any are found.

**Browser DevTools** are used during every professional design and development session. Learning to read the Styles panel in DevTools will make you significantly faster at fixing styling problems.

---

## Lesson Summary

In this lesson, you learned two foundational CSS skills that professional developers use every single day.

**CSS Comments:**
- Comments are written between `/*` and `*/`
- They are completely invisible to the browser
- They help explain code to yourself and other developers
- You can use single-line comments, multi-line comments, and section dividers
- Commenting out code lets you temporarily disable a rule without deleting it
- Never use `//` in CSS — it is invalid
- Never nest one comment inside another

**CSS Errors:**
- CSS errors are **silent** — no red warnings appear on screen
- When CSS sees an invalid property or value, it **skips** that rule and continues
- The three main error types are: syntax errors (wrong punctuation), invalid values (wrong type or missing unit), and wrong property names (typos)
- Use **browser DevTools** to see which properties are being skipped (shown with strikethrough)
- Use the **W3C CSS Validator** to find and list all errors in your CSS
- Prevent errors by: writing one declaration per line, using a code editor with syntax highlighting, validating regularly, and testing in the browser often

Together, these two skills — writing clear, commented CSS and understanding how to find and fix errors — form the foundation of professional, maintainable CSS development.

---

*End of Lesson 04 — CSS Comments and CSS Errors*
