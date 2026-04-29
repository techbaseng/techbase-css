---
render_with_liquid: false
title: "CSS Advanced Backgrounds"
nav_order: 48
---

# Lesson 48 — CSS Advanced Backgrounds

---

## Lesson Introduction

In an earlier lesson you learned the CSS background basics: setting a background colour, adding a single background image, controlling whether it repeats, and how it scrolls. Those fundamentals are essential — but modern web design demands much more.

What if you need two different images layered on top of each other in the same element? What if you want a hero banner image that always fills the entire screen, no matter the screen size? What if you need the background to paint only inside the text itself, or only under the padding area, not under the border? All of this is possible with the four CSS3 background features you will master in this lesson:

- **Multiple Backgrounds** — stacking several images on one element
- **`background-size`** — controlling exactly how large a background image is drawn
- **`background-origin`** — choosing which box model zone the background starts from
- **`background-clip`** — choosing how far the background is allowed to paint

These four features work together and are used constantly in professional web development. By the end of this lesson you will be able to use all of them confidently, individually and in combination.

---

## Prerequisite Concepts

### The CSS Box Model Zones

Every HTML element is made up of four nested rectangular zones, from inside to outside:

```
┌─────────────────────────────────┐
│           BORDER                │
│   ┌─────────────────────────┐   │
│   │        PADDING          │   │
│   │   ┌─────────────────┐   │   │
│   │   │    CONTENT      │   │   │
│   │   └─────────────────┘   │   │
│   └─────────────────────────┘   │
└─────────────────────────────────┘
  (outside the border = MARGIN)
```

- **Content box** — where your text or child elements live
- **Padding box** — the transparent space between content and border
- **Border box** — the border line(s) drawn around padding + content
- **Margin** — invisible space outside the border (not part of the element's background)

The properties `background-origin` and `background-clip` both reference these three zones by name: `content-box`, `padding-box`, and `border-box`. Knowing these terms is essential for this lesson.

### What is `background-image`?

You set a background image with:

```css
div {
  background-image: url(photo.jpg);
}
```

By default, this image tiles (repeats) to fill the entire element. You can stop tiling with `background-repeat: no-repeat;`.

### What is `url()` in CSS?

`url()` is a CSS function that points to an image file:

```css
url(myimage.png)                   /* same folder */
url(images/myimage.png)            /* subfolder */
url(https://example.com/img.png)   /* external URL */
```

---

## Part 1 — Multiple Backgrounds

### What Are Multiple Backgrounds and Why Do They Exist?

Before CSS3, if you wanted two images layered on the same element, you had to nest two separate HTML elements, each with one background. That made HTML messy and hard to maintain.

CSS3 introduced **multiple backgrounds**: the ability to assign more than one `background-image` to a single element, all stacked on top of each other like layers in a photo editing app.

Think of it like a stack of transparent slides. The first slide you name in your CSS goes on top. The last slide goes at the bottom. If any slide has transparent areas, the ones below it show through.

**Real-world uses:**
- A texture overlay on top of a photo (e.g., a dark vignette over a hero image)
- A logo watermark placed in a corner over a gradient background
- A decorative pattern on top of a solid colour
- Game UI panels with multiple layered decorative elements

### How to Add Multiple Backgrounds

Simply list multiple `url()` values in `background-image`, separated by **commas**:

```css
selector {
  background-image: url(top-layer.png), url(bottom-layer.png);
}
```

**Stacking order rule:** The **first** image listed is on top (closest to the viewer). The **last** image listed is at the bottom.

### Simple Example 1 — Two Images Layered

```css
#box {
  background-image: url(img_flwr.gif), url(paper.gif);
  background-position: right bottom, left top;
  background-repeat: no-repeat, repeat;
  width: 400px;
  height: 300px;
}
```

**Expected visual output:**
A 400×300 box. `paper.gif` tiles across the entire background (bottom layer). On top of it, `img_flwr.gif` is placed once in the bottom-right corner and does not repeat (top layer).

**Line-by-line breakdown:**
- `url(img_flwr.gif), url(paper.gif)` — two images; flower is on top, paper is the base
- `background-position: right bottom, left top` — positions match image order: flower → right bottom, paper → left top
- `background-repeat: no-repeat, repeat` — repeat settings match order: flower → no repeat, paper → repeat

> **The comma rule is critical.** Each comma-separated value corresponds to the image at the same position. First value → first image, second value → second image, and so on. If you only give one value for `background-repeat` but have two images, the single value applies to both.

### Simple Example 2 — Background Shorthand with Multiple Backgrounds

You can also use the `background` shorthand property for each layer, separating layers with commas. The bottom layer (last one) can include a background colour:

```css
#box {
  background:
    url(img_flwr.gif) right bottom no-repeat,
    url(paper.gif) left top repeat;
}
```

**Expected visual output:** Identical to Example 1. The shorthand packs position and repeat together per layer.

### Simple Example 3 — Image Over a Colour

You can mix an image layer with a plain colour as the final (bottom) layer:

```css
#box {
  background:
    url(logo.png) center no-repeat,
    #f0e8d0;
}
```

**Expected visual output:** The box has a warm beige (#f0e8d0) background. The logo image is centred on top of it without repeating.

> **Thinking prompt:** What happens if the logo has no transparent areas? The colour would be completely hidden behind the logo. What if the logo is a PNG with transparency? The beige would show through the transparent parts.

---

## Part 2 — `background-size`

### What is `background-size` and Why Does It Exist?

By default, a background image is displayed at its natural (original) size. If you have a 200×200 pixel image and a 600×400 element, the image tiles to fill it — showing nine copies. But what if you want just one copy, perfectly scaled to fill the whole element?

`background-size` solves this. It lets you control exactly how large the background image is drawn, regardless of its natural dimensions.

**Real-world uses:**
- Hero banners that always fill the full screen width
- Profile picture backgrounds that scale with their container
- Texture overlays sized precisely to match an element
- Retina-display images: using a 2× resolution image displayed at half size for sharpness

### Syntax

```css
background-size: value;
```

Values can be:
- **A length** — e.g., `200px`, `10em` — sets exact width (height auto-scales)
- **Two lengths** — e.g., `200px 100px` — sets exact width then height
- **A percentage** — e.g., `50%` — relative to the element's width (height auto-scales)
- **`auto`** — uses the image's natural size (the default)
- **`cover`** — scales the image as small as possible while still covering the entire element (may crop)
- **`contain`** — scales the image as large as possible while keeping the whole image visible (may leave gaps)

### Understanding `cover` vs `contain`

These two keyword values are the most important and most commonly used:

**`cover` analogy:** Imagine stretching a photo on a canvas and trimming the edges to fit perfectly. The photo always fills the canvas completely — no gaps — but some parts may be cut off.

**`contain` analogy:** Imagine shrinking a photo until the whole thing fits inside a frame without cropping anything. The entire photo is always visible — but there may be empty space around the edges.

### Simple Example 1 — Fixed Pixel Size

```css
#box {
  background-image: url(img_flwr.gif);
  background-size: 80px 60px;
  background-repeat: repeat;
  width: 400px;
  height: 300px;
}
```

**Expected visual output:** The flower image is drawn at 80px wide × 60px tall and then tiles to fill the 400×300 box.

### Simple Example 2 — `cover`

```css
#hero {
  background-image: url(mountain.jpg);
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  width: 100%;
  height: 400px;
}
```

**Expected visual output:** The mountain photo covers the entire 400px-tall hero section. The image is centred and may be cropped on the sides or top/bottom to ensure no empty space.

### Simple Example 3 — `contain`

```css
#preview {
  background-image: url(logo.png);
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  width: 300px;
  height: 200px;
}
```

**Expected visual output:** The logo is scaled down (or up) until it fully fits inside the 300×200 box. The entire logo is always visible. If the logo's proportions don't match the box's proportions, there will be empty space on two sides.

### Simple Example 4 — Percentage Size

```css
#box {
  background-image: url(flower.png);
  background-size: 50%;
  background-repeat: no-repeat;
  width: 400px;
  height: 300px;
}
```

**Expected visual output:** The flower image is scaled to 50% of the element's width (200px). Height is calculated automatically to maintain the image's natural proportions.

> **Thinking prompt:** If the element is 400px wide and you set `background-size: 50%`, the image becomes 200px wide. If the element is later resized to 800px (e.g., on a wider screen), what happens to the image? It becomes 400px wide — because 50% of 800px is 400px. This is why percentages are useful for responsive designs.

### Multiple Background Sizes

When you have multiple background images, you give comma-separated sizes:

```css
#box {
  background-image: url(star.png), url(texture.jpg);
  background-size: 30px 30px, cover;
  background-repeat: no-repeat, no-repeat;
}
```

**Expected visual output:** The star is 30×30px. The texture covers the entire element behind it.

---

## Part 3 — `background-origin`

### What is `background-origin` and Why Does It Exist?

When you set a background image, where does the browser start drawing it from? By default, the background starts from the top-left corner of the **padding box** (the area that includes the padding, but is inside the border). This is usually what you want — but sometimes you want different behaviour.

`background-origin` lets you choose which box model zone defines the **starting point** (also called the "origin") for the background image's positioning grid.

**In simple terms:** It answers the question: "When I say `background-position: left top`, where exactly is 'left top'?"

**Real-world uses:**
- Precisely aligning a background image relative to the content area (ignoring padding)
- Making a background start from inside the border (border-box origin)
- Fine-grained control in complex card and UI panel designs

### Syntax

```css
background-origin: value;
```

**Three possible values:**

| Value | Meaning |
|-------|---------|
| `padding-box` | Background positions relative to the padding edge (this is the **default**) |
| `border-box` | Background positions relative to the border edge (image can appear under the border) |
| `content-box` | Background positions relative to the content edge (image starts at the content, after the padding) |

### Visual Analogy

Imagine painting a wall mural. `background-origin` decides *where you put your tape measure to start measuring*:
- `padding-box` → measure from the inside of the wall frame (including the skirting board / padding)
- `border-box` → measure from the very outer edge of the wall frame (including the border itself)
- `content-box` → measure from the inner glass/canvas (only the content area)

### Simple Example 1 — `padding-box` (Default)

```css
#box {
  border: 10px dashed black;
  padding: 25px;
  background-image: url(flower.gif);
  background-repeat: no-repeat;
  background-origin: padding-box; /* this is the default */
}
```

**Expected visual output:** The flower image starts at the top-left corner of the padding area — right inside the border. The border itself has no background image underneath it.

### Simple Example 2 — `content-box`

```css
#box {
  border: 10px dashed black;
  padding: 25px;
  background-image: url(flower.gif);
  background-repeat: no-repeat;
  background-origin: content-box;
}
```

**Expected visual output:** The flower image starts at the top-left corner of the *content* area — 25px further in from where it was in the previous example. The padding zone has no background image in it.

> **Thinking prompt:** If padding is 0, does `padding-box` and `content-box` produce the same result? Yes! When there is no padding, the padding edge and the content edge are at the same position.

### Simple Example 3 — `border-box`

```css
#box {
  border: 10px dashed black;
  padding: 25px;
  background-image: url(flower.gif);
  background-repeat: no-repeat;
  background-origin: border-box;
}
```

**Expected visual output:** The flower image starts at the very outer edge of the border. Part of the image will appear underneath the border lines.

### Comparing All Three Origins Side-by-Side

```css
/* All three boxes have the same border, padding, and image */

#a { background-origin: border-box; }   /* starts at border edge */
#b { background-origin: padding-box; }  /* starts at padding edge (default) */
#c { background-origin: content-box; }  /* starts at content edge */
```

The flower image shifts further inward as you go from `border-box` → `padding-box` → `content-box`.

---

## Part 4 — `background-clip`

### What is `background-clip` and Why Does It Exist?

While `background-origin` controls where a background *starts*, `background-clip` controls where the background is *allowed to paint*. It clips (cuts off) the background at a specific boundary.

Think of `background-clip` as a cookie cutter: you pour the background (dough) over the element, then the cookie cutter cuts away everything outside the chosen boundary.

**Real-world uses:**
- Preventing a background colour from showing under a thick border
- Creating a "text fill" effect where the background image is visible only through the text characters
- Designing cards where only the content zone gets a background colour

### Syntax

```css
background-clip: value;
```

**Values:**

| Value | Meaning |
|-------|---------|
| `border-box` | Background paints under the border, padding, and content — this is the **default** |
| `padding-box` | Background paints under padding and content only — clipped at the border edge |
| `content-box` | Background paints only in the content area — clipped at the padding edge |
| `text` | Background is clipped to the shape of the text (requires `-webkit-` prefix in some browsers) |

### Simple Example 1 — `border-box` (Default Behaviour)

```css
#box {
  background-color: yellow;
  border: 10px dotted black;
  padding: 20px;
  background-clip: border-box; /* default */
}
```

**Expected visual output:** Yellow background fills the entire element including under the dotted border. The dotted border has yellow showing through its gaps.

### Simple Example 2 — `padding-box`

```css
#box {
  background-color: yellow;
  border: 10px dotted black;
  padding: 20px;
  background-clip: padding-box;
}
```

**Expected visual output:** Yellow background fills padding and content, but stops at the border. The gaps in the dotted border now show the *page background* (white or whatever the parent background is), not yellow. The border now visually "frames" the yellow area.

### Simple Example 3 — `content-box`

```css
#box {
  background-color: yellow;
  border: 10px dotted black;
  padding: 20px;
  background-clip: content-box;
}
```

**Expected visual output:** Yellow background appears only inside the content area. The padding area (20px all around) shows the page background. The border area also shows the page background. The element has a yellow rectangle at the very centre surrounded by visible transparent padding.

### Comparing All Three Clip Values Side-by-Side

```css
#clip-border  { background-clip: border-box; }   /* yellow extends to edge of border */
#clip-padding { background-clip: padding-box; }  /* yellow stops at inner border edge */
#clip-content { background-clip: content-box; }  /* yellow only in content zone */
```

The yellow region shrinks inward as you go from `border-box` → `padding-box` → `content-box`.

### The Special `text` Value

The `text` value clips the background to the shape of the element's text characters. This creates the popular "gradient text" or "image text fill" effect:

```css
h1 {
  background-image: linear-gradient(to right, #ff6b6b, #ffd93d);
  background-clip: text;
  -webkit-background-clip: text;  /* required for Chrome/Safari */
  color: transparent;             /* make text colour transparent so background shows */
  font-size: 60px;
  font-weight: bold;
}
```

**Expected visual output:** The heading text is filled with a gradient from red-orange to yellow. The text looks as if it was painted with a gradient brush. No background appears outside the text characters.

**Why `color: transparent`?** The text colour normally sits on top of the background. If the text is opaque (e.g., black), it covers the background. Setting `color: transparent` makes the text itself invisible, so only the background (clipped to the text shape) is visible.

> **Browser note:** The `text` value requires the `-webkit-background-clip: text;` vendor prefix for Chrome and Safari. Always include both the prefixed and unprefixed versions.

---

## Combined Concepts: How They Work Together

`background-origin` and `background-clip` are often confused because they both reference the same three box zones. Here is the critical distinction:

| Property | Controls |
|----------|---------|
| `background-origin` | Where the background *positioning grid starts* (where is the 0,0 point?) |
| `background-clip` | Where the background is *allowed to paint* (what area gets filled?) |

**A useful analogy:** Think of hanging wallpaper.
- `background-origin` is where you put your pencil mark to start measuring from (top-left of padding? top-left of content?).
- `background-clip` is how far the wallpaper is allowed to go — does it go under the door frame (border), stop at the door frame (padding), or only go on the main wall section (content)?

### Example — Different `origin` and `clip`

```css
#box {
  background-image: url(flower.gif);
  background-repeat: no-repeat;
  background-origin: content-box;  /* position starts from content zone */
  background-clip: padding-box;    /* but paint is allowed into padding zone */
  border: 10px solid black;
  padding: 30px;
}
```

**Expected visual output:** The flower image is *positioned* as if starting from the top-left of the content zone, but its pixels are *visible* as far out as the padding edge. If the flower is large enough, it can overflow into the padding area, but it is clipped there — it will not paint under the border.

---

## Complete Properties Reference

### Multiple Backgrounds Summary

```css
/* Syntax: list images separated by commas */
background-image: url(top.png), url(middle.png), url(bottom.png);

/* Each property can have comma-separated values matching image order */
background-position: center top, left bottom, right center;
background-repeat: no-repeat, repeat-x, repeat;
background-size: contain, 50px, cover;
```

### `background-size` Values

| Value | Effect |
|-------|--------|
| `auto` | Natural image size (default) |
| `cover` | Scale to cover element fully; may crop image |
| `contain` | Scale to fit fully inside element; may leave gaps |
| `100px` | Fixed 100px width; height auto-scaled |
| `100px 80px` | Fixed 100px × 80px |
| `50%` | 50% of element width; height auto-scaled |
| `50% 25%` | 50% width, 25% height |

### `background-origin` Values

| Value | Starting point for positioning |
|-------|-------------------------------|
| `border-box` | Outer edge of the border |
| `padding-box` | Inner edge of the border (outer edge of padding) — **default** |
| `content-box` | Outer edge of the content (inner edge of padding) |

### `background-clip` Values

| Value | Background paints in… |
|-------|----------------------|
| `border-box` | Border + padding + content — **default** |
| `padding-box` | Padding + content only |
| `content-box` | Content only |
| `text` | Text character shapes only |

---

## Simple Standalone Examples

### Example A — Full-Page Hero with `cover`

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      margin: 0;
    }

    .hero {
      background-image: url(landscape.jpg);
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
      height: 100vh;        /* 100% of the viewport height */
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .hero h1 {
      color: white;
      font-size: 48px;
    }
  </style>
</head>
<body>
  <div class="hero">
    <h1>Welcome</h1>
  </div>
</body>
</html>
```

**Expected visual output:** A full-browser-height section with a landscape photo that always fills the entire viewport. "Welcome" is centred over it in white text. If you resize the browser, the photo always covers the area — cropping as needed.

---

### Example B — Layered Background: Texture Over Colour

```css
.card {
  background-image: url(noise-texture.png), linear-gradient(135deg, #667eea, #764ba2);
  background-repeat: repeat, no-repeat;
  background-size: auto, cover;
  padding: 30px;
  color: white;
}
```

**Expected visual output:** A card with a purple-to-indigo gradient as the base layer. A subtle noise texture tiles over the top, giving the surface a slightly grainy, tactile feel. Text appears in white.

---

### Example C — Gradient Text with `background-clip: text`

```html
<style>
  .gradient-title {
    font-size: 72px;
    font-weight: 900;
    background-image: linear-gradient(to right, #f093fb, #f5576c);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    display: inline-block;
  }
</style>

<h1 class="gradient-title">Hello World</h1>
```

**Expected visual output:** "Hello World" rendered in bold text where each letter is filled with a pink-to-red gradient. The background is transparent outside the letters.

> **Why `display: inline-block`?** By default, `<h1>` is a block element that stretches the full width. With `inline-block`, the element shrinks to fit the text. Without this, the gradient could appear in an unexpectedly wide area.

---

### Example D — `background-clip: padding-box` with a Visible Border

```css
.box {
  background-color: #3498db;
  border: 8px double white;
  padding: 20px;
  background-clip: padding-box;
  color: white;
  font-size: 18px;
}
```

**Expected visual output:** A blue box with a white double border. Because `background-clip: padding-box` is set, the blue colour stops exactly at the inner edge of the border. The border itself appears cleanly white, with no blue bleeding through. The double border lines are crisp white on a non-blue background.

---

## Guided Practice Exercises

### Exercise 1 — Multiple Backgrounds Warm-Up

**Objective:** Stack two background images on one element.

**Scenario:** You are building a weather widget. You want a cloud image floating over a sky-gradient background.

**Steps:**
1. Create a `<div>` with class `weather-widget`, 300px wide and 200px tall.
2. Apply two backgrounds:
   - First (top): `cloud.png`, positioned top-right, no-repeat
   - Second (bottom): a linear gradient from `#87CEEB` (sky blue) to `#ffffff` (white)

```css
.weather-widget {
  width: 300px;
  height: 200px;
  background-image: url(cloud.png), linear-gradient(to bottom, #87CEEB, #ffffff);
  background-position: top right, center;
  background-repeat: no-repeat, no-repeat;
}
```

**Expected output:** A blue-to-white gradient sky. A cloud image sits in the top-right corner.

**Self-check questions:**
- What happens if you reverse the order of the two backgrounds? (The gradient covers the cloud entirely — order matters!)
- What if you change `top right` to `center`? (The cloud moves to the centre of the widget.)
- What if you add `background-size: 80px, cover` to the rule? (The cloud becomes 80px wide; the gradient covers the full element.)

---

### Exercise 2 — Responsive Banner with `background-size: cover`

**Objective:** Build a responsive hero banner.

**Scenario:** You are building a landing page for a coffee shop. The hero image must always fill the full width of the page without distorting.

**Steps:**
1. Create a `<section>` with class `hero`.
2. Set its height to `80vh` (80% of the viewport height).
3. Apply a background image with `cover` and centred position.
4. Add a semi-transparent overlay effect by adding a second background layer: `linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.4))` as the first layer (on top).

```css
.hero {
  background-image:
    linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.4)),
    url(coffee-shop.jpg);
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  height: 80vh;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 36px;
}
```

**Expected output:** The coffee shop photo fills the entire section. A semi-transparent dark overlay sits on top, making text readable. "Our Coffee" (or similar text) appears centred in white.

**What-if challenge:** Change `rgba(0,0,0,0.4)` to `rgba(0,0,0,0.8)`. What happens? (The overlay becomes much darker, the photo is barely visible.)

---

### Exercise 3 — Comparing `background-origin` Values

**Objective:** See visually how `background-origin` moves the image starting point.

**Scenario:** You are documenting CSS box model concepts and need three demonstration boxes.

**Steps:** Create three identical `<div>` elements except for their `background-origin` value:

```css
/* Shared styles */
.demo {
  border: 15px solid rgba(0, 0, 0, 0.3);
  padding: 30px;
  background-image: url(flower.gif);
  background-repeat: no-repeat;
  width: 200px;
  height: 150px;
  margin: 10px;
  display: inline-block;
}

.origin-border  { background-origin: border-box; }
.origin-padding { background-origin: padding-box; }
.origin-content { background-origin: content-box; }
```

**Expected output:** Three boxes side by side. In the first, the flower starts at the outermost border edge. In the second, it starts at the inner border edge (padding zone start). In the third, it starts at the content zone start — shifted furthest inward.

**Self-check questions:**
- In which box is the flower furthest to the top-left? (`border-box` — it starts from the absolute outer edge)
- What would happen if padding were 0? (`padding-box` and `content-box` would look identical)

---

### Exercise 4 — `background-clip` Colour Boundaries

**Objective:** Understand how `background-clip` affects where a background colour is painted.

**Scenario:** You are designing a tooltip component with a thick, visible border. You want the background colour to stop at the border edge so the border looks clean.

```css
/* Shared base */
.tooltip {
  background-color: #fff3cd;
  border: 6px solid #856404;
  padding: 15px;
  font-size: 14px;
  width: 200px;
  margin: 10px;
  display: inline-block;
}

.clip-border  { background-clip: border-box; }   /* yellow under the border too */
.clip-padding { background-clip: padding-box; }  /* yellow stops at border inside */
.clip-content { background-clip: content-box; }  /* yellow only in content zone */
```

**Expected output:** Three tooltip boxes. The first has the yellow colour filling behind the border. The second has yellow only inside the border (clean separation). The third has yellow only in the text area, with transparent padding visible.

**What-if challenge:** Set `border` to `8px dashed #856404`. Now look at `border-box` vs `padding-box`. In `border-box`, yellow shows through the dashes. In `padding-box`, the page background shows through the dashes. Which looks better? (Usually `padding-box` produces a cleaner, more professional look with dashed borders.)

---

### Exercise 5 — Gradient Text Effect

**Objective:** Apply `background-clip: text` to create a gradient-filled heading.

**Steps:**
1. Add an `<h1>` to your page with your name or any text.
2. Apply these styles:

```css
h1.gradient-text {
  font-size: 64px;
  font-weight: 900;
  background-image: linear-gradient(90deg, #11998e, #38ef7d);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  display: inline-block;
  margin: 0;
}
```

**Expected output:** Your heading text fills with a teal-to-green gradient. Nothing outside the letters is coloured.

**What-if experiments:**
- Change the gradient direction to `180deg` (top to bottom). How does it look?
- Change it to `radial-gradient(circle, #ff9a9e, #fad0c4)` for a radial fill.
- Add a second `<p>` element with `background-clip: text`. Does it work on smaller body text?

---

## Mini-Project: Layered Hero Card

### Project Overview

You will build a stylish **hero card** component — the kind used as an introduction section on a personal website or portfolio — that uses all four advanced background features from this lesson.

**Features to include:**
- A background photo behind a gradient overlay (multiple backgrounds)
- `background-size: cover` so the photo always fills the card
- A second inner card element using `background-clip: padding-box` for a clean border
- A heading using `background-clip: text` with a gradient fill

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Hero Card</title>
  <link rel="stylesheet" href="hero-card.css">
</head>
<body>

  <div class="hero-card">
    <div class="inner-panel">
      <h1 class="gradient-name">Taylor Smith</h1>
      <p class="tagline">Web Designer & Developer</p>
      <p class="bio">
        I build clean, accessible, and beautiful web experiences
        from scratch. Let's create something great together.
      </p>
    </div>
  </div>

</body>
</html>
```

**Milestone output:** Raw HTML, unstyled. Text visible on white background.

---

### Stage 2 — Hero Card: Multiple Backgrounds + `cover`

```css
/* hero-card.css */

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #1a1a2e;
}

.hero-card {
  width: 500px;
  height: 350px;
  border-radius: 16px;
  overflow: hidden;

  /* Multiple backgrounds: dark gradient overlay on top of photo */
  background-image:
    linear-gradient(135deg, rgba(17, 153, 142, 0.6), rgba(56, 239, 125, 0.3)),
    url(portrait.jpg);

  /* background-size: cover for the photo layer */
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;

  display: flex;
  align-items: center;
  justify-content: center;
  padding: 30px;
}
```

**Milestone output:** A card with a portrait photo covered by a teal-green gradient overlay. Content is centred.

---

### Stage 3 — Inner Panel with `background-clip`

```css
.inner-panel {
  background-color: rgba(255, 255, 255, 0.15);
  border: 2px solid rgba(255, 255, 255, 0.4);
  border-radius: 12px;
  padding: 24px 32px;
  text-align: center;
  color: white;

  /* background stops at the border — doesn't paint under it */
  background-clip: padding-box;
}
```

**Milestone output:** The card now has a frosted-glass inner panel. The semi-transparent white background fills exactly to the border edge — the border itself is transparent/white, not tinted.

---

### Stage 4 — Gradient Name with `background-clip: text`

```css
.gradient-name {
  font-size: 36px;
  font-weight: 900;
  background-image: linear-gradient(to right, #ffffff, #38ef7d);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  display: inline-block;
  margin-bottom: 6px;
}

.tagline {
  font-size: 13px;
  text-transform: uppercase;
  letter-spacing: 2px;
  color: rgba(255, 255, 255, 0.7);
  margin-bottom: 16px;
}

.bio {
  font-size: 14px;
  line-height: 1.7;
  color: rgba(255, 255, 255, 0.85);
}
```

**Final milestone output:** A polished hero card. The name is filled with a white-to-green gradient. The tagline is subtle uppercase text. The bio is readable on the frosted-glass panel. The photo and teal overlay create a professional backdrop.

---

### Stage 5 — Optional Enhancement: `background-origin`

Add a subtle corner logo or watermark that positions precisely from the content zone:

```css
.inner-panel {
  /* ... previous styles ... */
  background-image: url(small-logo.png);
  background-repeat: no-repeat;
  background-position: right bottom;
  background-origin: content-box;  /* logo aligns to content, not padding edge */
  background-size: 40px;
}
```

**Milestone output:** A small 40px logo sits in the bottom-right of the inner panel's content area.

---

### Reflection Questions for the Mini-Project

- Why was `background-size: cover` important for the hero card? (Without it, the portrait photo would tile at its natural size instead of filling the card.)
- How does the gradient overlay in the multiple background setup improve readability? (It darkens or tints the photo, making white text easier to read.)
- What would happen to the inner panel if you changed `background-clip: padding-box` to `background-clip: border-box`? (The semi-transparent white would fill behind the border too, slightly changing its appearance — the border would blend into the panel background.)
- Why does the gradient name require `color: transparent`? (Without it, the text colour (usually black) sits on top of the background and hides the gradient completely.)
- Can you apply `background-size: cover` and `background-clip: content-box` to the same element? Yes — `background-size` controls *how large* the image is drawn; `background-clip` controls *where* it is visible. They are independent.

---

## Common Beginner Mistakes

### Mistake 1 — Wrong Order in Multiple Backgrounds

```css
/* ❌ Gradient covers the photo — wrong stack order */
background-image:
  url(photo.jpg),
  linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5));
```

```css
/* ✅ Gradient overlay on top, photo beneath */
background-image:
  linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
  url(photo.jpg);
```

**Why:** The first listed layer is on top. A fully opaque image listed first will cover everything below it.

---

### Mistake 2 — Mismatched Comma-Separated Values

```css
/* ❌ Two images, but only one background-position value */
background-image: url(star.png), url(sky.jpg);
background-position: top right;  /* only applies clearly to the first */
```

```css
/* ✅ One value per image */
background-image: url(star.png), url(sky.jpg);
background-position: top right, center center;
```

**Why:** When you have multiple background images, each background property (`background-position`, `background-repeat`, `background-size`) should have the same number of comma-separated values. If you provide fewer values, the browser cycles through them — which can cause unexpected results.

---

### Mistake 3 — Forgetting `color: transparent` for `background-clip: text`

```css
/* ❌ Text colour hides the gradient */
h1 {
  background-image: linear-gradient(to right, red, blue);
  background-clip: text;
  -webkit-background-clip: text;
  /* color is black by default — gradient invisible */
}
```

```css
/* ✅ Set text colour to transparent to reveal the clipped background */
h1 {
  background-image: linear-gradient(to right, red, blue);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
```

---

### Mistake 4 — Forgetting the `-webkit-` Prefix for `background-clip: text`

```css
/* ❌ May not work in Chrome/Safari */
h1 {
  background-clip: text;
  color: transparent;
}
```

```css
/* ✅ Always include the prefixed version too */
h1 {
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
```

---

### Mistake 5 — Confusing `background-origin` with `background-clip`

These two are the most commonly confused:
- `background-origin` → sets the **coordinate origin** (where does the 0,0 point start for positioning?)
- `background-clip` → sets the **paint boundary** (how far does the paint go?)

They use the same three keyword values (`border-box`, `padding-box`, `content-box`) but control completely different aspects. Remember: **origin = start point, clip = stop point**.

---

### Mistake 6 — Using `background-size: cover` Without Setting `background-repeat: no-repeat`

```css
/* ❌ The image scales to cover, but then also tiles — unexpected results */
.hero {
  background-image: url(photo.jpg);
  background-size: cover;
}
```

```css
/* ✅ When using cover, always turn off repeat */
.hero {
  background-image: url(photo.jpg);
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
}
```

**Why:** `background-size: cover` scales the image to fill the element. If `background-repeat` is still `repeat` (the default), the browser will then tile the already-large image if the calculation results in space. In practice with `cover` this is rare, but it is a good habit to always explicitly set `no-repeat` with `cover` or `contain`.

---

### Mistake 7 — Using `background-size: contain` and Wondering Why There Are Gaps

```css
/* This is working correctly — but beginners are often surprised by gaps */
.box {
  background-image: url(logo.png);
  background-size: contain;
  background-repeat: no-repeat;
  width: 400px;
  height: 300px;
}
```

If `logo.png` is a wide horizontal image, it will fill the 400px width but the height will be less than 300px — leaving empty space at the bottom. This is by design — `contain` always keeps the entire image visible without cropping. If you want no gaps and are OK with cropping, use `cover`.

---

## Reflection Questions

1. You have a div with `background-image: url(a.png), url(b.png)`. Which image appears on top? (`a.png` — the first listed image is the top layer.)

2. What is the difference between `background-size: cover` and `background-size: 100%`? (`cover` maintains proportions and covers the entire element (may crop). `100%` makes the image exactly the element's width, and the height auto-scales — which may leave vertical gaps.)

3. If you set `background-clip: content-box` and there is no padding, where does the background paint? (Everywhere — because with no padding, content-box and border-box are the same size.)

4. Can you apply `background-origin: content-box` and `background-clip: border-box` at the same time? Yes. The image positions from the content edge, but it paints all the way to the border edge.

5. Why might a designer use `background-clip: text` on a heading instead of just colouring the text with `color`? (Because `color` can only be a flat colour or `currentColor`. `background-clip: text` allows gradients, images, and patterns to fill the text — something impossible with `color` alone.)

6. You have three background images and only two `background-size` values. What does the browser do with the third image? (The browser cycles through the given values — the third image gets the first size value.)

---

## Completion Checklist

Before moving on, confirm you can do each of the following:

- [ ] Add two or more background images to one element using comma separation
- [ ] Explain the stacking order rule for multiple backgrounds (first listed = on top)
- [ ] Set `background-size` using pixels, percentages, `cover`, and `contain`
- [ ] Explain the difference between `cover` and `contain` without looking at notes
- [ ] Use `background-origin` with all three values and explain what changes
- [ ] Use `background-clip` with all three box-model values and explain what changes
- [ ] Explain the difference between `background-origin` and `background-clip`
- [ ] Create a gradient-filled text effect using `background-clip: text` and `color: transparent`
- [ ] Avoid all seven common mistakes described in this lesson
- [ ] Complete the hero card mini-project combining all four features

---

## Lesson Summary

This lesson introduced four powerful CSS3 background features that dramatically expand what you can do with element backgrounds.

**Multiple Backgrounds** let you stack any number of images or gradients on one element using comma-separated `background-image` values. The first value is always on top. All related background properties (`position`, `repeat`, `size`) accept matching comma-separated values.

**`background-size`** controls how large a background image is drawn. The most important values are `cover` (fills element fully, may crop) and `contain` (shows full image, may leave gaps). Fixed pixel or percentage values give precise control.

**`background-origin`** defines the coordinate origin for background positioning — the point from which `background-position` measurements begin. Values are `border-box` (outermost), `padding-box` (default, inner border edge), and `content-box` (inner padding edge).

**`background-clip`** defines the paint boundary — how far the background colour or image is allowed to extend. Values are `border-box` (default, fills everything), `padding-box` (stops at border), `content-box` (stops at padding), and `text` (clips to text character shapes).

The **key distinction** to remember: `background-origin` controls where the background *starts measuring from*; `background-clip` controls where the background *stops painting*.

Together, these four features are used constantly in modern web design for hero banners, layered UI panels, responsive images, gradient text effects, and much more.

---

*End of Lesson 48 — CSS Advanced Backgrounds*
