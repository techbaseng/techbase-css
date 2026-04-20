---
render_with_liquid: false
title: "CSS Opacity and Transparency"
nav_order: 31
---

# Lesson 31: CSS Opacity and Transparency

---

## Lesson Introduction

Have you ever noticed on a website how an image looks slightly faded until you hover your mouse over it — and then it suddenly becomes sharp and vivid? Or how a pop-up box has a semi-transparent dark background that lets you still see the page behind it? Or how some text overlays an image, sitting on a partially see-through coloured panel?

All of these effects are created using CSS **opacity** and **transparency** techniques.

In this lesson, you will learn:

- What opacity and transparency mean in CSS
- How to use the `opacity` property to make elements see-through
- The difference between opacity values (0.0 to 1.0) and what each means visually
- How to use opacity with the `:hover` selector for interactive image effects
- A very important problem with `opacity` — and how to solve it using **RGBA colour values**
- How to create a transparent background box with text overlaid on an image
- Real-world uses of opacity in modern web design

By the end of this lesson, you will be able to confidently apply transparency effects to images, backgrounds, boxes, and text on any web page.

---

## Prerequisite Concepts

Before learning opacity, let's quickly review two things that will help you understand this lesson better.

### What Is a CSS Property?

A CSS property is an instruction you give to the browser about how an element should look. For example:
- `color: red;` tells the browser to make the text red
- `font-size: 20px;` tells the browser to make the text 20 pixels tall
- `opacity: 0.5;` tells the browser to make the element 50% transparent

### What Are RGB and RGBA Colours?

You may already know that colours on screens are made from three light channels: **Red**, **Green**, and **Blue** (RGB).

In CSS, you can write colours like this:
```css
color: rgb(255, 0, 0);   /* Pure red */
color: rgb(0, 128, 0);   /* Green */
color: rgb(0, 0, 255);   /* Pure blue */
```

**RGBA** is the same thing, but with a fourth channel: **Alpha**. The alpha channel controls transparency:
```css
color: rgba(255, 0, 0, 1.0);   /* Pure red, fully opaque */
color: rgba(255, 0, 0, 0.5);   /* Pure red, 50% transparent */
color: rgba(255, 0, 0, 0.0);   /* Pure red, fully invisible */
```

Understanding RGBA is crucial for this lesson, because it is the key to solving a major opacity problem we will explore.

---

## Section 1: What Is Opacity? What Is Transparency?

### The Simple Explanation

**Opacity** describes how solid or how see-through something is.

- **High opacity** = more solid, less see-through (like a thick wall)
- **Low opacity** = more see-through, less solid (like a glass window)

**Transparency** is the opposite of opacity:
- A **fully opaque** element is completely solid — you cannot see through it at all
- A **fully transparent** element is completely invisible — like thin air
- A **semi-transparent** element is somewhere in between — like frosted glass or tinted sunglasses

**Real-world analogy:** Think of a sticker on a glass window. A plain white sticker is fully opaque — you cannot see through it. A frosted decorative sticker is semi-transparent — you can vaguely see through it. Clean, clear glass is fully transparent — you see right through it perfectly.

### How CSS Opacity Works

In CSS, the `opacity` property accepts a number from `0.0` to `1.0`:

| Value | Meaning | Visual Effect |
|-------|---------|---------------|
| `1` or `1.0` | Fully opaque | Normal — nothing see-through |
| `0.75` | 75% opaque | Slightly transparent |
| `0.5` | 50% opaque | Half transparent (semi-transparent) |
| `0.25` | 25% opaque | Very transparent |
| `0` or `0.0` | Fully transparent | Completely invisible |

> **Key rule to remember:** The **lower** the opacity value, the **more transparent** the element becomes. Think of it as a percentage: `0.5` = 50% opaque = 50% see-through.

---

## Section 2: Basic Opacity on Images

### The Syntax

```css
selector {
  opacity: value;  /* A number from 0.0 to 1.0 */
}
```

That's it. One line. Let's see it in action.

### Example 1: Four Images at Different Opacity Levels

```html
<!-- HTML -->
<img src="forest.jpg" alt="Forest" class="op-100">
<img src="forest.jpg" alt="Forest" class="op-60">
<img src="forest.jpg" alt="Forest" class="op-30">
<img src="forest.jpg" alt="Forest" class="op-10">
```

```css
/* CSS */
img {
  width: 200px;
  height: 150px;
}

.op-100 { opacity: 1;    }   /* Fully opaque  — normal image */
.op-60  { opacity: 0.6;  }   /* 60% opaque    — slightly faded */
.op-30  { opacity: 0.3;  }   /* 30% opaque    — very faded */
.op-10  { opacity: 0.1;  }   /* 10% opaque    — almost invisible */
```

**Expected Output (visual description):**
```
[ Normal image ]  [ Slightly faded ]  [ Very faded ]  [ Almost invisible ]
   opacity: 1        opacity: 0.6      opacity: 0.3      opacity: 0.1
```

**Line-by-line explanation:**
- `opacity: 1;` — The image looks completely normal. No transparency at all.
- `opacity: 0.6;` — The image is 60% solid. You can still see it clearly, just slightly faded.
- `opacity: 0.3;` — The image is 30% solid. It looks quite washed out and the white background shows through.
- `opacity: 0.1;` — The image is only 10% solid. It barely appears at all — almost completely transparent.

> **Thinking prompt:** What value would give you 80% opacity? What about 5% opacity? Try writing those values before checking: `opacity: 0.8;` and `opacity: 0.05;`

---

### Example 2: A Single Image with Reduced Opacity

Let's see a concrete, simple example — making a single image 40% transparent:

```html
<!-- HTML -->
<img src="mountain.jpg" alt="Mountain" class="faded-img">
```

```css
/* CSS */
.faded-img {
  opacity: 0.4;    /* Image is 40% opaque (60% transparent) */
  width: 300px;
}
```

**Expected Output:** The mountain image appears washed out and faded — you can see the white page background showing through the image itself.

> **Real-world use:** Faded images are often used for "coming soon" sections, disabled items in a shop, background watermarks, or decorative elements that should not distract from the main content.

---

## Section 3: Opacity with Hover — Interactive Image Effects

One of the most popular uses of opacity is combining it with the CSS `:hover` selector. This lets you change the transparency of an image when the user moves their mouse over it — creating a smooth visual feedback effect.

### What Is `:hover`?

The `:hover` pseudo-class applies styles to an element **only when the user's mouse is positioned over it**. The moment the mouse moves away, the styles go back to their normal state.

```css
/* Normal state */
img {
  opacity: 0.5;
}

/* State when mouse is hovering over the image */
img:hover {
  opacity: 1.0;
}
```

This reads as: "Normally the image is 50% transparent. When the user hovers over it, make it fully opaque."

---

### Example 3: Image Becomes Fully Visible on Hover (Reverse Transparent Effect)

This is the most common hover effect — the image starts semi-transparent and becomes fully visible when hovered.

```html
<!-- HTML -->
<img src="product.jpg" alt="Product" class="hover-reveal">
```

```css
/* CSS */
.hover-reveal {
  opacity: 0.5;          /* Start at 50% opacity — looks faded */
  width: 200px;
  height: 150px;
}

.hover-reveal:hover {
  opacity: 1.0;          /* On hover — become fully opaque (normal) */
}
```

**Expected Output:**
- **Before hover:** The image looks faded, semi-transparent
- **On hover:** The image snaps to full, clear visibility

> **Real-world use:** Online shops often use this to indicate that an item is "available" — it starts faded and becomes sharp when you hover, as if it's "coming to life" for you to select.

---

### Example 4: Image Becomes Transparent on Hover (Transparent Hover Effect)

This is the reverse — the image starts fully opaque and becomes transparent when hovered.

```html
<!-- HTML -->
<img src="photo.jpg" alt="Photo" class="hover-fade">
```

```css
/* CSS */
.hover-fade {
  opacity: 1.0;          /* Start fully opaque — normal image */
  width: 200px;
  height: 150px;
}

.hover-fade:hover {
  opacity: 0.4;          /* On hover — become 40% opacity (faded) */
}
```

**Expected Output:**
- **Before hover:** Normal, fully visible image
- **On hover:** Image fades out to 40% opacity — the page background shows through

> **Thinking prompt:** Why might a designer choose to fade an image *down* on hover rather than fade it *up*? One reason: to draw attention to a caption or overlay text that appears on top of the image when hovered!

---

### Combining Both Examples — Multiple Images Side by Side

Here is a more realistic scenario: a row of photos where each one starts faded and becomes clear on hover.

```html
<!-- HTML -->
<div class="photo-row">
  <img src="photo1.jpg" alt="City">
  <img src="photo2.jpg" alt="Nature">
  <img src="photo3.jpg" alt="People">
</div>
```

```css
/* CSS */
.photo-row img {
  opacity: 0.5;           /* All images start at 50% opacity */
  width: 200px;
  height: 150px;
  margin: 5px;
  border: 2px solid #ccc;
}

.photo-row img:hover {
  opacity: 1.0;           /* Each image becomes fully opaque when hovered */
}
```

**Expected Output (visual):**
```
[ Faded City ] [ Faded Nature ] [ Faded People ]
       ↑ When you hover over any one image, only THAT image becomes fully visible.
         The others remain faded.
```

> **Thinking prompt:** What would happen if you wrote `opacity: 1.0` on the normal state and `opacity: 0.5` on the `:hover` state? The images would start fully visible and fade when hovered — the exact opposite effect!

---

## Section 4: The Big Problem — Opacity Affects Child Elements!

This is one of the most important things to understand about the CSS `opacity` property, and it trips up beginners constantly.

### The Problem Explained

When you apply `opacity` to an element, **every child element inside it also becomes transparent** — at the exact same opacity level. You cannot make just the background transparent while keeping the text inside fully opaque.

**Why does this happen?** Because `opacity` affects the entire element as a single unit — like painting it with a see-through film. Everything inside the box gets the same film applied to it.

**Example of the problem:**

```html
<!-- HTML -->
<div class="transparent-box">
  <p>This text is supposed to be fully readable!</p>
</div>
```

```css
/* CSS — THE PROBLEM */
.transparent-box {
  background-color: green;
  opacity: 0.3;            /* Makes BOTH the green background AND the text transparent! */
  padding: 20px;
  width: 300px;
}
```

**Expected Output (problem):**
```
[  Very faint green box with barely readable text  ]
   "This text is supposed to be fully readable!"
   (But the text is also 30% opaque — very hard to read!)
```

Both the green background and the paragraph text inside become 30% transparent. This is almost certainly NOT what the designer wanted. They wanted the green background to be see-through, but the text to remain fully solid and readable.

> **This is the #1 opacity mistake that beginners make.** Always ask yourself: "Do I want the text/children inside to also be transparent?" If NO — do NOT use `opacity`. Use RGBA instead.

---

## Section 5: The Solution — RGBA Colour Values

### What Is RGBA?

RGBA stands for **Red, Green, Blue, Alpha**. It is a way to specify a colour that includes its transparency level, all in one value.

The syntax is:
```css
background-color: rgba(red, green, blue, alpha);
```

Where:
- `red`, `green`, `blue` = colour channel values from `0` to `255`
- `alpha` = transparency from `0.0` (fully transparent) to `1.0` (fully opaque)

**The crucial difference from `opacity`:** RGBA only makes the **background colour** transparent. The **text and child elements inside remain fully opaque**. It is like painting the wall of a glass house — the wall is see-through, but the people inside are not!

### Side-by-Side Comparison

**Version 1 — Using `opacity` (WRONG for this use case):**
```css
.box-opacity {
  background-color: green;
  opacity: 0.3;     /* BOTH background AND text become 30% transparent — text is hard to read */
}
```

**Version 2 — Using `rgba` (CORRECT):**
```css
.box-rgba {
  background-color: rgba(0, 128, 0, 0.3);  /* Only the BACKGROUND is 30% transparent */
                                            /* Text inside remains 100% opaque and readable */
}
```

The second version is what you almost always want when you have text on a transparent background.

---

### Example 5: RGBA Background — Text Stays Readable

```html
<!-- HTML -->
<div class="card-rgba">
  <h3>Mountain Retreat</h3>
  <p>Escape to the mountains for a peaceful weekend. Fresh air,
     stunning views, and complete relaxation await you.</p>
</div>
```

```css
/* CSS */
.card-rgba {
  background-color: rgba(0, 0, 128, 0.4);   /* Blue background at 40% opacity */
                                              /* Text inside remains FULLY opaque */
  color: white;
  padding: 25px;
  width: 350px;
  border-radius: 8px;
}
```

**Expected Output:**
```
┌─────────────────────────────────────┐
│  Mountain Retreat                   │  ← Text is FULLY WHITE and SHARP
│  Escape to the mountains for a      │  ← Blue background is semi-transparent
│  peaceful weekend. Fresh air...     │  ← You can see THROUGH the blue box
└─────────────────────────────────────┘
```

> **Notice:** The text `Mountain Retreat` is crystal clear white. The blue background is semi-transparent. This is because `rgba()` only applies transparency to the colour value — NOT to the child elements inside.

---

### Example 6: Comparing `opacity` vs `rgba` Side by Side

This is the most instructive example in the whole lesson. Study it carefully.

```html
<!-- HTML: Two identical boxes, two different approaches -->
<h3>Method 1: Using opacity (text gets transparent too)</h3>
<div class="box-with-opacity">
  <p>This text is hard to read because opacity affects EVERYTHING inside.</p>
</div>

<h3>Method 2: Using rgba (only background is transparent)</h3>
<div class="box-with-rgba">
  <p>This text is perfectly readable because rgba only affects the background colour.</p>
</div>
```

```css
/* CSS */
.box-with-opacity {
  background-color: rgb(4, 170, 109);   /* A green colour */
  opacity: 0.3;                          /* Makes BOTH background AND text 30% opaque */
  padding: 20px;
  margin-bottom: 20px;
  color: black;
}

.box-with-rgba {
  background-color: rgba(4, 170, 109, 0.3);  /* Same green, but ONLY the background is 30% transparent */
  padding: 20px;
  color: black;                               /* Text remains fully opaque */
}
```

**Expected Output:**
```
Method 1 (opacity):
[ Very faint green box — text is barely legible ]
  "This text is hard to read..."  ← faint and hard to see

Method 2 (rgba):
[ Semi-transparent green box — text is sharp and clear ]
  "This text is perfectly readable..."  ← fully solid and readable
```

> **The takeaway:** Use `opacity` when you want the ENTIRE element (including text and all children) to be transparent. Use `rgba()` when you only want the background colour to be transparent while keeping the text inside fully readable.

---

## Section 6: Text Over an Image Using a Transparent Box

One of the most beautiful and practical uses of transparency is placing readable text over an image. The trick is to layer a semi-transparent box on top of the image and put the text inside that box.

### How to Layer Elements

To place one element visually on top of another, we use CSS `position`:
- The container gets `position: relative;` — it becomes the reference point
- The inner transparent box gets `position: absolute;` — it is placed relative to the container

This technique is used everywhere in professional web design — hero banners, product cards, image captions, and more.

---

### Example 7: Text Overlay Box on an Image (The Classic Design Pattern)

```html
<!-- HTML -->
<div class="image-container">
  <!-- The background image is set via CSS below -->
  <div class="overlay-box">
    <p>Welcome to the Jungle</p>
  </div>
</div>
```

```css
/* CSS */
.image-container {
  position: relative;               /* Reference point for the absolute box */
  width: 400px;
  height: 250px;
  background-image: url("jungle.jpg");
  background-size: cover;           /* Image fills the entire container */
  background-position: center;
  border: 3px solid #333;
}

.overlay-box {
  position: absolute;               /* Positioned relative to .image-container */
  bottom: 20px;                     /* 20px from the bottom of the container */
  left: 20px;                       /* 20px from the left edge */
  right: 20px;                      /* 20px from the right edge */
  background-color: rgba(0, 0, 0, 0.6);  /* Semi-transparent BLACK background */
  color: white;                     /* White text — fully opaque */
  padding: 15px;
  text-align: center;
  font-size: 1.2em;
}
```

**Expected Output (visual):**
```
┌──────────────────────────────────────────┐
│                                          │
│          [ Jungle photograph ]           │
│                                          │
│  ┌────────────────────────────────────┐  │
│  │     Welcome to the Jungle          │  │  ← text is white & clear
│  └────────────────────────────────────┘  │  ← box is semi-transparent black
└──────────────────────────────────────────┘
```

**Line-by-line breakdown:**
- `.image-container` — This outer div holds the background image. `position: relative` makes it the anchor for the overlay box.
- `background-image: url(...)` — Sets the jungle photo as the background.
- `background-size: cover` — Stretches the image to fill the container without distortion.
- `.overlay-box` — This is the transparent text panel layered over the image.
- `position: absolute` — Places this box relative to its parent (`.image-container`).
- `bottom: 20px; left: 20px; right: 20px;` — Positions the box near the bottom, with 20px gaps on three sides.
- `background-color: rgba(0, 0, 0, 0.6)` — Black background at 60% opacity. The image shows through slightly.
- `color: white` — The text is fully white and fully opaque. It stands out clearly.

> **Real-world use:** This exact pattern is used on virtually every modern website for hero sections, feature banners, blog article thumbnails, product cards, and event announcements. If you master this pattern, you can build professional-looking web components right now!

---

### Example 8: The Same Pattern with a Coloured Overlay

Instead of a black semi-transparent overlay, you can use any colour for different visual moods:

```css
/* Blue overlay — calm, professional */
.overlay-blue {
  background-color: rgba(0, 60, 180, 0.7);
  color: white;
}

/* Red overlay — urgent, exciting */
.overlay-red {
  background-color: rgba(200, 0, 0, 0.6);
  color: white;
}

/* Green overlay — nature, eco, health */
.overlay-green {
  background-color: rgba(0, 128, 0, 0.5);
  color: white;
}

/* White overlay — clean, minimal */
.overlay-white {
  background-color: rgba(255, 255, 255, 0.8);
  color: #333;    /* Dark text on white overlay */
}
```

> **Design tip:** The alpha value in your `rgba()` matters for readability. If the image is very busy/complex, use a higher alpha (like `0.7` or `0.8`) to ensure text stands out. If the image is simple with few colours, a lower alpha (like `0.4`) can look elegant and still be readable.

---

## Section 7: The CSS `opacity` Property Reference Summary

Here is a complete reference table for the `opacity` property:

| Property | `opacity` |
|----------|-----------|
| **What it does** | Controls how transparent/see-through an element is |
| **Applies to** | Any HTML element (images, divs, text, buttons, etc.) |
| **Value range** | `0.0` (fully transparent) to `1.0` (fully opaque) |
| **Default value** | `1` (fully opaque) |
| **Affects children?** | YES — all child elements inherit the same transparency |
| **Alternative** | `rgba()` for background-only transparency |

---

## Section 8: Guided Practice Exercises

### Exercise 1: Warm-Up — Basic Opacity Scale

**Objective:** Apply different opacity levels to a single image.

**Scenario:** You are building a photography portfolio page. You want to show a decorative row of the same image at five different fade levels.

**Steps:**
1. Create an HTML file with five `<img>` tags, all with the same `src`
2. Give them classes: `op-1`, `op-2`, `op-3`, `op-4`, `op-5`
3. Apply the following opacity values in your CSS:
   - `.op-1` → `opacity: 1.0`
   - `.op-2` → `opacity: 0.8`
   - `.op-3` → `opacity: 0.6`
   - `.op-4` → `opacity: 0.4`
   - `.op-5` → `opacity: 0.2`

**Starter code:**
```html
<!DOCTYPE html>
<html>
<head>
  <style>
    img { width: 120px; height: 90px; margin: 5px; }
    /* Add your opacity classes here */
  </style>
</head>
<body>
  <img src="landscape.jpg" alt="Landscape" class="op-1">
  <img src="landscape.jpg" alt="Landscape" class="op-2">
  <img src="landscape.jpg" alt="Landscape" class="op-3">
  <img src="landscape.jpg" alt="Landscape" class="op-4">
  <img src="landscape.jpg" alt="Landscape" class="op-5">
</body>
</html>
```

**Expected Output (visual):**
```
[ Full ] [ Slightly faded ] [ Half ] [ Very faded ] [ Almost invisible ]
```

**Self-check Questions:**
- Can you see the white page background showing through the more transparent images?
- Which image looks completely normal?
- Which image is almost invisible?
- What value would give you exactly 50% opacity?

---

### Exercise 2: Hover Reveal Effect

**Objective:** Make images go from semi-transparent to fully opaque on hover.

**Scenario:** You are creating a team members gallery. Each team member photo starts faded. When the user hovers over a photo, it becomes fully visible — as if the person is "stepping forward".

**Steps:**
1. Create a `<div class="team-gallery">` with three `<img>` elements inside
2. Style all images with `opacity: 0.4`, a fixed width and height, and a margin
3. Add an `img:hover` rule that sets `opacity: 1.0`

**Expected Output:**
```
[ Faded ] [ Faded ] [ Faded ]
   ↑ Hover over any image → it becomes fully clear
```

**What-If Challenge:** What if you added a `transition: opacity 0.3s ease;` to the `img` rule? Try it! Instead of the opacity snapping instantly, it would smoothly fade over 0.3 seconds — a much more polished effect!

```css
img {
  opacity: 0.4;
  transition: opacity 0.3s ease;  /* Smooth fade transition */
  width: 200px;
  height: 150px;
}

img:hover {
  opacity: 1.0;
}
```

---

### Exercise 3: The Opacity vs RGBA Comparison

**Objective:** Personally see the difference between `opacity` and `rgba()`.

**Scenario:** You are testing two different approaches to creating a semi-transparent card with a heading and paragraph inside.

**Step 1 — Create the first card using `opacity`:**
```html
<div class="card-opacity">
  <h3>Card with opacity</h3>
  <p>Can you read this text easily?</p>
</div>
```
```css
.card-opacity {
  background-color: darkblue;
  color: white;
  opacity: 0.4;
  padding: 20px;
  width: 300px;
  margin-bottom: 20px;
}
```

**Step 2 — Create the second card using `rgba()`:**
```html
<div class="card-rgba">
  <h3>Card with rgba</h3>
  <p>Can you read this text easily?</p>
</div>
```
```css
.card-rgba {
  background-color: rgba(0, 0, 139, 0.4);  /* Dark blue at 40% opacity */
  color: white;                              /* Text is FULLY opaque */
  padding: 20px;
  width: 300px;
}
```

**Expected Observation:**
- Card 1: Both the dark blue background and the white text are 40% transparent — the text is hard to read
- Card 2: Only the dark blue background is 40% transparent — the text is fully white and clearly readable

**Self-check Question:** Which card would you use if you wanted readable text? Why?

---

### Exercise 4: Build a Text-Over-Image Banner

**Objective:** Create a hero banner: an image with a semi-transparent overlay and large text.

**Scenario:** You are building a travel website header. It needs a scenic photo with a dark, semi-transparent banner at the bottom containing the destination name.

**Starter HTML:**
```html
<div class="hero-banner">
  <div class="hero-text">
    <h1>Discover Lagos</h1>
    <p>The heartbeat of West Africa awaits</p>
  </div>
</div>
```

**Your Task:** Write the CSS to:
1. Give `.hero-banner` a background image, a height of `350px`, and `position: relative`
2. Give `.hero-text` a `position: absolute`, place it at the bottom with `15px` of padding on all sides
3. Use `rgba(0, 0, 0, 0.65)` as the background colour of `.hero-text`
4. Make the text white

**Expected Output:**
```
┌─────────────────────────────────────────────┐
│                                             │
│         [ Scenic Lagos photo ]              │
│                                             │
│  ┌─────────────────────────────────────┐    │
│  │  Discover Lagos                     │    │
│  │  The heartbeat of West Africa...    │    │
│  └─────────────────────────────────────┘    │
└─────────────────────────────────────────────┘
```

---

## Section 9: Mini Project — Transparent Profile Card

In this project, you will build a visually attractive profile card that uses transparency to layer text over a background image. This is a pattern used all over the web in user profiles, author bios, and social media cards.

### Project: Social Media Profile Card

**What you will build:**
A card with a scenic cover photo, a semi-transparent author info bar at the bottom, and a profile name and role shown clearly on top of the transparent bar.

---

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Profile Card</title>
  <link rel="stylesheet" href="profile.css">
</head>
<body>

  <div class="profile-card">

    <!-- The cover photo is set as CSS background on .profile-card -->

    <!-- Semi-transparent info bar at the bottom -->
    <div class="profile-info">
      <h2 class="profile-name">Adaeze Okonkwo</h2>
      <p class="profile-role">Senior Frontend Developer</p>
      <p class="profile-location">Lagos, Nigeria</p>
    </div>

  </div>

</body>
</html>
```

---

### Stage 2 — CSS

```css
/* profile.css */

/* Reset */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #1a1a2e;
  font-family: 'Arial', sans-serif;
}

/* ---- Profile Card Container ---- */
.profile-card {
  position: relative;              /* Anchor for the absolute info bar */
  width: 360px;
  height: 280px;
  border-radius: 12px;
  overflow: hidden;                /* Clips the info bar to the card's rounded corners */
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.5);

  /* Cover photo as background */
  background-image: url("city-skyline.jpg");
  background-size: cover;
  background-position: center top;
}

/* ---- Semi-transparent Info Bar ---- */
.profile-info {
  position: absolute;              /* Placed relative to .profile-card */
  bottom: 0;                       /* Sticks to the BOTTOM of the card */
  left: 0;
  right: 0;

  background-color: rgba(10, 10, 30, 0.75);  /* Very dark navy, 75% opaque */
                                               /* Shows the photo slightly through the bar */
  color: white;
  padding: 16px 20px;
}

/* ---- Text Inside the Info Bar ---- */
.profile-name {
  font-size: 1.3em;
  font-weight: bold;
  margin-bottom: 4px;
  color: #ffffff;                  /* Fully white — fully opaque */
}

.profile-role {
  font-size: 0.9em;
  color: rgba(255, 255, 255, 0.85); /* Slightly transparent white for the role */
  margin-bottom: 2px;
}

.profile-location {
  font-size: 0.8em;
  color: rgba(255, 255, 255, 0.6);  /* More transparent white for less important info */
}
```

---

### Stage 3 — Milestone Output

When opened in a browser:

```
┌─────────────────────────────────────────┐
│                                         │
│      [ City Skyline Photograph ]        │
│                                         │
│                                         │
├─────────────────────────────────────────┤
│  Adaeze Okonkwo              ← white    │  ← Semi-transparent dark navy bar
│  Senior Frontend Developer   ← faint    │    You can still see the photo
│  Lagos, Nigeria              ← fainter  │    faintly through the bar
└─────────────────────────────────────────┘
```

---

### Stage 4 — Reflection Questions

1. Why did we use `rgba(10, 10, 30, 0.75)` instead of `opacity: 0.75` on `.profile-info`? What would have happened if we had used `opacity: 0.75`?
2. The `.profile-location` text uses `rgba(255, 255, 255, 0.6)`. What does this mean? Why is this text slightly more faded than the name?
3. What does `overflow: hidden` do on `.profile-card`? What would happen without it?
4. If you wanted the info bar to cover the TOP of the card instead of the bottom, which CSS property would you change?

### Optional Enhancements

- Add a circular profile avatar image positioned in the top-left corner of the card
- Add a hover effect: when you hover over the card, the info bar's opacity increases to `rgba(10, 10, 30, 0.92)` for better readability
- Add a gradient overlay on the image using `background: linear-gradient(...)` instead of the solid transparent box
- Create three profile cards side by side using a flex container

---

## Section 10: Common Beginner Mistakes

### Mistake 1: Using `opacity` When You Want Only the Background to Be Transparent

**The Problem:**
```css
/* WRONG — text will also become faded */
.info-box {
  background-color: blue;
  opacity: 0.3;    /* Text inside is also 30% opaque! */
  color: white;
}
```

**The Fix:**
```css
/* CORRECT — only the background is transparent, text stays fully opaque */
.info-box {
  background-color: rgba(0, 0, 255, 0.3);   /* Blue at 30% opacity */
  color: white;                              /* Fully opaque white text */
}
```

---

### Mistake 2: Using Opacity Values Greater Than 1

**The Problem:**
```css
/* WRONG — opacity: 1.5 is invalid! Maximum is 1.0 */
img {
  opacity: 1.5;   /* Browser ignores this or treats it as 1.0 */
}
```

**The Fix:**
```css
/* CORRECT — always use values between 0.0 and 1.0 */
img {
  opacity: 1.0;   /* Fully opaque */
}
```

---

### Mistake 3: Forgetting `position: relative` on the Container

When placing a transparent overlay box over an image, the container **must** have `position: relative`. Without it, the absolute-positioned overlay will be placed relative to the entire page, not just the image container.

**The Problem:**
```css
/* WRONG — no position set on container */
.image-container {
  width: 400px;
  height: 250px;
  background-image: url("photo.jpg");
  /* No position: relative! The overlay will escape to the page! */
}

.overlay {
  position: absolute;   /* This will position relative to the PAGE, not the container */
  bottom: 0;
}
```

**The Fix:**
```css
/* CORRECT */
.image-container {
  position: relative;    /* REQUIRED for the overlay to work correctly */
  width: 400px;
  height: 250px;
  background-image: url("photo.jpg");
}

.overlay {
  position: absolute;
  bottom: 0;             /* Now positions relative to .image-container */
}
```

---

### Mistake 4: Setting `opacity: 0` to Hide an Element When You Mean `display: none`

**The difference:**
- `opacity: 0` makes the element invisible BUT it still takes up space on the page. It is there — just see-through.
- `display: none` removes the element from the page completely — no space is reserved.

```css
/* opacity: 0 — element is invisible but STILL TAKES UP SPACE */
.invisible-but-there {
  opacity: 0;
}

/* display: none — element is completely GONE from layout */
.actually-hidden {
  display: none;
}
```

> Use `opacity: 0` when you want to animate an element fading in/out. Use `display: none` when you want the element to truly disappear from the layout.

---

### Mistake 5: Confusing the Alpha in rgba() with the `opacity` Property

Both control transparency, but they work differently:

| Feature | `opacity` property | `rgba()` alpha channel |
|---------|-------------------|----------------------|
| What becomes transparent | The ENTIRE element + all children | ONLY the colour value applied |
| Can children stay opaque? | No — they inherit opacity | Yes — only the background is affected |
| Where it is written | As a separate property | Inside the colour value |
| Example | `opacity: 0.5;` | `background: rgba(255, 0, 0, 0.5);` |

---

## Section 11: Reflection Questions

Test your understanding with these questions:

1. What does `opacity: 0` do to an element? What does `opacity: 1` do?
2. What is the difference between `opacity: 0.5` and `rgba(0, 0, 0, 0.5)` when used on a box with text inside?
3. If you set `opacity: 0.3` on a `<div>` that contains a `<p>` tag, what happens to the text in the `<p>` tag?
4. How would you make a bright red background that is 70% transparent while keeping white text inside fully readable?
5. What two things does a `:hover` selector do that make opacity effects interactive?
6. In the text-over-image pattern, why do we use `position: relative` on the container and `position: absolute` on the overlay?
7. What does the `A` in RGBA stand for? What is its value range?
8. You have an image with `opacity: 0.4`. On `:hover`, you want it to become fully opaque. Write the CSS rule.
9. What is the difference between `opacity: 0` and `display: none`?
10. Describe a real-world situation on a website where you would use a semi-transparent overlay on an image.

---

## Section 12: Completion Checklist

Use this checklist to confirm you have fully understood this lesson:

- [ ] I know what opacity and transparency mean and how they relate to each other
- [ ] I can use the `opacity` property with values from `0.0` to `1.0`
- [ ] I understand that `0.0` = fully transparent and `1.0` = fully opaque
- [ ] I can apply `opacity` to images to make them faded
- [ ] I can use `opacity` with `:hover` to create interactive fade effects
- [ ] I understand that `opacity` makes child elements (including text) transparent too
- [ ] I know how to use `rgba()` to make only a background colour transparent
- [ ] I can explain the difference between `opacity` and `rgba()` transparency
- [ ] I can build the text-over-image overlay pattern using `position: relative` and `position: absolute`
- [ ] I know when to use `opacity: 0` versus `display: none`
- [ ] I can identify and correct common opacity mistakes

---

## Lesson Summary

Excellent work completing this lesson! Here is a complete recap of everything you learned.

**The `opacity` property** controls how transparent an entire element is. Its values range from `0.0` (completely invisible) to `1.0` (completely solid). It is applied as a regular CSS property: `opacity: 0.5;`

**Opacity with `:hover`** creates interactive transparency effects. You can make images fade in on hover or fade out on hover by setting different opacity values in the normal state and the `:hover` state.

**The child inheritance problem:** When you apply `opacity` to an element, every child element (including text) also becomes the same level of transparent. This makes text inside transparent backgrounds very hard to read.

**The RGBA solution:** Instead of using `opacity` on the whole element, use `rgba()` as the background-color value. This makes only the background colour transparent, while all text and children inside remain fully opaque and readable.

```css
/* The RGBA formula */
background-color: rgba(red, green, blue, alpha);
/* alpha: 0.0 = invisible, 1.0 = fully solid */
```

**Text over image:** The professional pattern for placing text over a photo uses `position: relative` on the container, `position: absolute` on the overlay box, and `rgba()` for the overlay's semi-transparent background colour.

**Key decision guide:**
- Want the whole element (including text) transparent? → Use `opacity`
- Want only the background transparent while keeping text readable? → Use `rgba()`
- Want an element invisible but still taking up space? → Use `opacity: 0`
- Want an element completely gone from the layout? → Use `display: none`

> **What comes next?** Now that you can control transparency, you are ready to explore more advanced visual effects in CSS — including CSS transitions (smooth animated changes), CSS filters (blur, grayscale, contrast), and CSS pseudo-elements for creative hover overlays!

---

*Lesson 31 Complete — CSS Opacity and Transparency*
