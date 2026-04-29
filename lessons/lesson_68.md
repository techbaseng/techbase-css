---
render_with_liquid: false
title: "Lesson 68: CSS Media Queries"
nav_order: 68
---

# Lesson 68: CSS Media Queries

---

## Lesson Introduction

Have you ever opened a website on your phone and it looked completely different from how it looked on your laptop? The text was bigger, the menu changed into a hamburger icon, and the columns stacked on top of each other instead of sitting side by side. That magic is powered by **CSS Media Queries**.

A media query is a CSS technique that lets you write styles that only apply when certain conditions about the user's screen are true. Think of it as CSS with an "if" statement built in: *"If the screen is smaller than 600 pixels, use this CSS. Otherwise, use the normal CSS."*

This is the foundation of **responsive web design** — the ability to make one website that works beautifully on a phone, a tablet, a laptop, and a wide desktop monitor, all at once.

In Nigeria, where most internet users access the web on mobile phones — not desktops — knowing media queries is not optional. It is essential. If your website does not work well on a small screen, most of your audience will leave immediately.

---

### What You Will Learn

By the end of this lesson, you will be able to:

1. Explain what a media query is and why it exists
2. Write the correct `@media` rule syntax from memory
3. Use `min-width` and `max-width` to apply styles at different screen sizes
4. Combine multiple conditions using `and`, `not`, `only`, and `,` (comma)
5. Target specific media types (`screen`, `print`)
6. Check orientation (`landscape` vs `portrait`)
7. Understand mobile-first vs desktop-first design approaches
8. Build a responsive layout that adapts across phone, tablet, and desktop
9. Apply practical examples like changing menus, columns, font sizes, and hiding elements

---

## Prerequisite Concepts

Before continuing, make sure you are comfortable with these ideas:

**CSS Selectors and Properties:** You write CSS rules by targeting elements. Inside those rules you write property-value pairs like `color: red` or `font-size: 18px`.

**The `<meta viewport>` tag:** For media queries to work correctly on mobile devices, your HTML page must include this line inside the `<head>`:
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
Without this, a phone browser will zoom out the page to fit the whole desktop layout and your media queries won't trigger correctly. This tag tells the phone to use its actual screen width, not a pretend desktop width.

**CSS `display` property:** You already know that `display: none` hides an element and `display: block` shows it. Media queries make heavy use of this to show or hide elements on different screens.

**CSS units — `px`:** Pixels (`px`) are the unit you will use most often in media query breakpoints.

---

## Part 1: What Is a Media Query and Why Does It Exist?

### 1.1 — The Problem It Solves

Imagine you are building a news website for a Lagos-based media company. Your design has three columns sitting side by side on a desktop screen — one column for top stories, one for sports, one for entertainment.

On a phone with a 375px wide screen, those three columns would each be only about 120px wide. That is too narrow to read anything. The text would overflow, the images would shrink to thumbnails, and users would have a terrible experience.

Without media queries, you would need to build two completely separate websites — one for desktop, one for mobile. That was how websites used to work in the early 2000s. It was expensive, slow, and hard to maintain.

Media queries let you write **one** stylesheet that detects the screen size and automatically adjusts the layout. The three desktop columns collapse into a single full-width column on the phone. Same website, same HTML, different CSS rules triggered by the screen condition.

### 1.2 — The `@media` Rule

A media query is written with the `@media` keyword. Here is its basic structure:

```css
@media media-type and (media-feature) {
  /* CSS rules that apply ONLY when the condition is true */
}
```

Let us break down each part:

- `@media` — the keyword that starts every media query
- `media-type` — the kind of device (screen, print, etc.)
- `and` — a logical connector meaning "AND also"
- `(media-feature)` — the condition to check, such as the screen width
- `{ ... }` — inside here, you write normal CSS rules

> **Think of it like this:** `@media screen and (max-width: 600px)` reads in plain English as: *"If the user is on a screen AND the screen is at most 600 pixels wide, apply these styles."*

---

### 1.3 — Media Types

The `media-type` part tells CSS what kind of device to target. There are four types:

| Media Type | Targets |
|---|---|
| `screen` | Computer monitors, phones, tablets — any device with a screen |
| `print` | The page when it is being printed or in print preview mode |
| `all` | All media types (default if you omit the type) |
| `speech` | Screen readers that read content aloud |

In everyday web development, `screen` is by far the most commonly used. `print` is used to hide navigation bars, sidebars, and ads when someone prints a page — you only want the article content to appear on paper.

---

### 1.4 — Your First Media Query

**The simplest possible example:** Change the background colour based on screen width.

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      background-color: lightblue;  /* Default: large screens */
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 40px;
    }

    /* When screen is 600px wide or less */
    @media screen and (max-width: 600px) {
      body {
        background-color: lightyellow;  /* Small screens: yellow background */
      }
    }
  </style>
</head>
<body>
  <h1>Responsive Background</h1>
  <p>Resize the browser window and watch the background colour change!</p>
</body>
</html>
```

**Expected output in browser:**
- On a wide screen (more than 600px): light blue background
- On a narrow screen (600px or less, e.g. a phone): light yellow background

> **Try it yourself:** Open this in your browser and slowly drag the window narrower. At the moment the window crosses 600px wide, the background will switch from blue to yellow. That exact point where the style changes is called a **breakpoint**.

---

## Part 2: Media Features — What Conditions Can You Check?

### 2.1 — `max-width` and `min-width`

These are the two most important and commonly used media features. They check the **width of the viewport** (the browser window).

**`max-width`** — means "at most this width" or "up to and including this width"
```css
@media screen and (max-width: 600px) {
  /* Applied when screen is 600px or LESS */
}
```

**`min-width`** — means "at least this width" or "from this width and above"
```css
@media screen and (min-width: 768px) {
  /* Applied when screen is 768px or MORE */
}
```

**Analogy:** Think of `max-width: 600px` as a *"small screen"* filter — it catches phones and small windows. Think of `min-width: 768px` as a *"big screen"* filter — it catches tablets and desktops.

---

### 2.2 — `max-height` and `min-height`

You can also check the **height** of the viewport. This is less commonly used but still important:

```css
@media screen and (max-height: 500px) {
  /* Applied when screen height is 500px or less */
  /* Useful for landscape-orientation phones */
}
```

---

### 2.3 — `orientation`

This checks whether the device is being held **vertically** (portrait) or **horizontally** (landscape):

```css
@media screen and (orientation: portrait) {
  /* Phone held upright */
}

@media screen and (orientation: landscape) {
  /* Phone or tablet turned sideways */
}
```

**Real-world use:** Many apps and sites change their layout when you rotate your phone. The navigation bar might move from the bottom to the side in landscape mode.

---

### 2.4 — Example: Changing Layout Based on Width

**Scenario:** A Nigerian study platform wants to show exam tips in two columns on desktop but a single column on mobile.

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * { box-sizing: border-box; }

    body {
      font-family: Arial, sans-serif;
      margin: 20px;
    }

    .container {
      display: flex;
      gap: 20px;
    }

    .card {
      flex: 1;
      background-color: #e8f4e8;
      border: 2px solid #2c7a2c;
      border-radius: 8px;
      padding: 20px;
    }

    /* On screens 600px or narrower, stack the columns */
    @media screen and (max-width: 600px) {
      .container {
        flex-direction: column;  /* Stack vertically instead of side by side */
      }
    }
  </style>
</head>
<body>
  <h2>JAMB Exam Tips – Naija Scholars</h2>
  <div class="container">
    <div class="card">
      <h3>Mathematics</h3>
      <p>Practice algebra daily. Focus on quadratic equations, sequences, and sets.</p>
    </div>
    <div class="card">
      <h3>English Language</h3>
      <p>Read comprehension passages every day. Build vocabulary from past questions.</p>
    </div>
  </div>
</body>
</html>
```

**Expected output on wide screen (above 600px):**
Two green cards sitting side by side.

**Expected output on phone (600px or less):**
Two green cards stacked one on top of the other, each taking the full width.

> **Thinking prompt:** What happens at exactly 600px — is the column or the row layout applied? (Answer: The media query includes 600px, so at exactly 600px, the column layout applies.)

---

### 2.5 — Example: Changing Font Size for Readability

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
    }

    h1 {
      font-size: 36px;       /* Large heading on desktop */
      color: #1a3c6e;
    }

    p {
      font-size: 16px;       /* Normal body text on desktop */
      line-height: 1.7;
    }

    /* Smaller text on small screens */
    @media screen and (max-width: 480px) {
      h1 {
        font-size: 24px;     /* Reduced heading for phone */
      }

      p {
        font-size: 14px;     /* Slightly smaller body text */
      }
    }
  </style>
</head>
<body>
  <h1>Welcome to Eko News Daily</h1>
  <p>
    Lagos — The Federal Government has announced a new initiative to expand internet access
    to secondary schools across all 36 states and the FCT, starting from the 2025 academic year.
    The programme targets over 10,000 schools nationwide.
  </p>
</body>
</html>
```

**Expected output on desktop:** Large 36px heading, comfortable 16px body text.

**Expected output on phone (480px or less):** Heading shrinks to 24px, body text to 14px — still readable but not overwhelming the small screen.

---

## Part 3: Logical Operators — Combining Conditions

### 3.1 — The `and` Operator

Use `and` to combine two conditions that must **both** be true:

```css
/* Screen must be at least 600px AND at most 900px */
@media screen and (min-width: 600px) and (max-width: 900px) {
  body {
    background-color: #fff3cd;  /* Tablet range: yellow */
  }
}
```

This targets a specific **range** of screen widths. The style only applies between 600px and 900px — the tablet range.

---

### 3.2 — The Comma `,` Operator (OR)

A comma works like an **OR** — it applies the style if **either** condition is true:

```css
/* Applies to screens smaller than 400px OR if the device is in print mode */
@media screen and (max-width: 400px), print {
  .sidebar {
    display: none;
  }
}
```

---

### 3.3 — The `not` Operator

`not` inverts the condition — applies the style to everything that does NOT match:

```css
/* Apply to everything EXCEPT screens */
@media not screen {
  body {
    font-family: Georgia, serif;
  }
}
```

---

### 3.4 — The `only` Operator

`only` is used to hide styles from older browsers that do not support media queries. Modern browsers ignore it:

```css
@media only screen and (max-width: 600px) {
  /* Same behaviour in modern browsers */
}
```

> **Practical note:** In modern web development, `only` is rarely needed since all current browsers support media queries. You will mostly see `screen and (...)` without `only`.

---

### 3.5 — Example: Three Breakpoints (Phone, Tablet, Desktop)

This is the most important pattern in responsive design. Let us set three different background colours to visualise the three breakpoints:

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 40px 20px;
      transition: background-color 0.3s;
    }

    /* Default (Desktop): wide screens */
    body {
      background-color: #dce8ff;  /* Blue: desktop */
    }

    .label::after {
      content: "Desktop View (768px and above)";
    }

    /* Tablet: between 481px and 767px */
    @media screen and (max-width: 767px) {
      body {
        background-color: #d4edda;   /* Green: tablet */
      }
      .label::after {
        content: "Tablet View (481px – 767px)";
      }
    }

    /* Phone: 480px and below */
    @media screen and (max-width: 480px) {
      body {
        background-color: #ffe5d0;   /* Orange: phone */
      }
      .label::after {
        content: "Phone View (480px and below)";
      }
    }
  </style>
</head>
<body>
  <h2>Responsive Breakpoint Demo</h2>
  <p class="label"></p>
  <p>Resize this window slowly to see the background change at each breakpoint.</p>
</body>
</html>
```

**Expected output:**
- Wide window: blue background, text says "Desktop View"
- Between 481–767px: green background, text says "Tablet View"
- 480px and below: orange background, text says "Phone View"

> **Important technical note:** When you use `max-width` breakpoints like this, they work from largest to smallest. The last matching media query wins. The 480px query is more specific than the 767px query, so it overrides it correctly on phones.

---

## Part 4: The `print` Media Type

### 4.1 — Styling Pages for Print

When someone prints a web page (or uses browser print preview), you can apply completely different styles. The most common use cases are:

- Hide the navigation bar, sidebar, and footer
- Hide advertisements
- Make text darker and larger for paper reading
- Remove background colours (ink-saving)

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    /* Normal screen styles */
    nav {
      background-color: #1a3c6e;
      padding: 15px;
      color: white;
    }

    .article {
      max-width: 700px;
      margin: 20px auto;
      font-family: Arial, sans-serif;
      line-height: 1.8;
    }

    .ad-banner {
      background-color: #ffe082;
      padding: 20px;
      text-align: center;
      margin: 20px 0;
    }

    footer {
      background-color: #333;
      color: white;
      padding: 15px;
      text-align: center;
    }

    /* Print styles: hide everything except the article */
    @media print {
      nav, .ad-banner, footer {
        display: none;    /* Hidden when printing */
      }

      .article {
        margin: 0;
        font-size: 12pt; /* Use pt units for print */
        line-height: 1.6;
        color: black;
      }
    }
  </style>
</head>
<body>
  <nav>Eko News Daily | Home | Politics | Sports | Business</nav>

  <div class="article">
    <h2>Lagos Expands Free WiFi to 50 New Locations</h2>
    <p>The Lagos State Government announced on Monday that it will expand its free public
    WiFi programme to 50 additional locations across the state, including markets,
    motor parks, and public parks. The initiative is expected to benefit over two million
    residents by the end of the year.</p>
  </div>

  <div class="ad-banner">
    🎉 ADVERTISEMENT: Shop the best deals at Naija Mall! 🎉
  </div>

  <footer>© 2024 Eko News Daily. All Rights Reserved.</footer>
</body>
</html>
```

**Expected output on screen:** Navigation, article, advertisement banner, and footer are all visible.

**Expected output in print preview (Ctrl+P):** Only the article content appears. The navigation, ad banner, and footer are completely hidden. This is clean, ink-efficient output.

---

## Part 5: Mobile-First vs Desktop-First Design

### 5.1 — The Two Approaches Explained

There are two common ways to write media queries:

**Desktop-first:** You write your default CSS for large screens, then use `max-width` queries to override for smaller screens.

**Mobile-first:** You write your default CSS for small screens, then use `min-width` queries to enhance for larger screens.

**Desktop-first pattern:**
```css
/* Default: desktop styles */
.column {
  width: 33%;
  float: left;
}

/* Override for phones */
@media screen and (max-width: 600px) {
  .column {
    width: 100%;
    float: none;
  }
}
```

**Mobile-first pattern:**
```css
/* Default: phone styles */
.column {
  width: 100%;
}

/* Enhance for desktop */
@media screen and (min-width: 600px) {
  .column {
    width: 33%;
    float: left;
  }
}
```

### 5.2 — Which Approach Is Better?

**Mobile-first is widely preferred in the industry** for several reasons:

1. Most users in Nigeria and globally now use mobile phones as their primary device
2. Starting small forces you to prioritise essential content
3. Browsers download and process CSS top-to-bottom — if a phone user's browser downloads the full desktop CSS first, it wastes data and processing time on styles it will never use
4. Google's search algorithm uses mobile-first indexing — mobile-friendly sites rank better

> **Real-world context:** In Nigeria, where mobile internet (and often expensive data plans) dominates, mobile-first is not just a good practice — it is a business necessity. A website that performs well on a 4G phone in Abuja will always perform well on a fibre connection in Lagos.

---

### 5.3 — Complete Mobile-First Example

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * { box-sizing: border-box; }

    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f9f9f9;
    }

    /* ===== MOBILE FIRST: Default styles for small screens ===== */

    header {
      background-color: #1a3c6e;
      color: white;
      padding: 15px 20px;
      text-align: center;
    }

    nav {
      background-color: #2c5fa5;
    }

    nav a {
      display: block;           /* Stack nav links vertically on mobile */
      color: white;
      padding: 12px 20px;
      text-decoration: none;
      border-bottom: 1px solid #1a3c6e;
    }

    nav a:hover {
      background-color: #1a3c6e;
    }

    .main-content {
      padding: 20px;
    }

    .card {
      background: white;
      border-radius: 8px;
      padding: 20px;
      margin-bottom: 16px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }

    .card h3 {
      color: #1a3c6e;
      margin-top: 0;
    }

    /* ===== TABLET: 600px and above ===== */
    @media screen and (min-width: 600px) {
      nav {
        display: flex;              /* Switch nav to horizontal row */
      }

      nav a {
        display: inline-block;
        border-bottom: none;
        border-right: 1px solid #1a3c6e;
        padding: 15px 20px;
      }

      .card-grid {
        display: grid;
        grid-template-columns: 1fr 1fr;   /* Two columns on tablet */
        gap: 16px;
      }

      .card {
        margin-bottom: 0;
      }
    }

    /* ===== DESKTOP: 1024px and above ===== */
    @media screen and (min-width: 1024px) {
      .main-content {
        max-width: 1100px;
        margin: 0 auto;
        padding: 30px;
      }

      .card-grid {
        grid-template-columns: 1fr 1fr 1fr;  /* Three columns on desktop */
      }

      header {
        text-align: left;
        padding: 20px 30px;
      }
    }
  </style>
</head>
<body>

  <header>
    <h1>Naija Tech Hub</h1>
  </header>

  <nav>
    <a href="#">Home</a>
    <a href="#">Courses</a>
    <a href="#">Events</a>
    <a href="#">Contact</a>
  </nav>

  <div class="main-content">
    <h2>Latest Courses</h2>
    <div class="card-grid">
      <div class="card">
        <h3>Web Development</h3>
        <p>Learn HTML, CSS, and JavaScript from scratch. Build real projects for Nigerian clients.</p>
      </div>
      <div class="card">
        <h3>Data Analysis</h3>
        <p>Use Excel and Python to analyse business data. Great for finance and banking careers.</p>
      </div>
      <div class="card">
        <h3>UI/UX Design</h3>
        <p>Design beautiful apps and websites. Master Figma and usability testing techniques.</p>
      </div>
    </div>
  </div>

</body>
</html>
```

**Expected output — Phone (below 600px):**
- Navigation links stacked vertically, full width
- Cards stacked in one column

**Expected output — Tablet (600px–1023px):**
- Navigation links in a horizontal row
- Cards in a two-column grid

**Expected output — Desktop (1024px and above):**
- Navigation links horizontal, content centred with max-width
- Cards in a three-column grid

---

## Part 6: More Practical Media Query Examples

### 6.1 — Show / Hide Elements at Different Sizes

A common pattern is to show a full navigation menu on desktop but hide it on mobile (replacing it with a "Menu" button, though in pure CSS you can at least hide/show alternatives).

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 20px; }

    /* Desktop nav: visible by default */
    .desktop-nav {
      background-color: #1a3c6e;
      padding: 10px 20px;
      display: flex;
      gap: 20px;
    }

    .desktop-nav a {
      color: white;
      text-decoration: none;
      font-size: 15px;
    }

    /* Mobile message: hidden by default on large screens */
    .mobile-msg {
      display: none;
      background-color: #1a3c6e;
      color: white;
      padding: 15px 20px;
      font-size: 15px;
      text-align: center;
    }

    /* On phones: hide the desktop nav, show the mobile message */
    @media screen and (max-width: 600px) {
      .desktop-nav {
        display: none;
      }

      .mobile-msg {
        display: block;
      }
    }
  </style>
</head>
<body>

  <nav class="desktop-nav">
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Services</a>
    <a href="#">Contact</a>
  </nav>

  <div class="mobile-msg">
    ☰ Open Menu (Mobile Navigation Here)
  </div>

  <h2>Welcome to Our Website</h2>
  <p>Resize the window below 600px to see the desktop navigation replaced by a mobile menu bar.</p>

</body>
</html>
```

**Expected output on wide screen:** Full horizontal navigation bar with all four links visible.
**Expected output on phone:** The nav bar is hidden; a simple mobile menu bar appears instead.

---

### 6.2 — Responsive Typography

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: 'Georgia', serif;
      margin: 0;
      padding: 20px;
      line-height: 1.8;
      color: #333;
    }

    h1 { font-size: 48px; color: #1a3c6e; }
    h2 { font-size: 32px; }
    p  { font-size: 18px; }

    @media screen and (max-width: 768px) {
      h1 { font-size: 32px; }
      h2 { font-size: 24px; }
      p  { font-size: 16px; }
      body { padding: 15px; }
    }

    @media screen and (max-width: 480px) {
      h1 { font-size: 24px; }
      h2 { font-size: 20px; }
      p  { font-size: 15px; }
      body { padding: 10px; }
    }
  </style>
</head>
<body>
  <h1>The Future of Fintech in Nigeria</h1>
  <h2>Digital Payments Are Reshaping the Economy</h2>
  <p>
    From Kano to Port Harcourt, Nigerians are embracing mobile banking and digital wallets.
    Companies like Flutterwave, Paystack, and PiggyVest have proven that world-class
    financial technology can be built right here in Lagos.
  </p>
</body>
</html>
```

**Expected output:** Headings and body text scale down proportionally at each breakpoint, remaining readable on all screen sizes without requiring zooming.

---

### 6.3 — Responsive Image Width

Images should never overflow their container on small screens. This is a one-line fix combined with a media query approach:

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 20px; }

    img {
      width: 100%;       /* Image fills its container, never overflows */
      height: auto;      /* Keep proportions correct */
      border-radius: 8px;
    }

    .image-container {
      max-width: 600px;   /* On desktop, cap the image at 600px */
    }

    /* On mobile, let the image go full width */
    @media screen and (max-width: 600px) {
      .image-container {
        max-width: 100%;
      }
    }
  </style>
</head>
<body>
  <h2>Eko Atlantic Beach Resort</h2>
  <div class="image-container">
    <!-- Replace with an actual image src in your project -->
    <img src="https://via.placeholder.com/600x300/1a3c6e/ffffff?text=Eko+Atlantic+Beach"
         alt="Eko Atlantic Beach Resort, Lagos">
  </div>
  <p>A stunning coastal resort in Victoria Island, Lagos.</p>
</body>
</html>
```

**Expected output:** The image takes up its natural width on desktop (capped at 600px) and fills the full screen width on phones — never overflowing or requiring horizontal scrolling.

---

## Part 7: Guided Practice Exercises

### Exercise 1 — Responsive Colours and Text

**Objective:** Create a page where the background colour and heading size change at two breakpoints.

**Scenario:** You are building a quick dashboard widget for a fintech startup. The colour scheme changes based on how the analyst is viewing it — desktop blue, tablet green, mobile orange.

**Steps:**
1. Create an HTML page with `<meta viewport>` in the head
2. Add a `<div class="dashboard">` with a heading "Transaction Summary" and a paragraph with sample data
3. Set default (desktop) background to `#d6eaf8` (light blue), heading to 32px
4. Add a media query for max-width 768px: background `#d5f5e3` (light green), heading 26px
5. Add a media query for max-width 480px: background `#fde8d8` (light orange), heading 22px

**Full Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * { box-sizing: border-box; }

    .dashboard {
      font-family: Arial, sans-serif;
      padding: 30px;
      background-color: #d6eaf8;    /* Default: desktop blue */
      min-height: 200px;
      border-radius: 10px;
      max-width: 700px;
      margin: 20px auto;
    }

    .dashboard h2 {
      font-size: 32px;              /* Desktop heading */
      color: #1a3c6e;
      margin-top: 0;
    }

    @media screen and (max-width: 768px) {
      .dashboard {
        background-color: #d5f5e3;  /* Tablet: green */
      }
      .dashboard h2 {
        font-size: 26px;
      }
    }

    @media screen and (max-width: 480px) {
      .dashboard {
        background-color: #fde8d8;  /* Phone: orange */
        padding: 20px;
      }
      .dashboard h2 {
        font-size: 22px;
      }
    }
  </style>
</head>
<body>
  <div class="dashboard">
    <h2>Transaction Summary</h2>
    <p>Total transactions today: <strong>4,821</strong></p>
    <p>Successful: <strong>4,709</strong> &nbsp;|&nbsp; Failed: <strong>112</strong></p>
    <p>Revenue: <strong>₦ 38,450,000</strong></p>
  </div>
</body>
</html>
```

**Self-check questions:**
- At 769px, which background colour shows — blue or green?
- At 480px exactly, which background colour shows — green or orange?
- What would happen if you switched the order of the two media queries in the CSS?

---

### Exercise 2 — Show and Hide Elements Across Screen Sizes

**Objective:** Build a page with different content visible at different screen sizes.

**Scenario:** A Lagos restaurant website has a full promotional banner on desktop but replaces it with a simple text notice on mobile (to save space and load faster).

**Steps:**
1. Create a `.promo-banner` div with a colourful full-width banner and promotional text
2. Create a `.promo-mobile` paragraph with a simpler text version
3. By default: show `.promo-banner`, hide `.promo-mobile`
4. At max-width 600px: hide `.promo-banner`, show `.promo-mobile`

**Full Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * { box-sizing: border-box; }
    body { font-family: Arial, sans-serif; margin: 0; }

    /* Desktop promotional banner */
    .promo-banner {
      background: linear-gradient(135deg, #ff6b35, #f7931e);
      color: white;
      padding: 40px 30px;
      text-align: center;
    }

    .promo-banner h2 {
      font-size: 36px;
      margin: 0 0 10px 0;
    }

    .promo-banner p {
      font-size: 18px;
      margin: 0;
    }

    /* Mobile-only compact notice: hidden by default */
    .promo-mobile {
      display: none;
      background-color: #ff6b35;
      color: white;
      text-align: center;
      padding: 12px;
      font-size: 15px;
      font-weight: bold;
    }

    /* Main content */
    .content {
      padding: 20px;
    }

    /* Switch at 600px */
    @media screen and (max-width: 600px) {
      .promo-banner {
        display: none;         /* Hide big banner on phone */
      }

      .promo-mobile {
        display: block;        /* Show compact notice on phone */
      }
    }
  </style>
</head>
<body>

  <!-- Big desktop banner -->
  <div class="promo-banner">
    <h2>🍛 Grand Opening Weekend!</h2>
    <p>Visit Mama Chidi's Restaurant in Ikeja this Saturday & Sunday for 30% off all meals.</p>
  </div>

  <!-- Compact mobile notice -->
  <p class="promo-mobile">🍛 30% Off This Weekend at Mama Chidi's, Ikeja!</p>

  <div class="content">
    <h3>Today's Menu Highlights</h3>
    <p>Egusi soup with eba, Jollof rice with grilled chicken, Pepper soup, Suya platter.</p>
  </div>

</body>
</html>
```

**Expected output on desktop:** Full orange gradient banner with large heading and description.
**Expected output on phone:** Compact single-line orange notice; the large banner is gone.

---

### Exercise 3 — Responsive Three-Column Grid

**Objective:** Build a product listing that adapts from three columns (desktop) to two columns (tablet) to one column (phone).

**Scenario:** An online shop selling Nigerian fashion items in Lagos.

**Full Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * { box-sizing: border-box; }

    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
      background-color: #fafafa;
    }

    h2 { color: #333; text-align: center; }

    .product-grid {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;  /* Default: 3 columns */
      gap: 20px;
      max-width: 1100px;
      margin: 0 auto;
    }

    .product-card {
      background: white;
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
    }

    .product-card .img-placeholder {
      height: 160px;
      background-color: #1a3c6e;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-size: 14px;
    }

    .product-card .info {
      padding: 14px;
    }

    .product-card h4 {
      margin: 0 0 6px 0;
      color: #333;
    }

    .product-card .price {
      color: #cc4400;
      font-weight: bold;
      font-size: 16px;
    }

    /* Tablet: 2 columns */
    @media screen and (max-width: 768px) {
      .product-grid {
        grid-template-columns: 1fr 1fr;
      }
    }

    /* Phone: 1 column */
    @media screen and (max-width: 480px) {
      .product-grid {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <h2>Abuja Fashion House — Collections</h2>
  <div class="product-grid">
    <div class="product-card">
      <div class="img-placeholder">Ankara Dress</div>
      <div class="info">
        <h4>Ankara Wrap Dress</h4>
        <p>Traditional fabric, modern cut</p>
        <span class="price">₦12,500</span>
      </div>
    </div>
    <div class="product-card">
      <div class="img-placeholder">Agbada Set</div>
      <div class="info">
        <h4>Senator Agbada Set</h4>
        <p>Embroidered, premium fabric</p>
        <span class="price">₦28,000</span>
      </div>
    </div>
    <div class="product-card">
      <div class="img-placeholder">Iro & Buba</div>
      <div class="info">
        <h4>Iro & Buba (Aso-oke)</h4>
        <p>Hand-woven, ceremonial grade</p>
        <span class="price">₦35,000</span>
      </div>
    </div>
  </div>
</body>
</html>
```

**Expected output — Desktop (769px and above):** Three product cards side by side.
**Expected output — Tablet (481–768px):** Two cards per row.
**Expected output — Phone (480px and below):** One card per row, full width.

---

## Part 8: Code Challenges

These challenges are adapted from the W3Schools CSS Media Queries challenge set.

---

### Challenge 1

**Task:** Change the `background-color` of the `<body>` element to `lightblue` when the screen width is 600px or less.

```html
<!-- Starting code -->
<style>
  body {
    background-color: white;
    /* Add your media query below */
  }
</style>
<body><h1>Hello</h1></body>
```

**Solution:**

```html
<style>
  body {
    background-color: white;
  }

  @media screen and (max-width: 600px) {
    body {
      background-color: lightblue;
    }
  }
</style>
```

---

### Challenge 2

**Task:** Use a media query to change the `font-size` of the `<h1>` element to `20px` when the screen is 400px or narrower.

```html
<!-- Starting code -->
<style>
  h1 {
    font-size: 36px;
  }
  /* Add your media query here */
</style>
<h1>Responsive Heading</h1>
```

**Solution:**

```html
<style>
  h1 {
    font-size: 36px;
  }

  @media screen and (max-width: 400px) {
    h1 {
      font-size: 20px;
    }
  }
</style>
<h1>Responsive Heading</h1>
```

---

### Challenge 3

**Task:** Hide the element with class `extra` when the screen width is less than 700px.

```html
<!-- Starting code -->
<style>
  .extra {
    display: block;
    background: lightyellow;
    padding: 10px;
  }
  /* Add your media query here */
</style>
<p class="extra">This is extra content hidden on small screens.</p>
```

**Solution:**

```html
<style>
  .extra {
    display: block;
    background: lightyellow;
    padding: 10px;
  }

  @media screen and (max-width: 699px) {
    .extra {
      display: none;
    }
  }
</style>
<p class="extra">This is extra content hidden on small screens.</p>
```

---

### Challenge 4

**Task:** Use a media query to set `font-size` to `30px` when the browser **width** is between `600px` and `900px` (inclusive on both ends).

**Solution:**

```html
<style>
  p {
    font-size: 16px;
  }

  @media screen and (min-width: 600px) and (max-width: 900px) {
    p {
      font-size: 30px;
    }
  }
</style>
<p>This text changes size on tablet-width screens.</p>
```

---

### Challenge 5

**Task:** Use a media query to change the `background-color` to `pink` when the document is in **print mode** (when the page is printed).

**Solution:**

```html
<style>
  body {
    background-color: white;
  }

  @media print {
    body {
      background-color: pink;
    }
  }
</style>
```

---

### Challenge 6

**Task:** Apply styles when the screen is in **landscape orientation** (wider than it is tall): make the `<body>` background `#e0ffe0`.

**Solution:**

```html
<style>
  body {
    background-color: white;
  }

  @media screen and (orientation: landscape) {
    body {
      background-color: #e0ffe0;
    }
  }
</style>
```

---

## Part 9: Mini Project — Naija News Responsive Website

**Project name:** Naija News — A Fully Responsive News Homepage

**Goal:** Build a complete, three-breakpoint responsive news homepage that works on phone, tablet, and desktop — using everything covered in this lesson.

---

### Stage 1: Mobile Base (Default styles — phone first)

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Naija News Daily</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      color: #333;
    }

    /* ======= HEADER ======= */
    header {
      background-color: #cc0000;
      color: white;
      padding: 15px 20px;
      text-align: center;
    }

    header h1 {
      font-size: 24px;
      letter-spacing: 1px;
    }

    header p {
      font-size: 12px;
      opacity: 0.85;
      margin-top: 4px;
    }

    /* ======= NAVIGATION ======= */
    nav {
      background-color: #1a1a1a;
    }

    nav a {
      display: block;
      color: #ccc;
      padding: 12px 20px;
      text-decoration: none;
      font-size: 14px;
      border-bottom: 1px solid #333;
    }

    nav a:hover {
      background-color: #333;
      color: white;
    }

    /* ======= MAIN LAYOUT ======= */
    .page-wrapper {
      padding: 16px;
    }

    /* ======= NEWS CARDS ======= */
    .news-grid {
      display: grid;
      grid-template-columns: 1fr;   /* One column on phone */
      gap: 16px;
      margin-bottom: 20px;
    }

    .news-card {
      background: white;
      border-radius: 6px;
      overflow: hidden;
      box-shadow: 0 2px 6px rgba(0,0,0,0.08);
    }

    .news-card .category {
      background-color: #cc0000;
      color: white;
      font-size: 11px;
      font-weight: bold;
      padding: 4px 10px;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    .news-card .card-body {
      padding: 16px;
    }

    .news-card h3 {
      font-size: 16px;
      margin-bottom: 8px;
      line-height: 1.4;
    }

    .news-card p {
      font-size: 13px;
      color: #666;
      line-height: 1.6;
    }

    .news-card .meta {
      font-size: 11px;
      color: #999;
      margin-top: 10px;
    }

    /* ======= SIDEBAR (stacked below on mobile) ======= */
    .sidebar {
      background: white;
      border-radius: 6px;
      padding: 16px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.08);
    }

    .sidebar h4 {
      font-size: 14px;
      text-transform: uppercase;
      letter-spacing: 1px;
      color: #cc0000;
      border-bottom: 2px solid #cc0000;
      padding-bottom: 6px;
      margin-bottom: 12px;
    }

    .sidebar ul {
      list-style: none;
      padding: 0;
    }

    .sidebar ul li {
      padding: 8px 0;
      font-size: 13px;
      border-bottom: 1px solid #eee;
      color: #444;
    }

    /* ======= FOOTER ======= */
    footer {
      background-color: #1a1a1a;
      color: #aaa;
      text-align: center;
      padding: 16px;
      margin-top: 20px;
      font-size: 12px;
    }
  </style>
</head>
<body>

  <header>
    <h1>📰 NAIJA NEWS DAILY</h1>
    <p>Nigeria's most trusted news source | Sunday, April 2025</p>
  </header>

  <nav>
    <a href="#">🏠 Home</a>
    <a href="#">🗳️ Politics</a>
    <a href="#">📈 Business</a>
    <a href="#">⚽ Sports</a>
    <a href="#">💡 Technology</a>
  </nav>

  <div class="page-wrapper">
    <div class="news-grid">

      <div class="news-card">
        <div class="category">Breaking</div>
        <div class="card-body">
          <h3>Federal Government Approves New Minimum Wage for Civil Servants</h3>
          <p>The FG has approved a new minimum wage following weeks of negotiations with
          labour unions across the country. The new rate takes effect immediately.</p>
          <div class="meta">By Emeka Eze | 2 hours ago</div>
        </div>
      </div>

      <div class="news-card">
        <div class="category">Business</div>
        <div class="card-body">
          <h3>Naira Strengthens Against Dollar as CBN Intervention Continues</h3>
          <p>The naira has gained ground against the US dollar for the third consecutive week
          following sustained intervention by the Central Bank of Nigeria.</p>
          <div class="meta">By Bola Adeyemi | 4 hours ago</div>
        </div>
      </div>

      <div class="news-card">
        <div class="category">Sports</div>
        <div class="card-body">
          <h3>Super Eagles Qualify for AFCON 2025 Quarterfinals</h3>
          <p>Nigeria's Super Eagles secured a 2–0 victory over their rivals in a
          commanding display that puts them firmly in the tournament's final eight.</p>
          <div class="meta">By Tunde Okonkwo | 6 hours ago</div>
        </div>
      </div>

    </div><!-- .news-grid -->

    <aside class="sidebar">
      <h4>Most Read Today</h4>
      <ul>
        <li>Lagos Traffic: New Flyover to Open Next Month</li>
        <li>Dangote Refinery Begins Petrol Distribution</li>
        <li>WAEC Results 2025: How to Check Your Score</li>
        <li>Funke Akindele's New Film Breaks Box Office Record</li>
        <li>CBN Raises Interest Rate to 26%</li>
      </ul>
    </aside>
  </div>

  <footer>
    © 2024 Naija News Daily Limited | Lagos, Nigeria | All Rights Reserved
  </footer>

</body>
</html>
```

**Milestone 1 output (phone):** Red header, stacked vertical nav links, one-column news cards, sidebar below cards.

---

### Stage 2: Add Tablet and Desktop Breakpoints

Add these media queries inside the `<style>` block, after all existing CSS:

```css
/* ======= TABLET: 600px and above ======= */
@media screen and (min-width: 600px) {

  header h1 {
    font-size: 32px;
  }

  /* Nav goes horizontal */
  nav {
    display: flex;
    flex-wrap: wrap;
  }

  nav a {
    display: inline-block;
    flex: 1;
    text-align: center;
    border-bottom: none;
    border-right: 1px solid #333;
    padding: 14px 10px;
  }

  /* Cards go 2 columns */
  .news-grid {
    grid-template-columns: 1fr 1fr;
  }
}

/* ======= DESKTOP: 1024px and above ======= */
@media screen and (min-width: 1024px) {

  header {
    text-align: left;
    padding: 20px 40px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  header h1 { font-size: 36px; }

  header p { font-size: 14px; }

  .page-wrapper {
    max-width: 1200px;
    margin: 0 auto;
    padding: 24px 40px;
    display: grid;
    grid-template-columns: 2fr 1fr;   /* Main content : sidebar side by side */
    gap: 30px;
    align-items: start;
  }

  /* Cards go 3 columns */
  .news-grid {
    grid-template-columns: 1fr 1fr;   /* Still 2 wide — 3rd stacks below */
  }

  /* First card spans both columns — hero story */
  .news-card:first-child {
    grid-column: 1 / -1;
  }

  .news-card:first-child h3 {
    font-size: 22px;
  }

  .news-card p {
    font-size: 14px;
  }
}

/* ======= PRINT ======= */
@media print {
  nav, footer, .sidebar {
    display: none;
  }

  header {
    background-color: white;
    color: black;
    text-align: left;
    padding: 10px 0;
    border-bottom: 2px solid black;
  }

  .page-wrapper {
    display: block;
    padding: 0;
  }

  .news-card {
    box-shadow: none;
    border: 1px solid #ddd;
    margin-bottom: 10px;
    break-inside: avoid;
  }

  .news-card .category {
    background-color: black;
  }
}
```

**Final milestone output:**

- **Phone:** Red header centred, vertical nav, one-column cards, sidebar below
- **Tablet:** Header with larger title, horizontal nav, two-column card grid
- **Desktop:** Left-aligned header with date right-aligned, sidebar moves beside the articles, first card acts as a full-width hero story
- **Print:** Only the news articles show; nav, sidebar, and footer disappear

---

### Optional Extensions

- Add a media query that changes the navigation background to dark green when the screen is in **landscape** orientation on a small device
- Use `@media screen and (min-width: 1440px)` to add a max-width cap and centre the layout on very wide monitors
- Experiment with what happens when you use `not screen` — what kind of device would your normal styles apply to?

---

## Common Beginner Mistakes

### Mistake 1 — Missing the `<meta viewport>` Tag

**Wrong — media queries don't trigger on mobile phones:**
```html
<head>
  <title>My Site</title>
  <!-- No viewport meta tag -->
</head>
```

**Why it fails:** Without the viewport meta, mobile browsers zoom out to show the full "desktop" version of the page. The viewport width appears to be 980px even on a 375px phone screen. Your `max-width: 480px` query never fires because the browser thinks the screen is 980px wide.

**Correct:**
```html
<head>
  <title>My Site</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
```

---

### Mistake 2 — Wrong Order of Media Queries (Desktop-First)

**Wrong:**
```css
@media screen and (max-width: 480px) {
  body { background-color: orange; }
}

@media screen and (max-width: 768px) {
  body { background-color: green; }
}
```

**Why it fails:** At 400px wide, both queries match. The `max-width: 768px` query comes last so it overrides the `max-width: 480px` query. On phones, you would get green instead of orange — not what you intended.

**Correct (largest max-width first):**
```css
@media screen and (max-width: 768px) {
  body { background-color: green; }
}

@media screen and (max-width: 480px) {
  body { background-color: orange; }  /* Overrides green on small phones */
}
```

> **Rule:** For `max-width` queries (desktop-first), write them from **largest to smallest**. For `min-width` queries (mobile-first), write them from **smallest to largest**.

---

### Mistake 3 — Forgetting Parentheses Around Media Features

**Wrong:**
```css
@media screen and max-width: 600px {  /* No parentheses! */
  body { background: blue; }
}
```

**Why it fails:** The browser cannot parse this. The entire media query block is ignored silently — no error shown, no style applied.

**Correct:**
```css
@media screen and (max-width: 600px) {
  body { background: blue; }
}
```

---

### Mistake 4 — Using `px` in `and` Conditions With `min`/`max` the Wrong Way

**Wrong (logic error):**
```css
/* This targets screens smaller than 400px AND larger than 800px */
/* Impossible — no screen can be both at the same time */
@media screen and (max-width: 400px) and (min-width: 800px) {
  body { background: red; }
}
```

**Why it fails:** A screen cannot be less than 400px AND greater than 800px simultaneously. This rule will never apply.

**Correct (targets screens between 400px and 800px):**
```css
@media screen and (min-width: 400px) and (max-width: 800px) {
  body { background: red; }
}
```

---

### Mistake 5 — Writing Media Queries Outside the `<style>` Block or Before the Opening CSS

**Wrong:**
```css
@media screen and (max-width: 600px) {
  body { color: red; }
}

body {
  color: black;   /* This always wins because it comes after the media query! */
}
```

**Why it fails:** The regular `body { color: black; }` rule comes after the media query in the file. CSS cascade means the last rule for the same selector and property wins. The media query colour is overridden by the rule below it.

**Correct — put your default styles BEFORE your media queries:**
```css
body {
  color: black;   /* Default */
}

@media screen and (max-width: 600px) {
  body { color: red; }   /* Overrides only on small screens */
}
```

---

## Reflection Questions

1. You are building a website for a Lagos street food vendor. Most of their customers will visit on cheap Android phones. Which approach — mobile-first or desktop-first — would you choose, and why?

2. Explain in simple language what `@media screen and (min-width: 768px) and (max-width: 1024px)` means. What range of devices would it target?

3. A classmate removes the `<meta name="viewport">` tag from their page. They test on their laptop and everything looks fine. But on a phone, the media queries do not work. Why?

4. You want to change the `font-size` of a heading to `18px` only on screens smaller than `500px`. Write the complete CSS code.

5. What is the difference between `max-width` and `min-width` in a media query? Give a real-life analogy.

6. A print media query hides the navigation, sidebar, and footer. Why is this important? Who benefits from this?

7. You want styles to apply when the phone is held in landscape mode. Which media feature do you use and what value do you set?

---

## Completion Checklist

Before moving to the next lesson, confirm that you can do all of the following:

- [ ] I can explain what a media query is in plain language
- [ ] I always include `<meta name="viewport">` in my HTML head
- [ ] I know the full syntax: `@media media-type and (feature) { }`
- [ ] I know the four media types: `screen`, `print`, `all`, `speech`
- [ ] I can use `max-width` to apply styles on small screens
- [ ] I can use `min-width` to apply styles on large screens
- [ ] I can target a range using `and` with both `min-width` and `max-width`
- [ ] I understand the difference between mobile-first and desktop-first approaches
- [ ] I can use `orientation: landscape` and `orientation: portrait`
- [ ] I can use `@media print` to style pages for printing
- [ ] I can show and hide elements at different breakpoints using `display: none` and `display: block`
- [ ] I know the correct order for media queries (large-to-small for `max-width`)
- [ ] I completed all exercises and the mini project
- [ ] I can identify and fix the five common mistakes listed in this lesson

---

## Lesson Summary

CSS Media Queries are the engine of responsive web design. They give your stylesheet the ability to ask questions about the user's device and respond with different styles depending on the answers.

The core tool is the `@media` rule. You specify a **media type** (`screen`, `print`) and one or more **media features** (`max-width`, `min-width`, `orientation`) connected by logical operators (`and`, `not`, `,`). Any CSS inside the query block only applies when all conditions are true.

The most important media features for everyday responsive design are `max-width` (for desktop-first) and `min-width` (for mobile-first). Common breakpoints used by most developers are around 480px (phone), 768px (tablet), and 1024px (desktop), though you should choose breakpoints based on your content rather than specific device models.

In Nigeria's mobile-dominant internet landscape, the mobile-first approach is especially important. Write your default styles for small screens, then progressively enhance for larger ones using `min-width` media queries. Always include the `<meta viewport>` tag — without it, your media queries will not work on real mobile devices.

---

## Quick Reference Card

| Syntax | What It Does |
|---|---|
| `@media screen and (max-width: 600px) { }` | Styles for screens 600px or narrower |
| `@media screen and (min-width: 768px) { }` | Styles for screens 768px or wider |
| `@media screen and (min-width: 600px) and (max-width: 900px) { }` | Styles for 600–900px range |
| `@media print { }` | Styles applied when printing |
| `@media screen and (orientation: portrait) { }` | Phone held upright |
| `@media screen and (orientation: landscape) { }` | Device turned sideways |
| `@media not screen { }` | Everything except screens |
| `@media screen and (...), print { }` | Screen OR print (comma = OR) |
| Common breakpoints | Phone: ≤480px / Tablet: ≤768px / Desktop: ≥1024px |
| Mobile-first uses | `min-width` (start small, scale up) |
| Desktop-first uses | `max-width` (start large, scale down) |
| Always required | `<meta name="viewport" content="width=device-width, initial-scale=1.0">` |

---

*End of Lesson 68 — CSS Media Queries*
