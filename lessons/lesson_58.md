---
render_with_liquid: false
title: "CSS Image Styling — Shapes, Effects, Filters, Hover, Modals & Centering"
nav_order: 58
---

# Lesson 58: CSS Image Styling — Shapes, Effects, Filters, Hover Overlays, Modals & Centering

---

## Lesson Introduction

Welcome to one of the most visual and exciting topics in all of CSS! In this lesson, you will learn how to take a plain, boring image on a webpage and completely transform it using CSS alone — no image editing software required.

By the time you finish this lesson, you will know how to:
- Style images with rounded corners, borders, shadows, and transparency
- Create image effects like grayscale, blur, and sepia using CSS filters
- Build hover overlays that reveal text or colour when the user's mouse moves over an image
- Make images pop up in a modal (a lightbox-style enlargement)
- Centre images perfectly on any page
- Clip and reshape images into circles, hexagons, and triangles
- Apply real-world techniques used in professional portfolios, news sites, and online shops

> **Who is this lesson for?**
> This lesson assumes you know what an HTML `<img>` tag is and that you have written at least a few lines of CSS before (like changing a colour or a font size). If you have done those things, you are perfectly ready.

---

## Prerequisite Concepts

Before diving in, let us quickly recap two things you will use constantly in this lesson.

### What is an `<img>` tag?

The `<img>` tag is used in HTML to display an image on a webpage.

```html
<img src="photo.jpg" alt="A mountain at sunset">
```

- `src` — the path to the image file (where it lives)
- `alt` — a text description (shown when the image cannot load, and read by screen readers)

### What is a CSS property?

A CSS property is an instruction you give to a browser about how an element should look.

```css
img {
  width: 300px;      /* Makes the image 300 pixels wide */
  border: 2px solid black;  /* Adds a solid black border */
}
```

The pattern is always: `property: value;`

---

## Part 1 — CSS Image Styling Fundamentals

### 1.1 Why Style Images with CSS?

Think of a photograph printed on plain white paper versus the same photo in a professional picture frame with a mat border. The content is identical, but the styled version looks far more polished and intentional.

CSS lets you:
- Add **borders** and **padding** to frame images
- Make images **responsive** so they shrink on small screens
- Add **rounded corners** for a modern card feel
- Create **transparency** effects
- Add **hover effects** so images react to mouse movement
- Apply **filter effects** like making an image black-and-white

### 1.2 Making an Image Responsive

**The Problem:** If you place an image on a webpage and the screen is smaller than the image, the image overflows and breaks the layout.

**The Solution:** Tell the image it should never be wider than its container.

```css
img {
  max-width: 100%;
  height: auto;
}
```

**Line-by-line explanation:**

| Line | What it does |
|------|--------------|
| `max-width: 100%;` | The image may be as wide as its container but never wider. On a 400px container, the image shrinks to 400px. On a 1200px screen, it shows at its natural size. |
| `height: auto;` | The height adjusts automatically so the image does not get squashed or stretched. |

**Expected result:** The image scales down gracefully on phones and tablets but never becomes wider than the page.

> **Real-world use:** Every professional website uses `max-width: 100%` on images for mobile responsiveness. This is possibly the single most important image CSS rule you will ever write.

---

### 1.3 Adding a Border to an Image

Just like any other HTML element, you can add a border to an image.

```css
img {
  border: 3px solid grey;
}
```

**Expected result:** A grey 3-pixel-wide solid border appears around the image.

**Variations:**

```css
/* Dashed border */
img { border: 2px dashed navy; }

/* Thick red border */
img { border: 8px solid red; }

/* Dotted border */
img { border: 4px dotted green; }
```

---

### 1.4 Rounded Corners on Images

The `border-radius` property cuts the corners of an element. When applied to an image, it rounds those corners.

**Simple example — slightly rounded corners:**

```css
img {
  border-radius: 8px;
}
```

**Expected result:** The four corners of the image are gently rounded.

**More rounded:**

```css
img {
  border-radius: 20px;
}
```

**Fully circular image:**

For this to produce a perfect circle, the image must be **square** (equal width and height).

```css
img {
  border-radius: 50%;
  width: 150px;
  height: 150px;
  object-fit: cover;  /* Ensures the image fills the circle without distorting */
}
```

**Expected result:** The image appears as a perfect circle — ideal for profile pictures and avatars.

> **Why does `50%` create a circle?** Because `border-radius: 50%` rounds each corner by half the element's width and height. On a square element, this results in a perfect circle.

> **What happens if you change `50%` to `25%`?** Try it! You will get a rounded square shape.

---

### 1.5 The Thumbnail Image

A thumbnail is a small preview image, often used in galleries and product listings. Typically it has a border and a small amount of padding.

```css
img.thumbnail {
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 5px;
  width: 150px;
}
```

```html
<img class="thumbnail" src="product.jpg" alt="Red sneaker">
```

**Expected result:** A small image with a light grey border, subtle rounded corners, and 5px of breathing room between the image edge and the border.

**Adding a hover effect to the thumbnail:**

```css
img.thumbnail:hover {
  box-shadow: 0 0 2px 1px rgba(0, 140, 186, 0.5);
}
```

**Line-by-line explanation of `box-shadow`:**

| Value | Meaning |
|-------|---------|
| `0` | Horizontal shadow offset (no sideways shift) |
| `0` | Vertical shadow offset (no up/down shift) |
| `2px` | How blurry the shadow is |
| `1px` | How far the shadow spreads outward |
| `rgba(0, 140, 186, 0.5)` | A semi-transparent blue colour |

**Expected result:** When you hover over the thumbnail, a soft blue glow appears around it.

---

### 1.6 The Polaroid Card Effect

A Polaroid is a vintage-style photo card — a photo with a white border and a caption underneath.

```css
div.polaroid {
  width: 250px;
  background-color: white;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  margin-bottom: 25px;
  text-align: center;
}

div.polaroid img {
  width: 100%;
}

div.container {
  padding: 10px 5px;
}
```

```html
<div class="polaroid">
  <img src="nature.jpg" alt="Forest path">
  <div class="container">
    <p>A Walk in the Woods</p>
  </div>
</div>
```

**Expected result:** A white card with a photo on top and a caption below, with a soft drop shadow giving it depth. It looks like a real Polaroid photograph sitting on a table.

---

### 1.7 Image Transparency with `opacity`

The `opacity` property controls how see-through an element is.

- `opacity: 1` — completely visible (default)
- `opacity: 0` — completely invisible
- `opacity: 0.5` — 50% see-through

```css
img {
  opacity: 0.5;
}
```

**Expected result:** The image appears faded, letting whatever is behind it show through.

**Combining opacity with hover:**

```css
img {
  opacity: 1;
  transition: opacity 0.3s ease;
}

img:hover {
  opacity: 0.5;
}
```

**What this does:** On hover, the image smoothly fades to 50% opacity over 0.3 seconds. The `transition` property creates the smooth animation.

**The reverse — faded by default, solid on hover:**

```css
img {
  opacity: 0.5;
  transition: opacity 0.3s;
}

img:hover {
  opacity: 1;
}
```

**Use case:** This is used on image galleries where dimmed images "come alive" when hovered.

---

## Part 2 — Image Effects

### 2.1 Image Text Overlay Basics

Sometimes you want to place text directly on top of an image — like a headline over a hero image, or a price tag over a product photo.

To do this, you need a **container with `position: relative`** and the text element inside it with **`position: absolute`**.

**Why?** Because `position: absolute` positions an element *relative to its nearest positioned ancestor*. By giving the parent `position: relative`, you make it that anchor point.

**Basic image with text overlay:**

```css
.image-container {
  position: relative;   /* This becomes the anchor */
  width: 300px;
}

.image-container img {
  width: 100%;
  display: block;
}

.overlay-text {
  position: absolute;   /* Positioned inside the container */
  top: 50%;             /* 50% down from the top */
  left: 50%;            /* 50% from the left */
  transform: translate(-50%, -50%);  /* Centres the text perfectly */
  color: white;
  font-size: 24px;
  font-weight: bold;
}
```

```html
<div class="image-container">
  <img src="mountain.jpg" alt="Mountain">
  <div class="overlay-text">Hello World</div>
</div>
```

**Expected result:** The text "Hello World" appears centred on top of the image.

> **Why `transform: translate(-50%, -50%)`?** When you set `top: 50%` and `left: 50%`, you position the *top-left corner* of the text element at the centre. The transform shifts the element back by half its own width and half its own height, so the *centre* of the text lands exactly at the centre of the image.

---

### 2.2 Text Position Variations

You can position text in any corner or edge of the image:

```css
/* Top left */
.top-left {
  position: absolute;
  top: 8px;
  left: 16px;
  color: white;
}

/* Top right */
.top-right {
  position: absolute;
  top: 8px;
  right: 16px;
  color: white;
}

/* Bottom left */
.bottom-left {
  position: absolute;
  bottom: 8px;
  left: 16px;
  color: white;
}

/* Bottom right */
.bottom-right {
  position: absolute;
  bottom: 8px;
  right: 16px;
  color: white;
}
```

**Real-world use:** News websites use bottom-left text overlays for photo captions. Online shops use top-right overlays for "Sale!" badges.

---

### 2.3 Flipping an Image

CSS transforms allow you to flip (mirror) an image horizontally or vertically.

**Horizontal flip (mirror):**

```css
img {
  transform: scaleX(-1);
}
```

**Vertical flip (upside down):**

```css
img {
  transform: scaleY(-1);
}
```

**Both (rotate 180°):**

```css
img {
  transform: scale(-1, -1);
}
```

**Expected result:** The image appears mirrored or flipped.

---

### 2.4 The Shake Animation

You can make an image shake using CSS `@keyframes` animation.

```css
img:hover {
  animation: shake 0.5s;
}

@keyframes shake {
  0%   { transform: translate(1px, 1px)   rotate(0deg);  }
  10%  { transform: translate(-1px, -2px) rotate(-1deg); }
  20%  { transform: translate(-3px, 0px)  rotate(1deg);  }
  30%  { transform: translate(3px, 2px)   rotate(0deg);  }
  40%  { transform: translate(1px, -1px)  rotate(1deg);  }
  50%  { transform: translate(-1px, 2px)  rotate(-1deg); }
  60%  { transform: translate(-3px, 1px)  rotate(0deg);  }
  70%  { transform: translate(3px, 1px)   rotate(-1deg); }
  80%  { transform: translate(-1px, -1px) rotate(1deg);  }
  90%  { transform: translate(1px, 2px)   rotate(0deg);  }
  100% { transform: translate(1px, -2px)  rotate(-1deg); }
}
```

**How this works:**
- `@keyframes shake` defines a sequence of positions (frames) the image moves through
- Each percentage (0%, 10%, etc.) is a point in time during the animation
- `transform: translate(x, y)` moves the image by small pixel amounts left/right and up/down
- `rotate()` tilts the image slightly at each step
- The result looks like rapid, realistic shaking

**Expected result:** When hovered, the image shakes like it is vibrating.

---

## Part 3 — Image Hover Overlay Effects

### 3.1 What is a Hover Overlay?

A hover overlay is a layer (usually a coloured or semi-transparent panel with text) that appears *on top of* an image when the user hovers their mouse over it.

**Real-world examples:**
- A product gallery where hovering shows "Quick View" text
- A team member photo where hovering shows their job title
- A portfolio image where hovering shows the project name

The **technique** always involves:
1. A container `<div>` with `position: relative`
2. The `<img>` inside it
3. An overlay `<div>` inside the container, set to `position: absolute` and covering the full image
4. CSS that controls the overlay's visibility (using `opacity` or `height`)

---

### 3.2 Fade-In Overlay

This overlay is invisible by default and fades in on hover.

```css
.container {
  position: relative;
  width: 300px;
}

.image {
  display: block;
  width: 100%;
}

.overlay {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100%;
  width: 100%;
  opacity: 0;                          /* Hidden by default */
  transition: opacity 0.5s ease;      /* Smooth 0.5s fade */
  background-color: rgba(0, 0, 0, 0.7); /* Semi-transparent black */
}

.container:hover .overlay {
  opacity: 1;                          /* Fully visible on hover */
}

.text {
  color: white;
  font-size: 20px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

```html
<div class="container">
  <img class="image" src="forest.jpg" alt="Forest">
  <div class="overlay">
    <div class="text">Hello World</div>
  </div>
</div>
```

**Expected result:** The image is visible normally. When hovered, a dark transparent layer smoothly fades in over the image, revealing white text in the centre.

> **Think about it:** What would happen if you changed `rgba(0, 0, 0, 0.7)` to `rgba(255, 0, 0, 0.5)`? You would get a red tint instead of a dark one!

---

### 3.3 Slide-In Overlay (from the bottom)

Instead of fading in, this overlay slides up from the bottom of the image.

```css
.overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(29, 161, 242, 0.9);  /* Blue */
  overflow: hidden;
  width: 100%;
  height: 0;                         /* Starts at zero height */
  transition: height 0.5s ease;     /* Animates height on hover */
}

.container:hover .overlay {
  height: 100%;                      /* Expands to full height on hover */
}
```

**Expected result:** On hover, a blue overlay smoothly slides up from the bottom of the image, like a curtain rising.

---

### 3.4 Slide-In Overlay (from the top)

```css
.overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  background-color: rgba(29, 161, 242, 0.9);
  overflow: hidden;
  width: 100%;
  height: 0;
  transition: height 0.5s ease;
}

.container:hover .overlay {
  height: 100%;
}
```

**Expected result:** The overlay slides down from the top of the image.

---

### 3.5 Slide-In Overlay (from the left)

```css
.overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  background-color: rgba(29, 161, 242, 0.9);
  overflow: hidden;
  width: 0;                          /* Starts at zero width */
  height: 100%;
  transition: width 0.5s ease;      /* Animates width on hover */
}

.container:hover .overlay {
  width: 100%;                       /* Expands to full width on hover */
}
```

**Expected result:** The overlay slides in from the left side.

---

### 3.6 Slide-In Overlay (from the right)

```css
.overlay {
  position: absolute;
  bottom: 0;
  right: 0;                          /* Anchored to the right */
  background-color: rgba(29, 161, 242, 0.9);
  overflow: hidden;
  width: 0;
  height: 100%;
  transition: width 0.5s ease;
}

.container:hover .overlay {
  width: 100%;
}
```

**Expected result:** The overlay slides in from the right side.

---

### 3.7 Image Zoom on Hover

Another popular effect is zooming in on hover. This uses `overflow: hidden` on the container and `transform: scale()` on the image.

```css
.zoom-container {
  overflow: hidden;    /* Clips the image so it doesn't overflow when scaled */
  width: 300px;
  height: 200px;
}

.zoom-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.zoom-container:hover img {
  transform: scale(1.2);  /* Zooms to 120% of original size */
}
```

**Expected result:** When hovered, the image gently zooms in while staying neatly clipped inside its container.

---

## Part 4 — Image Modal (Lightbox)

### 4.1 What is a Modal?

A **modal** is a pop-up panel that appears on top of the rest of the page, dimming everything behind it. You have seen these before — clicking on a thumbnail in Google Images shows the full-size photo in a modal.

For images, this is also called a **lightbox** effect.

**How it works (overview):**
1. User clicks a small image (thumbnail)
2. JavaScript copies the image's `src` into a larger `<img>` tag inside a hidden modal `<div>`
3. CSS makes the modal visible (changes `display` from `none` to `block`)
4. User clicks the close button (×) or clicks outside the image to close it

---

### 4.2 The Complete Image Modal Example

**HTML structure:**

```html
<!-- The thumbnail the user clicks -->
<img id="myImage" src="photo.jpg" alt="My Photo" style="width:100%;max-width:300px;cursor:pointer">

<!-- The Modal -->
<div id="myModal" class="modal">
  <!-- Close button -->
  <span class="close">&times;</span>
  <!-- The large image inside the modal -->
  <img class="modal-content" id="imgInModal">
  <!-- Caption -->
  <div id="caption"></div>
</div>
```

**CSS for the modal:**

```css
/* The dark background overlay */
.modal {
  display: none;              /* Hidden by default */
  position: fixed;            /* Covers the full viewport */
  z-index: 1000;              /* On top of everything */
  padding-top: 100px;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0, 0, 0, 0.9);  /* Very dark background */
}

/* The large image inside the modal */
.modal-content {
  margin: auto;
  display: block;
  width: 80%;
  max-width: 700px;
}

/* Caption text */
#caption {
  margin: auto;
  display: block;
  width: 80%;
  max-width: 700px;
  text-align: center;
  color: #ccc;
  padding: 10px 0;
  height: 150px;
}

/* Smooth appearance animation */
.modal-content,
#caption {
  animation-name: zoom;
  animation-duration: 0.6s;
}

@keyframes zoom {
  from { transform: scale(0); }
  to   { transform: scale(1); }
}

/* Close button */
.close {
  position: absolute;
  top: 15px;
  right: 35px;
  color: #f1f1f1;
  font-size: 40px;
  font-weight: bold;
  cursor: pointer;
}

.close:hover,
.close:focus {
  color: #bbb;
}
```

**JavaScript to open and close the modal:**

```javascript
// Get elements
var modal = document.getElementById("myModal");
var img = document.getElementById("myImage");
var modalImg = document.getElementById("imgInModal");
var captionText = document.getElementById("caption");

// When the small image is clicked, open the modal
img.onclick = function() {
  modal.style.display = "block";        // Show the modal
  modalImg.src = this.src;              // Copy the src to the large image
  captionText.innerHTML = this.alt;     // Use alt text as caption
}

// When the close button (×) is clicked, close the modal
var span = document.getElementsByClassName("close")[0];
span.onclick = function() {
  modal.style.display = "none";
}

// When the user clicks outside the modal image, close it
modal.onclick = function(event) {
  if (event.target == modal) {
    modal.style.display = "none";
  }
}
```

**Line-by-line explanation of the JavaScript:**

| Line | What it does |
|------|--------------|
| `document.getElementById("myModal")` | Finds the modal div in the HTML |
| `modal.style.display = "block"` | Makes the modal visible |
| `modalImg.src = this.src` | Sets the big image source to the clicked thumbnail's source |
| `captionText.innerHTML = this.alt` | Shows the image's alt text as the caption |
| `modal.style.display = "none"` | Hides the modal when × is clicked |
| `if (event.target == modal)` | Checks if the user clicked the dark background (not the image itself) |

**Expected result:** Clicking the small photo opens a full-screen dark overlay with the larger version of the photo zooming in smoothly. Clicking × or the dark background closes it.

---

## Part 5 — Centring Images

### 5.1 Why Centring an Image is Not Obvious

You might think `text-align: center` would centre an image. And sometimes it does — but only if the image is inside a `block` element and is itself `inline`. Let us learn the proper and reliable methods.

---

### 5.2 Method 1: Auto Margins (Most Common)

The most widely used method uses `display: block` and `margin: auto`.

```css
img {
  display: block;   /* Makes the image a block element */
  margin: auto;     /* Equal space on left and right */
}
```

**Why `display: block`?** By default, images are `inline` elements. `margin: auto` only works horizontally on **block-level** elements. Changing to `block` makes the auto-margin work.

**Expected result:** The image is horizontally centred inside its container.

**Full example with a width set:**

```css
img {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
```

**Expected result:** A responsive image that is always 50% of its container's width and perfectly centred.

---

### 5.3 Method 2: Centering with Flexbox

Flexbox gives you powerful centering control with very little code.

```css
.center-container {
  display: flex;
  justify-content: center;  /* Centres horizontally */
  align-items: center;      /* Centres vertically */
}
```

```html
<div class="center-container">
  <img src="photo.jpg" alt="Centred photo">
</div>
```

**Expected result:** The image is perfectly centred both horizontally and vertically inside the container.

---

### 5.4 Method 3: Centering with text-align (for inline images)

If the image is inside a `<p>`, `<div>`, or similar container, you can centre it using `text-align: center` on the *parent*:

```css
.parent {
  text-align: center;
}
```

```html
<div class="parent">
  <img src="photo.jpg" alt="Photo">
</div>
```

**Expected result:** The image appears centred. This works because the image behaves like an inline element (like a letter of text).

---

### 5.5 Centering an Image Vertically and Horizontally on the Full Page

```css
body {
  margin: 0;
}

.full-page-center {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;         /* Full viewport height */
}
```

```html
<div class="full-page-center">
  <img src="logo.png" alt="Logo" style="width: 300px;">
</div>
```

**Expected result:** The image is perfectly centred both horizontally and vertically on the entire browser window.

---

## Part 6 — CSS Image Filters

### 6.1 What Are CSS Filters?

CSS filters are visual effects you can apply directly to an image (or any element) using pure CSS. They work the same way Photoshop filters do — but you do not need any image editing software!

The CSS property is simply called `filter`.

**Syntax:**

```css
img {
  filter: <function>(<value>);
}
```

You can also **chain multiple filters** in one rule:

```css
img {
  filter: grayscale(50%) blur(2px);
}
```

---

### 6.2 All CSS Filter Functions Explained

#### `grayscale(%)` — Remove colour

Converts the image towards black and white.

- `0%` = original colour (no effect)
- `100%` = completely black and white

```css
img { filter: grayscale(100%); }
```

**Expected result:** A fully black-and-white image.

```css
img { filter: grayscale(50%); }
```

**Expected result:** A washed-out, desaturated version (halfway between colour and black-and-white).

> **Real-world use:** News websites use greyscale on photos of deceased people. Design agencies use it for a "before" effect in portfolio before/after sliders.

---

#### `sepia(%)` — Vintage brown tone

Sepia gives images a warm, vintage, old-photograph look.

- `0%` = original colour
- `100%` = full sepia (brown-orange tones)

```css
img { filter: sepia(100%); }
```

**Expected result:** The image looks like an old faded photograph from the 1800s.

---

#### `blur(px)` — Soften the image

Applies a Gaussian blur to the image.

- `0px` = sharp (no blur)
- Higher values = more blurry

```css
img { filter: blur(4px); }
```

**Expected result:** The image appears soft and out-of-focus.

> **Real-world use:** Blurred images are used as background images (so text on top is readable), for loading placeholders, and for creating depth-of-field effects.

---

#### `brightness(%)` — Make lighter or darker

- `100%` = original brightness
- `< 100%` = darker
- `> 100%` = lighter/washed out

```css
img { filter: brightness(150%); }   /* Brighter */
img { filter: brightness(50%);  }   /* Darker */
```

---

#### `contrast(%)` — Increase or decrease contrast

Contrast is the difference between the lightest and darkest parts of an image.

- `100%` = normal
- `> 100%` = more vivid/dramatic
- `< 100%` = flat and grey-looking

```css
img { filter: contrast(200%); }   /* Very high contrast */
img { filter: contrast(50%);  }   /* Low contrast, faded look */
```

---

#### `saturate(%)` — Boost or reduce colour intensity

- `100%` = normal
- `> 100%` = very vivid, over-saturated colours
- `0%` = removes all colour (same effect as grayscale)

```css
img { filter: saturate(300%); }   /* Very vivid, punchy colours */
img { filter: saturate(0%);   }   /* Black and white */
```

---

#### `hue-rotate(deg)` — Rotate the colour wheel

This shifts all the colours in the image around the colour wheel.

- `0deg` = original colours
- `90deg` = shift all colours 90 degrees
- `180deg` = complementary colours (reds become cyan, blues become orange)

```css
img { filter: hue-rotate(90deg); }
```

**Expected result:** The image's colours are all shifted — grass that was green might appear blue or purple.

---

#### `invert(%)` — Invert all colours (like a photo negative)

- `0%` = original
- `100%` = fully inverted (dark becomes light, colours become their opposites)

```css
img { filter: invert(100%); }
```

**Expected result:** The image looks like a photo negative — whites become black, blacks become white, and every colour becomes its complement.

---

#### `opacity(%)` — Set transparency via filter

This works the same as the `opacity` property but as a filter function.

```css
img { filter: opacity(50%); }
```

**Note:** For simple transparency, using the `opacity` property directly is more common. The filter version can be useful when chaining filters.

---

#### `drop-shadow()` — Add a shadow

This is similar to `box-shadow` but follows the actual shape of the image (including transparency), not just the rectangular bounding box.

```css
img {
  filter: drop-shadow(5px 5px 10px black);
}
```

**Parameters:** `drop-shadow(x-offset y-offset blur-radius colour)`

| Parameter | Meaning |
|-----------|---------|
| `5px` | Move shadow 5px to the right |
| `5px` | Move shadow 5px downward |
| `10px` | Blur radius (how soft the shadow is) |
| `black` | Shadow colour |

**Expected result:** A soft black shadow appears beneath and to the right of the image, following its shape.

> **Tip:** This is especially powerful for PNG images with transparent backgrounds — `box-shadow` would add a shadow to the rectangle, but `drop-shadow` follows the actual visible shape.

---

### 6.3 Chaining Multiple Filters

You can apply several filters at once by listing them space-separated:

```css
img {
  filter: grayscale(50%) blur(2px) brightness(80%);
}
```

**Expected result:** The image is half-desaturated, slightly blurred, and 20% darker.

---

### 6.4 Filter on Hover (Smooth Transition)

Filters work beautifully with CSS transitions for smooth hover effects:

```css
img {
  filter: grayscale(100%);           /* Start in black and white */
  transition: filter 0.5s ease;
}

img:hover {
  filter: grayscale(0%);             /* Become colourful on hover */
}
```

**Expected result:** Images are black-and-white by default. Hovering transforms them into colour over 0.5 seconds. This technique is used frequently in modern photography portfolios.

---

## Part 7 — CSS Image Shapes

### 7.1 Why Shape Images with CSS?

By default, images are rectangular. But CSS gives you powerful tools to cut images into different shapes — circles, ovals, triangles, and custom polygon shapes.

---

### 7.2 Circular Image

As you learned earlier, `border-radius: 50%` on a square image creates a circle.

```css
img {
  border-radius: 50%;
  width: 200px;
  height: 200px;
  object-fit: cover;   /* Fills the circle without stretching */
}
```

**Expected result:** A circular image — great for profile pictures and avatars.

> **What is `object-fit: cover`?** If the original image is not square, `object-fit: cover` scales it so it completely fills the circle, cropping the edges. Without it, the image might be squeezed or show gaps.

---

### 7.3 Oval / Ellipse Shape

For an oval, use different values for horizontal and vertical `border-radius`:

```css
img {
  border-radius: 50% / 20%;  /* 50% horizontal, 20% vertical */
  width: 300px;
  height: 150px;
}
```

Or use the 4-value shorthand for full control:

```css
img {
  border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
}
```

---

### 7.4 Using `clip-path` for Advanced Shapes

The `clip-path` property is a powerful way to cut an element into virtually any shape by defining a "clipping region". Only the parts of the image *inside* the clip region are shown; everything outside is hidden.

#### Circle with `clip-path`

```css
img {
  clip-path: circle(50%);
}
```

**Expected result:** Same as `border-radius: 50%` but using the clip-path approach.

You can also control the position:

```css
img {
  clip-path: circle(50% at 50% 50%);   /* Circle centred in the middle */
}
```

---

#### Ellipse with `clip-path`

```css
img {
  clip-path: ellipse(60% 40% at 50% 50%);
}
```

**Parameters:** `ellipse(x-radius y-radius at x-position y-position)`

**Expected result:** An oval-shaped image.

---

#### Triangle with `clip-path`

```css
img {
  clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
}
```

**How to read `polygon()`:** Each pair of values (like `50% 0%`) is one point of the polygon. Three points = triangle.

| Point | Meaning |
|-------|---------|
| `50% 0%` | Top centre |
| `0% 100%` | Bottom left |
| `100% 100%` | Bottom right |

**Expected result:** The image is clipped into a triangle pointing upward.

---

#### Pentagon with `clip-path`

```css
img {
  clip-path: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%);
}
```

**Expected result:** A five-sided shape.

---

#### Rhombus (Diamond) with `clip-path`

```css
img {
  clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
}
```

**Expected result:** A diamond/rhombus-shaped image.

---

#### Star with `clip-path`

A five-pointed star uses 10 polygon points:

```css
img {
  clip-path: polygon(
    50% 0%, 61% 35%, 98% 35%, 68% 57%,
    79% 91%, 50% 70%, 21% 91%, 32% 57%,
    2% 35%, 39% 35%
  );
}
```

**Expected result:** A star-shaped image — unique and eye-catching for decorative purposes.

---

### 7.5 Using `shape-outside` for Text Wrapping Around Shapes

`shape-outside` controls how text wraps around a *floated* image. This is different from `clip-path` — it does not change the visible shape of the image, but tells the surrounding text to follow the shape.

```css
img {
  float: left;
  shape-outside: circle(50%);
  clip-path: circle(50%);   /* Visually makes the image circular */
  width: 200px;
  height: 200px;
}
```

**Expected result:** The image appears circular AND the text beside it wraps in a curve around the circle, rather than wrapping around the rectangular bounding box.

**Other shape values:**

```css
img { shape-outside: ellipse(150px 100px at 50% 50%); }
img { shape-outside: polygon(50% 0%, 100% 100%, 0% 100%); }
img { shape-outside: url(image.png); }  /* Uses the image's transparency as the shape */
```

---

## Part 8 — Guided Practice Exercises

### Exercise 1: The Profile Card

**Objective:** Build a professional-looking profile card with a circular photo, name, and role.

**Scenario:** You are building a team page for a small company website.

**Steps:**

1. Create an HTML file with the following structure:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Profile Card</title>
  <style>
    /* Your CSS goes here */
  </style>
</head>
<body>
  <div class="card">
    <img src="https://via.placeholder.com/150" alt="Jane Doe">
    <h2>Jane Doe</h2>
    <p>Lead Developer</p>
  </div>
</body>
</html>
```

2. Add CSS to:
   - Make the card `300px` wide with a `box-shadow`
   - Make the image circular (`border-radius: 50%`)
   - Centre everything with `text-align: center`
   - Add `padding: 20px`

**Expected output:** A neat card with a round photo, centred name, and role.

**Hint:**

```css
.card {
  width: 300px;
  text-align: center;
  padding: 20px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
  border-radius: 10px;
}

.card img {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  object-fit: cover;
}
```

**Self-check questions:**
- Does the image appear circular?
- Is the card shadow visible?
- What happens if you remove `object-fit: cover`?

---

### Exercise 2: Hover Gallery with Overlay

**Objective:** Create a 3-image row where hovering each image reveals a dark overlay with a caption.

**Steps:**

1. Create three image containers with overlays
2. Use `opacity: 0` by default and `opacity: 1` on hover
3. Include a `transition: 0.4s ease` for smoothness

**Starter code:**

```html
<div class="gallery">
  <div class="img-container">
    <img src="https://via.placeholder.com/300x200" alt="Sunset">
    <div class="overlay"><div class="caption">Sunset</div></div>
  </div>
  <div class="img-container">
    <img src="https://via.placeholder.com/300x200" alt="Ocean">
    <div class="overlay"><div class="caption">Ocean</div></div>
  </div>
  <div class="img-container">
    <img src="https://via.placeholder.com/300x200" alt="Mountains">
    <div class="overlay"><div class="caption">Mountains</div></div>
  </div>
</div>
```

**CSS to complete:**

```css
.gallery {
  display: flex;
  gap: 10px;
}

.img-container {
  position: relative;
  width: 300px;
}

.img-container img {
  width: 100%;
  display: block;
}

.overlay {
  position: absolute;
  top: 0; left: 0; right: 0; bottom: 0;
  background-color: rgba(0, 0, 0, 0.65);
  opacity: 0;
  transition: opacity 0.4s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.img-container:hover .overlay {
  opacity: 1;
}

.caption {
  color: white;
  font-size: 22px;
  font-weight: bold;
}
```

**Expected result:** Three images in a row. Each shows a dark overlay with its caption text on hover.

---

### Exercise 3: Filter Showcase

**Objective:** Apply 5 different filters to 5 copies of the same image.

**Challenge:** Create a row of 5 images with labels, each using a different filter:
1. Original (no filter)
2. `grayscale(100%)`
3. `sepia(100%)`
4. `blur(3px)`
5. `brightness(150%)`

**Starter CSS:**

```css
.filters {
  display: flex;
  gap: 15px;
  flex-wrap: wrap;
}

.filter-item {
  text-align: center;
}

.filter-item img {
  width: 150px;
  height: 100px;
  object-fit: cover;
}

.filter-item p {
  font-size: 12px;
  margin: 5px 0 0;
}

.grayscale  { filter: grayscale(100%); }
.sepia      { filter: sepia(100%); }
.blurred    { filter: blur(3px); }
.bright     { filter: brightness(150%); }
```

---

### Exercise 4: Image Shapes Gallery

**Objective:** Display the same image in five different shapes.

**CSS to write:**

```css
.circle   { clip-path: circle(50%); }
.ellipse  { clip-path: ellipse(55% 40%); }
.triangle { clip-path: polygon(50% 0%, 0% 100%, 100% 100%); }
.diamond  { clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
.star     { clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%); }
```

Apply these classes to the same image repeated five times. Add `width: 200px; height: 200px; object-fit: cover;` to all of them.

---

## Part 9 — Mini-Project: Image Showcase Page

### Project Overview

You will build a complete, polished **"Photo Gallery Showcase"** webpage that demonstrates all the techniques from this lesson.

### Stage 1: Setup

Create `gallery.html` with a basic page layout:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Photo Gallery Showcase</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      padding: 30px;
    }
    h1 {
      text-align: center;
      margin-bottom: 30px;
      color: #333;
    }
    section {
      margin-bottom: 50px;
    }
    h2 {
      margin-bottom: 15px;
      color: #555;
      border-bottom: 2px solid #ccc;
      padding-bottom: 5px;
    }
  </style>
</head>
<body>
  <h1>CSS Image Showcase</h1>
  <!-- Sections go here -->
</body>
</html>
```

---

### Stage 2: Section 1 — Styled Images

Add a section showing rounded images, thumbnails, and a polaroid:

```html
<section>
  <h2>1. Image Styling</h2>
  <div style="display:flex; gap:20px; flex-wrap:wrap; align-items:center;">

    <!-- Circular -->
    <div style="text-align:center;">
      <img src="https://picsum.photos/150" alt="Circle"
           style="border-radius:50%; width:150px; height:150px; object-fit:cover; border:3px solid #777;">
      <p>Circular</p>
    </div>

    <!-- Thumbnail -->
    <div style="text-align:center;">
      <img src="https://picsum.photos/200/150" alt="Thumbnail"
           style="border:1px solid #ddd; border-radius:4px; padding:5px; width:150px;">
      <p>Thumbnail</p>
    </div>

    <!-- Polaroid -->
    <div style="background:white; width:180px; box-shadow:0 4px 8px rgba(0,0,0,0.2); text-align:center; padding-bottom:10px;">
      <img src="https://picsum.photos/180/120" alt="Polaroid" style="width:100%; display:block;">
      <p style="padding:5px; font-size:13px; color:#555;">Polaroid Style</p>
    </div>

  </div>
</section>
```

---

### Stage 3: Section 2 — Hover Overlays

```html
<section>
  <h2>2. Hover Overlays</h2>
  <div style="display:flex; gap:15px; flex-wrap:wrap;">

    <div class="hover-box">
      <img src="https://picsum.photos/250/180?random=1" alt="Nature">
      <div class="hover-overlay fade-overlay">
        <span class="hover-text">Fade In</span>
      </div>
    </div>

    <div class="hover-box">
      <img src="https://picsum.photos/250/180?random=2" alt="City">
      <div class="hover-overlay slide-overlay">
        <span class="hover-text">Slide Up</span>
      </div>
    </div>

  </div>
</section>
```

```css
.hover-box {
  position: relative;
  width: 250px;
  overflow: hidden;
}
.hover-box img {
  width: 100%;
  display: block;
}
.hover-overlay {
  position: absolute;
  top: 0; left: 0; right: 0; bottom: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0,0,0,0.65);
}
.hover-text {
  color: white;
  font-size: 18px;
  font-weight: bold;
}

/* Fade overlay */
.fade-overlay {
  opacity: 0;
  transition: opacity 0.4s ease;
}
.hover-box:hover .fade-overlay {
  opacity: 1;
}

/* Slide overlay */
.slide-overlay {
  height: 0;
  overflow: hidden;
  transition: height 0.4s ease;
}
.hover-box:hover .slide-overlay {
  height: 100%;
}
```

---

### Stage 4: Section 3 — Filters

```html
<section>
  <h2>3. CSS Filters</h2>
  <div style="display:flex; gap:15px; flex-wrap:wrap;">
    <div class="filter-card">
      <img src="https://picsum.photos/180/120?random=10" alt="Normal">
      <p>Original</p>
    </div>
    <div class="filter-card">
      <img src="https://picsum.photos/180/120?random=10" alt="Greyscale"
           style="filter:grayscale(100%)">
      <p>Grayscale</p>
    </div>
    <div class="filter-card">
      <img src="https://picsum.photos/180/120?random=10" alt="Sepia"
           style="filter:sepia(100%)">
      <p>Sepia</p>
    </div>
    <div class="filter-card">
      <img src="https://picsum.photos/180/120?random=10" alt="Blur"
           style="filter:blur(3px)">
      <p>Blur</p>
    </div>
    <div class="filter-card">
      <img src="https://picsum.photos/180/120?random=10" alt="Invert"
           style="filter:invert(100%)">
      <p>Invert</p>
    </div>
  </div>
</section>
```

```css
.filter-card {
  text-align: center;
}
.filter-card img {
  width: 180px;
  height: 120px;
  object-fit: cover;
  display: block;
}
.filter-card p {
  font-size: 13px;
  color: #555;
  margin-top: 5px;
}
```

---

### Stage 5: Section 4 — Shapes

```html
<section>
  <h2>4. Image Shapes</h2>
  <div style="display:flex; gap:20px; flex-wrap:wrap; align-items:center;">

    <div style="text-align:center;">
      <img src="https://picsum.photos/200?random=20" alt="Circle"
           style="width:150px;height:150px;object-fit:cover;clip-path:circle(50%);">
      <p>Circle</p>
    </div>

    <div style="text-align:center;">
      <img src="https://picsum.photos/200?random=20" alt="Diamond"
           style="width:150px;height:150px;object-fit:cover;clip-path:polygon(50% 0%,100% 50%,50% 100%,0% 50%);">
      <p>Diamond</p>
    </div>

    <div style="text-align:center;">
      <img src="https://picsum.photos/200?random=20" alt="Triangle"
           style="width:150px;height:150px;object-fit:cover;clip-path:polygon(50% 0%,0% 100%,100% 100%);">
      <p>Triangle</p>
    </div>

    <div style="text-align:center;">
      <img src="https://picsum.photos/200?random=20" alt="Star"
           style="width:150px;height:150px;object-fit:cover;clip-path:polygon(50% 0%,61% 35%,98% 35%,68% 57%,79% 91%,50% 70%,21% 91%,32% 57%,2% 35%,39% 35%);">
      <p>Star</p>
    </div>

  </div>
</section>
```

---

### Stage 6: Section 5 — Modal

Add the modal HTML and JavaScript from Part 4. Pick one of your images as the trigger.

**Milestone output check:**
- ✅ Section 1 shows circular, thumbnail, and polaroid images
- ✅ Section 2 shows fade and slide hover overlays
- ✅ Section 3 shows a row of filtered images
- ✅ Section 4 shows images in different shapes
- ✅ Section 5 shows a clickable modal

---

## Part 10 — Common Beginner Mistakes

### Mistake 1: Forgetting `position: relative` on the container

**Wrong:**
```css
.container img { ... }
.overlay { position: absolute; top: 0; left: 0; } /* Positions relative to the viewport! */
```

**Correct:**
```css
.container { position: relative; }  /* Anchors the overlay */
.overlay { position: absolute; top: 0; left: 0; }
```

> Without `position: relative` on the parent, `position: absolute` on the overlay will position itself relative to the nearest *positioned* ancestor — which might be the entire viewport.

---

### Mistake 2: Using `border-radius: 50%` on a non-square image expecting a circle

**Problem:** If your image is 300px wide and 200px tall, `border-radius: 50%` gives you an **oval**, not a circle.

**Fix:** Set equal `width` and `height` and add `object-fit: cover`:

```css
img {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  object-fit: cover;
}
```

---

### Mistake 3: Forgetting `display: block` when using `margin: auto`

**Wrong:**
```css
img {
  margin: auto;   /* Does nothing on an inline element */
}
```

**Correct:**
```css
img {
  display: block;
  margin: auto;
}
```

---

### Mistake 4: Stacking filters incorrectly (spaces, not commas)

**Wrong:**
```css
img { filter: grayscale(100%), blur(2px); }  /* Comma is wrong! */
```

**Correct:**
```css
img { filter: grayscale(100%) blur(2px); }   /* Space-separated */
```

---

### Mistake 5: Using `clip-path` without `object-fit: cover`

When you clip an image with `clip-path`, the image's original proportions remain. If the image is not square and you're clipping to a circle, it might look off.

**Always pair with:**
```css
img {
  width: 200px;
  height: 200px;
  object-fit: cover;
  clip-path: circle(50%);
}
```

---

### Mistake 6: Not adding `overflow: hidden` when using height/width animation for overlays

When you animate an overlay from `height: 0` to `height: 100%`, you need `overflow: hidden` to prevent the content inside from showing before the animation completes.

**Wrong:**
```css
.overlay { height: 0; }  /* Text is still visible because it overflows! */
```

**Correct:**
```css
.overlay { height: 0; overflow: hidden; }
```

---

### Mistake 7: Not using `transition` for smooth hover effects

**Without transition:**
The effect snaps instantly — looks jarring and unprofessional.

**With transition:**
```css
img {
  filter: grayscale(100%);
  transition: filter 0.4s ease;
}
img:hover {
  filter: grayscale(0%);
}
```

The change is smooth and polished.

---

## Part 11 — Reflection Questions

1. **Why does `border-radius: 50%` only create a perfect circle on a square element?**

2. **What is the difference between `opacity: 0.5` (property) and `filter: opacity(50%)` (filter function)? In what situations might you prefer the filter version?**

3. **When would you use `clip-path: polygon()` instead of `border-radius` to shape an image?**

4. **A developer sets `position: absolute` on an overlay div but it appears in the wrong corner of the screen. What is the most likely cause, and how would you fix it?**

5. **You have a portfolio grid of 12 images. All are in colour. When the user hovers, they should turn to colour while the rest stay greyscale. What CSS approach would you use?**

6. **What does `object-fit: cover` do, and why is it important when using `clip-path` on images?**

7. **A client wants images to "zoom in" smoothly on hover without the image breaking outside its container. What two CSS properties are essential for this effect?**

8. **What is the difference between `box-shadow` and `filter: drop-shadow()`, and when would you prefer each?**

---

## Part 12 — Completion Checklist

Use this list to check your understanding before moving to the next lesson:

- [ ] I can make an image responsive using `max-width: 100%` and `height: auto`
- [ ] I can add borders, padding, and `box-shadow` to images
- [ ] I can create circular images with `border-radius: 50%` and `object-fit: cover`
- [ ] I can build a Polaroid card with a white background and drop shadow
- [ ] I can create an image hover overlay using `position: relative` / `position: absolute`
- [ ] I can make a fade-in, slide-up, slide-left, and slide-right overlay
- [ ] I can build a complete image modal (lightbox) with CSS and JavaScript
- [ ] I can centre an image using `display: block; margin: auto;`
- [ ] I can centre an image using Flexbox
- [ ] I can apply CSS filters: `grayscale`, `sepia`, `blur`, `brightness`, `contrast`, `saturate`, `hue-rotate`, `invert`, `drop-shadow`, `opacity`
- [ ] I can chain multiple CSS filters on one element
- [ ] I can make filters animate smoothly with `transition`
- [ ] I can shape images into circles, ellipses, triangles, diamonds, and stars using `clip-path`
- [ ] I can use `shape-outside` for text to wrap around shaped images
- [ ] I know the 7 most common beginner mistakes and how to fix them

---

## Lesson Summary

In this lesson, you went from knowing basic CSS to being able to style images like a professional front-end developer.

**Here is what you covered:**

**Styling Fundamentals** — You learned that `max-width: 100%` makes images responsive, `border-radius` rounds corners, `border-radius: 50%` makes circles, and `box-shadow` adds depth. The Polaroid card and thumbnail hover patterns are reusable in any real project.

**Image Effects** — Text overlays require `position: relative` on the container and `position: absolute` on the text. The `transform: translate(-50%, -50%)` trick is the reliable way to perfectly centre overlaid text. CSS animations like the shake effect use `@keyframes`.

**Hover Overlays** — Fade-in overlays use `opacity: 0` → `opacity: 1`. Slide overlays use `height: 0` → `height: 100%` (or width). Both need `transition` for smooth animation and `overflow: hidden` to prevent content leaking.

**Image Modals** — A modal is an `display: none` div that becomes `display: block` via JavaScript when a thumbnail is clicked. It uses `position: fixed`, `z-index`, and a dark background to float over the rest of the page.

**Image Centering** — The most reliable method is `display: block; margin: auto;`. Flexbox with `justify-content: center` is the most powerful and flexible approach.

**CSS Filters** — The `filter` property gives you Photoshop-like tools in CSS: `grayscale`, `sepia`, `blur`, `brightness`, `contrast`, `saturate`, `hue-rotate`, `invert`, `opacity`, and `drop-shadow`. Chain multiple filters with spaces (not commas).

**Image Shapes** — `border-radius: 50%` makes circles. `clip-path: polygon()` makes triangles, diamonds, pentagons, stars, and any custom shape. `shape-outside` makes text flow around shaped images.

---

> **Next up:** Now that you can style images beautifully, the next lesson will cover `object-fit` and `object-position` — giving you precise control over how images fill their containers.
