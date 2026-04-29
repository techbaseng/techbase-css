---
render_with_liquid: false
title: "CSS Accessibility Styling"
nav_order: 44
---

# Lesson 44: CSS Accessibility Styling

---

## Lesson Introduction

Have you ever visited a website and found it impossible to read because the text was too small, the colours barely showed up, or clicking a button gave you no sign that it actually worked? Now imagine experiencing that on every website you visit — not because of a bad connection, but because you have a visual impairment, colour blindness, or a motor disability that makes using a mouse difficult.

That is the daily reality for hundreds of millions of people around the world.

**Web accessibility** means building websites that everyone can use — including people with disabilities. CSS (Cascading Style Sheets) plays a huge role in this. Even though CSS is "just about styling," the choices you make — font sizes, colours, contrast, focus outlines — have a real impact on whether someone can actually use your website.

In this lesson you will learn:
- What web accessibility means and why it matters
- How CSS choices directly affect people with disabilities
- How to write CSS that is visually appealing AND accessible
- The specific CSS properties and techniques that improve accessibility
- Common accessibility mistakes and how to fix them
- How to apply all of this in a real-world mini project

By the end, you will be able to write CSS that welcomes every visitor to your website, regardless of ability.

---

## Prerequisite Concepts

Before diving into CSS accessibility, make sure you understand these foundational ideas. If any of them are new, read through them carefully — they will make the rest of the lesson much clearer.

### What Is CSS?

CSS stands for **Cascading Style Sheets**. It is the language you use to style HTML elements — controlling colours, fonts, spacing, layout, and more. You write CSS rules like this:

```css
/* This is a CSS rule */
p {
  color: black;        /* text colour */
  font-size: 16px;     /* text size */
  background: white;   /* background colour */
}
```

- `p` is the **selector** — it targets all `<p>` (paragraph) HTML elements.
- Everything inside `{ }` is a list of **declarations**.
- Each declaration has a **property** (like `color`) and a **value** (like `black`).

### What Are HTML Elements?

HTML elements are the building blocks of a web page. Examples include:
- `<p>` — a paragraph of text
- `<a>` — a link
- `<button>` — a clickable button
- `<input>` — a text field you can type into
- `<h1>` to `<h6>` — headings of different sizes

### What Is a Focus State?

When a user navigates a web page using their **keyboard** (pressing the Tab key to move between links and buttons), the browser highlights the element that is currently "active" or selected. This highlighted state is called the **focus state**. It lets keyboard users know where they are on the page — just like a mouse cursor shows mouse users where they are.

### What Is Colour Contrast?

Colour contrast refers to the difference in brightness between the text colour and the background colour. High contrast (like black text on white) is easy to read. Low contrast (like grey text on light grey) is very hard to read — especially for people with visual impairments.

---

## Part 1: Understanding Web Accessibility

### What Is Web Accessibility?

**Web accessibility** (often abbreviated **a11y** — because there are 11 letters between the 'a' and the 'y') is the practice of designing and building websites so that everyone can use them, including people who have:

- **Visual impairments** — blindness, low vision, colour blindness
- **Motor impairments** — difficulty using a mouse; they navigate with a keyboard or other assistive devices
- **Cognitive impairments** — difficulty reading, concentrating, or understanding complex layouts
- **Auditory impairments** — deafness or hard of hearing (relevant mainly for audio/video content)

> 💡 **Real-world connection:** According to the World Health Organisation, about 1.3 billion people globally live with some form of disability. Building accessible websites is not a bonus feature — it is a fundamental responsibility.

### Why Does CSS Matter for Accessibility?

You might think CSS is just decoration. But consider these real situations:

- A developer removes the focus outline with `outline: none` to make the design look cleaner → keyboard users can no longer see where they are on the page → they cannot use the website.
- A developer sets text to `font-size: 10px` for a stylish look → users with low vision cannot read it → they leave the site.
- A developer uses light grey text on a white background → it looks minimal and modern → people with colour blindness struggle to read any content.

Every CSS decision you make either opens doors or closes them.

### The WCAG Guidelines

The **Web Content Accessibility Guidelines (WCAG)** are international standards created by the W3C (World Wide Web Consortium) to define what makes a website accessible. They are organised around four principles — websites must be:

1. **Perceivable** — users can see or hear the content
2. **Operable** — users can navigate and interact with it
3. **Understandable** — content and controls make sense
4. **Robust** — the site works with assistive technologies like screen readers

Many of the CSS techniques in this lesson directly help you meet WCAG standards.

---

## Part 2: Colour and Contrast Accessibility

### Why Colour Contrast Matters

Imagine reading a book where the words were printed in very light grey ink on white paper. You would have to squint and strain just to make out the letters. Now imagine that is your every day experience on the web.

People with low vision, colour blindness, or age-related vision changes rely on high contrast to read text. WCAG recommends a minimum contrast ratio of **4.5:1** for normal text and **3:1** for large text.

> 🤔 **Thinking prompt:** What does "contrast ratio 4.5:1" mean? It means the lighter colour is 4.5 times brighter than the darker colour. Black text on white background has a ratio of 21:1 — the maximum possible.

### Example 1 — Low Contrast (Bad)

```css
/* ❌ BAD: very hard to read */
p {
  color: #aaaaaa;        /* light grey text */
  background-color: #ffffff;  /* white background */
  font-size: 16px;
}
```

**Expected output on screen:** Very faint, barely visible grey text on a white page. Difficult for anyone with low vision, older adults, or people reading in bright sunlight.

### Example 2 — High Contrast (Good)

```css
/* ✅ GOOD: easy to read for everyone */
p {
  color: #000000;        /* black text */
  background-color: #ffffff;  /* white background */
  font-size: 16px;
}
```

**Expected output on screen:** Crisp black text on a white background. Maximum readability for all users.

### Example 3 — Dark Mode Contrast

```css
/* ✅ GOOD dark mode: light text on dark background */
body {
  color: #f0f0f0;           /* near-white text */
  background-color: #121212; /* near-black background */
}
```

**Expected output:** Light text shows clearly against a very dark background. Still high contrast, just inverted.

> 💡 **Tip:** Always use a free online contrast checker tool (like WebAIM's Contrast Checker at https://webaim.org/resources/contrastchecker/) to verify your colour combinations before publishing.

### Do Not Rely on Colour Alone

One of the most important accessibility rules is: **never use colour as the only way to convey information**.

#### Bad Example — Colour-Only Error Indicator

```css
/* ❌ BAD: only colour differentiates valid from invalid */
input.valid {
  border: 2px solid green;
}

input.invalid {
  border: 2px solid red;
}
```

**Problem:** A user who is red-green colour blind (a very common form of colour blindness) cannot tell the difference between a valid and an invalid input field.

#### Good Example — Colour + Text + Icon

```css
/* ✅ GOOD: colour + visible label is used */
input.invalid {
  border: 2px solid #cc0000;
  background-color: #fff0f0;
}

.error-message {
  color: #cc0000;
  font-weight: bold;
}
```

```html
<input class="invalid" type="text" value="bad input">
<span class="error-message">⚠ This field is required</span>
```

**Expected output:** The input has a red border AND a visible error message with a warning icon. Even without seeing red, the user knows there is an error.

---

## Part 3: Font Size and Readability

### Why Font Size Matters

Small fonts are a major accessibility barrier. Older users, people with low vision, and even tired readers struggle with tiny text. The web standard recommends a minimum body font size of **16px**, but many designers incorrectly use 12px or 14px to cram more onto the screen.

### Absolute vs. Relative Units

This is a critical accessibility concept:

- **Absolute units** (like `px`) are fixed. A `12px` font stays `12px` even if the user zooms their browser or increases their system font size.
- **Relative units** (like `rem` or `em`) scale with the user's browser settings. If a user has set their browser to display larger text, `1rem` text will correctly grow larger.

> 🔑 **Key rule:** Use `rem` or `em` for font sizes, not `px`. This respects the user's own accessibility settings.

#### Understanding `rem`

`1rem` = the font size of the root `<html>` element. By default, browsers set this to `16px`. So:
- `1rem` = 16px
- `1.5rem` = 24px
- `0.875rem` ≈ 14px

#### Example 1 — Bad: Fixed Pixel Sizes

```css
/* ❌ BAD: ignores user's browser accessibility settings */
body {
  font-size: 12px;
}

h1 {
  font-size: 20px;
}
```

**Problem:** If a user has their browser set to display larger text (a common accessibility setting), these fixed `px` values will NOT respond — the text stays tiny.

#### Example 2 — Good: Relative `rem` Sizes

```css
/* ✅ GOOD: respects user's accessibility settings */
html {
  font-size: 16px; /* this is our base — 1rem = 16px */
}

body {
  font-size: 1rem;    /* 16px — readable default */
}

h1 {
  font-size: 2rem;    /* 32px — clearly a heading */
}

h2 {
  font-size: 1.5rem;  /* 24px — a clear subheading */
}

small {
  font-size: 0.875rem; /* 14px — slightly smaller but still usable */
}
```

**Expected output:** Text sizes scale properly when users adjust their browser font settings. The hierarchy is clear: main heading is largest, body text is comfortable, small text is slightly smaller but still readable.

> 🤔 **What if this value changes?** Try setting `html { font-size: 20px; }` instead of 16px. Now `1rem = 20px`, so all your sizes scale up proportionally. This is the power of relative units.

### Line Height for Readability

Text crammed into tight lines is hard to read, especially for people with dyslexia or cognitive disabilities. Use `line-height` to add comfortable breathing room between lines.

```css
/* ✅ GOOD: comfortable line spacing */
p {
  font-size: 1rem;
  line-height: 1.6;    /* 1.6 times the font size — very readable */
  max-width: 70ch;     /* ch = width of the "0" character; 70ch ≈ ideal line length */
}
```

- `line-height: 1.6` means each line is 1.6 × 16px = 25.6px tall — enough space between lines.
- `max-width: 70ch` limits how wide a paragraph can get. Very long lines (100+ characters) are hard to read. 60–70 characters per line is ideal.

**Expected output:** Paragraphs with comfortable spacing between lines, and lines that don't stretch uncomfortably across a wide monitor.

---

## Part 4: Focus Styles — Keyboard Navigation Accessibility

### What Is a Focus Style?

When a user presses the **Tab** key on their keyboard, the browser moves focus from one interactive element to the next — links, buttons, form inputs, etc. The browser shows which element is focused using a **focus indicator** — typically a coloured outline or glow around the element.

This is critically important for:
- People who cannot use a mouse (motor disabilities, tremors, paralysis)
- People who prefer the keyboard for speed
- Screen reader users who navigate by Tab key

### The Cardinal Sin: `outline: none`

The single most common accessibility mistake in CSS is this:

```css
/* ❌ EXTREMELY BAD: removes all keyboard navigation visibility */
* {
  outline: none;
}

/* or */

a:focus,
button:focus {
  outline: none;
}
```

**Why this is written:** Developers dislike the browser's default blue or dotted outline because it can look out of place with a custom design.

**Why this is catastrophic:** It removes ALL visual indication of where the keyboard focus is. Keyboard users are now completely lost on the page — they cannot tell what they are about to activate.

> 💡 **Analogy:** Imagine driving a car but someone has removed all the road markings, traffic lights, and signs. That is what `outline: none` does to keyboard users.

### The Solution: Style the Focus, Don't Remove It

Instead of removing the outline, **redesign it** to match your brand while keeping it clearly visible.

#### Example 1 — Simple Custom Focus Style

```css
/* ✅ GOOD: visible custom focus style */
a:focus {
  outline: 3px solid #005fcc;   /* a strong blue outline */
  outline-offset: 4px;           /* gap between the element and the outline */
  border-radius: 4px;            /* slightly rounded corners */
}
```

**Expected visual output:**
- When a user tabs to any link, a thick blue outline appears around it with a small gap.
- The outline is clearly visible, does not overlap the element, and looks intentional.

#### Example 2 — Focus Style for Buttons

```css
/* ✅ GOOD: button focus style */
button:focus-visible {
  outline: 3px solid #ff6600;    /* orange outline */
  outline-offset: 3px;
  background-color: #fff3e0;     /* slightly lighter background hint */
}
```

**Expected output:** When a user tabs to a button, an orange outline appears around it. The slight background change adds a second visual cue.

### The `:focus-visible` Pseudo-Class

The `:focus-visible` pseudo-class is a modern improvement over `:focus`. Here is the difference:

- `:focus` applies styles whenever any element is focused — including when a mouse user clicks a button (which creates a brief focus state that looks ugly).
- `:focus-visible` applies styles ONLY when the browser determines the focus should be visually shown — mainly during keyboard navigation.

This gives you the best of both worlds: clean design for mouse users, visible focus for keyboard users.

```css
/* ✅ BEST PRACTICE: use :focus-visible */
button:focus-visible {
  outline: 3px solid #005fcc;
  outline-offset: 4px;
}
```

---

## Part 5: Accessible Form Styling

### Why Forms Need Special Accessibility Attention

Forms are where users do the most important things on a website — log in, sign up, search, submit orders. If form elements are poorly styled, users with disabilities may not be able to complete basic tasks.

Key principles for accessible form CSS:

1. Make inputs large enough to click/tap
2. Use high-contrast borders so inputs are visible
3. Clearly style the focus state of inputs
4. Make error messages visible and distinct

### Example 1 — Basic Accessible Input Styling

```css
/* ✅ GOOD: accessible text input */
input[type="text"],
input[type="email"],
input[type="password"],
textarea {
  display: block;
  width: 100%;
  padding: 12px 16px;       /* generous internal space — easier to click */
  font-size: 1rem;           /* not too small */
  border: 2px solid #555555; /* clearly visible border */
  border-radius: 4px;
  background-color: #ffffff;
  color: #111111;
  box-sizing: border-box;
}
```

**Expected output:** Form inputs are large, have a clear visible border, comfortable internal padding, and readable text.

### Example 2 — Focus State for Inputs

```css
/* ✅ GOOD: clearly visible focus for form fields */
input[type="text"]:focus,
input[type="email"]:focus,
textarea:focus {
  outline: 3px solid #005fcc;  /* blue outline */
  outline-offset: 2px;
  border-color: #005fcc;        /* also change border colour for extra cue */
}
```

**Expected output:** When a user clicks on or tabs into an input field, it gets a blue outline and a blue border — very clear indication that this field is active.

### Example 3 — Error State Styling

```css
/* ✅ GOOD: error state uses colour AND other visual cues */
input.error {
  border: 2px solid #cc0000;    /* red border */
  background-color: #fff5f5;    /* very light red tint */
}

.error-message {
  color: #cc0000;
  font-size: 0.875rem;
  font-weight: bold;
  margin-top: 4px;
  display: block;
}
```

```html
<!-- HTML showing how this is used -->
<label for="email">Email Address</label>
<input type="email" id="email" class="error" value="not-an-email">
<span class="error-message">⚠ Please enter a valid email address</span>
```

**Expected output:**
- Input has a red border and very faint red background
- Below it, a bold red message with a warning icon explains the error
- Even someone who cannot see red will understand from the icon and text that something is wrong

---

## Part 6: The `visibility: hidden` and `display: none` Trap

### Hiding Content Correctly for Accessibility

Sometimes you want to visually hide something (like a label you don't want cluttering the design), but you still need it to be available to screen readers (software that reads web pages aloud to blind users).

The problem is that `display: none` and `visibility: hidden` **remove content from screen readers entirely** — the screen reader will skip it completely. This can break accessibility for blind users.

#### Bad Approach — Hides from Everyone Including Screen Readers

```css
/* ❌ BAD for screen reader users */
.sr-only-bad {
  display: none;
}

/* Also bad */
.also-bad {
  visibility: hidden;
}
```

**Problem:** A screen reader user will not hear this content at all, even if it contains important information they need.

#### Good Approach — The "Visually Hidden" Pattern

This is a very well-known accessibility technique. It hides content visually but keeps it in the document for screen readers:

```css
/* ✅ GOOD: visually hidden but screen-reader accessible */
.visually-hidden {
  position: absolute;       /* remove from normal flow */
  width: 1px;               /* make it tiny */
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);  /* clip it to nothing visible */
  white-space: nowrap;
  border: 0;
}
```

```html
<!-- Example: a button with only an icon, but a label for screen readers -->
<button>
  <span aria-hidden="true">🔍</span>
  <span class="visually-hidden">Search</span>
</button>
```

**Expected output:**
- Visually, the button shows only the search icon emoji
- A screen reader will announce: "Search, button" — the user knows what this button does
- The label text "Search" is not visible on screen but IS read aloud

---

## Part 7: Skip Navigation Links

### The Problem with Long Navigation Menus

Imagine a website with a navigation bar containing 20 links. A sighted mouse user can ignore the nav and scroll directly to the content. But a keyboard or screen reader user must Tab through every single one of those 20 links every time they load a new page — before they can get to the actual article or content they came for. This is exhausting and frustrating.

### The Solution: Skip Links

A **skip navigation link** is a link at the very top of the page that says "Skip to main content." Sighted users usually never see it (it is hidden). Keyboard users press Tab first and it appears, allowing them to jump past the navigation with one click.

#### HTML

```html
<a href="#main-content" class="skip-link">Skip to main content</a>

<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
    <li><a href="/blog">Blog</a></li>
    <!-- more nav links... -->
  </ul>
</nav>

<main id="main-content">
  <h1>Article Title</h1>
  <p>Article content starts here...</p>
</main>
```

#### CSS

```css
/* ✅ GOOD: skip link is hidden visually but appears on focus */
.skip-link {
  position: absolute;
  top: -9999px;          /* pushed way off screen by default */
  left: 0;
  padding: 12px 20px;
  background-color: #005fcc;
  color: #ffffff;
  font-size: 1rem;
  font-weight: bold;
  text-decoration: none;
  border-radius: 0 0 8px 0;
  z-index: 9999;
}

/* When a keyboard user tabs to it, bring it into view */
.skip-link:focus {
  top: 0;               /* moves back into the visible area */
}
```

**Expected output:**
- For mouse users: the skip link is invisible — they never see it.
- When a keyboard user presses Tab, the skip link slides into view at the top of the page.
- They press Enter and jump directly to `#main-content`, bypassing all the navigation.
- Time saved: instead of tabbing through 20 nav links, they go straight to the content.

---

## Part 8: Motion and Animation Accessibility

### The Problem with Animations

Some users experience **vestibular disorders** — conditions that affect balance and spatial orientation. For these users, moving, spinning, or flashing content on screen can cause dizziness, nausea, and headaches. Excessive animation is also distracting for users with attention disorders.

### The `prefers-reduced-motion` Media Query

CSS provides a media query that detects whether the user has turned on the "Reduce Motion" setting in their operating system (available on macOS, Windows, iOS, and Android). You can then disable or simplify animations for those users.

#### Example 1 — Without Motion Consideration (Bad)

```css
/* ❌ Could be problematic for motion-sensitive users */
.hero-image {
  animation: slowSpin 10s linear infinite;
}

@keyframes slowSpin {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}
```

**Problem:** The image constantly spins. For users with vestibular disorders, this could cause genuine physical discomfort.

#### Example 2 — Respectful Motion (Good)

```css
/* ✅ GOOD: animation runs normally by default */
.hero-image {
  animation: slowSpin 10s linear infinite;
}

@keyframes slowSpin {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}

/* ✅ But if the user prefers reduced motion, stop the animation */
@media (prefers-reduced-motion: reduce) {
  .hero-image {
    animation: none;     /* completely stops the animation */
  }
}
```

**Expected output:**
- Most users see the spinning animation as intended.
- Users who have enabled "Reduce Motion" in their OS settings will see a still image — no spinning.

#### Example 3 — Gentle Alternative Instead of None

```css
/* ✅ EVEN BETTER: provide a subtle alternative instead of nothing */
.fade-in {
  animation: fadeIn 0.5s ease-in;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}

@media (prefers-reduced-motion: reduce) {
  .fade-in {
    /* Instead of removing the animation, make it instant */
    animation-duration: 0.01ms;
  }
}
```

---

## Part 9: Accessible Link Styling

### Why Links Need Special Attention

Links are how users navigate the web. Poorly styled links create two main accessibility problems:

1. **Not distinguishable from regular text** — if links look exactly like body text, users do not know they can click them
2. **Only colour indicates link state** — colour-blind users cannot tell the difference between a visited and unvisited link

### Example 1 — Poor Link Styling

```css
/* ❌ BAD: links look like regular text */
a {
  color: inherit;           /* same colour as body text */
  text-decoration: none;    /* no underline */
}
```

**Problem:** Users cannot visually identify links at all.

### Example 2 — Accessible Link Styling

```css
/* ✅ GOOD: links are clearly identifiable */
a {
  color: #0057b8;           /* distinct blue colour */
  text-decoration: underline; /* underline adds non-colour cue */
  font-weight: 500;
}

/* Different states */
a:visited {
  color: #7b00c8;           /* purple for visited links — a well-known convention */
}

a:hover {
  color: #003d82;           /* darker on hover */
  text-decoration: none;    /* removing underline on hover is ok when colour changes */
}

a:focus-visible {
  outline: 3px solid #0057b8;
  outline-offset: 3px;
  border-radius: 2px;
}

a:active {
  color: #002966;           /* even darker when actively clicked */
}
```

**Expected output:**
- Links are clearly blue and underlined — distinguishable by colour AND underline (two cues).
- Visited links turn purple — a familiar web convention users recognise.
- Hovered links darken — feedback that something will happen.
- Focused links (keyboard) get an outline — keyboard users know where they are.
- Active links (being clicked) darken further — immediate click feedback.

> 🔑 **Rule:** Use at least two visual indicators for a link state — not just colour. The underline is the classic second indicator.

---

## Part 10: Text Spacing and Readability

### WCAG Text Spacing Requirements

WCAG 1.4.12 (Text Spacing) states that users must be able to adjust text spacing without losing content or functionality. This means your CSS must not break when users apply custom spacing via accessibility tools. You should design WITH good spacing in the first place.

Good default text spacing rules:

```css
/* ✅ GOOD: comfortable text spacing by default */
body {
  font-size: 1rem;
  line-height: 1.6;       /* at least 1.5 recommended by WCAG */
  letter-spacing: 0.02em; /* small letter gap for readability */
  word-spacing: 0.05em;   /* small word gap */
}

p {
  margin-bottom: 1.5em;   /* space between paragraphs */
  max-width: 70ch;        /* ideal line length */
}
```

**Expected output:** Body text has comfortable line height, slight letter spacing, and paragraphs have clear gaps between them. Lines are limited in width to prevent eye fatigue from reading very long lines.

---

## Guided Practice Exercises

### Exercise 1 — Fix the Contrast

**Objective:** Identify and fix low-contrast CSS.

**Scenario:** A student blog has the following CSS that makes posts nearly unreadable.

**Starting Code (Broken):**

```css
body {
  background-color: #f5f5f5;
  color: #cccccc;         /* light grey text on light grey background */
  font-size: 13px;        /* too small */
  font-family: Arial, sans-serif;
}

a {
  color: #dddddd;         /* almost invisible links */
  text-decoration: none;  /* no underline */
}
```

**Steps to Fix:**
1. Change the `color` for `body` to something with at least 4.5:1 contrast ratio against `#f5f5f5`
2. Increase `font-size` to at least `1rem`
3. Give links a clear, distinct colour and add `text-decoration: underline`

**Expected Fixed Code:**

```css
body {
  background-color: #f5f5f5;
  color: #1a1a1a;           /* ✅ near-black — high contrast on light grey */
  font-size: 1rem;           /* ✅ comfortable size */
  font-family: Arial, sans-serif;
  line-height: 1.6;          /* ✅ bonus: comfortable line height */
}

a {
  color: #0057b8;            /* ✅ strong blue — distinct from body text */
  text-decoration: underline; /* ✅ second visual cue beyond colour */
}
```

**Self-check Questions:**
- Does the text now look clearly readable?
- Can you tell links from regular text without relying only on colour?
- Would a user who enlarges their browser font see the text grow properly?

---

### Exercise 2 — Restore the Focus Outline

**Objective:** Fix a site where the focus outline has been removed.

**Starting Code (Broken):**

```css
* {
  outline: none;   /* ❌ removes keyboard navigation visibility */
  box-sizing: border-box;
}

button {
  padding: 10px 20px;
  background: #007bff;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 14px;
}

a {
  color: #007bff;
  text-decoration: none;
}
```

**Steps to Fix:**
1. Remove the `outline: none` from the universal selector `*`
2. Add `font-size: 1rem` to the button
3. Add focus styles to buttons and links

**Expected Fixed Code:**

```css
* {
  /* removed outline: none — let the browser default show */
  box-sizing: border-box;
}

button {
  padding: 10px 20px;
  background: #007bff;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 1rem;   /* ✅ relative unit */
}

button:focus-visible {
  outline: 3px solid #ff8800;   /* ✅ visible orange focus ring */
  outline-offset: 3px;
}

a {
  color: #0057b8;
  text-decoration: underline;    /* ✅ added underline */
}

a:focus-visible {
  outline: 3px solid #0057b8;   /* ✅ visible focus outline */
  outline-offset: 4px;
  border-radius: 2px;
}
```

**Self-check Questions:**
- Open your browser, press Tab — can you see exactly which element is focused?
- Is the focus indicator clearly visible on both the button and the link?

---

### Exercise 3 — Add `prefers-reduced-motion` Support

**Objective:** Make an animated hero banner respectful of users with motion sensitivity.

**Starting Code:**

```css
.hero {
  animation: slideIn 1s ease-out;
}

@keyframes slideIn {
  from {
    transform: translateX(-100px);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}
```

**Task:** Add a `prefers-reduced-motion` media query that removes the slide animation but keeps a gentle fade-in instead.

**Expected Fixed Code:**

```css
.hero {
  animation: slideIn 1s ease-out;
}

@keyframes slideIn {
  from {
    transform: translateX(-100px);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

/* ✅ For users who prefer reduced motion */
@media (prefers-reduced-motion: reduce) {
  .hero {
    animation: gentleFade 0.5s ease-in;  /* gentle fade instead of slide */
  }
}

@keyframes gentleFade {
  from { opacity: 0; }
  to   { opacity: 1; }
}
```

**Self-check Questions:**
- What is the difference between using `animation: none` and providing a gentler alternative?
- Which approach is more considerate of the user experience?

---

## Mini Project: Accessible Blog Card Component

### Project Description

You will build a fully accessible blog post card — the kind you see on news sites and blogs, showing a post title, short excerpt, author name, and a "Read More" link.

**Accessibility goals:**
- High colour contrast
- Keyboard-focusable card with visible focus state
- Link that is clearly styled
- Focus-visible outline on interactive elements
- No reliance on colour alone
- Respect for `prefers-reduced-motion`

---

### Stage 1 — HTML Structure

First, write the HTML. This is the foundation.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Accessible Blog Card</title>
  <link rel="stylesheet" href="blog-card.css">
</head>
<body>

  <a href="#main" class="skip-link">Skip to content</a>

  <main id="main">
    <h1>Latest Articles</h1>

    <article class="blog-card">
      <h2 class="card-title">
        <a href="/articles/css-tips" class="card-link">
          10 CSS Tips Every Developer Should Know
        </a>
      </h2>
      <p class="card-meta">
        <span class="card-author">By Amara Okafor</span>
        <span class="card-date"> · April 22, 2026</span>
      </p>
      <p class="card-excerpt">
        From custom properties to advanced selectors, these CSS tricks will
        level up your stylesheet game and make your code cleaner and more
        maintainable...
      </p>
      <a href="/articles/css-tips" class="read-more" aria-label="Read more: 10 CSS Tips Every Developer Should Know">
        Read More →
      </a>
    </article>

  </main>

</body>
</html>
```

**Milestone output:** A plain unstyled card with a title, meta info, excerpt, and read-more link. It is functional but needs styling.

---

### Stage 2 — Core Accessible CSS

Now write the CSS in `blog-card.css`:

```css
/* ===========================
   BASE STYLES
   =========================== */

/* Reset and accessibility base */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  font-size: 16px; /* 1rem = 16px */
}

body {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 1rem;
  line-height: 1.6;
  color: #1a1a1a;           /* near-black — high contrast */
  background-color: #f8f8f8;
  padding: 2rem;
}

/* ===========================
   SKIP LINK
   =========================== */

.skip-link {
  position: absolute;
  top: -9999px;
  left: 0;
  padding: 12px 20px;
  background-color: #003d82;
  color: #ffffff;
  font-size: 1rem;
  font-weight: bold;
  text-decoration: none;
  border-radius: 0 0 8px 0;
  z-index: 9999;
}

.skip-link:focus {
  top: 0;   /* slides into view on keyboard focus */
}

/* ===========================
   PAGE HEADING
   =========================== */

h1 {
  font-size: 2rem;
  color: #111111;
  margin-bottom: 2rem;
}

/* ===========================
   BLOG CARD
   =========================== */

.blog-card {
  background-color: #ffffff;
  border: 1px solid #d0d0d0;
  border-radius: 8px;
  padding: 1.5rem 2rem;
  max-width: 600px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  transition: box-shadow 0.2s ease;
}

/* Hover effect for the card — adds depth */
.blog-card:hover {
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.14);
}

/* ===========================
   CARD TITLE
   =========================== */

.card-title {
  font-size: 1.4rem;
  line-height: 1.3;
  margin-bottom: 0.5rem;
}

/* The title is a link */
.card-link {
  color: #0057b8;            /* clear blue — high contrast on white */
  text-decoration: none;     /* remove underline from title by default */
  font-weight: bold;
}

.card-link:hover {
  text-decoration: underline; /* show underline on hover for clarity */
  color: #003d82;
}

.card-link:focus-visible {
  outline: 3px solid #0057b8;
  outline-offset: 4px;
  border-radius: 3px;
  text-decoration: underline;
}

.card-link:visited {
  color: #6a0dad;            /* visited purple — known convention */
}

/* ===========================
   CARD META (author, date)
   =========================== */

.card-meta {
  font-size: 0.875rem;
  color: #555555;            /* medium grey — still sufficient contrast on white */
  margin-bottom: 1rem;
}

.card-author {
  font-weight: bold;
  color: #333333;
}

/* ===========================
   CARD EXCERPT
   =========================== */

.card-excerpt {
  font-size: 1rem;
  color: #333333;
  line-height: 1.7;
  margin-bottom: 1.25rem;
  max-width: 65ch;
}

/* ===========================
   READ MORE LINK
   =========================== */

.read-more {
  display: inline-block;
  font-size: 0.9rem;
  font-weight: bold;
  color: #0057b8;
  text-decoration: underline;     /* always underlined — two cues */
  padding: 6px 0;
  transition: color 0.15s ease;
}

.read-more:hover {
  color: #003d82;
}

.read-more:focus-visible {
  outline: 3px solid #0057b8;
  outline-offset: 4px;
  border-radius: 2px;
}

.read-more:visited {
  color: #6a0dad;
}

/* ===========================
   REDUCE MOTION
   =========================== */

@media (prefers-reduced-motion: reduce) {
  .blog-card {
    transition: none;   /* remove hover transition for motion-sensitive users */
  }
}
```

**Milestone output:** A clean, well-spaced white card on a light grey page. Title is blue and bold. Meta text is slightly smaller. Excerpt is comfortable to read. "Read More" link is clearly styled. Skip link is invisible until you tab to it.

---

### Stage 3 — Test Your Accessibility

Go through this checklist manually:

1. **Contrast check:** Is the body text (`#1a1a1a`) on white (`#ffffff`) clearly readable? (It is — ratio is 18.1:1)
2. **Keyboard test:** Press Tab from the browser address bar. Do you see the skip link appear? Then does focus move to the card title link? Then to the Read More link? Can you see the focus outline at each step?
3. **Font size test:** In your browser settings, increase the default font size. Does the card text get larger too? (It should, because we used `rem`)
4. **Link identification:** Are links clearly distinguishable from body text without relying solely on colour?
5. **Hover test:** Hover over both links. Does something visible change?

### Optional Enhancement — Dark Mode Support

```css
/* ✅ BONUS: accessible dark mode */
@media (prefers-color-scheme: dark) {
  body {
    background-color: #121212;
    color: #e8e8e8;
  }

  .blog-card {
    background-color: #1e1e1e;
    border-color: #444444;
  }

  .card-title .card-link {
    color: #6ab0ff;   /* lighter blue for dark background */
  }

  .card-excerpt {
    color: #cccccc;
  }

  .card-meta {
    color: #aaaaaa;
  }

  .read-more {
    color: #6ab0ff;
  }
}
```

**Expected dark mode output:** On a system with dark mode enabled, the page switches to a dark background with light text, maintaining high contrast throughout.

---

## Common Beginner Mistakes

### Mistake 1 — Using `outline: none` Globally

```css
/* ❌ NEVER DO THIS */
* { outline: none; }
```

**Why it's wrong:** Removes all keyboard navigation visibility. Keyboard and screen reader users are lost.

**Fix:** Remove that rule and use `:focus-visible` with custom styles instead.

---

### Mistake 2 — Using Only Colour to Show State

```css
/* ❌ BAD: colour is the only way to see the error */
input.error { border-color: red; }
```

**Fix:** Also add a visible error message with text, and use a border-width change or background change as a second cue:

```css
/* ✅ GOOD */
input.error {
  border: 3px solid #cc0000;   /* thicker border — extra non-colour cue */
  background-color: #fff5f5;
}
/* plus an error message element with text */
```

---

### Mistake 3 — Setting Fixed `px` Font Sizes

```css
/* ❌ BAD: ignores user's accessibility settings */
body { font-size: 12px; }
```

**Fix:**

```css
/* ✅ GOOD */
html { font-size: 16px; }
body { font-size: 1rem; }
```

---

### Mistake 4 — Using `display: none` to Hide Important Content from Screen Readers

```css
/* ❌ BAD if this content is needed by screen readers */
.label { display: none; }
```

**Fix:** Use the visually-hidden pattern instead:

```css
/* ✅ GOOD */
.visually-hidden {
  position: absolute;
  width: 1px; height: 1px;
  padding: 0; margin: -1px;
  overflow: hidden;
  clip: rect(0,0,0,0);
  white-space: nowrap;
  border: 0;
}
```

---

### Mistake 5 — Making Touch/Click Targets Too Small

```css
/* ❌ BAD: 20x20px is far too small for a touch target */
.icon-button {
  width: 20px;
  height: 20px;
}
```

WCAG recommends a minimum touch target size of **44×44 pixels**. Small buttons are hard to press for people with motor impairments or tremors.

**Fix:**

```css
/* ✅ GOOD */
.icon-button {
  width: 44px;
  height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
}
```

---

### Mistake 6 — Removing Underlines from ALL Links

```css
/* ❌ BAD: underline is a key accessibility indicator */
a { text-decoration: none; }
```

Without underlines, colour is the only way to distinguish links from body text. Colour-blind users may not be able to find links at all.

**Fix:** Keep underlines for body links, or if you remove them for design reasons, ensure another clear visual differentiator is present (like a different font weight or background highlight).

---

## Reflection Questions

Take a moment to think about these before moving on:

1. Why is `outline: none` one of the most dangerous things you can write in CSS from an accessibility perspective?

2. A designer tells you that grey text on white looks more elegant than black text. What would you say to them about accessibility? How would you find a compromise that is both attractive and readable?

3. What is the difference between `:focus` and `:focus-visible`? When would you use each?

4. A colleague says "only 1% of users use keyboard navigation, so it doesn't matter." How would you respond?

5. Why does using `rem` units instead of `px` for font sizes improve accessibility?

6. Why is it important to not rely on colour alone to communicate information (like errors, warnings, or link states)?

7. You have a website with a complex animated hero banner. A user emails you saying the animation makes them feel nauseous. What CSS technique would you use to help them?

8. What is a skip link, and who benefits from it most?

---

## Completion Checklist

Use this to verify you have mastered the lesson:

- [ ] I understand what web accessibility means and why it matters
- [ ] I can explain why CSS choices directly impact users with disabilities
- [ ] I know how to choose colour combinations with sufficient contrast
- [ ] I understand the difference between relying on colour alone vs. using multiple cues
- [ ] I can write accessible `font-size` using `rem` units
- [ ] I understand the purpose of `line-height` and `max-width` for readable text
- [ ] I know what a focus state is and why it must never be removed
- [ ] I can write `:focus-visible` styles for links, buttons, and inputs
- [ ] I understand the visually-hidden pattern and when to use it vs. `display: none`
- [ ] I can implement a skip navigation link
- [ ] I can use `@media (prefers-reduced-motion: reduce)` to respect motion sensitivity
- [ ] I have built the blog card mini project with all accessibility features
- [ ] I can identify and fix the 6 common accessibility mistakes

---

## Lesson Summary

Web accessibility through CSS is not about adding extra steps — it is about making deliberate, thoughtful choices when you write your stylesheets. In this lesson, you learned:

**Colour and Contrast:** Text must have sufficient contrast against its background (minimum 4.5:1 ratio for normal text). Never use colour as the sole way to communicate meaning — always add text, icons, or border changes as additional cues.

**Font Sizes:** Use `rem` or `em` units instead of `px` so your text scales when users adjust their browser settings. Aim for at least `1rem` (16px) for body text, comfortable `line-height` of 1.5–1.6, and limited line lengths of 60–70 characters.

**Focus Styles:** Never write `outline: none`. Instead, redesign the focus indicator to match your brand while keeping it clearly visible. Use `:focus-visible` to show focus outlines for keyboard users without interfering with mouse interactions.

**Forms:** Style inputs with visible borders, generous padding, clear focus states, and error messages that use both colour AND text/icons.

**Hiding Content:** Use `display: none` only when content should be hidden from everyone. Use the visually-hidden CSS pattern when you want to hide content visually but keep it available for screen readers.

**Skip Links:** Add a skip navigation link at the top of each page. It is invisible to mouse users but appears for keyboard users, allowing them to jump directly to the main content.

**Motion:** Use `@media (prefers-reduced-motion: reduce)` to disable or soften animations for users who are sensitive to motion.

**Links:** Ensure links are always distinguishable from body text using at least two visual cues (e.g., colour + underline). Style all four link states: default, visited, hover, focus.

> 🌟 **Final thought:** Every time you write CSS, ask yourself: "Could someone use this if they couldn't use a mouse? Could they read this with low vision? Could they tell what is clickable if they couldn't see colour well?" Accessibility is not a feature — it is the foundation of good web design.

---

*Sources: W3Schools CSS Accessibility (https://www.w3schools.com/css/css_accessibility.asp) and CSS Accessibility Code Challenges (https://www.w3schools.com/css/css_challenges_accessibility.asp)*
