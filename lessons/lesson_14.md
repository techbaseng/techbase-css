---
render_with_liquid: false
title: "CSS Fonts for Absolute Beginners"
nav_order: 14
---

# CSS Fonts for Absolute Beginners

Welcome, future web designer! In this lesson, we are going to learn everything about styling text fonts using CSS. If you've ever wondered how websites change the look of their words—making them bigger, bolder, or using fancy styles—you are in the exact right place.

By the end of this lesson, you will know how to choose safe fonts, change text size, make text bold or italic, use custom fonts from Google, and even pair two different fonts together like a professional designer. We will start from the very beginning, assuming you have zero prior knowledge.

Let's get started!

## What Are CSS Fonts? (The Big Picture)

Before we write any code, let's understand **why** we change fonts.

**The Problem:** Imagine every website in the world used the exact same plain, boring text style (like an old typewriter). It would be hard to tell what is important, what is a title, or what brand you are looking at. It would be difficult to read and visually unappealing.

**The Solution:** CSS Fonts give us the power to control the "voice" of our text. Just like you change your tone of voice when telling a story or giving instructions, fonts help us communicate visually.

**Real-World Relevance:**
- **Brand Identity:** Think of the Coca-Cola logo or the Disney logo. Their specific fonts are a huge part of their identity. With CSS, you control the identity of your website.
- **Readability:** Have you ever tried to read tiny, squished text on your phone? Proper font sizing and style prevent that frustration for your users.
- **Professionalism:** A website with well-chosen fonts looks trustworthy and modern. A website with mismatched or default fonts looks unfinished.

### How Fonts Work on a Computer (Prerequisite Knowledge)
A very common beginner mistake is thinking: *"I chose a cool font, so everyone will see it!"*

**The Truth:** For a visitor to see a specific font on your website, that font must be **installed on their computer** (or phone).

**What is a Font Family?**
A **font family** is like a family of related designs. For example, the "Arial" family includes Arial, Arial Bold, Arial Italic, and Arial Black. In CSS, we usually just tell the browser to use the family name (like `Arial`), and the browser figures out which specific file to use for bold or italic text.

Let's use an analogy:
> Think of fonts like **clothing brands**. If you tell a friend to "wear a Nike shirt," they can only do that if they *own* a Nike shirt. If they don't own Nike, they might wear a similar Adidas shirt, or just a plain generic shirt. **CSS Fonts work exactly like this.**

In the next section, we will learn how to handle the situation when a visitor doesn't have our first-choice "brand" of font.

---

## Part 1: The Foundation - Web Safe Fonts and Fallbacks

Let's tackle the problem we just described: *What happens if the user's computer doesn't have the font we want?*

### What is a "Web Safe" Font?
**Web Safe Fonts** are fonts that are installed on almost **every** computer and phone in the world. If you use one of these, you can be 99% sure everyone will see it correctly.

**Why does this matter?** If you are building a simple business site or a personal blog, using Web Safe Fonts is the safest, fastest, and most reliable way to style text.

**The Five Generic Font Families**
At the very end of our font instructions, we always include a **generic family** name. This is the ultimate backup plan. It tells the browser: *"If you don't have ANY of the specific fonts I listed, just use ANY font you have that looks like this general category."*

The five categories are:
1.  **serif**: Fonts with small decorative lines (called "feet") at the ends of letters. They look formal, classic, and traditional. (Example: Times New Roman).
2.  **sans-serif**: Fonts **without** those little feet. They look clean, modern, and simple. (Example: Arial).
3.  **monospace**: Every single letter takes up the exact same amount of horizontal space (like a typewriter). Good for showing computer code.
4.  **cursive**: Fonts that look like handwriting.
5.  **fantasy**: Decorative, playful fonts.

### The "Fallback" System (Your Safety Net)
In CSS, we don't just list one font. We list a **priority list** separated by commas. This is called a **Font Stack** or **Fallback List**.

**How it works (Input → Process → Output):**
1.  **Input:** The browser reads your CSS rule: `font-family: "Gill Sans", Arial, sans-serif;`
2.  **Process:** The browser checks the visitor's computer.
    - *Does it have "Gill Sans"?* **Yes** → Stop searching! Display "Gill Sans".
    - *Does it have "Gill Sans"?* **No** → Move to the next one. Does it have "Arial"? **Yes** → Display "Arial".
    - *Does it have "Arial"?* **No** → Move to the final backup. Find **any** available `sans-serif` font and display that.
3.  **Output:** The user sees the text in the first available font from your list.

### Common Font Stacks (Your Cheat Sheet)
Here are the most reliable combinations you can copy and paste. Notice how names with spaces (like "Times New Roman") need **quotation marks**.

**Serif (Classic, Formal)**
```css
body {
  font-family: "Times New Roman", Times, serif;
}
/* Expected Output: Text looks like a newspaper or book. */
```

**Sans-Serif (Modern, Clean)**
```css
body {
  font-family: Arial, Helvetica, sans-serif;
}
/* Expected Output: Text looks smooth and modern, like Google or Facebook. */
```

**Monospace (Code / Typewriter)**
```css
code {
  font-family: "Courier New", Courier, monospace;
}
/* Expected Output: Every letter lines up perfectly in columns. */
```

> **Common Beginner Mistake #1: Forgetting the Generic Family**
> **Wrong:** `font-family: "Gill Sans", Arial;`
> **Problem:** If the user has neither Gill Sans nor Arial, the browser will use its **default** font (usually Times New Roman), which might look completely wrong with your modern design.
> **Corrected:** `font-family: "Gill Sans", Arial, sans-serif;`
> **Why this is better:** By adding `sans-serif`, you guarantee that even if all else fails, the browser picks a clean, modern-looking font.

---

## Part 2: Making Text Stand Out - Font Style, Weight, and Variant

Now that we know *what* font to use, let's control *how* it looks.

### 1. CSS `font-style`
**What it is:** Controls if the text is slanted.
**Values:**
- `normal`: Straight up and down (Default).
- `italic`: A special, cursive-looking slanted version of the font (uses a specific "Italic" font file if available).
- `oblique`: Just tilts the normal letters to the right. (It looks very similar to italic, but is a computer-generated tilt rather than a designed font).

**Simple Example:**
```css
p.normal-text {
  font-style: normal;
}
p.slanted-text {
  font-style: italic;
}
p.tilted-text {
  font-style: oblique;
}
```
**Expected Output:**
- **normal-text:** This text is straight.
- **slanted-text:** *This text is elegant and italic.*
- **tilted-text:** *This text is mechanically tilted.*

### 2. CSS `font-weight`
**What it is:** How thick or thin the characters are.
**Problem it solves:** Without changing the font size, how do we make a word "pop" or look like a heading? We make it **bold**.

**Understanding Values:**
- **Keywords:** `normal` (default), `bold`.
- **Relative Keywords:** `lighter`, `bolder` (Makes it lighter or bolder than the parent element).
- **Numeric Scale:** `100` (Thin) to `900` (Extra Black).
    - `400` is the same as `normal`.
    - `700` is the same as `bold`.

**Progressive Examples:**
*Level 1: Simple Bold*
```css
.highlight {
  font-weight: bold;
}
```
**Expected Output:** <span style="font-weight: bold;">This text is bold.</span>

*Level 2: Numeric Scale*
```css
.thin-text {
  font-weight: 300; /* Lighter than normal */
}
.extra-bold {
  font-weight: 900; /* Very thick */
}
```
**Expected Output:**
- <span style="font-weight: 300;">This text is light.</span>
- <span style="font-weight: 900;">This text is heavy and commanding.</span>

> **Common Beginner Mistake #2: Why isn't `font-weight: 500` working?**
> **Problem:** You set `font-weight: 500`, but the text looks exactly the same as `normal`.
> **Reason:** The specific font file you are using (e.g., "Times New Roman") might only have a "Regular" (400) and "Bold" (700) version installed on the user's computer. It doesn't have a "Medium" (500) version.
> **Lesson:** While numeric values give you more control *if* the font supports it, `bold` is safer for maximum compatibility.

### 3. CSS `font-variant`
**What it is:** A special trick for making text look like **Small Caps**.

**What does `small-caps` do?**
It transforms lowercase letters into **UPPERCASE LETTERS**, but makes them **smaller** than the normal uppercase letters.

**Why is this useful?**
It's a very elegant, professional way to style acronyms (like NASA or NATO) or subheadings without yelling at the reader in full-size ALL CAPS.

**Example:**
```css
.acronym {
  font-variant: small-caps;
}
```
**Expected Output:**
If you write: `<span class="acronym">nasa</span>`
The browser displays: **N**<small>ASA</small> (Notice the 'N' is big, but 'ASA' are smaller capital letters).

---

## Part 3: Controlling the Scale - CSS Font Size

Controlling font size is one of the most important skills for making a website readable on a phone, tablet, and desktop.

**The Golden Rule of Web Design:** Never use font size adjustments to make a paragraph look like a heading. Always use the correct HTML tags (`<h1>` to `<h6>` for headings, `<p>` for paragraph) and just style their sizes.

### 1. Absolute Sizing: Pixels (`px`)
**What it is:** A fixed, precise measurement. 1 pixel is one tiny dot on the screen.
**Why use it:** You want exact control. It's easy for beginners to understand.
**The Big Drawback:** Users **cannot** change the text size in their browser settings. For someone with poor eyesight, this makes the website hard to read.

**Example:**
```css
p {
  font-size: 16px; /* This is the default browser size */
}
h1 {
  font-size: 40px;
}
```
**Expected Output:** The `<h1>` is exactly 40 pixels tall. It will stay 40 pixels tall on a giant monitor and a tiny phone (which might make it look huge on mobile).

### 2. Relative Sizing: `em` and `rem`
This is where modern web design happens. Relative units **scale**.

**The `em` Unit**
**What it is:** A multiplier of the **parent element's** font size.
**Analogy:** Think of a Russian Doll. The size of the doll inside depends on the size of the doll outside.
- If the parent is `16px`, `1em` = `16px`.
- If the parent is `16px`, `2em` = `32px`.
- If the parent is `16px`, `0.5em` = `8px`.

**The Problem with `em`:** Compounding.
If you have a list inside a list, and you set both to `0.8em`, the inner list gets smaller and smaller and smaller! It can get out of control.

**Example with `em`:**
```css
body {
  font-size: 16px; /* Base size */
}
h1 {
  font-size: 2.5em; /* 2.5 * 16px = 40px */
}
p {
  font-size: 1em; /* 1 * 16px = 16px */
}
```

**The `rem` Unit (Root EM)**
**What it is:** A multiplier of the **ROOT `<html>` element's** font size ONLY. It **ignores** the parent element.
**Analogy:** A universal remote control. It only listens to the main base station (the `<html>` tag), not the TV in the bedroom.
**Why it's the King of Scalability:** You can change the font size of the `<html>` tag, and **EVERYTHING** on the page using `rem` scales perfectly and predictably without weird compounding math.

**Example with `rem`:**
```css
html {
  font-size: 16px; /* Root size setting */
}
h1 {
  font-size: 2.5rem; /* Always 40px, regardless of where it is on the page */
}
p {
  font-size: 1rem; /* Always 16px */
}
```

### 3. Viewport Sizing: `vw`
**What it is:** "Viewport Width". 1 `vw` = 1% of the browser window's width.
**What problem it solves:** Creating **fluid typography** that grows on big screens and shrinks on small screens.
**Real-World Use Case:** Hero headers that span the entire screen.

**Example:**
```css
h1 {
  font-size: 8vw;
}
```
**Expected Output:** If the browser is 1000px wide, the font is 80px. If you resize the browser to 500px wide, the font shrinks automatically to 40px.

> **Quick Comparison Chart (Cheat Sheet):**
> | Unit | Relative To... | Best For |
> | :-- | :-- | :-- |
> | `px` | Screen Pixels | Precise control, small borders |
> | `em` | Parent Element | Padding/Margins relative to text size |
> | `rem` | Root `<html>` Element | **ALL FONT SIZES** (Highly Recommended!) |
> | `vw` | Browser Width | Fluid headlines |

---

## Part 4: Using Custom Fonts - Google Fonts

What if you are tired of Arial and Times New Roman? What if you want a unique, beautiful font that nobody else has on their computer? **Google Fonts** is the answer.

**What is Google Fonts?**
It's a free library of over 1,000 fonts hosted on Google's super-fast servers. We can "borrow" these fonts temporarily for our website.

**How it Works (The Magic Trick):**
1.  **The Link:** You add a special link in the `<head>` of your HTML. This tells the browser, "Go download this font from Google real quick before you draw the page."
2.  **The CSS:** You then use the `font-family` property with the name of the Google Font.

**Step-by-Step Example: Using "Sofia" Font**

1.  **Find the Link:** Go to [fonts.google.com](https://fonts.google.com), find "Sofia", and copy the `<link>` tag.
2.  **Paste in HTML:**
    ```html
    <head>
        <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Sofia">
    </head>
    ```
3.  **Use in CSS:**
    ```css
    body {
        font-family: "Sofia", cursive; /* Notice we still use a generic fallback! */
    }
    ```
**Expected Output:** All your text will now be in the stylish, handwriting-like "Sofia" font.

### Using Multiple Google Fonts
You can request several fonts at once to save time. Just separate their names with a pipe `|` symbol.

```html
<head>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Audiowide|Trirong|Sofia">
</head>
```
**CSS:**
```css
h1.tech { font-family: "Audiowide", sans-serif; }
h1.serif { font-family: "Trirong", serif; }
h1.cursive { font-family: "Sofia", cursive; }
```

> **Performance Warning:** Adding 10 different Google Fonts will slow down your website. Try to stick to 2 or 3 maximum.

### Advanced Google Fonts: Font Effects
Google offers some cool visual effects (Fire, Neon, 3D) that you can enable without writing complex CSS yourself.

**How to Use Effects:**
1.  **Add `&effect=` to the URL:**
    `...css?family=Sofia&effect=fire|neon`
2.  **Add a Class to the HTML element:**
    `<h1 class="font-effect-fire">This text is on fire!</h1>`

**Example: Neon and Emboss**
```html
<head>
<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Sofia&effect=neon|emboss">
<style>
body { font-family: "Sofia", sans-serif; font-size: 40px; }
</style>
</head>
<body>
    <h1 class="font-effect-neon">Neon Sign</h1>
    <h1 class="font-effect-emboss">Embossed Metal</h1>
</body>
```
**Expected Output:** The text will appear to glow like a neon sign or be pressed into the page like metal.

---

## Part 5: Professional Design - Font Pairings

Now we enter the world of **typography design**. A great font pairing makes a website look expensive and professional. A bad pairing makes it look like a ransom note.

**The Four Rules of Pairing Fonts:**

1.  **Complement, Don't Conflict:** Find fonts that share a similar mood (e.g., serious, playful, modern) but look different enough.
2.  **Use Superfamilies:** This is the "Easy Button." Fonts like "Lucida Sans" and "Lucida Serif" were literally designed by the same person to work together.
3.  **Contrast is King:** The classic rule is **Serif Heading + Sans-Serif Body**. The difference between the structured serif title and the clean sans-serif text creates visual interest.
4.  **Choose Only One Boss:** One font should dominate. This is usually the heading font. Use **size** and **weight** to make it the clear leader.

### Classic Pairing #1: Georgia (Serif) & Verdana (Sans-Serif)
This is the "Old Faithful" of web design. Both are web safe.

```css
body {
  font-family: Verdana, sans-serif;
  font-size: 16px;
}
h1, h2, h3 {
  font-family: Georgia, serif;
  color: #333;
}
```
**Expected Result:** The body text is incredibly easy to read, while the headings have a touch of traditional elegance.

### Popular Google Pairing #1: Merriweather & Open Sans
This is a modern classic. Merriweather is a beautiful serif font designed for screens, and Open Sans is a neutral, friendly sans-serif.

**Setup:**
```html
<head>
    <link href="https://fonts.googleapis.com/css?family=Merriweather|Open+Sans" rel="stylesheet">
</head>
```
**CSS:**
```css
body {
  font-family: "Open Sans", sans-serif;
  line-height: 1.6; /* Improves readability */
}
h1 {
  font-family: "Merriweather", serif;
  font-weight: 700; /* Bold weight */
}
```
**Where you see this:** This pairing is used by countless blogs, news sites, and corporate websites because it is both readable and trustworthy.

### The "One Boss" Rule in Action
Notice how we make the heading the "Boss" by giving it a **different color**, **larger size**, and **different family**.

```css
body {
  background-color: #f4f4f4;
  font-family: 'Trebuchet MS', sans-serif;
  color: #555;
}
h1 {
  font-family: 'Impact', sans-serif;
  font-size: 4rem;
  color: #000;
  letter-spacing: 2px; /* Adds gap between letters */
}
```
**Expected Output:** The `h1` screams "I AM THE TITLE" while the `body` quietly whispers "I am the supporting information."

---

## Part 6: The Shortcut - CSS Font Shorthand

By now, we've written a lot of CSS properties for fonts. There is a shortcut to write them all on one line: the `font` property.

**The Order Matters!** You **MUST** follow this exact sequence:
`font: font-style font-variant font-weight font-size/line-height font-family;`

**Required Pieces:** You **must** include `font-size` and `font-family`. Everything else is optional (and will default to `normal`).

**Long Way (What we learned):**
```css
p {
  font-style: italic;
  font-variant: normal;
  font-weight: bold;
  font-size: 1.2rem;
  line-height: 1.5;
  font-family: Arial, sans-serif;
}
```

**Short Way (Shorthand):**
```css
p {
  font: italic normal bold 1.2rem/1.5 Arial, sans-serif;
}
```
**Expected Output:** Both code blocks do **exactly the same thing**.

**Important Note on `line-height`:** If you want to set the line height (space between lines), you add it after the font-size with a slash `/`.

```css
h1 {
  font: 2.5rem/1.2 "Helvetica Neue", sans-serif;
}
/* font-size is 2.5rem. Line-height is 1.2 (120% of font-size). Font-family is Helvetica Neue. */
```

> **Common Beginner Mistake #3: Wrong Order in Shorthand**
> **Wrong:** `font: Arial 16px;`
> **Problem:** The browser expects the **size** BEFORE the **family**.
> **Corrected:** `font: 16px Arial, sans-serif;`

---

## Part 7: Guided Practice Exercises

Let's put this knowledge to the test. Open your code editor and follow along!

### Exercise 1: Build a Font Stack
**Objective:** Ensure a heading uses a modern font stack that works on any computer.

**Scenario:** You are building a tech startup website. The brand requires a clean, modern sans-serif look.

**Steps:**
1.  Create an `h1` and a `p` in HTML.
2.  Write a CSS rule for `h1` that tries to use **'Trebuchet MS'** first, then **'Lucida Sans'**, then any **sans-serif**.
3.  Write a rule for `p` that uses **Arial**, then **Helvetica**, then **sans-serif**.

**Expected Output:**
- The heading should look clean and slightly wider than standard Arial (if Trebuchet is installed).
- The paragraph should be crisp and readable.

**Self-Check Question:** Why did we use `sans-serif` at the end of both lists?
*Answer: To ensure that if the specific fonts aren't available, the browser doesn't accidentally use a serif font like Times New Roman, ruining the modern look.*

### Exercise 2: Responsive Text with `rem`
**Objective:** Create a layout where all text scales up or down based on a single root setting.

**Scenario:** You want to be able to increase all text on the site for mobile users just by changing one line of code.

**Steps:**
1.  Set the `html` element to have a `font-size` of `20px` (just to make it obvious).
2.  Style `h1` to be `2rem`.
3.  Style `p` to be `1rem`.

**What If Challenge:** Change the `html` font-size to `16px`.
**Observation:** The `h1` changes from 40px to 32px. The `p` changes from 20px to 16px. This is the power of `rem`!

---

## Part 8: Mini Project - Personal Profile Card

Let's combine everything we've learned into a realistic project: A stylish "About Me" profile card.

**Stage 1: Setup (HTML Structure)**
```html
<!DOCTYPE html>
<html>
<head>
    <link href="https://fonts.googleapis.com/css?family=Montserrat|Lora" rel="stylesheet">
    <style>
        /* We will put our CSS here */
    </style>
</head>
<body>
    <div class="card">
        <h1>Alex Rivera</h1>
        <h2>Web Developer & Designer</h2>
        <p>I turn complex problems into simple, beautiful, and intuitive designs. When I'm not coding, you'll find me hiking or reading sci-fi novels.</p>
        <p class="location">📍 Austin, TX</p>
    </div>
</body>
</html>
```

**Stage 2: Core Logic (Styling the Fonts)**
We want a modern, elegant card. We will use **Montserrat** (Sans-Serif) for headings and **Lora** (Serif) for the body.
```css
html {
    font-size: 16px;
    background: #e0e5ec; /* Soft background */
}
.card {
    background: white;
    border-radius: 20px;
    padding: 30px;
    margin: 50px auto;
    width: 400px;
    box-shadow: 0 10px 20px rgba(0,0,0,0.1);
}
h1 {
    font-family: 'Montserrat', sans-serif;
    font-weight: 700; /* Bold */
    font-size: 2.5rem; /* 40px */
    margin-bottom: 0;
}
h2 {
    font-family: 'Montserrat', sans-serif;
    font-weight: 400; /* Normal weight */
    font-size: 1.2rem;
    color: #666;
    margin-top: 5px;
}
p {
    font-family: 'Lora', serif;
    line-height: 1.6;
    font-size: 1rem;
}
.location {
    font-weight: bold;
    color: #e74c3c;
}
```
**Expected Output:** You have a card with a bold, modern name (Montserrat) and a highly readable, elegant description (Lora). The hierarchy is clear.

**Stage 3: Enhancement (Adding Small Caps)**
Let's make the "Web Developer" subtitle look more professional.
```css
h2 {
    /* Add this line to the existing h2 rule */
    font-variant: small-caps;
    letter-spacing: 1px;
}
```

**Stage 4: Final Polish & Reflection**
**Reflection Questions:**
1.  Why did we choose Lora for the paragraph? *(Answer: Serif fonts like Lora are often easier to read in long blocks of text on screens.)*
2.  What happens if Google Fonts fails to load? *(Answer: The browser will use the fallbacks `sans-serif` and `serif`, which we defined. The site will still look decent, just with Arial/Times instead.)*

---

## Part 9: Common Beginner Mistakes Summary

1.  **Missing Fallbacks:** `font-family: "Cool Font";` **Fix:** Always add a generic family like `sans-serif`.
2.  **No Quotation Marks:** `font-family: Times New Roman;` **Fix:** Wrap multi-word names in quotes: `font-family: "Times New Roman", serif;`
3.  **Assuming Fonts Exist:** Using a fancy font from your own computer that is not a Google Font or Web Safe. **Fix:** Check if it's a Web Safe Font or use Google Fonts.
4.  **Too Many Fonts:** Using 5 different Google Fonts on one page. **Fix:** Limit to 2 fonts (one for headings, one for body).

---

## Part 10: Challenge: Code This!

Test your understanding. Open the code challenge below.

**Instructions:**
Inside your editor, complete the following steps:
1.  Set the `.serif` class `font-family` to **"Times New Roman", Times, serif**.
2.  Set the `.sans` class `font-family` to **Arial, Helvetica, sans-serif**.
3.  **Add a new rule** for `.mono` that sets `font-family` to **"Courier New", Courier, monospace**.

**Solution:**
```html
<!DOCTYPE html>
<html>
<head>
<style>
.serif {
  font-family: "Times New Roman", Times, serif;
}
.sans {
  font-family: Arial, Helvetica, sans-serif;
}
.mono {
  font-family: "Courier New", Courier, monospace;
}
</style>
</head>
<body>
  <p class="serif">This is a serif font (Times New Roman).</p>
  <p class="sans">This is a sans-serif font (Arial).</p>
  <p class="mono">This is a monospace font (Courier New).</p>
</body>
</html>
```

---

## Lesson Summary & Completion Checklist

Congratulations! You've mastered the art of CSS Fonts.

**You should now be able to:**
- ✅ Explain why we need Web Safe Fonts and Fallbacks.
- ✅ Create a reliable `font-family` stack using serif, sans-serif, and monospace.
- ✅ Make text bold using `font-weight` and italic using `font-style`.
- ✅ Use `font-variant: small-caps` for elegant acronyms.
- ✅ Set text size using `px`, `em`, and `rem` (and know when to use each).
- ✅ Import and use custom fonts from Google Fonts.
- ✅ Pair two different fonts together harmoniously.
- ✅ Use the `font` shorthand property correctly.

**Real-World Connection:** Every single website you visit uses these exact techniques to present text. Whether it's a news article, a product description on Amazon, or a button on a banking app, CSS Fonts make the web readable, accessible, and beautiful.

Keep practicing by inspecting the fonts on your favorite websites (Right-click → Inspect → Look for `font-family` in the Styles panel). Happy styling