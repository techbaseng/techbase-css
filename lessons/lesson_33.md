---
render_with_liquid: false
title: "CSS Dropdowns — Building Hidden Menus That Appear on Hover"
nav_order: 33
---

# Lesson 33 — CSS Dropdowns

---

## Lesson Introduction

Think about the navigation bar at the top of almost every professional website — Amazon, Google, GitHub, any news site. When you hover over a menu item, a panel of extra options slides down beneath it. That panel is a **dropdown**. It stays hidden until you need it, and appears right when you hover.

This is one of the most practical, most commonly built UI components in web development. The good news: you can build a fully functional, styled dropdown menu using **only HTML and CSS** — no JavaScript required.

In this lesson you will learn:
- What a CSS dropdown is and how the hover mechanism works
- How to build a simple text dropdown on a `<div>` element
- How to build a dropdown on a styled button
- How to build a dropdown navigation menu inside a `<nav>` bar
- How to build a **dropdown content box** that contains an image and descriptive text (not just links)
- How to control the exact position of the dropdown content
- How to add a right-aligned dropdown
- How to combine all of these into a complete, real-world navigation bar with multiple dropdowns

By the end of this lesson, you will be able to build the kind of dropdown menus seen on real professional websites, from scratch, with clean CSS.

---

## Prerequisite Concepts

Before building dropdowns, make sure you are comfortable with these four CSS concepts that power every dropdown you will ever build.

### 1. The `display` Property — Showing and Hiding Elements

The `display` property controls whether an element is visible and takes up space on the page.

```css
/* Hide an element completely — takes up NO space */
.hidden {
  display: none;
}

/* Show it again as a block */
.visible {
  display: block;
}
```

**This is the ON/OFF switch for dropdowns.** The dropdown content starts with `display: none` and switches to `display: block` when triggered.

---

### 2. The `:hover` Pseudo-class — Reacting to Mouse Movement

`:hover` is a CSS pseudo-class that applies styles **only while the user's cursor is on top of an element**.

```css
/* When the user hovers over a button, change its background colour */
button:hover {
  background-color: blue;
}
```

**This is the trigger for dropdowns.** When the user hovers over the trigger element, we use `:hover` to show the dropdown content.

---

### 3. `position: relative` and `position: absolute` — Placing the Dropdown Panel

These two positioning values work as a team to place the dropdown panel exactly where you want it.

- `position: relative` on the **parent/wrapper**: "This element is the anchor. Measure from here."
- `position: absolute` on the **dropdown content**: "Place me at an exact position relative to my nearest `position: relative` ancestor."

```css
.wrapper {
  position: relative;  /* The anchor point */
}

.dropdown-content {
  position: absolute;  /* Positioned relative to .wrapper */
  top: 100%;           /* Start just below the wrapper (100% of wrapper's height) */
  left: 0;             /* Align left edge with wrapper's left edge */
}
```

**This is how the dropdown panel appears directly below its trigger** — instead of floating somewhere random on the page.

---

### 4. The Descendant Combinator for Hover — The Magic Link

This is the CSS pattern that makes everything work together:

```css
/* WHEN .dropdown is hovered → SHOW .dropdown-content inside it */
.dropdown:hover .dropdown-content {
  display: block;
}
```

Read this as: "When the element with class `dropdown` is being hovered, find the element with class `dropdown-content` that lives **inside** it, and set its display to block."

This is the core pattern behind every pure CSS dropdown.

---

## Part 1 — The Basic Hover Dropdown

Let's build the simplest possible dropdown: a text element that reveals a panel of links when hovered.

### Understanding the Structure

A CSS dropdown always has this two-part structure:

```
[Trigger element]          ← the thing you hover over
  └── [Dropdown content]   ← the hidden panel that appears
```

Both are wrapped in a **container** that has `position: relative`.

### Example 1 — The Simplest Dropdown (Text Trigger)

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* ── 1. The outer wrapper ─────────────────────────
       position: relative makes this the anchor for the
       absolutely-positioned dropdown panel below       */
    .dropdown {
      position: relative;
      display: inline-block;   /* shrink-wrap to content width */
    }

    /* ── 2. The dropdown panel ────────────────────────
       Starts hidden. Positioned absolutely so it floats
       directly below the trigger without pushing
       other content down                               */
    .dropdown-content {
      display: none;             /* HIDDEN by default */
      position: absolute;        /* floats above page flow */
      background-color: #f9f9f9;
      min-width: 160px;
      box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
      z-index: 1;                /* ensures it appears above other elements */
    }

    /* ── 3. Links inside the dropdown panel ──────────*/
    .dropdown-content a {
      color: black;
      padding: 12px 16px;
      text-decoration: none;
      display: block;            /* makes each link its own full row */
    }

    /* ── 4. Hover effect on the links ────────────────*/
    .dropdown-content a:hover {
      background-color: #ddd;
    }

    /* ── 5. THE KEY RULE: show the panel on hover ────
       When .dropdown is hovered → .dropdown-content
       inside it switches from display:none to
       display:block                                   */
    .dropdown:hover .dropdown-content {
      display: block;
    }
  </style>
</head>
<body>

  <h2>Hover over the text below:</h2>

  <div class="dropdown">
    <span>Hover over me ▼</span>   <!-- the trigger text -->

    <div class="dropdown-content">  <!-- the hidden panel -->
      <a href="#">Link 1</a>
      <a href="#">Link 2</a>
      <a href="#">Link 3</a>
    </div>
  </div>

</body>
</html>
```

**Expected Output:**

Before hover:
```
Hover over me ▼
(nothing else visible)
```

After hovering over "Hover over me ▼":
```
Hover over me ▼
┌──────────────────┐
│ Link 1           │
│ Link 2           │
│ Link 3           │
└──────────────────┘
```

---

**Breaking down every single line — nothing skipped:**

**`.dropdown { position: relative; display: inline-block; }`**
This is the outer wrapper. `position: relative` is crucial — it tells CSS "when the dropdown panel inside uses `position: absolute`, measure its position from me." `display: inline-block` makes the wrapper only as wide as its content, so multiple dropdowns can sit side by side.

**`.dropdown-content { display: none; }`**
The panel starts invisible. `display: none` removes it from the page entirely — it takes up zero space and is completely invisible.

**`position: absolute;`**
The panel is lifted out of the normal page flow. It won't push content below it down when it appears. It hovers above everything else.

**`z-index: 1;`**
This ensures the dropdown panel appears **on top of** any other elements it might overlap. Think of it like layers in a photo editor — `z-index` controls which layer is on top.

**`.dropdown-content a { display: block; }`**
By default, `<a>` links are `inline` — they'd all appear on one line. Setting `display: block` makes each link fill the full width of the panel, creating a proper vertical menu look.

**`.dropdown:hover .dropdown-content { display: block; }`**
This is the magic line. It means: "When `.dropdown` is hovered, find the `.dropdown-content` inside it and set `display: block`." This overrides the `display: none` that was hiding the panel, making it instantly visible.

> **💡 Why does the panel stay visible while hovering over the links?** Because the links are *inside* `.dropdown`. When you move your cursor from the trigger text down to a link, your cursor is still hovering over `.dropdown` (the wrapper) — so the hover state is maintained and the panel stays open.

> **🤔 Thinking prompt:** What would happen if you removed `position: relative` from `.dropdown`? The dropdown panel would use `position: absolute` but with no relative parent — it would be positioned relative to the browser window instead, and appear in the wrong place entirely.

---

### Example 2 — Dropdown on a Styled Button

In practice, you almost always want the trigger to look like a button. This is the same mechanism, just with a `<button>` element styled as the trigger.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* The trigger button */
    .dropbtn {
      background-color: #4CAF50;   /* green */
      color: white;
      padding: 16px;
      font-size: 16px;
      border: none;
      cursor: pointer;
    }

    /* Hover and focus state for the trigger button */
    .dropbtn:hover,
    .dropbtn:focus {
      background-color: #3e8e41;   /* darker green on hover */
    }

    /* The wrapper */
    .dropdown {
      position: relative;
      display: inline-block;
    }

    /* The hidden panel */
    .dropdown-content {
      display: none;
      position: absolute;
      background-color: #f9f9f9;
      min-width: 160px;
      box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
      z-index: 1;
    }

    /* Links in the panel */
    .dropdown-content a {
      color: black;
      padding: 12px 16px;
      text-decoration: none;
      display: block;
    }

    .dropdown-content a:hover {
      background-color: #f1f1f1;
    }

    /* Show the panel when the wrapper is hovered */
    .dropdown:hover .dropdown-content {
      display: block;
    }
  </style>
</head>
<body>

  <div class="dropdown">
    <button class="dropbtn">Dropdown ▼</button>
    <div class="dropdown-content">
      <a href="#">Link 1</a>
      <a href="#">Link 2</a>
      <a href="#">Link 3</a>
    </div>
  </div>

</body>
</html>
```

**Expected Output:**

Before hover:
```
[ Dropdown ▼ ]  (green button)
```

After hovering:
```
[ Dropdown ▼ ]
┌─────────────────┐
│ Link 1          │
│ Link 2          │
│ Link 3          │
└─────────────────┘
```

**What changed from Example 1?**
- The trigger is now a `<button class="dropbtn">` instead of a plain `<span>` — giving us a real styled button.
- We added `.dropbtn:focus` styling so keyboard users who tab to the button also see a visual response.
- The hover colours are green and a darker green for the active state.

> **🌍 Real-world connection:** This button dropdown pattern is used everywhere — "Account" menus, "Settings" dropdowns, "Share" buttons, and language/currency selectors on e-commerce sites.

---

## Part 2 — Dropdown Inside a Navigation Bar

Now we will place a dropdown inside a proper horizontal navigation bar — the pattern you'll use on virtually every real website project.

### Example 3 — Navbar with a Dropdown Menu

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* ── Reset ─────────────────────────────────────── */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    /* ── The navigation bar container ─────────────── */
    .navbar {
      overflow: hidden;             /* clears floated children */
      background-color: #333;
    }

    /* ── Regular navbar links ──────────────────────── */
    .navbar a {
      float: left;                  /* line up links horizontally */
      font-size: 16px;
      color: white;
      text-align: center;
      padding: 14px 16px;
      text-decoration: none;
    }

    /* ── The dropdown wrapper inside the navbar ────── */
    .navbar .dropdown {
      float: left;                  /* lines up with the other nav links */
      overflow: hidden;
    }

    /* ── The dropdown trigger button (styled like nav links) */
    .navbar .dropdown .dropbtn {
      font-size: 16px;
      border: none;
      outline: none;
      color: white;
      padding: 14px 16px;
      background-color: inherit;    /* matches the navbar background */
      font-family: inherit;
      margin: 0;
      cursor: pointer;
    }

    /* ── Hover state for nav links and dropdown trigger */
    .navbar a:hover,
    .navbar .dropdown:hover .dropbtn {
      background-color: red;
    }

    /* ── The dropdown panel ─────────────────────────── */
    .dropdown-content {
      display: none;
      position: absolute;
      background-color: #f9f9f9;
      min-width: 160px;
      box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
      z-index: 1;
    }

    /* ── Links inside the dropdown panel ─────────────── */
    .dropdown-content a {
      float: none;                  /* override the float from .navbar a */
      color: black;
      padding: 12px 16px;
      text-decoration: none;
      display: block;
      text-align: left;
    }

    /* ── Hover state for links in the panel ──────────── */
    .dropdown-content a:hover {
      background-color: #ddd;
    }

    /* ── Show the dropdown panel on hover ────────────── */
    .dropdown:hover .dropdown-content {
      display: block;
    }
  </style>
</head>
<body>

  <div class="navbar">
    <a href="#">Home</a>
    <a href="#">News</a>
    <div class="dropdown">
      <button class="dropbtn">Dropdown ▼</button>
      <div class="dropdown-content">
        <a href="#">Link 1</a>
        <a href="#">Link 2</a>
        <a href="#">Link 3</a>
      </div>
    </div>
  </div>

  <h3 style="padding: 20px;">Hover over "Dropdown" in the navbar above.</h3>

</body>
</html>
```

**Expected Output:**

Before hover:
```
[ Home ]  [ News ]  [ Dropdown ▼ ]     ← dark grey navbar
```

After hovering "Dropdown ▼":
```
[ Home ]  [ News ]  [ Dropdown ▼ ]     ← "Dropdown ▼" turns red
                    ┌─────────────────┐
                    │ Link 1          │
                    │ Link 2          │
                    │ Link 3          │
                    └─────────────────┘
```

**Key lines explained:**

**`float: left`** on `.navbar a` and `.navbar .dropdown` — This is how the nav links line up horizontally across the bar. Without float, they would stack vertically.

**`overflow: hidden`** on `.navbar` — When child elements are floated, the parent collapses to zero height. `overflow: hidden` on the parent forces it to expand and contain its floated children.

**`background-color: inherit`** on `.dropbtn` — The button inherits the background colour of the navbar (`#333`), so it blends in and looks like a regular nav link rather than a separate styled button.

**`float: none`** on `.dropdown-content a` — The links inside the dropdown panel would otherwise inherit the `float: left` rule from `.navbar a`. We override this with `float: none` so the links stack vertically inside the panel, as expected.

---

## Part 3 — Advanced Dropdown: Image and Text Content

A dropdown doesn't have to contain just links. You can put **any HTML content** inside the panel — images, headings, paragraphs, cards. This is called a **mega dropdown** or **content dropdown**.

### Example 4 — Dropdown with an Image Card

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Wrapper */
    .dropdown {
      position: relative;
      display: inline-block;
    }

    /* Styled trigger button */
    .dropbtn {
      background-color: #4CAF50;
      color: white;
      padding: 16px;
      font-size: 16px;
      border: none;
      cursor: pointer;
    }

    .dropbtn:hover {
      background-color: #3e8e41;
    }

    /* Dropdown panel — wider to fit image + text */
    .dropdown-content {
      display: none;
      position: absolute;
      background-color: #f9f9f9;
      width: 200px;               /* wide enough for image */
      box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
      z-index: 1;
    }

    /* Style for any paragraph text inside the panel */
    .dropdown-content p {
      padding: 10px 14px;
      font-size: 14px;
      color: #555;
    }

    /* Style for any links inside the panel */
    .dropdown-content a {
      padding: 10px 14px;
      display: block;
      text-decoration: none;
      color: #333;
    }

    .dropdown-content a:hover {
      background-color: #ddd;
    }

    /* Image fills full width of the panel */
    .dropdown-content img {
      width: 100%;
    }

    /* Show panel on hover */
    .dropdown:hover .dropdown-content {
      display: block;
    }
  </style>
</head>
<body>

  <div class="dropdown">
    <button class="dropbtn">Our Products ▼</button>

    <div class="dropdown-content">
      <!-- An image at the top of the panel -->
      <img src="https://via.placeholder.com/200x100?text=Product+Image" alt="Product">

      <!-- Descriptive text below the image -->
      <p>Discover our latest collection of tech accessories.</p>

      <!-- Links below the text -->
      <a href="#">Laptops</a>
      <a href="#">Tablets</a>
      <a href="#">Accessories</a>
    </div>
  </div>

</body>
</html>
```

**Expected Output after hover:**
```
[ Our Products ▼ ]
┌──────────────────────┐
│ [Product Image 200px]│
│ Discover our latest  │
│ collection of tech   │
│ accessories.         │
│ Laptops              │
│ Tablets              │
│ Accessories          │
└──────────────────────┘
```

**Key insight:** The `dropdown-content` div is just a normal `<div>` that is hidden by default. You can put **anything** inside it — images, paragraphs, forms, grids of cards. The only CSS rules that matter are `display: none` (hidden) and `display: block` (shown on hover). Everything else is up to you.

---

## Part 4 — Right-Aligned Dropdown

By default, the dropdown panel aligns its **left edge** with the left edge of the trigger. If your trigger is near the right side of the screen, the panel might overflow off-screen. You can fix this by aligning the **right edge** of the panel instead.

### Example 5 — Right-Aligned Dropdown Panel

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .dropdown {
      position: relative;
      display: inline-block;
    }

    .dropbtn {
      background-color: #3498db;
      color: white;
      padding: 14px 20px;
      font-size: 16px;
      border: none;
      cursor: pointer;
      border-radius: 4px;
    }

    .dropbtn:hover {
      background-color: #2980b9;
    }

    .dropdown-content {
      display: none;
      position: absolute;
      right: 0;             /* ← RIGHT-aligned: panel's right edge = wrapper's right edge */
      background-color: #f9f9f9;
      min-width: 160px;
      box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
      z-index: 1;
    }

    .dropdown-content a {
      color: black;
      padding: 12px 16px;
      text-decoration: none;
      display: block;
    }

    .dropdown-content a:hover {
      background-color: #ddd;
    }

    .dropdown:hover .dropdown-content {
      display: block;
    }
  </style>
</head>
<body>

  <!-- Push the dropdown to the right side of the page for demonstration -->
  <div style="text-align: right; padding: 20px;">
    <div class="dropdown">
      <button class="dropbtn">Account ▼</button>
      <div class="dropdown-content">
        <a href="#">My Profile</a>
        <a href="#">Settings</a>
        <a href="#">Sign Out</a>
      </div>
    </div>
  </div>

</body>
</html>
```

**Expected Output (panel aligns to the right):**
```
                              [ Account ▼ ]
                    ┌─────────────────────┐
                    │ My Profile          │
                    │ Settings            │
                    │ Sign Out            │
                    └─────────────────────┘
                              ↑ right edge aligned with button
```

**The key difference:** `right: 0` instead of `left: 0`.

- `left: 0` — panel's left edge aligns with the wrapper's left edge (default, opens to the right)
- `right: 0` — panel's right edge aligns with the wrapper's right edge (opens to the left)

> **🌍 Real-world connection:** The "Account" or "Profile" dropdown in the top-right corner of websites like GitHub, Twitter/X, and Amazon always uses `right: 0` so the panel doesn't overflow off-screen to the right.

---

## Part 5 — Dropdown Button Highlight Stays Active

There is one subtle detail worth teaching: when the user's mouse moves from the trigger button down into the dropdown panel, we want the trigger button to **stay highlighted**. We achieve this because the entire `.dropdown` wrapper is still hovered — the panel is inside it.

But what if we want the button itself to have a distinct "active" colour? We need to match the hover state of both the button and the panel trigger at the same time:

```css
/* Keep the button highlighted while the panel is open */
.dropdown:hover .dropbtn {
  background-color: #3e8e41;   /* stays the darker green */
}
```

This selector reads: "When `.dropdown` is being hovered, style the `.dropbtn` inside it." This keeps the button looking "pressed" the whole time the panel is open.

---

## Guided Practice Exercises

### Exercise 1 — Warm-Up: Your First Dropdown

**Objective:** Build the basic dropdown from scratch without looking at the examples.

**Scenario:** You are building a small settings widget. Create a button labelled "Settings ⚙" that reveals three options when hovered: "Edit Profile", "Change Password", and "Logout".

**Requirements:**
- The trigger must be a styled button with a blue background (`#2196F3`)
- The panel must have a white background and a subtle shadow
- Each option must highlight grey on hover
- The panel must appear directly below the button

**Starter HTML (fill in the CSS):**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Write your CSS here */

    .dropbtn {
      /* Style the button: blue background, white text, padding, no border */
    }

    .dropdown {
      /* Make it the position anchor and inline */
    }

    .dropdown-content {
      /* Hidden by default, absolute position, white bg, shadow, z-index */
    }

    .dropdown-content a {
      /* Each option: block display, black text, padding, no underline */
    }

    .dropdown-content a:hover {
      /* Light grey background on hover */
    }

    .dropdown:hover .dropdown-content {
      /* Show the panel */
    }
  </style>
</head>
<body>
  <div class="dropdown">
    <button class="dropbtn">Settings ⚙</button>
    <div class="dropdown-content">
      <a href="#">Edit Profile</a>
      <a href="#">Change Password</a>
      <a href="#">Logout</a>
    </div>
  </div>
</body>
</html>
```

**Expected Output after hover:**
```
[ Settings ⚙ ]  (blue button)
┌──────────────────┐
│ Edit Profile     │
│ Change Password  │
│ Logout           │
└──────────────────┘
```

**Self-check Questions:**
1. What happens if you forget `position: relative` on `.dropdown`?
2. What does `z-index: 1` do, and when would you need a higher value?
3. Why must `.dropdown-content a` have `display: block`?

---

### Exercise 2 — Navbar with Two Dropdowns

**Objective:** Build a nav bar with two separate dropdowns.

**Scenario:** You are building a portfolio website. The navigation needs: Home (plain link), Projects (dropdown), Blog (plain link), Contact (dropdown).

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    .navbar {
      background-color: #2c3e50;
      overflow: hidden;
    }

    .navbar a, .navbar .dropbtn {
      float: left;
      color: white;
      text-align: center;
      padding: 14px 18px;
      text-decoration: none;
      font-size: 15px;
      font-family: Arial, sans-serif;
      background: none;
      border: none;
      cursor: pointer;
    }

    .navbar a:hover, .navbar .dropdown:hover .dropbtn {
      background-color: #e74c3c;
    }

    .navbar .dropdown {
      float: left;
      overflow: hidden;
    }

    .dropdown-content {
      display: none;
      position: absolute;
      background-color: #34495e;
      min-width: 160px;
      z-index: 1;
      box-shadow: 0 8px 16px rgba(0,0,0,0.3);
    }

    .dropdown-content a {
      float: none;
      color: #ecf0f1;
      padding: 12px 16px;
      text-decoration: none;
      display: block;
      text-align: left;
      font-size: 14px;
    }

    .dropdown-content a:hover {
      background-color: #e74c3c;
      color: white;
    }

    .dropdown:hover .dropdown-content {
      display: block;
    }
  </style>
</head>
<body>

  <div class="navbar">
    <a href="#">Home</a>

    <div class="dropdown">
      <button class="dropbtn">Projects ▼</button>
      <div class="dropdown-content">
        <a href="#">Web Design</a>
        <a href="#">Mobile Apps</a>
        <a href="#">Data Projects</a>
      </div>
    </div>

    <a href="#">Blog</a>

    <div class="dropdown">
      <button class="dropbtn">Contact ▼</button>
      <div class="dropdown-content">
        <a href="#">Email Me</a>
        <a href="#">LinkedIn</a>
        <a href="#">GitHub</a>
      </div>
    </div>
  </div>

  <p style="padding: 20px; font-family: Arial;">
    Hover over "Projects" or "Contact" to see the dropdowns.
  </p>

</body>
</html>
```

**Expected Output:**
```
[ Home ]  [ Projects ▼ ]  [ Blog ]  [ Contact ▼ ]   ← dark blue bar

Hovering "Projects ▼":
                ┌──────────────────┐
                │ Web Design       │
                │ Mobile Apps      │
                │ Data Projects    │
                └──────────────────┘

Hovering "Contact ▼":
                              ┌──────────────────┐
                              │ Email Me         │
                              │ LinkedIn         │
                              │ GitHub           │
                              └──────────────────┘
```

**Self-check Questions:**
1. Why do we need `float: none` on `.dropdown-content a`?
2. If you removed `overflow: hidden` from `.navbar`, what would happen?
3. How could you make both dropdowns right-aligned?

---

### Exercise 3 — Dropdown with Mixed Content (Image + Links)

**Objective:** Build a dropdown that contains a featured image and links — like a "Featured Product" panel.

**Your task:** Build a "Shop" button dropdown that shows:
- A placeholder product image at the top
- A short tagline paragraph
- Three category links: Electronics, Clothing, Books

Use the structure from Example 4 but style it with your own colour palette (try a dark theme: dark grey panel, white text, orange hover).

**Expected Output after hover:**
```
[ Shop ▼ ]
┌────────────────────────┐
│  [Product Banner img]  │
│  New arrivals this     │
│  season — shop now!    │
│ Electronics            │
│ Clothing               │
│ Books                  │
└────────────────────────┘
```

**Hints:**
- Set `.dropdown-content` width to `220px`
- Set `.dropdown-content img { width: 100%; display: block; }`
- For a dark theme: `background-color: #2c2c2c`, link colour `#eee`
- Orange hover: `background-color: #e67e22`

---

## Mini Project — Complete E-Commerce Navigation Bar

You will now build a fully styled, multi-dropdown navigation bar for a fictional online store called **"ShopNow"**. It includes plain links, two dropdown menus, and a right-aligned account dropdown.

---

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html>
<head>
  <title>ShopNow — Navigation</title>
  <link rel="stylesheet" href="shopnow-nav.css">
</head>
<body>

  <nav class="topnav">

    <!-- Logo / Brand -->
    <a href="#" class="brand">🛒 ShopNow</a>

    <!-- Plain nav links -->
    <a href="#">Home</a>
    <a href="#">Deals</a>

    <!-- Dropdown 1: Categories -->
    <div class="dropdown">
      <button class="dropbtn">Categories ▼</button>
      <div class="dropdown-content">
        <a href="#">Electronics</a>
        <a href="#">Clothing &amp; Fashion</a>
        <a href="#">Books &amp; Stationery</a>
        <a href="#">Home &amp; Kitchen</a>
        <a href="#">Sports &amp; Outdoors</a>
      </div>
    </div>

    <!-- Dropdown 2: Brands (with image card) -->
    <div class="dropdown">
      <button class="dropbtn">Brands ▼</button>
      <div class="dropdown-content brands-panel">
        <img src="https://via.placeholder.com/220x80?text=Featured+Brands" alt="Brands">
        <p>Shop top-rated brands at unbeatable prices.</p>
        <a href="#">Apple</a>
        <a href="#">Samsung</a>
        <a href="#">Nike</a>
        <a href="#">Sony</a>
      </div>
    </div>

    <a href="#">Contact</a>

    <!-- Right-aligned Account Dropdown -->
    <div class="dropdown right-dropdown">
      <button class="dropbtn account-btn">My Account ▼</button>
      <div class="dropdown-content account-panel">
        <a href="#">👤 Profile</a>
        <a href="#">📦 My Orders</a>
        <a href="#">❤️ Wishlist</a>
        <hr style="border-color: #eee;">
        <a href="#" style="color: #e74c3c;">🚪 Sign Out</a>
      </div>
    </div>

  </nav>

  <div style="padding: 30px; font-family: Arial;">
    <h2>Welcome to ShopNow!</h2>
    <p>Hover over the navigation items above to explore the dropdowns.</p>
  </div>

</body>
</html>
```

---

### Stage 2 — The CSS (`shopnow-nav.css`)

```css
/* ── Reset ──────────────────────────────────────── */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, sans-serif;
}

/* ── Navigation bar container ───────────────────── */
.topnav {
  background-color: #1a1a2e;
  overflow: hidden;
  display: flex;              /* use flex for easy alignment */
  align-items: center;
}

/* ── Brand / Logo ────────────────────────────────── */
.topnav .brand {
  font-size: 20px;
  font-weight: bold;
  color: #e94560;
  padding: 14px 20px;
  text-decoration: none;
  white-space: nowrap;
}

/* ── Regular nav links ───────────────────────────── */
.topnav a {
  color: #ccc;
  padding: 14px 16px;
  text-decoration: none;
  font-size: 15px;
  display: block;
}

.topnav a:hover {
  background-color: #e94560;
  color: white;
}

/* ── Dropdown wrapper ────────────────────────────── */
.topnav .dropdown {
  position: relative;   /* anchor for the absolute panel */
}

/* ── Dropdown trigger button ─────────────────────── */
.topnav .dropdown .dropbtn {
  background-color: inherit;   /* blends into navbar */
  color: #ccc;
  padding: 14px 16px;
  font-size: 15px;
  border: none;
  cursor: pointer;
  font-family: inherit;
  white-space: nowrap;
}

/* Highlight trigger button when dropdown is open */
.topnav .dropdown:hover .dropbtn {
  background-color: #e94560;
  color: white;
}

/* ── Dropdown panel ──────────────────────────────── */
.dropdown-content {
  display: none;
  position: absolute;
  top: 100%;           /* appears directly below the navbar */
  left: 0;
  background-color: #ffffff;
  min-width: 200px;
  box-shadow: 0 8px 20px rgba(0,0,0,0.2);
  z-index: 100;
  border-top: 3px solid #e94560;   /* accent top border */
}

/* ── Links inside the panel ──────────────────────── */
.dropdown-content a {
  color: #333;
  padding: 11px 16px;
  text-decoration: none;
  display: block;
  font-size: 14px;
}

.dropdown-content a:hover {
  background-color: #f5f5f5;
  color: #e94560;
  padding-left: 22px;    /* subtle indent on hover */
  transition: padding-left 0.1s;
}

/* ── Brands panel: image + paragraph ─────────────── */
.brands-panel {
  width: 220px;
}

.brands-panel img {
  width: 100%;
  display: block;
}

.brands-panel p {
  padding: 10px 14px;
  font-size: 13px;
  color: #777;
  border-bottom: 1px solid #eee;
  margin-bottom: 4px;
}

/* ── Right-aligned Account dropdown ─────────────── */
.right-dropdown {
  margin-left: auto;    /* push to far right using flex auto margin */
}

.account-btn {
  color: #f0c040 !important;   /* gold colour for account button */
}

.account-panel {
  right: 0;    /* align panel's right edge to button's right edge */
  left: auto;
  min-width: 180px;
}

/* ── Show panel on hover ─────────────────────────── */
.dropdown:hover .dropdown-content {
  display: block;
}
```

---

### Stage 3 — Final All-in-One Version

For convenience, here is the complete project in a single HTML file:

```html
<!DOCTYPE html>
<html>
<head>
  <title>ShopNow — Navigation Bar</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: Arial, sans-serif; }

    .topnav {
      background-color: #1a1a2e;
      overflow: hidden;
      display: flex;
      align-items: center;
    }

    .topnav .brand {
      font-size: 20px; font-weight: bold; color: #e94560;
      padding: 14px 20px; text-decoration: none; white-space: nowrap;
    }

    .topnav a {
      color: #ccc; padding: 14px 16px; text-decoration: none;
      font-size: 15px; display: block;
    }
    .topnav a:hover { background-color: #e94560; color: white; }

    .topnav .dropdown { position: relative; }

    .topnav .dropdown .dropbtn {
      background-color: inherit; color: #ccc; padding: 14px 16px;
      font-size: 15px; border: none; cursor: pointer;
      font-family: inherit; white-space: nowrap;
    }
    .topnav .dropdown:hover .dropbtn { background-color: #e94560; color: white; }

    .dropdown-content {
      display: none; position: absolute; top: 100%; left: 0;
      background-color: #fff; min-width: 200px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.2);
      z-index: 100; border-top: 3px solid #e94560;
    }

    .dropdown-content a {
      color: #333; padding: 11px 16px; text-decoration: none;
      display: block; font-size: 14px;
    }
    .dropdown-content a:hover {
      background-color: #f5f5f5; color: #e94560;
      padding-left: 22px; transition: padding-left 0.1s;
    }

    .brands-panel { width: 220px; }
    .brands-panel img { width: 100%; display: block; }
    .brands-panel p {
      padding: 10px 14px; font-size: 13px; color: #777;
      border-bottom: 1px solid #eee; margin-bottom: 4px;
    }

    .right-dropdown { margin-left: auto; }
    .account-btn { color: #f0c040 !important; }
    .account-panel { right: 0; left: auto; min-width: 180px; }

    .dropdown:hover .dropdown-content { display: block; }
  </style>
</head>
<body>

  <nav class="topnav">
    <a href="#" class="brand">🛒 ShopNow</a>
    <a href="#">Home</a>
    <a href="#">Deals</a>

    <div class="dropdown">
      <button class="dropbtn">Categories ▼</button>
      <div class="dropdown-content">
        <a href="#">Electronics</a>
        <a href="#">Clothing &amp; Fashion</a>
        <a href="#">Books &amp; Stationery</a>
        <a href="#">Home &amp; Kitchen</a>
        <a href="#">Sports &amp; Outdoors</a>
      </div>
    </div>

    <div class="dropdown">
      <button class="dropbtn">Brands ▼</button>
      <div class="dropdown-content brands-panel">
        <img src="https://via.placeholder.com/220x80?text=Featured+Brands" alt="Brands">
        <p>Shop top-rated brands at unbeatable prices.</p>
        <a href="#">Apple</a>
        <a href="#">Samsung</a>
        <a href="#">Nike</a>
        <a href="#">Sony</a>
      </div>
    </div>

    <a href="#">Contact</a>

    <div class="dropdown right-dropdown">
      <button class="dropbtn account-btn">My Account ▼</button>
      <div class="dropdown-content account-panel">
        <a href="#">👤 Profile</a>
        <a href="#">📦 My Orders</a>
        <a href="#">❤️ Wishlist</a>
        <hr style="border-color:#eee; margin: 4px 0;">
        <a href="#" style="color:#e74c3c;">🚪 Sign Out</a>
      </div>
    </div>
  </nav>

  <div style="padding: 30px;">
    <h2>Welcome to ShopNow!</h2>
    <p style="margin-top: 10px; color: #666;">
      Hover over "Categories", "Brands", or "My Account" in the nav above.
    </p>
  </div>

</body>
</html>
```

**Final Milestone Output:**
```
🛒 ShopNow  Home  Deals  [Categories ▼]  [Brands ▼]  Contact     [My Account ▼]
(dark navy bar with red/orange accents)

Hovering "Categories ▼":
┌─────────────────────┐
│ Electronics         │
│ Clothing & Fashion  │
│ Books & Stationery  │
│ Home & Kitchen      │
│ Sports & Outdoors   │
└─────────────────────┘

Hovering "Brands ▼":
┌───────────────────────┐
│ [Featured Brands img] │
│ Shop top-rated brands │
│ Apple                 │
│ Samsung               │
│ Nike                  │
│ Sony                  │
└───────────────────────┘

Hovering "My Account ▼" (right side):
                  ┌──────────────────┐
                  │ 👤 Profile       │
                  │ 📦 My Orders     │
                  │ ❤️ Wishlist      │
                  │ ─────────────── │
                  │ 🚪 Sign Out      │
                  └──────────────────┘
```

**Reflection Questions:**
1. Why does the Account dropdown use `right: 0` while the others use `left: 0`?
2. What does `margin-left: auto` do to `.right-dropdown` inside a flex container?
3. Why do we use `z-index: 100` on the dropdown panel?
4. What would happen if you forgot `top: 100%` on `.dropdown-content`?

**Optional Advanced Extensions:**
- Add a smooth fade-in animation using CSS `opacity` and `transition`
- Add a `min-width: 100%` rule to make the panel at least as wide as the trigger button
- Make the navbar responsive: on mobile (under 600px), stack all items vertically and remove hover — use a checkbox hack or media queries
- Add a "New" badge next to one of the category links using a CSS `::after` pseudo-element

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting `position: relative` on the Wrapper

```css
/* WRONG: no position: relative on the wrapper */
.dropdown {
  display: inline-block;
  /* missing: position: relative */
}

.dropdown-content {
  display: none;
  position: absolute;
  top: 0; left: 0;   /* this now positions relative to the <body>! */
}
```

**What goes wrong:** The dropdown panel appears in the top-left corner of the browser window, not beneath the button.

**Fix:** Always add `position: relative` to the wrapper `.dropdown`.

---

### Mistake 2 — Putting the Hover Rule on the Wrong Element

```css
/* WRONG: hovering the panel itself, not the wrapper */
.dropdown-content:hover .dropdown-content {
  display: block;
}

/* CORRECT: hovering the WRAPPER reveals the CONTENT inside it */
.dropdown:hover .dropdown-content {
  display: block;
}
```

**What goes wrong:** The panel can never be shown — you can't hover over something that's already hidden.

---

### Mistake 3 — The Panel Disappears When Moving the Mouse from Trigger to Links

```html
<!-- WRONG: gap between trigger and panel -->
<button class="dropbtn">Menu</button>

<!-- A gap here (margin/padding) causes the mouse to leave .dropdown -->

<div class="dropdown-content">...</div>
```

```css
/* Fix: ensure no gap between trigger bottom and panel top */
.dropdown-content {
  position: absolute;
  top: 100%;    /* Starts exactly at the bottom of the wrapper — no gap */
  left: 0;
}
```

**What goes wrong:** If there is any gap between the bottom of the trigger and the top of the panel, the mouse leaves `.dropdown` as it passes through the gap, the hover state ends, and the panel disappears.

**Fix:** Always use `top: 100%` (no gap) or ensure the panel starts exactly where the trigger ends.

---

### Mistake 4 — Forgetting `float: none` on Links Inside a Navbar Dropdown

```css
/* In a float-based navbar, .navbar a has float: left */
.navbar a {
  float: left;   /* This applies to ALL <a> tags in .navbar */
}

/* So links in .dropdown-content also inherit float: left and stack horizontally! */

/* Fix: explicitly remove float inside the panel */
.dropdown-content a {
  float: none;   /* override the inherited float */
  display: block;
}
```

**What goes wrong:** All the dropdown links appear on one horizontal line instead of stacking vertically.

---

### Mistake 5 — Using `visibility: hidden` Instead of `display: none`

```css
/* WORKS but not ideal */
.dropdown-content {
  visibility: hidden;   /* element is invisible but STILL TAKES UP SPACE */
}

.dropdown:hover .dropdown-content {
  visibility: visible;
}

/* BETTER: use display: none so the panel takes up no space when hidden */
.dropdown-content {
  display: none;
}

.dropdown:hover .dropdown-content {
  display: block;
}
```

**What goes wrong with `visibility: hidden`:** The hidden panel still occupies space in the layout, which causes a large invisible empty area below your trigger button. Other content gets pushed down even though nothing appears there.

---

### Mistake 6 — The Dropdown Panel Goes Behind Other Content

```css
/* WRONG: no z-index, panel gets buried under other elements */
.dropdown-content {
  display: none;
  position: absolute;
  /* missing z-index */
}

/* FIX: give the panel a high enough z-index */
.dropdown-content {
  display: none;
  position: absolute;
  z-index: 100;   /* ensures it floats above everything else */
}
```

**What goes wrong:** Images, other `<div>` elements, or banners appear on top of the dropdown panel, making the links unreadable or hidden.

---

## Reflection Questions

1. **In your own words**, explain the two-part CSS pattern that makes a dropdown work. What property hides it, and what property + selector combination shows it?

2. **Why is `position: relative` needed on the wrapper** and `position: absolute` needed on the panel? What would break if you forgot one of these?

3. **What does `z-index: 1` (or higher) do**, and when would a dropdown need a very high `z-index` value?

4. **What is the difference between `left: 0` and `right: 0`** on the dropdown panel, and when would you use each?

5. **Why does the dropdown panel stay visible** while you move the mouse from the trigger button down to the links?

6. **In a float-based navbar**, why do we need `float: none` on `.dropdown-content a` when we never explicitly floated them?

7. **Name three types of content** (other than links) that you could put inside a dropdown panel and describe a real-world use case for each.

---

## Completion Checklist

Before moving to the next lesson, confirm you can do each of the following:

- [ ] Explain how `display: none` / `display: block` controls dropdown visibility
- [ ] Explain how `:hover` triggers the dropdown to show
- [ ] Explain why `position: relative` must be on the wrapper and `position: absolute` on the panel
- [ ] Build a simple dropdown on a plain text trigger from scratch
- [ ] Build a dropdown on a styled button trigger
- [ ] Place a dropdown inside a horizontal navbar
- [ ] Build a dropdown panel that contains an image and paragraph text (not just links)
- [ ] Create a right-aligned dropdown using `right: 0`
- [ ] Keep the trigger button highlighted while the dropdown panel is open
- [ ] Build the full ShopNow project navigation bar
- [ ] Identify and fix all six common beginner mistakes described in this lesson

---

## Lesson Summary

In this lesson, you built CSS dropdowns from the ground up — from the simplest text trigger all the way to a multi-dropdown e-commerce navigation bar.

**The Core Mechanism — Three CSS Rules You Must Memorise:**

```css
/* 1. The wrapper is the anchor */
.dropdown {
  position: relative;
  display: inline-block;
}

/* 2. The panel starts hidden and floats over content */
.dropdown-content {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 1;
}

/* 3. Show the panel when the wrapper is hovered */
.dropdown:hover .dropdown-content {
  display: block;
}
```

These three rules are the skeleton of every CSS dropdown in existence. Everything else is cosmetic.

**Quick Reference — All Dropdown Techniques Covered:**

| Technique | Key CSS |
|---|---|
| Basic hover dropdown | `.dropdown:hover .dropdown-content { display: block; }` |
| Button trigger | Style a `<button>` with `.dropbtn` class |
| Dropdown in navbar | `float: left` on wrapper, `float: none` on panel links |
| Content panel (image + text) | Any HTML inside `.dropdown-content` with `img { width: 100% }` |
| Right-aligned panel | `right: 0; left: auto` on `.dropdown-content` |
| Highlight trigger while open | `.dropdown:hover .dropbtn { background-color: ... }` |

**Real-World Significance:** CSS dropdowns power the navigation menus of the vast majority of websites on the internet — from personal portfolios to large e-commerce platforms. Mastering this pattern means you can build professional, interactive navigation menus without writing a single line of JavaScript.

---

*End of Lesson 33 — You are now ready to move on to CSS Image Galleries in Lesson 34!*
