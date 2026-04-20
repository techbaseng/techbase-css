---
render_with_liquid: false
title: "CSS Backgrounds — Colours, Images, Repeat, Attachment & Shorthand"
nav_order: 6
---

# Lesson 06 — CSS Backgrounds: Painting the Canvas Behind Your Content

---

## Lesson Introduction

Every webpage you have ever visited has a background. Sometimes it is a plain colour — like the white page of a news article. Sometimes it is a beautiful photograph spanning the full screen. Sometimes it is a subtle repeating pattern that gives texture to the design. All of these effects are created with one family of CSS properties: the **background properties**.

Think of an HTML element as a picture frame. The content (text, images, buttons) is the artwork inside the frame. The **background** is the wall behind the artwork — the surface you see wherever there is no content covering it.

In this lesson you will master every background property CSS offers, one at a time, from the simplest to the most sophisticated. By the end you will be able to:

- Set a solid **background colour** for any element
- Place a **background image** behind any element
- Control whether an image **repeats** (tiles) or appears only once
- Control the **position** of a background image
- Decide whether the background **scrolls** with the page or stays fixed
- Write all background properties in a single line using the **shorthand property**
- Combine everything into a polished, real-world webpage section

---

## Prerequisite Concepts

### What is a CSS property?

A CSS property is a specific visual characteristic you can control. For example, `color` controls text colour, `font-size` controls text size, and `background-color` controls the background colour of an element.

### What does "behind" mean in CSS?

HTML elements are stacked in layers. The background of an element sits behind its text and child elements. So if you set a red background on a `<div>` that contains a paragraph, the red colour appears under the paragraph text — not on top of it.

### What is a URL in CSS?

When you reference an image file in CSS, you wrap its path in `url()`:

```css
background-image: url("photo.jpg");
```

This tells the browser: *"Go find the file called photo.jpg and use it here."* The path can be a file path (`"images/banner.jpg"`) or a full web address (`"https://example.com/img/pattern.png"`).

---

## Part 1 — `background-color`: Painting With a Solid Colour

### What is it?

`background-color` sets the **solid fill colour** of an element's background area — the space behind the element's content and padding.

### Why does it exist?

Before images or gradients, colour is the most fundamental background tool. Solid background colours are used everywhere: page backgrounds, navigation bars, buttons, cards, alerts, hero banners, table rows, and more.

### How colour values work

You can write colour values in several ways in CSS:

| Format | Example | Meaning |
|---|---|---|
| Named colour | `red`, `blue`, `navy` | English colour name |
| HEX code | `#ff0000` | 6-digit hexadecimal value |
| Short HEX | `#f00` | 3-digit shorthand for HEX |
| RGB | `rgb(255, 0, 0)` | Red, Green, Blue 0–255 |
| RGBA | `rgba(255, 0, 0, 0.5)` | RGB + alpha (transparency) |
| HSL | `hsl(0, 100%, 50%)` | Hue, Saturation, Lightness |

All of these formats work with `background-color`.

---

### Simple Example 1 — Colour the whole page body

**HTML + CSS:**
```html
<!DOCTYPE html>
<html>
<head>
<style>
  body {
    background-color: lightblue;
  }
</style>
</head>
<body>
  <h1>Hello, World!</h1>
  <p>This page has a light blue background.</p>
</body>
</html>
```

**Expected Output:**
The entire visible webpage background turns **light blue**. The heading and paragraph text sit on top of this colour.

**Line-by-line explanation:**
- `body` — selects the `<body>` element, which represents the entire visible page area
- `background-color: lightblue;` — fills the body's background with the named colour "lightblue"

---

### Simple Example 2 — Colour individual elements differently

You can set different background colours for different elements on the same page:

```html
<style>
  body {
    background-color: #f0f0f0;  /* light grey page */
  }

  h1 {
    background-color: navy;
    color: white;
    padding: 10px;
  }

  p {
    background-color: #fff9c4;  /* pale yellow */
    padding: 8px;
  }
</style>
```

**Expected Output:**
- The page body has a light grey background
- The `<h1>` heading has a **navy background with white text**
- Each `<p>` paragraph has a **pale yellow background**

> **Thinking Prompt:** The `body` has grey background. The `h1` has navy. What colour do you see around the `h1`? Is it grey or navy? *(Answer: You see grey around it — the body grey shows where the h1 does not cover.)*

---

### Simple Example 3 — Using HEX and RGBA

```css
div {
  background-color: #2c3e50;        /* dark blue-grey HEX */
  color: white;
  padding: 20px;
}

.transparent-box {
  background-color: rgba(0, 0, 255, 0.2);  /* 20% opacity blue */
}
```

**Expected Output:**
- The `<div>` has a rich dark navy background
- The `.transparent-box` has a very faint, see-through blue background (you can see content behind it)

---

### The `opacity` property vs RGBA

There are two ways to make a background semi-transparent:

**Method 1: RGBA background (preferred — only the background becomes transparent):**
```css
div {
  background-color: rgba(0, 0, 255, 0.3);
}
```

**Method 2: opacity property (entire element becomes transparent — including text!):**
```css
div {
  background-color: blue;
  opacity: 0.3;  /* Text also becomes faded! */
}
```

> ⚠️ **Important difference:** RGBA only makes the background colour transparent. The `opacity` property makes the *entire element* — including its text and child elements — transparent. Use RGBA when you only want to affect the background.

---

### Real-World Use Case

Almost every professional website uses `background-color` extensively:

```css
/* Navigation bar */
nav {
  background-color: #1a1a2e;
}

/* Alert/notification box */
.alert-success {
  background-color: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
  padding: 12px 16px;
}

/* Button */
.btn-primary {
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
}
```

---

## Part 2 — `background-image`: Placing an Image Behind Your Content

### What is it?

`background-image` places an image (or a gradient) in the background of an element — behind its text and content.

### Why does it exist?

Flat colours are great for many uses, but sometimes you need photography, textures, patterns, or gradients as a backdrop. Background images make hero sections, full-screen landing pages, patterned cards, and decorative headers possible.

### How it works

```css
element {
  background-image: url("path/to/image.jpg");
}
```

The `url()` function points to the image file. The path can be:
- **Relative**: `"images/banner.jpg"` — relative to your CSS file's location
- **Absolute**: `"https://example.com/img/photo.jpg"` — a full web URL

---

### Simple Example 1 — Set a background image on the body

```css
body {
  background-image: url("paper.gif");
}
```

**Expected Output:**
The image `paper.gif` tiles (repeats) to fill the entire page background by default.

> **Why does it repeat?** By default, CSS tiles (repeats) background images in both directions to fill the available space — like wallpaper. You will learn to control this in Part 3.

---

### Simple Example 2 — Background image on a specific element

```html
<style>
  .hero {
    background-image: url("mountain.jpg");
    height: 400px;
    width: 100%;
  }
</style>

<div class="hero">
  <h1>Welcome to My Website</h1>
</div>
```

**Expected Output:**
A 400px tall section with the mountain photo as a background. The heading "Welcome to My Website" appears on top of the image.

**Line-by-line explanation:**
- `background-image: url("mountain.jpg");` — loads the mountain photo as the background
- `height: 400px;` — the div needs an explicit height, otherwise it would collapse if it has no content height to fill
- `width: 100%;` — makes the div span the full width of its container

---

### Simple Example 3 — Stacking a background image on top of a background colour

A very useful technique: set both a `background-color` and `background-image`. The colour acts as a **fallback** — it shows if the image fails to load:

```css
.hero {
  background-image: url("banner.jpg");
  background-color: #2c3e50;   /* shows if image doesn't load */
  height: 400px;
}
```

**Expected Output:**
If `banner.jpg` loads successfully, the photo appears. If the image file cannot be found or takes too long to load, the user sees a dark navy background instead of a broken/blank area.

> **Pro Tip:** Always set a `background-color` fallback when using `background-image`. This is essential for accessibility and robustness in real projects.

---

### Important: Background Image vs `<img>` Tag

You might wonder: when should you use `background-image` in CSS versus an `<img>` tag in HTML?

| Use `background-image` (CSS) | Use `<img>` (HTML) |
|---|---|
| Decorative images (textures, hero backdrops) | Content images (product photos, diagrams) |
| When you want text layered on top | When the image IS the content |
| Patterns and design elements | Profile pictures, logos |
| Images that don't need `alt` text | Images that need accessibility descriptions |

---

## Part 3 — `background-repeat`: Controlling the Tile Behaviour

### What is it?

By default, CSS **tiles** (repeats) background images in both the horizontal and vertical directions to fill the available space. `background-repeat` lets you control — or stop — this tiling behaviour.

### Why does it exist?

Tiling is perfect for small texture and pattern images, but it is a disaster for large photos. Imagine a beautiful landscape photo tiled across your page dozens of times — it would look broken and ugly. `background-repeat` gives you control over how (and whether) the image repeats.

### The four main values

| Value | What it does |
|---|---|
| `repeat` | Repeats in both X and Y directions (default) |
| `repeat-x` | Repeats **only horizontally** (left to right) |
| `repeat-y` | Repeats **only vertically** (top to bottom) |
| `no-repeat` | Image appears **exactly once** — no tiling |

---

### Simple Example 1 — Default behaviour (repeat in both directions)

```css
body {
  background-image: url("small-pattern.png");
  background-repeat: repeat;   /* this is the default */
}
```

**Expected Output:**
The `small-pattern.png` tiles like wallpaper across the entire page in rows and columns.

---

### Simple Example 2 — Repeat only horizontally

A horizontal stripe effect — great for decorative top/bottom borders:

```css
body {
  background-image: url("gradient-stripe.png");
  background-repeat: repeat-x;
}
```

**Expected Output:**
The image repeats from left to right in a single row across the top of the page. It does NOT repeat downward. Below the first row, the background colour (or white default) shows.

---

### Simple Example 3 — Repeat only vertically

```css
body {
  background-image: url("side-pattern.png");
  background-repeat: repeat-y;
}
```

**Expected Output:**
The image repeats from top to bottom in a single column on the left side of the page. It does NOT repeat horizontally.

---

### Simple Example 4 — No repeat (most common for photo backgrounds)

```css
body {
  background-image: url("mountain-photo.jpg");
  background-repeat: no-repeat;
}
```

**Expected Output:**
The mountain photo appears exactly once in the top-left corner of the page. The rest of the page background uses the default white (or whatever `background-color` is set).

> **Thinking Prompt:** After seeing the photo in the corner, you will learn in Part 4 how to position it differently — in the centre, or stretched to fill the whole page.

---

### `background-position` — Placing the Image Precisely

When using `no-repeat`, the image defaults to the **top-left corner**. `background-position` lets you move it anywhere.

**Syntax:**
```css
background-position: horizontal vertical;
```

**Keyword values:**
- Horizontal: `left`, `center`, `right`
- Vertical: `top`, `center`, `bottom`

**Pixel values:**
- `background-position: 50px 100px;` — 50px from left, 100px from top

**Percentage values:**
- `background-position: 50% 50%;` — perfectly centred

---

### Simple Example — Centre a background image

```css
body {
  background-image: url("mountain-photo.jpg");
  background-repeat: no-repeat;
  background-position: center top;
}
```

**Expected Output:**
The mountain photo appears once, centred horizontally, aligned to the top of the page.

---

### Simple Example — Centre both ways

```css
body {
  background-image: url("logo-watermark.png");
  background-repeat: no-repeat;
  background-position: center center;
}
```

**Expected Output:**
The image appears exactly once, perfectly centred both horizontally and vertically on the page.

---

### Real-World Use Case

Patterns (small repeating images) are commonly used for subtle textures:

```css
.card {
  background-image: url("subtle-dots.png");
  background-repeat: repeat;
  background-color: #ffffff;
  padding: 30px;
}
```

Large hero photos always use `no-repeat`:

```css
.hero-section {
  background-image: url("hero-photo.jpg");
  background-repeat: no-repeat;
  background-position: center center;
  height: 600px;
}
```

---

## Part 4 — `background-attachment`: Fixed or Scrolling Background

### What is it?

`background-attachment` controls whether a background image **moves with the page as you scroll**, or **stays fixed** in place while the content scrolls over it.

### Why does it exist?

This single property creates one of the most impressive visual effects in web design: the **parallax effect** — where the background appears to stay still while foreground content scrolls past it. It creates an illusion of depth and is widely used in modern landing pages.

### The two main values

| Value | What it does |
|---|---|
| `scroll` | Background moves with the page as you scroll (default behaviour) |
| `fixed` | Background stays fixed in the viewport; content scrolls over it (parallax effect) |

There is also a third value `local` which fixes the image relative to the element's own scrolling, but `scroll` and `fixed` cover 95% of real use cases.

---

### Simple Example 1 — Default scroll behaviour

```css
body {
  background-image: url("nature.jpg");
  background-attachment: scroll;  /* this is the default */
  background-repeat: no-repeat;
}
```

**Expected Output:**
When you scroll the page, the background image moves upward along with the rest of the content — everything scrolls together as one unit.

---

### Simple Example 2 — Fixed background (parallax effect)

```css
body {
  background-image: url("nature.jpg");
  background-attachment: fixed;
  background-repeat: no-repeat;
  background-position: center center;
}
```

**Expected Output:**
The background image stays perfectly stationary as you scroll the page. The text and other content move over the image, creating a layered, three-dimensional sensation. This is the classic **parallax effect**.

---

### Seeing the Difference

The difference between `scroll` and `fixed` is most noticeable on long pages:

```html
<style>
  body {
    background-image: url("forest.jpg");
    background-attachment: fixed;
    background-size: cover;
    background-position: center;
  }

  .content-section {
    background-color: rgba(255, 255, 255, 0.85);
    margin: 60px auto;
    max-width: 800px;
    padding: 40px;
  }
</style>

<div class="content-section">
  <h2>Section One</h2>
  <p>Lots of text here...</p>
</div>

<div class="content-section">
  <h2>Section Two</h2>
  <p>More text here...</p>
</div>
```

**Expected Output:**
The forest photo fills the page background and stays fixed. The semi-transparent white sections (`.content-section`) scroll over it smoothly, creating a beautiful parallax effect.

---

### `background-size` — Making Images Fill the Element

Introduced alongside modern CSS, `background-size` controls how large the background image is rendered. While not part of the original four properties, it is essential for using background images well.

| Value | What it does |
|---|---|
| `auto` | Image displays at its natural size (default) |
| `cover` | Scales image to **cover the entire element** — may crop edges |
| `contain` | Scales image to **fit entirely within** the element — may show gaps |
| `100px 200px` | Sets exact width and height |
| `50% auto` | Sets percentage width, auto height |

```css
.hero {
  background-image: url("banner.jpg");
  background-size: cover;        /* fills the entire hero section */
  background-position: center;
  background-repeat: no-repeat;
  height: 500px;
}
```

**Expected Output:**
The banner image scales to completely cover the 500px hero section. If the image's aspect ratio differs from the container, the image is cropped on the edges but never distorted.

> **`cover` vs `contain` analogy:** `cover` is like filling a frame by zooming in — the whole frame is covered but parts of the photo may be cut off. `contain` is like fitting a photo inside a frame without cropping — all of the photo is visible but there may be empty space around it.

---

## Part 5 — The `background` Shorthand Property

### What is it?

Instead of writing five or six separate background property declarations, CSS lets you combine them all into a single line using the **`background` shorthand property**.

### Why does it exist?

Shorthand properties exist to make code shorter, faster to write, and easier to read. Once you are comfortable with each individual property, the shorthand becomes the natural and preferred way to write backgrounds in professional code.

### The full shorthand syntax

```css
background: color image position/size repeat attachment;
```

You can include any or all of these values in a single declaration. The order matters for some values (particularly `position/size`).

---

### Understanding the Syntax Step by Step

Here is the longhand version:

```css
body {
  background-color:      #ffffff;
  background-image:      url("paper.png");
  background-position:   right top;
  background-size:       auto;
  background-repeat:     no-repeat;
  background-attachment: fixed;
}
```

And here is the exact same thing as a shorthand:

```css
body {
  background: #ffffff url("paper.png") right top / auto no-repeat fixed;
}
```

The **`/`** (forward slash) separates `background-position` from `background-size`. Everything to the left of `/` is the position; everything to the right is the size.

---

### Simple Example 1 — Colour and image only

The most minimal shorthand — colour + image:

```css
body {
  background: #f4f4f4 url("texture.png");
}
```

This is equivalent to:

```css
body {
  background-color: #f4f4f4;
  background-image: url("texture.png");
}
```

**Expected Output:**
The body has a light grey colour (fallback), and the texture image tiles over it by default.

---

### Simple Example 2 — Full shorthand with all main values

```css
body {
  background: #ffffff url("mountain.jpg") center center / cover no-repeat fixed;
}
```

Breaking this down word by word:
- `#ffffff` → `background-color: #ffffff` (white fallback)
- `url("mountain.jpg")` → `background-image: url("mountain.jpg")`
- `center center` → `background-position: center center` (centred)
- `/` → separator between position and size
- `cover` → `background-size: cover` (fill the container)
- `no-repeat` → `background-repeat: no-repeat`
- `fixed` → `background-attachment: fixed` (parallax)

**Expected Output:**
The mountain image covers the full page background, is centred, doesn't repeat, and stays fixed as you scroll — the complete parallax hero effect — all in one line.

---

### Simple Example 3 — Shorthand for a card with a texture

```css
.card {
  background: #fff url("dots-pattern.png") repeat;
  border: 1px solid #ddd;
  padding: 20px;
}
```

**Expected Output:**
Each `.card` element has a white background with a repeating dot texture on top of it.

---

### What Happens to Values You Don't Specify?

When you use the shorthand and omit a value, CSS **resets** that property to its initial (default) value. This is an important gotcha:

```css
/* Full longhand set previously: */
div {
  background-color: navy;
  background-image: url("pattern.png");
  background-repeat: no-repeat;
}

/* Then you override with shorthand: */
div {
  background: red;  /* ← Only sets color; ALL OTHER values reset to default! */
}
```

**Result:** The image is gone. Repeat is back to `repeat`. Only `background-color: red` remains.

> ⚠️ **Important:** The `background` shorthand resets all unspecified background sub-properties to their defaults. This can cause unexpected results if you use the shorthand to update only one property. When you only want to change one value, use the individual property instead.

---

### All CSS Background Properties — Reference Table

| Property | Purpose | Common Values |
|---|---|---|
| `background-color` | Sets solid background colour | Named colour, HEX, RGB, RGBA |
| `background-image` | Sets background image or gradient | `url("file.jpg")`, `none` |
| `background-repeat` | Controls image tiling | `repeat`, `no-repeat`, `repeat-x`, `repeat-y` |
| `background-position` | Positions the background image | `top left`, `center center`, `50% 50%`, `0px 0px` |
| `background-size` | Controls image size | `auto`, `cover`, `contain`, pixel/percentage values |
| `background-attachment` | Scroll vs fixed behaviour | `scroll`, `fixed`, `local` |
| `background` | Shorthand for all the above | See shorthand syntax |

---

## Part 6 — Guided Practice Exercises

### Exercise 1 — Styled Blog Post Header

**Objective:** Practice `background-color`, `background-image`, `no-repeat`, `background-position`, and `background-size`.

**Scenario:** You are building the header section of a travel blog. The header should display a stunning full-width photo with the blog title on top.

**HTML (given):**
```html
<!DOCTYPE html>
<html>
<head>
  <title>Travel Blog</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <header class="blog-header">
    <h1>Discover the World</h1>
    <p>Adventures, tips and stories from a passionate traveller</p>
  </header>

  <main class="content">
    <article>
      <h2>My Trip to the Mountains</h2>
      <p>The air was crisp and the views were breathtaking...</p>
    </article>

    <article>
      <h2>Street Food in Lagos</h2>
      <p>The flavours of suya and puff puff never get old...</p>
    </article>
  </main>

</body>
</html>
```

**Your Task — write the CSS:**

1. Style `.blog-header` with a background image of your choice (use any image URL or a placeholder like `"banner.jpg"`), `no-repeat`, `cover` size, centred position, and a dark navy fallback colour (`#1a1a2e`). Give it a `height` of `400px`.
2. Make the text in `.blog-header` white so it shows up against the dark image.
3. Give the `body` a `background-color` of `#f5f5f5` (light grey).
4. Give each `article` a `background-color` of white, some padding (`20px`), and a bottom margin (`16px`).
5. **Bonus:** Add `background-attachment: fixed` to the header to create a parallax effect.

**Solution:**
```css
/* Task 3 — body background */
body {
  background-color: #f5f5f5;
  margin: 0;
  font-family: Arial, sans-serif;
}

/* Task 1 — header background */
.blog-header {
  background-color: #1a1a2e;              /* fallback colour */
  background-image: url("banner.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  background-attachment: fixed;           /* bonus parallax */
  height: 400px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

/* Task 2 — header text */
.blog-header h1,
.blog-header p {
  color: white;
  text-align: center;
}

/* Task 4 — article cards */
article {
  background-color: white;
  padding: 20px;
  margin-bottom: 16px;
  max-width: 800px;
  margin-left: auto;
  margin-right: auto;
}
```

**Self-check Questions:**
- What colour would you see in the header if `banner.jpg` could not be found?
- Why does the header need an explicit `height`?
- What would change if you switched `background-size: cover` to `background-size: contain`?

---

### Exercise 2 — Pattern Card Grid

**Objective:** Practice `background-repeat`, `background-color` as fallback, and the `background` shorthand.

**Scenario:** You are building a grid of feature cards for a design agency website. Each card should have a distinct background personality.

**HTML (given):**
```html
<div class="card-grid">

  <div class="card card-plain">
    <h3>Strategy</h3>
    <p>We craft brand strategies that resonate.</p>
  </div>

  <div class="card card-pattern">
    <h3>Design</h3>
    <p>Clean, modern interfaces tailored to you.</p>
  </div>

  <div class="card card-dark">
    <h3>Development</h3>
    <p>Fast, accessible, and beautiful websites.</p>
  </div>

</div>
```

**Your Task:**

1. Give `.card` base styles: `padding: 30px`, `border-radius: 8px`, `margin: 10px`.
2. Use the **`background` shorthand** to style `.card-plain` with only a solid colour: `#e8f4fd`.
3. Style `.card-pattern` using the shorthand with a white fallback colour, a small repeating pattern image (`"dots.png"` — imagine it exists), and `repeat`.
4. Style `.card-dark` using the shorthand with `#2c3e50` background colour and white text.

**Solution:**
```css
/* Task 1 — Base card */
.card {
  padding: 30px;
  border-radius: 8px;
  margin: 10px;
}

/* Task 2 — Plain card (shorthand, colour only) */
.card-plain {
  background: #e8f4fd;
}

/* Task 3 — Pattern card (shorthand with image) */
.card-pattern {
  background: #ffffff url("dots.png") repeat;
}

/* Task 4 — Dark card */
.card-dark {
  background: #2c3e50;
  color: white;
}
```

---

### Exercise 3 — Converting Longhand to Shorthand

**Objective:** Practice reading and writing the `background` shorthand.

**Given longhand CSS — convert each to shorthand:**

**Set A:**
```css
/* Longhand */
div.box-a {
  background-color: #ffeeba;
  background-image: url("stripe.png");
  background-repeat: repeat-x;
  background-position: top left;
}
```

**Set B:**
```css
/* Longhand */
section.hero {
  background-color: #000;
  background-image: url("hero.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center center;
  background-attachment: fixed;
}
```

**Solutions:**
```css
/* Set A — shorthand */
div.box-a {
  background: #ffeeba url("stripe.png") top left repeat-x;
}

/* Set B — shorthand */
section.hero {
  background: #000 url("hero.jpg") center center / cover no-repeat fixed;
}
```

> **Note on Set B:** The `/` between `center center` and `cover` is required — it separates position from size. This is mandatory CSS syntax.

---

## Part 7 — Mini Project: Styled Landing Page Section

Build a polished, multi-section landing page that uses every background property you have learned.

### Project Brief

You are building the homepage for a fictional eco-travel company called **"Verdant Journeys."** The page should have three distinct sections, each with a different background treatment.

---

### Stage 1 — HTML Structure

Create `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Verdant Journeys — Eco Travel</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- Section 1: Hero -->
  <section id="hero">
    <div class="hero-content">
      <h1>Travel. Sustainably.</h1>
      <p>Discover the world without leaving it worse than you found it.</p>
      <a href="#" class="btn">Explore Tours</a>
    </div>
  </section>

  <!-- Section 2: Features -->
  <section id="features">
    <h2>Why Choose Verdant?</h2>
    <div class="features-grid">
      <div class="feature-card">
        <h3>🌿 Carbon Neutral</h3>
        <p>All our tours are offset 100% through certified reforestation.</p>
      </div>
      <div class="feature-card">
        <h3>🗺️ Local Guides</h3>
        <p>Expert guides from the communities you visit.</p>
      </div>
      <div class="feature-card">
        <h3>🌍 Small Groups</h3>
        <p>Maximum 12 people per tour. Intimate and impactful.</p>
      </div>
    </div>
  </section>

  <!-- Section 3: Testimonial with parallax -->
  <section id="testimonial">
    <div class="testimonial-content">
      <blockquote>"The most transformative trip of my life. Verdant didn't just show me places — they showed me people."</blockquote>
      <cite>— Ngozi A., Lagos</cite>
    </div>
  </section>

  <!-- Section 4: Footer -->
  <footer id="site-footer">
    <p>© 2025 Verdant Journeys. Travelling responsibly since 2015.</p>
  </footer>

</body>
</html>
```

---

### Stage 2 — Base and Reset Styles

Create `style.css`:

```css
/* ===== BASE RESET ===== */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Georgia', serif;
  background-color: #f9f9f9;
  color: #333;
}
```

**Milestone:** Blank page, clean slate, no browser default spacing.

---

### Stage 3 — Hero Section (Full-screen Fixed Background)

```css
/* ===== HERO SECTION ===== */
#hero {
  /* Shorthand: colour + image + position/size + repeat + attachment */
  background: #2d5016 url("forest-hero.jpg") center center / cover no-repeat fixed;
  height: 100vh;           /* 100% of the viewport height */
  display: flex;
  align-items: center;
  justify-content: center;
}

.hero-content {
  text-align: center;
  color: white;
  background-color: rgba(0, 0, 0, 0.45);  /* dark semi-transparent overlay */
  padding: 50px 60px;
  border-radius: 4px;
}

.hero-content h1 {
  font-size: 52px;
  margin-bottom: 16px;
  letter-spacing: 2px;
}

.hero-content p {
  font-size: 18px;
  margin-bottom: 28px;
}

.btn {
  background-color: #5a9c32;
  color: white;
  padding: 14px 32px;
  text-decoration: none;
  border-radius: 4px;
  font-size: 16px;
}
```

**Milestone:** A full-screen hero with forest backdrop, white text, semi-transparent overlay, and a green call-to-action button. The background is fixed (parallax).

---

### Stage 4 — Features Section (Textured Cards)

```css
/* ===== FEATURES SECTION ===== */
#features {
  background-color: #f0f4ec;   /* light sage green */
  padding: 80px 40px;
  text-align: center;
}

#features h2 {
  font-size: 32px;
  margin-bottom: 40px;
  color: #2d5016;
}

.features-grid {
  display: flex;
  gap: 24px;
  justify-content: center;
  flex-wrap: wrap;
}

.feature-card {
  /* Using individual properties here for clarity */
  background-color: white;
  background-image: url("leaf-texture.png");
  background-repeat: repeat;
  width: 260px;
  padding: 32px 24px;
  border-radius: 8px;
  border: 1px solid #d4e6c3;
}

.feature-card h3 {
  font-size: 20px;
  margin-bottom: 12px;
  color: #2d5016;
}
```

**Milestone:** Three white cards with subtle leaf texture. Each card has a heading with an emoji, body text, and rounded corners on a sage green section background.

---

### Stage 5 — Testimonial Section (Second Fixed Background)

```css
/* ===== TESTIMONIAL SECTION ===== */
#testimonial {
  background: #1a3a0a url("mountain-path.jpg") center center / cover no-repeat fixed;
  height: 350px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.testimonial-content {
  text-align: center;
  max-width: 700px;
  padding: 0 30px;
}

#testimonial blockquote {
  font-size: 24px;
  font-style: italic;
  color: white;
  line-height: 1.6;
  margin-bottom: 16px;
  text-shadow: 1px 1px 4px rgba(0,0,0,0.5);
}

#testimonial cite {
  color: #c5e8a0;
  font-size: 16px;
}
```

**Milestone:** A second parallax section. As users scroll from Features, the mountain path photo appears fixed while the content seems to float over it. The quote has a subtle text-shadow for legibility.

---

### Stage 6 — Footer

```css
/* ===== FOOTER ===== */
#site-footer {
  background: #2d5016;
  color: #c5e8a0;
  text-align: center;
  padding: 24px 40px;
  font-size: 14px;
}
```

**Final Output:**
A complete four-section landing page demonstrating: solid colour backgrounds, full-cover background images, fixed (parallax) attachments, semi-transparent overlay using RGBA, repeating texture patterns, the `background` shorthand, and colour fallbacks.

---

### Reflection Questions

1. You used `background-attachment: fixed` on two sections. What effect does this create when scrolling between them?
2. Why was `background-color: #2d5016` included in the hero shorthand if there is already an image?
3. The `.hero-content` div has `background-color: rgba(0, 0, 0, 0.45)`. What does this do, and why is it used instead of just setting `opacity: 0.45`?
4. The feature cards use `background-image: url("leaf-texture.png")` with `repeat`. What would happen if you changed this to `no-repeat`?
5. Why did the testimonial section need an explicit `height: 350px`?
6. Rewrite the `.feature-card` background properties as a single shorthand line.

---

## Part 8 — Common Beginner Mistakes

### Mistake 1 — Background image not showing (wrong path)

**Wrong:**
```css
body {
  background-image: url(mountain.jpg);   /* no quotes */
}

/* or */
body {
  background-image: url("images/mountain.jpg");  /* file is actually in root folder */
}
```

**Why it's wrong:** A missing or incorrect file path means the browser cannot find the image — it silently fails with no error shown on the page.

**Correct:**
```css
body {
  background-image: url("mountain.jpg");   /* quotes are recommended */
}
```

> **Debugging tip:** Open browser DevTools (F12), go to the Network tab, reload the page, and look for the image file. A red status (404) means the path is wrong.

---

### Mistake 2 — Background image invisible because element has no height

**Wrong:**
```css
.hero {
  background-image: url("banner.jpg");
  background-size: cover;
}
```

**HTML:**
```html
<div class="hero"></div>  <!-- empty div! -->
```

**Why it's wrong:** An empty `<div>` has `height: 0` by default. With no content to expand it, the div collapses to zero height — the background is technically there but invisible because the element is zero pixels tall.

**Correct:**
```css
.hero {
  background-image: url("banner.jpg");
  background-size: cover;
  height: 500px;   /* explicit height required */
}
```

---

### Mistake 3 — Forgetting `background-repeat: no-repeat` on photos

**Wrong:**
```css
body {
  background-image: url("portrait-photo.jpg");
  /* missing no-repeat! */
}
```

**Why it's wrong:** Without `no-repeat`, the photo tiles repeatedly across the page, which almost never looks good for actual photographs.

**Correct:**
```css
body {
  background-image: url("portrait-photo.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}
```

---

### Mistake 4 — Using `opacity` when you only want to fade the background

**Wrong:**
```css
.overlay {
  background-color: black;
  opacity: 0.5;   /* this fades EVERYTHING — text becomes unreadable too! */
}
```

**Correct:**
```css
.overlay {
  background-color: rgba(0, 0, 0, 0.5);  /* only the background is faded */
}
```

---

### Mistake 5 — Wrong shorthand order for position/size (missing the slash)

**Wrong:**
```css
body {
  background: url("hero.jpg") center center cover no-repeat;
  /* Missing / between position and size! */
}
```

**Why it's wrong:** CSS does not know where the position ends and the size begins without the `/` separator.

**Correct:**
```css
body {
  background: url("hero.jpg") center center / cover no-repeat;
  /*                          position ↑ / ↑ size       */
}
```

---

### Mistake 6 — Overwriting background properties accidentally with shorthand

**Wrong:**
```css
.card {
  background-image: url("texture.png");
  background-repeat: repeat;
}

/* Later, you add: */
.card {
  background: white;   /* THIS REMOVES the image and repeat settings! */
}
```

**Why it's wrong:** The `background` shorthand resets all unspecified sub-properties to their initial defaults. The image and repeat settings are wiped out.

**Correct:** If you only want to update the colour, use the individual property:
```css
.card {
  background-color: white;   /* Only changes the colour; image/repeat unchanged */
}
```

---

## Part 9 — Reflection Questions

1. What is the difference between `background-color` and `background-image`? Can they both be applied to the same element at the same time?
2. You set `background-image: url("photo.jpg")` on a `<p>` element but nothing appears. You can see the paragraph text. What is the most likely reason the background isn't showing?
3. What does `background-repeat: repeat-x` do differently from `repeat-y`? Give a real use case where each would be useful.
4. Explain the parallax effect in your own words. Which CSS property creates it, and what value do you use?
5. Expand this shorthand into full individual properties:
   ```css
   background: #333 url("night-sky.jpg") center top / cover no-repeat fixed;
   ```
6. A colleague writes `background-size: contain` for a hero section. The result has white bars on the left and right side of the image. Why is this happening, and what should they change it to?
7. Why is it good practice to always include a `background-color` even when you also set a `background-image`?

---

## Completion Checklist

- [ ] I understand what `background-color` does and can write it using HEX, RGB, RGBA, and named colours
- [ ] I can apply `background-image` to any element using `url()`
- [ ] I understand the difference between `background-image` and an HTML `<img>` tag
- [ ] I can control image tiling with `background-repeat` (repeat, no-repeat, repeat-x, repeat-y)
- [ ] I can position a background image using `background-position`
- [ ] I understand `background-size` values: `auto`, `cover`, and `contain`
- [ ] I can explain the difference between `background-attachment: scroll` and `fixed`
- [ ] I can create a parallax scrolling effect using `background-attachment: fixed`
- [ ] I can write all background properties in a single `background` shorthand declaration
- [ ] I understand the `/` separator between position and size in the shorthand
- [ ] I know why the shorthand can accidentally reset unrelated background properties
- [ ] I can use `rgba()` to create a semi-transparent background without affecting text opacity
- [ ] I completed Exercise 1 (Blog Header)
- [ ] I completed Exercise 2 (Pattern Cards)
- [ ] I completed Exercise 3 (Longhand to Shorthand Conversion)
- [ ] I completed the Mini Project (Verdant Journeys landing page)

---

## Lesson Summary

CSS background properties give you complete control over the visual canvas that sits behind every element on your page.

`background-color` is the most fundamental — it fills any element's background with a solid colour, specified as a named colour, HEX code, RGB value, or RGBA value (with transparency). `background-image` lets you place any image file or gradient behind an element's content using the `url()` function. Because images tile by default, `background-repeat` is essential for controlling whether an image fills a space like wallpaper (`repeat`), runs in one direction only (`repeat-x`, `repeat-y`), or appears just once (`no-repeat`). `background-position` then lets you place that non-repeating image exactly where you want it — by keyword, pixel value, or percentage.

`background-size` extends this further: `cover` scales the image to fill the entire container (cropping if needed, but never leaving gaps), while `contain` scales it to fit entirely within the container (showing background colour in any remaining space). `background-attachment` introduces one of web design's most beloved effects — setting it to `fixed` creates a parallax illusion where the background stays stationary while content scrolls over it.

Finally, the `background` shorthand lets you express all of these settings in a single clean line, using the syntax `background: color image position/size repeat attachment`. The `/` between position and size is mandatory. Omitting values in the shorthand resets them to their defaults — so use individual properties when you only want to change one setting.

A professional pattern you will use constantly: always pair `background-image` with a `background-color` fallback, always set `background-repeat: no-repeat` for photographs, always set `background-size: cover` for hero banners, and always give elements explicit height when their background needs to be visible.

---

*Sources: W3Schools CSS Backgrounds series — background-color, background-image, background-repeat, background-attachment, and background shorthand (https://www.w3schools.com/css/)*
