---
render_with_liquid: false
title: "CSS Website Layout"
nav_order: 45
---

# Lesson 45: CSS Website Layout

---

## Lesson Introduction

Have you ever looked at a professional website and wondered: how did they put the logo at the top, the navigation menu beside it, a sidebar on the left, the main content in the middle, and a footer stretched across the bottom — all perfectly arranged? That arrangement is called a **website layout**, and CSS is the tool that makes it happen.

In this lesson, you will learn how to take a blank web page and organise it into a real, structured layout — just like the websites you use every day. You will understand every single zone of a typical webpage, why each zone exists, how CSS positions and sizes each one, and how to combine them all into one complete working design.

By the end of this lesson you will be able to:
- Identify and name every major section of a standard website layout
- Write CSS to style a full webpage with a header, navigation bar, content area, sidebar, and footer
- Use `float`, `flexbox`, and CSS Grid approaches to arrange sections side by side
- Make layouts responsive so they work on both wide desktop screens and narrow phone screens
- Build a complete personal blog homepage as a mini project

This is one of the most practical and exciting CSS lessons because you are finally assembling all your CSS knowledge into something that looks like a real website.

---

## Prerequisite Concepts

Before you begin, make sure you are comfortable with these foundational ideas. Read through each one — they will be used constantly throughout this lesson.

### What Is an HTML Element?

An HTML element is a piece of content wrapped in a tag. For example:
```html
<div>This is a block of content</div>
<p>This is a paragraph</p>
<header>This is a header section</header>
```

### What Is a Block-Level Element?

A **block-level element** automatically takes up the full width of its parent container and starts on a new line. Examples: `<div>`, `<p>`, `<header>`, `<nav>`, `<section>`, `<footer>`, `<h1>`.

### What Is the CSS Box Model?

Every HTML element is a box. The box has:
- **Content** — the actual text or image inside
- **Padding** — space between the content and the border
- **Border** — a line around the padding
- **Margin** — space outside the border, pushing other elements away

```css
div {
  width: 300px;
  padding: 20px;
  border: 2px solid black;
  margin: 10px;
}
```

### What Is `width` and `height`?

`width` sets how wide an element is. `height` sets how tall it is. You can use `px` (fixed pixels) or `%` (percentage of the parent's width).

### What Is `float`?

`float` moves an element to the left or right of its container, letting other content flow around it — like how text wraps around a photo in a magazine.

### What Is Flexbox?

Flexbox is a CSS layout system that places child elements in a row or column automatically, with powerful alignment controls. You activate it with `display: flex` on the parent element.

### What Is CSS Grid?

CSS Grid is a two-dimensional layout system. It lets you define rows AND columns simultaneously, creating grid-like structures. You activate it with `display: grid` on the parent element.

### What Is a Media Query?

A media query checks the size of the screen and applies different CSS rules depending on the result:
```css
@media (max-width: 768px) {
  /* CSS rules for screens 768px wide or narrower */
}
```

---

## Part 1: Understanding the Anatomy of a Website Layout

### What Does "Website Layout" Mean?

A website layout is the organised structure of all the visual zones on a webpage. Think of building a house: before you put up walls and furniture, you draw a floor plan showing which room goes where. A website layout is the floor plan of your webpage.

Almost every website in the world — news sites, social media platforms, government pages, online stores — follows a similar layout blueprint with these major zones:

```
┌─────────────────────────────────────┐
│              HEADER                 │  ← logo, site name
├─────────────────────────────────────┤
│            NAVIGATION BAR           │  ← links menu
├──────────────────────┬──────────────┤
│                      │              │
│    MAIN CONTENT      │   SIDEBAR    │  ← article + extras
│                      │              │
├─────────────────────────────────────┤
│               FOOTER                │  ← copyright, links
└─────────────────────────────────────┘
```

Let's understand each zone before writing any code.

### Zone 1 — The Header

The **header** sits at the very top of the page. It typically contains:
- The website logo or brand name
- A tagline or subtitle
- Sometimes a search bar

> 💡 **Real-world analogy:** The header is like the front cover of a magazine — it identifies what you are reading immediately.

The HTML element for this is `<header>`.

### Zone 2 — The Navigation Bar (Navbar)

The **navbar** contains a list of links — Home, About, Blog, Contact, etc. It can be:
- Horizontal (sitting below the header, spanning full width)
- Vertical (running down the left side of the page as a sidebar)
- Sticky (staying fixed at the top as you scroll)

The HTML element for this is `<nav>`.

### Zone 3 — The Main Content Area

The **main content** area is the largest zone — it is where the actual articles, products, forms, or page content lives. This is what users came to your site to read.

The HTML element for this is `<main>` or a `<section>`.

### Zone 4 — The Sidebar

The **sidebar** is a narrower column beside the main content. It often contains:
- Related articles
- Advertisements
- A category list
- A search widget
- A social media feed

The HTML element is typically `<aside>`.

### Zone 5 — The Footer

The **footer** sits at the very bottom of the page. It typically contains:
- Copyright notice
- Secondary links (Privacy Policy, Terms of Service)
- Contact information
- Social media icons

The HTML element for this is `<footer>`.

---

## Part 2: Setting Up the HTML Structure

Before writing any CSS, you always need the HTML skeleton. This is the foundation every CSS layout rule will be built on.

### The Complete HTML Skeleton

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Website</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- Zone 1: Header -->
  <header class="site-header">
    <h1>My Awesome Website</h1>
    <p>Welcome to my little corner of the internet</p>
  </header>

  <!-- Zone 2: Navigation Bar -->
  <nav class="navbar">
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">About</a></li>
      <li><a href="#">Blog</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  </nav>

  <!-- Zone 3 + 4: Content and Sidebar wrapper -->
  <div class="content-wrapper">

    <!-- Zone 3: Main Content -->
    <main class="main-content">
      <h2>Latest Articles</h2>
      <p>This is where your main page content goes. Articles, images, videos, and more all live here in the main content area.</p>
      <p>You can have multiple paragraphs, sections, and subsections here.</p>
    </main>

    <!-- Zone 4: Sidebar -->
    <aside class="sidebar">
      <h3>Categories</h3>
      <ul>
        <li><a href="#">Technology</a></li>
        <li><a href="#">Design</a></li>
        <li><a href="#">Science</a></li>
        <li><a href="#">Travel</a></li>
      </ul>
    </aside>

  </div><!-- end content-wrapper -->

  <!-- Zone 5: Footer -->
  <footer class="site-footer">
    <p>&copy; 2026 My Awesome Website. All rights reserved.</p>
  </footer>

</body>
</html>
```

**Line-by-line breakdown of important parts:**

- `<meta name="viewport" content="width=device-width, initial-scale=1.0">` — this tells mobile browsers to display the page at the correct width. Without this, your layout will look tiny on phones.
- `<link rel="stylesheet" href="style.css">` — connects your CSS file to the HTML.
- `class="site-header"` — gives this element a class name so CSS can target it.
- `<div class="content-wrapper">` — wraps the main content and sidebar together. This wrapper is what you will make into a two-column layout.
- `&copy;` — the HTML code for the © copyright symbol.

**Milestone output (no CSS yet):** A plain unstyled page where all five zones stack vertically one after another — a tall single column of text. This is correct! CSS will arrange them properly.

---

## Part 3: Styling Each Zone — Step by Step

Now let's style each zone individually before combining them.

### Step 1 — The Universal Reset

Before styling anything, add a reset to ensure consistent behaviour across all browsers:

```css
/* style.css */

/* === RESET === */
* {
  box-sizing: border-box;  /* padding and border are included IN the width */
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 16px;
  line-height: 1.6;
  color: #333333;
  background-color: #f0f0f0;
}
```

**Why `box-sizing: border-box`?**

Without it, adding padding to a `300px` wide element makes it wider than `300px`, because the padding is added *outside* the specified width. With `border-box`, the padding is included *inside* the `300px`, so the element stays exactly `300px`. This prevents many confusing layout bugs.

> 🤔 **Thinking prompt:** What happens if you forget `box-sizing: border-box` on a sidebar that is supposed to be exactly `25%` wide? Try removing it and see if it overflows.

---

### Step 2 — The Header

```css
/* === HEADER === */
.site-header {
  background-color: #2c3e50;   /* dark blue-grey background */
  color: #ffffff;               /* white text */
  padding: 30px 20px;           /* 30px top/bottom, 20px left/right */
  text-align: center;
}

.site-header h1 {
  font-size: 2.5rem;
  margin-bottom: 8px;
}

.site-header p {
  font-size: 1rem;
  color: #bdc3c7;               /* slightly dimmed subtitle text */
}
```

**Expected output:** A wide, dark blue-grey banner stretched across the full top of the page. Inside it, a large white site title and a smaller grey subtitle, all centred.

**Understanding each line:**
- `background-color: #2c3e50` — sets a rich dark background. The header will stand out strongly.
- `padding: 30px 20px` — shorthand for: `padding-top: 30px; padding-right: 20px; padding-bottom: 30px; padding-left: 20px`.
- `color: #ffffff` — sets text colour to white. This applies to all text inside `.site-header` unless overridden.
- `.site-header h1` — this is a **descendant selector** — it targets only `<h1>` elements that are inside `.site-header`.

---

### Step 3 — The Navigation Bar

```css
/* === NAVBAR === */
.navbar {
  background-color: #34495e;   /* slightly lighter than header */
  overflow: hidden;             /* contains floated children */
}

.navbar ul {
  list-style: none;             /* removes bullet points */
  display: flex;                /* arranges links in a row */
  padding: 0;
  margin: 0;
}

.navbar ul li a {
  display: block;               /* makes the entire cell clickable */
  color: #ecf0f1;               /* off-white link colour */
  text-decoration: none;        /* removes underline */
  padding: 14px 20px;           /* comfortable click area */
  font-size: 1rem;
  transition: background-color 0.2s ease;  /* smooth hover effect */
}

.navbar ul li a:hover {
  background-color: #2c3e50;   /* darkens on hover */
  color: #ffffff;
}
```

**Expected output:** A horizontal dark bar below the header, containing four links in a row: Home | About | Blog | Contact. Each link has padding making it a comfortable size to click. Hovering over a link darkens it.

**Understanding each line:**
- `list-style: none` — removes the bullet points (•) from the `<ul>`.
- `display: flex` on the `<ul>` — turns the list into a horizontal flex container, so all `<li>` items sit side by side in a row instead of stacking vertically.
- `display: block` on the `<a>` — makes the link fill its entire `<li>` cell, so users can click anywhere in the cell, not just on the text.
- `transition: background-color 0.2s ease` — animates the background colour change over 0.2 seconds when hovering.

---

### Step 4 — The Two-Column Content Layout

This is the most important part: making the main content and sidebar sit **side by side** in two columns.

There are three approaches taught across web development:

**Approach A — Using Float (Classic Method)**

```css
/* === CONTENT WRAPPER (float approach) === */
.content-wrapper {
  overflow: hidden;            /* clearfix: collapses around floated children */
  max-width: 1100px;           /* prevents content spreading too wide */
  margin: 20px auto;           /* centres the wrapper on the page */
  padding: 0 20px;
}

.main-content {
  float: left;                 /* float to the LEFT */
  width: 70%;                  /* takes up 70% of the wrapper */
  background-color: #ffffff;
  padding: 25px;
  min-height: 400px;
}

.sidebar {
  float: right;                /* float to the RIGHT */
  width: 28%;                  /* takes up 28% (2% gap between them) */
  background-color: #ffffff;
  padding: 20px;
  min-height: 400px;
}
```

**Expected output:** Main content takes up about 70% of the page width on the left. Sidebar takes up about 28% on the right. A 2% visual gap separates them. Both columns sit at the same height.

**Understanding floats:**
- `float: left` pulls the element to the left and lets content flow to its right.
- `float: right` pulls it to the right and lets content flow to its left.
- Together, the two floated elements sit beside each other.
- `overflow: hidden` on the parent is a **clearfix technique** — without it, the parent collapses to zero height because floated elements are taken out of the normal document flow.

> 🤔 **What if you remove `overflow: hidden` from `.content-wrapper`?** The footer will slide up and overlap the content — because the parent doesn't know how tall its floated children are.

---

**Approach B — Using Flexbox (Modern Recommended Method)**

Flexbox is the modern standard. It is simpler, more powerful, and avoids the clearfix problem entirely.

```css
/* === CONTENT WRAPPER (flexbox approach) === */
.content-wrapper {
  display: flex;               /* activates flexbox */
  flex-direction: row;         /* children go in a row (left to right) */
  gap: 20px;                   /* 20px gap between main content and sidebar */
  max-width: 1100px;
  margin: 20px auto;
  padding: 0 20px;
}

.main-content {
  flex: 3;                     /* takes 3 parts of available space */
  background-color: #ffffff;
  padding: 25px;
  min-height: 400px;
}

.sidebar {
  flex: 1;                     /* takes 1 part of available space */
  background-color: #ffffff;
  padding: 20px;
  min-height: 400px;
}
```

**Understanding `flex: 3` and `flex: 1`:**
- These are **flex grow values**. They define the ratio of space each child gets.
- `flex: 3` means: give this element 3 units of the available space.
- `flex: 1` means: give this element 1 unit of the available space.
- Together: 3 + 1 = 4 total units. Main content gets 3/4 (75%) of the space. Sidebar gets 1/4 (25%).
- `gap: 20px` automatically creates a 20px space between the children.

> 💡 **Analogy:** Imagine a pizza cut into 4 slices. With `flex: 3` and `flex: 1`, main content gets 3 slices and the sidebar gets 1 slice. The pizza is shared in a 3:1 ratio.

---

**Approach C — Using CSS Grid (Most Powerful Method)**

```css
/* === CONTENT WRAPPER (CSS Grid approach) === */
.content-wrapper {
  display: grid;
  grid-template-columns: 3fr 1fr;  /* two columns: 3 parts and 1 part */
  gap: 20px;
  max-width: 1100px;
  margin: 20px auto;
  padding: 0 20px;
}

.main-content {
  background-color: #ffffff;
  padding: 25px;
  min-height: 400px;
}

.sidebar {
  background-color: #ffffff;
  padding: 20px;
  min-height: 400px;
}
```

**Understanding `grid-template-columns: 3fr 1fr`:**
- `fr` stands for **fraction unit** — it divides the available space into fractions.
- `3fr 1fr` creates two columns: the first gets 3 fractions, the second gets 1 fraction — a 75%/25% split.
- The first child (`.main-content`) automatically goes in column 1. The second child (`.sidebar`) automatically goes in column 2.
- `gap: 20px` creates space between the grid cells.

For the rest of this lesson we will use the **Flexbox approach** as it is the most widely used modern method.

---

### Step 5 — Styling the Main Content Area

```css
/* === MAIN CONTENT === */
.main-content {
  flex: 3;
  background-color: #ffffff;
  padding: 30px;
  border-radius: 6px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
}

.main-content h2 {
  font-size: 1.8rem;
  color: #2c3e50;
  margin-bottom: 15px;
  border-bottom: 3px solid #3498db;   /* a coloured underline */
  padding-bottom: 10px;
}

.main-content p {
  color: #555555;
  margin-bottom: 15px;
  line-height: 1.7;
}
```

**Expected output:** A white card with a light drop shadow. Inside it, a heading with a blue underline, followed by readable paragraphs with comfortable spacing.

**Understanding each new property:**
- `border-radius: 6px` — rounds the corners of the white card slightly.
- `box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08)` — adds a subtle shadow beneath the card.
  - `0` = no horizontal shadow offset
  - `2px` = 2px downward vertical offset
  - `6px` = blur radius (how soft the shadow is)
  - `rgba(0, 0, 0, 0.08)` = very faint black (8% opacity)
- `border-bottom: 3px solid #3498db` — draws a 3px thick solid blue line only at the bottom of the `<h2>`.

---

### Step 6 — Styling the Sidebar

```css
/* === SIDEBAR === */
.sidebar {
  flex: 1;
  background-color: #ffffff;
  padding: 20px;
  border-radius: 6px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
  align-self: flex-start;     /* prevents sidebar from stretching to match content height */
}

.sidebar h3 {
  font-size: 1.1rem;
  color: #2c3e50;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 15px;
  border-bottom: 2px solid #ecf0f1;
  padding-bottom: 8px;
}

.sidebar ul {
  list-style: none;
}

.sidebar ul li {
  margin-bottom: 8px;
}

.sidebar ul li a {
  text-decoration: none;
  color: #3498db;
  font-size: 0.95rem;
  transition: color 0.2s ease;
}

.sidebar ul li a:hover {
  color: #2c3e50;
}
```

**Expected output:** A narrower white card on the right. Inside, a bold "CATEGORIES" heading (in small caps style) and a list of blue links that darken on hover.

**Understanding new properties:**
- `align-self: flex-start` — in a flexbox row, by default all children stretch to the same height as the tallest sibling. `align-self: flex-start` tells the sidebar to only be as tall as its own content, not stretch to match the main content column.
- `text-transform: uppercase` — converts the heading text to ALL CAPITALS in CSS (the HTML text stays unchanged).
- `letter-spacing: 1px` — adds 1px of space between each letter, creating a spread-out uppercase look.

---

### Step 7 — The Footer

```css
/* === FOOTER === */
.site-footer {
  background-color: #2c3e50;
  color: #bdc3c7;
  text-align: center;
  padding: 25px 20px;
  margin-top: 20px;
  font-size: 0.9rem;
}

.site-footer a {
  color: #3498db;
  text-decoration: none;
}

.site-footer a:hover {
  text-decoration: underline;
}
```

**Expected output:** A dark footer at the bottom of the page matching the header's colour scheme, with centred copyright text in a muted grey colour.

---

## Part 4: Putting the Complete CSS Together

Here is the full `style.css` with all zones styled, using the Flexbox approach:

```css
/* ============================================================
   COMPLETE WEBSITE LAYOUT — style.css
   ============================================================ */

/* === RESET === */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

/* === BODY === */
body {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 16px;
  line-height: 1.6;
  color: #333333;
  background-color: #f0f0f0;
}

/* === HEADER === */
.site-header {
  background-color: #2c3e50;
  color: #ffffff;
  padding: 30px 20px;
  text-align: center;
}

.site-header h1 {
  font-size: 2.5rem;
  margin-bottom: 8px;
}

.site-header p {
  font-size: 1rem;
  color: #bdc3c7;
}

/* === NAVBAR === */
.navbar {
  background-color: #34495e;
}

.navbar ul {
  list-style: none;
  display: flex;
  padding: 0;
  margin: 0;
}

.navbar ul li a {
  display: block;
  color: #ecf0f1;
  text-decoration: none;
  padding: 14px 20px;
  font-size: 1rem;
  transition: background-color 0.2s ease;
}

.navbar ul li a:hover {
  background-color: #2c3e50;
  color: #ffffff;
}

/* === CONTENT WRAPPER (Flexbox) === */
.content-wrapper {
  display: flex;
  flex-direction: row;
  gap: 20px;
  max-width: 1100px;
  margin: 20px auto;
  padding: 0 20px;
}

/* === MAIN CONTENT === */
.main-content {
  flex: 3;
  background-color: #ffffff;
  padding: 30px;
  border-radius: 6px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
}

.main-content h2 {
  font-size: 1.8rem;
  color: #2c3e50;
  margin-bottom: 15px;
  border-bottom: 3px solid #3498db;
  padding-bottom: 10px;
}

.main-content p {
  color: #555555;
  margin-bottom: 15px;
  line-height: 1.7;
}

/* === SIDEBAR === */
.sidebar {
  flex: 1;
  background-color: #ffffff;
  padding: 20px;
  border-radius: 6px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
  align-self: flex-start;
}

.sidebar h3 {
  font-size: 1.1rem;
  color: #2c3e50;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 15px;
  border-bottom: 2px solid #ecf0f1;
  padding-bottom: 8px;
}

.sidebar ul {
  list-style: none;
}

.sidebar ul li {
  margin-bottom: 8px;
}

.sidebar ul li a {
  text-decoration: none;
  color: #3498db;
  font-size: 0.95rem;
  transition: color 0.2s ease;
}

.sidebar ul li a:hover {
  color: #2c3e50;
}

/* === FOOTER === */
.site-footer {
  background-color: #2c3e50;
  color: #bdc3c7;
  text-align: center;
  padding: 25px 20px;
  margin-top: 20px;
  font-size: 0.9rem;
}

.site-footer a {
  color: #3498db;
  text-decoration: none;
}

.site-footer a:hover {
  text-decoration: underline;
}
```

**Full expected output:** A complete webpage with a dark blue header, dark horizontal navigation bar with hoverable links, two-column content area (70% main / 25% sidebar), and a matching dark footer. The content area is centred on the page with a max-width, sitting on a light grey background.

---

## Part 5: Making the Layout Responsive

### What Is Responsive Design?

A **responsive** layout adjusts itself to look good on different screen sizes. A layout that works on a wide desktop screen but looks broken on a narrow phone screen is not responsive.

On a phone, a two-column layout is too narrow — both columns become tiny slivers of content. The solution is to **stack the columns vertically** on small screens.

### Using Media Queries

A **media query** is CSS code that only applies when a specific condition is true — in this case, when the screen is narrower than a certain width.

```css
/* === RESPONSIVE LAYOUT === */

/* Tablets and smaller screens (768px wide or less) */
@media (max-width: 768px) {

  /* Stack columns vertically instead of side by side */
  .content-wrapper {
    flex-direction: column;    /* change from row to column */
  }

  /* Both sections now take full width */
  .main-content,
  .sidebar {
    flex: none;                /* remove flex ratio */
    width: 100%;               /* take full width */
  }

  /* Stack navbar links vertically */
  .navbar ul {
    flex-direction: column;    /* stack links vertically */
  }

  /* Make header text a bit smaller on phones */
  .site-header h1 {
    font-size: 1.8rem;
  }
}

/* Very small phones (480px wide or less) */
@media (max-width: 480px) {
  .site-header {
    padding: 20px 15px;
  }

  .main-content,
  .sidebar {
    padding: 15px;
  }

  .navbar ul li a {
    padding: 12px 15px;
  }
}
```

**Expected output on a phone (screen ≤ 768px):**
- The header still spans the full width with slightly smaller text.
- Navbar links stack vertically — each link on its own row.
- The main content area takes full width on top.
- The sidebar sits below it, also full width.
- No horizontal scrolling needed.

**Expected output on a tablet/desktop (screen > 768px):**
- The original two-column layout is shown — main content left, sidebar right.
- Navbar links are horizontal.

> 🤔 **Thinking prompt:** Why do we put the responsive rules AFTER the main CSS? Because CSS cascades — later rules override earlier ones when conditions are met. The mobile styles override the desktop styles when the screen is narrow.

---

## Part 6: Layout Variations

The basic layout we built is just one pattern. Real websites use many variations. Let's look at the most common ones.

### Variation 1 — No Sidebar (Full-Width Content)

Sometimes a page doesn't need a sidebar — for example, a blog post page that focuses entirely on reading.

```css
/* No sidebar — content takes full width */
.content-wrapper-full {
  display: flex;
  max-width: 800px;       /* narrower max-width for better readability */
  margin: 30px auto;
  padding: 0 20px;
}

.main-content-full {
  flex: 1;                /* single column takes all available space */
  background-color: #ffffff;
  padding: 40px;
  border-radius: 6px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
}
```

**Expected output:** A single centred white content card that is narrower than the viewport, with comfortable reading width.

### Variation 2 — Left Sidebar Instead of Right

The sidebar can also appear on the LEFT side of the content. In Flexbox, you control order with the HTML order of elements — the first element in HTML is on the left.

Simply swap the HTML order:

```html
<!-- Sidebar first in HTML = sidebar on the LEFT -->
<div class="content-wrapper">
  <aside class="sidebar">...</aside>    <!-- this comes first → LEFT column -->
  <main class="main-content">...</main> <!-- this comes second → RIGHT column -->
</div>
```

Or keep the HTML order and use CSS `order`:

```css
/* Force sidebar to appear first (left) regardless of HTML order */
.sidebar {
  order: -1;    /* -1 means "go before everything else" */
}
```

### Variation 3 — Three-Column Layout

For complex pages like dashboards, you might need three columns.

```css
.three-column-wrapper {
  display: flex;
  gap: 20px;
  max-width: 1200px;
  margin: 20px auto;
  padding: 0 20px;
}

.left-sidebar  { flex: 1; background: #fff; padding: 20px; }
.center-content { flex: 3; background: #fff; padding: 25px; }
.right-sidebar { flex: 1; background: #fff; padding: 20px; }
```

```html
<div class="three-column-wrapper">
  <aside class="left-sidebar">Left nav</aside>
  <main class="center-content">Main content</main>
  <aside class="right-sidebar">Right widgets</aside>
</div>
```

**Expected output:** Three columns in a 1:3:1 ratio. The centre is the widest (main content), flanked by two equal narrow sidebars.

### Variation 4 — Sticky Header (Fixed Navigation)

A **sticky header** stays visible at the top of the screen as the user scrolls down — very useful for navigation.

```css
.navbar {
  background-color: #34495e;
  position: sticky;    /* stays in place as you scroll */
  top: 0;              /* stuck to the very top of the viewport */
  z-index: 100;        /* sits on top of all other page content */
}
```

**Understanding these properties:**
- `position: sticky` — the element behaves normally until it would scroll off screen, then it "sticks" at the specified offset.
- `top: 0` — the sticking position is 0px from the top of the viewport.
- `z-index: 100` — ensures the navbar visually floats above any page content that would scroll underneath it.

### Variation 5 — Hero Section

A **hero section** is a large, visually striking banner at the top of a homepage — often with a background image, a large headline, and a call-to-action button.

```html
<section class="hero">
  <div class="hero-content">
    <h1>Build Something Amazing</h1>
    <p>Start your coding journey today with our beginner-friendly courses.</p>
    <a href="#" class="hero-btn">Get Started</a>
  </div>
</section>
```

```css
.hero {
  background-color: #1a252f;
  background-image: linear-gradient(135deg, #1a252f 0%, #2c3e50 50%, #3498db 100%);
  color: #ffffff;
  padding: 100px 20px;
  text-align: center;
}

.hero h1 {
  font-size: 3rem;
  margin-bottom: 20px;
  line-height: 1.2;
}

.hero p {
  font-size: 1.2rem;
  color: #bdc3c7;
  max-width: 600px;
  margin: 0 auto 30px;
}

.hero-btn {
  display: inline-block;
  background-color: #3498db;
  color: #ffffff;
  padding: 14px 32px;
  font-size: 1.1rem;
  text-decoration: none;
  border-radius: 4px;
  font-weight: bold;
  transition: background-color 0.2s ease;
}

.hero-btn:hover {
  background-color: #2980b9;
}
```

**Expected output:** A tall, dramatic banner with a dark gradient background transitioning from dark blue-grey to bright blue. Inside, a huge white headline, a short subtitle paragraph, and a bright blue button. Hovering the button darkens it slightly.

**Understanding `linear-gradient`:**
- `linear-gradient(135deg, #1a252f, #2c3e50, #3498db)` creates a smooth colour transition at a 135-degree diagonal angle.
- The first colour is in the top-left, the last is in the bottom-right.

---

## Part 7: The Role of `max-width` and Centring

### Why `max-width` Matters

Without a `max-width`, content stretches to fill the entire browser window. On a very wide monitor (1920px+), text lines become so long they are exhausting to read — your eyes have to travel all the way across the screen. A `max-width` limits how wide content can grow.

```css
/* Without max-width — content spreads across entire screen */
.content-wrapper {
  display: flex;
  padding: 0 20px;
}

/* With max-width — content has a comfortable maximum width */
.content-wrapper {
  display: flex;
  max-width: 1100px;   /* never wider than 1100px */
  margin: 0 auto;      /* centres the wrapper horizontally */
  padding: 0 20px;
}
```

**Understanding `margin: 0 auto`:**
- `margin: 0 auto` means: `margin-top: 0; margin-bottom: 0; margin-left: auto; margin-right: auto`.
- `auto` on both left and right tells the browser to distribute the remaining space equally — which centres the element.
- This only works when the element has a defined `width` or `max-width`.

> 💡 **Analogy:** Think of it like centering a book on a desk. The book (content) has a fixed width. Placing equal margins on both sides (equal amounts of desk space on left and right) centres the book on the desk.

---

## Guided Practice Exercises

### Exercise 1 — Build a Two-Column News Layout

**Objective:** Create a news website layout with a wide main content area and a narrow sidebar.

**Scenario:** You are building a technology news website called "TechDaily."

**HTML to use:**
```html
<header class="site-header">
  <h1>TechDaily</h1>
  <p>Your source for the latest in technology</p>
</header>

<nav class="navbar">
  <ul>
    <li><a href="#">Home</a></li>
    <li><a href="#">AI</a></li>
    <li><a href="#">Gadgets</a></li>
    <li><a href="#">Science</a></li>
    <li><a href="#">Business</a></li>
  </ul>
</nav>

<div class="content-wrapper">
  <main class="main-content">
    <h2>Breaking: New AI Model Surpasses Human Performance</h2>
    <p>Researchers at a leading AI laboratory have announced a breakthrough model that demonstrates superhuman performance on a wide range of reasoning and problem-solving tasks.</p>
    <p>The model was trained on a massive dataset and uses a novel architecture that significantly improves efficiency compared to previous generations.</p>

    <h2>Smartphone Sales Hit Record High in Q1 2026</h2>
    <p>Global smartphone shipments reached an all-time high in the first quarter of 2026, driven by strong demand in emerging markets and a new wave of foldable devices.</p>
  </main>

  <aside class="sidebar">
    <h3>Trending Topics</h3>
    <ul>
      <li><a href="#">Artificial Intelligence</a></li>
      <li><a href="#">Electric Vehicles</a></li>
      <li><a href="#">Space Exploration</a></li>
      <li><a href="#">Quantum Computing</a></li>
    </ul>

    <h3 style="margin-top: 20px;">Newsletter</h3>
    <p style="font-size: 0.9rem; color: #666;">Get the latest tech news delivered to your inbox every morning.</p>
  </aside>
</div>

<footer class="site-footer">
  <p>&copy; 2026 TechDaily. All rights reserved.</p>
</footer>
```

**Steps:**
1. Apply the complete CSS from Part 4 of this lesson.
2. Change the header background to a deep red (`#c0392b`) and the navbar to a slightly lighter red (`#e74c3c`).
3. Change the `border-bottom` on main content headings to red (`#c0392b`).
4. Add the responsive media query from Part 5.

**Expected output:** A professional-looking red-themed tech news site with a two-column layout that collapses to single column on mobile.

**Self-check questions:**
- On a desktop, is the main content wider than the sidebar?
- On a narrow window (less than 768px), do the columns stack vertically?
- Does hovering over navbar links show a visual colour change?

---

### Exercise 2 — Add a Hero Section

**Objective:** Add a hero section between the navbar and the content area.

**Scenario:** Your news site needs a featured story hero at the top.

**HTML to add (insert between `</nav>` and `<div class="content-wrapper">`):**
```html
<section class="hero">
  <div class="hero-content">
    <h2>Featured: The Future of Renewable Energy</h2>
    <p>An in-depth look at how solar, wind, and hydrogen technologies are reshaping global energy markets in 2026.</p>
    <a href="#" class="hero-btn">Read Full Story</a>
  </div>
</section>
```

**CSS to add:**
```css
.hero {
  background-image: linear-gradient(135deg, #c0392b, #8e44ad);
  color: #ffffff;
  padding: 80px 20px;
  text-align: center;
}

.hero h2 {
  font-size: 2.2rem;
  margin-bottom: 16px;
}

.hero p {
  font-size: 1.1rem;
  max-width: 600px;
  margin: 0 auto 25px;
  color: rgba(255, 255, 255, 0.85);
}

.hero-btn {
  display: inline-block;
  background-color: #ffffff;
  color: #c0392b;
  padding: 12px 28px;
  font-weight: bold;
  text-decoration: none;
  border-radius: 4px;
  transition: background-color 0.2s ease, color 0.2s ease;
}

.hero-btn:hover {
  background-color: #c0392b;
  color: #ffffff;
}
```

**Expected output:** A dramatic red-to-purple gradient banner below the navbar, with a large headline, short description, and a white button that inverts colours on hover.

**Self-check questions:**
- Does the gradient flow diagonally?
- Does the button invert its colours when hovered?
- Is the description text narrower than the full hero width?

---

### Exercise 3 — Make the Footer Multi-Column

**Objective:** Transform the footer into a three-column layout with links, social media, and a tagline.

**New HTML for footer:**
```html
<footer class="site-footer">
  <div class="footer-inner">
    <div class="footer-col">
      <h4>TechDaily</h4>
      <p>Your trusted source for technology news since 2015.</p>
    </div>
    <div class="footer-col">
      <h4>Quick Links</h4>
      <ul>
        <li><a href="#">About Us</a></li>
        <li><a href="#">Contact</a></li>
        <li><a href="#">Privacy Policy</a></li>
        <li><a href="#">Terms of Service</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h4>Follow Us</h4>
      <ul>
        <li><a href="#">Twitter / X</a></li>
        <li><a href="#">LinkedIn</a></li>
        <li><a href="#">YouTube</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <p>&copy; 2026 TechDaily. All rights reserved.</p>
  </div>
</footer>
```

**CSS for multi-column footer:**
```css
.site-footer {
  background-color: #1a252f;
  color: #bdc3c7;
  margin-top: 30px;
  padding-bottom: 0;
}

.footer-inner {
  display: flex;
  gap: 40px;
  max-width: 1100px;
  margin: 0 auto;
  padding: 40px 20px;
}

.footer-col {
  flex: 1;
}

.footer-col h4 {
  color: #ffffff;
  font-size: 1rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 15px;
  border-bottom: 2px solid #2c3e50;
  padding-bottom: 8px;
}

.footer-col p {
  font-size: 0.9rem;
  line-height: 1.7;
}

.footer-col ul {
  list-style: none;
}

.footer-col ul li {
  margin-bottom: 8px;
}

.footer-col ul li a {
  color: #95a5a6;
  text-decoration: none;
  font-size: 0.9rem;
  transition: color 0.2s ease;
}

.footer-col ul li a:hover {
  color: #ffffff;
}

.footer-bottom {
  background-color: #111a22;
  text-align: center;
  padding: 15px 20px;
  font-size: 0.85rem;
  color: #7f8c8d;
}

/* Responsive footer */
@media (max-width: 768px) {
  .footer-inner {
    flex-direction: column;
    gap: 25px;
  }
}
```

**Expected output:** A rich dark footer with three equal columns. Left: site description. Middle: quick links. Right: social links. Below that, a very dark strip with the copyright line. On mobile, the three columns stack vertically.

---

## Mini Project: Personal Blog Homepage

### Project Description

Build a complete personal blog homepage from scratch. This project combines everything learned in this lesson into one polished, professional design.

**Design brief:**
- Your blog is called "The Curious Mind"
- Colour scheme: warm teal (`#16a085`) and dark charcoal (`#2c3e50`)
- Two-column layout: blog posts on the left (75%), sidebar on the right (25%)
- Include a hero section, sticky navbar, three-column footer
- Fully responsive

---

### Stage 1 — HTML Structure

Create `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>The Curious Mind — A Personal Blog</title>
  <link rel="stylesheet" href="blog.css">
</head>
<body>

  <!-- HEADER -->
  <header class="site-header">
    <div class="header-inner">
      <h1>The Curious Mind</h1>
      <p>Exploring ideas at the intersection of science, technology, and everyday life</p>
    </div>
  </header>

  <!-- NAVBAR (sticky) -->
  <nav class="navbar">
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">Science</a></li>
      <li><a href="#">Technology</a></li>
      <li><a href="#">Philosophy</a></li>
      <li><a href="#">About</a></li>
    </ul>
  </nav>

  <!-- HERO -->
  <section class="hero">
    <div class="hero-content">
      <span class="hero-label">Featured Article</span>
      <h2>Why Curiosity Is the Most Important Skill of the 21st Century</h2>
      <p>In an age of artificial intelligence and rapid change, the ability to ask good questions may matter more than knowing the answers.</p>
      <a href="#" class="hero-btn">Read Article</a>
    </div>
  </section>

  <!-- MAIN CONTENT + SIDEBAR -->
  <div class="content-wrapper">

    <main class="main-content">
      <h2 class="section-title">Recent Posts</h2>

      <!-- Blog Post 1 -->
      <article class="blog-post">
        <span class="post-category">Science</span>
        <h3 class="post-title"><a href="#">The Hidden World of Mycorrhizal Networks</a></h3>
        <div class="post-meta">
          <span>By Amara Osei</span>
          <span class="meta-divider">·</span>
          <span>April 18, 2026</span>
          <span class="meta-divider">·</span>
          <span>6 min read</span>
        </div>
        <p class="post-excerpt">Beneath every forest floor lies an extraordinary network of fungal threads connecting trees and plants in a communication system scientists are only beginning to understand...</p>
        <a href="#" class="read-more">Read More →</a>
      </article>

      <!-- Blog Post 2 -->
      <article class="blog-post">
        <span class="post-category">Technology</span>
        <h3 class="post-title"><a href="#">What I Learned Building My First Mechanical Keyboard</a></h3>
        <div class="post-meta">
          <span>By Amara Osei</span>
          <span class="meta-divider">·</span>
          <span>April 10, 2026</span>
          <span class="meta-divider">·</span>
          <span>8 min read</span>
        </div>
        <p class="post-excerpt">Building a mechanical keyboard from scratch turned out to be one of the most satisfying weekend projects I've ever attempted — and also one of the most unexpectedly educational...</p>
        <a href="#" class="read-more">Read More →</a>
      </article>

      <!-- Blog Post 3 -->
      <article class="blog-post">
        <span class="post-category">Philosophy</span>
        <h3 class="post-title"><a href="#">The Stoic Approach to Dealing with Uncertainty</a></h3>
        <div class="post-meta">
          <span>By Amara Osei</span>
          <span class="meta-divider">·</span>
          <span>March 30, 2026</span>
          <span class="meta-divider">·</span>
          <span>5 min read</span>
        </div>
        <p class="post-excerpt">Ancient Stoic philosophy offers surprisingly practical tools for navigating a world of constant change and unpredictability — wisdom that feels more relevant than ever...</p>
        <a href="#" class="read-more">Read More →</a>
      </article>
    </main>

    <!-- SIDEBAR -->
    <aside class="sidebar">
      <div class="sidebar-widget">
        <h3>About Me</h3>
        <div class="author-bio">
          <div class="author-avatar">AM</div>
          <p>Hi! I'm Amara — a writer, tinkerer, and lifelong student of everything fascinating about the world.</p>
        </div>
      </div>

      <div class="sidebar-widget">
        <h3>Categories</h3>
        <ul class="category-list">
          <li><a href="#">Science <span>(12)</span></a></li>
          <li><a href="#">Technology <span>(8)</span></a></li>
          <li><a href="#">Philosophy <span>(6)</span></a></li>
          <li><a href="#">Travel <span>(4)</span></a></li>
        </ul>
      </div>

      <div class="sidebar-widget">
        <h3>Newsletter</h3>
        <p class="widget-text">New posts every Thursday. No spam, ever.</p>
        <input type="email" class="widget-input" placeholder="your@email.com">
        <button class="widget-btn">Subscribe</button>
      </div>
    </aside>

  </div><!-- end content-wrapper -->

  <!-- FOOTER -->
  <footer class="site-footer">
    <div class="footer-inner">
      <div class="footer-col">
        <h4>The Curious Mind</h4>
        <p>Independent writing about science, technology, and the examined life.</p>
      </div>
      <div class="footer-col">
        <h4>Navigate</h4>
        <ul>
          <li><a href="#">Home</a></li>
          <li><a href="#">All Articles</a></li>
          <li><a href="#">About</a></li>
          <li><a href="#">Contact</a></li>
        </ul>
      </div>
      <div class="footer-col">
        <h4>Connect</h4>
        <ul>
          <li><a href="#">Twitter / X</a></li>
          <li><a href="#">Mastodon</a></li>
          <li><a href="#">RSS Feed</a></li>
        </ul>
      </div>
    </div>
    <div class="footer-bottom">
      <p>&copy; 2026 The Curious Mind · Made with CSS and coffee</p>
    </div>
  </footer>

</body>
</html>
```

**Milestone 1 output:** A plain unstyled page with all content visible, stacked vertically in one column. All zones present but no visual design yet.

---

### Stage 2 — Complete CSS (`blog.css`)

```css
/* ============================================================
   THE CURIOUS MIND — blog.css
   ============================================================ */

/* === RESET & BASE === */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html { font-size: 16px; }

body {
  font-family: 'Georgia', 'Times New Roman', serif;
  font-size: 1rem;
  line-height: 1.7;
  color: #333333;
  background-color: #f5f5f0;
}

/* === HEADER === */
.site-header {
  background-color: #2c3e50;
  color: #ffffff;
  padding: 40px 20px;
  text-align: center;
}

.header-inner {
  max-width: 800px;
  margin: 0 auto;
}

.site-header h1 {
  font-size: 2.8rem;
  font-weight: normal;
  letter-spacing: -1px;
  margin-bottom: 10px;
}

.site-header p {
  font-size: 1rem;
  color: #95a5a6;
  font-style: italic;
}

/* === NAVBAR (sticky) === */
.navbar {
  background-color: #16a085;
  position: sticky;
  top: 0;
  z-index: 100;
}

.navbar ul {
  list-style: none;
  display: flex;
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 20px;
}

.navbar ul li a {
  display: block;
  color: #ffffff;
  text-decoration: none;
  padding: 15px 18px;
  font-size: 0.95rem;
  font-family: Arial, sans-serif;
  transition: background-color 0.2s ease;
}

.navbar ul li a:hover {
  background-color: #1abc9c;
}

/* === HERO === */
.hero {
  background-color: #1a252f;
  background-image: linear-gradient(135deg, #16a085 0%, #1a252f 60%);
  color: #ffffff;
  padding: 80px 20px;
  text-align: center;
}

.hero-content {
  max-width: 700px;
  margin: 0 auto;
}

.hero-label {
  display: inline-block;
  background-color: rgba(255,255,255,0.15);
  color: #a8e6cf;
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 2px;
  padding: 4px 12px;
  border-radius: 20px;
  margin-bottom: 16px;
  font-family: Arial, sans-serif;
}

.hero h2 {
  font-size: 2.2rem;
  line-height: 1.3;
  margin-bottom: 18px;
  font-weight: normal;
}

.hero p {
  font-size: 1.1rem;
  color: rgba(255,255,255,0.8);
  margin-bottom: 28px;
}

.hero-btn {
  display: inline-block;
  background-color: #16a085;
  color: #ffffff;
  padding: 13px 30px;
  font-size: 1rem;
  text-decoration: none;
  border-radius: 4px;
  font-family: Arial, sans-serif;
  font-weight: bold;
  transition: background-color 0.2s ease, transform 0.15s ease;
}

.hero-btn:hover {
  background-color: #1abc9c;
  transform: translateY(-2px);    /* slight lift effect on hover */
}

/* === CONTENT WRAPPER === */
.content-wrapper {
  display: flex;
  gap: 28px;
  max-width: 1100px;
  margin: 30px auto;
  padding: 0 20px;
}

/* === MAIN CONTENT === */
.main-content {
  flex: 3;
}

.section-title {
  font-size: 1.4rem;
  color: #2c3e50;
  text-transform: uppercase;
  letter-spacing: 2px;
  font-family: Arial, sans-serif;
  margin-bottom: 20px;
  padding-bottom: 10px;
  border-bottom: 3px solid #16a085;
}

/* === INDIVIDUAL BLOG POST CARD === */
.blog-post {
  background-color: #ffffff;
  padding: 28px;
  margin-bottom: 22px;
  border-radius: 6px;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.07);
  border-left: 4px solid #16a085;   /* coloured left accent border */
  transition: box-shadow 0.2s ease, transform 0.15s ease;
}

.blog-post:hover {
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.12);
  transform: translateY(-2px);
}

.post-category {
  display: inline-block;
  background-color: #e8f8f5;
  color: #16a085;
  font-size: 0.75rem;
  font-family: Arial, sans-serif;
  text-transform: uppercase;
  letter-spacing: 1px;
  padding: 3px 10px;
  border-radius: 12px;
  margin-bottom: 10px;
}

.post-title {
  font-size: 1.4rem;
  line-height: 1.4;
  margin-bottom: 8px;
}

.post-title a {
  color: #2c3e50;
  text-decoration: none;
  transition: color 0.2s ease;
}

.post-title a:hover {
  color: #16a085;
}

.post-meta {
  font-size: 0.85rem;
  color: #95a5a6;
  font-family: Arial, sans-serif;
  margin-bottom: 12px;
}

.meta-divider {
  margin: 0 6px;
}

.post-excerpt {
  color: #555555;
  font-size: 0.98rem;
  margin-bottom: 16px;
}

.read-more {
  display: inline-block;
  color: #16a085;
  text-decoration: none;
  font-family: Arial, sans-serif;
  font-size: 0.9rem;
  font-weight: bold;
  transition: color 0.2s ease;
}

.read-more:hover {
  color: #1abc9c;
}

/* === SIDEBAR === */
.sidebar {
  flex: 1;
  align-self: flex-start;
}

.sidebar-widget {
  background-color: #ffffff;
  padding: 22px;
  margin-bottom: 20px;
  border-radius: 6px;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.07);
}

.sidebar-widget h3 {
  font-size: 0.9rem;
  font-family: Arial, sans-serif;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  color: #2c3e50;
  margin-bottom: 15px;
  padding-bottom: 8px;
  border-bottom: 2px solid #e8f8f5;
}

/* Author bio widget */
.author-bio {
  display: flex;
  align-items: flex-start;
  gap: 12px;
}

.author-avatar {
  width: 50px;
  height: 50px;
  background-color: #16a085;
  color: #ffffff;
  font-family: Arial, sans-serif;
  font-weight: bold;
  font-size: 0.9rem;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  flex-shrink: 0;
}

.author-bio p {
  font-size: 0.9rem;
  color: #666;
  line-height: 1.5;
}

/* Category list widget */
.category-list {
  list-style: none;
}

.category-list li {
  border-bottom: 1px solid #f0f0eb;
  padding: 8px 0;
}

.category-list li:last-child {
  border-bottom: none;
}

.category-list li a {
  color: #555555;
  text-decoration: none;
  font-family: Arial, sans-serif;
  font-size: 0.9rem;
  display: flex;
  justify-content: space-between;
  transition: color 0.2s ease;
}

.category-list li a:hover {
  color: #16a085;
}

.category-list li a span {
  color: #aaaaaa;
}

/* Newsletter widget */
.widget-text {
  font-size: 0.85rem;
  color: #777;
  margin-bottom: 12px;
}

.widget-input {
  display: block;
  width: 100%;
  padding: 10px 12px;
  font-size: 0.9rem;
  border: 2px solid #ddd;
  border-radius: 4px;
  margin-bottom: 8px;
  font-family: Arial, sans-serif;
  transition: border-color 0.2s ease;
}

.widget-input:focus {
  outline: none;
  border-color: #16a085;
}

.widget-btn {
  display: block;
  width: 100%;
  padding: 10px;
  background-color: #16a085;
  color: #ffffff;
  font-size: 0.9rem;
  font-family: Arial, sans-serif;
  font-weight: bold;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.widget-btn:hover {
  background-color: #1abc9c;
}

/* === FOOTER === */
.site-footer {
  background-color: #1a252f;
  color: #7f8c8d;
  margin-top: 40px;
}

.footer-inner {
  display: flex;
  gap: 40px;
  max-width: 1100px;
  margin: 0 auto;
  padding: 50px 20px 40px;
}

.footer-col {
  flex: 1;
}

.footer-col h4 {
  color: #ffffff;
  font-family: Arial, sans-serif;
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  margin-bottom: 16px;
  padding-bottom: 8px;
  border-bottom: 1px solid #2c3e50;
}

.footer-col p {
  font-size: 0.9rem;
  line-height: 1.7;
}

.footer-col ul {
  list-style: none;
}

.footer-col ul li {
  margin-bottom: 8px;
}

.footer-col ul li a {
  color: #7f8c8d;
  text-decoration: none;
  font-size: 0.9rem;
  transition: color 0.2s ease;
}

.footer-col ul li a:hover {
  color: #16a085;
}

.footer-bottom {
  background-color: #111a22;
  text-align: center;
  padding: 16px 20px;
  font-size: 0.82rem;
  font-family: Arial, sans-serif;
  color: #5d6d7e;
}

/* === RESPONSIVE DESIGN === */
@media (max-width: 768px) {

  /* Stack all content vertically */
  .content-wrapper {
    flex-direction: column;
  }

  .main-content,
  .sidebar {
    flex: none;
    width: 100%;
  }

  /* Stack navbar links */
  .navbar ul {
    flex-direction: column;
    padding: 0;
  }

  /* Stack footer columns */
  .footer-inner {
    flex-direction: column;
    gap: 25px;
    padding: 30px 20px;
  }

  /* Smaller hero on mobile */
  .hero {
    padding: 50px 20px;
  }

  .hero h2 {
    font-size: 1.6rem;
  }

  /* Smaller header on mobile */
  .site-header h1 {
    font-size: 2rem;
  }

  /* Author bio stacks vertically */
  .author-bio {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }
}

@media (max-width: 480px) {
  .site-header {
    padding: 25px 15px;
  }

  .blog-post {
    padding: 20px 18px;
  }

  .hero h2 {
    font-size: 1.4rem;
  }
}
```

**Milestone 2 output:** A fully styled personal blog with teal and dark charcoal colour scheme, hero banner with gradient, article cards with accent borders and hover lift effects, a sidebar with three widgets (bio, categories, newsletter), and a three-column footer. Fully responsive — collapses to single column on mobile.

---

### Stage 3 — Testing Your Layout

Work through this checklist:

1. **Desktop test:** Open the page in a browser at full width. Verify: header → navbar → hero → two-column content → footer from top to bottom.
2. **Sticky navbar test:** Scroll down the page. Does the teal navbar stay fixed at the top?
3. **Hover tests:** Hover over each navbar link, each article title, the hero button, the Read More links, the footer links. Each should show a colour change.
4. **Resize test:** Drag your browser window narrower. At about 768px, the layout should shift to single column.
5. **Mobile test:** Open browser DevTools (F12), toggle device simulation to a phone width. Verify single-column stacking.

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting `overflow: hidden` on a Float Container

```css
/* ❌ BAD: float children collapse the parent to zero height */
.content-wrapper {
  max-width: 1100px;
  margin: 0 auto;
  /* missing overflow: hidden */
}

.main-content { float: left; width: 70%; }
.sidebar { float: right; width: 28%; }
```

**Result:** The footer slides up and overlaps the content — the parent `div` has no height because its floated children are invisible to it.

**Fix:** Add `overflow: hidden` to the parent, or switch to Flexbox (which doesn't have this problem):
```css
/* ✅ FIX 1: clearfix */
.content-wrapper { overflow: hidden; }

/* ✅ FIX 2: use flexbox instead */
.content-wrapper { display: flex; gap: 20px; }
```

---

### Mistake 2 — Using `width: 100%` Without `box-sizing: border-box`

```css
/* ❌ BAD: padding causes overflow */
.main-content {
  float: left;
  width: 70%;
  padding: 30px;   /* adds 60px (30+30) to the element's width — total > 70% */
}
```

**Result:** The element overflows beyond 70% because the padding is added *outside* the 70% width. This pushes the sidebar down to the next row.

**Fix:**
```css
/* ✅ GOOD: with box-sizing, padding is included IN the 70% */
* {
  box-sizing: border-box;
}

.main-content {
  float: left;
  width: 70%;
  padding: 30px;    /* now safely contained within 70% */
}
```

---

### Mistake 3 — Missing the Viewport Meta Tag

```html
<!-- ❌ BAD: no viewport meta tag -->
<head>
  <title>My Site</title>
</head>
```

**Result:** On mobile phones, the browser renders the page as if it were a desktop (980px wide), then shrinks the whole page down. Your layout appears tiny and unreadable.

**Fix:**
```html
<!-- ✅ GOOD: always include this -->
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Site</title>
</head>
```

---

### Mistake 4 — Not Using `max-width` on Content

```css
/* ❌ BAD: on a 2500px wide monitor, lines stretch impossibly long */
.content-wrapper {
  display: flex;
  width: 100%;
  padding: 0 20px;
}
```

**Fix:**
```css
/* ✅ GOOD: content has a sensible maximum width */
.content-wrapper {
  display: flex;
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 20px;
}
```

---

### Mistake 5 — Setting the Sidebar to Exactly 30% With a Gap

```css
/* ❌ BAD: 70% + 30% = 100%, leaving no room for the gap */
.main-content { width: 70%; }
.sidebar { width: 30%; }
/* A 20px gap makes the total width 100% + 20px = overflow */
```

**Fix with Flexbox — use `flex` ratios instead of fixed percentages:**
```css
/* ✅ GOOD: flexbox handles gaps and proportions automatically */
.content-wrapper { display: flex; gap: 20px; }
.main-content { flex: 3; }   /* 3/4 of available space after gap */
.sidebar { flex: 1; }         /* 1/4 of available space after gap */
```

---

### Mistake 6 — Forgetting Responsive Styles

```css
/* ❌ BAD: two-column layout breaks on mobile */
.content-wrapper {
  display: flex;
}
/* no media query for small screens */
```

**Result:** On a 375px phone, the main content column is about 280px wide and the sidebar is about 95px wide — both too narrow to be readable.

**Fix:**
```css
/* ✅ GOOD: add a media query */
@media (max-width: 768px) {
  .content-wrapper {
    flex-direction: column;  /* stack vertically */
  }
}
```

---

## Reflection Questions

Think through these before moving on:

1. What are the five main zones of a standard website layout, and what is the purpose of each?

2. Why do you need `overflow: hidden` on a parent element when its children are floated? What problem does it solve?

3. What is the difference between using `float` and `display: flex` to create side-by-side columns? What are the advantages of Flexbox?

4. A colleague says "I'll set the main content to `width: 75%` and the sidebar to `width: 25%`." What problem might arise, and how would you fix it?

5. What does `margin: 0 auto` do, and why does it only work when the element has a defined `width` or `max-width`?

6. Why is the viewport meta tag essential for responsive layouts?

7. When would you choose a full-width (no sidebar) layout instead of a two-column layout? Give two real-world examples.

8. What does `flex: 3` mean when used alongside `flex: 1` in the same flex container? What ratio does this create?

9. You have a sticky navbar with `position: sticky; top: 0`. Why is `z-index: 100` also needed?

10. What is the purpose of a `max-width` on the content wrapper? What problem does it solve on very large monitors?

---

## Completion Checklist

Verify you have mastered this lesson:

- [ ] I can name and describe all five main zones of a website layout
- [ ] I can write the complete HTML skeleton for a multi-zone webpage
- [ ] I understand `box-sizing: border-box` and why it is added as a reset
- [ ] I can style a full-width header with centred text
- [ ] I can create a horizontal navigation bar using Flexbox
- [ ] I understand how `float: left` and `float: right` create side-by-side columns
- [ ] I can create a two-column layout using Flexbox (`flex: 3` and `flex: 1`)
- [ ] I can create a two-column layout using CSS Grid (`grid-template-columns: 3fr 1fr`)
- [ ] I understand `margin: 0 auto` and how it centres a block element
- [ ] I understand `max-width` and why it improves readability on wide screens
- [ ] I can write a sticky navbar using `position: sticky; top: 0; z-index: 100`
- [ ] I can build a hero section with a gradient background
- [ ] I can write a multi-column footer using Flexbox
- [ ] I can use `@media (max-width: 768px)` to make a layout responsive
- [ ] I have built the complete blog homepage mini project
- [ ] I can identify and fix the 6 common layout mistakes

---

## Lesson Summary

In this lesson, you learned how to build a complete website layout from scratch using CSS. You went from understanding the anatomy of a webpage to writing a fully styled, responsive, professional design.

**The five zones:** Every website has a recognisable structure — header (branding at the top), navbar (navigation links), main content (the primary zone), sidebar (supplementary content), and footer (bottom info and links). Understanding these zones is the foundation of all web design.

**HTML structure first:** You always build the HTML skeleton first, using semantic elements like `<header>`, `<nav>`, `<main>`, `<aside>`, and `<footer>`. CSS then arranges and decorates this structure.

**The box model reset:** Starting every stylesheet with `* { box-sizing: border-box; margin: 0; padding: 0; }` prevents common sizing bugs and creates a clean starting point.

**Two-column layouts:** You learned three approaches — float (classic), Flexbox (modern standard), and Grid (most powerful). Flexbox with `flex: 3` and `flex: 1` creates a clean 75%/25% column split that automatically handles gaps and proportions.

**Centring content:** `max-width` limits how wide content grows on large screens. `margin: 0 auto` centres the container horizontally. Together, they create the comfortable reading column found on nearly every professional website.

**Sticky navigation:** `position: sticky; top: 0; z-index: 100` keeps a navbar visible as users scroll — a standard pattern on modern sites.

**Hero sections:** A hero is a large visually striking banner that uses gradient backgrounds, large typography, and prominent call-to-action buttons to immediately engage visitors.

**Responsive design:** Every layout needs media queries to collapse two-column arrangements into single-column stacks on mobile. `@media (max-width: 768px) { .content-wrapper { flex-direction: column; } }` is the foundational mobile breakpoint.

> 🌟 **Final thought:** Web layout is architecture. Just as an architect plans where rooms go before building walls, a web developer plans where zones go before writing CSS. Master the layout first, then add decoration. You now have the skills to build the structural foundation of any website you can imagine.

---

*Sources: W3Schools CSS Website Layout (https://www.w3schools.com/css/css_website_layout.asp) and CSS Website Layout Code Challenges (https://www.w3schools.com/css/css_challenges_website_layout.asp)*
