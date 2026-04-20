---
render_with_liquid: false
title: "CSS Image Gallery and Image Sprites — Building Visual Displays and Optimising Performance"
nav_order: 34
---

# Lesson 34 — CSS Image Gallery and Image Sprites: Building Visual Displays and Optimising Performance

---

## Lesson Introduction

Two of the most visible skills in front-end web development are creating beautiful image galleries and making pages load fast. This lesson teaches both — and shows you exactly how they connect.

**Part One: CSS Image Galleries**
You will learn how to take a raw collection of images and turn them into a polished, responsive grid gallery — the kind you see on photography portfolios, e-commerce product pages, Instagram-style apps, and news websites. You will build galleries from scratch using pure CSS: fixed-width galleries, responsive galleries, hover overlay effects, and caption displays.

**Part Two: CSS Image Sprites**
You will learn one of the most important performance techniques in CSS: combining many small images into one single file called a *sprite sheet*, then using CSS to "cut out" each individual image as needed. This dramatically reduces the number of network requests your page makes, making it load faster for users.

By the end of this lesson you will be able to:
- Build a fully responsive image gallery with hover effects using CSS alone
- Understand what image sprites are and why they exist
- Use `background-image` and `background-position` to display individual sprite icons
- Create a sprite-based navigation bar with hover states
- Build a combined mini-project: a portfolio gallery page with a sprite-powered icon toolbar

---

## Prerequisite Concepts

Before starting, you need to be comfortable with these ideas. Brief explanations are provided.

### CSS Box Model
Every HTML element is a rectangular box with `width`, `height`, `padding`, `border`, and `margin`. Controlling box dimensions is central to placing gallery images precisely.

### `position: relative` and `position: absolute`
When an element has `position: relative`, its children can use `position: absolute` to place themselves relative to it. This is the foundation of image overlay effects.

```css
.parent {
  position: relative;   /* Children positioned relative to this */
}
.child {
  position: absolute;   /* Positioned within .parent */
  top: 0;
  left: 0;
}
```

### `background-image` and `background-position`
These two properties are the foundation of image sprites.

```css
.element {
  background-image: url("photo.jpg");     /* Which image file to use */
  background-position: 0 0;              /* Where to start showing the image */
  background-repeat: no-repeat;          /* Don't tile the image */
}
```

### `overflow: hidden`
Hides content that goes outside a box's boundaries — essential for cropping images.

### `opacity` and `transition`
`opacity` controls how transparent an element is (0 = invisible, 1 = fully visible). `transition` makes property changes animate smoothly over time.

```css
.overlay {
  opacity: 0;
  transition: opacity 0.3s ease;   /* Fade in/out over 0.3 seconds */
}
.parent:hover .overlay {
  opacity: 1;
}
```

---

## PART ONE — CSS Image Gallery

---

## Section 1 — What Is an Image Gallery?

### The Concept

An image gallery is a structured visual layout that displays a collection of images in an organised grid or row. You encounter them everywhere:

- A photographer's portfolio showing their work in a neat 3-column grid
- An e-commerce site displaying product thumbnails in rows of four
- A social media app's profile page showing a grid of posted photos
- A news website showing article thumbnail images in a responsive layout

Without CSS, images just stack vertically one after another. CSS gives you the tools to arrange them in grids, control their sizes, add borders, captions, and hover effects — transforming a plain list into a professional gallery.

### The Core Problem CSS Solves

```html
<!-- HTML without CSS — images just stack vertically, uncontrolled -->
<img src="photo1.jpg">
<img src="photo2.jpg">
<img src="photo3.jpg">
<img src="photo4.jpg">
```

Without CSS, these four images appear one below the other in a messy column. With CSS, you can arrange them into a beautiful 2×2 or 4×1 grid, add space between them, make them uniform sizes, and add hover effects.

---

## Section 2 — Building a Basic Image Gallery

### Step 1 — HTML Structure for a Gallery

The standard pattern for a CSS gallery uses a **container `<div>`** wrapping individual **gallery item `<div>`s**, each containing an `<img>` and optional caption.

```html
<!-- The basic gallery HTML structure -->
<div class="gallery">

  <div class="gallery-item">
    <img src="photo1.jpg" alt="Mountain landscape" />
    <div class="caption">Mountain Landscape</div>
  </div>

  <div class="gallery-item">
    <img src="photo2.jpg" alt="Ocean sunset" />
    <div class="caption">Ocean Sunset</div>
  </div>

  <div class="gallery-item">
    <img src="photo3.jpg" alt="Forest path" />
    <div class="caption">Forest Path</div>
  </div>

  <div class="gallery-item">
    <img src="photo4.jpg" alt="City skyline" />
    <div class="caption">City Skyline</div>
  </div>

</div>
```

**Why this structure?**
- The outer `.gallery` div controls the overall layout (grid, flexbox, etc.)
- Each `.gallery-item` div wraps one image and its caption together as a unit
- The `alt` attribute on every `<img>` is required for accessibility
- The `.caption` div allows caption text to be styled independently

---

### Step 2 — Making Images a Uniform Size

Images rarely arrive with the same dimensions. Left unstyled, your gallery would have a jumble of different sizes. CSS fixes this.

```css
/* Make all gallery images the same size */
.gallery-item img {
  width: 300px;         /* Fixed width — all images will be this wide */
  height: 200px;        /* Fixed height — all images will be this tall */
  object-fit: cover;    /* Scale and crop the image to fill the box perfectly */
  display: block;       /* Remove the small gap that appears under inline images */
}
```

**What does `object-fit: cover` do?**

Think of it like a photo frame. The frame (your `<img>` element) is a fixed 300×200 rectangle. Some photos may be landscape (wide), some portrait (tall), and some square. Without `object-fit: cover`, images would distort to fit — faces would be squashed or stretched. With `object-fit: cover`, the image is scaled up and cropped so that it fills the frame completely without any distortion. Some edges may be cropped, but the proportions are always correct.

```css
/* Comparison of object-fit values */
img { object-fit: fill;    }  /* Default: stretches/distorts to fit exactly */
img { object-fit: cover;   }  /* Crops to fill — no distortion, may crop edges */
img { object-fit: contain; }  /* Shrinks to fit inside — may show empty space */
img { object-fit: none;    }  /* Shows image at its natural size, may overflow */
```

**Expected Output with `cover`:**
All images appear as uniform 300×200 rectangles, each perfectly filled with their respective photo, with no distortion.

---

### Step 3 — Arranging Images in a Row Using Flexbox

```css
/* Arrange gallery items in a horizontal row */
.gallery {
  display: flex;          /* Flexbox layout — items go side by side */
  flex-wrap: wrap;        /* Items wrap to the next line when the row is full */
  gap: 10px;              /* 10px space between every item */
  padding: 10px;
}

.gallery-item {
  border: 1px solid #ddd;
  background-color: #fff;
  border-radius: 4px;
  overflow: hidden;       /* Clips the image within the rounded corners */
}
```

**Expected Output:** Four gallery items arranged in a horizontal row with 10px gaps between them. On a narrow screen, items wrap automatically to the next row.

> 💭 **Think about it:** What happens if you remove `flex-wrap: wrap`? All items stay on one row and might overflow off-screen, or they get squashed to fit. `flex-wrap: wrap` is what lets the gallery reflow onto multiple rows naturally.

---

### Step 4 — Adding a Caption Below Each Image

```css
/* Style the caption text below each image */
.caption {
  padding: 8px 12px;
  font-size: 14px;
  color: #555;
  text-align: center;
  font-family: Arial, sans-serif;
  background-color: #fff;
}
```

**Expected Output:** Each gallery item shows the image above, with a clean caption text centred below it on a white background.

---

### Full Basic Gallery Example

Here is the complete beginner gallery putting all four steps together:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Basic CSS Image Gallery</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f0f0f0;
      padding: 20px;
    }

    /* Step 3: Flexbox layout */
    .gallery {
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
      padding: 10px;
    }

    /* Step 3: Gallery item container */
    .gallery-item {
      border: 1px solid #ccc;
      background-color: #fff;
      border-radius: 6px;
      overflow: hidden;
      box-shadow: 0 2px 6px rgba(0,0,0,0.08);
    }

    /* Step 2: Uniform image size */
    .gallery-item img {
      width: 220px;
      height: 150px;
      object-fit: cover;
      display: block;
    }

    /* Step 4: Caption styling */
    .caption {
      padding: 8px 12px;
      font-size: 13px;
      color: #555;
      text-align: center;
    }
  </style>
</head>
<body>

  <h2>Nature Photography</h2>

  <div class="gallery">

    <div class="gallery-item">
      <img src="https://via.placeholder.com/220x150/4a8f6e/ffffff?text=Mountains" alt="Mountains" />
      <div class="caption">Mountain Range</div>
    </div>

    <div class="gallery-item">
      <img src="https://via.placeholder.com/220x150/2c7bb6/ffffff?text=Ocean" alt="Ocean" />
      <div class="caption">Ocean Sunset</div>
    </div>

    <div class="gallery-item">
      <img src="https://via.placeholder.com/220x150/6b8e23/ffffff?text=Forest" alt="Forest" />
      <div class="caption">Forest Path</div>
    </div>

    <div class="gallery-item">
      <img src="https://via.placeholder.com/220x150/c47a1b/ffffff?text=Desert" alt="Desert" />
      <div class="caption">Desert Dunes</div>
    </div>

    <div class="gallery-item">
      <img src="https://via.placeholder.com/220x150/8b3a8b/ffffff?text=Flowers" alt="Flowers" />
      <div class="caption">Wildflowers</div>
    </div>

    <div class="gallery-item">
      <img src="https://via.placeholder.com/220x150/1a6b8a/ffffff?text=Lake" alt="Lake" />
      <div class="caption">Still Lake</div>
    </div>

  </div>

</body>
</html>
```

**Expected Output:** Six gallery items arranged in a horizontal row (wrapping to a second row if needed), each showing a coloured placeholder image with a caption below. Clean, professional, and ordered.

---

## Section 3 — Responsive Gallery (Adapting to All Screen Sizes)

A responsive gallery automatically rearranges itself depending on the screen size. On a wide desktop, it might show four images per row. On a tablet, two per row. On a mobile phone, one per row.

### Using CSS Grid for Responsiveness

CSS Grid is the most powerful and modern way to build responsive galleries. The magic keyword is `auto-fill` combined with `minmax()`.

```css
/* Responsive gallery using CSS Grid */
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  /* ↑ "Fill the row with as many columns as fit,
        each at least 200px wide, growing equally to fill space" */
  gap: 12px;
  padding: 12px;
}
```

**Breaking down `repeat(auto-fill, minmax(200px, 1fr))`:**

- `repeat(...)` — create a repeating column pattern
- `auto-fill` — automatically add as many columns as will fit in the available width
- `minmax(200px, 1fr)` — each column is at minimum 200px wide, and can grow to fill equal fractions of the remaining space
- The browser figures out how many columns to show automatically — no JavaScript needed

**Expected Output at different screen widths:**
```
Desktop (1200px wide):   [ img ] [ img ] [ img ] [ img ] [ img ]  ← 5 columns
Tablet (768px wide):     [ img ] [ img ] [ img ]                  ← 3 columns
Mobile (400px wide):     [ img ] [ img ]                          ← 2 columns
Very small (250px wide): [ img ]                                   ← 1 column
```

### Using Media Queries for More Explicit Control

If you want to control exactly how many columns appear at each breakpoint:

```css
/* Gallery items — start with full width (mobile first) */
.gallery {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  padding: 10px;
}

.gallery-item {
  width: calc(100% - 10px);    /* Mobile: 1 item per row */
}

/* Tablet and above: 2 items per row */
@media only screen and (min-width: 480px) {
  .gallery-item {
    width: calc(50% - 10px);
  }
}

/* Desktop and above: 4 items per row */
@media only screen and (min-width: 768px) {
  .gallery-item {
    width: calc(25% - 10px);
  }
}
```

**Expected Output:**
- On screens narrower than 480px: one full-width image per row
- On screens 480px–767px: two images per row
- On screens 768px and wider: four images per row

> ⭐ **Best practice:** The CSS Grid `auto-fill` + `minmax` approach requires fewer lines of code and adapts more fluidly than media queries. Use it for most gallery layouts. Use explicit media queries when you need pixel-perfect control over exact column counts.

---

## Section 4 — Image Hover Overlay Effects

Hover overlay effects are one of the most visually impressive features of CSS galleries. When a user hovers over an image, a translucent layer fades in on top of it — often revealing the image caption, a zoom effect, or an action button.

### How an Overlay Works (The Mental Model)

Imagine a painting on a wall. Now imagine a glass panel that slides in front of the painting when you walk towards it. The glass is invisible until you get close, then it becomes visible.

In CSS:
- The **painting** is your `<img>` element
- The **glass panel** is an `::after` pseudo-element or an overlay `<div>` positioned absolutely on top of the image
- The **walking towards it** is the `:hover` state
- The **glass becoming visible** is `opacity` transitioning from `0` to `1`

### The Three-Layer Stack

Every gallery item with a hover overlay has this structure:

```
Layer 3 (top):    Overlay text / caption     ← position: absolute, shown on hover
Layer 2 (middle): Dark overlay panel         ← position: absolute, opacity 0 → 1
Layer 1 (bottom): The actual <img>           ← always visible
```

The parent `.gallery-item` holds all three layers together with `position: relative`.

### Basic Fade-In Overlay Example

```html
<!-- HTML -->
<div class="gallery-item">
  <img src="photo.jpg" alt="Mountain" />
  <div class="overlay">
    <div class="overlay-text">Mountain Range</div>
  </div>
</div>
```

```css
/* CSS */

/* The gallery item must be relative so the overlay positions inside it */
.gallery-item {
  position: relative;
  overflow: hidden;     /* Clips the overlay within the item boundaries */
  width: 250px;
  height: 170px;
}

/* Make the image fill the gallery item */
.gallery-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

/* The overlay sits exactly on top of the image */
.overlay {
  position: absolute;   /* Takes it out of normal flow */
  top: 0;               /* Start at the very top of .gallery-item */
  left: 0;              /* Start at the very left */
  width: 100%;          /* Cover the full width */
  height: 100%;         /* Cover the full height */
  background-color: rgba(0, 0, 0, 0.6);  /* Semi-transparent black */
  opacity: 0;           /* Invisible by default */
  transition: opacity 0.4s ease;          /* Smooth fade animation */

  /* Centre the overlay text */
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Show the overlay on hover */
.gallery-item:hover .overlay {
  opacity: 1;           /* Fully visible when parent is hovered */
}

/* Style the text inside the overlay */
.overlay-text {
  color: white;
  font-size: 16px;
  font-weight: bold;
  text-align: center;
  padding: 10px;
  letter-spacing: 1px;
}
```

**Expected Output:**
- Normal state: Image displays cleanly with no overlay visible
- On hover: A dark translucent panel fades smoothly over the image, revealing the white caption text in the centre

**Line-by-line explanation of the key parts:**

| CSS Line | What It Does |
|---|---|
| `position: relative` on `.gallery-item` | Creates a coordinate origin so `.overlay` can position itself inside |
| `overflow: hidden` on `.gallery-item` | Prevents the overlay from showing outside the item's box |
| `position: absolute` on `.overlay` | Removes it from normal flow so it sits on top of the image |
| `top: 0; left: 0; width: 100%; height: 100%` | Makes the overlay exactly cover the image |
| `opacity: 0` | Makes it invisible in the default state |
| `transition: opacity 0.4s ease` | Animates the fade-in over 0.4 seconds |
| `.gallery-item:hover .overlay { opacity: 1 }` | Triggers the fade-in when the parent is hovered |

---

### Zoom Effect on Hover

A popular alternative or complement to the overlay effect is a subtle zoom — the image grows slightly when hovered, creating a sense of life and interactivity.

```css
/* CSS */
.gallery-item {
  overflow: hidden;    /* CRITICAL: clips the zoomed image within the box */
  width: 250px;
  height: 170px;
}

.gallery-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.4s ease;   /* Animate the zoom */
}

/* Zoom the image on hover */
.gallery-item:hover img {
  transform: scale(1.1);   /* Scale to 110% of original size */
}
```

**Expected Output:**
- Normal state: Image at normal size
- On hover: Image smoothly grows to 110% of its size — a subtle but satisfying zoom effect. The `overflow: hidden` prevents the enlarged image from breaking outside the box boundaries.

> 💭 **Think about it:** What would happen if you removed `overflow: hidden` from `.gallery-item` before adding the zoom? The zoomed image would overflow its container and overlap neighbouring gallery items. `overflow: hidden` is the invisible guard that keeps the zoom contained.

---

### Combining Overlay and Zoom Together

The most professional gallery effect combines both — the image zooms AND an overlay fades in simultaneously:

```css
/* CSS — combined overlay + zoom */
.gallery-item {
  position: relative;
  overflow: hidden;
  width: 250px;
  height: 170px;
  border-radius: 6px;
  cursor: pointer;
}

.gallery-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.5s ease;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    to bottom,
    rgba(0,0,0,0) 40%,
    rgba(0,0,0,0.75) 100%
  );
  opacity: 0;
  transition: opacity 0.4s ease;
  display: flex;
  align-items: flex-end;
  padding: 16px;
}

.overlay-text {
  color: white;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 0.5px;
}

/* On hover: zoom the image AND show the overlay */
.gallery-item:hover img {
  transform: scale(1.08);
}

.gallery-item:hover .overlay {
  opacity: 1;
}
```

**Expected Output:**
- Normal state: Clean image, no overlay
- On hover: Image smoothly zooms to 108%, and a gradient overlay fades in from the bottom — the caption text appears over the dark gradient at the bottom of the image

This gradient overlay approach (`rgba(0,0,0,0)` at the top fading to `rgba(0,0,0,0.75)` at the bottom) is more elegant than a solid dark overlay. The image top remains clearly visible, and only the bottom where the caption sits has the dark gradient background.

---

## Section 5 — Full Responsive Gallery with Hover Effects

This is the complete gallery combining all the concepts: responsive grid, uniform images, and hover overlay with zoom.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Responsive Gallery with Hover Effects</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: Arial, sans-serif;
      background-color: #1a1a2e;
      padding: 30px 20px;
    }

    h2 {
      color: #fff;
      text-align: center;
      margin-bottom: 24px;
      letter-spacing: 2px;
      text-transform: uppercase;
      font-size: 20px;
    }

    /* Responsive grid: auto columns, minimum 200px each */
    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      gap: 14px;
      max-width: 900px;
      margin: 0 auto;
    }

    /* Gallery item: the parent container for image + overlay */
    .gallery-item {
      position: relative;
      overflow: hidden;
      border-radius: 8px;
      aspect-ratio: 4 / 3;  /* Maintains a 4:3 ratio as width changes */
      cursor: pointer;
      box-shadow: 0 4px 15px rgba(0,0,0,0.3);
    }

    /* Image fills the item completely */
    .gallery-item img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
      transition: transform 0.5s ease;
    }

    /* Gradient overlay — invisible by default */
    .overlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: linear-gradient(
        to bottom,
        transparent 30%,
        rgba(0, 0, 0, 0.8) 100%
      );
      opacity: 0;
      transition: opacity 0.4s ease;
      display: flex;
      flex-direction: column;
      justify-content: flex-end;
      padding: 14px;
    }

    .overlay-title {
      color: #fff;
      font-size: 15px;
      font-weight: bold;
      margin-bottom: 4px;
    }

    .overlay-subtitle {
      color: rgba(255,255,255,0.75);
      font-size: 12px;
    }

    /* Hover effects */
    .gallery-item:hover img {
      transform: scale(1.08);
    }

    .gallery-item:hover .overlay {
      opacity: 1;
    }

    /* Small screens: force 2 columns */
    @media (max-width: 400px) {
      .gallery {
        grid-template-columns: repeat(2, 1fr);
      }
    }
  </style>
</head>
<body>

  <h2>Africa Through the Lens</h2>

  <div class="gallery">

    <div class="gallery-item">
      <img src="https://via.placeholder.com/400x300/4a8f6e/ffffff?text=Lagos" alt="Lagos" />
      <div class="overlay">
        <div class="overlay-title">Lagos, Nigeria</div>
        <div class="overlay-subtitle">West Africa</div>
      </div>
    </div>

    <div class="gallery-item">
      <img src="https://via.placeholder.com/400x300/1a6b8a/ffffff?text=Nairobi" alt="Nairobi" />
      <div class="overlay">
        <div class="overlay-title">Nairobi, Kenya</div>
        <div class="overlay-subtitle">East Africa</div>
      </div>
    </div>

    <div class="gallery-item">
      <img src="https://via.placeholder.com/400x300/8b3a1a/ffffff?text=Cairo" alt="Cairo" />
      <div class="overlay">
        <div class="overlay-title">Cairo, Egypt</div>
        <div class="overlay-subtitle">North Africa</div>
      </div>
    </div>

    <div class="gallery-item">
      <img src="https://via.placeholder.com/400x300/2c7bb6/ffffff?text=Cape+Town" alt="Cape Town" />
      <div class="overlay">
        <div class="overlay-title">Cape Town, S.A.</div>
        <div class="overlay-subtitle">Southern Africa</div>
      </div>
    </div>

    <div class="gallery-item">
      <img src="https://via.placeholder.com/400x300/6b5b2e/ffffff?text=Accra" alt="Accra" />
      <div class="overlay">
        <div class="overlay-title">Accra, Ghana</div>
        <div class="overlay-subtitle">West Africa</div>
      </div>
    </div>

    <div class="gallery-item">
      <img src="https://via.placeholder.com/400x300/4a3a8f/ffffff?text=Addis+Ababa" alt="Addis Ababa" />
      <div class="overlay">
        <div class="overlay-title">Addis Ababa</div>
        <div class="overlay-subtitle">East Africa</div>
      </div>
    </div>

  </div>
</body>
</html>
```

**Expected Output:** A dark-themed gallery page with six city images in a responsive grid. On hover, each image zooms slightly and a gradient overlay fades in from the bottom revealing the city name and region.

---

## PART TWO — CSS Image Sprites

---

## Section 6 — What Is an Image Sprite?

### The Problem Sprites Solve

Every time a web browser needs to display an image, it must make a separate **HTTP request** to the web server — it asks the server, "Please send me this image file." This is like making a separate phone call for each item on your shopping list. If your page has 15 small icons, the browser makes 15 separate requests.

Each request takes time — even if small, it adds up:
- Request 1: `home-icon.png` → 50ms
- Request 2: `search-icon.png` → 45ms
- Request 3: `cart-icon.png` → 52ms
- …and so on for 15 icons = potentially 750ms+ of waiting

**The sprite solution:** Combine all 15 icons into a single image file. The browser makes just ONE request and downloads all 15 icons in one go. Then CSS tells each element which *portion* of that combined image to display.

This is exactly like a film strip. A film strip is one long piece of film containing many individual frames. A projector shows one frame at a time by positioning the right frame in front of the light. CSS sprites work the same way: one image file, many individual pictures, a CSS "window" that shows just the one you want.

### Visual Diagram of a Sprite Sheet

Imagine a sprite sheet that looks like this (greatly simplified):

```
Sprite sheet: img_icons.png (total size: 180px × 60px)
+------------------+------------------+------------------+
|                  |                  |                  |
|   HOME ICON      |   SEARCH ICON    |   CART ICON      |
|   (60×60px)      |   (60×60px)      |   (60×60px)      |
|                  |                  |                  |
+------------------+------------------+------------------+
  x=0, y=0          x=60, y=0          x=120, y=0
```

To display the home icon, you tell CSS:
- Use `img_icons.png` as the background image
- Set the element width to 60px and height to 60px
- Position the background at `0 0` (show from the left edge, top edge)

To display the search icon:
- Use the same `img_icons.png`
- Set width to 60px and height to 60px
- Position the background at `-60px 0` (shift the image 60px LEFT so the search icon aligns with the window)

The negative value shifts the image so the right part comes into view. Think of it as sliding the entire film strip to the left until the frame you want is visible.

### Why Negative Values in `background-position`?

This confuses most beginners, so let's slow down and explain it carefully.

The browser creates a **fixed viewport window** the size of your element (for example, 60×60px). The sprite sheet sits *behind* this window. By default, the sprite sheet starts at position `0 0` — its top-left corner aligns with the window's top-left corner.

When you write `background-position: -60px 0`:
- You are moving the *sprite sheet* 60px to the LEFT
- This means the part of the sprite sheet now visible through the 60×60 window is the section that starts 60px from the left edge — which is the second icon

```
background-position: 0 0         background-position: -60px 0
+------------------+             +------------------+
| HOME     |search |             |search    | CART  |
| VISIBLE  |hidden |             | VISIBLE  |hidden |
+------------------+             +------------------+
↑ window edge                    ↑ window edge
(sprite moved 0px left)          (sprite moved 60px left)
```

---

## Section 7 — Basic Sprite Usage

### Simple Example — Three Navigation Icons

```html
<!-- HTML -->
<!-- Each img starts with a tiny 1×1 transparent placeholder.
     The src must not be empty, but the actual display
     comes from the CSS background-image. -->
<img id="home"  src="img_trans.gif" width="1" height="1" alt="Home" />
<img id="prev"  src="img_trans.gif" width="1" height="1" alt="Previous" />
<img id="next"  src="img_trans.gif" width="1" height="1" alt="Next" />
```

```css
/* CSS */

/* Home icon — positioned at the very start of the sprite (0, 0) */
#home {
  width: 46px;
  height: 44px;
  background-image: url("img_navsprites.gif");
  background-position: 0 0;           /* Top-left: this is the home icon */
}

/* Previous icon — starts 47px to the right of the home icon */
#prev {
  width: 43px;
  height: 44px;
  background-image: url("img_navsprites.gif");
  background-position: -47px 0;       /* Move sprite 47px left to reveal prev icon */
}

/* Next icon — starts 91px to the right of the start */
#next {
  width: 43px;
  height: 44px;
  background-image: url("img_navsprites.gif");
  background-position: -91px 0;       /* Move sprite 91px left to reveal next icon */
}
```

**Expected Output:** Three icon images rendered side by side. Each shows a different portion of the single sprite file. The browser made ONE network request for `img_navsprites.gif`, not three separate requests.

### Modern Alternative: Using `<div>` Instead of `<img>`

In modern CSS, it is more common to use `<div>` or `<span>` elements for sprite icons rather than `<img>` tags. This avoids the awkward empty `src` attribute:

```html
<!-- Modern approach using div elements -->
<div class="icon icon-home"></div>
<div class="icon icon-search"></div>
<div class="icon icon-cart"></div>
```

```css
/* CSS */

/* Shared styles for all sprite icons */
.icon {
  width: 40px;
  height: 40px;
  background-image: url("icons-sprite.png");
  background-repeat: no-repeat;
  display: inline-block;    /* Make divs sit side by side */
}

/* Individual positions for each icon */
.icon-home   { background-position:  0px  0px; }
.icon-search { background-position: -40px 0px; }
.icon-cart   { background-position: -80px 0px; }
```

**Expected Output:** Three icons displayed side by side, each showing a different part of the sprite image.

---

## Section 8 — Sprite Navigation Bar with Hover States

The most powerful use of sprites is a navigation bar where each item has a **normal state** and a **hover state** — and both states live in the same sprite file!

### How It Works

The sprite sheet is designed so that:
- Row 1 (y = 0): All normal/default icon states
- Row 2 (y = -60px): All hover/active icon states

```
Sprite sheet: img_navsprites_hover.gif
+----------+----------+----------+
| Home     | Prev     | Next     |  ← Row 1: normal icons (y=0)
| (normal) | (normal) | (normal) |
+----------+----------+----------+
| Home     | Prev     | Next     |  ← Row 2: hover icons (y=-60px)
| (hover)  | (hover)  | (hover)  |
+----------+----------+----------+
  x=0        x=-47px    x=-91px
```

To show the hover version of the home icon:
- Move the sprite 0px horizontally (home icon is still in the first column)
- Move the sprite 60px UPWARD (use `-60px` for y), which reveals the hover row

### Navigation Bar with Hover Effect

```html
<!-- HTML -->
<ul id="navlist">
  <li id="home">  <a href="#" title="Home"></a>     </li>
  <li id="prev">  <a href="#" title="Previous"></a> </li>
  <li id="next">  <a href="#" title="Next"></a>     </li>
</ul>
```

```css
/* CSS */

/* Reset the list */
#navlist {
  position: relative;
  height: 44px;
  list-style: none;
  padding: 0;
  margin: 0;
}

/* Position each list item absolutely */
#navlist li {
  margin: 0;
  padding: 0;
  position: absolute;
  top: 0;
}

/* Make each link a clickable block */
#navlist li a {
  display: block;
  height: 44px;
  text-decoration: none;
}

/* ---- Home icon ---- */
#home      { left: 0;   }
#home a    { width: 46px; background: url("img_navsprites_hover.gif") 0 0; }
#home a:hover { background-position: 0 -45px; }   /* Shift down to row 2 */

/* ---- Previous icon ---- */
#prev      { left: 63px; }
#prev a    { width: 43px; background: url("img_navsprites_hover.gif") -47px 0; }
#prev a:hover { background-position: -47px -45px; }

/* ---- Next icon ---- */
#next      { left: 129px; }
#next a    { width: 43px; background: url("img_navsprites_hover.gif") -91px 0; }
#next a:hover { background-position: -91px -45px; }
```

**Expected Output:**
- Normal state: Three navigation icons shown from row 1 of the sprite
- On hover over home icon: The background shifts to row 2 (y = -45px), revealing the highlighted version of the home icon — instant visual feedback, ZERO additional network requests

### Using Emoji as a Sprite Simulation (No Image File Needed)

Since real sprite image files are not available in this lesson environment, here is a fully working simulation using CSS background colours to demonstrate the sprite concept. The same CSS logic applies perfectly to real sprite images:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    body { font-family: Arial, sans-serif; padding: 30px; background: #f5f5f5; }
    h3 { margin-bottom: 16px; color: #333; }

    /* ---- SIMULATED SPRITE SHEET ----
       In a real project, this would be ONE background-image url pointing to
       a PNG sprite sheet. Here we use coloured backgrounds to simulate it. */

    .nav-bar {
      display: flex;
      gap: 4px;
      background: #2c3e50;
      padding: 8px 12px;
      border-radius: 8px;
      display: inline-flex;
    }

    /* Base icon style — this is what all sprite icons share */
    .nav-icon {
      width: 44px;
      height: 44px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 20px;
      border-radius: 6px;
      cursor: pointer;
      transition: background-color 0.2s ease, transform 0.2s ease;
      color: rgba(255,255,255,0.7);
      /* In a real sprite implementation this would be:
         background-image: url("nav-sprite.png");
         background-repeat: no-repeat;
         width: 44px;
         height: 44px;    */
    }

    /* Normal state background positions (simulated with colours) */
    .nav-icon-home    { background-color: transparent; }
    .nav-icon-search  { background-color: transparent; }
    .nav-icon-cart    { background-color: transparent; }
    .nav-icon-profile { background-color: transparent; }
    .nav-icon-menu    { background-color: transparent; }

    /* Hover states — in a sprite this would change background-position */
    .nav-icon:hover {
      background-color: rgba(255,255,255,0.15);
      color: #ffffff;
      transform: translateY(-2px);
    }

    /* In a real sprite: */
    /* .nav-icon-home:hover   { background-position:  0px -44px; } */
    /* .nav-icon-search:hover { background-position: -44px -44px; } */
    /* .nav-icon-cart:hover   { background-position: -88px -44px; } */

    .sprite-label {
      margin-top: 20px;
      font-size: 13px;
      color: #888;
      font-style: italic;
    }

    .comparison-box {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 20px;
      margin-top: 20px;
      max-width: 600px;
    }
    .comparison-card {
      background: white;
      border: 1px solid #ddd;
      border-radius: 8px;
      padding: 16px;
    }
    .comparison-card h4 {
      font-size: 13px;
      margin-bottom: 8px;
      color: #555;
    }
    .req-item {
      font-size: 12px;
      padding: 3px 0;
      color: #888;
      border-bottom: 1px solid #f0f0f0;
    }
    .req-item.single {
      color: #27ae60;
      font-weight: bold;
    }
    .total {
      font-size: 13px;
      font-weight: bold;
      margin-top: 8px;
      padding-top: 6px;
      border-top: 2px solid #ddd;
    }
    .bad  { color: #e74c3c; }
    .good { color: #27ae60; }
  </style>
</head>
<body>

  <h3>Sprite-style Navigation Bar</h3>

  <div class="nav-bar">
    <div class="nav-icon nav-icon-home"    title="Home">🏠</div>
    <div class="nav-icon nav-icon-search"  title="Search">🔍</div>
    <div class="nav-icon nav-icon-cart"    title="Cart">🛒</div>
    <div class="nav-icon nav-icon-profile" title="Profile">👤</div>
    <div class="nav-icon nav-icon-menu"    title="Menu">☰</div>
  </div>

  <p class="sprite-label">↑ Hover over each icon. In a real sprite implementation, 
  all 5 icons + their hover states would be loaded in ONE network request.</p>

  <h3>HTTP Request Comparison</h3>

  <div class="comparison-box">
    <div class="comparison-card">
      <h4>❌ Without Sprites (5 separate images)</h4>
      <div class="req-item">GET home.png → 45ms</div>
      <div class="req-item">GET search.png → 52ms</div>
      <div class="req-item">GET cart.png → 48ms</div>
      <div class="req-item">GET profile.png → 51ms</div>
      <div class="req-item">GET menu.png → 49ms</div>
      <div class="total bad">5 requests · ~245ms total</div>
    </div>
    <div class="comparison-card">
      <h4>✅ With Sprites (1 combined image)</h4>
      <div class="req-item single">GET icons-sprite.png → 55ms</div>
      <div class="req-item" style="color: transparent">·</div>
      <div class="req-item" style="color: transparent">·</div>
      <div class="req-item" style="color: transparent">·</div>
      <div class="req-item" style="color: transparent">·</div>
      <div class="total good">1 request · ~55ms total</div>
    </div>
  </div>

</body>
</html>
```

**Expected Output:** A dark navigation bar with five icon buttons. Hovering reveals a highlighted state. The comparison cards below show the dramatic difference in network requests between sprite and non-sprite approaches.

---

## Section 9 — How to Calculate `background-position` for Any Sprite

This section teaches you the systematic method for finding the correct position values for any icon in any sprite sheet.

### The Formula

```
background-position-x = -(distance from LEFT edge of sprite to the icon's left edge)
background-position-y = -(distance from TOP edge of sprite to the icon's top edge)
```

### Worked Example

Suppose you have a sprite sheet that is 200px wide × 100px tall, with four 50×50px icons arranged in a 2×2 grid:

```
Sprite sheet: icons.png (200px × 100px)
+-------------------+-------------------+
|                   |                   |
|    ICON A         |    ICON B         |  ← Row 1 (y=0 to y=49)
|    (50×50)        |    (50×50)        |
|                   |                   |
+-------------------+-------------------+
|                   |                   |
|    ICON C         |    ICON D         |  ← Row 2 (y=50 to y=99)
|    (50×50)        |    (50×50)        |
|                   |                   |
+-------------------+-------------------+
 x=0 to x=49          x=50 to x=99
```

To display each icon:

```css
/* Icon A — top-left corner of the sprite */
.icon-a {
  width: 50px;
  height: 50px;
  background-image: url("icons.png");
  background-repeat: no-repeat;
  background-position: 0 0;           /* 0px from left, 0px from top */
}

/* Icon B — 50px from the left edge */
.icon-b {
  width: 50px;
  height: 50px;
  background-image: url("icons.png");
  background-repeat: no-repeat;
  background-position: -50px 0;       /* 50px from left, 0px from top */
}

/* Icon C — 50px from the top edge */
.icon-c {
  width: 50px;
  height: 50px;
  background-image: url("icons.png");
  background-repeat: no-repeat;
  background-position: 0 -50px;       /* 0px from left, 50px from top */
}

/* Icon D — 50px from left AND 50px from top */
.icon-d {
  width: 50px;
  height: 50px;
  background-image: url("icons.png");
  background-repeat: no-repeat;
  background-position: -50px -50px;   /* 50px from left, 50px from top */
}
```

### Practical Tools for Finding Sprite Positions

In real professional work, you do not calculate positions by hand. You use tools:

- **SpriteCow** (spritecow.com) — upload a sprite sheet, hover over an icon, and it gives you the exact CSS
- **CSS Sprite Generator** (spritegen.website-performance.org) — upload images, it generates the combined sprite and all CSS
- **Browser DevTools** — open Chrome DevTools, use the `Computed` panel to inspect the background-position of any element
- **Image editor rulers** — in Photoshop, Figma, or GIMP, hover over a pixel and the coordinates are shown in the toolbar

---

## Section 10 — Sprite Best Practices

### Tip 1 — Group Related Icons Together
Keep icons that are used together in the same sprite sheet. Don't mix navigation icons, social media icons, and product category icons in one massive sheet.

```
✅ Good: nav-sprite.png (home, search, cart, profile, menu)
✅ Good: social-sprite.png (facebook, twitter, instagram, linkedin)
❌ Bad:  everything-sprite.png (50+ unrelated icons all mixed together)
```

### Tip 2 — Leave Padding Between Icons
When CSS scales, rotates, or blurs elements, colours from neighbouring icons in the sprite can "bleed" into the current icon's window. A 2–5px gap prevents this.

### Tip 3 — Use Consistent Icon Sizes
Design all icons in a sprite at the same dimensions (e.g., all 40×40px). This makes position calculations simple and predictable.

### Tip 4 — Use `background-repeat: no-repeat`
Always add this when working with sprites. Without it, the sprite image tiles across the element, showing unwanted repeated copies of other icons.

```css
/* Always include this! */
.icon {
  background-image: url("sprite.png");
  background-repeat: no-repeat;   /* ← ESSENTIAL */
}
```

### Tip 5 — When NOT to Use Sprites
- **SVG icon fonts** (like Font Awesome) are often better for purely vector icons — they scale perfectly on retina screens
- **Inline SVGs** give you CSS control over individual parts (colour, stroke)
- **HTTP/2** server connections reduce the HTTP request penalty, so sprites give slightly less benefit on modern servers — but they are still worthwhile

---

## Part Three — Guided Practice Exercises

### Exercise 1 — Build a Fixed Gallery

**Objective:** Create a gallery of six images arranged in a 3-column grid with borders, uniform sizes, and captions.

**Scenario:** You are building a "Team Members" section for a company website. Display six team member photos in a 3-column grid, each with the person's name below their photo.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    body { font-family: Arial, sans-serif; background: #f4f4f4; padding: 30px; }

    h2 { text-align: center; color: #333; margin-bottom: 24px; }

    .gallery {
      display: flex;
      flex-wrap: wrap;
      gap: 16px;
      justify-content: center;
    }

    .gallery-item {
      width: 180px;
      border: 2px solid #ddd;
      border-radius: 8px;
      overflow: hidden;
      background: white;
      text-align: center;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .gallery-item img {
      width: 180px;
      height: 180px;
      object-fit: cover;
      display: block;
    }

    .caption {
      padding: 10px 8px;
      font-size: 14px;
      font-weight: bold;
      color: #333;
    }

    .caption .role {
      font-size: 12px;
      font-weight: normal;
      color: #888;
      margin-top: 2px;
    }
  </style>
</head>
<body>

  <h2>Meet Our Team</h2>

  <div class="gallery">
    <div class="gallery-item">
      <img src="https://via.placeholder.com/180x180/4a90d9/fff?text=CK" alt="Chidi Kelechi" />
      <div class="caption">Chidi Kelechi <div class="role">CEO &amp; Founder</div></div>
    </div>
    <div class="gallery-item">
      <img src="https://via.placeholder.com/180x180/e74c3c/fff?text=AA" alt="Adaeze Agu" />
      <div class="caption">Adaeze Agu <div class="role">Lead Designer</div></div>
    </div>
    <div class="gallery-item">
      <img src="https://via.placeholder.com/180x180/27ae60/fff?text=EM" alt="Emeka Madu" />
      <div class="caption">Emeka Madu <div class="role">Head of Engineering</div></div>
    </div>
    <div class="gallery-item">
      <img src="https://via.placeholder.com/180x180/8e44ad/fff?text=ZO" alt="Zara Osei" />
      <div class="caption">Zara Osei <div class="role">Marketing Manager</div></div>
    </div>
    <div class="gallery-item">
      <img src="https://via.placeholder.com/180x180/e67e22/fff?text=KB" alt="Kwame Boateng" />
      <div class="caption">Kwame Boateng <div class="role">Data Analyst</div></div>
    </div>
    <div class="gallery-item">
      <img src="https://via.placeholder.com/180x180/16a085/fff?text=FN" alt="Fatima Ndiaye" />
      <div class="caption">Fatima Ndiaye <div class="role">Customer Success</div></div>
    </div>
  </div>

</body>
</html>
```

**Expected Output:** Six team member "photo" cards arranged in rows of three. Each card has a coloured placeholder image with initials, and below it the person's name and role in styled text.

**Self-check Questions:**
- What happens if you remove `flex-wrap: wrap`?
- What does `object-fit: cover` do to the images?
- How would you change this to a 2-column layout?

---

### Exercise 2 — Adding Hover Overlay to a Gallery

**Objective:** Take the gallery from Exercise 1 and add a hover overlay effect that reveals an "info" panel over each photo.

```css
/* Add these styles to your Exercise 1 code */

/* Make items position-relative for absolute overlay */
.gallery-item {
  position: relative;   /* Add this to existing .gallery-item rule */
  cursor: pointer;
}

/* Overlay panel */
.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 180px;          /* Match the image height */
  background-color: rgba(74, 144, 217, 0.85);
  opacity: 0;
  transition: opacity 0.35s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.overlay span {
  color: white;
  font-size: 13px;
  font-weight: bold;
  text-align: center;
  padding: 10px;
}

/* Show overlay on hover */
.gallery-item:hover .overlay {
  opacity: 1;
}
```

```html
<!-- Add this overlay div inside each .gallery-item, after the img -->
<div class="overlay"><span>View Profile</span></div>
```

**Expected Output:** Same gallery as Exercise 1, but hovering over any team member photo reveals a blue translucent overlay with "View Profile" text.

---

### Exercise 3 — Responsive Gallery with Media Queries

**Objective:** Create a gallery that shows 4 columns on desktop, 2 on tablet, 1 on mobile.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    body { font-family: Arial, sans-serif; background: #1c1c2e; padding: 20px; }
    h2 { color: white; text-align: center; margin-bottom: 20px; }

    .gallery {
      display: grid;
      grid-template-columns: repeat(4, 1fr);   /* 4 columns by default */
      gap: 10px;
    }

    .gallery-item {
      overflow: hidden;
      border-radius: 6px;
      aspect-ratio: 1;                          /* Square items */
      position: relative;
    }

    .gallery-item img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
      transition: transform 0.4s ease;
    }

    .gallery-item:hover img { transform: scale(1.1); }

    /* Tablet: 2 columns */
    @media (max-width: 700px) {
      .gallery { grid-template-columns: repeat(2, 1fr); }
    }

    /* Mobile: 1 column */
    @media (max-width: 400px) {
      .gallery { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>
  <h2>Photo Collection</h2>
  <div class="gallery">
    <div class="gallery-item"><img src="https://via.placeholder.com/300x300/4a8f6e/fff?text=1" alt="1" /></div>
    <div class="gallery-item"><img src="https://via.placeholder.com/300x300/2c7bb6/fff?text=2" alt="2" /></div>
    <div class="gallery-item"><img src="https://via.placeholder.com/300x300/8b3a1a/fff?text=3" alt="3" /></div>
    <div class="gallery-item"><img src="https://via.placeholder.com/300x300/6b5b2e/fff?text=4" alt="4" /></div>
    <div class="gallery-item"><img src="https://via.placeholder.com/300x300/4a3a8f/fff?text=5" alt="5" /></div>
    <div class="gallery-item"><img src="https://via.placeholder.com/300x300/8e44ad/fff?text=6" alt="6" /></div>
    <div class="gallery-item"><img src="https://via.placeholder.com/300x300/16a085/fff?text=7" alt="7" /></div>
    <div class="gallery-item"><img src="https://via.placeholder.com/300x300/e67e22/fff?text=8" alt="8" /></div>
  </div>
</body>
</html>
```

**Expected Output:** On a wide screen: 8 images in a 4×2 grid. Resize the browser to below 700px: 4 rows of 2. Below 400px: 8 individual full-width images stacked.

---

### Exercise 4 — Sprite Position Calculator

**Objective:** Practice calculating `background-position` values without a real image.

Given this sprite layout where every icon is exactly **50×50px**:

```
Sprite sheet: 150px wide × 100px tall
+------------------+------------------+------------------+
| PLAY (50×50)     | PAUSE (50×50)    | STOP (50×50)     |  ← Row 1 (y=0)
| x=0, y=0         | x=50, y=0        | x=100, y=0       |
+------------------+------------------+------------------+
| PLAY HOVER       | PAUSE HOVER      | STOP HOVER       |  ← Row 2 (y=-50)
| x=0, y=50        | x=50, y=50       | x=100, y=50      |
+------------------+------------------+------------------+
```

Fill in the correct `background-position` values:

```css
/* Normal states */
.play  { background-position: ___; }    /* Answer: 0 0 */
.pause { background-position: ___; }    /* Answer: -50px 0 */
.stop  { background-position: ___; }    /* Answer: -100px 0 */

/* Hover states */
.play:hover  { background-position: ___; }   /* Answer: 0 -50px */
.pause:hover { background-position: ___; }   /* Answer: -50px -50px */
.stop:hover  { background-position: ___; }   /* Answer: -100px -50px */
```

**Self-check:** Remember the formula: the value is the *negative* distance from the left edge (for x) and *negative* distance from the top edge (for y) to the icon you want to show.

---

## Part Four — Mini Project: Portfolio Gallery with Sprite Icon Toolbar

### Project Overview

You will build a complete **Photography Portfolio Page** that combines everything from this lesson:

1. A responsive image gallery grid with hover overlay effects
2. A sprite-simulated icon toolbar at the top (using CSS techniques that mirror real sprite implementation)
3. A filter button row that categorises photos

This mirrors exactly how professional portfolio websites like Behance, Dribbble, and 500px are built.

---

### Complete Project Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Amara Obi — Photography Portfolio</title>
  <style>

    /* ============================================
       RESET AND BASE
       ============================================ */
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      background-color: #0f0f1a;
      color: #e0e0e0;
      min-height: 100vh;
    }

    /* ============================================
       HEADER + SPRITE-STYLE ICON TOOLBAR
       ============================================ */
    header {
      background-color: #16162a;
      border-bottom: 1px solid rgba(255,255,255,0.08);
      padding: 0 24px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      height: 60px;
    }

    .logo {
      font-size: 18px;
      font-weight: bold;
      color: #fff;
      letter-spacing: 1px;
    }

    .logo span { color: #4a90d9; }

    /* Sprite-style icon toolbar
       In production: replace emoji with background-image + background-position
       on a real sprite sheet PNG. The CSS structure is identical. */
    .icon-toolbar {
      display: flex;
      gap: 4px;
    }

    /* Base class shared by all icons — mirrors sprite technique */
    .toolbar-icon {
      width: 38px;
      height: 38px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 6px;
      cursor: pointer;
      font-size: 17px;
      color: rgba(255,255,255,0.5);
      transition: background-color 0.2s ease, color 0.2s ease, transform 0.15s ease;
      /* Real sprite version would use:
         background-image: url("toolbar-sprite.png");
         background-repeat: no-repeat;
         width: 38px;
         height: 38px;      */
    }

    /* Hover state — mirrors changing background-position to a hover row */
    .toolbar-icon:hover {
      background-color: rgba(74, 144, 217, 0.2);
      color: #4a90d9;
      transform: translateY(-1px);
    }

    /* Active/selected state */
    .toolbar-icon.active {
      background-color: rgba(74, 144, 217, 0.25);
      color: #4a90d9;
    }

    /* ============================================
       PAGE CONTENT WRAPPER
       ============================================ */
    .content {
      max-width: 1000px;
      margin: 0 auto;
      padding: 32px 20px;
    }

    /* ============================================
       SECTION HEADER + FILTER BUTTONS
       ============================================ */
    .section-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 20px;
      flex-wrap: wrap;
      gap: 12px;
    }

    .section-title {
      font-size: 22px;
      font-weight: bold;
      color: #fff;
    }

    .section-title span { color: #4a90d9; }

    .filter-row {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
    }

    .filter-btn {
      padding: 6px 16px;
      border-radius: 20px;
      font-size: 13px;
      cursor: pointer;
      border: 1px solid rgba(255,255,255,0.15);
      background: transparent;
      color: rgba(255,255,255,0.6);
      transition: all 0.2s ease;
    }

    .filter-btn:hover,
    .filter-btn.active {
      background-color: #4a90d9;
      border-color: #4a90d9;
      color: #fff;
    }

    /* ============================================
       RESPONSIVE GALLERY GRID
       ============================================ */
    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
      gap: 12px;
    }

    /* ============================================
       GALLERY ITEM (position: relative for overlay)
       ============================================ */
    .gallery-item {
      position: relative;
      overflow: hidden;
      border-radius: 8px;
      aspect-ratio: 4 / 3;
      cursor: pointer;
      box-shadow: 0 4px 16px rgba(0,0,0,0.4);
    }

    /* Image fills item, zoom transition */
    .gallery-item img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
      transition: transform 0.5s ease;
    }

    /* Overlay: gradient + hidden by default */
    .overlay {
      position: absolute;
      inset: 0;             /* shorthand for top:0; left:0; right:0; bottom:0 */
      background: linear-gradient(
        to bottom,
        rgba(0,0,0,0.05) 0%,
        rgba(15, 15, 26, 0.88) 100%
      );
      opacity: 0;
      transition: opacity 0.38s ease;
      display: flex;
      flex-direction: column;
      justify-content: flex-end;
      padding: 16px;
    }

    .overlay-category {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 1.5px;
      color: #4a90d9;
      margin-bottom: 4px;
    }

    .overlay-title {
      font-size: 15px;
      font-weight: bold;
      color: #fff;
      margin-bottom: 6px;
    }

    .overlay-actions {
      display: flex;
      gap: 6px;
    }

    .overlay-btn {
      font-size: 11px;
      padding: 4px 10px;
      border-radius: 12px;
      border: 1px solid rgba(255,255,255,0.4);
      color: rgba(255,255,255,0.8);
      background: rgba(255,255,255,0.1);
      cursor: pointer;
      transition: background 0.2s;
    }

    .overlay-btn:hover { background: rgba(255,255,255,0.25); }

    /* Hover triggers: zoom image, show overlay */
    .gallery-item:hover img {
      transform: scale(1.07);
    }

    .gallery-item:hover .overlay {
      opacity: 1;
    }

    /* "Featured" item spans 2 columns */
    .gallery-item.featured {
      grid-column: span 2;
      aspect-ratio: 16 / 9;
    }

    /* ============================================
       STATS BAR BELOW GALLERY
       ============================================ */
    .stats-bar {
      display: flex;
      gap: 30px;
      margin-top: 28px;
      padding: 16px 0;
      border-top: 1px solid rgba(255,255,255,0.08);
      justify-content: center;
      flex-wrap: wrap;
    }

    .stat {
      text-align: center;
    }

    .stat-number {
      font-size: 24px;
      font-weight: bold;
      color: #4a90d9;
    }

    .stat-label {
      font-size: 12px;
      color: rgba(255,255,255,0.5);
      margin-top: 2px;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    /* ============================================
       RESPONSIVE ADJUSTMENTS
       ============================================ */
    @media (max-width: 600px) {
      .gallery {
        grid-template-columns: repeat(2, 1fr);
      }
      .gallery-item.featured {
        grid-column: span 2;
      }
    }

    @media (max-width: 380px) {
      .gallery {
        grid-template-columns: 1fr;
      }
      .gallery-item.featured {
        grid-column: span 1;
      }
    }

  </style>
</head>
<body>

  <!-- HEADER WITH SPRITE-STYLE TOOLBAR -->
  <header>
    <div class="logo">Amara <span>Obi</span></div>

    <div class="icon-toolbar">
      <!-- These icons simulate a sprite sheet navigation bar.
           In production each .toolbar-icon would use:
           background-image: url("toolbar-sprite.png");
           background-repeat: no-repeat;
           background-position: [calculated px values];     -->
      <div class="toolbar-icon active" title="Gallery View">⊞</div>
      <div class="toolbar-icon" title="List View">≡</div>
      <div class="toolbar-icon" title="Favourites">♡</div>
      <div class="toolbar-icon" title="Upload">⬆</div>
      <div class="toolbar-icon" title="Share">↗</div>
      <div class="toolbar-icon" title="Settings">⚙</div>
    </div>
  </header>

  <!-- MAIN CONTENT -->
  <div class="content">

    <!-- SECTION HEADER + FILTERS -->
    <div class="section-header">
      <div class="section-title">My <span>Portfolio</span></div>
      <div class="filter-row">
        <button class="filter-btn active">All</button>
        <button class="filter-btn">Landscape</button>
        <button class="filter-btn">Portrait</button>
        <button class="filter-btn">Urban</button>
        <button class="filter-btn">Wildlife</button>
      </div>
    </div>

    <!-- GALLERY GRID -->
    <div class="gallery">

      <!-- Featured item spans 2 columns -->
      <div class="gallery-item featured">
        <img src="https://via.placeholder.com/880x495/2c5282/ffffff?text=Lagos+Golden+Hour" alt="Lagos Golden Hour" />
        <div class="overlay">
          <div class="overlay-category">Landscape</div>
          <div class="overlay-title">Lagos Golden Hour</div>
          <div class="overlay-actions">
            <button class="overlay-btn">♡ Like</button>
            <button class="overlay-btn">⬇ Save</button>
          </div>
        </div>
      </div>

      <div class="gallery-item">
        <img src="https://via.placeholder.com/440x330/4a8f6e/ffffff?text=Market+Life" alt="Market Life" />
        <div class="overlay">
          <div class="overlay-category">Urban</div>
          <div class="overlay-title">Market Life</div>
          <div class="overlay-actions">
            <button class="overlay-btn">♡ Like</button>
            <button class="overlay-btn">⬇ Save</button>
          </div>
        </div>
      </div>

      <div class="gallery-item">
        <img src="https://via.placeholder.com/440x330/8b3a1a/ffffff?text=Savanna+Dusk" alt="Savanna Dusk" />
        <div class="overlay">
          <div class="overlay-category">Wildlife</div>
          <div class="overlay-title">Savanna Dusk</div>
          <div class="overlay-actions">
            <button class="overlay-btn">♡ Like</button>
            <button class="overlay-btn">⬇ Save</button>
          </div>
        </div>
      </div>

      <div class="gallery-item">
        <img src="https://via.placeholder.com/440x330/5b2d8e/ffffff?text=City+Portrait" alt="City Portrait" />
        <div class="overlay">
          <div class="overlay-category">Portrait</div>
          <div class="overlay-title">City Portrait</div>
          <div class="overlay-actions">
            <button class="overlay-btn">♡ Like</button>
            <button class="overlay-btn">⬇ Save</button>
          </div>
        </div>
      </div>

      <div class="gallery-item">
        <img src="https://via.placeholder.com/440x330/1a6b8a/ffffff?text=Coastal+Mist" alt="Coastal Mist" />
        <div class="overlay">
          <div class="overlay-category">Landscape</div>
          <div class="overlay-title">Coastal Mist</div>
          <div class="overlay-actions">
            <button class="overlay-btn">♡ Like</button>
            <button class="overlay-btn">⬇ Save</button>
          </div>
        </div>
      </div>

      <div class="gallery-item">
        <img src="https://via.placeholder.com/440x330/6b8e23/ffffff?text=Forest+Rain" alt="Forest Rain" />
        <div class="overlay">
          <div class="overlay-category">Wildlife</div>
          <div class="overlay-title">Forest Rain</div>
          <div class="overlay-actions">
            <button class="overlay-btn">♡ Like</button>
            <button class="overlay-btn">⬇ Save</button>
          </div>
        </div>
      </div>

      <div class="gallery-item">
        <img src="https://via.placeholder.com/440x330/c47a1b/ffffff?text=Street+Story" alt="Street Story" />
        <div class="overlay">
          <div class="overlay-category">Urban</div>
          <div class="overlay-title">Street Story</div>
          <div class="overlay-actions">
            <button class="overlay-btn">♡ Like</button>
            <button class="overlay-btn">⬇ Save</button>
          </div>
        </div>
      </div>

    </div><!-- end .gallery -->

    <!-- STATS BAR -->
    <div class="stats-bar">
      <div class="stat">
        <div class="stat-number">128</div>
        <div class="stat-label">Photos</div>
      </div>
      <div class="stat">
        <div class="stat-number">4.2k</div>
        <div class="stat-label">Views</div>
      </div>
      <div class="stat">
        <div class="stat-number">342</div>
        <div class="stat-label">Likes</div>
      </div>
      <div class="stat">
        <div class="stat-number">18</div>
        <div class="stat-label">Collections</div>
      </div>
    </div>

  </div><!-- end .content -->

</body>
</html>
```

**Final Output Description:**
- A dark-themed portfolio page with a header containing a logo and a 6-icon toolbar (sprite-pattern icons with hover states)
- Category filter buttons below the header
- A responsive gallery grid: the first image spans two columns (featured), followed by six regular items
- On hover: each photo zooms slightly and a gradient overlay fades in from the bottom showing the category, title, and action buttons
- A stats bar below showing portfolio metrics
- Fully responsive: collapses from auto-fill columns to 2-column on tablet to 1-column on mobile

**Reflection Questions:**

1. How many CSS properties are used to achieve the hover overlay effect? List them all.
2. What would break if you removed `overflow: hidden` from `.gallery-item`?
3. The `.gallery-item.featured` rule uses `grid-column: span 2`. What does `span 2` mean and what does it do visually?
4. The toolbar icons use exactly the same CSS pattern as a real sprite sheet navigation bar. What single CSS change would you make to each `.toolbar-icon` to convert it from emoji to a real sprite image?
5. If you had 8 photos and wanted them in a strict 4×2 grid on all screen sizes, what change would you make to the `.gallery` rule?

**Optional Advanced Extensions:**
- Add a second row of filter buttons and make them filter the gallery with JavaScript `display: none` toggling
- Create a lightbox: clicking any image opens it full-screen in an overlay modal
- Build an actual sprite sheet in any image editor and wire up the toolbar icons to it
- Add `transition: opacity 0.5s` to `.gallery-item` so photos fade in on page load using JavaScript's `IntersectionObserver`

---

## Common Beginner Mistakes

### Mistake 1 — Not Setting `position: relative` on the Gallery Item

```css
/* WRONG — overlay ends up relative to the entire page, not the image card */
.gallery-item {
  overflow: hidden;
  /* Missing: position: relative; */
}
.overlay {
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
}
```

```css
/* CORRECT */
.gallery-item {
  position: relative;   /* ← This line is essential */
  overflow: hidden;
}
.overlay {
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
}
```

**Why:** An `absolutely` positioned element positions itself relative to its nearest ancestor that has `position` set to `relative`, `absolute`, `fixed`, or `sticky`. Without `position: relative` on `.gallery-item`, the overlay escapes and positions itself relative to some parent element much further up the tree.

---

### Mistake 2 — Forgetting `overflow: hidden` on the Zoomed Image Container

```css
/* WRONG — zoom effect breaks outside the card boundary */
.gallery-item {
  position: relative;
  /* Missing: overflow: hidden; */
  width: 250px;
  height: 170px;
}
.gallery-item:hover img {
  transform: scale(1.15);   /* Image grows but overflows the card! */
}
```

```css
/* CORRECT */
.gallery-item {
  position: relative;
  overflow: hidden;   /* ← Clips the zoomed image to stay inside the card */
  width: 250px;
  height: 170px;
}
```

**Why:** `transform: scale()` enlarges an element beyond its original boundaries. Without `overflow: hidden`, the scaled image visually overlaps neighbouring gallery cards.

---

### Mistake 3 — Using Positive Values for Sprite `background-position`

```css
/* WRONG — positive values move the background away from the window edge */
.icon-search {
  background-position: 60px 0;   /* Moves the sprite to the RIGHT — shows blank space */
}
```

```css
/* CORRECT — negative values shift the sprite so the right portion shows */
.icon-search {
  background-position: -60px 0;  /* Moves sprite 60px LEFT — search icon now visible */
}
```

**Why:** Think of sliding a long filmstrip left to bring the next frame into view. You slide *left* (negative direction). A positive value would slide the strip *right* — showing blank space or repeating the first frame.

---

### Mistake 4 — Forgetting `background-repeat: no-repeat` on Sprite Icons

```css
/* WRONG — sprite image tiles across the element, showing multiple icons */
.icon {
  width: 40px;
  height: 40px;
  background-image: url("icons-sprite.png");
  background-position: -40px 0;
  /* Missing: background-repeat: no-repeat; */
}
```

```css
/* CORRECT — sprite shows exactly once in the correct position */
.icon {
  width: 40px;
  height: 40px;
  background-image: url("icons-sprite.png");
  background-repeat: no-repeat;   /* ← Essential for sprites */
  background-position: -40px 0;
}
```

**Why:** By default, `background-image` tiles (repeats) across the entire element. For sprites, you never want tiling — you want to show only the specific section at the specified position.

---

### Mistake 5 — Distorted Gallery Images (Not Using `object-fit`)

```css
/* WRONG — images stretch and distort to fit the fixed dimensions */
.gallery-item img {
  width: 250px;
  height: 170px;
  /* Missing: object-fit: cover; */
}
```

```css
/* CORRECT — images scale and crop to fill, no distortion */
.gallery-item img {
  width: 250px;
  height: 170px;
  object-fit: cover;   /* ← Makes images fill their container without distortion */
  display: block;
}
```

**Why:** Without `object-fit: cover`, the browser stretches the image to exactly match the specified `width` and `height`, regardless of the image's natural proportions. This produces distorted, squashed, or stretched photos.

---

### Mistake 6 — Wrong Image Dimensions for the Sprite Element

```css
/* WRONG — element is bigger than one icon, showing parts of neighbouring icons */
.icon-play {
  width: 200px;    /* Way too wide — shows the entire sprite sheet! */
  height: 200px;   /* Way too tall */
  background-image: url("sprite.png");
  background-position: 0 0;
}
```

```css
/* CORRECT — element dimensions must match the individual icon's dimensions */
.icon-play {
  width: 40px;     /* Exactly the width of one icon in the sprite */
  height: 40px;    /* Exactly the height of one icon in the sprite */
  background-image: url("sprite.png");
  background-repeat: no-repeat;
  background-position: 0 0;
}
```

**Why:** The element's `width` and `height` define the viewport "window" through which you see the sprite. If the window is larger than one icon, neighbouring icons bleed into view.

---

## Reflection Questions

Think through each question before moving to the next lesson:

1. What CSS property makes an overlay `<div>` sit exactly on top of an image inside the same gallery item?
2. What is the difference between `object-fit: cover` and `object-fit: contain`? When would you use each?
3. What is the CSS Grid shorthand that creates a responsive gallery without media queries? Write it.
4. What does `aspect-ratio: 4 / 3` do to a gallery item?
5. Explain in plain English why `background-position: -90px 0` is used on a sprite icon (not `90px 0`).
6. What two CSS properties are the absolute minimum required to display a specific icon from a sprite sheet?
7. A gallery has `transition: transform 0.5s ease` on the image and `transform: scale(1.1)` on hover, but the zoomed image overlaps neighbouring cards. Which single CSS property is missing from the gallery item?
8. If a sprite sheet has icons that are 30px wide and you want to show the 4th icon in a single horizontal row, what would `background-position-x` value be?
9. What is the main performance benefit of using image sprites instead of individual image files?
10. Why is `display: block` recommended on `<img>` tags inside gallery items?

---

## Lesson Completion Checklist

Before moving to the next lesson, confirm "yes" to every item:

- [ ] I understand what a CSS image gallery is and the HTML structure it uses
- [ ] I can make gallery images uniform with `width`, `height`, and `object-fit: cover`
- [ ] I can arrange gallery items using `display: flex` or `display: grid`
- [ ] I can build a responsive gallery using `repeat(auto-fill, minmax())` or media queries
- [ ] I understand why `position: relative` on the gallery item and `position: absolute` on the overlay are both needed
- [ ] I can create a hover overlay effect using `opacity` and `transition`
- [ ] I can add a zoom-on-hover effect using `transform: scale()` and `overflow: hidden`
- [ ] I understand what an image sprite is and why it improves performance
- [ ] I understand why `background-position` values are negative for sprites
- [ ] I can calculate the `background-position` for any icon in a sprite grid
- [ ] I know that `background-repeat: no-repeat` is essential for sprites
- [ ] I completed all four guided practice exercises
- [ ] I completed the Portfolio Gallery mini-project
- [ ] I can name at least five common beginner mistakes and how to fix them

---

## Lesson Summary

### Part One — CSS Image Gallery

A CSS image gallery transforms a raw collection of images into a structured, visually polished layout. The essential pattern is a **container + gallery item + image + optional overlay**.

Key techniques:
- `object-fit: cover` — fills the image container without distortion
- `display: flex; flex-wrap: wrap` or `display: grid` — arrange items in rows
- `repeat(auto-fill, minmax(200px, 1fr))` — responsive grid with no media queries
- `position: relative` on the parent + `position: absolute` on the overlay — the foundation of all hover overlay effects
- `opacity: 0` → `opacity: 1` with `transition` — smooth fade-in on hover
- `transform: scale(1.1)` with `overflow: hidden` — smooth zoom-in on hover, contained within the card

### Part Two — CSS Image Sprites

An image sprite is a single image file containing many individual images arranged on a grid. CSS uses `background-image`, `background-position`, and `background-repeat` to display exactly one portion of the sprite at a time.

Key concepts:
- Each HTTP request takes time — sprites reduce many requests to one
- `background-position` uses **negative values** to shift the sprite image so the correct portion appears in the element's viewport window
- The formula: `background-position: -(x offset) -(y offset)`
- Element `width` and `height` define the viewport window size — they must match one icon's dimensions exactly
- `background-repeat: no-repeat` is always required with sprites
- Hover states are achieved by shifting to a second row in the sprite (`background-position-y: -[icon height]px`)

In the next lesson, you will explore **CSS Attribute Selectors** — a powerful way to target HTML elements based on their attributes and attribute values.

---

*Sources: W3Schools CSS Image Gallery Tutorial, W3Schools CSS Image Sprites Tutorial, W3Schools CSS Challenges (Image Gallery and Sprites), MDN Web Docs background-position, CSS-Tricks CSS Sprites, Tutorial Republic CSS Sprites Guide, Edureka CSS Image Sprites, DEV Community CSS Sprites 2025, freeCodeCamp Image Gallery Guide*
