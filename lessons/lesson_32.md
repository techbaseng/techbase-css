---
render_with_liquid: false
title: "CSS Navigation Bars – Vertical and Horizontal Navbars"
nav_order: 32
---

# Lesson 32: CSS Navigation Bars — Building Vertical and Horizontal Navbars

---

## Lesson Introduction

Every website you have ever visited has a **navigation bar** — also called a **navbar**. It is the row of links at the top of a page (or the column of links down the side) that lets visitors jump between different sections or pages.

Navigation bars are one of the first things a visitor sees when they land on a website. A clean, well-styled navbar instantly makes a site feel professional. A clunky, unstyled one — just a plain blue list of underlined links — signals an unfinished project.

The great news is that building a beautiful, fully functional navbar in CSS is completely achievable for a beginner. It is mostly a matter of:
1. Starting with the right HTML structure (a `<ul>` list of links)
2. Removing the default list styles that make it look ugly
3. Applying positioning, colours, hover effects, and spacing

In this lesson you will learn:
- Why a `<ul>` list is the correct HTML foundation for any navbar
- How to strip out default list styling to get a clean starting point
- How to build a **vertical navigation bar** (links stacked top to bottom, like a sidebar)
- How to build a **horizontal navigation bar** (links side by side in a row, like a top menu)
- How to style link states: normal, visited, hover, and active
- How to add dropdown menus, borders, dividers, and sticky positioning
- How to combine everything into a complete, professional website header

By the end you will have built two complete navbars and a full website header mini-project.

---

## Prerequisite Concepts

Before diving in, let us quickly review three things this lesson depends on.

### The `<a>` Tag and Link States

A link (`<a>`) has four special states that CSS can style separately:

- `a:link` — an unvisited link (the default blue underlined look)
- `a:visited` — a link the user has already clicked (usually turns purple)
- `a:hover` — when the user's mouse is over the link
- `a:active` — the brief moment the user is clicking the link

> **Order matters!** Always write them in this order: `link → visited → hover → active`. A helpful memory trick: **L**o**V**e **HA**te (Link, Visited, Hover, Active).

### `display: block` vs `display: inline`

By default, `<a>` tags are **inline** elements — they only take up as much space as their text content. This makes them hard to click precisely, especially on mobile.

Making a link `display: block` turns it into a block element that fills the full width of its container. This gives it a much larger, easier-to-click area — very important for navigation links.

### Lists and Default Styles

An unordered list (`<ul>`) by default comes with:
- Bullet points (`list-style-type: disc`)
- Indentation (left padding and margin)
- Vertical stacking of items

For navbars, we always start by removing these defaults:

```css
ul {
  list-style-type: none;  /* removes bullets */
  margin: 0;              /* removes default margin */
  padding: 0;             /* removes default indentation */
}
```

---

## Part 1: Why Use a List for Navigation?

You might wonder: why start with a `<ul>` list? Why not just a row of `<div>` elements or plain `<a>` tags?

The answer is **semantic HTML** — using HTML elements for their correct intended meaning. A navigation menu is literally a list of links. Using `<ul>` and `<li>` tells the browser, search engines, and screen readers (used by visually impaired users) exactly what this content is.

This matters for:
- **Accessibility**: Screen readers announce "list of 5 items" to blind users, helping them understand the navigation structure.
- **SEO**: Search engines give weight to navigation links, and proper structure helps them understand your site.
- **Maintainability**: Other developers instantly recognise the pattern.

**The Standard HTML Structure for Every Navbar:**

```html
<nav>
  <ul>
    <li><a href="#home">Home</a></li>
    <li><a href="#about">About</a></li>
    <li><a href="#services">Services</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>
```

- `<nav>` — the semantic HTML5 element that marks a navigation section
- `<ul>` — the unordered list container
- `<li>` — each individual list item (one per link)
- `<a>` — the actual clickable link

This HTML alone, unstyled, looks like a plain bulleted list. CSS is what transforms it into a polished navbar.

---

## Part 2: The Starting Reset — Stripping Default List Styles

The very first step before building any navbar is always to remove the browser's default list styling. This is your clean canvas.

```css
/* Step 1: Remove default list appearance */
ul {
  list-style-type: none;   /* kills the bullet points */
  margin: 0;               /* kills the default outer spacing */
  padding: 0;              /* kills the default left indentation */
}
```

**Before (without reset):**
- Bullet points on every item
- Items indented from the left
- Links appear as blue underlined text

**After (with reset):**
- Plain text items with no bullets
- No indentation
- Ready to be styled however you like

> **Thinking Prompt:** Open any website in your browser. Right-click the navigation bar and choose "Inspect". Can you find the `<ul>` and `<li>` elements that make up the nav? Nearly every website uses this pattern.

---

## Part 3: Building a Vertical Navigation Bar

A **vertical navbar** shows links stacked on top of each other, like a sidebar menu. It is common on dashboards, admin panels, documentation sites, and mobile menus.

### Step 1: The Base HTML

```html
<!DOCTYPE html>
<html>
<head>
  <title>Vertical Navbar</title>
  <link rel="stylesheet" href="vertical-nav.css">
</head>
<body>

  <nav>
    <ul>
      <li><a href="#home">Home</a></li>
      <li><a href="#news">News</a></li>
      <li><a href="#contact">Contact</a></li>
      <li><a href="#about">About</a></li>
    </ul>
  </nav>

</body>
</html>
```

### Step 2: The Core CSS — Making It Vertical

```css
/* vertical-nav.css */

/* Reset */
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  width: 200px;              /* the navbar has a fixed width */
  background-color: #f1f1f1; /* light grey background */
}

/* Each link */
li a {
  display: block;            /* CRUCIAL — makes the entire area clickable, not just the text */
  color: #333;               /* dark grey text */
  padding: 10px 16px;        /* comfortable vertical and horizontal breathing room */
  text-decoration: none;     /* removes the underline */
}
```

**Expected Output (so far):**
- A 200px-wide light grey sidebar
- Four links stacked vertically, each with comfortable padding
- No underlines, no bullets, clean text

### Step 3: Adding Hover and Active States

```css
/* Change background on hover */
li a:hover {
  background-color: #555;    /* dark grey */
  color: white;
}

/* Highlight the currently active/selected page */
li a.active {
  background-color: #04aa6d; /* green — clearly shows which page is current */
  color: white;
}
```

**Update the HTML** — add `class="active"` to the current page's link:

```html
<li><a href="#home" class="active">Home</a></li>
```

**Expected Output:**
- Hovering over any link turns the background dark grey with white text.
- The "Home" link has a permanent green background showing it is the current page.

### Step 4: Adding a Border

```css
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  width: 200px;
  background-color: #f1f1f1;
  border: 1px solid #ccc;    /* a subtle outer border for the whole navbar */
}

/* Divider lines between items */
li {
  border-bottom: 1px solid #ccc;  /* each item has a line underneath it */
}

/* Remove border from last item so it doesn't double up with the outer border */
li:last-child {
  border-bottom: none;
}
```

**Expected Output:**
- A bordered navbar with a thin line between each link item — like a clean menu card.

### Complete Vertical Navbar — Full Code

```html
<!DOCTYPE html>
<html>
<head>
<style>
  * { box-sizing: border-box; }

  body {
    font-family: Arial, sans-serif;
    margin: 0;
  }

  ul.vertical-nav {
    list-style-type: none;
    margin: 0;
    padding: 0;
    width: 220px;
    background-color: #f8f8f8;
    border: 1px solid #ddd;
    border-radius: 6px;
    overflow: hidden;
  }

  ul.vertical-nav li {
    border-bottom: 1px solid #ddd;
  }

  ul.vertical-nav li:last-child {
    border-bottom: none;
  }

  ul.vertical-nav li a {
    display: block;
    color: #333;
    padding: 12px 18px;
    text-decoration: none;
    font-size: 15px;
    transition: background-color 0.2s, color 0.2s; /* smooth colour change */
  }

  ul.vertical-nav li a:hover {
    background-color: #0078d7;
    color: white;
  }

  ul.vertical-nav li a.active {
    background-color: #0078d7;
    color: white;
    font-weight: bold;
  }
</style>
</head>
<body>

  <nav style="padding: 30px;">
    <ul class="vertical-nav">
      <li><a href="#home" class="active">🏠 Home</a></li>
      <li><a href="#news">📰 News</a></li>
      <li><a href="#contact">✉️ Contact</a></li>
      <li><a href="#about">ℹ️ About</a></li>
    </ul>
  </nav>

</body>
</html>
```

**Expected Output:**
- A polished sidebar nav 220px wide with rounded corners.
- Each item has a thin divider line.
- "Home" has a blue background (active state).
- Hovering over other links smoothly transitions to a blue background with white text.

---

## Part 4: Centering Content Next to a Vertical Navbar

In a real webpage, a vertical navbar sits beside the main content. Here is a simple two-column layout using Flexbox:

```html
<!DOCTYPE html>
<html>
<head>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: Arial, sans-serif;
    display: flex;
    min-height: 100vh;
  }

  /* The sidebar nav */
  .sidebar {
    width: 220px;
    min-height: 100vh;
    background-color: #2d2d2d;
    flex-shrink: 0;     /* sidebar never shrinks */
  }

  .sidebar ul {
    list-style: none;
    padding: 20px 0;
  }

  .sidebar li a {
    display: block;
    color: #ccc;
    padding: 14px 24px;
    text-decoration: none;
    font-size: 15px;
    transition: background-color 0.2s;
  }

  .sidebar li a:hover {
    background-color: #444;
    color: white;
  }

  .sidebar li a.active {
    background-color: #e94560;
    color: white;
  }

  /* Main content area */
  .main-content {
    flex: 1;               /* takes all remaining space */
    padding: 40px;
    background-color: #f5f5f5;
  }

  .main-content h1 {
    font-size: 28px;
    color: #1a1a2e;
    margin-bottom: 16px;
  }
</style>
</head>
<body>

  <nav class="sidebar">
    <ul>
      <li><a href="#" class="active">Dashboard</a></li>
      <li><a href="#">Analytics</a></li>
      <li><a href="#">Reports</a></li>
      <li><a href="#">Settings</a></li>
      <li><a href="#">Logout</a></li>
    </ul>
  </nav>

  <main class="main-content">
    <h1>Welcome to the Dashboard</h1>
    <p>Select an option from the sidebar to get started.</p>
  </main>

</body>
</html>
```

**Expected Output:**
- A dark sidebar on the left with navigation links (white/grey text, red active state).
- A light grey main content area filling the rest of the screen.
- Both areas stretch to the full viewport height.

---

## Part 5: Building a Horizontal Navigation Bar

A **horizontal navbar** runs across the top of the page with links side by side. This is the most common navbar style — used on almost every website header.

There are two main CSS techniques to make list items sit side by side:
- **`display: inline-block`** on the `<li>` elements
- **Flexbox** on the `<ul>` — the modern, recommended approach

### Method 1: `display: inline-block` on `<li>`

```html
<!DOCTYPE html>
<html>
<head>
<style>
  ul.horiz-nav {
    list-style-type: none;
    margin: 0;
    padding: 0;
    background-color: #333;
    overflow: hidden;        /* clearfix-style safety net */
  }

  /* Make list items sit side by side */
  ul.horiz-nav li {
    display: inline-block;   /* items sit in a horizontal row */
  }

  ul.horiz-nav li a {
    display: block;
    color: white;
    padding: 14px 20px;
    text-decoration: none;
    font-size: 15px;
  }

  ul.horiz-nav li a:hover {
    background-color: #555;
  }

  ul.horiz-nav li a.active {
    background-color: #04aa6d;
  }
</style>
</head>
<body>

  <nav>
    <ul class="horiz-nav">
      <li><a href="#home" class="active">Home</a></li>
      <li><a href="#news">News</a></li>
      <li><a href="#contact">Contact</a></li>
      <li><a href="#about">About</a></li>
    </ul>
  </nav>

</body>
</html>
```

**Expected Output:**
- A dark horizontal bar spanning the full page width.
- Four links side by side with comfortable padding.
- "Home" has a green background. Other links go dark grey on hover.

**Why `display: inline-block` on `<li>` AND `display: block` on `<a>`?**

- `display: inline-block` on `<li>` makes the list items sit side by side (instead of stacking vertically).
- `display: block` on `<a>` makes the clickable area fill the entire padding box of the link — not just the text. This gives a larger, more comfortable click target.

### Method 2: Flexbox on `<ul>` (Recommended)

```css
ul.flex-nav {
  list-style-type: none;
  margin: 0;
  padding: 0;
  background-color: #333;
  display: flex;             /* makes children (li items) sit in a row */
}

ul.flex-nav li a {
  display: block;
  color: white;
  padding: 14px 20px;
  text-decoration: none;
}

ul.flex-nav li a:hover {
  background-color: #555;
}
```

Using `display: flex` on the `<ul>` makes all its `<li>` children automatically sit side by side without needing to change the `<li>` display property at all.

> **Which method should you use?** Flexbox is the modern, preferred approach. It handles spacing and alignment far more easily and works better for responsive design. Use `inline-block` only when you need to support very old browsers or are working in older codebases.

---

## Part 6: Right-Aligning a Navbar Link

Sometimes you need most links on the left but one link — like "Login" or "Sign Up" — pushed to the far right. Flexbox makes this trivial with `margin-left: auto` on the last item.

```css
ul.flex-nav {
  list-style-type: none;
  margin: 0;
  padding: 0;
  background-color: #333;
  display: flex;
}

ul.flex-nav li a {
  display: block;
  color: white;
  padding: 14px 20px;
  text-decoration: none;
}

ul.flex-nav li a:hover {
  background-color: #555;
}

/* Push the last item to the far right */
ul.flex-nav li:last-child {
  margin-left: auto;
}
```

```html
<ul class="flex-nav">
  <li><a href="#" class="active">Home</a></li>
  <li><a href="#">About</a></li>
  <li><a href="#">Contact</a></li>
  <li><a href="#">Login</a></li>  <!-- this gets pushed right -->
</ul>
```

**Expected Output:**
- "Home", "About", "Contact" are on the left.
- "Login" is pushed all the way to the right side of the bar.

**How does `margin-left: auto` work here?**
In a flex container, `margin: auto` absorbs all the available free space in the specified direction. Setting `margin-left: auto` on an item tells it to push itself as far right as possible by consuming all the leftover horizontal space.

---

## Part 7: Adding a Logo to the Left Side

In a real website header, the logo sits on the left and the navigation links sit on the right (or follow the logo). Here is the full pattern:

```html
<!DOCTYPE html>
<html>
<head>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }

  .topnav {
    background-color: #1a1a2e;
    display: flex;
    align-items: center;     /* vertically centre all children */
    padding: 0 30px;
  }

  .logo {
    color: gold;
    font-size: 22px;
    font-weight: bold;
    padding: 14px 0;
    text-decoration: none;
    margin-right: auto;      /* push everything else to the right */
  }

  .nav-links {
    list-style: none;
    display: flex;
  }

  .nav-links li a {
    display: block;
    color: #ccc;
    padding: 14px 18px;
    text-decoration: none;
    font-size: 15px;
    transition: color 0.2s;
  }

  .nav-links li a:hover {
    color: white;
  }

  .nav-links li a.active {
    color: gold;
    font-weight: bold;
  }

  .nav-links .btn-cta {
    background-color: #e94560;
    color: white !important;
    border-radius: 20px;
    padding: 8px 20px !important;
    margin: 10px 0 10px 10px;
    transition: background-color 0.2s !important;
  }

  .nav-links .btn-cta:hover {
    background-color: #c73652 !important;
  }
</style>
</head>
<body>

  <header>
    <nav class="topnav">
      <a class="logo" href="#">BrandName</a>
      <ul class="nav-links">
        <li><a href="#" class="active">Home</a></li>
        <li><a href="#">Features</a></li>
        <li><a href="#">Pricing</a></li>
        <li><a href="#">Blog</a></li>
        <li><a href="#" class="btn-cta">Get Started</a></li>
      </ul>
    </nav>
  </header>

</body>
</html>
```

**Expected Output:**
- A dark blue header bar.
- "BrandName" logo in gold on the far left.
- Nav links in grey on the right, with "Home" highlighted in gold.
- A red pill-shaped "Get Started" call-to-action button at the far right.

---

## Part 8: Fixed/Sticky Navigation Bars

One of the most common requirements in modern web design is a navbar that **stays at the top of the screen** as the user scrolls down the page.

### Fixed Navbar

A `position: fixed` navbar stays anchored to the top of the browser viewport at all times, regardless of scrolling.

```css
.fixed-nav {
  position: fixed;       /* removes it from normal document flow */
  top: 0;                /* pins it to the very top */
  left: 0;               /* stretches from the left edge */
  width: 100%;           /* full width */
  background-color: #333;
  z-index: 1000;         /* above all other page content */
}
```

> **Important:** A fixed navbar is removed from the normal document flow. This means the content below it will slide underneath it. You must add `padding-top` (equal to the navbar height) to the `<body>` or main content area to prevent content from being hidden behind the navbar.

```css
body {
  padding-top: 60px;   /* matches the navbar height */
}
```

### Sticky Navbar

A `position: sticky` navbar behaves like a normal element in the flow until the user scrolls past it — then it sticks to the top.

```css
.sticky-nav {
  position: sticky;
  top: 0;               /* stick to the very top when scrolled to */
  background-color: #333;
  z-index: 100;
}
```

**Difference between `fixed` and `sticky`:**
- `fixed`: Always at the top, even when you first load the page. Content must be padded to account for it.
- `sticky`: Sits in normal flow at first, then sticks when scrolled past. No need to pad content.

```html
<!DOCTYPE html>
<html>
<head>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }

  body { font-family: Arial, sans-serif; }

  .sticky-nav {
    position: sticky;
    top: 0;
    background-color: #0f3460;
    display: flex;
    list-style: none;
    padding: 0 20px;
    z-index: 100;
    box-shadow: 0 2px 8px rgba(0,0,0,0.3);
  }

  .sticky-nav li a {
    display: block;
    color: white;
    padding: 16px 18px;
    text-decoration: none;
  }

  .sticky-nav li a:hover {
    background-color: rgba(255,255,255,0.1);
  }

  .content-section {
    padding: 60px 40px;
    min-height: 100vh;
    border-bottom: 1px solid #eee;
  }

  .content-section:nth-child(odd) {
    background-color: #f9f9f9;
  }
</style>
</head>
<body>

  <ul class="sticky-nav">
    <li><a href="#section1">Section 1</a></li>
    <li><a href="#section2">Section 2</a></li>
    <li><a href="#section3">Section 3</a></li>
  </ul>

  <div class="content-section" id="section1">
    <h2>Section 1</h2>
    <p>Scroll down to see the navbar stick to the top.</p>
  </div>

  <div class="content-section" id="section2">
    <h2>Section 2</h2>
    <p>The navbar is still visible at the top as you scroll.</p>
  </div>

  <div class="content-section" id="section3">
    <h2>Section 3</h2>
    <p>All three sections are reachable via the sticky navbar.</p>
  </div>

</body>
</html>
```

**Expected Output:**
- Three tall page sections.
- A dark blue navbar that sits at the top normally when the page loads.
- As you scroll down, the navbar sticks to the top of the viewport and stays there.

---

## Part 9: Adding a Dropdown Menu to a Horizontal Navbar

A **dropdown menu** appears when you hover over a navbar link, revealing sub-links below it. This is achieved entirely with CSS using `position: absolute` and `:hover`.

```html
<!DOCTYPE html>
<html>
<head>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }

  /* The main navbar */
  ul.dropdown-nav {
    list-style: none;
    background-color: #333;
    display: flex;
  }

  ul.dropdown-nav > li {
    position: relative;    /* anchor for the absolute dropdown */
  }

  ul.dropdown-nav > li > a {
    display: block;
    color: white;
    padding: 14px 20px;
    text-decoration: none;
  }

  ul.dropdown-nav > li > a:hover {
    background-color: #555;
  }

  /* The dropdown container — hidden by default */
  .dropdown-content {
    display: none;                /* hidden until hover */
    position: absolute;
    top: 100%;                    /* appears directly below the parent li */
    left: 0;
    background-color: #444;
    min-width: 180px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.3);
    z-index: 1;
  }

  /* Each dropdown link */
  .dropdown-content a {
    display: block;
    color: white;
    padding: 12px 18px;
    text-decoration: none;
    font-size: 14px;
  }

  .dropdown-content a:hover {
    background-color: #666;
  }

  /* Show dropdown when hovering the parent li */
  ul.dropdown-nav > li:hover .dropdown-content {
    display: block;
  }
</style>
</head>
<body>

  <nav>
    <ul class="dropdown-nav">
      <li><a href="#">Home</a></li>

      <li>
        <a href="#">Services ▾</a>   <!-- ▾ is a small downward triangle indicator -->
        <div class="dropdown-content">
          <a href="#">Web Design</a>
          <a href="#">Development</a>
          <a href="#">Hosting</a>
        </div>
      </li>

      <li>
        <a href="#">Products ▾</a>
        <div class="dropdown-content">
          <a href="#">Software</a>
          <a href="#">Hardware</a>
          <a href="#">Support</a>
        </div>
      </li>

      <li><a href="#">Contact</a></li>
    </ul>
  </nav>

</body>
</html>
```

**Expected Output:**
- A dark horizontal navbar with four items.
- "Home" and "Contact" are plain links.
- Hovering over "Services" reveals a dropdown with three sub-links.
- Hovering over "Products" reveals another dropdown with three sub-links.
- Dropdowns disappear when you move the mouse away.

**How the dropdown works — step by step:**

1. `.dropdown-content` is hidden by default (`display: none`).
2. The parent `<li>` has `position: relative` — this makes it the anchor for the dropdown's absolute positioning.
3. `.dropdown-content` has `position: absolute` with `top: 100%` — this places it directly below the parent `<li>`.
4. `ul.dropdown-nav > li:hover .dropdown-content` — when the user hovers over the parent `<li>`, this selector applies `display: block` to the dropdown, making it visible.
5. Because the mouse moves from the `<li>` into the `.dropdown-content` (which is a child of `<li>`), the hover state is maintained and the dropdown stays open.

> **Thinking Prompt:** What happens to the dropdown if you remove `position: relative` from the `<li>`? (The dropdown loses its anchor and positions itself relative to the nearest positioned ancestor — possibly the whole page — causing it to appear in the wrong place.)

---

## Part 10: Styling a Full Horizontal Navbar — Variations and Options

### Adding a Bottom Border/Underline on Active Link

```css
.nav-links li a.active {
  border-bottom: 3px solid gold;  /* underline style active indicator */
  color: white;
}
```

### Adding a Divider Between Links

```css
ul.horiz-nav li {
  border-right: 1px solid #555;  /* vertical divider line on the right */
}

ul.horiz-nav li:last-child {
  border-right: none;            /* remove from last item */
}
```

### Making the Active Link Stand Out with a Top Border

```css
.nav-links li a.active {
  border-top: 3px solid #e94560;   /* coloured top line for active page */
  padding-top: 11px;               /* compensate for the 3px border */
}
```

### Adding a Background Colour Change on the Entire Navbar on Scroll (using a class)

You can add a class with JavaScript to change the navbar's appearance once the user has scrolled down. In pure CSS, you can pre-style that class:

```css
.scrolled {
  background-color: rgba(0, 0, 0, 0.95);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.4);
}
```

---

## Part 11: Guided Practice Exercises

### Exercise 1 — Build a Basic Vertical Navbar (Warm-Up)

**Objective:** Transform a plain list into a styled vertical sidebar navigation.

**Scenario:** You are building a dashboard sidebar for a project management app.

**Starter Code:**

```html
<!DOCTYPE html>
<html>
<head>
<style>
  /* Your CSS goes here */
</style>
</head>
<body>

  <nav>
    <ul>
      <li><a href="#">Dashboard</a></li>
      <li><a href="#">Projects</a></li>
      <li><a href="#">Tasks</a></li>
      <li><a href="#">Team</a></li>
      <li><a href="#">Settings</a></li>
    </ul>
  </nav>

</body>
</html>
```

**Your Task — Add CSS to achieve:**
1. Remove bullets and default spacing from `ul`
2. Set `ul` width to `240px` and background to `#1e293b` (dark navy)
3. Make each `<a>` `display: block`, colour `#94a3b8` (grey), padding `13px 20px`, no underline
4. On hover: background `#334155`, colour `white`
5. Add `class="active"` to "Dashboard" and style it: background `#3b82f6` (blue), colour `white`

**Expected Output:**
A dark navy sidebar with "Dashboard" highlighted in blue and the rest styled as grey text that turns white on hover.

**Solution:**

```css
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  width: 240px;
  background-color: #1e293b;
}

ul li a {
  display: block;
  color: #94a3b8;
  padding: 13px 20px;
  text-decoration: none;
  transition: background-color 0.2s, color 0.2s;
}

ul li a:hover {
  background-color: #334155;
  color: white;
}

ul li a.active {
  background-color: #3b82f6;
  color: white;
}
```

**Self-Check:** Remove `display: block` from `li a`. What changes? (Clicking the link only works when you click the text itself — the padding area is no longer clickable. This demonstrates why `display: block` is essential.)

---

### Exercise 2 — Build a Horizontal Navbar with a Right-Aligned Button

**Objective:** Create a top navigation bar with a logo on the left and links + a CTA button on the right.

**Your Task:**

```html
<!DOCTYPE html>
<html>
<head>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }

  /* Style the header to use Flexbox, dark background, align items vertically */
  .header { /* your styles */ }

  /* Style the logo: gold colour, large font, no underline */
  .logo { /* your styles */ }

  /* Style the ul: no list style, display flex */
  .nav-list { /* your styles */ }

  /* Style each link: white text, padding, no underline, hover darkens */
  .nav-list li a { /* your styles */ }

  /* Style the .cta button: red background, white text, rounded corners */
  .cta { /* your styles */ }
</style>
</head>
<body>

  <header class="header">
    <a class="logo" href="#">ShopNow</a>
    <ul class="nav-list">
      <li><a href="#">Home</a></li>
      <li><a href="#">Shop</a></li>
      <li><a href="#">Deals</a></li>
      <li><a href="#" class="cta">Sign Up Free</a></li>
    </ul>
  </header>

</body>
</html>
```

**Expected Output:**
- Dark header with "ShopNow" logo on the left in gold.
- "Home", "Shop", "Deals" links in white on the right.
- "Sign Up Free" button with red background and rounded corners.

**Solution:**

```css
.header {
  background-color: #1a1a2e;
  display: flex;
  align-items: center;
  padding: 0 30px;
}

.logo {
  color: gold;
  font-size: 22px;
  font-weight: bold;
  text-decoration: none;
  padding: 14px 0;
  margin-right: auto;  /* pushes everything else to the right */
}

.nav-list {
  list-style: none;
  display: flex;
  align-items: center;
  gap: 5px;
}

.nav-list li a {
  display: block;
  color: white;
  padding: 10px 16px;
  text-decoration: none;
  border-radius: 4px;
  transition: background-color 0.2s;
}

.nav-list li a:hover {
  background-color: rgba(255,255,255,0.1);
}

.cta {
  background-color: #e94560;
  color: white !important;
  border-radius: 20px;
  padding: 9px 20px !important;
}

.cta:hover {
  background-color: #c73652 !important;
}
```

---

### Exercise 3 — Dropdown Menu Challenge

**Objective:** Add a dropdown submenu to one link in a horizontal navbar.

**Your Task:**
Take the horizontal navbar from Exercise 2 and add a "Categories" link that has a dropdown with: Electronics, Clothing, and Home & Garden.

**Hint — Key steps:**
1. Add a new `<li>` for "Categories" with a nested `<div class="dropdown-content">` inside it.
2. Give the parent `<li>` `position: relative`.
3. Give `.dropdown-content` `display: none`, `position: absolute`, `top: 100%`, a dark background, and `min-width: 160px`.
4. Add `li:hover .dropdown-content { display: block; }`.

**Expected Output:**
- Hovering over "Categories" reveals a dropdown with three items.
- The dropdown has a dark background with white text.
- Moving the mouse away hides the dropdown.

---

### Exercise 4 — Sticky Navbar with Scroll Effect

**Objective:** Build a page with a sticky navbar and three full-height sections.

**Your Task:**
1. Create a `<ul>` navbar with `position: sticky; top: 0`.
2. Create three `<section>` elements each with `height: 100vh` and different background colours.
3. Each navbar link should point to a section using `href="#section1"` etc. and `id="section1"` on the sections.

**Expected Output:**
- The page initially shows the navbar at the top with the first section below.
- As you scroll, the navbar stays pinned to the top of the viewport.
- Clicking a nav link jumps to that section.

---

## Part 12: Mini Project — Complete Website Header

In this project you will build a full, production-quality website header that includes a logo, horizontal navigation, a sticky behaviour, and a dropdown menu — everything you have learned combined.

### Project HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TechFlow — Home</title>
  <link rel="stylesheet" href="header.css">
</head>
<body>

  <!-- STICKY HEADER -->
  <header class="site-header">
    <nav class="navbar">

      <!-- Logo -->
      <a class="nav-logo" href="#">⚡ TechFlow</a>

      <!-- Navigation Links -->
      <ul class="nav-menu">
        <li><a href="#home" class="active">Home</a></li>

        <!-- Dropdown: Solutions -->
        <li class="has-dropdown">
          <a href="#">Solutions ▾</a>
          <ul class="dropdown">
            <li><a href="#">Web Development</a></li>
            <li><a href="#">Mobile Apps</a></li>
            <li><a href="#">Cloud Hosting</a></li>
            <li><a href="#">Data Analytics</a></li>
          </ul>
        </li>

        <li><a href="#pricing">Pricing</a></li>
        <li><a href="#blog">Blog</a></li>
        <li><a href="#about">About</a></li>
      </ul>

      <!-- CTA Buttons -->
      <div class="nav-cta">
        <a href="#login" class="btn-ghost">Log In</a>
        <a href="#signup" class="btn-primary">Start Free Trial</a>
      </div>

    </nav>
  </header>

  <!-- HERO SECTION (to demonstrate sticky navbar) -->
  <main>
    <section class="hero" id="home">
      <div class="hero-content">
        <h1>Build Faster.<br>Ship Smarter.</h1>
        <p>The all-in-one platform for modern development teams.</p>
        <a href="#" class="hero-btn">Get Started — It's Free</a>
      </div>
    </section>

    <section class="section-alt" id="pricing">
      <h2>Pricing</h2>
      <p>Scroll up to see the sticky navbar in action.</p>
    </section>

    <section class="section-plain" id="blog">
      <h2>Blog</h2>
      <p>Latest articles and tutorials.</p>
    </section>

    <section class="section-alt" id="about">
      <h2>About Us</h2>
      <p>Building tools developers love since 2019.</p>
    </section>
  </main>

</body>
</html>
```

### Project CSS

```css
/* header.css */

/* =====================
   RESET & BASE
   ===================== */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Segoe UI', Arial, sans-serif;
  color: #1a1a2e;
}

/* =====================
   STICKY SITE HEADER
   ===================== */
.site-header {
  position: sticky;
  top: 0;
  z-index: 1000;
  background-color: #0f0f1a;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.5);
}

/* =====================
   NAVBAR LAYOUT
   ===================== */
.navbar {
  display: flex;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;       /* centres the navbar content on wide screens */
  padding: 0 30px;
  height: 64px;         /* fixed navbar height */
}

/* =====================
   LOGO
   ===================== */
.nav-logo {
  color: #7c3aed;       /* purple */
  font-size: 22px;
  font-weight: 800;
  text-decoration: none;
  letter-spacing: -0.5px;
  margin-right: auto;   /* pushes menu and CTA to the right */
  white-space: nowrap;
}

/* =====================
   NAV MENU (ul)
   ===================== */
.nav-menu {
  list-style: none;
  display: flex;
  align-items: center;
  gap: 2px;
}

.nav-menu > li {
  position: relative;   /* anchor for dropdown */
}

.nav-menu > li > a {
  display: block;
  color: #cbd5e1;
  padding: 8px 14px;
  text-decoration: none;
  font-size: 14px;
  font-weight: 500;
  border-radius: 6px;
  transition: background-color 0.2s, color 0.2s;
  white-space: nowrap;
}

.nav-menu > li > a:hover {
  background-color: rgba(255, 255, 255, 0.07);
  color: white;
}

.nav-menu > li > a.active {
  color: white;
  background-color: rgba(124, 58, 237, 0.2);  /* subtle purple glow */
}

/* =====================
   DROPDOWN MENU
   ===================== */
.dropdown {
  display: none;                    /* hidden by default */
  position: absolute;
  top: calc(100% + 8px);            /* 8px gap below the parent link */
  left: 0;
  background-color: #1e1e30;
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 10px;
  min-width: 200px;
  padding: 8px 0;
  box-shadow: 0 8px 24px rgba(0,0,0,0.4);
  list-style: none;
  z-index: 100;
}

.dropdown li a {
  display: block;
  color: #94a3b8;
  padding: 10px 18px;
  text-decoration: none;
  font-size: 14px;
  transition: background-color 0.15s, color 0.15s;
}

.dropdown li a:hover {
  background-color: rgba(124,58,237,0.15);
  color: white;
}

/* Show dropdown when parent li is hovered */
.has-dropdown:hover .dropdown {
  display: block;
}

/* =====================
   CTA BUTTONS
   ===================== */
.nav-cta {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-left: 20px;
}

.btn-ghost {
  color: #94a3b8;
  padding: 7px 16px;
  text-decoration: none;
  font-size: 14px;
  font-weight: 500;
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 8px;
  transition: border-color 0.2s, color 0.2s;
  white-space: nowrap;
}

.btn-ghost:hover {
  border-color: rgba(255,255,255,0.3);
  color: white;
}

.btn-primary {
  background-color: #7c3aed;
  color: white;
  padding: 8px 18px;
  text-decoration: none;
  font-size: 14px;
  font-weight: 600;
  border-radius: 8px;
  transition: background-color 0.2s, transform 0.1s;
  white-space: nowrap;
}

.btn-primary:hover {
  background-color: #6d28d9;
  transform: translateY(-1px);
}

/* =====================
   HERO SECTION
   ===================== */
.hero {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(135deg, #0f0f1a 0%, #1a0533 50%, #0f0f1a 100%);
  text-align: center;
  padding: 40px 20px;
}

.hero-content h1 {
  font-size: 56px;
  font-weight: 900;
  color: white;
  line-height: 1.1;
  margin-bottom: 20px;
}

.hero-content p {
  font-size: 20px;
  color: #94a3b8;
  margin-bottom: 36px;
  max-width: 500px;
}

.hero-btn {
  display: inline-block;
  background-color: #7c3aed;
  color: white;
  padding: 16px 36px;
  border-radius: 10px;
  text-decoration: none;
  font-size: 16px;
  font-weight: 700;
  transition: background-color 0.2s, transform 0.2s;
}

.hero-btn:hover {
  background-color: #6d28d9;
  transform: translateY(-2px);
}

/* =====================
   OTHER SECTIONS
   ===================== */
.section-alt {
  min-height: 80vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #f8fafc;
  gap: 16px;
}

.section-plain {
  min-height: 80vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #fff;
  gap: 16px;
}

.section-alt h2,
.section-plain h2 {
  font-size: 32px;
  color: #1a1a2e;
}

.section-alt p,
.section-plain p {
  color: #64748b;
}
```

### Project Milestone Outputs

**Stage 1 (HTML only):** Plain unstyled text, bulleted list, bare links.

**Stage 2 (After navbar styles):** Dark sticky header with logo on the left, navigation links in the centre-right, and two buttons at the far right.

**Stage 3 (After dropdown):** Hovering over "Solutions" reveals a card-style dropdown with four sub-links.

**Stage 4 (After hero section):** A full-screen dark gradient hero section with large heading and a purple "Get Started" button.

**Stage 5 (Complete):** Scrolling down through the four sections while the navbar stays fixed at the top. The "Home" link has an active purple tint.

### Project Reflection Questions

1. The `.navbar` has `max-width: 1200px` and `margin: 0 auto`. What is the purpose of these two properties together? (They ensure that on very large screens, the navbar content doesn't stretch to the full screen width — it stays centred and readable at 1200px max.)

2. Why does `.nav-logo` have `margin-right: auto`? What would happen if you removed it? (It pushes the menu and CTA buttons to the right. Without it, the logo, links, and buttons would all cluster together on the left.)

3. The `.has-dropdown` uses `li:hover .dropdown`. Could you do this with CSS transitions to animate the dropdown appearing? How? (You could remove `display: none/block` and instead use `opacity: 0 → 1` + `visibility: hidden → visible` + a `transition: opacity` to fade it in. `display` cannot be transitioned directly.)

4. The `.site-header` has `position: sticky; top: 0`. Why does it also need `z-index: 1000`? (Without a z-index, the sticky header would be covered by content sections as you scroll, because those sections would naturally appear on top of it in the paint order.)

5. What single CSS change would convert this horizontal header into a vertical sidebar? (Change the `.navbar` to `flex-direction: column`, adjust widths and heights, and possibly change the dropdown to open to the right instead of downwards.)

---

## Part 13: Common Beginner Mistakes

### Mistake 1 — Forgetting `display: block` on `<a>` tags

**Wrong:**
```css
li a {
  color: white;
  padding: 12px 20px;   /* padding applies only to text area — hard to click */
  text-decoration: none;
}
```

**Correct:**
```css
li a {
  display: block;       /* the ENTIRE padded area becomes clickable */
  color: white;
  padding: 12px 20px;
  text-decoration: none;
}
```

---

### Mistake 2 — Forgetting to reset list styles

**Wrong (using raw `<ul>` without reset):**
The navbar shows bullet points and left indentation — it looks completely broken.

**Correct:**
```css
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
```

---

### Mistake 3 — Fixed navbar hiding page content

```css
/* The navbar is fixed, but content starts at the very top — hidden underneath! */
.navbar { position: fixed; top: 0; }

/* MISSING: compensate for the navbar height */
body { padding-top: 70px; }  /* add this — matches the navbar height */
```

---

### Mistake 4 — Dropdown disappears before you can click it

**The problem:** Dropdown disappears because there is a gap between the nav link and the dropdown, and hovering the gap triggers `mouseleave`.

**Cause:** `top: 100%` with a margin between the trigger and the dropdown.

**Fix:** Remove the gap entirely or use `top: calc(100% + 8px)` but also extend the parent's hover area to cover the gap with a transparent `::after` pseudo-element, or simply use `top: 100%` without a gap.

```css
/* Simple fix — no gap */
.dropdown {
  top: 100%;     /* no gap — the dropdown immediately connects to the trigger */
}
```

---

### Mistake 5 — Dropdown appearing behind other page content

```css
/* Dropdown is invisible because other elements are rendering above it */
.has-dropdown {
  position: relative;
  /* Missing z-index on the dropdown! */
}

.dropdown {
  position: absolute;
  z-index: 100;   /* ADD THIS — must be high enough to sit above page content */
}
```

---

### Mistake 6 — Using `float` for horizontal nav and forgetting `overflow: hidden` on the parent

```css
/* li items are floated and the parent ul collapses to zero height */
ul {
  background-color: #333;
  /* Missing: overflow: hidden; or a clearfix */
}

li { float: left; }
```

**Fix:**
```css
ul {
  background-color: #333;
  overflow: hidden;   /* or overflow: auto — forces ul to contain its floated children */
}
```

---

## Reflection Questions

1. Why is a `<ul>` list the correct HTML element to use as the foundation of a navbar? What would be wrong with using a `<div>` with `<span>` children instead?

2. You have a vertical navbar and the links are very hard to click — you have to click exactly on the tiny text. What single CSS property fixes this? (`display: block` on the `<a>` tags.)

3. A horizontal navbar has all its links clustered on the left, but you want the last link ("Sign Up") pushed to the far right. You are using Flexbox on the `<ul>`. What is the simplest CSS fix? (`margin-left: auto` on the last `<li>`.)

4. What is the difference between `position: fixed` and `position: sticky` for a navbar? When would you choose one over the other?

5. A dropdown menu works when you hover over it, but disappears the instant you move the mouse from the trigger link to the dropdown. What causes this and how do you fix it? (A gap between the link and the dropdown. Remove the gap so the dropdown directly connects to the trigger, maintaining the hover state.)

6. You add a sticky navbar to a page, but it does not appear to stick. What are two possible reasons? (The parent element might have `overflow: hidden` which prevents sticky from working; or the navbar's parent container does not have a defined height to scroll within.)

---

## Completion Checklist

- [ ] I understand why a `<ul>` list is the correct HTML structure for a navbar
- [ ] I can remove default list styles (bullets, margin, padding) as a starting point
- [ ] I understand why `display: block` on `<a>` tags is essential for proper click areas
- [ ] I can build a complete **vertical navbar** with hover and active states
- [ ] I can place a vertical navbar next to main content using Flexbox
- [ ] I can build a **horizontal navbar** using both `display: inline-block` and Flexbox methods
- [ ] I know when to use Flexbox vs `inline-block` for horizontal navbars
- [ ] I can push a single nav item (like a "Login" button) to the far right using `margin-left: auto`
- [ ] I can add a **logo** to the left and links to the right in a header layout
- [ ] I understand the difference between `position: fixed` and `position: sticky` navbars
- [ ] I can build a **dropdown submenu** using `position: absolute` and `:hover`
- [ ] I know why `position: relative` on the parent `<li>` is required for dropdowns
- [ ] I know why `z-index` is needed on dropdowns and sticky navbars
- [ ] I completed all four guided exercises
- [ ] I built the complete TechFlow website header mini-project
- [ ] I can identify and fix the six common beginner navbar mistakes

---

## Lesson Summary

A CSS navigation bar always starts the same way: a semantic `<nav>` element containing a `<ul>` list of `<li>` items, each holding an `<a>` link. The first CSS task is always to reset the default list styles with `list-style-type: none`, `margin: 0`, and `padding: 0`. The second task is always to set `display: block` on the `<a>` tags so the full padded area is clickable.

**Vertical navbars** stack links top to bottom and are ideal for dashboards and sidebars. The key properties are a fixed `width` on the `<ul>`, `display: block` on links, and Flexbox on the page body to place the sidebar alongside content.

**Horizontal navbars** place links side by side and are ideal for website headers. The cleanest modern approach is `display: flex` on the `<ul>`. A logo is placed before the `<ul>` in the flex container with `margin-right: auto` to push the links right. Individual links are pushed to the far right using `margin-left: auto` on a specific `<li>`.

**Dropdown menus** are built by nesting a second `<ul>` or `<div>` inside a `<li>`, setting `display: none` by default and `display: block` on the parent's `:hover`. The parent `<li>` needs `position: relative` and the dropdown needs `position: absolute`, `top: 100%`, and a `z-index` to sit above page content.

**Sticky navbars** use `position: sticky; top: 0` and need `z-index` to stay above all page content. **Fixed navbars** use `position: fixed; top: 0` and require `padding-top` on the body to prevent content hiding behind the navbar.

**Real World Uses of CSS Navbars:**
- Top horizontal header on almost every website
- Sidebar navigation in dashboards (Notion, Trello, Figma)
- Sticky headers that reveal on scroll on news sites and blogs
- Dropdown mega-menus on e-commerce sites (Amazon, Jumia)
- Mobile hamburger menus (built by toggling a class on the navbar)
- Tab-bar style horizontal navs in web applications
- Breadcrumb navigation showing the current page path
