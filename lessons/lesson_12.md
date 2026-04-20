---
render_with_liquid: false
title: "CSS Outlines — Style, Width, Color, Shorthand & Offset"
nav_order: 12
---

# Lesson 12: CSS Outlines — Style, Width, Color, Shorthand & Offset

---

## Lesson Introduction

Welcome to Lesson 12! In this lesson, you will learn everything about **CSS outlines** — one of the most useful visual tools for highlighting elements on a web page.

By the end of this lesson, you will be able to:
- Understand what an outline is and how it differs from a border
- Apply all available outline styles
- Control outline width using keywords and measurements
- Choose outline colours using names, HEX, RGB, and the special `invert` value
- Write outlines using the shorthand property
- Create a gap between an element and its outline using `outline-offset`
- Build a complete mini-project combining all outline skills

No prior experience with CSS outlines is needed. Let's begin from the very beginning.

---

## Prerequisite Concepts

Before diving in, let's make sure you understand the concepts this lesson builds on.

### What Is a CSS Property?

A **CSS property** is an instruction you write to tell the browser how an element should look. For example:

```css
color: red;
```

Here, `color` is the **property** and `red` is the **value**.

### What Is the CSS Box Model?

Every element on a webpage is surrounded by an invisible box. That box has four layers (from the inside out):

```
+---------------------------+
|        MARGIN             |  <- Space outside everything
|  +---------------------+  |
|  |      BORDER         |  |  <- A visible line around the element
|  |  +---------------+  |  |
|  |  |   PADDING     |  |  |  <- Space inside the border
|  |  |  +---------+  |  |  |
|  |  |  | CONTENT |  |  |  |  <- Your actual text or image
|  |  |  +---------+  |  |  |
|  |  +---------------+  |  |
|  +---------------------+  |
+---------------------------+
          OUTLINE is drawn here -> OUTSIDE the border
```

> **Key point:** The **outline** sits outside the border and outside the margin space. It does NOT affect the layout (it does not push other elements away).

### What Is a CSS Border vs. an Outline?

This is one of the most important distinctions in this lesson:

| Feature | Border | Outline |
|---|---|---|
| Position | Between padding and margin | Outside the border |
| Affects layout? | YES — adds to element size | NO — invisible to layout |
| Can style each side separately? | YES | NO — all 4 sides are the same |
| Takes up space? | YES | NO |
| Offset support? | NO | YES (`outline-offset`) |

**Analogy:** Think of a **border** as the frame of a picture. Think of an **outline** as a glowing halo around the frame — it floats outside the frame without changing its size or position.

---

## Part 1: CSS Outline Style

### What Is `outline-style`?

The `outline-style` property sets the type of line that is drawn around an element. Just like `border-style`, you can choose from several visual styles.

> **Important rule:** You MUST set an `outline-style` before any other outline property will be visible. Without a style, the outline will not appear — even if you set a colour or width.

### All Available `outline-style` Values

Here is a table of every possible value:

| Value | What It Looks Like |
|---|---|
| `dotted` | A line made of dots |
| `dashed` | A line made of short dashes |
| `solid` | A single solid continuous line |
| `double` | Two solid lines with a gap between them |
| `groove` | A carved/sunken 3D effect |
| `ridge` | A raised/protruding 3D effect (opposite of groove) |
| `inset` | Makes the element look embedded/sunken into the page |
| `outset` | Makes the element look like it is popping out of the page |
| `none` | No outline (this is the default) |
| `hidden` | Hides the outline (same visual result as `none`) |

### Simple Example: Showing Every Outline Style

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      padding: 10px;
      margin: 10px;
    }

    p.dotted   { outline-style: dotted; }
    p.dashed   { outline-style: dashed; }
    p.solid    { outline-style: solid; }
    p.double   { outline-style: double; }
    p.groove   { outline-style: groove; }
    p.ridge    { outline-style: ridge; }
    p.inset    { outline-style: inset; }
    p.outset   { outline-style: outset; }
    p.none     { outline-style: none; }
    p.hidden   { outline-style: hidden; }
  </style>
</head>
<body>
  <p class="dotted">I have a dotted outline.</p>
  <p class="dashed">I have a dashed outline.</p>
  <p class="solid">I have a solid outline.</p>
  <p class="double">I have a double outline.</p>
  <p class="groove">I have a groove outline.</p>
  <p class="ridge">I have a ridge outline.</p>
  <p class="inset">I have an inset outline.</p>
  <p class="outset">I have an outset outline.</p>
  <p class="none">I have no outline.</p>
  <p class="hidden">I have a hidden outline.</p>
</body>
</html>
```

**Expected Visual Output:**
Each paragraph renders with a different style of line surrounding it. The `none` and `hidden` paragraphs show no visible line.

> **Thinking Prompt:** What happens if you add `outline-color: red;` to one of these but forget to add `outline-style`? Nothing will appear! Try it and see why.

### Line-by-Line Explanation

- `p { padding: 10px; margin: 10px; }` — Adds breathing room inside and outside each paragraph so the outline is easy to see.
- `outline-style: dotted;` — The keyword `dotted` tells the browser to render the outline as a series of dots.
- No other outline properties are needed for the outline to appear. The browser uses default values for colour (usually the element's text colour) and default width (medium).

---

## Part 2: CSS Outline Width

### What Is `outline-width`?

The `outline-width` property controls **how thick or thin** the outline line is. A thin outline is subtle, while a thick one is bold and attention-grabbing.

> **Remember:** `outline-width` only works if `outline-style` has been set to something other than `none` or `hidden`.

### The Three Ways to Set Outline Width

**Method 1: Keyword Values**

CSS provides three built-in keyword sizes:

| Keyword | Typical Rendered Size |
|---|---|
| `thin` | approximately 1px |
| `medium` | approximately 3px (this is the default) |
| `thick` | approximately 5px |

The exact pixel rendering depends on the browser, but the relative sizes (thin < medium < thick) are always respected.

**Method 2: Pixel Values (`px`)**

You can specify any exact thickness in pixels:

```css
outline-width: 2px;
outline-width: 8px;
outline-width: 15px;
```

**Method 3: Other CSS Units**

You can also use `em`, `rem`, `%`, etc. — but `px` is the most common for outlines.

### Example: All Width Options

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      padding: 10px;
      margin: 15px;
      outline-style: solid; /* Required for width to be visible */
    }

    p.thin    { outline-width: thin; }
    p.medium  { outline-width: medium; }
    p.thick   { outline-width: thick; }
    p.px2     { outline-width: 2px; }
    p.px8     { outline-width: 8px; }
    p.px15    { outline-width: 15px; }
  </style>
</head>
<body>
  <p class="thin">Outline width: thin</p>
  <p class="medium">Outline width: medium (default)</p>
  <p class="thick">Outline width: thick</p>
  <p class="px2">Outline width: 2px</p>
  <p class="px8">Outline width: 8px</p>
  <p class="px15">Outline width: 15px</p>
</body>
</html>
```

**Expected Visual Output:**
Each paragraph has a solid outline. The outline gets progressively thicker from `thin` down to `15px`.

> **Thinking Prompt:** What would happen if you set `outline-width: 50px`? Does the outline push the other elements down? (Answer: No — outlines never affect layout.)

### Two More Quick Examples

**Example A — Combining style and width:**

```css
h1 {
  outline-style: dashed;
  outline-width: 4px;
}
```

**Expected Output:** A 4-pixel-wide dashed outline around every `<h1>` heading.

**Example B — Using `em` units:**

```css
button {
  outline-style: solid;
  outline-width: 0.2em;
}
```

**Expected Output:** The outline width scales proportionally to the button's font size.

---

## Part 3: CSS Outline Color

### What Is `outline-color`?

The `outline-color` property sets the **colour** of the outline line. You can use any standard CSS colour format.

> **Remember:** `outline-style` must be set first, or the colour will have nothing to apply to.

### Four Ways to Set Outline Color

**Method 1: Named Colours**

CSS has 140+ built-in colour names:

```css
outline-color: red;
outline-color: blue;
outline-color: coral;
outline-color: steelblue;
```

**Method 2: HEX Codes**

A HEX code is a 6-character code starting with `#`:

```css
outline-color: #ff0000;   /* Red */
outline-color: #336699;   /* Steel blue */
outline-color: #000000;   /* Black */
```

**Method 3: RGB Values**

RGB stands for Red, Green, Blue. Each channel ranges from 0 to 255:

```css
outline-color: rgb(255, 0, 0);     /* Red */
outline-color: rgb(0, 128, 0);     /* Green */
outline-color: rgb(100, 100, 255); /* Light blue */
```

**Method 4: `invert` — The Special Outline Value**

The `invert` value is unique to outlines (it does NOT work on borders). It performs a **colour inversion** on the screen area behind the outline.

```css
outline-color: invert;
```

**Why is `invert` useful?**
Imagine you have a button on a blue background. If you set the outline to `blue`, it would be invisible against the blue background! With `invert`, the outline always shows as a **contrasting** colour against whatever is behind it. It is guaranteed to be visible regardless of the background colour.

> **Note:** `invert` is part of the CSS specification, but browser support varies. It works reliably in most modern browsers. Always test it.

### Example: All Color Methods

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      padding: 10px;
      margin: 15px;
      outline-style: solid;
      outline-width: 3px;
    }

    p.named  { outline-color: red; }
    p.hex    { outline-color: #00cc44; }
    p.rgb    { outline-color: rgb(30, 100, 255); }
    p.invert { outline-color: invert; }
  </style>
</head>
<body>
  <p class="named">Named color: red</p>
  <p class="hex">HEX color: #00cc44 (green)</p>
  <p class="rgb">RGB color: rgb(30, 100, 255) (blue)</p>
  <p class="invert">Color: invert (adapts to background)</p>
</body>
</html>
```

**Expected Visual Output:**
- First paragraph: red outline
- Second paragraph: green outline
- Third paragraph: blue outline
- Fourth paragraph: outline appears as the inverse of the white background (which renders as black)

### Two More Quick Examples

**Example A — Bright highlight on a dark background:**

```css
.card {
  background-color: #222222;
  outline-style: solid;
  outline-width: 2px;
  outline-color: #ffdd00;  /* Yellow — highly visible on dark background */
}
```

**Example B — Using rgba for a semi-transparent outline:**

```css
.input-field {
  outline-style: solid;
  outline-width: 3px;
  outline-color: rgba(0, 100, 255, 0.5);  /* Semi-transparent blue */
}
```

---

## Part 4: CSS Outline Shorthand

### What Is the Outline Shorthand?

Just like `border` has a shorthand (`border: 2px solid red;`), CSS outlines have a shorthand property called `outline`. It lets you set the style, width, and colour all in one line.

### The Shorthand Syntax

```css
outline: [outline-width] [outline-style] [outline-color];
```

The **order** of values is: **width, then style, then color**

> **Critical rule:** The only **required** value is `outline-style`. Without it, nothing will appear. Width and colour are optional and will use defaults if omitted.

### Examples: Shorthand in Action

**Full shorthand (all three values):**

```css
p {
  outline: 3px solid red;
}
```

**Expected Output:** A 3-pixel-wide solid red outline around every `<p>`.

**Omitting width (uses default `medium`):**

```css
p {
  outline: dashed blue;
}
```

**Expected Output:** A medium-width dashed blue outline.

**Omitting color (uses default — usually the element's text colour):**

```css
p {
  outline: 5px dotted;
}
```

**Expected Output:** A 5px dotted outline in the element's default colour.

**Style only (absolute minimum):**

```css
p {
  outline: solid;
}
```

**Expected Output:** A medium-width solid outline in the default colour.

### Full Demonstration

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      padding: 10px;
      margin: 15px;
    }

    p.ex1 { outline: 3px solid red; }
    p.ex2 { outline: 2px dashed #0066cc; }
    p.ex3 { outline: thick dotted green; }
    p.ex4 { outline: double orange; }
    p.ex5 { outline: 6px ridge purple; }
    p.ex6 { outline: solid; }
  </style>
</head>
<body>
  <p class="ex1">outline: 3px solid red</p>
  <p class="ex2">outline: 2px dashed #0066cc</p>
  <p class="ex3">outline: thick dotted green</p>
  <p class="ex4">outline: double orange</p>
  <p class="ex5">outline: 6px ridge purple</p>
  <p class="ex6">outline: solid (defaults only)</p>
</body>
</html>
```

**Expected Visual Output:**
Six paragraphs each displaying a distinct outline style, colour, and thickness combination based on the shorthand values.

### Real-World Use Case: Focus Styling

One of the most important real-world uses of the outline shorthand is styling focused form inputs:

```css
input:focus {
  outline: 3px solid #005fcc;
}
```

When a user clicks or tabs into an input field, a clear blue outline appears — this is critical for **keyboard accessibility** so users who navigate with keyboards can see which element is active.

> **Pro tip:** Never write `outline: none;` on focusable elements without providing an alternative visible focus indicator. This is a major accessibility violation that harms users with disabilities who rely on keyboard navigation.

---

## Part 5: CSS Outline Offset

### What Is `outline-offset`?

`outline-offset` adds a **gap (space)** between the element's border edge and the outline. By default, an outline sits directly against the element's border with no gap between them.

With `outline-offset`, you can push the outline further away to create an elegant floating effect.

### Why Use `outline-offset`?

- Creates a visually attractive "double frame" look
- Makes focus indicators more polished
- Allows space between the element and its outline for design purposes

### Syntax

```css
outline-offset: [value];
```

The value can be:
- A **positive number** (e.g., `5px`) — pushes the outline outward
- A **negative number** (e.g., `-5px`) — pulls the outline inward (the outline appears inside the border)
- **Zero** — no gap (default behaviour)

### Simple Example: Visualising Different Offsets

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      padding: 15px;
      margin: 30px;
      border: 2px solid black;
      outline: 3px solid red;
    }

    p.no-offset  { outline-offset: 0px; }
    p.small      { outline-offset: 5px; }
    p.medium     { outline-offset: 15px; }
    p.large      { outline-offset: 30px; }
    p.negative   { outline-offset: -10px; }
  </style>
</head>
<body>
  <p class="no-offset">offset: 0px (default — outline touches border)</p>
  <p class="small">offset: 5px (small gap)</p>
  <p class="medium">offset: 15px (medium gap)</p>
  <p class="large">offset: 30px (large gap)</p>
  <p class="negative">offset: -10px (outline goes inside the element)</p>
</body>
</html>
```

**Expected Visual Output:**
- `0px`: The red outline sits right against the black border — they touch.
- `5px`: A small visible gap appears between the border and the outline.
- `15px`: A clear gap — the outline appears to float around the element.
- `30px`: A large gap — the outline is far from the element.
- `-10px`: The outline is drawn inside the border area, overlapping the element's interior.

> **Thinking Prompt:** What happens when you use a very large `outline-offset` like `50px`? Does it overlap the next element? (Remember: outlines do not affect layout, so neighbouring elements are visually unaffected.)

### Second Example: Elegant Card Design

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .card {
      display: inline-block;
      padding: 20px 40px;
      margin: 40px;
      background-color: #f0f4ff;
      border: 1px solid #ccc;
      outline: 2px solid #3366ff;
      outline-offset: 8px;
      font-size: 18px;
    }
  </style>
</head>
<body>
  <div class="card">I am a stylish card!</div>
</body>
</html>
```

**Expected Visual Output:**
A light-blue-background card with a thin grey border and a blue outline that floats 8px outside the border, creating a professional double-frame visual effect.

### Negative Offset — Inset Appearance

```css
.inset-look {
  padding: 20px;
  outline: 3px solid navy;
  outline-offset: -8px;
}
```

**Expected Output:** A navy outline that is drawn 8 pixels inside the element's border edge, as if it were stamped inside the element — creating an elegant inset badge effect.

---

## Guided Practice Exercises

### Exercise 1 — Basic Outline Styles

**Objective:** Get comfortable setting outline styles on different HTML elements.

**Scenario:** You are styling a study card app. Each card (a `<div>`) needs a distinct outline to categorise it visually.

**Steps:**

1. Create an HTML file with four `<div>` elements.
2. Give each div padding of `15px` and margin of `20px`.
3. Apply these outlines:
   - First card: `outline-style: solid;`
   - Second card: `outline-style: dashed;`
   - Third card: `outline-style: double;`
   - Fourth card: `outline-style: dotted;`

**Expected Output:**

```
[Card 1 — surrounded by a solid outline]
[Card 2 — surrounded by a dashed outline]
[Card 3 — surrounded by a double outline]
[Card 4 — surrounded by a dotted outline]
```

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .card {
      padding: 15px;
      margin: 20px;
      width: 200px;
    }
    .card1 { outline-style: solid; }
    .card2 { outline-style: dashed; }
    .card3 { outline-style: double; }
    .card4 { outline-style: dotted; }
  </style>
</head>
<body>
  <div class="card card1">Card 1 — Solid</div>
  <div class="card card2">Card 2 — Dashed</div>
  <div class="card card3">Card 3 — Double</div>
  <div class="card card4">Card 4 — Dotted</div>
</body>
</html>
```

**Self-check Questions:**
- Did all four outlines appear?
- Which style looks the most prominent — `solid` or `double`?
- What happens if you remove `outline-style` from one card?

**What-if challenge:** Change the third card to `outline-style: groove;` — does it look different on your screen? (The groove effect depends on the default colour.)

---

### Exercise 2 — Outline Width and Color

**Objective:** Practise combining width and colour with style.

**Scenario:** You are building a notification banner system. Different types of notifications need different outline appearances.

**Steps:**

1. Create three `<div>` elements representing info, warning, and error banners.
2. Style them with these outlines:
   - Info: `outline: 2px solid blue;`
   - Warning: `outline: 3px dashed orange;`
   - Error: `outline: 4px solid red;`
3. Add `10px` padding to each.

**Expected Output:**
Three boxes with thin blue solid, medium dashed orange, and thick solid red outlines respectively.

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      padding: 10px;
      margin: 15px;
      width: 300px;
    }
    .info    { outline: 2px solid blue; }
    .warning { outline: 3px dashed orange; }
    .error   { outline: 4px solid red; }
  </style>
</head>
<body>
  <div class="info">Info: Your profile has been updated.</div>
  <div class="warning">Warning: Your session is about to expire.</div>
  <div class="error">Error: Something went wrong. Please try again.</div>
</body>
</html>
```

**Self-check Questions:**
- Can you easily tell the difference between the three banners at a glance?
- Does changing the width from `2px` to `6px` for the info banner make it too visually heavy?

---

### Exercise 3 — Outline Offset in Practice

**Objective:** Practise the `outline-offset` property to create a floating outline effect.

**Scenario:** You are designing highlighted image thumbnails for a photography portfolio.

**Steps:**

1. Create a `<div>` with a background colour, fixed width and height, and a dark border.
2. Add a gold outline with a `6px` offset.
3. Observe the floating frame effect.

**Expected Output:** A square "photo card" with a gold outline floating 6px outside its dark border.

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .photo-card {
      width: 150px;
      height: 150px;
      background-color: #ccddee;
      border: 2px solid #333;
      outline: 3px solid gold;
      outline-offset: 6px;
      margin: 40px;
      display: inline-block;
    }
  </style>
</head>
<body>
  <div class="photo-card"></div>
</body>
</html>
```

**Self-check Questions:**
- Is the gold outline clearly separated from the dark border?
- What happens when you set `outline-offset: -5px`? Does the outline move inside the box?
- Try `outline-offset: 20px` — does the element's size or position change?

---

## Mini Project: "Focus-Friendly Profile Card"

### Project Goal

Build a small interactive profile card that shows off all the outline skills from this lesson. The card will have:
- A styled border
- An attractive floating outline using `outline-offset`
- A form input that highlights with a coloured outline when focused

### Stage 1 — Setup: The Basic Structure

```html
<!DOCTYPE html>
<html>
<head>
  <title>Profile Card</title>
  <style>
    body {
      background-color: #f5f5f5;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
      font-family: Arial, sans-serif;
    }
  </style>
</head>
<body>
  <div class="profile-card">
    <h2>Alex Morgan</h2>
    <p>Web Developer &amp; Designer</p>
    <label for="message">Send a message:</label><br>
    <input type="text" id="message" placeholder="Type here...">
  </div>
</body>
</html>
```

**Milestone Output:** A plain unstyled card centred on a light grey background. No outlines yet — just structure.

---

### Stage 2 — Core Styling: Card Border and Floating Outline

Add these styles inside the `<style>` block:

```css
.profile-card {
  background-color: white;
  padding: 30px 40px;
  border: 2px solid #cccccc;
  outline: 3px solid #3366ff;
  outline-offset: 8px;
  width: 300px;
  border-radius: 6px;
}

.profile-card h2 {
  color: #222222;
  margin: 0 0 8px 0;
}

.profile-card p {
  color: #666666;
  margin: 0 0 20px 0;
}
```

**Milestone Output:** A white card with a light grey border and a blue floating outline 8px away from the card edge. Looks polished and professional.

---

### Stage 3 — Input Focus Outline

```css
.profile-card label {
  font-size: 13px;
  color: #444;
}

.profile-card input[type="text"] {
  width: 100%;
  padding: 8px;
  border: 1px solid #cccccc;
  outline: 2px solid transparent; /* Invisible by default */
  outline-offset: 2px;
  border-radius: 4px;
  font-size: 14px;
  box-sizing: border-box;
  margin-top: 6px;
}

.profile-card input[type="text"]:focus {
  outline: 3px solid #3366ff; /* Visible when focused */
  outline-offset: 3px;
}
```

**Milestone Output:** When the user clicks or tabs into the input, a clear blue outline appears around it. When not focused, no outline is shown.

---

### Stage 4 — Final Combined Code

```html
<!DOCTYPE html>
<html>
<head>
  <title>Profile Card</title>
  <style>
    body {
      background-color: #f5f5f5;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
      font-family: Arial, sans-serif;
    }

    .profile-card {
      background-color: white;
      padding: 30px 40px;
      border: 2px solid #cccccc;
      outline: 3px solid #3366ff;
      outline-offset: 8px;
      width: 300px;
      border-radius: 6px;
    }

    .profile-card h2 {
      color: #222222;
      margin: 0 0 8px 0;
    }

    .profile-card p {
      color: #666666;
      margin: 0 0 20px 0;
    }

    .profile-card label {
      font-size: 13px;
      color: #444;
    }

    .profile-card input[type="text"] {
      width: 100%;
      padding: 8px;
      border: 1px solid #cccccc;
      outline: 2px solid transparent;
      outline-offset: 2px;
      border-radius: 4px;
      font-size: 14px;
      box-sizing: border-box;
      margin-top: 6px;
    }

    .profile-card input[type="text"]:focus {
      outline: 3px solid #3366ff;
      outline-offset: 3px;
    }
  </style>
</head>
<body>
  <div class="profile-card">
    <h2>Alex Morgan</h2>
    <p>Web Developer &amp; Designer</p>
    <label for="message">Send a message:</label><br>
    <input type="text" id="message" placeholder="Type here...">
  </div>
</body>
</html>
```

**Final Output:** A professional-looking centred profile card with a floating blue outline, a grey border, and a focused input that highlights in blue when clicked or tabbed into.

**Reflection Questions:**
- Why did we use `outline: 2px solid transparent;` by default and only show the real outline on `:focus`?
- What would happen to the layout if we had used `border` instead of `outline` on the card?
- How does `outline-offset: 8px` on the card change the visual compared to `0px`?

**Optional Extensions:**
- Add a `:hover` state to the card that changes the outline colour to orange.
- Try changing the card's outline to `outline: 3px dashed #3366ff;` and compare the look.
- Add a second card with a `groove` outline and a negative `outline-offset` of `-5px`.

---

## Common Beginner Mistakes

### Mistake 1: Setting outline properties without `outline-style`

**Wrong:**

```css
p {
  outline-color: red;
  outline-width: 3px;
  /* No outline-style! Nothing will appear */
}
```

**Problem:** Nothing appears. Colour and width are meaningless without a style.

**Correct:**

```css
p {
  outline-color: red;
  outline-width: 3px;
  outline-style: solid; /* This makes everything visible */
}
```

---

### Mistake 2: Confusing outline with border — trying to style individual sides

**Wrong thinking:** "I'll use `outline-top` to add a line to just the top."

**Reality:** Outlines do NOT support individual sides. `outline-top`, `outline-left`, `outline-right`, and `outline-bottom` do not exist.

```css
/* This is INVALID and will not work: */
outline-top: 2px solid red; /* Does not exist */

/* Use border for individual sides instead: */
border-top: 2px solid red; /* This works */
```

---

### Mistake 3: Expecting outlines to push other elements away

**Wrong thinking:** "My outline is 10px wide, so it will push nearby content away."

**Reality:** Outlines take up **zero space**. They can visually overlap adjacent elements but never shift them.

```css
/* This 20px outline will NOT affect the layout at all */
.box {
  outline: 20px solid blue;
}
```

---

### Mistake 4: Removing focus outlines without replacement

**Wrong:**

```css
/* NEVER do this without providing an alternative */
* {
  outline: none; /* Accessibility violation */
}
```

**Why it's harmful:** Users who navigate with keyboards (including many people with motor disabilities) rely on visible focus outlines to know which element is active.

**Correct — Replace it with a visible alternative:**

```css
*:focus {
  outline: 3px solid #0066cc; /* Custom, but still clearly visible */
  outline-offset: 3px;
}
```

---

### Mistake 5: Wrong shorthand order

**Wrong:**

```css
outline: red solid 3px; /* Incorrect — colour placed first */
```

**Correct:**

```css
outline: 3px solid red; /* Width, then Style, then Color */
```

The correct shorthand order is always: **width first, then style, then color**.

---

### Mistake 6: Using `outline-offset` without setting a style

```css
/* This will not work because there is no outline to offset */
p {
  outline-offset: 10px; /* No outline-style set above this */
}
```

**Correct:**

```css
p {
  outline-style: solid;   /* Now there is an outline to offset */
  outline-offset: 10px;
}
```

---

## Reflection Questions

1. What is the key difference between `outline` and `border` in terms of layout impact?
2. Why does `outline-style` have to be set before any other outline property will appear?
3. When would you prefer `outline-color: invert;` over a specific colour like `outline-color: red;`?
4. What does a negative `outline-offset` do, and when might you actually want to use it?
5. Why is removing `outline: none;` from focusable elements considered an accessibility violation?
6. In the shorthand `outline: 4px dashed green;`, which value controls thickness, which controls appearance, and which controls colour?
7. Think of a website you use regularly. Where do you think outlines are most useful on that website?

---

## Completion Checklist

Use this checklist to confirm you have mastered everything in this lesson:

- [ ] I understand what an outline is and how it differs from a border
- [ ] I can apply all `outline-style` values: `dotted`, `dashed`, `solid`, `double`, `groove`, `ridge`, `inset`, `outset`, `none`, `hidden`
- [ ] I understand that `outline-style` must be set for any other outline property to work
- [ ] I can set outline width using `thin`, `medium`, `thick`, and pixel values
- [ ] I can set outline colour using named colours, HEX, RGB, and `invert`
- [ ] I can use the shorthand `outline: [width] [style] [color];` correctly
- [ ] I can set `outline-offset` using positive and negative values
- [ ] I understand that outlines do NOT affect layout
- [ ] I understand that outlines cannot be set per-side (no `outline-top` etc.)
- [ ] I know NOT to remove focus outlines without providing an accessible alternative
- [ ] I have completed all three guided exercises
- [ ] I have built the profile card mini project
- [ ] I can explain when and why to use outlines in real web projects

---

## Lesson Summary

Here is a quick reference for everything you learned in Lesson 12:

### All Outline Properties at a Glance

| Property | Purpose | Example Value |
|---|---|---|
| `outline-style` | Type of line | `solid`, `dashed`, `dotted`, `double` |
| `outline-width` | Thickness of line | `thin`, `medium`, `thick`, `3px` |
| `outline-color` | Colour of line | `red`, `#ff0000`, `rgb(255,0,0)`, `invert` |
| `outline` | Shorthand (all in one) | `3px solid blue` |
| `outline-offset` | Gap between border and outline | `5px`, `-3px` |

### Outline Style Values

`dotted` • `dashed` • `solid` • `double` • `groove` • `ridge` • `inset` • `outset` • `none` • `hidden`

### Shorthand Syntax

```css
outline: [width] [style] [color];
/* Example: */
outline: 3px solid #0066cc;
/* Only style is required. Width and color are optional. */
```

### Key Rules to Never Forget

1. **`outline-style` is required.** Without it, nothing is visible.
2. **Outlines do not affect layout.** They take up no space.
3. **Outlines cannot be set per side.** All four sides are always the same.
4. **Never remove focus outlines** without providing an accessible alternative.
5. **`outline-offset`** adds (or subtracts) a gap between the border and the outline.

### Real-World Applications

- **Accessibility:** Focus outlines on form fields, buttons, and links make websites usable for keyboard and screen-reader users.
- **UI Design:** Floating outlines with `outline-offset` create elegant card highlights, selected-state indicators, and premium-looking component frames.
- **Debugging CSS:** Temporarily adding `outline: 1px solid red;` to all elements is a very common developer trick to visualise element boundaries without affecting layout.
- **Interactive Feedback:** Hover and focus state outlines give users clear visual confirmation that they have interacted with an element.

---

*You have completed Lesson 12: CSS Outlines. In the next lesson, you will begin exploring CSS Text — including text colour, alignment, decoration, and spacing.*
