---
render_with_liquid: false
title: "Lesson 17: CSS Lists — Styling Unordered and Ordered Lists"
nav_order: 17
---

# Lesson 17: CSS Lists — Styling Unordered and Ordered Lists

---

## Lesson Introduction

Lists are everywhere on the web. Every navigation menu, every step-by-step guide, every bullet-pointed feature comparison — all of these are built with HTML lists. By default, browser lists are plain: black dots for bullets, plain numbers for ordered steps, and a fixed amount of indentation.

But with CSS, you can transform lists completely. You can change the bullet to a square, a circle, a Roman numeral, or even a custom image. You can remove the bullet entirely and use the list as a layout tool. You can add colours, borders, hover effects, and padding to turn a plain list into a polished feature section or a styled navigation menu.

This lesson covers everything from the W3Schools CSS Styling Lists tutorial and its code challenges, merged into one smooth, progressive lesson that starts from absolute zero and ends with a real-world styled project.

---

## Prerequisite Concepts

### What is an HTML List?

There are two main types of lists in HTML:

**1. Unordered List (`<ul>`)** — items without a specific order. Each item gets a bullet point by default.

```html
<ul>
  <li>Apples</li>
  <li>Bananas</li>
  <li>Cherries</li>
</ul>
```

**Expected output in browser:**
```
• Apples
• Bananas
• Cherries
```

**2. Ordered List (`<ol>`)** — items with a specific order. Each item gets a number by default.

```html
<ol>
  <li>Preheat oven to 180°C</li>
  <li>Mix the ingredients</li>
  <li>Bake for 30 minutes</li>
</ol>
```

**Expected output in browser:**
```
1. Preheat oven to 180°C
2. Mix the ingredients
3. Bake for 30 minutes
```

**The `<li>` tag** stands for "list item." Every item inside a `<ul>` or `<ol>` must be wrapped in `<li>` tags.

> **Real-world analogy:** A `<ul>` is like a shopping list — the order doesn't matter. A `<ol>` is like a recipe — the order absolutely matters.

### What Properties Does CSS Give Us for Lists?

CSS provides three dedicated list-styling properties:

| Property | What It Controls |
|---|---|
| `list-style-type` | The shape or style of the bullet or number |
| `list-style-image` | Replaces the bullet with a custom image |
| `list-style-position` | Whether the bullet sits inside or outside the list item box |

Plus a shorthand: `list-style` — which sets all three in one line.

We will explore each one thoroughly.

---

## Part 1 — `list-style-type`: Changing the Bullet or Number Style

### What is `list-style-type`?

`list-style-type` is the CSS property that controls what kind of marker appears before each list item. The "marker" is the bullet dot, number, letter, or symbol at the start of each `<li>`.

**Why does this matter?** Different contexts call for different visual styles. A recipe needs numbers. A feature list needs clean bullets. A sidebar menu needs no bullets at all. CSS gives you full control over which marker is used.

---

### Values for Unordered Lists (`<ul>`)

#### `disc` — Filled Circle (Default)

This is the browser's default bullet. It is a solid, filled circle.

```html
<ul style="list-style-type: disc;">
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>
```

**Expected output:**
```
● HTML
● CSS
● JavaScript
```

---

#### `circle` — Hollow Circle

An outline circle — not filled, just the ring.

```css
ul {
  list-style-type: circle;
}
```

```html
<ul>
  <li>Python</li>
  <li>Java</li>
  <li>C++</li>
</ul>
```

**Expected output:**
```
○ Python
○ Java
○ C++
```

> **Thinking prompt:** When would a hollow circle look better than a filled disc? Think about light backgrounds vs dark backgrounds.

---

#### `square` — Filled Square

A solid filled square. Popular in modern, structured layouts.

```css
ul {
  list-style-type: square;
}
```

**Expected output:**
```
■ Item One
■ Item Two
■ Item Three
```

---

#### `none` — No Bullet at All

This completely removes the bullet marker. It is one of the most useful values because it lets you use `<ul>` purely as a layout container without any visual marker.

```css
ul {
  list-style-type: none;
}
```

**Expected output:**
```
Item One
Item Two
Item Three
```

No bullet at all — just the text. This is used extensively for navigation menus, card lists, and anywhere a list structure is needed without the visual marker.

---

### Values for Ordered Lists (`<ol>`)

#### `decimal` — Numbers (Default)

The default for ordered lists. 1, 2, 3, 4...

```css
ol {
  list-style-type: decimal;
}
```

**Expected output:**
```
1. Step One
2. Step Two
3. Step Three
```

---

#### `decimal-leading-zero` — Numbers with Leading Zero

Good for lists that need zero-padded numbers: 01, 02, 03...

```css
ol {
  list-style-type: decimal-leading-zero;
}
```

**Expected output:**
```
01. Step One
02. Step Two
03. Step Three
```

---

#### `lower-roman` — Lowercase Roman Numerals

Uses i, ii, iii, iv, v... Great for outlines, legal documents, or academic formatting.

```css
ol {
  list-style-type: lower-roman;
}
```

**Expected output:**
```
i.  Chapter One
ii. Chapter Two
iii. Chapter Three
```

---

#### `upper-roman` — Uppercase Roman Numerals

Uses I, II, III, IV, V... More formal than lowercase.

```css
ol {
  list-style-type: upper-roman;
}
```

**Expected output:**
```
I.   Introduction
II.  Methodology
III. Results
```

---

#### `lower-alpha` — Lowercase Letters

Uses a, b, c, d... Excellent for sub-lists or multiple choice questions.

```css
ol {
  list-style-type: lower-alpha;
}
```

**Expected output:**
```
a. Option One
b. Option Two
c. Option Three
```

---

#### `upper-alpha` — Uppercase Letters

Uses A, B, C, D... Often used in formal outlines.

```css
ol {
  list-style-type: upper-alpha;
}
```

**Expected output:**
```
A. First Point
B. Second Point
C. Third Point
```

---

#### `lower-greek` — Lowercase Greek Letters

Uses α, β, γ... Useful in scientific or mathematical contexts.

```css
ol {
  list-style-type: lower-greek;
}
```

---

#### `none` — No Number Marker

Just like with `<ul>`, you can strip the number entirely from an ordered list:

```css
ol {
  list-style-type: none;
}
```

---

### Side-by-Side Comparison — All Major Types

Here is a complete demo showing all major types in one file:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .disc    { list-style-type: disc; }
    .circle  { list-style-type: circle; }
    .square  { list-style-type: square; }
    .none    { list-style-type: none; }

    .decimal { list-style-type: decimal; }
    .roman-l { list-style-type: lower-roman; }
    .roman-u { list-style-type: upper-roman; }
    .alpha-l { list-style-type: lower-alpha; }
    .alpha-u { list-style-type: upper-alpha; }
  </style>
</head>
<body>

  <h3>Unordered</h3>
  <ul class="disc">   <li>disc</li>   <li>disc</li>   </ul>
  <ul class="circle"> <li>circle</li> <li>circle</li> </ul>
  <ul class="square"> <li>square</li> <li>square</li> </ul>
  <ul class="none">   <li>none</li>   <li>none</li>   </ul>

  <h3>Ordered</h3>
  <ol class="decimal"> <li>decimal</li> <li>decimal</li> </ol>
  <ol class="roman-l"> <li>lower-roman</li> <li>lower-roman</li> </ol>
  <ol class="roman-u"> <li>upper-roman</li> <li>upper-roman</li> </ol>
  <ol class="alpha-l"> <li>lower-alpha</li> <li>lower-alpha</li> </ol>
  <ol class="alpha-u"> <li>upper-alpha</li> <li>upper-alpha</li> </ol>

</body>
</html>
```

**Expected output:** A clear visual comparison of all list-style-type values rendered side by side.

---

## Part 2 — `list-style-image`: Using a Custom Image as a Bullet

### What is `list-style-image`?

Instead of a shape (disc, square, circle), you can use any image file as the bullet point. This is done with the `list-style-image` property.

**Why would you use this?** Brand consistency, visual flair, or themed websites. For example, a cooking website might use a small chef's hat icon as a bullet, or a travel blog might use a small plane icon.

### Syntax

```css
ul {
  list-style-image: url("path/to/image.png");
}
```

- `url(...)` — tells CSS this is a file path or URL
- The path inside the quotes points to your image file

### Full Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    ul.custom-bullets {
      list-style-image: url("https://www.w3schools.com/css/sqpurple.gif");
    }
  </style>
</head>
<body>

  <ul class="custom-bullets">
    <li>Coffee</li>
    <li>Tea</li>
    <li>Milk</li>
  </ul>

</body>
</html>
```

**Expected output:** Each list item has a small purple square image as its bullet instead of the default disc.

> **Important note:** `list-style-image` gives you limited control over the size and position of the image. For more precise control, designers often prefer removing the bullet with `list-style-type: none` and then adding the image using the CSS `background-image` property on the `<li>` element, with `padding-left` to make room for it. We will see this technique in the exercises.

---

## Part 3 — `list-style-position`: Inside vs Outside

### What is `list-style-position`?

This property controls where the bullet marker is positioned relative to the list item's content box. It has two values: `outside` (the default) and `inside`.

### `outside` — Default Behaviour

The bullet marker sits **outside** the list item's text box. This means if the text wraps to a second line, the wrapped text aligns back to the left edge of the first line — the bullet "hangs" to the left of the text.

```css
ul {
  list-style-position: outside;
}
```

**Visual representation:**
```
● This is a long list item text that wraps
  to the next line and aligns with the
  start of the first line of text.
```

The bullet hangs outside, and wrapped text indents inward.

---

### `inside` — Bullet Inside the Content Box

The bullet marker is placed **inside** the list item's content area. Wrapped lines of text align all the way to the left edge of the container — the same left edge where the bullet sits.

```css
ul {
  list-style-position: inside;
}
```

**Visual representation:**
```
● This is a long list item text that wraps
to the next line and goes all the way to
the left edge, under the bullet.
```

---

### Comparing Both Side by Side

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    ul.outside-list {
      list-style-position: outside;
      background-color: #f9f9f9;
      border: 1px solid #ccc;
      padding: 10px 40px;
    }

    ul.inside-list {
      list-style-position: inside;
      background-color: #f0f8ff;
      border: 1px solid #9bc;
      padding: 10px 20px;
    }
  </style>
</head>
<body>

  <h3>Outside (default)</h3>
  <ul class="outside-list">
    <li>This is a list item with enough text to wrap onto the next line so you can see the difference clearly</li>
    <li>Short item</li>
  </ul>

  <h3>Inside</h3>
  <ul class="inside-list">
    <li>This is a list item with enough text to wrap onto the next line so you can see the difference clearly</li>
    <li>Short item</li>
  </ul>

</body>
</html>
```

**Expected output:** You can clearly see the text wrapping difference. With `outside`, wrapped text indents away from the left. With `inside`, wrapped text aligns with the very left edge of the container.

> **When to use `inside`:** When you want a compact, aligned look, especially for list items inside cards, sidebar panels, or text-heavy content blocks where indentation would feel excessive.

---

## Part 4 — `list-style` Shorthand

### What is the Shorthand?

Instead of writing three separate properties, you can combine `list-style-type`, `list-style-position`, and `list-style-image` into one line with the `list-style` shorthand.

### Syntax

```css
list-style: [type] [position] [image];
```

All three values are optional. You only need to include the ones you want to set.

### Examples

**Set type and position only:**

```css
ul {
  list-style: square inside;
}
```

This is equivalent to:
```css
ul {
  list-style-type: square;
  list-style-position: inside;
  /* list-style-image defaults to none */
}
```

---

**Set type only:**

```css
ol {
  list-style: upper-roman;
}
```

Equivalent to:
```css
ol {
  list-style-type: upper-roman;
}
```

---

**Remove all markers:**

```css
ul {
  list-style: none;
}
```

This is the most common shorthand usage — stripping all list styling in one line.

---

**Set image and position:**

```css
ul {
  list-style: url("bullet.png") inside;
}
```

---

### Full Demo

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    ul.features {
      list-style: square inside;
      color: #333;
      font-size: 16px;
      line-height: 1.8;
    }

    ol.steps {
      list-style: upper-roman outside;
      color: #1a237e;
      font-size: 16px;
      line-height: 1.8;
    }
  </style>
</head>
<body>

  <h3>Product Features</h3>
  <ul class="features">
    <li>Lightning fast performance</li>
    <li>Works on all devices</li>
    <li>Free to use forever</li>
  </ul>

  <h3>Setup Steps</h3>
  <ol class="steps">
    <li>Download the installer</li>
    <li>Run the setup wizard</li>
    <li>Launch the application</li>
  </ol>

</body>
</html>
```

**Expected output:**
- Features list: square bullets positioned inside, dark grey text
- Steps list: uppercase Roman numerals (I, II, III) positioned outside, dark navy text

---

## Part 5 — Removing Default List Spacing and Padding

### Why Remove Default Spacing?

Browsers add default `padding-left` and sometimes `margin` to `<ul>` and `<ol>` elements. This is what creates the indentation you always see in browser lists. When you are building a navigation menu or a styled card list, this default indentation gets in the way.

### The Browser Default (What You Are Fighting)

```css
/* Browser adds this automatically — you cannot see it but it is there */
ul, ol {
  padding-left: 40px;
  margin-top: 1em;
  margin-bottom: 1em;
}
```

### How to Remove It

```css
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
```

**Line by line:**
- `list-style-type: none;` — removes the bullet markers
- `margin: 0;` — removes the vertical space above and below the whole list
- `padding: 0;` — removes the left indentation

**Expected output:** The list items appear flush to the left edge of their container, with no bullets and no extra spacing.

> **This is the foundation of every CSS navigation menu.** Once you remove the default list styling, you have a clean, flat group of `<li>` elements you can style however you want.

---

## Part 6 — Styling List Items: Colour, Background, and Padding

CSS treats `<li>` as a block-level element — meaning you can apply background colours, padding, margins, and borders directly to it. This is how you build styled lists that look like feature tables, settings menus, or product detail panels.

### Adding Colour and Background to List Items

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    ul.coloured-list {
      list-style-type: none;
      padding: 0;
      margin: 0;
      width: 220px;
    }

    ul.coloured-list li {
      background-color: #4CAF50;
      color: white;
      padding: 10px 16px;
      margin-bottom: 4px;
    }
  </style>
</head>
<body>

  <ul class="coloured-list">
    <li>Dashboard</li>
    <li>Reports</li>
    <li>Settings</li>
    <li>Log Out</li>
  </ul>

</body>
</html>
```

**Line by line:**
- `ul.coloured-list li` — targets every `<li>` inside a `<ul>` with class `coloured-list`
- `background-color: #4CAF50;` — gives each item a green background
- `color: white;` — white text for contrast
- `padding: 10px 16px;` — breathing room inside each item (10px top/bottom, 16px left/right)
- `margin-bottom: 4px;` — a small gap between each item

**Expected output:** A vertical stack of green pills with white text — resembling a sidebar navigation menu.

---

### Adding a Border Separator Between Items

Instead of a margin gap, you can use a bottom border to visually separate items:

```css
ul.bordered-list li {
  padding: 12px 16px;
  border-bottom: 1px solid #ccc;
  background-color: white;
}

ul.bordered-list li:last-child {
  border-bottom: none;  /* Remove border from the very last item */
}
```

**New here:** `li:last-child` is a CSS pseudo-class that selects only the LAST `<li>` in the list. We remove its bottom border because it is at the bottom of the list and does not need a separator.

**Expected output:** A clean list with thin grey lines dividing each item — similar to a settings menu or inbox list.

---

### Full Styled Vertical List

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    ul.menu {
      list-style-type: none;
      padding: 0;
      margin: 0;
      width: 200px;
      border: 1px solid #ddd;
      border-radius: 6px;
      overflow: hidden;         /* clips rounded corners at items */
    }

    ul.menu li a {
      display: block;           /* makes the whole row clickable */
      padding: 12px 16px;
      text-decoration: none;
      color: #333;
      background-color: #f9f9f9;
      border-bottom: 1px solid #ddd;
      transition: background-color 0.2s ease;
    }

    ul.menu li:last-child a {
      border-bottom: none;
    }

    ul.menu li a:hover {
      background-color: #e3f2fd;
      color: #0d47a1;
    }
  </style>
</head>
<body>

  <ul class="menu">
    <li><a href="#">Home</a></li>
    <li><a href="#">Profile</a></li>
    <li><a href="#">Settings</a></li>
    <li><a href="#">Help</a></li>
    <li><a href="#">Sign Out</a></li>
  </ul>

</body>
</html>
```

**New things here:**
- `display: block;` on the `<a>` inside `<li>` — this makes the entire row (not just the text) clickable. Without this, only the text acts as a clickable area.
- `overflow: hidden;` on the `<ul>` — ensures the rounded corners of the border are not broken by the background colour of the first and last items.
- `transition: background-color 0.2s ease;` — smooth hover colour change.

**Expected output:** A polished, bordered vertical navigation panel. Each row changes to a soft blue background on hover. The whole row is clickable.

> **Thinking prompt:** What happens if you remove `display: block` from the `<a>` tag? The clickable area shrinks to only the text itself. Try it!

---

## Part 7 — Horizontal Lists

Lists are vertical by default. But with CSS, you can arrange list items horizontally — which is exactly how most horizontal navigation bars and breadcrumbs are built.

### Making a Horizontal List with `display: inline`

```css
ul.horizontal {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

ul.horizontal li {
  display: inline;
  margin-right: 20px;
}
```

**`display: inline`** removes the block-level stacking behaviour of `<li>`. Items now flow side by side like text.

```html
<ul class="horizontal">
  <li>Home</li>
  <li>About</li>
  <li>Services</li>
  <li>Contact</li>
</ul>
```

**Expected output:** The four items appear on one line, spaced 20px apart.

---

### Making a Horizontal List with `display: inline-block`

`inline-block` is usually preferred over `inline` for list items because it lets you apply padding and height:

```css
ul.navbar {
  list-style-type: none;
  margin: 0;
  padding: 0;
  background-color: #333;
  overflow: hidden;
}

ul.navbar li {
  display: inline-block;
}

ul.navbar li a {
  display: block;
  color: white;
  text-decoration: none;
  padding: 14px 20px;
  transition: background-color 0.2s ease;
}

ul.navbar li a:hover {
  background-color: #555;
}
```

```html
<ul class="navbar">
  <li><a href="#">Home</a></li>
  <li><a href="#">About</a></li>
  <li><a href="#">Services</a></li>
  <li><a href="#">Contact</a></li>
</ul>
```

**Expected output:** A dark horizontal navigation bar with white text links. Each link's background darkens on hover.

> **Why `display: block` on the `<a>` inside `display: inline-block` on `<li>`?**  
> The `<li>` is `inline-block`, which flows horizontally. The `<a>` inside is `block`, which fills the entire `<li>` so the click area covers the full padded rectangle — not just the text.

---

## Part 8 — The `list-style-image` Property in Depth

### When to Use a Background Image Instead of `list-style-image`

As mentioned earlier, `list-style-image` is limited. You cannot easily control the size, position, or spacing of the image. A more flexible technique is:

1. Set `list-style-type: none` to remove the default bullet
2. Add `padding-left` to the `<li>` to make space for the image
3. Use `background-image` + `background-repeat: no-repeat` + `background-position` on the `<li>`

```css
ul.custom-img-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

ul.custom-img-list li {
  padding-left: 30px;                  /* space for the image */
  background-image: url("arrow.png");  /* the image */
  background-repeat: no-repeat;        /* show it only once, not tiled */
  background-position: left center;    /* align image to left, centred vertically */
  background-size: 18px 18px;          /* control the size precisely */
  margin-bottom: 8px;
  line-height: 1.6;
}
```

**Line by line:**
- `padding-left: 30px;` — pushes the text 30px away from the left, creating a visible gap where the image sits
- `background-image: url("arrow.png");` — sets the image file as the background
- `background-repeat: no-repeat;` — prevents the image from tiling/repeating across the element
- `background-position: left center;` — places the image on the left side, vertically centred within the item's line height
- `background-size: 18px 18px;` — explicitly controls how large the image renders

**Expected output:** Each list item has a small icon on the left, with text cleanly pushed to the right of the icon.

This technique is used widely in professional web development for icon-prefixed feature lists.

---

## Part 9 — Code Challenge Walkthroughs

The W3Schools CSS list code challenges test your ability to apply all the properties above. Here are the core challenge types with full solutions:

### Challenge Type 1: Change the List Marker Type

**Task:** Give the unordered list a `square` marker style.

```html
<ul>
  <li>Item A</li>
  <li>Item B</li>
</ul>
```

**Solution:**
```css
ul {
  list-style-type: square;
}
```

---

### Challenge Type 2: Remove All Bullets

**Task:** Remove the bullet markers from the list.

**Solution:**
```css
ul {
  list-style-type: none;
}
```

---

### Challenge Type 3: Set Position to Inside

**Task:** Place the list marker inside the list item's content box.

**Solution:**
```css
ul {
  list-style-position: inside;
}
```

---

### Challenge Type 4: Use the Shorthand

**Task:** Using the `list-style` shorthand, set the type to `circle` and position to `inside`.

**Solution:**
```css
ul {
  list-style: circle inside;
}
```

---

### Challenge Type 5: Use a Custom Image Bullet

**Task:** Use the image `"sqpurple.gif"` as the list bullet.

**Solution:**
```css
ul {
  list-style-image: url("sqpurple.gif");
}
```

---

### Challenge Type 6: Style a Specific `<li>` with Colour

**Task:** Give each list item a `tomato` background and `white` text, with `8px 16px` padding.

**Solution:**
```css
li {
  background-color: tomato;
  color: white;
  padding: 8px 16px;
}
```

---

### Challenge Type 7: Reset Default Padding and Margin

**Task:** Remove the default browser indentation from the list.

**Solution:**
```css
ul {
  padding: 0;
  margin: 0;
}
```

---

## Guided Practice Exercises

### Exercise 1 — Feature Comparison List

**Objective:** Style an unordered list to look like a clean feature list, as seen on SaaS product websites.

**Scenario:** You are building a pricing page for a cloud storage app. Each plan has a list of features. Style the free plan's feature list with square bullets, clean spacing, and a coloured background per item.

**Starter HTML:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Write your CSS here */
  </style>
</head>
<body>

  <h2>Free Plan — Features</h2>
  <ul class="feature-list">
    <li>5 GB Storage</li>
    <li>1 User Account</li>
    <li>Basic File Sharing</li>
    <li>Email Support</li>
  </ul>

</body>
</html>
```

**Target styling:**
- No bullet markers
- Each item has a light blue background (`#e3f2fd`) with a left blue border accent (`4px solid #1565c0`)
- Padding of `10px 16px` per item
- A small margin between items (`4px`)
- Dark navy text (`#1a237e`)
- `border-radius: 4px` for softness

**Solution:**

```css
ul.feature-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
  width: 280px;
}

ul.feature-list li {
  background-color: #e3f2fd;
  border-left: 4px solid #1565c0;
  color: #1a237e;
  padding: 10px 16px;
  margin-bottom: 4px;
  border-radius: 4px;
  font-size: 15px;
}
```

**Expected output:** A clean card-like feature list with blue left-accent borders. Each item is clearly separated.

**Self-check questions:**
- Does each item have a left blue border?
- Is there no default bullet showing?
- Is there a small gap between each item?

**Optional What-If:** What happens if you add `border-radius: 0;` to the items? How does the look change?

---

### Exercise 2 — Ordered Step-by-Step Guide

**Objective:** Style an ordered list to look like a step-by-step guide card.

**Scenario:** You are building a "Getting Started" section for a developer tool. Style the numbered steps to look like milestone cards.

**Starter HTML:**

```html
<ol class="steps-list">
  <li>Create a free account</li>
  <li>Install the command line tool</li>
  <li>Run your first project</li>
  <li>Deploy to production</li>
</ol>
```

**Target styling:**
- Use `upper-roman` numerals
- Position markers `inside`
- Background colour `#fff3e0` (light orange)
- Orange left border (`4px solid #e65100`)
- Padding `12px 18px`, margin bottom `6px`
- Font size `16px`, colour `#bf360c` (dark orange)
- Border radius `4px`

**Solution:**

```css
ol.steps-list {
  list-style-type: upper-roman;
  list-style-position: inside;
  padding: 0;
  margin: 0;
  width: 320px;
}

ol.steps-list li {
  background-color: #fff3e0;
  border-left: 4px solid #e65100;
  color: #bf360c;
  padding: 12px 18px;
  margin-bottom: 6px;
  border-radius: 4px;
  font-size: 16px;
}
```

**Expected output:** Four orange-tinted milestone cards with Roman numerals inside each one.

---

### Exercise 3 — Horizontal Navigation Menu from a List

**Objective:** Transform an unordered list into a horizontal navigation bar.

**Scenario:** You are building a simple website header. Convert the list into a navigation bar with a dark background and white hover effects.

**Starter HTML:**

```html
<ul class="topnav">
  <li><a href="#">Home</a></li>
  <li><a href="#">Products</a></li>
  <li><a href="#">Pricing</a></li>
  <li><a href="#">Contact</a></li>
</ul>
```

**Solution:**

```css
ul.topnav {
  list-style-type: none;
  margin: 0;
  padding: 0;
  background-color: #2c3e50;
  overflow: hidden;
}

ul.topnav li {
  display: inline-block;
}

ul.topnav li a {
  display: block;
  color: #ecf0f1;
  text-decoration: none;
  padding: 14px 22px;
  font-size: 15px;
  font-family: Arial, sans-serif;
  transition: background-color 0.2s ease;
}

ul.topnav li a:hover {
  background-color: #1abc9c;
  color: white;
}
```

**Expected output:** A dark slate-blue horizontal bar with light grey text links. On hover, each link gains a teal background.

---

## Mini Project — Styled Recipe Page with Lists

### Project Overview

You will build a complete recipe page that uses both unordered and ordered lists — styled as polished, modern UI components. The page will include: a list of ingredients (unordered) and a list of preparation steps (ordered).

---

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html>
<head>
  <title>Classic Pasta Recipe</title>
  <style>
    /* CSS added in later stages */
  </style>
</head>
<body>

  <div class="recipe-card">
    <h1>Classic Pasta al Pomodoro</h1>
    <p class="subtitle">A simple, timeless Italian pasta dish ready in 30 minutes.</p>

    <h2>🛒 Ingredients</h2>
    <ul class="ingredients">
      <li>400g spaghetti</li>
      <li>800g canned tomatoes</li>
      <li>3 cloves of garlic</li>
      <li>Fresh basil leaves</li>
      <li>4 tbsp olive oil</li>
      <li>Salt and pepper to taste</li>
      <li>Grated Parmesan cheese</li>
    </ul>

    <h2>👨‍🍳 Instructions</h2>
    <ol class="instructions">
      <li>Bring a large pot of salted water to the boil.</li>
      <li>Finely slice the garlic cloves.</li>
      <li>Heat olive oil in a pan and gently fry the garlic until golden.</li>
      <li>Add canned tomatoes and simmer for 15 minutes.</li>
      <li>Cook spaghetti according to package instructions.</li>
      <li>Drain the pasta and toss with the tomato sauce.</li>
      <li>Garnish with fresh basil and grated Parmesan.</li>
    </ol>

  </div>

</body>
</html>
```

**Milestone output:** Plain HTML with default browser list styling.

---

### Stage 2 — Style the Page Container

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Georgia, serif;
  background-color: #fdf6ec;
  color: #333;
  padding: 40px 20px;
}

.recipe-card {
  max-width: 680px;
  margin: 0 auto;
  background-color: white;
  border-radius: 12px;
  padding: 40px 50px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.08);
}

h1 {
  font-size: 32px;
  color: #c0392b;
  margin-bottom: 8px;
}

.subtitle {
  font-size: 15px;
  color: #888;
  margin-bottom: 32px;
  font-style: italic;
}

h2 {
  font-size: 20px;
  color: #444;
  margin-bottom: 16px;
  margin-top: 32px;
  border-bottom: 2px solid #f0e0d0;
  padding-bottom: 6px;
}
```

**Milestone output:** A white card centred on a warm cream background. Title in warm red, section headers with bottom borders.

---

### Stage 3 — Style the Ingredients List

```css
ul.ingredients {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

ul.ingredients li {
  padding: 9px 12px 9px 36px;
  margin-bottom: 6px;
  background-color: #fff8f0;
  border-left: 3px solid #e67e22;
  border-radius: 4px;
  font-size: 15px;
  position: relative;
}

ul.ingredients li::before {
  content: "✓";               /* adds a tick before each item */
  position: absolute;
  left: 10px;
  color: #e67e22;
  font-weight: bold;
}
```

**New concept — `::before` pseudo-element:**  
`li::before` inserts content visually before each list item without adding it to the HTML. `content: "✓"` inserts a tick character. `position: absolute` with `left: 10px` places it precisely in the padding area we created with `padding-left: 36px`.

**Milestone output:** Each ingredient appears as a warm orange-bordered card with a tick mark on the left.

---

### Stage 4 — Style the Instructions List

```css
ol.instructions {
  list-style-type: none;
  padding: 0;
  margin: 0;
  counter-reset: step-counter;     /* initialise a custom counter */
}

ol.instructions li {
  padding: 12px 16px 12px 54px;
  margin-bottom: 8px;
  background-color: #fdf2f2;
  border-left: 3px solid #c0392b;
  border-radius: 4px;
  font-size: 15px;
  position: relative;
  counter-increment: step-counter; /* increment for each li */
  line-height: 1.6;
}

ol.instructions li::before {
  content: counter(step-counter);  /* show the counter number */
  position: absolute;
  left: 14px;
  top: 50%;
  transform: translateY(-50%);
  background-color: #c0392b;
  color: white;
  width: 26px;
  height: 26px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 13px;
  font-weight: bold;
  font-family: Arial, sans-serif;
}
```

**New concepts here:**

- `counter-reset: step-counter;` — creates a CSS counter named `step-counter` and sets it to 0 on the `<ol>`. Think of it like a variable that starts at zero.
- `counter-increment: step-counter;` — on each `<li>`, the counter goes up by 1. First `<li>` → 1, second → 2, etc.
- `content: counter(step-counter);` — in the `::before` pseudo-element, this outputs the current number as text.
- The round red circle with the number is built entirely in CSS using `border-radius: 50%`, `width/height`, and `display: flex` for centering.

**Milestone output:** Each instruction step has a red circle with a step number on the left, like a progress timeline.

---

### Stage 5 — Complete Final Page

Here is the complete, fully combined recipe page:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Classic Pasta Recipe</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      font-family: Georgia, serif;
      background-color: #fdf6ec;
      color: #333;
      padding: 40px 20px;
    }

    .recipe-card {
      max-width: 680px;
      margin: 0 auto;
      background-color: white;
      border-radius: 12px;
      padding: 40px 50px;
      box-shadow: 0 4px 16px rgba(0,0,0,0.08);
    }

    h1 { font-size: 32px; color: #c0392b; margin-bottom: 8px; }
    .subtitle { font-size: 15px; color: #888; margin-bottom: 32px; font-style: italic; }
    h2 { font-size: 20px; color: #444; margin-bottom: 16px; margin-top: 32px;
         border-bottom: 2px solid #f0e0d0; padding-bottom: 6px; }

    /* ---- Ingredients ---- */
    ul.ingredients { list-style-type: none; padding: 0; margin: 0; }
    ul.ingredients li {
      padding: 9px 12px 9px 36px;
      margin-bottom: 6px;
      background-color: #fff8f0;
      border-left: 3px solid #e67e22;
      border-radius: 4px;
      font-size: 15px;
      position: relative;
    }
    ul.ingredients li::before {
      content: "✓";
      position: absolute;
      left: 10px;
      color: #e67e22;
      font-weight: bold;
    }

    /* ---- Instructions ---- */
    ol.instructions {
      list-style-type: none;
      padding: 0;
      margin: 0;
      counter-reset: step-counter;
    }
    ol.instructions li {
      padding: 12px 16px 12px 54px;
      margin-bottom: 8px;
      background-color: #fdf2f2;
      border-left: 3px solid #c0392b;
      border-radius: 4px;
      font-size: 15px;
      position: relative;
      counter-increment: step-counter;
      line-height: 1.6;
    }
    ol.instructions li::before {
      content: counter(step-counter);
      position: absolute;
      left: 14px;
      top: 50%;
      transform: translateY(-50%);
      background-color: #c0392b;
      color: white;
      width: 26px;
      height: 26px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 13px;
      font-weight: bold;
      font-family: Arial, sans-serif;
    }
  </style>
</head>
<body>
  <div class="recipe-card">
    <h1>Classic Pasta al Pomodoro</h1>
    <p class="subtitle">A simple, timeless Italian pasta dish ready in 30 minutes.</p>

    <h2>🛒 Ingredients</h2>
    <ul class="ingredients">
      <li>400g spaghetti</li>
      <li>800g canned tomatoes</li>
      <li>3 cloves of garlic</li>
      <li>Fresh basil leaves</li>
      <li>4 tbsp olive oil</li>
      <li>Salt and pepper to taste</li>
      <li>Grated Parmesan cheese</li>
    </ul>

    <h2>👨‍🍳 Instructions</h2>
    <ol class="instructions">
      <li>Bring a large pot of salted water to the boil.</li>
      <li>Finely slice the garlic cloves.</li>
      <li>Heat olive oil in a pan and gently fry the garlic until golden.</li>
      <li>Add canned tomatoes and simmer for 15 minutes.</li>
      <li>Cook spaghetti according to package instructions.</li>
      <li>Drain the pasta and toss with the tomato sauce.</li>
      <li>Garnish with fresh basil and grated Parmesan.</li>
    </ol>
  </div>
</body>
</html>
```

**Final output:** A beautiful, professional recipe card with:
- Orange tick-marked ingredients in warm-toned bordered cards
- Red-numbered circular step indicators for instructions
- Clean white card on a cream background with soft shadow

**Reflection Questions:**
1. What would happen if you removed `counter-reset` from `ol.instructions`? Try it and observe.
2. How would you add a hover effect to each instruction step (e.g., slightly darker background)?
3. What would change if you used `list-style-position: inside` on the instructions before adding the custom counter?

**Optional Extension:** Add a third section — "Nutrition Info" — as a `<dl>` (definition list) with `<dt>` (term) and `<dd>` (definition) elements, styled with a two-column layout using CSS.

---

## Common Beginner Mistakes

### Mistake 1: Forgetting to Remove Default `padding-left` on `<ul>`

**Wrong:**
```css
ul {
  list-style-type: none;
  /* forgot padding: 0 */
}
```

**Problem:** The list still has the browser's default `padding-left: 40px`, so items appear indented even though there are no bullets. This catches many beginners off guard.

**Correct:**
```css
ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}
```

Always reset both `padding` and `margin` when removing default list styles.

---

### Mistake 2: Applying `display: inline` Instead of `display: inline-block` for Navigations

**Wrong:**
```css
li {
  display: inline;
  padding: 12px 20px;   /* vertical padding will not work correctly */
}
```

**Problem:** `display: inline` does not honour vertical padding in the same way as `inline-block`. The items will flow horizontally, but the padding will not expand the clickable area vertically.

**Correct:**
```css
li {
  display: inline-block;
  padding: 12px 20px;   /* now works perfectly */
}
```

---

### Mistake 3: Not Adding `display: block` to the `<a>` Inside `<li>`

**Wrong:**
```css
li a {
  color: white;
  padding: 12px 20px;
  /* missing display: block */
}
```

**Problem:** The `<a>` is still an inline element. The padding will not create a full-height clickable area. Only the text itself is clickable, not the surrounding padded space.

**Correct:**
```css
li a {
  display: block;   /* makes the full padded area clickable */
  color: white;
  padding: 12px 20px;
}
```

---

### Mistake 4: Using `list-style-image` and Wondering Why the Image Looks Odd

**Wrong approach (hard to control):**
```css
ul {
  list-style-image: url("icon.png");
}
```

**Problem:** You cannot control the image size or position precisely.

**Better approach:**
```css
ul {
  list-style-type: none;
  padding: 0;
}

li {
  padding-left: 28px;
  background-image: url("icon.png");
  background-repeat: no-repeat;
  background-position: left center;
  background-size: 18px 18px;
}
```

This gives you complete control over image size and alignment.

---

### Mistake 5: Applying `list-style` Shorthand in the Wrong Order

**Wrong:**
```css
ul {
  list-style: inside square;  /* position before type */
}
```

**Problem:** The order matters. The shorthand is `type position image`. While most browsers are forgiving, writing them in an unusual order can cause confusion or unexpected results.

**Correct:**
```css
ul {
  list-style: square inside;  /* type then position */
}
```

---

### Mistake 6: Forgetting `overflow: hidden` on the `<ul>` Navbar

**Wrong:**
```css
ul.navbar {
  background-color: #333;
  /* missing overflow: hidden */
}
ul.navbar li { display: inline-block; }
```

**Problem:** If the list items have a background colour, the parent `<ul>` may not visually contain them (the height collapses). Adding `overflow: hidden` forces the `<ul>` to stretch around its children.

**Correct:**
```css
ul.navbar {
  background-color: #333;
  overflow: hidden;   /* prevents height collapse */
}
```

---

## Reflection Questions

1. What is the difference between `list-style-type: none` and `list-style: none`? Which one removes more?

2. When would you use `list-style-position: inside` versus `outside`? Give a real-world example of each.

3. What is the most commonly used `list-style-type` value for navigation menus? Why?

4. If you want each list item to have a coloured background, do you apply the `background-color` to the `<ul>` or to each `<li>`? Why?

5. Why do you need `display: block` on an `<a>` tag inside a navigation `<li>`? What does it change?

6. What two CSS resets are almost always applied together when removing default list styling? Why are both needed?

7. Why is `background-image` on `<li>` generally better than `list-style-image` for custom bullet icons?

8. What does `counter-reset` do, and why must it be placed on the `<ol>` rather than on the `<li>`?

---

## Completion Checklist

Before moving on, confirm you can do all of the following:

- [ ] I can explain the difference between `<ul>` and `<ol>` and when to use each
- [ ] I can set `list-style-type` to `disc`, `circle`, `square`, and `none`
- [ ] I can set `list-style-type` to `decimal`, `lower-roman`, `upper-roman`, `lower-alpha`, and `upper-alpha`
- [ ] I understand what `list-style-position: inside` and `outside` do and how wrapped text behaves differently
- [ ] I can use the `list-style` shorthand to set type and position in one line
- [ ] I can remove default browser padding and margin from a list
- [ ] I can style `<li>` elements with background colour, padding, border, and border-radius
- [ ] I can use `border-bottom` and `li:last-child` to create a clean separator-style list
- [ ] I can make a horizontal navigation bar from a `<ul>` using `display: inline-block`
- [ ] I understand why `display: block` on `<a>` inside `<li>` is important for click area
- [ ] I can use `background-image` on `<li>` for a custom bullet icon with precise control
- [ ] I can use CSS counters (`counter-reset` and `counter-increment`) with `::before` for custom numbering
- [ ] I know the six most common beginner mistakes when styling lists and how to avoid them

---

## Lesson Summary

In this lesson, you went from the raw HTML basics of `<ul>` and `<ol>` all the way to building professional, design-quality list components with CSS.

You learned that `list-style-type` controls the bullet or numbering marker, supporting types from simple shapes (disc, circle, square) to alphabetic and Roman numeral sequences. You learned that `list-style-position` controls whether the marker sits inside or outside the text content box, affecting how long lines of text wrap. You learned that `list-style-image` can replace a bullet with an image, and that the more powerful technique is using `background-image` on `<li>` for precise control. The shorthand `list-style` lets you set all three in a single clean line.

Beyond the dedicated list properties, you saw how removing default `padding` and `margin`, setting `display: inline-block`, and applying `background-color`, `padding`, and `border` directly to `<li>` elements transforms lists into the building blocks of navigation bars, feature panels, and step-by-step guides.

The mini-project brought everything together into a real-world recipe card — using custom CSS counters with `::before` pseudo-elements to create beautifully styled step indicators that would feel at home on any professional website.

In the next lesson, you will explore **CSS Tables** — how to apply borders, spacing, alignment, and colour to HTML tables to turn raw data grids into polished, readable information displays.

---

*Sources: W3Schools CSS Styling Lists Tutorial (https://www.w3schools.com/css/css_list.asp), CSS List Code Challenges (https://www.w3schools.com/css/css_challenges_list.asp)*
