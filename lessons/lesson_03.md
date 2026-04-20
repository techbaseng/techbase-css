---
render_with_liquid: false
title: "How to Add CSS to HTML — External, Internal, Inline & the Cascade"
nav_order: 3
---

# Lesson 03 — How to Add CSS to HTML

## External CSS · Internal CSS · Inline CSS · Multiple Style Sheets · The Cascading Order

---

## Lesson Introduction

Welcome to Lesson 03!

In the previous lessons you learned **what CSS is** and **how CSS rules are written**. Now comes the most practical question of all:

> **"I have written some CSS — but where exactly do I put it so the browser can find it and use it?"**

That is exactly what this lesson answers. There are **three different places** you can write CSS:

1. In a **separate file** (called External CSS)
2. **Inside the `<head>` section** of your HTML page (called Internal CSS)
3. **Directly on a single HTML tag** (called Inline CSS)

Each one has a purpose, strengths, and weaknesses. You will learn all three, see real working code for each, and by the end of this lesson you will also understand the **Cascading Order** — the rule that settles what happens when two or more style instructions fight over the same HTML element.

This lesson follows the exact content from the W3Schools CSS How-To series and expands every topic into a deeply beginner-friendly explanation.

---

## What You Need to Know Before Starting

> **Prerequisite Check** — If any of these terms are unfamiliar, read the short explanations below before continuing.

### What is HTML?

HTML (HyperText Markup Language) is the language used to write the **structure** of a web page. It uses **tags** (words inside angle brackets) to describe content. For example:

```html
<h1>This is a big heading</h1>
<p>This is a paragraph of text.</p>
```

The browser reads these tags and knows: "show a big bold heading, then show a paragraph."

### What is CSS?

CSS (Cascading Style Sheets) is the language used to **style** HTML content — meaning it controls colour, font, size, spacing, layout, and much more.

A CSS rule looks like this:

```css
h1 {
  color: blue;
  font-size: 36px;
}
```

- `h1` is the **selector** — it tells CSS which HTML element to target.
- `color: blue;` and `font-size: 36px;` are **declarations** — they say what to change and what value to use.

### What is the `<head>` section?

Every HTML page has two main sections:

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- Information ABOUT the page goes here (not visible on screen) -->
  </head>
  <body>
    <!-- The actual page content goes here (this IS visible) -->
  </body>
</html>
```

The `<head>` section is invisible to the user but very important — it is where you link external files (like CSS files) and write internal styles.

### What is a `.css` file?

A `.css` file is a plain text file that contains only CSS code — no HTML, no paragraphs, just CSS rules. You create it using any text editor (Notepad, VS Code, etc.) and save it with the `.css` extension (e.g. `mystyle.css`).

---

## Section 1 — The Three Ways to Add CSS

When a browser reads a style sheet, it formats the HTML document according to the information in that style sheet. There are three ways to insert a style sheet:

1. **External CSS** — store styles in a separate `.css` file
2. **Internal CSS** — write styles inside a `<style>` block in the HTML `<head>`
3. **Inline CSS** — write styles directly on individual HTML elements using the `style` attribute

Let's explore each one in depth.

---

## Section 2 — External CSS

### What Is It and Why Does It Exist?

Imagine you are building a website with 50 pages. Every page should have the same colours, fonts, and spacing. If you wrote your CSS inside every page separately, you would have to update 50 files every time you wanted to change the background colour. That would be an enormous amount of work!

**External CSS** solves this problem. You write all your styles once in a single `.css` file, and then every HTML page simply **links** to that file. Want to change the background colour across all 50 pages? Edit one file. Done.

> **Analogy:** Think of an external CSS file like a company style guide that all departments follow. Every team member refers to the same document instead of inventing their own rules.

### How It Works — Step by Step

**Step 1:** Create your HTML file (e.g. `index.html`).

**Step 2:** Create a separate text file with a `.css` extension (e.g. `mystyle.css`).

**Step 3:** Inside your HTML file's `<head>` section, add a `<link>` tag that points to your `.css` file.

**Step 4:** The browser reads the HTML, sees the `<link>`, fetches the CSS file, and applies all the styles.

### The `<link>` Tag — Line by Line Explanation

```html
<link rel="stylesheet" href="mystyle.css">
```

| Part | What it means |
|------|---------------|
| `<link>` | An HTML tag used to connect an external resource to this page |
| `rel="stylesheet"` | Tells the browser what kind of relationship this link has — it is a stylesheet |
| `href="mystyle.css"` | The path/address of the CSS file (`href` = hyperlink reference) |

> **Important:** The `<link>` tag does not have a closing tag — it is a self-closing tag.

### Full Working Example — External CSS

**File 1: `index.html`**

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="mystyle.css">
</head>
<body>

  <h1>This is a heading</h1>
  <p>This is a paragraph.</p>

</body>
</html>
```

**File 2: `mystyle.css`** (saved separately in the same folder)

```css
body {
  background-color: lightblue;
}

h1 {
  color: navy;
  margin-left: 20px;
}
```

**What the browser renders:**

```
[Page background is light blue]
[Heading: "This is a heading" — displayed in navy blue, shifted 20px from the left]
[Paragraph: "This is a paragraph." — shown in default black text]
```

### Explaining Every Line of `mystyle.css`

```css
body {
  background-color: lightblue;
}
```

- `body` — targets the entire page body (everything visible on screen)
- `background-color: lightblue;` — sets the background of the whole page to light blue

```css
h1 {
  color: navy;
  margin-left: 20px;
}
```

- `h1` — targets all `<h1>` (main heading) elements
- `color: navy;` — sets the text colour to navy (a dark blue)
- `margin-left: 20px;` — adds 20 pixels of space to the left of the heading

> **Critical Rule — No spaces in values with units:**
>
> ✅ Correct: `margin-left: 20px;`
>
> ❌ Incorrect: `margin-left: 20 px;`
>
> Adding a space between the number and the unit (like `20 px` instead of `20px`) will break the rule — the browser will ignore it entirely. Always write the number and unit together with no space.

### Rules for the External `.css` File

- The file must be saved with the `.css` extension
- The file must contain **only CSS code** — no HTML tags, no `<style>` tags, nothing else
- The file can be placed in the same folder as your HTML files, or in a subfolder (e.g. `css/mystyle.css`)

### Why External CSS is the Professional Standard

In the real world — in software companies, web agencies, and open-source projects — external CSS is the standard approach. Here is why:

- **One change, site-wide effect** — update one file, every page updates
- **Clean separation** — HTML handles structure, CSS handles style
- **Team collaboration** — designers can work on `.css` files while developers work on `.html` files simultaneously
- **Faster loading** — browsers cache (store) external CSS files, so the file only downloads once even across many pages

---

## Section 3 — Internal CSS

### What Is It and Why Does It Exist?

Sometimes a single HTML page needs a completely unique style — different from every other page on the site. Maybe it is a special landing page, a unique error page, or a one-off report. In these cases, it can be convenient to write the CSS **directly inside the HTML file itself**, rather than creating a separate `.css` file.

**Internal CSS** allows you to place your style rules inside a `<style>` block within the `<head>` section of your HTML document.

> **Analogy:** If external CSS is a company-wide dress code, internal CSS is a note on a specific employee's desk saying "wear formal attire today only."

### Where to Place Internal CSS

The `<style>` element goes inside the `<head>` section of your HTML page:

```html
<!DOCTYPE html>
<html>
<head>

  <style>
    /* Your CSS rules go here */
  </style>

</head>
<body>
  <!-- Your HTML content goes here -->
</body>
</html>
```

> The text between `/*` and `*/` is a **CSS comment** — it is ignored by the browser and is just a note for you (the developer). Comments are very useful for explaining your own code.

### Full Working Example — Internal CSS

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      background-color: linen;
    }

    h1 {
      color: maroon;
      margin-left: 40px;
    }
  </style>
</head>
<body>

  <h1>This is a heading</h1>
  <p>This is a paragraph.</p>

</body>
</html>
```

**What the browser renders:**

```
[Page background is a warm linen/cream colour]
[Heading: "This is a heading" — displayed in dark maroon red, shifted 40px from left]
[Paragraph: "This is a paragraph." — shown in default black text]
```

### Explaining Every Part

```html
<style>
```
This tag **opens** the internal style block. Everything between `<style>` and `</style>` is CSS code.

```css
body {
  background-color: linen;
}
```
- `body` — targets the entire page
- `background-color: linen;` — sets the background to a soft, warm cream colour called "linen"

```css
h1 {
  color: maroon;
  margin-left: 40px;
}
```
- `h1` — targets all main headings
- `color: maroon;` — sets the text to dark red
- `margin-left: 40px;` — pushes the heading 40 pixels from the left edge

```html
</style>
```
This tag **closes** the internal style block.

### When to Use Internal CSS

**Good situations for internal CSS:**

- A single unique page that stands alone (e.g. a custom 404 error page)
- Quick testing and experimenting (it is faster to test without creating extra files)
- Email templates (some email clients block external stylesheets)

**When NOT to use internal CSS:**

- Multi-page websites (updating each page separately is tedious and error-prone)
- When the same styles apply to many pages (use external CSS instead)

### Internal CSS vs External CSS — Comparison

| Feature | External CSS | Internal CSS |
|---------|-------------|--------------|
| Location | Separate `.css` file | Inside `<head>` of HTML file |
| Applies to | Multiple pages | Only that one page |
| Best for | Full websites | Single unique pages |
| File count | 2+ files | 1 file |
| Maintenance | Very easy (one update) | Harder (each page separately) |

---

## Section 4 — Inline CSS

### What Is It and Why Does It Exist?

**Inline CSS** is the most targeted and specific of all three methods. Instead of writing a rule that targets an element type (like "all `<h1>` headings"), inline CSS applies a style **directly to one single HTML tag**.

You use the `style` attribute directly on the element you want to style.

> **Analogy:** If external CSS is a company dress code and internal CSS is a note for one department, inline CSS is a sticky note attached directly to one person saying "you specifically, wear a red tie today."

### How to Write Inline CSS

Add the `style` attribute inside the opening tag of any HTML element:

```html
<tagname style="property: value; property: value;">
```

- The value of the `style` attribute is CSS code
- Multiple CSS declarations are separated by semicolons `;`
- There are no curly braces `{}` — you are writing declarations directly
- Everything must be on one line (or very compact)

### Full Working Example — Inline CSS

```html
<!DOCTYPE html>
<html>
<body>

  <h1 style="color: blue; text-align: center;">This is a heading</h1>
  <p style="color: red;">This is a paragraph.</p>

</body>
</html>
```

**What the browser renders:**

```
[Heading: "This is a heading" — blue text, centred on the page]
[Paragraph: "This is a paragraph." — red text, left-aligned by default]
```

### Explaining Every Part — Line by Line

```html
<h1 style="color: blue; text-align: center;">This is a heading</h1>
```

| Part | Explanation |
|------|-------------|
| `<h1` | Opening tag for a main heading |
| `style="..."` | The style attribute — everything in quotes is CSS |
| `color: blue;` | Sets the text colour to blue |
| `text-align: center;` | Centres the heading text horizontally |
| `"This is a heading"` | The visible text that appears on screen |
| `</h1>` | Closing tag for the heading |

```html
<p style="color: red;">This is a paragraph.</p>
```

| Part | Explanation |
|------|-------------|
| `<p` | Opening tag for a paragraph |
| `style="color: red;"` | Makes the paragraph text red |
| `"This is a paragraph."` | The visible text |
| `</p>` | Closing tag for the paragraph |

### The Important Warning About Inline CSS

> **⚠️ Tip:** An inline style loses many of the advantages of a style sheet by mixing content with presentation. Use this method sparingly.

What does "mixing content with presentation" mean?

HTML should describe **what** the content is (a heading, a paragraph, a list). CSS should describe **how** it looks (blue, centred, large). Keeping these separate makes your code cleaner, easier to read, and much easier to maintain.

When you write inline CSS, you combine both responsibilities in one place. This quickly becomes very messy on large pages, makes maintenance difficult, and defeats the whole purpose of having a stylesheet.

**When inline CSS is acceptable:**

- Applying a unique one-off style to a single element with no equivalent needed elsewhere
- HTML emails (some clients strip `<style>` blocks but respect inline styles)
- JavaScript dynamically changing styles (a more advanced use case)
- Quick debugging to test if a style works on one element

---

## Section 5 — Multiple Style Sheets and What Happens When They Conflict

### The Problem: Two Rules for the Same Element

What happens when you have both an external CSS file AND internal CSS — and they both have a rule for the same HTML element?

For example:

Your **external file** (`mystyle.css`) says:
```css
h1 {
  color: navy;
}
```

Your **internal style block** says:
```css
h1 {
  color: orange;
}
```

Both files are loaded on the same page. Which colour wins? The answer depends on **the order in which the styles are loaded**.

### Rule: The Last Style Read Wins

CSS is read top to bottom. If two rules target the same element and set the same property, **the one that comes later in the reading order takes effect**.

### Example A — Internal Style Defined AFTER the External Link

```html
<head>
  <link rel="stylesheet" type="text/css" href="mystyle.css">
  <style>
    h1 {
      color: orange;
    }
  </style>
</head>
```

**Reading order:**
1. Browser reads `<link>` → loads `mystyle.css` → sees `color: navy`
2. Browser reads `<style>` → sees `color: orange`
3. `orange` was read **last**, so it wins

**Result:** The `<h1>` will be displayed in **orange**.

### Example B — Internal Style Defined BEFORE the External Link

```html
<head>
  <style>
    h1 {
      color: orange;
    }
  </style>
  <link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

**Reading order:**
1. Browser reads `<style>` → sees `color: orange`
2. Browser reads `<link>` → loads `mystyle.css` → sees `color: navy`
3. `navy` was read **last**, so it wins

**Result:** The `<h1>` will be displayed in **navy**.

> **Thinking prompt:** What would happen if the internal `<style>` block and the external file both set `color: orange`? (Answer: orange wins either way — both agree, so there is no conflict.)

---

## Section 6 — The Cascading Order (Priority Rules)

### What Does "Cascading" Actually Mean?

The "C" in CSS stands for **Cascading**. A cascade is like a waterfall — water flows from high to low, with higher sources taking priority. In CSS, "cascading" describes how styles from multiple sources are combined, and which source has priority when there is a conflict.

When a browser encounters an HTML element, it may find style instructions coming from several places at once. The cascading order determines which instruction wins.

### The Cascading Priority Order

All styles on a page are combined into one final "virtual" stylesheet using these priority rules (highest priority listed first):

| Priority | Source |
|----------|--------|
| 1 (HIGHEST) | Inline style (written directly on the HTML element) |
| 2 | Internal and external style sheets (in the head section) |
| 3 (LOWEST) | Browser default styles |

**Inline style always wins.** It overrides external stylesheets, internal stylesheets, and the browser's built-in default styles.

### What are Browser Default Styles?

Before you write a single line of CSS, your browser already has some built-in styles. For example:

- `<h1>` elements are displayed large and bold by default
- `<a>` links are underlined and blue by default
- `<p>` paragraphs have some default top and bottom spacing

These are **browser defaults** — they have the lowest priority and will be overridden by any CSS you write yourself.

### Visualising the Cascade

```
Browser Default Styles
        ↑ overridden by
External/Internal CSS Stylesheets
        ↑ overridden by
Inline CSS (style="...")
```

Think of it as three layers stacked on top of each other. Each higher layer paints over whatever the lower layer had.

### A Complete Worked Example

Let's trace exactly what happens when all three sources exist simultaneously.

```html
<!DOCTYPE html>
<html>
<head>
  <!-- External CSS file sets h1 to green -->
  <link rel="stylesheet" href="styles.css">

  <!-- Internal CSS sets h1 to orange (comes AFTER the link, so it overrides the external file) -->
  <style>
    h1 {
      color: orange;
    }
  </style>
</head>
<body>

  <!-- Inline CSS sets THIS specific h1 to purple -->
  <h1 style="color: purple;">What colour am I?</h1>

  <!-- This h1 has NO inline style, so it uses the last stylesheet rule: orange -->
  <h1>What colour am I?</h1>

</body>
</html>
```

**`styles.css` content:**
```css
h1 {
  color: green;
}
```

**Results:**

```
First <h1>:  "What colour am I?" → PURPLE  (inline style wins — highest priority)
Second <h1>: "What colour am I?" → ORANGE  (internal CSS wins over external because it was read last)
```

### Why the Cascade Matters in Real Projects

Understanding the cascade helps you:

- **Debug styling problems** — if a style is not applying, something higher in the cascade is overriding it
- **Write predictable code** — you can confidently predict which rule will win
- **Avoid unnecessary `!important`** — many beginners overuse `!important` (a CSS override keyword) because they do not understand the cascade; understanding it means you rarely need it
- **Organise stylesheets professionally** — you can intentionally layer styles: browser defaults → global styles → page-specific styles → element-specific inline tweaks

---

## Section 7 — Simple Standalone Examples

### Example 1 — External CSS (Simple Version)

**`hello.html`:**

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="hello.css">
</head>
<body>
  <h1>Hello World</h1>
  <p>CSS is styling this page from an external file.</p>
</body>
</html>
```

**`hello.css`:**

```css
body {
  background-color: lightyellow;
}

h1 {
  color: darkgreen;
}

p {
  color: grey;
}
```

**Expected Output:**

```
[Page background: pale yellow]
[Heading "Hello World": dark green text]
[Paragraph: grey text]
```

---

### Example 2 — Internal CSS (Simple Version)

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      background-color: lightpink;
    }
    h2 {
      color: darkblue;
      text-align: center;
    }
  </style>
</head>
<body>
  <h2>Welcome to My Page</h2>
  <p>This page uses internal CSS.</p>
</body>
</html>
```

**Expected Output:**

```
[Page background: light pink]
[Heading "Welcome to My Page": dark blue, centred]
[Paragraph: default black text]
```

---

### Example 3 — Inline CSS (Simple Version)

```html
<!DOCTYPE html>
<html>
<body>
  <p style="color: green; font-size: 20px;">This paragraph is green and large.</p>
  <p>This paragraph has no inline style — it is the default.</p>
</body>
</html>
```

**Expected Output:**

```
[First paragraph: green text, font size 20px]
[Second paragraph: default black text, default size]
```

---

### Example 4 — Cascade in Action

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      color: blue;
      font-size: 18px;
    }
  </style>
</head>
<body>
  <p>I am blue and 18px (from internal CSS).</p>
  <p style="color: red;">I am red and 18px (inline overrides colour, but not font-size).</p>
</body>
</html>
```

**Expected Output:**

```
[First paragraph: blue text, 18px]
[Second paragraph: red text, 18px]
```

> **Thinking prompt:** Why does the second paragraph still have `font-size: 18px` even though it uses inline CSS? Because inline CSS only specified `color: red;` — it did not override `font-size`. So `font-size: 18px` from the internal stylesheet still applies. The cascade merges rules; it does not erase unrelated ones.

---

## Section 8 — Common Beginner Mistakes

### Mistake 1 — Space Between Number and Unit

```css
/* ❌ WRONG */
margin-left: 20 px;

/* ✅ CORRECT */
margin-left: 20px;
```

A space between `20` and `px` breaks the CSS rule completely. The browser will ignore the declaration as if it was never written.

---

### Mistake 2 — Forgetting `rel="stylesheet"` in the `<link>` Tag

```html
<!-- ❌ WRONG — browser does not know this is a stylesheet -->
<link href="style.css">

<!-- ✅ CORRECT -->
<link rel="stylesheet" href="style.css">
```

Without `rel="stylesheet"`, the browser will still load the file but will not apply it as CSS styles.

---

### Mistake 3 — Writing HTML Tags Inside the `.css` File

```css
/* ❌ WRONG — HTML tags have no place in a CSS file */
<style>
body {
  background: red;
}
</style>

/* ✅ CORRECT — a CSS file contains ONLY CSS rules, no HTML tags */
body {
  background: red;
}
```

---

### Mistake 4 — Putting the `<style>` Block in the `<body>` Instead of `<head>`

```html
<!-- ❌ WRONG — style block belongs in <head>, not <body> -->
<body>
  <style>
    p { color: red; }
  </style>
  <p>Hello</p>
</body>

<!-- ✅ CORRECT -->
<head>
  <style>
    p { color: red; }
  </style>
</head>
<body>
  <p>Hello</p>
</body>
```

While browsers are forgiving and may still render it, placing `<style>` in `<body>` is invalid HTML and can cause unexpected behaviour.

---

### Mistake 5 — Using Curly Braces in Inline CSS

```html
<!-- ❌ WRONG — no curly braces in inline CSS -->
<p style="{color: red;}">Hello</p>

<!-- ✅ CORRECT — just the declarations, no braces -->
<p style="color: red;">Hello</p>
```

Inline CSS is written directly inside the `style` attribute as a list of property-value pairs separated by semicolons. There is no selector and no curly braces.

---

### Mistake 6 — Wrong Order in the `<head>` and Being Surprised by the Result

```html
<!-- This will result in the EXTERNAL file's colour winning (it is read last) -->
<head>
  <style>
    h1 { color: orange; }
  </style>
  <link rel="stylesheet" href="style.css"> <!-- style.css sets h1 to navy -->
</head>
```

If you expected orange but see navy, remember: the **last rule read wins**. Swap the order to fix it.

---

### Mistake 7 — Overusing Inline CSS

Writing inline CSS on every element defeats the entire purpose of stylesheets. If you find yourself doing this:

```html
<p style="color: blue; font-size: 16px; margin: 10px;">Paragraph 1</p>
<p style="color: blue; font-size: 16px; margin: 10px;">Paragraph 2</p>
<p style="color: blue; font-size: 16px; margin: 10px;">Paragraph 3</p>
```

Write an internal or external CSS rule instead:

```css
p {
  color: blue;
  font-size: 16px;
  margin: 10px;
}
```

Now all paragraphs share the same style with one clean rule. To change all of them, you only edit one place.

---

## Section 9 — Guided Practice Exercises

### Exercise 1 — Set Up Your First External CSS

**Objective:** Create two separate files — an HTML file and a CSS file — and link them together.

**Scenario:** You are building a simple "About Me" page for a friend. The page needs a coloured background, a styled heading, and some styled paragraph text.

**Steps:**

1. Create a new folder on your computer called `my-first-css`.
2. Inside the folder, create a file called `about.html`.
3. Inside the same folder, create a file called `style.css`.
4. Write the following in `about.html`:

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>About Me</h1>
  <p>My name is Alex. I am learning CSS.</p>
  <p>I enjoy coding, reading, and travelling.</p>
</body>
</html>
```

5. Write the following in `style.css`:

```css
body {
  background-color: lightyellow;
}

h1 {
  color: darkblue;
  margin-left: 15px;
}

p {
  color: #333333;
  margin-left: 15px;
}
```

6. Open `about.html` in a browser.

**Expected Output:**

```
[Page background: pale yellow]
[Heading "About Me": dark blue, 15px from left]
[Paragraphs: dark grey (#333333), 15px from left]
```

**Self-Check Questions:**
- Can you see the yellow background? If not, double-check that `style.css` is in the same folder as `about.html`.
- Is the heading dark blue? If not, check that the `<link>` tag is correct.
- What happens if you change `lightyellow` to `lightcoral` in the CSS file and refresh the browser?

**Optional "What-If" Challenge:**
- Add a third paragraph with the inline style `style="color: red;"`. Does the red inline colour override the `color: #333333` from the external stylesheet? Why?

---

### Exercise 2 — Use Internal CSS for a Unique Page

**Objective:** Style a page using only internal CSS inside a `<style>` block.

**Scenario:** You are creating a special "Thank You" confirmation page after a user submits a form. This page has its own unique look.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      background-color: #e8f5e9;
      font-family: Arial, sans-serif;
    }

    h1 {
      color: green;
      text-align: center;
    }

    p {
      color: #1b5e20;
      text-align: center;
      font-size: 18px;
    }
  </style>
</head>
<body>
  <h1>Thank You!</h1>
  <p>Your message has been received.</p>
  <p>We will get back to you within 24 hours.</p>
</body>
</html>
```

**Expected Output:**

```
[Page background: very light green]
[Heading "Thank You!": green, centred]
[Paragraphs: dark forest green, centred, 18px]
```

**Self-Check Questions:**
- What would happen if you added a `<link>` to an external CSS file that also sets `h1 { color: red; }` — and you placed the `<link>` AFTER your `<style>` block? What colour would the heading be?
- What if the `<link>` was placed BEFORE your `<style>` block?

---

### Exercise 3 — Practice the Cascade

**Objective:** Understand how conflicting styles resolve.

```html
<!DOCTYPE html>
<html>
<head>
  <!-- Simulating what an external file would contain by using internal CSS first -->
  <style>
    /* Rule A — imagine this came from an external file */
    h1 {
      color: navy;
      font-size: 30px;
    }
  </style>

  <!-- Rule B — internal CSS defined AFTER Rule A -->
  <style>
    h1 {
      color: orange;
    }
  </style>
</head>
<body>

  <!-- Rule C — inline CSS defined directly on the element -->
  <h1 style="color: purple;">What colour am I?</h1>

  <!-- No inline CSS — which stylesheet rule wins? -->
  <h1>What colour am I now?</h1>

</body>
</html>
```

**Before running this code, predict the answers:**

1. What colour will the first `<h1>` be?
2. What colour will the second `<h1>` be?
3. What font-size will both `<h1>` elements use?

**Expected Answers:**

1. **Purple** — inline CSS has the highest priority and overrides everything
2. **Orange** — the second `<style>` block was read after the first, so `orange` overrides `navy`
3. **30px** — only Rule A set a `font-size`. Rule B and inline only set `color`. So `30px` is never overridden and applies to both headings.

> **Thinking prompt:** Why does the first `<h1>` (with `color: purple;` inline) still use `font-size: 30px`? Because inline CSS specified ONLY `color`. It did not specify `font-size`. So `font-size: 30px` from the stylesheet still applies alongside the inline `color: purple`. The cascade combines non-conflicting rules.

---

## Section 10 — Mini Project: Build a Simple Styled Web Page

### Project Description

You will build a simple two-page mini website for an imaginary coffee shop called "Morning Brew." The project uses all three CSS methods and demonstrates the cascade.

### Project Structure

```
morning-brew/
├── index.html        (Home Page)
├── menu.html         (Menu Page)
└── styles.css        (Shared External Stylesheet)
```

---

### Stage 1 — Setup: Create the External Stylesheet

**`styles.css`** — This file styles both pages:

```css
/* General page styling */
body {
  background-color: #fff8f0;
  font-family: Georgia, serif;
  margin: 0;
  padding: 20px;
}

/* Header/brand styling */
h1 {
  color: #5c3317;
  text-align: center;
  font-size: 36px;
  margin-bottom: 5px;
}

/* Subheadings */
h2 {
  color: #8b4513;
  margin-left: 10px;
}

/* Paragraph text */
p {
  color: #4a3728;
  line-height: 1.6;
  margin-left: 10px;
}
```

**Expected result when applied:** A warm, coffee-toned colour scheme across all pages.

---

### Stage 2 — Home Page (External + Internal CSS)

**`index.html`:**

```html
<!DOCTYPE html>
<html>
<head>
  <!-- External CSS for the shared brand styles -->
  <link rel="stylesheet" href="styles.css">

  <!-- Internal CSS unique to this home page only -->
  <style>
    .welcome-banner {
      background-color: #5c3317;
      color: white;
      text-align: center;
      padding: 15px;
      border-radius: 8px;
      margin-bottom: 20px;
    }

    .welcome-banner h2 {
      color: white;
      margin: 0;
    }
  </style>
</head>
<body>

  <h1>Morning Brew Coffee Shop</h1>

  <div class="welcome-banner">
    <h2>Welcome! We are Open 7am–8pm Daily</h2>
  </div>

  <h2>About Us</h2>
  <p>
    Morning Brew is a cosy neighbourhood coffee shop founded in 2018.
    We serve freshly roasted coffee, handmade pastries, and simple meals.
  </p>

  <h2>Find Us</h2>
  <p>123 Sunrise Avenue, Lagos Island, Lagos</p>

</body>
</html>
```

**Milestone Output:**

```
[Page background: warm cream tone]
[Big centred heading: "Morning Brew Coffee Shop" in dark brown]
[Dark brown welcome banner with white text: "Welcome! We are Open 7am-8pm Daily"]
[Subheadings: medium brown]
[Paragraphs: dark warm brown, comfortably spaced]
```

---

### Stage 3 — Menu Page (External + Inline CSS)

**`menu.html`:**

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <h1>Morning Brew — Our Menu</h1>

  <h2>Coffee</h2>
  <p>Espresso — ₦800</p>
  <p>Cappuccino — ₦1,200</p>
  <p>Latte — ₦1,400</p>

  <!-- Special deal highlighted with inline CSS -->
  <p style="color: green; font-weight: bold;">
    ☕ Today's Special: Flat White — ₦900 (Save ₦300!)
  </p>

  <h2>Pastries</h2>
  <p>Croissant — ₦600</p>
  <p>Blueberry Muffin — ₦700</p>

  <!-- Out of stock item — inline CSS makes it grey and crossed out -->
  <p style="color: grey; text-decoration: line-through;">
    Chocolate Éclair — ₦850 (Out of Stock)
  </p>

</body>
</html>
```

**Milestone Output:**

```
[Heading: "Morning Brew — Our Menu" in dark brown, centred]
[Menu items: dark warm brown text]
[Today's Special: green bold text with checkmark emoji]
[Out-of-stock item: grey, crossed-out text]
```

---

### Stage 4 — Reflection

After completing the mini project, answer these questions:

1. The `styles.css` file controlled the look of both pages. If you change `background-color` in `styles.css`, which pages are affected?
2. The welcome banner on `index.html` used **internal CSS**. Why was it not put in `styles.css`?
3. The "Today's Special" line used **inline CSS**. Why was this a reasonable choice here compared to the rest of the menu text?
4. What would happen if you added `h1 { color: red; }` inside a `<style>` block on `menu.html` and placed it AFTER the `<link>` to `styles.css`?

**Optional Extension:** Add a third page (`contact.html`) that only uses external CSS. Create a simple contact section with a heading and two paragraphs. Observe that no extra CSS work is needed — the brand look appears automatically.

---

## Section 11 — Reflection Questions

Think carefully about each of these questions. They review the key ideas from the lesson.

1. You are building a 30-page website. All pages should have the same fonts and colours. Which CSS method would you choose and why?

2. You have a single special promotional page that needs a completely different look from the rest of the website. Which CSS method would be most convenient for this page's unique styles?

3. One of your colleagues writes all their styles as inline CSS. What problems might they experience when the client asks to change all the heading colours from blue to green?

4. You link an external CSS file and also write an internal `<style>` block. Both define a rule for `<p>` text colour. You notice the external file's colour is showing. What does this tell you about the order of the `<link>` tag and the `<style>` block in the `<head>`?

5. True or False: "Inline CSS has the lowest priority in the cascade." Explain your answer.

6. You write: `font-size: 24 px;` — will this work? Why or why not?

7. A new developer on your team adds `<style>` blocks inside the `<body>` section of HTML files. Is this correct? What would you tell them?

8. Can an external `.css` file contain HTML tags like `<h1>` or `<p>`? Why or why not?

---

## Section 12 — Completion Checklist

Go through this list and confirm you can do or explain each item:

- [ ] I can explain the difference between External, Internal, and Inline CSS in simple words
- [ ] I can write a `<link>` tag to connect an HTML page to an external CSS file
- [ ] I know what `rel="stylesheet"` and `href` mean in a `<link>` tag
- [ ] I can write a `<style>` block inside the `<head>` section with CSS rules
- [ ] I can apply inline CSS to a single HTML element using the `style` attribute
- [ ] I understand that the last-read stylesheet rule wins when two rules conflict
- [ ] I can correctly describe the cascading priority order: inline → stylesheet → browser defaults
- [ ] I know not to put spaces between a number and its unit (e.g., `20px` not `20 px`)
- [ ] I know not to write HTML tags inside a `.css` file
- [ ] I can choose the right CSS method for a given situation
- [ ] I completed at least one of the three guided practice exercises
- [ ] I completed at least Stage 1 and Stage 2 of the Mini Project

---

## Lesson Summary

You have now mastered one of the most foundational skills in CSS — knowing **how to connect your styles to your HTML**.

Here is a compact review of everything you learned:

**The Three Ways to Add CSS:**

| Method | Syntax | Best For |
|--------|--------|----------|
| External CSS | `<link rel="stylesheet" href="file.css">` in `<head>` | Multi-page websites, professional projects |
| Internal CSS | `<style> ... </style>` inside `<head>` | Single unique pages, quick tests |
| Inline CSS | `style="property: value;"` on an element | One-off styles, emails, debugging |

**Multiple Style Sheets Rule:**
When two stylesheets both define a style for the same element, the **last one read** takes effect.

**The Cascading Order (Highest to Lowest Priority):**
1. Inline CSS (always wins)
2. Internal and External CSS (order of placement determines which wins between them)
3. Browser Default Styles (lowest — always overridden)

**Key Rules to Remember:**
- Never add spaces between a number and its unit: write `20px` not `20 px`
- External `.css` files must contain only CSS — no HTML tags
- Always place `<link>` and `<style>` tags inside `<head>`, not `<body>`
- Prefer external CSS for anything that needs to be reused across more than one page
- Use inline CSS sparingly — it mixes content with presentation and is hard to maintain

**Real-World Connection:**
Every professional website you have ever visited uses external CSS. Large sites like Wikipedia, GitHub, or any banking website have carefully organised external stylesheets that apply styles consistently across hundreds or thousands of pages. The cascade allows designers to set broad global styles (body font, link colours) and override them precisely where needed — all following the same rules you just learned.

---

*End of Lesson 03 — You are now ready to move on to CSS Comments and CSS Colours.*
