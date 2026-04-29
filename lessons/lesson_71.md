---
render_with_liquid: false
title: "CSS Responsive Web Design (RWD)"
nav_order: 71
---

# CSS Responsive Web Design (RWD)

## Lesson Introduction

Have you ever visited a website on your phone and had to pinch, zoom, and scroll sideways just to read the text? Or visited a website that looked perfect on a laptop but had tiny, unreadable text on a mobile screen? That is the problem that **Responsive Web Design** (RWD) solves.

**Responsive Web Design** is a technique that makes your website automatically adjust its layout, text size, images, and videos to look great on any device — whether it is a large desktop monitor, a tablet, or a small smartphone. The page **responds** to the screen it is being displayed on.

In this lesson, you will learn all seven pillars of RWD:

1. **What RWD is** and why it exists
2. **The Viewport** — controlling how the browser scales your page
3. **Responsive Grid Views** — building flexible column layouts
4. **Media Queries** — applying different styles for different screen sizes
5. **Responsive Images** — making images scale properly
6. **Responsive Videos** — making videos fit any screen
7. **CSS Frameworks & Templates** — tools that make RWD faster

By the end of this lesson, you will be able to build a complete responsive webpage that looks great on any screen.

---

## Prerequisite Concepts

Before we begin, you need to be comfortable with:

- Basic HTML (elements, attributes, `<div>`, `<img>`, headings, paragraphs)
- Basic CSS (selectors, properties, values, `width`, `padding`, `border`)
- The CSS Box Model (content, padding, border, margin)
- `box-sizing: border-box` (from Lesson 67)

If you are not yet comfortable with these, review Lessons 60–67 first.

---

## Part 1 — What Is Responsive Web Design?

### The Problem: One Website, Many Screen Sizes

In the early days of the internet, everyone browsed the web on a desktop computer with a monitor. Web designers built pages for a fixed width — usually around 960px — and that was enough.

Today, people use the web on many different devices:

| Device | Typical Screen Width |
|---|---|
| Large desktop monitor | 1920px or wider |
| Standard laptop | 1280px – 1440px |
| Tablet (landscape) | 768px – 1024px |
| Tablet (portrait) | 600px – 768px |
| Smartphone | 320px – 480px |

If you build a website that is only designed for 1200px wide, it will look broken on a 375px phone — text will be tiny, images will overflow, and the user will have to scroll sideways. This is a terrible experience.

### The Solution: Responsive Web Design

**Responsive Web Design (RWD)** was introduced by web designer Ethan Marcotte in 2010. The core idea is:

> Instead of building separate websites for mobile and desktop, build ONE website that **responds** intelligently to the size of the screen it is displayed on.

RWD uses three core CSS techniques working together:

1. **Fluid grids** — layouts that use percentages instead of fixed pixels, so columns stretch and shrink
2. **Flexible images** — images that scale to fit their container
3. **Media queries** — CSS rules that apply only at certain screen widths

> 🌍 **Real World Fact:** As of today, more than 60% of all web traffic comes from mobile devices. Building a responsive website is not optional — it is a professional requirement.

---

## Part 2 — The Viewport

### What Is the Viewport?

The **viewport** is the visible area of a web page on your screen. It is the window through which you see the website.

On a desktop computer, the viewport is usually the entire browser window. On a phone, the viewport is the physical screen of the phone.

**The problem:** When smartphones first appeared, browsers tried to display websites by zooming out so the full desktop width (typically 980px) fit on the phone screen. This made the page look tiny and unreadable, even though the phone screen was only 375px wide.

The fix was the **viewport meta tag** — a line of HTML code that tells the browser: *"Don't zoom out and fake a wide screen. Use the actual device width."*

### The Viewport Meta Tag

This is the single most important line you add to every responsive webpage. It goes inside the `<head>` section of your HTML:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Line-by-line explanation:**

- `<meta>` — An HTML meta tag. It provides information about the page to the browser. It does not display anything visible on screen.
- `name="viewport"` — Identifies this as the viewport configuration instruction.
- `content="..."` — Contains the viewport settings as a comma-separated list.
- `width=device-width` — Sets the viewport width to be exactly the device's actual screen width. On a 375px phone, the viewport becomes 375px. On a 1440px laptop, it becomes 1440px.
- `initial-scale=1.0` — Sets the initial zoom level to 1 (100% — no zooming in or out when the page first loads).

### Example: The Difference Without and With the Viewport Tag

**WITHOUT the viewport tag:**

```html
<!DOCTYPE html>
<html>
<head>
  <!-- No viewport meta tag -->
  <title>No Viewport</title>
</head>
<body>
  <h1>Welcome to my website</h1>
  <p>This page has no viewport tag. On a phone, the browser will zoom out to show
  the full 980px-wide "virtual" page. Everything looks tiny.</p>
</body>
</html>
```

**On a phone:** The browser shows the page as if it were 980px wide, scaled down to fit the phone screen. Text appears tiny and unreadable.

**WITH the viewport tag:**

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>With Viewport</title>
</head>
<body>
  <h1>Welcome to my website</h1>
  <p>This page has the viewport tag. On a phone, the browser uses the
  actual screen width. Text is readable at a natural size.</p>
</body>
</html>
```

**On a phone:** The page uses the actual 375px screen width. Text is readable. This is the foundation of every responsive page.

> ✅ **Rule:** Every responsive webpage you build must have `<meta name="viewport" content="width=device-width, initial-scale=1.0">` in the `<head>`. Without it, none of your other responsive techniques will work correctly.

### Other Viewport Settings (for reference)

| Setting | What It Does |
|---|---|
| `width=device-width` | Use the device's actual screen width |
| `initial-scale=1.0` | Start at 100% zoom |
| `maximum-scale=1.0` | Prevent the user from zooming in (use with caution — bad for accessibility) |
| `user-scalable=no` | Prevent all zooming (avoid — harms accessibility) |

> 💡 **Tip:** Never use `user-scalable=no`. It prevents people with visual impairments from zooming in to read your content. The Web Content Accessibility Guidelines (WCAG) require that users can zoom the page.

---

## Part 3 — Responsive Grid Views

### What Is a Grid View?

A **grid view** is a way of dividing a webpage into invisible vertical columns that elements can sit inside. It is like having graph paper behind your page.

**Why use a grid?**

Without a grid, it is very hard to control where things sit on a page, especially across different screen sizes. A grid gives you a consistent, mathematical system for layout.

The most popular responsive grid system uses **12 columns**. Why 12? Because 12 is divisible by 1, 2, 3, 4, 6, and 12 — giving you many layout options:

```
12 columns = full width (one section)
6 + 6      = two equal halves (50% + 50%)
4 + 4 + 4  = three equal thirds
3 + 9      = sidebar + main content (25% + 75%)
4 + 8      = sidebar + main content (33% + 67%)
```

### Building a Simple Responsive Grid

The key insight is to use **percentages** instead of pixels for widths, so columns shrink and grow with the screen:

```css
/* First, always start with the box-sizing reset */
* {
  box-sizing: border-box;
}

/* Every column shares these base styles */
[class*="col-"] {
  float: left;        /* Place columns side by side */
  padding: 15px;      /* Inner spacing */
}

/* 12-column grid: each unit = 100% / 12 = 8.33% */
.col-1  { width: 8.33%; }
.col-2  { width: 16.66%; }
.col-3  { width: 25%; }
.col-4  { width: 33.33%; }
.col-5  { width: 41.66%; }
.col-6  { width: 50%; }
.col-7  { width: 58.33%; }
.col-8  { width: 66.66%; }
.col-9  { width: 75%; }
.col-10 { width: 83.33%; }
.col-11 { width: 91.66%; }
.col-12 { width: 100%; }

/* Row: contains columns and clears floats */
.row::after {
  content: "";
  display: table;
  clear: both;
}
```

**How does `[class*="col-"]` work?**

This is an **attribute selector**. The `*=` means "contains". So `[class*="col-"]` targets any element whose `class` attribute contains the text `col-`. This applies the shared styles to ALL column classes at once (col-1, col-2, col-3, etc.) without repeating code.

### Example: A Three-Column Layout Using the Grid

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
    }

    .row::after {
      content: "";
      display: table;
      clear: both;
    }

    [class*="col-"] {
      float: left;
      padding: 15px;
      border: 1px solid #ccc;
      background-color: #f9f9f9;
    }

    .col-4  { width: 33.33%; }
    .col-8  { width: 66.66%; }
    .col-12 { width: 100%; }
  </style>
</head>
<body>

  <!-- Header spans full width -->
  <div class="row">
    <div class="col-12" style="background:#333; color:white; text-align:center;">
      <h1>My Website</h1>
    </div>
  </div>

  <!-- Sidebar (4 cols) + Main content (8 cols) -->
  <div class="row">
    <div class="col-4">
      <h3>Sidebar</h3>
      <p>Navigation links, widgets, etc.</p>
    </div>
    <div class="col-8">
      <h3>Main Content</h3>
      <p>This is the main article area. It takes up 8 of 12 columns (66.66% width).</p>
    </div>
  </div>

  <!-- Footer spans full width -->
  <div class="row">
    <div class="col-12" style="background:#333; color:white; text-align:center;">
      <p>Footer © 2026</p>
    </div>
  </div>

</body>
</html>
```

**Expected output:**

```
┌─────────────────── My Website (full width) ──────────────────┐
├──────────────┬───────────────────────────────────────────────┤
│   Sidebar    │          Main Content                         │
│  (33.33%)    │          (66.66%)                             │
├──────────────┴───────────────────────────────────────────────┤
│            Footer (full width)                               │
└──────────────────────────────────────────────────────────────┘
```

> 💡 **Think about it:** On a wide desktop, this layout looks great. But what happens on a 375px phone? The sidebar becomes 33.33% of 375px = 125px — too narrow for readable text. This is where **media queries** come in (Part 4).

---

## Part 4 — Media Queries

### What Is a Media Query?

A **media query** is a CSS rule that applies styles **only when certain conditions are true** — specifically, when the browser's screen meets certain size requirements.

Think of it as an **if statement** for CSS:

> "IF the screen is narrower than 600px, THEN use these special styles."

This is the engine that powers responsive design. Without media queries, your page would look the same on every screen size.

### Media Query Syntax

```css
@media only screen and (max-width: 600px) {
  /* These styles ONLY apply when the screen is 600px wide or less */
  body {
    background-color: lightblue;
  }
}
```

**Every part explained:**

- `@media` — The at-rule that starts a media query block
- `only screen` — Applies only to screens (not printers, screen readers, etc.). `only` is optional but good practice.
- `and` — Combines conditions (you can chain multiple conditions)
- `(max-width: 600px)` — The condition: screen width must be 600px or less
- `{ ... }` — The CSS rules that apply when the condition is true

### The Two Key Conditions

**`max-width`** — Applies styles when the screen is AT MOST this wide (for small screens):

```css
@media only screen and (max-width: 768px) {
  /* Styles for screens UP TO 768px wide (tablets and phones) */
}
```

**`min-width`** — Applies styles when the screen is AT LEAST this wide (for larger screens):

```css
@media only screen and (min-width: 769px) {
  /* Styles for screens 769px and WIDER (desktop) */
}
```

### Breakpoints — Common Screen Width Thresholds

A **breakpoint** is a specific screen width where your layout changes. These are the most common breakpoints used in professional web development:

| Breakpoint Name | Width | Target Devices |
|---|---|---|
| Extra small (xs) | Up to 576px | Small phones |
| Small (sm) | 576px – 768px | Large phones |
| Medium (md) | 768px – 992px | Tablets |
| Large (lg) | 992px – 1200px | Laptops |
| Extra large (xl) | 1200px and up | Desktops, wide monitors |

> 💡 **Note:** There is no single "correct" set of breakpoints. Different frameworks and projects use different values. The most important thing is to choose breakpoints based on where YOUR design breaks, not arbitrary numbers.

### Example 1 — Basic Media Query: Change Background Colour

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      background-color: lightgreen;  /* Default: green for large screens */
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 30px;
    }

    /* When screen is 768px or narrower: */
    @media only screen and (max-width: 768px) {
      body {
        background-color: lightyellow;  /* Tablet: yellow */
      }
    }

    /* When screen is 480px or narrower: */
    @media only screen and (max-width: 480px) {
      body {
        background-color: lightcoral;  /* Phone: coral/red */
      }
    }
  </style>
</head>
<body>
  <h1>Resize this window!</h1>
  <p>Watch the background colour change as the window gets narrower.</p>
  <p>Wide screen = green. Tablet width = yellow. Phone width = coral.</p>
</body>
</html>
```

**Expected output:**

```
Screen wider than 768px  → Green background
Screen 480px – 768px     → Yellow background
Screen narrower than 480px → Coral/red background
```

### Example 2 — Media Query: Making the Grid Responsive

Now we can connect our grid from Part 3 with media queries to make it stack on mobile:

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * { box-sizing: border-box; }

    body { font-family: Arial; margin: 0; }

    .row::after {
      content: "";
      display: table;
      clear: both;
    }

    [class*="col-"] {
      float: left;
      padding: 15px;
      border: 1px solid #ddd;
    }

    /* Desktop: side by side */
    .col-4 { width: 33.33%; }
    .col-8 { width: 66.66%; }

    /* On screens narrower than 768px (tablets and phones):
       all columns become full width and STACK vertically */
    @media only screen and (max-width: 768px) {
      [class*="col-"] {
        width: 100%;   /* Each column fills the full screen width */
        float: none;   /* Remove the float so they stack */
      }
    }
  </style>
</head>
<body>
  <div class="row">
    <div class="col-4" style="background:#e8f4f8;">
      <h3>Sidebar</h3>
      <p>On desktop: 33% wide. On mobile: full width, sits ABOVE main content.</p>
    </div>
    <div class="col-8" style="background:#f8f4e8;">
      <h3>Main Content</h3>
      <p>On desktop: 66% wide. On mobile: full width, sits BELOW sidebar.</p>
    </div>
  </div>
</body>
</html>
```

**Expected output:**

```
Desktop (wider than 768px):
┌───────────────────┬─────────────────────────────────────┐
│     Sidebar       │         Main Content                │
│     33.33%        │         66.66%                      │
└───────────────────┴─────────────────────────────────────┘

Mobile (narrower than 768px):
┌───────────────────────────────────────────────────────┐
│                   Sidebar (100% width)                │
└───────────────────────────────────────────────────────┘
┌───────────────────────────────────────────────────────┐
│                 Main Content (100% width)             │
└───────────────────────────────────────────────────────┘
```

### Example 3 — Media Query with Font Size Changes

```css
/* Default: large font for large screens */
h1 {
  font-size: 48px;
}

p {
  font-size: 18px;
}

/* Tablet: slightly smaller */
@media only screen and (max-width: 768px) {
  h1 {
    font-size: 32px;
  }
  p {
    font-size: 16px;
  }
}

/* Phone: compact sizes */
@media only screen and (max-width: 480px) {
  h1 {
    font-size: 24px;
  }
  p {
    font-size: 14px;
  }
}
```

**Expected output:**

```
Desktop  → h1: 48px, p: 18px
Tablet   → h1: 32px, p: 16px
Phone    → h1: 24px, p: 14px
```

### Multiple Conditions in One Media Query

You can combine conditions using `and`:

```css
/* ONLY applies when screen is between 600px and 900px wide */
@media only screen and (min-width: 600px) and (max-width: 900px) {
  .sidebar {
    display: none;  /* Hide sidebar on mid-size screens */
  }
}
```

### Mobile-First vs Desktop-First Approach

There are two main strategies for writing media queries:

**Desktop-First** — Write the default styles for large screens, then use `max-width` queries to override for smaller screens:

```css
/* Default: desktop styles */
.container { width: 1200px; }

/* Override for tablets */
@media only screen and (max-width: 992px) {
  .container { width: 100%; }
}
```

**Mobile-First** — Write the default styles for small screens first, then use `min-width` to add complexity for larger screens:

```css
/* Default: mobile styles */
.container { width: 100%; }

/* Override for desktop */
@media only screen and (min-width: 992px) {
  .container { width: 1200px; }
}
```

> ✅ **Professional recommendation:** Use **Mobile-First** design. Since most users browse on phones, start with the simplest layout and progressively enhance it for larger screens. This also leads to smaller, faster CSS files.

---

## Part 5 — Responsive Images

### The Problem with Fixed-Width Images

By default, an `<img>` element displays at its natural pixel size. If an image is 1200px wide and the screen is only 375px wide, the image overflows the screen — the user must scroll sideways to see it.

### The Simple Fix: `max-width: 100%`

```css
img {
  max-width: 100%;
  height: auto;
}
```

**Property-by-property explanation:**

- `max-width: 100%` — The image can be AT MOST as wide as its parent container. If the parent is 375px wide, the image shrinks to 375px. If the parent is 1200px wide, the image can grow up to its natural size. It never overflows its container.
- `height: auto` — When the width changes, the height adjusts automatically to maintain the image's natural aspect ratio. Without this, the image would be squished or stretched.

**The full reset for responsive images:**

```css
img {
  max-width: 100%;
  height: auto;
  display: block;   /* Optional: removes the small gap that appears below inline images */
}
```

### Example: Responsive vs Fixed Image

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * { box-sizing: border-box; }
    body { font-family: Arial; padding: 20px; }

    .container {
      max-width: 600px;
      margin: 0 auto;
      border: 2px solid #333;
      padding: 15px;
    }

    /* Responsive image */
    .responsive-img {
      max-width: 100%;
      height: auto;
    }

    /* Fixed image — will overflow on small screens */
    .fixed-img {
      width: 600px;   /* Fixed — bad practice */
    }
  </style>
</head>
<body>
  <div class="container">
    <h3>Responsive Image (good)</h3>
    <!-- Use a placeholder that represents a large image -->
    <img class="responsive-img"
         src="https://via.placeholder.com/800x400"
         alt="A large placeholder image that scales down responsively">

    <h3 style="margin-top:20px;">Fixed Image (bad on mobile)</h3>
    <img class="fixed-img"
         src="https://via.placeholder.com/800x400"
         alt="A fixed-width image that overflows on small screens">
  </div>
</body>
</html>
```

**Expected output:**

```
Inside a 600px container on a wide screen:
  Responsive image → fits perfectly (600px or less)
  Fixed image      → fits perfectly (happens to match)

Inside a 350px container on a phone:
  Responsive image → shrinks to 350px wide ✅ (no overflow)
  Fixed image      → stays 600px wide ❌ (overflows, horizontal scrollbar appears)
```

> 💡 **Think about it:** What would happen to the responsive image if the container grew to 1000px but the original image file is only 400px wide? It would stretch and look pixelated! That is why `max-width: 100%` is better than `width: 100%` — it allows the image to grow, but never beyond its natural size.

### Using `width: 100%` vs `max-width: 100%`

```css
/* width: 100% — always fills the full container, even if container is huge */
img { width: 100%; }

/* max-width: 100% — fills the container up to its natural size, then stops */
img { max-width: 100%; }
```

For most images, `max-width: 100%` is better. Use `width: 100%` only when you specifically want the image to always fill its container completely (such as a hero background image).

### Responsive Images with the `<picture>` Element

For advanced use cases, HTML provides the `<picture>` element, which lets you serve different image files at different screen sizes — smaller files for mobile (faster loading) and larger files for desktop:

```html
<picture>
  <!-- Use this image on screens 600px or wider -->
  <source media="(min-width: 600px)" srcset="image-large.jpg">
  <!-- Use this image on screens 400px or wider -->
  <source media="(min-width: 400px)" srcset="image-medium.jpg">
  <!-- Fallback for all other sizes -->
  <img src="image-small.jpg" alt="Description of image">
</picture>
```

**How it works:**
- The browser reads the `<source>` elements from top to bottom
- It uses the first `<source>` whose `media` condition matches
- If no `<source>` matches, it falls back to the `<img>` element
- This saves bandwidth on mobile — phones download the small image, not the large one

---

## Part 6 — Responsive Videos

### The Problem with Videos

Videos — especially those embedded from YouTube or Vimeo using `<iframe>` — often have a fixed width and height set in the embed code:

```html
<!-- Typical YouTube embed code — NOT responsive -->
<iframe width="560" height="315" src="https://www.youtube.com/embed/dQw4w9WgXcQ"></iframe>
```

This iframe is fixed at 560px × 315px. On a 375px phone, it overflows the screen.

### Making a Video Responsive: The Padding Trick

The classic technique for responsive video uses a **percentage-based padding hack** to maintain the video's aspect ratio:

```css
/* Step 1: A container div that sets the aspect ratio */
.video-container {
  position: relative;       /* Needed for the iframe to be positioned inside */
  padding-bottom: 56.25%;   /* 16:9 aspect ratio: 9 ÷ 16 = 0.5625 = 56.25% */
  height: 0;                /* Remove the container's own height */
  overflow: hidden;         /* Hide anything that sticks out */
  max-width: 100%;          /* Never wider than the page */
}

/* Step 2: Make the iframe fill the container */
.video-container iframe,
.video-container video {
  position: absolute;       /* Take the iframe out of normal flow */
  top: 0;                   /* Align to top of container */
  left: 0;                  /* Align to left of container */
  width: 100%;              /* Fill full container width */
  height: 100%;             /* Fill full container height */
}
```

**Why does `padding-bottom: 56.25%` work?**

In CSS, when you set `padding-bottom` as a percentage, it is calculated relative to the element's **width** — not its height. So as the container's width grows or shrinks, the padding-bottom grows or shrinks proportionally, always maintaining the 16:9 ratio.

For example:
- Container width = 800px → padding-bottom = 56.25% of 800 = 450px. Video is 800×450 ✅ (16:9)
- Container width = 400px → padding-bottom = 56.25% of 400 = 225px. Video is 400×225 ✅ (16:9)
- Container width = 375px → padding-bottom = 56.25% of 375 = 210.9px. Video is 375×211 ✅ (16:9)

### Other Common Aspect Ratios

| Aspect Ratio | Calculation | `padding-bottom` value |
|---|---|---|
| 16:9 (widescreen) | 9 ÷ 16 = 0.5625 | `56.25%` |
| 4:3 (standard) | 3 ÷ 4 = 0.75 | `75%` |
| 1:1 (square) | 1 ÷ 1 = 1.0 | `100%` |
| 21:9 (ultrawide) | 9 ÷ 21 = 0.4286 | `42.86%` |

### Full Example: Responsive YouTube Video

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * { box-sizing: border-box; }

    body {
      font-family: Arial;
      padding: 20px;
      max-width: 800px;
      margin: 0 auto;
    }

    .video-container {
      position: relative;
      padding-bottom: 56.25%;   /* 16:9 */
      height: 0;
      overflow: hidden;
      max-width: 100%;
      margin: 20px 0;
    }

    .video-container iframe {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      border: none;
    }
  </style>
</head>
<body>
  <h1>Responsive Video Example</h1>
  <p>The video below maintains its 16:9 aspect ratio on any screen size.</p>

  <div class="video-container">
    <!-- Replace the src with any YouTube embed URL -->
    <iframe
      src="https://www.youtube.com/embed/dQw4w9WgXcQ"
      allowfullscreen>
    </iframe>
  </div>

  <p>Resize this browser window to see the video scale perfectly.</p>
</body>
</html>
```

**Expected output:**

```
On a 800px wide screen: Video displays at 800 × 450px (16:9) ✅
On a 400px wide screen: Video displays at 400 × 225px (16:9) ✅
On a 320px phone:       Video displays at 320 × 180px (16:9) ✅
Aspect ratio is ALWAYS maintained. Video never overflows. ✅
```

### Using the Modern `aspect-ratio` Property

Modern CSS has a simpler way to handle aspect ratios. Browser support is now very good (2021+):

```css
.video-container iframe {
  width: 100%;
  aspect-ratio: 16 / 9;  /* Modern, clean approach */
  border: none;
}
```

This is much simpler than the padding trick. However, the padding technique remains important because it works in older browsers.

---

## Part 7 — CSS Frameworks and Templates

### What Is a CSS Framework?

A **CSS framework** is a pre-written collection of CSS (and sometimes JavaScript) that gives you ready-made responsive grids, components, and utilities — so you do not have to write all the responsive CSS from scratch.

Think of a framework like a construction kit. Instead of making every brick yourself, you have pre-made bricks in standard sizes. You assemble them to build your structure faster.

### Why Use a Framework?

- **Speed:** You can build responsive layouts in minutes instead of hours
- **Consistency:** All components follow the same grid and breakpoints
- **Tested:** Frameworks are tested across hundreds of browsers and devices
- **Community:** Large communities, documentation, tutorials, and support

### Popular CSS Frameworks

#### 1. Bootstrap

Bootstrap is the world's most popular CSS framework, created by Twitter. It provides a powerful 12-column responsive grid, pre-styled components (buttons, navbars, cards, modals), and a comprehensive utility system.

**How to add Bootstrap to your page (via CDN):**

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- Link Bootstrap CSS from a CDN (Content Delivery Network) -->
  <link rel="stylesheet"
        href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
  <title>Bootstrap Example</title>
</head>
<body>
  <!-- Bootstrap 12-column grid example -->
  <div class="container">
    <div class="row">
      <div class="col-md-4">Sidebar (4 cols on medium+ screens)</div>
      <div class="col-md-8">Main Content (8 cols on medium+ screens)</div>
    </div>
  </div>

  <!-- Bootstrap JavaScript (needed for interactive components) -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

**Bootstrap's responsive grid classes:**

| Class | Applies at |
|---|---|
| `col-` | Always (extra small, all sizes) |
| `col-sm-` | 576px and wider |
| `col-md-` | 768px and wider |
| `col-lg-` | 992px and wider |
| `col-xl-` | 1200px and wider |

So `col-md-4` means: on medium screens and larger, this column is 4/12 = 33.33% wide. On screens smaller than medium, it automatically becomes 100% wide (stacks vertically).

#### 2. W3.CSS

W3.CSS is a lightweight CSS framework created by W3Schools. It is simpler and smaller than Bootstrap, making it a great starting point for learning:

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- Link W3.CSS from CDN -->
  <link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">
  <title>W3.CSS Example</title>
</head>
<body>
  <div class="w3-row">
    <div class="w3-col m4">Sidebar (4/12 on medium)</div>
    <div class="w3-col m8">Main Content (8/12 on medium)</div>
  </div>
</body>
</html>
```

#### 3. Tailwind CSS

Tailwind CSS is a utility-first framework. Instead of pre-built components, it gives you small utility classes that you combine directly in your HTML:

```html
<!-- Tailwind example: a responsive card -->
<div class="bg-white shadow-md rounded-lg p-6 max-w-sm mx-auto">
  <h2 class="text-xl font-bold mb-2">Card Title</h2>
  <p class="text-gray-600">Card description text goes here.</p>
</div>
```

| Framework | Best for | Size |
|---|---|---|
| Bootstrap | Full-featured projects, teams | Large |
| W3.CSS | Learning, small projects | Very small |
| Tailwind CSS | Custom designs, modern projects | Configurable |
| Foundation | Enterprise, accessibility | Large |
| Bulma | Clean, modern sites | Medium |

### Using a CDN (Content Delivery Network)

A **CDN** is a network of servers around the world that hosts popular files. When you link to Bootstrap via CDN, users download Bootstrap from a server close to them, making it fast. It also means if users have visited another Bootstrap site, the file is already cached in their browser.

```html
<!-- CDN link (fast, no download needed) -->
<link rel="stylesheet"
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">

<!-- vs. local file (requires downloading Bootstrap manually) -->
<link rel="stylesheet" href="css/bootstrap.min.css">
```

### CSS Templates

A **CSS template** is a pre-built, complete webpage design that you can download and customise. Templates save you even more time than frameworks because the layout and styling are already done.

W3Schools provides free responsive CSS templates at `https://www.w3schools.com/css/css_templates.asp`. These include templates for:

- Business websites
- Blog layouts
- Portfolio pages
- Restaurant sites
- Two-column and three-column layouts

**When to use a template:**

- You need to build something quickly
- You want to see an example of a complete responsive page
- You want to learn by studying and modifying existing code

**When NOT to use a template:**

- You need a completely custom design
- The template's structure does not match your content needs
- Learning is the goal (build from scratch to truly understand the concepts)

---

## Guided Practice Exercises

### Exercise 1 — The Viewport Tag

**Objective:** Observe the difference the viewport meta tag makes on mobile.

**Steps:**

1. Create two HTML files:

**File 1: no-viewport.html**

```html
<!DOCTYPE html>
<html>
<head>
  <title>No Viewport</title>
  <style>
    body { font-family: Arial; padding: 20px; }
    h1 { color: red; }
    p { font-size: 16px; line-height: 1.6; }
  </style>
</head>
<body>
  <h1>No Viewport Meta Tag</h1>
  <p>This page has no viewport meta tag. When viewed on a mobile device,
  the browser will zoom out to show the full desktop page width (typically 980px).
  The text will appear very tiny and difficult to read.</p>
</body>
</html>
```

**File 2: with-viewport.html**

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>With Viewport</title>
  <style>
    body { font-family: Arial; padding: 20px; }
    h1 { color: green; }
    p { font-size: 16px; line-height: 1.6; }
  </style>
</head>
<body>
  <h1>With Viewport Meta Tag</h1>
  <p>This page has the viewport meta tag. When viewed on a mobile device,
  the browser uses the actual device width. Text is readable without zooming.
  This is the foundation of every responsive website.</p>
</body>
</html>
```

2. Open both files in your browser and resize the window to a narrow width (or use browser DevTools to simulate a mobile device by pressing F12 → toggle device toolbar)

**Expected output:**
```
no-viewport.html  → Page appears zoomed out, text very small on narrow screens
with-viewport.html → Page uses actual screen width, text is readable ✅
```

**Self-check:** Can you see the difference? Which file is easier to read at narrow widths?

---

### Exercise 2 — Media Queries: Show/Hide Navigation

**Objective:** Build a navigation bar that shows as horizontal tabs on desktop and hides/stacks on mobile.

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body { font-family: Arial; }

    nav {
      background-color: #333;
      overflow: hidden;
    }

    nav a {
      display: inline-block;
      color: white;
      text-decoration: none;
      padding: 14px 20px;
      font-size: 16px;
    }

    nav a:hover {
      background-color: #555;
    }

    /* --- HAMBURGER ICON (hidden on desktop) --- */
    .menu-icon {
      display: none;    /* Hidden on desktop */
      color: white;
      padding: 14px 20px;
      font-size: 24px;
      cursor: pointer;
    }

    /* --- ON MOBILE (max 600px): stack the nav links --- */
    @media only screen and (max-width: 600px) {
      nav a {
        display: block;   /* Stack links vertically */
        width: 100%;
        border-bottom: 1px solid #555;
      }

      .menu-icon {
        display: block;   /* Show hamburger on mobile */
      }
    }

    /* Content area */
    main {
      padding: 30px 20px;
    }
  </style>
</head>
<body>

  <nav>
    <span class="menu-icon">☰</span>
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Services</a>
    <a href="#">Portfolio</a>
    <a href="#">Contact</a>
  </nav>

  <main>
    <h1>Responsive Navigation</h1>
    <p>On a wide screen, the navigation links appear in a horizontal row.
    On a narrow screen (under 600px), the links stack vertically and a
    hamburger icon (☰) appears.</p>
    <p>Resize this window to see the change!</p>
  </main>

</body>
</html>
```

**Expected output:**

```
Wide screen (> 600px):
┌─[☰hidden]─[Home]──[About]──[Services]──[Portfolio]──[Contact]─┐

Narrow screen (≤ 600px):
┌─ ☰ ────────────────────────────────────────────────────────────┐
│  Home                                                          │
│  About                                                         │
│  Services                                                      │
│  Portfolio                                                     │
│  Contact                                                       │
└────────────────────────────────────────────────────────────────┘
```

**Self-check questions:**
- At what pixel width does the navigation change from horizontal to vertical?
- What CSS property change makes the links stack vertically on mobile?
- What does the `display: none` on `.menu-icon` do on desktop?

---

### Exercise 3 — Responsive Image Gallery

**Objective:** Build a 3-column image gallery that becomes 2 columns on tablets and 1 column on phones.

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: Arial;
      background: #f0f0f0;
      padding: 20px;
    }

    h1 {
      text-align: center;
      margin-bottom: 20px;
      color: #333;
    }

    .gallery {
      display: flex;
      flex-wrap: wrap;
      gap: 15px;
    }

    .gallery-item {
      flex: 1 1 calc(33.33% - 15px);  /* Desktop: 3 columns */
      background: white;
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    }

    .gallery-item img {
      width: 100%;
      height: 200px;
      object-fit: cover;    /* Crop image to fill, maintaining aspect ratio */
      display: block;
    }

    .gallery-item p {
      padding: 12px;
      color: #555;
      font-size: 14px;
    }

    /* Tablet: 2 columns */
    @media only screen and (max-width: 768px) {
      .gallery-item {
        flex: 1 1 calc(50% - 15px);
      }
    }

    /* Phone: 1 column */
    @media only screen and (max-width: 480px) {
      .gallery-item {
        flex: 1 1 100%;
      }
    }
  </style>
</head>
<body>

  <h1>Photo Gallery</h1>

  <div class="gallery">
    <div class="gallery-item">
      <img src="https://via.placeholder.com/400x300/4CAF50/fff?text=Photo+1" alt="Photo 1">
      <p>A beautiful landscape photo taken at sunrise.</p>
    </div>
    <div class="gallery-item">
      <img src="https://via.placeholder.com/400x300/2196F3/fff?text=Photo+2" alt="Photo 2">
      <p>Street photography from the city centre.</p>
    </div>
    <div class="gallery-item">
      <img src="https://via.placeholder.com/400x300/FF9800/fff?text=Photo+3" alt="Photo 3">
      <p>Abstract architecture from above.</p>
    </div>
    <div class="gallery-item">
      <img src="https://via.placeholder.com/400x300/9C27B0/fff?text=Photo+4" alt="Photo 4">
      <p>Wildlife photography in the forest.</p>
    </div>
    <div class="gallery-item">
      <img src="https://via.placeholder.com/400x300/F44336/fff?text=Photo+5" alt="Photo 5">
      <p>Ocean waves at golden hour.</p>
    </div>
    <div class="gallery-item">
      <img src="https://via.placeholder.com/400x300/009688/fff?text=Photo+6" alt="Photo 6">
      <p>Aerial view of mountain range.</p>
    </div>
  </div>

</body>
</html>
```

**Expected output:**

```
Desktop (> 768px):      3 items per row
Tablet (481px–768px):   2 items per row
Phone (≤ 480px):        1 item per row (full width, stacked)
```

**Self-check questions:**
- What does `flex: 1 1 calc(33.33% - 15px)` mean?
- What does `object-fit: cover` do to the images?
- What-if challenge: Change the phone breakpoint to 600px. What changes?

---

## Mini-Project: Responsive Business Landing Page

Let us build a complete responsive landing page for a fictional business. This project combines ALL the concepts from this lesson.

### Project Overview

We are building a landing page for "TechSolve" — a technology consulting company. The page will have:

- A navigation bar (horizontal on desktop, stacked on mobile)
- A hero section (full-width banner with headline)
- A three-column services section (stacks to 1 column on mobile)
- A responsive video embed
- A responsive contact section
- A footer

All built with pure CSS — no frameworks!

### Stage 1 — HTML Structure and Viewport

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TechSolve — Technology Consulting</title>
  <style>
    /* Global reset */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Arial', sans-serif;
      color: #333;
      line-height: 1.6;
    }
  </style>
</head>
<body>
  <!-- Content will go here -->
</body>
</html>
```

**Milestone:** Page loads as a blank white page. Foundation is set.

---

### Stage 2 — Navigation Bar

Add this CSS inside `<style>` and HTML inside `<body>`:

**CSS:**

```css
/* ========= NAVIGATION ========= */
nav {
  background-color: #1a1a2e;
  padding: 0 30px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: sticky;     /* Stays at top of screen when scrolling */
  top: 0;
  z-index: 1000;
}

.logo {
  color: #e94560;
  font-size: 24px;
  font-weight: bold;
  padding: 15px 0;
  text-decoration: none;
}

.nav-links {
  list-style: none;
  display: flex;
  gap: 5px;
}

.nav-links a {
  color: #ccc;
  text-decoration: none;
  padding: 15px 15px;
  display: block;
  transition: color 0.3s;
}

.nav-links a:hover {
  color: #e94560;
}

/* Mobile navigation */
@media only screen and (max-width: 768px) {
  nav {
    flex-direction: column;
    padding: 10px 20px;
  }

  .nav-links {
    flex-direction: column;
    width: 100%;
    gap: 0;
    padding-bottom: 10px;
  }

  .nav-links a {
    padding: 10px 0;
    border-bottom: 1px solid #333;
  }
}
```

**HTML:**

```html
<nav>
  <a href="#" class="logo">TechSolve</a>
  <ul class="nav-links">
    <li><a href="#services">Services</a></li>
    <li><a href="#about">About</a></li>
    <li><a href="#video">Demo</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>
```

---

### Stage 3 — Hero Section

**CSS:**

```css
/* ========= HERO ========= */
.hero {
  background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
  color: white;
  text-align: center;
  padding: 80px 20px;
}

.hero h1 {
  font-size: 48px;
  margin-bottom: 20px;
  color: #e94560;
}

.hero p {
  font-size: 20px;
  max-width: 600px;
  margin: 0 auto 30px;
  color: #ccc;
}

.cta-button {
  display: inline-block;
  background-color: #e94560;
  color: white;
  padding: 15px 40px;
  text-decoration: none;
  border-radius: 5px;
  font-size: 18px;
  transition: background-color 0.3s;
}

.cta-button:hover {
  background-color: #c73652;
}

/* Responsive hero */
@media only screen and (max-width: 768px) {
  .hero h1 { font-size: 32px; }
  .hero p  { font-size: 16px; }
  .hero    { padding: 50px 20px; }
}

@media only screen and (max-width: 480px) {
  .hero h1 { font-size: 24px; }
}
```

**HTML:**

```html
<section class="hero">
  <h1>Technology Solutions<br>That Drive Growth</h1>
  <p>We help businesses transform through innovative technology consulting,
  digital strategy, and custom software development.</p>
  <a href="#contact" class="cta-button">Get Free Consultation</a>
</section>
```

---

### Stage 4 — Services Section (3-Column Grid)

**CSS:**

```css
/* ========= SERVICES ========= */
#services {
  padding: 60px 20px;
  background: #f8f9fa;
}

#services h2 {
  text-align: center;
  font-size: 36px;
  margin-bottom: 40px;
  color: #1a1a2e;
}

.services-grid {
  display: flex;
  gap: 30px;
  max-width: 1100px;
  margin: 0 auto;
}

.service-card {
  flex: 1;
  background: white;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.08);
  text-align: center;
  transition: transform 0.3s;
}

.service-card:hover {
  transform: translateY(-5px);
}

.service-icon {
  font-size: 48px;
  margin-bottom: 20px;
}

.service-card h3 {
  font-size: 22px;
  margin-bottom: 15px;
  color: #1a1a2e;
}

.service-card p {
  color: #666;
  font-size: 15px;
}

/* Tablet: 2 columns, then 3rd wraps */
@media only screen and (max-width: 768px) {
  .services-grid {
    flex-wrap: wrap;
  }
  .service-card {
    flex: 1 1 calc(50% - 30px);
  }
}

/* Mobile: 1 column */
@media only screen and (max-width: 480px) {
  .service-card {
    flex: 1 1 100%;
  }
}
```

**HTML:**

```html
<section id="services">
  <h2>Our Services</h2>
  <div class="services-grid">
    <div class="service-card">
      <div class="service-icon">💻</div>
      <h3>Software Development</h3>
      <p>Custom web and mobile applications built with modern technologies
         and best practices for scalability and performance.</p>
    </div>
    <div class="service-card">
      <div class="service-icon">📊</div>
      <h3>Data Analytics</h3>
      <p>Turn your raw data into actionable insights. We build dashboards,
         reports, and predictive models that drive decisions.</p>
    </div>
    <div class="service-card">
      <div class="service-icon">☁️</div>
      <h3>Cloud Solutions</h3>
      <p>Migrate and optimise your infrastructure on AWS, Google Cloud,
         or Azure. Reduce costs, increase reliability.</p>
    </div>
  </div>
</section>
```

---

### Stage 5 — Responsive Video Section

**CSS:**

```css
/* ========= VIDEO ========= */
#video {
  padding: 60px 20px;
  background: #1a1a2e;
  color: white;
  text-align: center;
}

#video h2 {
  font-size: 36px;
  margin-bottom: 15px;
  color: #e94560;
}

#video p {
  margin-bottom: 30px;
  color: #ccc;
}

.video-container {
  position: relative;
  padding-bottom: 56.25%;
  height: 0;
  overflow: hidden;
  max-width: 800px;
  margin: 0 auto;
  border-radius: 10px;
}

.video-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: none;
  border-radius: 10px;
}
```

**HTML:**

```html
<section id="video">
  <h2>See Us In Action</h2>
  <p>Watch how TechSolve helped a client increase revenue by 40%.</p>
  <div class="video-container">
    <iframe
      src="https://www.youtube.com/embed/dQw4w9WgXcQ"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen>
    </iframe>
  </div>
</section>
```

---

### Stage 6 — Contact Section and Footer

**CSS:**

```css
/* ========= CONTACT ========= */
#contact {
  padding: 60px 20px;
  background: #f8f9fa;
}

#contact h2 {
  text-align: center;
  font-size: 36px;
  margin-bottom: 40px;
  color: #1a1a2e;
}

.contact-grid {
  display: flex;
  gap: 40px;
  max-width: 900px;
  margin: 0 auto;
}

.contact-info {
  flex: 1;
}

.contact-info h3 {
  font-size: 22px;
  margin-bottom: 15px;
  color: #1a1a2e;
}

.contact-info p {
  color: #666;
  margin-bottom: 10px;
}

.contact-form {
  flex: 1;
}

.contact-form input,
.contact-form textarea {
  width: 100%;
  padding: 12px;
  margin-bottom: 15px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 14px;
  font-family: Arial;
}

.contact-form textarea {
  height: 120px;
  resize: vertical;
}

.submit-btn {
  background-color: #e94560;
  color: white;
  border: none;
  padding: 14px 30px;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  width: 100%;
  transition: background-color 0.3s;
}

.submit-btn:hover {
  background-color: #c73652;
}

/* Mobile: stack contact info and form */
@media only screen and (max-width: 600px) {
  .contact-grid {
    flex-direction: column;
  }
}

/* ========= FOOTER ========= */
footer {
  background: #1a1a2e;
  color: #ccc;
  text-align: center;
  padding: 25px 20px;
  font-size: 14px;
}

footer span {
  color: #e94560;
}
```

**HTML:**

```html
<section id="contact">
  <h2>Get In Touch</h2>
  <div class="contact-grid">
    <div class="contact-info">
      <h3>Let's Talk</h3>
      <p>📍 123 Tech Drive, Lagos, Nigeria</p>
      <p>📞 +234 800 123 4567</p>
      <p>✉️ hello@techsolve.ng</p>
      <p>We respond within 24 hours on business days.</p>
    </div>
    <div class="contact-form">
      <input type="text" placeholder="Your Name">
      <input type="email" placeholder="Your Email">
      <textarea placeholder="Your Message"></textarea>
      <button class="submit-btn">Send Message</button>
    </div>
  </div>
</section>

<footer>
  <p>© 2026 <span>TechSolve</span>. All rights reserved. Built with pure CSS &amp; RWD.</p>
</footer>
```

---

### Final Expected Output

```
On DESKTOP (> 992px):
┌──────────── TechSolve [Home] [Services] [About] [Demo] [Contact] ───┐
├─────────────────────────────────────────────────────────────────────┤
│        Technology Solutions That Drive Growth (large headline)      │
│        CTA Button: "Get Free Consultation"                          │
├──────────────┬───────────────────┬──────────────────────────────────┤
│  💻 Software │  📊 Data Analytics│  ☁️ Cloud Solutions             │
│  Development │                   │                                  │
├──────────────┴───────────────────┴──────────────────────────────────┤
│              See Us In Action (responsive 16:9 video)               │
├─────────────────────────────┬───────────────────────────────────────┤
│  Contact Info               │  Contact Form                         │
├─────────────────────────────┴───────────────────────────────────────┤
│                     Footer: © 2026 TechSolve                        │
└─────────────────────────────────────────────────────────────────────┘

On TABLET (769px–992px):
- Nav links still horizontal but smaller
- Services: 2 cards on row 1, 1 card centered on row 2
- Video maintains 16:9 ratio
- Contact: info and form side by side

On MOBILE (≤ 480px):
- Nav stacks vertically below logo
- Hero text shrinks to 24px
- Services: single column, all 3 cards stack
- Video still 16:9 but fills phone width
- Contact: info ABOVE form (stacked)
- Everything readable without zooming ✅
```

**Reflection questions:**
- What happens if you remove the viewport meta tag? Try it and observe.
- Which section was the hardest to make responsive? Why?
- What framework would you add to make this faster to build next time?
- How would you add a fourth service card? Where would it sit on each screen size?

**Optional extension:** Add a `hamburger menu` that uses JavaScript to toggle the navigation links on mobile (so the nav is collapsed by default on mobile and opens when clicked).

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting the Viewport Meta Tag

```html
<!-- WRONG — no viewport tag -->
<head>
  <title>My Site</title>
  <style>/* lots of media queries that won't work properly */</style>
</head>

<!-- CORRECT — always include it -->
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Site</title>
</head>
```

Without the viewport tag, the browser will zoom out your page to its default wide view on mobile, and media queries will trigger based on the virtual width (980px) instead of the actual device width. Your breakpoints will fire at the wrong time.

---

### Mistake 2 — Using Pixels Instead of Percentages for Fluid Widths

```css
/* WRONG — fixed pixel widths do not flex with the screen */
.sidebar { width: 300px; }
.main    { width: 700px; }
/* Total = 1000px — overflows on anything narrower */

/* CORRECT — percentages flex with any screen */
.sidebar { width: 30%; }
.main    { width: 70%; }
/* Total = 100% — always fits ✅ */
```

---

### Mistake 3 — Writing Media Queries in the Wrong Order

CSS is read top to bottom. If you have overlapping media queries, the order matters:

```css
/* WRONG ORDER — the second rule overwrites the first on tablets */
@media (max-width: 768px) {
  .box { background: yellow; }  /* Tablets AND phones */
}
@media (max-width: 480px) {
  .box { background: red; }     /* Phones only */
}
/* This is actually fine — narrower max-width wins ✅ */

/* But this is wrong: */
@media (max-width: 480px) {
  .box { background: red; }     /* Phones: red */
}
@media (max-width: 768px) {
  .box { background: yellow; } /* Overwrites phones too — red never shows! */
}
```

**Fix:** Write media queries from largest to smallest (desktop-first) or smallest to largest (mobile-first) consistently.

---

### Mistake 4 — Setting Image Width to 100% Instead of max-width: 100%

```css
/* RISKY — image stretches beyond its natural size, becomes blurry */
img { width: 100%; }

/* BETTER — image scales down but never above its natural size */
img { max-width: 100%; height: auto; }
```

---

### Mistake 5 — Forgetting `height: auto` on Responsive Images

```css
/* WRONG — image squishes because width changes but height stays fixed */
img {
  max-width: 100%;
  /* height: auto missing! */
}

/* CORRECT — height adjusts proportionally with width */
img {
  max-width: 100%;
  height: auto;     /* ← Always include this with max-width */
}
```

---

### Mistake 6 — Not Testing on Real Devices

Many beginners only resize their browser window to simulate mobile. This is a good start, but real devices behave differently in subtle ways (touch interactions, font rendering, actual pixel density). Always test on real devices or use browser DevTools device simulation (F12 in Chrome → Toggle Device Toolbar).

---

## Reflection Questions

1. What is the purpose of the viewport meta tag, and what happens if you leave it out?

2. Why do responsive grid systems use 12 columns instead of, say, 10 or 5?

3. Write a media query that applies styles when the screen is between 600px and 900px wide.

4. What is the difference between `max-width: 100%` and `width: 100%` on an image?

5. Explain why `padding-bottom: 56.25%` creates a 16:9 aspect ratio for a video container.

6. What is the difference between the "desktop-first" and "mobile-first" approaches? Which is recommended and why?

7. Name two advantages of using a CSS framework like Bootstrap versus writing all your responsive CSS from scratch.

8. Why should you never use `user-scalable=no` in the viewport meta tag?

**Answers:**

1. The viewport meta tag tells the browser to use the device's actual screen width instead of simulating a fake wide desktop. Without it, mobile browsers zoom out to show a 980px virtual page, making text tiny and media queries unreliable.

2. Because 12 is divisible by 1, 2, 3, 4, 6, and 12 — giving you clean fractions for many common layout patterns (half, third, quarter, two-thirds, three-quarters) without awkward decimal widths.

3. `@media only screen and (min-width: 600px) and (max-width: 900px) { /* styles */ }`

4. `max-width: 100%` allows the image to be at most as wide as its container but never wider than its natural size. `width: 100%` forces the image to always fill its container, even if the container is larger than the image's natural size (causing stretching/blurriness).

5. In CSS, percentage `padding-bottom` is calculated relative to the element's WIDTH, not height. So `padding-bottom: 56.25%` of the container's width always equals 9/16 of that width, maintaining the 16:9 aspect ratio regardless of the actual width.

6. Desktop-first writes default styles for large screens and overrides with `max-width` queries for smaller screens. Mobile-first writes defaults for small screens and adds complexity with `min-width` queries. Mobile-first is recommended because most users are on mobile, it produces simpler CSS, and it encourages considering the smallest case first.

7. Any two from: faster development, pre-tested cross-browser compatibility, consistent grid system, ready-made components, built-in accessibility features, large community support.

8. `user-scalable=no` prevents users from zooming the page, which harms people with visual impairments who need to zoom to read content. The Web Content Accessibility Guidelines (WCAG) require that users can zoom up to 200% without losing content.

---

## Completion Checklist

Before moving to the next lesson, confirm you have achieved the following:

- [ ] I can explain what Responsive Web Design is and why it is important
- [ ] I always include `<meta name="viewport" content="width=device-width, initial-scale=1.0">` in my HTML
- [ ] I understand why the viewport meta tag is essential for mobile
- [ ] I can build a 12-column fluid grid using percentages
- [ ] I understand what a media query is and can write `@media` rules with `max-width` and `min-width`
- [ ] I know common breakpoints (480px, 768px, 992px, 1200px)
- [ ] I can make images responsive using `max-width: 100%; height: auto;`
- [ ] I understand the `<picture>` element for serving different image sizes
- [ ] I can make videos responsive using the `padding-bottom: 56.25%` technique
- [ ] I understand what a CSS framework is (Bootstrap, W3.CSS, Tailwind)
- [ ] I know the difference between mobile-first and desktop-first design
- [ ] I completed at least two of the three guided exercises
- [ ] I built (or studied) the TechSolve mini-project
- [ ] I tested my pages by resizing the browser window

---

## Lesson Summary

**Responsive Web Design (RWD)** is the practice of building web pages that automatically adapt their layout, typography, images, and media to look great on any screen — from a 320px phone to a 2560px desktop monitor.

RWD is built on seven interconnected pillars:

**1. The Viewport Meta Tag** — The foundation of every responsive page. `<meta name="viewport" content="width=device-width, initial-scale=1.0">` tells mobile browsers to use the actual device width instead of simulating a fake desktop.

**2. Fluid Grids** — Using percentages instead of fixed pixels for widths, so columns stretch and shrink naturally. The 12-column grid (`8.33%` per column) gives flexible layout options.

**3. Media Queries** — `@media only screen and (max-width: 768px) { }` lets you apply different CSS rules at different screen widths. Breakpoints (480px, 768px, 992px, 1200px) are the widths where the layout changes.

**4. Responsive Images** — `max-width: 100%; height: auto;` ensures images scale down on small screens without overflowing. The `<picture>` element serves different image files for different screen sizes.

**5. Responsive Videos** — The `padding-bottom: 56.25%` trick on a container div maintains the 16:9 aspect ratio at any width. The iframe inside uses `position: absolute; width: 100%; height: 100%;`.

**6. CSS Frameworks** — Bootstrap, W3.CSS, and Tailwind CSS provide pre-built responsive grids and components. They speed up development and ensure cross-browser consistency.

**7. Templates** — Pre-built responsive page designs that can be customised as a starting point.

| Technique | Core Code | What It Solves |
|---|---|---|
| Viewport | `<meta name="viewport" content="width=device-width, initial-scale=1.0">` | Scales page correctly on mobile |
| Fluid grid | `width: 33.33%` | Columns flex with screen size |
| Media query | `@media (max-width: 768px) { }` | Different styles per screen size |
| Responsive image | `max-width: 100%; height: auto;` | Images never overflow |
| Responsive video | `padding-bottom: 56.25%` | Video maintains 16:9 ratio |
| Framework | Bootstrap, W3.CSS, Tailwind | Pre-built responsive system |
