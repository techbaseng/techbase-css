---
render_with_liquid: false
title: "CSS object-fit and object-position"
nav_order: 59
---

# Lesson 59: CSS `object-fit` and `object-position`

---

## Lesson Introduction

Have you ever visited a website where product images look squashed or stretched — a round face turned into an oval, or a portrait photo cropped in a weird way? These are image-fitting problems, and they are extremely common in real web development.

In this lesson, you will learn two powerful CSS properties — **`object-fit`** and **`object-position`** — that give you full, professional control over how images (and videos) display inside fixed-size containers. These are the exact tools used by Nigerian e-commerce sites like Jumia, Konga, and Flutterwave's blog to display product and team photos cleanly, regardless of what shape the original image is.

### What You Will Learn

By the end of this lesson, you will be able to:

- Understand why images distort and how to fix it
- Use all five values of `object-fit` confidently
- Understand the difference between `contain` and `cover`
- Use `object-position` to control which part of an image is shown
- Combine `object-fit` and `object-position` for pixel-perfect image presentation
- Apply these properties to real-world card grids, galleries, and profile pages

---

## Prerequisite Concepts Recap

Before we start, let's confirm you are comfortable with these ideas from earlier lessons:

- **CSS `width` and `height`** — you know how to set fixed sizes on elements
- **CSS `overflow`** — you know that `overflow: hidden` hides content that goes beyond a container's bounds
- **The `<img>` element** — you know that images have their own natural dimensions from the image file itself
- **CSS `background-size`** (optional review) — `object-fit` works similarly to `background-size` but applies to `<img>` and `<video>` elements directly

---

## Section 1 — The Problem: Why Do Images Distort?

### Understanding Natural Image Dimensions

Every image file has its own natural width and height — these are called its **intrinsic dimensions**. A photo taken on an Infinix phone might be 3000px × 4000px (portrait). A landscape banner might be 1920px × 400px (very wide). These dimensions are fixed inside the file itself.

When you put an image inside a fixed-size container in HTML, the browser has to decide: *"This container is 200px × 200px square, but the image is 3000px × 4000px tall — what do I do?"*

By default, the browser stretches or squashes the image to fit the container exactly. The result? Distortion.

### Analogy — The Photograph in a Frame

Imagine you buy a square photo frame from Computer Village in Lagos, but the photo you want to put inside is tall and narrow (portrait). You have a few options:

1. **Squash the photo** to fit the square — it looks distorted
2. **Shrink the entire photo** until both sides fit inside the frame — there's empty space on the sides
3. **Zoom in and crop** the photo so it fills the frame — you lose some of the image edges
4. **Leave the photo at its natural size** — it overflows the frame

CSS `object-fit` maps directly to these real-world decisions.

### Seeing the Problem in Code

```html
<img class="product-photo" src="tall-portrait.jpg" alt="Product">
```

```css
.product-photo {
  width: 200px;
  height: 200px;
  /* No object-fit — browser stretches the tall image into a square */
}
```

**Expected output in browser:** The tall portrait image is squashed horizontally to fit the 200px × 200px square, making everything look wide and distorted.

---

## Section 2 — Introducing `object-fit`

### What Is `object-fit`?

`object-fit` is a CSS property that controls **how the content of a replaced element** (an `<img>` or `<video>`) is resized to fit its container. It does not change the container's size — it only controls how the image fills that container.

Think of it as instructions you give to the image: *"Here is the frame. This is how I want you to sit inside it."*

### Syntax

```css
img {
  width: 200px;
  height: 200px;
  object-fit: fill; /* or contain | cover | none | scale-down */
}
```

### The Five Values

| Value        | What It Does                                                                |
|--------------|-----------------------------------------------------------------------------|
| `fill`       | Stretches the image to fill the container exactly — may distort (default)   |
| `contain`    | Shrinks the image to fit entirely inside the container — no cropping, may show empty space |
| `cover`      | Zooms the image to cover the container completely — maintains ratio, may crop edges |
| `none`       | Displays the image at its natural size — may overflow or show empty space   |
| `scale-down` | Picks the smaller result of either `none` or `contain`                      |

---

## Section 3 — `object-fit: fill` (The Default)

### What Is It?

`fill` is the **default behaviour**. The image is stretched (or squashed) in both directions until it fills the container exactly. It **ignores** the image's natural proportions, which is why it causes distortion.

### When Would You Use It?

Almost never intentionally. It is the default you are trying to *escape from* by using the other values. You rarely set `object-fit: fill` explicitly unless you want to override a more specific rule.

### Example

```css
.fill-demo {
  width: 250px;
  height: 150px;
  object-fit: fill;   /* Default behaviour — stretches to fill exactly */
  border: 3px solid red;
}
```

```html
<img class="fill-demo" src="nigerian-food.jpg" alt="Nigerian food">
```

**Expected output in browser:** The food image is stretched to exactly 250×150px regardless of its original shape. If the original was square, the result will look wide and squashed.

> 💡 **Thinking Prompt:** What do you think would happen if the image's natural size was already 250×150px? Would `fill` cause any distortion in that case?

---

## Section 4 — `object-fit: contain`

### What Is It?

`contain` shrinks (or grows) the image while **preserving its natural proportions** (aspect ratio), so that the entire image fits inside the container. No part of the image is ever cropped. However, if the image's shape doesn't match the container, you will see empty space on two sides — these empty areas show the container's background colour.

### Real-World Analogy

Imagine placing a tall portrait photo inside a wide landscape frame. The photo shrinks until its full height fits, leaving empty space on the left and right. You see the complete photo — but the frame is not fully filled.

### Example

```css
.contain-demo {
  width: 300px;
  height: 200px;
  background-color: #f0f0f0;   /* Shows as letterbox bars */
  object-fit: contain;
  border: 3px solid #009900;
}
```

```html
<img class="contain-demo" src="adire-fabric.jpg" alt="Adire fabric">
```

**Expected output in browser:** The fabric image shrinks proportionally until it fits entirely within the 300×200 container. Grey bars appear on either the left/right or top/bottom (depending on the image's natural shape). The full image is always visible.

### When to Use `contain`

- Product images where you must show the **entire item** (shoes, fabric, electronics) without cropping anything off
- Logos and icons that must always appear complete
- Situations where showing the full image is more important than filling the container

---

## Section 5 — `object-fit: cover`

### What Is It?

`cover` is the **most commonly used value** in real web development. It zooms the image until it fully covers the container from edge to edge, while still **preserving its natural proportions**. Any parts of the image that overflow the container are simply clipped (hidden). The container is always perfectly filled with no empty space.

### Real-World Analogy

Imagine printing a tall portrait photo large enough that its width exactly matches your wide frame. The full width is covered, but the top and bottom of the photo are hidden behind the frame edges. The frame looks completely filled — but some of the photo is cropped.

### Example

```css
.cover-demo {
  width: 300px;
  height: 200px;
  object-fit: cover;
  border: 3px solid #006400;
}
```

```html
<img class="cover-demo" src="lagos-skyline.jpg" alt="Lagos skyline">
```

**Expected output in browser:** The skyline image fills the container perfectly with no empty space and no distortion. The image is cropped on the sides or top/bottom (wherever the overflow is), but the visible portion looks natural and undistorted.

### When to Use `cover`

- Profile photos in circular or square containers (the most popular use case)
- Hero banners and section backgrounds
- Product card images in a grid layout — they all appear the same size without distortion
- Blog post thumbnails

> ⚠️ **Important:** With `cover`, you are accepting that some parts of the image may be hidden (cropped). Use `object-position` (Section 8) to control which part is kept visible.

### Comparing `contain` vs `cover` Side by Side

```html
<div class="demo-row">
  <div>
    <p>contain</p>
    <img class="contain" src="ankara-pattern.jpg" alt="Ankara">
  </div>
  <div>
    <p>cover</p>
    <img class="cover" src="ankara-pattern.jpg" alt="Ankara">
  </div>
</div>
```

```css
.contain, .cover {
  width: 200px;
  height: 200px;
  border: 3px solid #333;
}

.contain {
  object-fit: contain;
  background-color: #eee;  /* Visible in the empty spaces */
}

.cover {
  object-fit: cover;
  /* No background needed — image always fills the container */
}
```

**Expected output in browser:** The `contain` image shows the full pattern but with grey bars. The `cover` image fills the square completely with the pattern — no bars, but edges may be cropped.

---

## Section 6 — `object-fit: none`

### What Is It?

`none` displays the image at its **natural (intrinsic) size** — completely ignoring the `width` and `height` set on the `<img>` element. If the image is larger than the container, it overflows. If it is smaller, empty space shows.

### When Would You Use It?

Rarely — mainly when you intentionally want the image displayed at its natural pixel size, and you are controlling overflow yourself. It is mostly useful as a comparison tool to see what the original image size looks like.

### Example

```css
.none-demo {
  width: 200px;
  height: 150px;
  object-fit: none;
  overflow: hidden;   /* Clip the overflow */
  border: 3px solid orange;
}
```

```html
<img class="none-demo" src="large-map-of-nigeria.jpg" alt="Nigeria map">
```

**Expected output in browser:** The image appears at its natural size (e.g., 800×600px). Only the portion that fits within the 200×150 container is visible — the rest is clipped by `overflow: hidden`. The visible portion is the top-left corner by default.

---

## Section 7 — `object-fit: scale-down`

### What Is It?

`scale-down` compares two options — `none` and `contain` — and picks whichever results in the **smaller displayed size**.

- If the image's natural size is **larger** than the container → behaves like `contain` (shrinks to fit)
- If the image's natural size is **smaller** than the container → behaves like `none` (stays at natural size, not stretched)

### Why Is This Useful?

It prevents small images from being blown up (stretched larger than their natural size), while still ensuring large images are shrunk to fit. This is ideal for situations where images come from different sources with unpredictable sizes.

### Example

```css
.scale-down-demo {
  width: 300px;
  height: 200px;
  object-fit: scale-down;
  background-color: #f5f5f5;
  border: 2px dashed #999;
}
```

```html
<!-- Small image: stays at natural size (no stretching) -->
<img class="scale-down-demo" src="small-logo-50px.png" alt="Small logo">

<!-- Large image: shrinks to fit (same as contain) -->
<img class="scale-down-demo" src="large-banner-1200px.jpg" alt="Large banner">
```

**Expected output in browser (first image):** The 50px logo stays at 50px — it is not stretched to fill the 300×200 container.
**Expected output in browser (second image):** The 1200px banner shrinks proportionally to fit inside the 300×200 container, same as `contain`.

---

## Section 8 — Introducing `object-position`

### What Is It?

`object-position` controls **which part of the image is visible** within the container after `object-fit` is applied.

When you use `object-fit: cover` or `object-fit: none`, part of the image is clipped. By default, the browser shows the **centre** of the image. But what if the important subject of the photo is at the top, or the left side, or 30% from the right? That is exactly what `object-position` lets you control.

### Why It Matters

Imagine a team photo where everyone's face is at the top of the image. With `object-fit: cover` in a square container, the browser shows the centre — which might be their chests, not their faces. `object-position: top` fixes this immediately.

### Syntax

```css
img {
  object-fit: cover;
  object-position: center;          /* Default */
  object-position: top;             /* Show the top of the image */
  object-position: bottom;          /* Show the bottom */
  object-position: left;            /* Show the left side */
  object-position: right;           /* Show the right side */
  object-position: top left;        /* Show the top-left corner */
  object-position: 30% 70%;         /* 30% from left, 70% from top */
  object-position: 50px 20px;       /* 50px from left, 20px from top */
}
```

> 💡 The two values in `object-position` represent **horizontal** position first, then **vertical** position. This matches how `background-position` works.

---

## Section 9 — `object-position` with Keyword Values

### The Keyword Values

You can use any combination of these keywords:

- **Horizontal:** `left`, `center`, `right`
- **Vertical:** `top`, `center`, `bottom`

When you write just one keyword, the other axis defaults to `center`.

### Example — Controlling Which Part of an Image Shows

```css
.portrait-card {
  width: 200px;
  height: 200px;
  object-fit: cover;
  border-radius: 50%;   /* Make it circular */
  border: 4px solid #006400;
}

.show-top    { object-position: top; }
.show-center { object-position: center; }   /* Default */
.show-bottom { object-position: bottom; }
.show-left   { object-position: left; }
.show-right  { object-position: right; }
```

```html
<!-- Imagine each uses the same tall portrait of "Adaeze" -->
<img class="portrait-card show-top"    src="adaeze.jpg" alt="Adaeze">
<img class="portrait-card show-center" src="adaeze.jpg" alt="Adaeze">
<img class="portrait-card show-bottom" src="adaeze.jpg" alt="Adaeze">
```

**Expected output in browser:**
- `show-top` → Adaeze's face and shoulders are visible (best for most portrait photos)
- `show-center` → the middle portion of the image is visible
- `show-bottom` → Adaeze's lower body is visible

> 💡 **Thinking Prompt:** If you had a group photo of all four Wizkid dancers, and only the right two are important, which `object-position` value would you use?

### Two-Keyword Example

```css
.corner-photo {
  width: 250px;
  height: 150px;
  object-fit: cover;
  object-position: top left;   /* Show the top-left corner of the image */
}
```

**Expected output in browser:** When the image is cropped to fit the container, the top-left corner of the original image is what you see.

---

## Section 10 — `object-position` with Length and Percentage Values

### Using Percentages

Percentage values give you very precise control. The format is:

```css
object-position: horizontal% vertical%;
```

- `0% 0%` = top-left corner
- `50% 50%` = centre (same as `center center`)
- `100% 100%` = bottom-right corner
- `30% 20%` = 30% across from left, 20% down from top

### Example — Precise Face Positioning

```css
.staff-photo {
  width: 180px;
  height: 180px;
  object-fit: cover;
  border-radius: 50%;
  object-position: 40% 15%;  /* Face is slightly left of centre, near the top */
}
```

```html
<img class="staff-photo" src="chukwuemeka-profile.jpg" alt="Chukwuemeka">
```

**Expected output in browser:** The circular crop shows Chukwuemeka's face exactly where you positioned it — 40% across and 15% down from the top. No more cropped-out foreheads!

### Using Pixel Values

```css
object-position: 50px 30px;
/* Shows the part of the image starting 50px from the left and 30px from the top */
```

### Using Negative Values

You can even use negative values to push the image in the opposite direction:

```css
object-position: -20px 0;
/* Shifts the image 20px to the left, showing content that starts 20px into the image */
```

---

## Section 11 — Combining `object-fit` and `object-position`

### The Power Pair

`object-fit` decides **how** the image fills the container. `object-position` decides **which part** of the image is shown. Used together, they give you complete, professional image control.

### Example — A Product Card Grid

```css
/* The card container */
.product-card {
  width: 220px;
  background-color: white;
  border-radius: 10px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

/* Fixed-size image area */
.product-card img {
  width: 100%;
  height: 200px;
  object-fit: cover;         /* Fill without distortion */
  object-position: center;   /* Show the centre (adjust per image if needed) */
  display: block;
}

/* Card text */
.product-card .info {
  padding: 12px;
}
```

```html
<div class="product-card">
  <img src="ankara-dress.jpg" alt="Ankara dress">
  <div class="info">
    <h3>Ankara Wrap Dress</h3>
    <p>₦8,500</p>
  </div>
</div>

<div class="product-card">
  <img src="leather-bag.jpg" alt="Leather bag">
  <div class="info">
    <h3>Aba Leather Handbag</h3>
    <p>₦12,000</p>
  </div>
</div>
```

**Expected output in browser:** Both product cards are the exact same size. Both images fill their 220px × 200px area perfectly with no distortion and no empty space, regardless of each image's original dimensions. The page looks professional and consistent.

### Example — A Team Page with Circular Avatars

```css
.team-avatar {
  width: 140px;
  height: 140px;
  border-radius: 50%;
  object-fit: cover;
  object-position: top center;   /* Show faces, not chests */
  border: 4px solid #006400;
  display: block;
  margin: 0 auto 10px;
}
```

```html
<figure>
  <img class="team-avatar" src="bola-portrait.jpg" alt="Bola Adeyemi">
  <figcaption>Bola Adeyemi — Lead Developer</figcaption>
</figure>

<figure>
  <img class="team-avatar" src="funke-portrait.jpg" alt="Funke Okafor">
  <figcaption>Funke Okafor — Product Designer</figcaption>
</figure>
```

**Expected output in browser:** Each team member's photo appears in a perfectly circular frame, showing their face and shoulders. All circles are the same size regardless of the original photo dimensions.

---

## Guided Exercises

---

### Exercise 1 — The Jumia-Style Product Grid (Beginner)

**Scenario:** You are building the product listing page for an online Nigerian market called "Oja Online." You have four product images of different shapes, but all cards must look identical.

**Objective:** Create four image cards, each 180px × 180px, that display images without distortion.

**Steps:**

1. Create an HTML file with four `<div class="card">` elements, each containing an `<img>` and a product name in a `<p>` tag
2. Use real image names or placeholder image services like `https://via.placeholder.com/300x400` (tall), `https://via.placeholder.com/400x200` (wide)
3. Style the `.card` to have a fixed width, border, and padding
4. Style the `img` with `width: 100%`, `height: 180px`, and `object-fit: cover`

**Hints:**
- Set `display: block` on the `img` to remove the small gap below it
- Don't forget `overflow: hidden` on the card to keep things tidy

**Solution:**

```css
.card-grid {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

.card {
  width: 180px;
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
  background-color: white;
}

.card img {
  width: 100%;
  height: 180px;
  object-fit: cover;
  object-position: center;
  display: block;
}

.card p {
  padding: 8px;
  margin: 0;
  font-size: 14px;
  text-align: center;
}
```

```html
<div class="card-grid">
  <div class="card">
    <img src="https://via.placeholder.com/300x500" alt="Tall product">
    <p>Ankara Blouse</p>
  </div>
  <div class="card">
    <img src="https://via.placeholder.com/600x200" alt="Wide product">
    <p>Gele Head Wrap</p>
  </div>
  <div class="card">
    <img src="https://via.placeholder.com/300x300" alt="Square product">
    <p>Beaded Necklace</p>
  </div>
  <div class="card">
    <img src="https://via.placeholder.com/400x350" alt="Near-square product">
    <p>Leather Sandal</p>
  </div>
</div>
```

**Expected output in browser:** All four cards are identical in size. All four images fill their 180px height without distortion. No empty bars appear.

**Self-check Questions:**
- What would happen if you changed `cover` to `contain`?
- What would you change if you wanted to ensure no image content is ever cropped?

---

### Exercise 2 — Team Profile Circles (Intermediate)

**Scenario:** You are building the "About Us" page for a Lagos tech startup called "Abuja Stack Ltd." The design team has given you portraits of five staff members — but the photos come in different shapes (some landscape, some portrait, some square).

**Objective:** Create circular profile avatars that all show faces correctly.

**Steps:**

1. Create five `<figure>` elements, each with an `<img>` and a `<figcaption>`
2. Style the image as a circle: `border-radius: 50%`, `width: 120px`, `height: 120px`
3. Apply `object-fit: cover` to fill the circle
4. Apply `object-position: top center` so faces show
5. Add a green border to each avatar

**Solution:**

```css
.profile-grid {
  display: flex;
  gap: 30px;
  flex-wrap: wrap;
  justify-content: center;
}

figure {
  text-align: center;
  margin: 0;
}

.avatar {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  object-position: top center;
  border: 4px solid #006400;
  display: block;
}

figcaption {
  margin-top: 8px;
  font-size: 13px;
  font-weight: bold;
  color: #333;
}
```

```html
<div class="profile-grid">
  <figure>
    <img class="avatar" src="https://via.placeholder.com/300x400" alt="Ngozi">
    <figcaption>Ngozi Eze<br>CEO</figcaption>
  </figure>
  <figure>
    <img class="avatar" src="https://via.placeholder.com/600x300" alt="Emeka">
    <figcaption>Emeka Obi<br>CTO</figcaption>
  </figure>
  <figure>
    <img class="avatar" src="https://via.placeholder.com/250x250" alt="Amina">
    <figcaption>Amina Sule<br>Designer</figcaption>
  </figure>
</div>
```

**Expected output in browser:** Three perfectly circular green-bordered avatars, all 120×120px, each showing the top portion (face area) of the photo regardless of the original image's shape.

**Self-check Questions:**
- If a staff member's photo had their face at the very bottom of the image, what `object-position` value would you use?
- What would happen if you removed `border-radius: 50%` but kept `object-fit: cover`?

---

### Exercise 3 — The Hero Banner Showcase (Advanced)

**Scenario:** You are building a homepage for a Nigerian cultural event website called "Afrobeats Festival Ibadan." You need a full-width hero banner image that always looks great no matter the screen size, and a logo that never stretches.

**Objective:** Use `object-fit: cover` for the hero banner and `object-fit: contain` for the logo, with appropriate positioning.

**Steps:**

1. Create a `.hero` section with `width: 100%`, `height: 400px`
2. Place an `<img>` inside it with `width: 100%`, `height: 100%`, `object-fit: cover`
3. Position the image to show the top portion: `object-position: top center`
4. Create a `.logo-box` div with `width: 150px`, `height: 80px`
5. Place a logo `<img>` inside with `object-fit: contain` and no background distortion

**Solution:**

```css
/* Hero banner */
.hero {
  width: 100%;
  height: 400px;
  overflow: hidden;
  position: relative;
}

.hero img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top center;
  display: block;
}

.hero-overlay {
  position: absolute;
  bottom: 30px;
  left: 40px;
  color: white;
  text-shadow: 2px 2px 8px rgba(0,0,0,0.8);
}

.hero-overlay h1 { font-size: 36px; margin: 0; }
.hero-overlay p  { font-size: 18px; margin: 5px 0 0; }

/* Logo */
.logo-box {
  width: 150px;
  height: 80px;
  background-color: #f0f0f0;
  border: 1px solid #ccc;
  padding: 5px;
}

.logo-box img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  object-position: center;
}
```

```html
<section class="hero">
  <img src="https://via.placeholder.com/1920x600" alt="Afrobeats festival crowd">
  <div class="hero-overlay">
    <h1>Afrobeats Festival Ibadan</h1>
    <p>December 2025 · Mapo Hill</p>
  </div>
</section>

<div class="logo-box">
  <img src="https://via.placeholder.com/300x100" alt="Festival Logo">
</div>
```

**Expected output in browser:** A full-width 400px-tall hero image fills the section without distortion, showing the top portion. Overlaid text sits at the bottom-left. Below it, the logo fits cleanly in its box without stretching, with padding space around it if the proportions differ.

---

## Code Challenges

---

### Challenge 1 — Fix the Broken Product Page

**Task:** The code below produces stretched, distorted images. Add the correct `object-fit` property to fix it so images fill their containers cleanly without distortion. Do not change any other rule.

```html
<div class="item"><img src="jollof-rice.jpg" alt="Jollof Rice"></div>
<div class="item"><img src="egusi-soup.jpg" alt="Egusi Soup"></div>
<div class="item"><img src="pounded-yam.jpg" alt="Pounded Yam"></div>
```

```css
.item {
  width: 200px;
  height: 150px;
  border: 2px solid #009900;
  overflow: hidden;
}

.item img {
  width: 100%;
  height: 100%;
  /* Your fix goes here */
}
```

**Solution:**

```css
.item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

---

### Challenge 2 — The Face-Cropping Problem

**Task:** A news website shows author profile pictures, but faces are being cut off at the top (the browser is showing the centre of tall portrait photos). Fix this using `object-position` without changing the existing `object-fit: cover` rule.

```css
.author-pic {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
  /* Your fix goes here */
}
```

**Solution:**

```css
.author-pic {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
  object-position: top center;
}
```

---

### Challenge 3 — Show a Specific Part of an Image

**Task:** You have a wide landscape photo of the Lagos Island skyline (3000px × 800px). You are displaying it in a `400px × 300px` container. You want to show the **right side** of the skyline — where the tallest buildings are. Use `object-position` to achieve this.

**Solution:**

```css
.skyline {
  width: 400px;
  height: 300px;
  object-fit: cover;
  object-position: right center;
}
```

Or for more precise control:

```css
.skyline {
  width: 400px;
  height: 300px;
  object-fit: cover;
  object-position: 80% 50%;  /* 80% from the left shows the right portion */
}
```

---

### Challenge 4 — Logo Display Without Stretching

**Task:** You are placing various partner logos into a uniform 160×60px container. Some logos are wide, some are square, some are tall. You want every logo to appear complete (no cropping) and centred, even if there is empty space around it. No logo should ever be stretched beyond its natural size.

**Solution:**

```css
.partner-logo-box {
  width: 160px;
  height: 60px;
  background-color: #fafafa;
  border: 1px solid #eee;
  display: flex;
  align-items: center;
  justify-content: center;
}

.partner-logo-box img {
  width: 100%;
  height: 100%;
  object-fit: scale-down;    /* Shrinks large logos; doesn't stretch small ones */
  object-position: center;
}
```

---

## Mini Project — The Oja Digital Market Gallery

### Project Overview

You will build a complete, professionally styled Nigerian online market gallery page for "Oja Digital." It will include a hero banner, a product image grid, and a team section — all using `object-fit` and `object-position` to ensure every image displays perfectly.

---

### Stage 1 — Set Up the HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Oja Digital — Nigerian Online Market</title>
  <link rel="stylesheet" href="oja-market.css">
</head>
<body>

  <!-- Hero Banner -->
  <section class="hero">
    <img src="https://via.placeholder.com/1920x700/006400/ffffff?text=Oja+Digital+Market"
         alt="Oja Digital Market banner">
    <div class="hero-text">
      <h1>Oja Digital</h1>
      <p>Authentic Nigerian Goods — From Every State</p>
    </div>
  </section>

  <!-- Product Grid -->
  <main class="products">
    <h2>Featured Products</h2>
    <div class="product-grid">
      <div class="product-card">
        <img src="https://via.placeholder.com/300x500/cc6600/ffffff?text=Ankara" alt="Ankara fabric">
        <div class="card-info">
          <h3>Ankara Fabric (6 yards)</h3>
          <p>₦4,500</p>
        </div>
      </div>
      <div class="product-card">
        <img src="https://via.placeholder.com/600x250/006400/ffffff?text=Gele" alt="Gele head wrap">
        <div class="card-info">
          <h3>Premium Gele</h3>
          <p>₦6,200</p>
        </div>
      </div>
      <div class="product-card">
        <img src="https://via.placeholder.com/400x400/330099/ffffff?text=Bag" alt="Leather bag">
        <div class="card-info">
          <h3>Aba Leather Bag</h3>
          <p>₦15,000</p>
        </div>
      </div>
      <div class="product-card">
        <img src="https://via.placeholder.com/350x600/cc0000/ffffff?text=Sandal" alt="Leather sandal">
        <div class="card-info">
          <h3>Handmade Sandal</h3>
          <p>₦5,800</p>
        </div>
      </div>
    </div>
  </main>

  <!-- Team Section -->
  <section class="team">
    <h2>Meet Our Team</h2>
    <div class="team-grid">
      <figure>
        <img class="avatar" src="https://via.placeholder.com/300x450/006400/ffffff?text=CEO"
             alt="Olumide Adeyemi">
        <figcaption>Olumide Adeyemi<br><small>Founder & CEO</small></figcaption>
      </figure>
      <figure>
        <img class="avatar" src="https://via.placeholder.com/450x300/cc6600/ffffff?text=CTO"
             alt="Ngozi Okonkwo">
        <figcaption>Ngozi Okonkwo<br><small>Chief Technology Officer</small></figcaption>
      </figure>
      <figure>
        <img class="avatar" src="https://via.placeholder.com/300x300/330099/ffffff?text=CMO"
             alt="Amina Bello">
        <figcaption>Amina Bello<br><small>Head of Marketing</small></figcaption>
      </figure>
    </div>
  </section>

  <!-- Partner Logos -->
  <section class="partners">
    <h2>Our Partners</h2>
    <div class="logo-strip">
      <div class="logo-box">
        <img src="https://via.placeholder.com/300x80/333333/ffffff?text=Partner+A" alt="Partner A">
      </div>
      <div class="logo-box">
        <img src="https://via.placeholder.com/80x80/666666/ffffff?text=P+B" alt="Partner B">
      </div>
      <div class="logo-box">
        <img src="https://via.placeholder.com/250x120/999999/ffffff?text=Partner+C" alt="Partner C">
      </div>
    </div>
  </section>

</body>
</html>
```

**Milestone 1 output:** A plain, unstyled page with all sections visible but images in various distorted shapes.

---

### Stage 2 — Base Styles and Hero Banner

```css
/* oja-market.css */

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Arial', sans-serif;
  background-color: #fafafa;
  color: #222;
}

h2 {
  text-align: center;
  margin: 40px 0 20px;
  color: #006400;
  font-size: 28px;
}

/* ── HERO BANNER ── */
.hero {
  width: 100%;
  height: 420px;
  position: relative;
  overflow: hidden;
}

.hero img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center top;   /* Show the top of the banner image */
  display: block;
}

.hero-text {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  text-align: center;
  color: white;
  text-shadow: 2px 2px 10px rgba(0,0,0,0.7);
}

.hero-text h1 { font-size: 42px; }
.hero-text p  { font-size: 18px; margin-top: 8px; }
```

**Milestone 2 output:** A full-width 420px-tall green hero banner with centred white text overlaid. The banner image fills the space without distortion.

---

### Stage 3 — Product Grid

```css
/* ── PRODUCT GRID ── */
.products {
  max-width: 1000px;
  margin: 0 auto;
  padding: 0 20px 40px;
}

.product-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

.product-card {
  width: 220px;
  background-color: white;
  border-radius: 10px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  overflow: hidden;
  transition: transform 0.2s;
}

.product-card:hover {
  transform: translateY(-4px);
}

.product-card img {
  width: 100%;
  height: 210px;
  object-fit: cover;
  object-position: center;   /* Show the most representative centre portion */
  display: block;
}

.card-info {
  padding: 12px 14px;
}

.card-info h3 {
  font-size: 15px;
  margin-bottom: 6px;
  color: #222;
}

.card-info p {
  font-size: 16px;
  font-weight: bold;
  color: #006400;
}
```

**Milestone 3 output:** Four uniform product cards in a flex grid. All images are the same height (210px) and display without distortion regardless of their original dimensions. Cards gently lift on hover.

---

### Stage 4 — Team and Partner Sections

```css
/* ── TEAM SECTION ── */
.team {
  background-color: #f0f5f0;
  padding: 20px 0 50px;
}

.team-grid {
  display: flex;
  gap: 40px;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 10px;
}

.team-grid figure {
  text-align: center;
}

.avatar {
  width: 130px;
  height: 130px;
  border-radius: 50%;
  object-fit: cover;
  object-position: top center;  /* Always show face area */
  border: 5px solid #006400;
  display: block;
  margin: 0 auto 10px;
}

figcaption {
  font-size: 14px;
  font-weight: bold;
  color: #333;
  line-height: 1.5;
}

figcaption small {
  font-weight: normal;
  color: #777;
}

/* ── PARTNER LOGOS ── */
.partners {
  padding: 20px 0 60px;
}

.logo-strip {
  display: flex;
  gap: 30px;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 10px;
}

.logo-box {
  width: 180px;
  height: 70px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 6px;
  padding: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.logo-box img {
  width: 100%;
  height: 100%;
  object-fit: scale-down;     /* Never stretch logos; shrink large ones */
  object-position: center;
}
```

**Milestone 4 (Final) output:** The complete Oja Digital market page now shows:
- A polished full-width hero banner
- Uniform product cards in a flex grid with no distorted images
- Circular team avatars showing faces (not chests or feet)
- Partner logos cleanly contained in uniform boxes — none are stretched beyond their natural size

---

## Common Beginner Mistakes

---

### Mistake 1 — Applying `object-fit` to a `<div>` Instead of `<img>`

**Wrong:**
```css
.card {
  object-fit: cover;   /* This does NOTHING on a div */
}
```

**Problem:** `object-fit` only works on **replaced elements** — elements that display external content like `<img>`, `<video>`, and `<iframe>`. It has no effect on `<div>`, `<p>`, or other container elements.

**Correct:** Apply `object-fit` to the `<img>` directly:
```css
.card img {
  object-fit: cover;   /* Correct — on the img element */
}
```

---

### Mistake 2 — Forgetting to Set Both `width` and `height` on the Image

**Wrong:**
```css
img {
  object-fit: cover;
  /* No width or height set */
}
```

**Problem:** `object-fit` only does something when the image is constrained to a specific size. Without `width` and `height`, the image displays at its natural dimensions — and `object-fit` has nothing to act on.

**Correct:**
```css
img {
  width: 100%;      /* or a fixed px value */
  height: 200px;    /* Must have a fixed height */
  object-fit: cover;
}
```

---

### Mistake 3 — Confusing `contain` and `cover`

**Wrong mental model:** "I want the image to cover my container, so I should use `contain`."

**Problem:** The names are the opposite of what many beginners expect.
- `contain` = **contains** the image *inside* the box → may show empty space
- `cover` = **covers** the box completely → may crop the image

**Memory tip:** `cover` = like a book cover — it fills the whole space. `contain` = the image is *contained* within borders — nothing spills out.

---

### Mistake 4 — Using `object-position` Without `object-fit`

**Wrong:**
```css
img {
  width: 200px;
  height: 150px;
  object-position: top;
  /* No object-fit! */
}
```

**Problem:** Without `object-fit: cover` or `object-fit: none`, the image is stretched to fill the container (`fill` is the default), and `object-position` has nothing meaningful to shift.

**Correct:**
```css
img {
  width: 200px;
  height: 150px;
  object-fit: cover;       /* First define how the image fills the space */
  object-position: top;    /* Then control which part is visible */
}
```

---

### Mistake 5 — Swapping `object-position` Value Order

**Wrong:**
```css
object-position: 50px top;   /* Invalid — mixing px and keyword incorrectly */
```

**Problem:** When mixing lengths and keywords, the **horizontal** value must come first, then the **vertical** value.

**Correct:**
```css
object-position: left 50px;     /* horizontal: left; vertical: 50px */
object-position: 30% top;       /* horizontal: 30%; vertical: top */
object-position: 50px 30px;     /* horizontal: 50px; vertical: 30px */
```

---

### Mistake 6 — Expecting `scale-down` to Always Behave Like `contain`

**Wrong thinking:** "`scale-down` and `contain` do the same thing."

**Problem:** They only look the same when the image is *larger* than the container. When the image is *smaller* than the container:
- `contain` **scales up** the small image to fill the container (without cropping)
- `scale-down` **keeps the image at its natural size** (does not scale up)

**When to use which:**
- Use `contain` when you want the image to always fill the container proportionally (allows upscaling)
- Use `scale-down` when you never want an image to appear larger than its natural size

---

## Reflection Questions

Think about these carefully before moving to the next lesson:

1. What is the key difference between `object-fit: contain` and `object-fit: cover`? Give a real-world scenario where each would be the correct choice.
2. Why does `object-fit` have no effect when applied to a `<div>` element?
3. If you have a portrait photo where the subject's face is in the top-right corner, what `object-position` value would you use to ensure the face is always visible in a square crop?
4. What does `object-fit: scale-down` do differently from `object-fit: contain` when the image is *smaller* than its container?
5. In a product grid, why is `cover` generally preferred over `contain` for product card images?

---

## Completion Checklist

Before marking this lesson complete, confirm that you can:

- [ ] Explain why images distort when placed in a fixed-size container without `object-fit`
- [ ] Use `object-fit: fill` and explain when it causes problems
- [ ] Use `object-fit: contain` and describe when empty space appears
- [ ] Use `object-fit: cover` and explain what gets cropped
- [ ] Use `object-fit: none` and explain when the image overflows
- [ ] Use `object-fit: scale-down` and explain how it differs from `contain`
- [ ] Use `object-position` with keyword values (`top`, `bottom`, `left`, `right`, `center`)
- [ ] Use `object-position` with percentage values for precise control
- [ ] Combine `object-fit` and `object-position` in a product card layout
- [ ] Apply circular avatar styling using `border-radius`, `object-fit: cover`, and `object-position: top`
- [ ] Use `scale-down` for logo containers of varying image sizes
- [ ] Completed all stages of the Oja Digital mini-project

---

## Lesson Summary

In this lesson, you learned two properties that solve one of the most common real-world CSS problems — displaying images of different shapes cleanly inside fixed-size containers.

**`object-fit`** controls how the image fills its container. `fill` stretches (the distorted default). `contain` shrinks the image to fit completely with possible empty space. `cover` zooms to fill completely with possible cropping — the most widely used value. `none` shows the natural size. `scale-down` picks the smaller of `none` or `contain`, preventing small images from being upscaled.

**`object-position`** controls which part of the image is visible after fitting. It accepts keyword pairs (`top`, `right`, `bottom`, `left`, `center`), percentage pairs (`30% 70%`), and pixel values (`50px 20px`). The horizontal value always comes first.

Used together, these two properties give you complete, professional control over image presentation — the same control used by every major Nigerian and global e-commerce and media website.

---

## Quick-Reference Card

```css
/* ── object-fit ── */
img {
  width: 200px;
  height: 200px;

  object-fit: fill;        /* Stretches to fit — may distort (default) */
  object-fit: contain;     /* Shrinks to fit fully — may show empty space */
  object-fit: cover;       /* Zooms to fill — may crop edges */
  object-fit: none;        /* Natural size — may overflow */
  object-fit: scale-down;  /* Smaller of 'none' or 'contain' — never upscales */
}

/* ── object-position ── */
img {
  object-fit: cover;

  object-position: center;          /* Default — shows centre of image */
  object-position: top;             /* Shows top portion */
  object-position: bottom;          /* Shows bottom portion */
  object-position: left;            /* Shows left portion */
  object-position: right;           /* Shows right portion */
  object-position: top right;       /* Shows top-right corner */
  object-position: 30% 60%;         /* 30% from left, 60% from top */
  object-position: 50px 20px;       /* 50px from left, 20px from top */
}

/* ── Most Common Pattern: Product Card ── */
.card img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  object-position: center;
  display: block;
}

/* ── Most Common Pattern: Circular Avatar ── */
.avatar {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  object-position: top center;
}

/* ── Most Common Pattern: Logo Box ── */
.logo-box img {
  width: 100%;
  height: 100%;
  object-fit: scale-down;
  object-position: center;
}
```

---

*End of Lesson 59 — CSS `object-fit` and `object-position`*
