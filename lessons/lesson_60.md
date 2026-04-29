---
render_with_liquid: false
title: "CSS Masking — PNG Images, Gradients, and SVG Masks"
nav_order: 60
---

# Lesson 60: CSS Masking — PNG Images, Gradients, and SVG Masks

---

## Lesson Introduction

Have you ever seen a photo on a website where part of it fades softly into the page background, or where the image is cut out into a star shape, or where text appears to be "carved out" of a colourful photograph? These stunning effects are created using a CSS technique called **masking**.

CSS masking is one of the most powerful and creative tools available to a web designer. It lets you control exactly which parts of an element are visible and which parts are hidden — and you can do this using an image, a gradient, or a special shape called an SVG.

Think of it like this: imagine you have a photograph printed on a piece of paper. Now you place a stencil on top of it. Where the stencil has holes, you can see the photo through. Where the stencil is solid, the photo is hidden. In CSS masking, the stencil is called a **mask layer**, and it is applied using the `mask-image` property.

In this lesson, you will learn:

- What CSS masking is and why it exists
- How `mask-image` works and what controls it
- How to use a **PNG image** as a mask
- How to use a **CSS gradient** as a mask
- How to use an **SVG shape** as a mask
- Supporting CSS mask properties: `mask-size`, `mask-repeat`, `mask-position`, and `mask-mode`
- How to handle browser compatibility (the `-webkit-` prefix)
- Guided practice exercises and a complete creative mini-project

No prior knowledge of masking is assumed. We start from the very beginning.

---

## Prerequisite Concepts

Before we study masking, let us quickly understand the building blocks we will be using. Do not skip this section — these ideas are the foundation of everything that follows.

---

### What is `opacity`?

`opacity` makes an entire element uniformly transparent. A value of `1` means fully visible. A value of `0` means fully invisible. A value like `0.5` means 50% see-through.

```css
img {
  opacity: 0.5; /* The whole image is 50% transparent */
}
```

**The problem:** `opacity` affects the *entire* element uniformly. You cannot make part of an image fully visible while another part fades out. That is exactly what masking solves.

---

### What is alpha transparency (the "alpha channel")?

When you see a PNG image file, it can have four channels of information for each pixel: Red, Green, Blue, and **Alpha**. The Alpha channel controls how transparent that pixel is. `alpha = 1` means fully opaque (visible). `alpha = 0` means fully transparent (invisible).

A PNG with transparency looks like a photo with the background "cut out" — common for logos, icons, and graphics designers work with daily.

**This alpha channel idea is central to CSS masking.** The mask reads the alpha values of the mask image and uses them to decide how much of the original element to show.

---

### What is a CSS gradient?

A CSS gradient is a smooth colour transition that goes from one colour to another. You have probably seen them before:

```css
/* Goes from black on the left to white on the right */
background: linear-gradient(to right, black, white);
```

Gradients can also go from a colour to **transparent**, which is how we use them as masks to create beautiful fade effects.

---

### What is an SVG?

SVG stands for **Scalable Vector Graphics**. Unlike regular images (which are made of pixels), SVG images are described with mathematical shapes — circles, rectangles, polygons, paths. They can be scaled to any size without becoming blurry. We can write SVG shapes directly inside our HTML, and CSS can use them as masks.

---

## Part 1 — What Is CSS Masking?

### The Core Idea

A **mask** is an invisible layer that sits on top of an element. It determines, pixel by pixel, how visible that element is underneath.

The rule is simple:
- Where the mask is **white (or fully opaque)** → the element shows through fully
- Where the mask is **black (or fully transparent)** → the element is hidden
- Where the mask is **grey (or semi-transparent)** → the element is partially visible

Think of the mask as a dimmer switch for different parts of your element — some areas can be fully bright, some fully dark, and some anywhere in between.

### Why Does Masking Exist?

Before CSS masking, creating shaped images or fade effects required photo-editing software. You had to open Photoshop, apply a mask, export a PNG, and then use that pre-processed image on your website. If you wanted to change the effect, you had to go back to Photoshop.

CSS masking moves this creative power directly into your stylesheet. The original image stays untouched. The shape, fade, or reveal effect lives purely in CSS and can be changed, animated, or made responsive without touching a single image file.

**Real-world uses of CSS masking:**
- Hero images that fade softly into the page background (gradient masks)
- Profile photos cropped into custom shapes — hexagons, stars, speech bubbles
- Text effects where words are "cut out" of photographs
- Decorative section dividers between different page areas
- Creative image galleries where each photo has a unique shape
- Animated reveal effects where an image gradually becomes visible

---

### The `mask-image` Property

The single most important CSS masking property is `mask-image`. It sets the image (or gradient, or SVG shape) to be used as the mask layer.

```css
element {
  mask-image: url("mask.png");
}
```

Everything we learn in this lesson builds on this one property.

> **Browser note:** Most browsers require you to write the property twice — once with a `-webkit-` prefix and once without — to ensure the widest possible compatibility. You will see this throughout all the examples:
>
> ```css
> -webkit-mask-image: url("mask.png"); /* Safari, older Chrome */
>         mask-image: url("mask.png"); /* Modern standard */
> ```
>
> Always include both lines. This is not a mistake — it is intentional and necessary.

---

## Part 2 — Masking with PNG Images

### Why Use a PNG as a Mask?

A PNG image can have an alpha (transparency) channel. This makes it the perfect mask: the transparent parts of the PNG will hide the element underneath, and the opaque parts will reveal it.

You can create complex shapes, artistic cutouts, and decorative frames — all from a single PNG file.

### How It Works — Step by Step

1. You have an element (like a photo or a coloured div).
2. You have a PNG file where some pixels are opaque (white) and some are transparent.
3. You apply the PNG as a `mask-image` to your element.
4. The browser reads each pixel of the PNG: where it is opaque → show the element; where it is transparent → hide the element.

### Simple Example — Circle Mask Using a PNG

Suppose you have a PNG file called `circle-mask.png` that is a solid white circle on a transparent background. When applied as a mask to a photo, only the circular area will show — everything outside the circle is hidden.

```html
<!DOCTYPE html>
<html>
<head>
<style>
  .masked-image {
    width: 300px;
    height: 300px;

    /* The image we want to mask */
    background-image: url("photo.jpg");
    background-size: cover;

    /* Apply the PNG mask */
    -webkit-mask-image: url("circle-mask.png");
            mask-image: url("circle-mask.png");

    /* Make the mask cover the whole element */
    -webkit-mask-size: cover;
            mask-size: cover;

    /* Do not tile/repeat the mask */
    -webkit-mask-repeat: no-repeat;
            mask-repeat: no-repeat;
  }
</style>
</head>
<body>
  <div class="masked-image"></div>
</body>
</html>
```

**Expected result:** The photo appears only inside the circular area defined by the PNG mask. Everything outside the circle is completely invisible.

Let us understand every CSS line:

- `background-image: url("photo.jpg")` — loads the photo we want to display
- `background-size: cover` — makes the photo fill the entire div
- `mask-image: url("circle-mask.png")` — sets the PNG as the mask layer
- `mask-size: cover` — stretches the mask to cover the entire element
- `mask-repeat: no-repeat` — prevents the mask from tiling/repeating

---

### Using a PNG Mask on an `<img>` Element

You are not limited to using masks on `div` elements with background images. You can apply masks directly to `<img>` tags too:

```html
<style>
  img.circle-crop {
    width: 250px;
    height: 250px;
    object-fit: cover; /* Crops the image to fit without distortion */

    -webkit-mask-image: url("circle-mask.png");
            mask-image: url("circle-mask.png");
    -webkit-mask-size: cover;
            mask-size: cover;
    -webkit-mask-repeat: no-repeat;
            mask-repeat: no-repeat;
  }
</style>

<img class="circle-crop" src="portrait.jpg" alt="Profile photo">
```

**Expected result:** The portrait photograph appears as a perfect circle, with everything outside the circle hidden.

> 💡 **Thinking Prompt:** What would happen if the circle PNG mask was smaller than the image? The mask would tile (repeat) across the image, creating multiple circles — unless you add `mask-repeat: no-repeat`.

---

### The `mask-size` Property

`mask-size` controls how large the mask image is rendered, just like `background-size` for backgrounds.

```css
/* Stretch mask to cover the whole element (may crop) */
mask-size: cover;

/* Fit mask inside element (may leave gaps) */
mask-size: contain;

/* Exact pixel size */
mask-size: 200px 200px;

/* Percentage of the element's size */
mask-size: 100% 100%;
```

**Example — same mask, different sizes:**

```css
/* Mask fills the entire element */
.example-a {
  -webkit-mask-image: url("star-mask.png");
          mask-image: url("star-mask.png");
  -webkit-mask-size: cover;
          mask-size: cover;
}

/* Mask is 50% of the element size */
.example-b {
  -webkit-mask-image: url("star-mask.png");
          mask-image: url("star-mask.png");
  -webkit-mask-size: 50%;
          mask-size: 50%;
}
```

**Expected result:** In `.example-a`, the star mask covers the whole element. In `.example-b`, the star is half the size of the element, and if `mask-repeat` is not disabled, you will see multiple stars tiling across it.

---

### The `mask-repeat` Property

`mask-repeat` controls whether the mask image tiles (repeats) when it is smaller than the element.

```css
/* Default — mask tiles in both directions */
mask-repeat: repeat;

/* Tiles only horizontally */
mask-repeat: repeat-x;

/* Tiles only vertically */
mask-repeat: repeat-y;

/* No tiling — mask appears exactly once */
mask-repeat: no-repeat;

/* Tiles as many times as fits, with spacing */
mask-repeat: space;

/* Tiles as many times as fits, stretched to fill exactly */
mask-repeat: round;
```

**Most common use:** `no-repeat` — because you usually want one mask covering the entire element.

---

### The `mask-position` Property

`mask-position` controls where the mask image is positioned within the element, just like `background-position`.

```css
/* Centre the mask */
mask-position: center;

/* Position at top-right corner */
mask-position: top right;

/* Exact pixel offset from top-left */
mask-position: 50px 20px;

/* Percentage-based position */
mask-position: 50% 50%;
```

**Example — centred mask:**

```css
.centred-mask {
  width: 400px;
  height: 300px;
  background-image: url("landscape.jpg");
  background-size: cover;

  -webkit-mask-image: url("diamond-mask.png");
          mask-image: url("diamond-mask.png");
  -webkit-mask-size: 200px 200px;   /* Smaller than the element */
          mask-size: 200px 200px;
  -webkit-mask-repeat: no-repeat;
          mask-repeat: no-repeat;
  -webkit-mask-position: center;    /* Centre the mask on the element */
          mask-position: center;
}
```

**Expected result:** The landscape photo is only visible through a diamond-shaped window centred in the middle of the element. Everything outside the diamond is hidden.

---

### The `mask-mode` Property

`mask-mode` controls what channel of the mask image is used to determine transparency.

```css
/* Uses the alpha channel of the mask image (default) */
mask-mode: alpha;

/* Uses the luminance (brightness) of the mask image */
mask-mode: luminance;

/* Automatically chooses based on mask type */
mask-mode: match-source;
```

**What does this mean in practice?**

- `alpha` mode: White/opaque parts of the mask = element is fully visible. Transparent parts = hidden. This is the most intuitive mode and the default for PNG masks.
- `luminance` mode: **Bright (white)** parts of the mask = element is visible. **Dark (black)** parts = hidden. Gradients between black and white create smooth transitions. This mode is often used when the mask image does not have an alpha channel (like a JPEG, which cannot be transparent).

```css
.luminance-mask {
  -webkit-mask-image: url("greyscale-mask.jpg");
          mask-image: url("greyscale-mask.jpg");
  -webkit-mask-mode: luminance; /* Use brightness, not transparency */
          mask-mode: luminance;
}
```

---

### Full PNG Masking Reference Table

| Property | What It Controls | Common Values |
|---|---|---|
| `mask-image` | Which image to use as the mask | `url("file.png")`, `none` |
| `mask-size` | How large the mask is | `cover`, `contain`, `100%`, `200px` |
| `mask-repeat` | Whether the mask tiles | `no-repeat`, `repeat`, `repeat-x` |
| `mask-position` | Where the mask is placed | `center`, `top right`, `50% 50%` |
| `mask-mode` | Which channel determines visibility | `alpha`, `luminance` |

> Always prefix all properties with `-webkit-` for Safari compatibility.

---

## Part 3 — Masking with CSS Gradients

### Why Use a Gradient as a Mask?

Using a gradient as a mask is one of the most elegant and commonly used techniques in modern web design. It creates effects like:

- An image that softly **fades to transparent** at one edge — instead of stopping sharply
- An image that is **fully visible in the centre** and fades out toward the edges
- A **text reveal effect** where words gradually appear from left to right
- A **section divider** where one background colour smoothly blends into the next

There is no PNG file involved at all — the mask is generated entirely in CSS using the `linear-gradient()` or `radial-gradient()` functions.

### The Golden Rule of Gradient Masks

Remember this rule and you will never be confused:

> **Where the gradient is WHITE (or opaque) → the element is VISIBLE**
> **Where the gradient is BLACK (or transparent) → the element is HIDDEN**

So a gradient that goes from `black` to `white` (left to right) creates a mask where the left side is hidden and the right side is fully visible. A gradient from `white` to `black` does the opposite.

The easiest way to write this is to go from `transparent` to a colour (or any opaque value), because browsers understand `transparent` as "hide this" regardless of mask mode:

```css
/* From transparent (hidden) on left → black (visible) on right */
mask-image: linear-gradient(to right, transparent, black);
```

---

### Example 1 — Image Fades to Transparent on the Right

```html
<style>
  .fade-right {
    width: 400px;
    height: 250px;
    background-image: url("forest.jpg");
    background-size: cover;

    /* Gradient mask: fully visible on left, fades to hidden on right */
    -webkit-mask-image: linear-gradient(to right, black, transparent);
            mask-image: linear-gradient(to right, black, transparent);
  }
</style>

<div class="fade-right"></div>
```

**Expected result:** The forest photo is fully visible on the left side. As you move toward the right, it becomes increasingly transparent, fading into the page background completely by the right edge.

This is the exact effect you see on many websites where a photo blends seamlessly into a white or coloured background — no hard edge, just a smooth fade.

---

### Example 2 — Image Fades to Transparent on the Left

```css
.fade-left {
  width: 400px;
  height: 250px;
  background-image: url("city.jpg");
  background-size: cover;

  /* Fully visible on right, fades to hidden on left */
  -webkit-mask-image: linear-gradient(to left, black, transparent);
          mask-image: linear-gradient(to left, black, transparent);
}
```

**Expected result:** The city photo is fully visible on the right and fades to transparent on the left.

---

### Example 3 — Image Fades from Top

```css
.fade-top {
  width: 400px;
  height: 250px;
  background-image: url("mountains.jpg");
  background-size: cover;

  /* Fully visible at bottom, fades to hidden at top */
  -webkit-mask-image: linear-gradient(to top, black, transparent);
          mask-image: linear-gradient(to top, black, transparent);
}
```

**Expected result:** The mountain photo is fully visible at the bottom and fades upward into transparency. Useful for text overlays on hero sections.

---

### Example 4 — Visible in the Centre, Fades on Both Sides

This uses a gradient with three colour stops:

```css
.fade-edges {
  width: 500px;
  height: 200px;
  background-image: url("beach.jpg");
  background-size: cover;

  /* Transparent on left → black in centre → transparent on right */
  -webkit-mask-image: linear-gradient(to right, transparent, black 30%, black 70%, transparent);
          mask-image: linear-gradient(to right, transparent, black 30%, black 70%, transparent);
}
```

**Decoding the gradient stops:**
- `transparent` — starts at 0%, element is hidden
- `black 30%` — by 30% of the width, element is fully visible
- `black 70%` — stays fully visible until 70%
- `transparent` — by 100% (right edge), element is hidden again

**Expected result:** The beach photo is hidden at both left and right edges, but fully visible in the central 40% of the image. This creates a natural vignette effect.

---

### Example 5 — Radial Gradient Mask (Spotlight Effect)

You can also use `radial-gradient()` to create a circular reveal effect, as if a spotlight is shining on part of the image:

```css
.spotlight {
  width: 400px;
  height: 400px;
  background-image: url("portrait.jpg");
  background-size: cover;

  /* Fully visible in the centre circle, fades out toward edges */
  -webkit-mask-image: radial-gradient(circle, black 40%, transparent 70%);
          mask-image: radial-gradient(circle, black 40%, transparent 70%);
}
```

**Decoding this:**
- `circle` — the gradient is circular, not elliptical
- `black 40%` — fully visible out to 40% radius from centre
- `transparent 70%` — fades to fully hidden by 70% radius

**Expected result:** The portrait is clearly visible in the centre of the image. Toward the edges, it gradually fades to invisible, as if illuminated by a spotlight from directly above.

> 💡 **Thinking Prompt:** What happens if you swap `black` and `transparent` in the radial gradient? The centre would be hidden and the edges visible — the opposite of a spotlight, more like a ring cutout!

---

### Example 6 — Text with Gradient Mask (Fading Text Effect)

Masking is not limited to images. You can apply a gradient mask to any HTML element, including paragraphs:

```css
.fading-text {
  font-size: 48px;
  font-weight: bold;
  color: navy;
  width: 400px;

  /* Text starts opaque and fades to invisible on the right */
  -webkit-mask-image: linear-gradient(to right, black 50%, transparent);
          mask-image: linear-gradient(to right, black 50%, transparent);
}
```

**Expected result:** The first half of the text is fully visible (navy blue). The text then gradually fades to invisible across the second half. This is often used for "read more" truncation effects or decorative headings.

---

### Gradient Mask Direction Quick Reference

| Gradient Direction | Visible Side | Hidden Side |
|---|---|---|
| `linear-gradient(to right, black, transparent)` | Left | Right |
| `linear-gradient(to left, black, transparent)` | Right | Left |
| `linear-gradient(to bottom, black, transparent)` | Top | Bottom |
| `linear-gradient(to top, black, transparent)` | Bottom | Top |
| `radial-gradient(circle, black, transparent)` | Centre | Edges |
| `radial-gradient(circle, transparent, black)` | Edges | Centre |

---

## Part 4 — Masking with SVG

### Why Use an SVG as a Mask?

SVG masks are the most powerful and flexible masking technique. Unlike a PNG image (which is a fixed set of pixels) or a gradient (which is always smooth), an SVG mask lets you define **any shape imaginable** using mathematical descriptions. You can create:

- Perfect geometric shapes: stars, hexagons, pentagons, arrows
- Complex organic shapes: speech bubbles, waves, clouds, country outlines
- Text-shaped cutouts where the image appears through the letters
- Combined shapes with holes, overlaps, and curves

And because SVG is vector-based, it scales perfectly to any screen size or resolution — critical for responsive design and high-DPI (Retina) displays.

### Two Ways to Use SVG Masks

There are two approaches:

1. **Reference an external SVG file** using `mask-image: url("mask.svg")`
2. **Embed the SVG directly in HTML** and reference a `<mask>` element using its `id`

We will cover both.

---

### Method 1 — Using an External SVG File as the Mask Image

If you have an SVG file that contains a solid white shape on a transparent background, you can use it exactly like a PNG:

```html
<style>
  .svg-masked {
    width: 300px;
    height: 300px;
    background-image: url("cityscape.jpg");
    background-size: cover;

    /* Use an SVG file as the mask */
    -webkit-mask-image: url("hexagon-mask.svg");
            mask-image: url("hexagon-mask.svg");
    -webkit-mask-size: cover;
            mask-size: cover;
    -webkit-mask-repeat: no-repeat;
            mask-repeat: no-repeat;
    -webkit-mask-position: center;
            mask-position: center;
  }
</style>

<div class="svg-masked"></div>
```

The `hexagon-mask.svg` file would contain a white hexagon shape on a transparent background:

```xml
<!-- hexagon-mask.svg -->
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100">
  <polygon
    fill="white"
    points="50,5 95,27.5 95,72.5 50,95 5,72.5 5,27.5"
  />
</svg>
```

**Expected result:** The city photo appears only within the hexagon shape. Everything outside the hexagon is hidden.

---

### Method 2 — Inline SVG `<mask>` Element (The Most Powerful Approach)

This is the most flexible technique. You write the SVG shape directly inside your HTML document, give it an `id`, and then reference it in your CSS `mask-image`.

**The structure:**

```html
<!-- Step 1: Define the SVG mask inside the HTML (can be hidden, zero-size) -->
<svg width="0" height="0">
  <defs>
    <mask id="my-mask">
      <!-- White = visible, black = hidden -->
      <rect width="100%" height="100%" fill="white"/>
      <circle cx="150" cy="150" r="100" fill="black"/>
    </mask>
  </defs>
</svg>

<!-- Step 2: Apply the mask to your element -->
<div class="masked-element"></div>
```

```css
/* Step 3: Reference the SVG mask by its ID */
.masked-element {
  width: 300px;
  height: 300px;
  background-image: url("abstract.jpg");
  background-size: cover;

  mask-image: url(#my-mask);
  /* Note: inline SVG masks usually do not need -webkit- prefix */
}
```

**Expected result:** The entire abstract photo is visible except for a circular hole cut out of the centre (because we drew a black circle inside a white rectangle — black hides, white reveals).

---

### Understanding How SVG `<mask>` Elements Work

Inside an SVG `<mask>`, the colours you draw determine visibility:

- **White fill** (`fill="white"`) → that area of the masked element is **fully visible**
- **Black fill** (`fill="black"`) → that area is **fully hidden**
- **Grey fill** (`fill="grey"`) → that area is **partially visible**

This is the opposite of what you might expect from transparency! In SVG masks, colour brightness controls visibility, not actual transparency.

**Example — Text Cutout Mask:**

Create an effect where your background image is only visible through the shapes of letters:

```html
<!-- Define the SVG text mask -->
<svg width="0" height="0">
  <defs>
    <mask id="text-mask">
      <!-- Black background = everything hidden by default -->
      <rect width="100%" height="100%" fill="black"/>
      <!-- White text = image shows through the letters -->
      <text
        x="50%"
        y="60%"
        text-anchor="middle"
        font-family="Arial Black, sans-serif"
        font-size="72"
        font-weight="900"
        fill="white">
        NATURE
      </text>
    </mask>
  </defs>
</svg>

<!-- Apply to a div with a background image -->
<div class="text-reveal"></div>
```

```css
.text-reveal {
  width: 500px;
  height: 150px;
  background-image: url("forest-sunset.jpg");
  background-size: cover;
  background-position: center;
  mask-image: url(#text-mask);
}
```

**Expected result:** The forest sunset photo is only visible through the letters "NATURE". Outside the letters, nothing is visible — the background is hidden. This creates a striking typographic image effect often seen in modern editorial design.

---

### Example — Star Shape SVG Mask

```html
<svg width="0" height="0">
  <defs>
    <mask id="star-mask">
      <rect width="100%" height="100%" fill="black"/>
      <!-- A five-pointed star drawn as a polygon -->
      <polygon
        fill="white"
        points="150,20 180,110 270,110 200,165 225,255 150,200 75,255 100,165 30,110 120,110"
      />
    </mask>
  </defs>
</svg>

<div class="star-photo"></div>
```

```css
.star-photo {
  width: 300px;
  height: 300px;
  background-image: url("fireworks.jpg");
  background-size: cover;
  mask-image: url(#star-mask);
  -webkit-mask-image: url(#star-mask);
}
```

**Expected result:** The fireworks photo is only visible inside the star polygon. Everything outside the star shape is hidden.

---

### Example — Multiple Shapes in One SVG Mask

You can combine multiple shapes in a single mask for complex effects:

```html
<svg width="0" height="0">
  <defs>
    <mask id="circles-mask">
      <!-- White background — everything visible by default -->
      <rect width="100%" height="100%" fill="white"/>
      <!-- Three black circles cut holes in the image -->
      <circle cx="80"  cy="80"  r="60" fill="black"/>
      <circle cx="220" cy="80"  r="60" fill="black"/>
      <circle cx="150" cy="200" r="60" fill="black"/>
    </mask>
  </defs>
</svg>

<div class="holey-image"></div>
```

```css
.holey-image {
  width: 300px;
  height: 280px;
  background-image: url("abstract-art.jpg");
  background-size: cover;
  mask-image: url(#circles-mask);
}
```

**Expected result:** The abstract art photo fills the element, but three circular holes are punched through it — you see the page background through those circles.

---

### Combining SVG Masks with Gradients (Advanced)

You can even combine gradient fills inside SVG mask shapes for partially transparent edges:

```html
<svg width="0" height="0">
  <defs>
    <!-- A gradient that goes from white to black -->
    <linearGradient id="fade-gradient" x1="0" y1="0" x2="1" y2="0">
      <stop offset="0%" stop-color="white"/>
      <stop offset="100%" stop-color="black"/>
    </linearGradient>

    <mask id="gradient-rect-mask">
      <!-- Rectangle filled with the fade gradient -->
      <rect width="100%" height="100%" fill="url(#fade-gradient)"/>
    </mask>
  </defs>
</svg>

<div class="fade-div"></div>
```

```css
.fade-div {
  width: 400px;
  height: 200px;
  background-image: url("landscape.jpg");
  background-size: cover;
  mask-image: url(#gradient-rect-mask);
}
```

**Expected result:** The landscape is fully visible on the left (where the gradient is white) and fully hidden on the right (where the gradient is black) — the same visual result as a CSS `linear-gradient` mask, but defined as SVG.

---

## Part 5 — Code Challenges (From the W3Schools Challenge Page)

The W3Schools CSS Masking challenge page covers the following types of tasks. Here are those challenge types, explained fully with worked solutions.

---

### Challenge Type 1: Apply a Gradient Mask to Fade an Image

**Task:** Make a `div` with a background image that fades from visible to transparent from left to right.

**Solution:**

```css
.challenge-1 {
  width: 400px;
  height: 250px;
  background-image: url("landscape.jpg");
  background-size: cover;

  -webkit-mask-image: linear-gradient(to right, black, transparent);
          mask-image: linear-gradient(to right, black, transparent);
}
```

**Key point:** `black` = visible, `transparent` = hidden. The gradient runs from left (black = visible) to right (transparent = hidden).

---

### Challenge Type 2: Apply a PNG Mask with `mask-size` and `mask-repeat`

**Task:** Apply a star-shaped PNG mask to an image, make the mask fill the entire element, and prevent it from repeating.

**Solution:**

```css
.challenge-2 {
  width: 300px;
  height: 300px;
  background-image: url("photo.jpg");
  background-size: cover;

  -webkit-mask-image: url("star.png");
          mask-image: url("star.png");
  -webkit-mask-size: cover;
          mask-size: cover;
  -webkit-mask-repeat: no-repeat;
          mask-repeat: no-repeat;
  -webkit-mask-position: center;
          mask-position: center;
}
```

---

### Challenge Type 3: Create a Circular Fade Using Radial Gradient

**Task:** Make a photo fully visible in the centre, fading to transparent at the edges.

**Solution:**

```css
.challenge-3 {
  width: 350px;
  height: 350px;
  background-image: url("portrait.jpg");
  background-size: cover;

  -webkit-mask-image: radial-gradient(circle, black 50%, transparent 75%);
          mask-image: radial-gradient(circle, black 50%, transparent 75%);
}
```

**Decoding:** Fully visible from centre to 50% radius, then fades to hidden by 75% radius. Outside 75% — completely hidden.

---

### Challenge Type 4: SVG Mask Applied via `mask-image`

**Task:** Use an SVG circle as a mask on a photo element.

**Solution (inline SVG + CSS reference):**

```html
<svg width="0" height="0">
  <defs>
    <mask id="circle-cut">
      <circle cx="150" cy="150" r="150" fill="white"/>
    </mask>
  </defs>
</svg>

<div class="challenge-4"></div>
```

```css
.challenge-4 {
  width: 300px;
  height: 300px;
  background-image: url("photo.jpg");
  background-size: cover;
  mask-image: url(#circle-cut);
  -webkit-mask-image: url(#circle-cut);
}
```

---

### Challenge Type 5: Multi-stop Gradient Mask (Visible Only in Centre)

**Task:** Create an image that is hidden at both left and right edges, with a visible band in the middle.

**Solution:**

```css
.challenge-5 {
  width: 500px;
  height: 200px;
  background-image: url("banner.jpg");
  background-size: cover;

  -webkit-mask-image: linear-gradient(
    to right,
    transparent 0%,
    black 25%,
    black 75%,
    transparent 100%
  );
  mask-image: linear-gradient(
    to right,
    transparent 0%,
    black 25%,
    black 75%,
    transparent 100%
  );
}
```

---

## Part 6 — Guided Practice Exercises

### Exercise 1 — Fade-Out Social Media Header

**Objective:** Create a wide hero banner image that fades from visible on the left to transparent on the right, so it blends seamlessly into a white page.

**Scenario:** You are designing a photography portfolio. The header has a wide landscape photo. Instead of a hard edge on the right, you want it to fade gently into the white background.

**Steps:**
1. Create a `div` with `width: 600px` and `height: 200px`.
2. Set a landscape `background-image` and `background-size: cover`.
3. Apply a `linear-gradient` mask going from `black` on the left to `transparent` on the right.
4. Remember to include both the `-webkit-` prefix and the standard property.

**Expected Output:** A wide photo that is fully visible on the left half and gradually fades to nothing on the right half.

**Self-check Questions:**
- Is the right edge of the image completely invisible (no hard line)?
- Does the photo fill the div correctly?
- Have you included both the `-webkit-mask-image` and `mask-image` lines?

---

### Exercise 2 — Profile Photo in a Hexagon

**Objective:** Crop a profile photo into a hexagonal shape using an SVG mask.

**Scenario:** You are building a team members page for a tech company. Each team member's photo should appear inside a hexagon shape for a modern, geometric look.

**Steps:**
1. Create an inline `<svg>` with `width="0" height="0"` containing a `<defs>` block.
2. Inside `<defs>`, define a `<mask id="hex-mask">`.
3. Inside the mask, draw a white `<polygon>` hexagon (use the points: `"50,5 95,27.5 95,72.5 50,95 5,72.5 5,27.5"` on a viewBox of 0 0 100 100).
4. Apply the mask to a `div` with a `background-image`.

**Expected Output:** A team member photo visible only inside a hexagonal shape.

**Hint:** The SVG polygon coordinate system is separate from your CSS pixel layout. Use `mask-size: cover` to stretch the SVG mask to fit your element.

---

### Exercise 3 — Spotlight Reveal

**Objective:** Apply a radial gradient mask so that the centre of an image is clearly visible while the edges fade away.

**Scenario:** You are showcasing a product photo on an e-commerce site. You want a soft spotlight effect that draws the viewer's eye to the product in the centre, with the surroundings fading into the background.

**Steps:**
1. Create a square `div` (e.g., `350px × 350px`) with a product background image.
2. Apply a `radial-gradient` mask: fully visible at centre, fading to transparent at the outer edge.
3. Tune the gradient stops until the transition feels natural.

**Expected Output:** Product photo fully visible in the centre, fading softly toward transparent at the edges — a professional spotlight look.

**What-if Challenge:** What if you set the first stop to `transparent` and the second to `black`? You would get the opposite effect: a ring of visibility at the edges and a hole in the centre — like looking through a porthole.

---

### Exercise 4 — Text Carved from a Photo (SVG Text Mask)

**Objective:** Create a bold heading that is "filled" with a photograph — so the image shows through the letters.

**Scenario:** You are designing a landing page for a travel agency. The hero section will have the word "TRAVEL" in massive letters, with a beautiful aerial ocean photo visible only through the letters.

**Steps:**
1. Create an inline `<svg>` with a `<mask id="word-mask">`.
2. Inside the mask: fill the background with `black` (a full-size `<rect fill="black"/>`).
3. Add `<text>` with `fill="white"`, a very bold font, and the word "TRAVEL".
4. Apply the mask to a wide, short `div` with a background photo.
5. Ensure the text coordinates are centred within the SVG viewBox.

**Expected Output:** A striking headline where the ocean photo shines through the letters "TRAVEL" against a hidden/transparent background.

---

## Part 7 — Mini Project: Creative Photo Gallery with Masking

In this mini-project, you will build a gallery of four images, each using a different masking technique, presented in a polished grid layout.

---

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>CSS Masking Gallery</title>
  <link rel="stylesheet" href="gallery.css">
</head>
<body>

  <!-- SVG mask definitions (invisible, zero-size) -->
  <svg width="0" height="0" style="position:absolute">
    <defs>

      <!-- Mask 1: Circle -->
      <mask id="mask-circle">
        <circle cx="150" cy="150" r="145" fill="white"/>
      </mask>

      <!-- Mask 2: Star -->
      <mask id="mask-star">
        <polygon
          fill="white"
          points="150,15 180,105 275,105 200,162 225,255 150,200 75,255 100,162 25,105 120,105"
        />
      </mask>

      <!-- Mask 3: Diamond -->
      <mask id="mask-diamond">
        <polygon fill="white" points="150,10 290,150 150,290 10,150"/>
      </mask>

      <!-- Mask 4: Speech bubble (rectangle + triangle) -->
      <mask id="mask-speech">
        <rect x="5" y="5" width="260" height="200" rx="20" ry="20" fill="white"/>
        <polygon fill="white" points="40,205 80,205 40,270"/>
      </mask>

    </defs>
  </svg>

  <h1>CSS Masking Gallery</h1>

  <div class="gallery">

    <div class="card">
      <div class="photo circle-mask" style="background-image: url('forest.jpg')"></div>
      <p>Circle — PNG / SVG Mask</p>
    </div>

    <div class="card">
      <div class="photo gradient-fade" style="background-image: url('mountains.jpg')"></div>
      <p>Gradient Fade — Right</p>
    </div>

    <div class="card">
      <div class="photo star-mask" style="background-image: url('beach.jpg')"></div>
      <p>Star — SVG Mask</p>
    </div>

    <div class="card">
      <div class="photo spotlight" style="background-image: url('cityscape.jpg')"></div>
      <p>Spotlight — Radial Gradient</p>
    </div>

  </div>

</body>
</html>
```

**Milestone output:** Four placeholder boxes appear in a grid, each labelled with its masking technique.

---

### Stage 2 — Gallery Layout CSS

```css
/* gallery.css */

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Segoe UI', Tahoma, sans-serif;
  background: #1a1a2e;  /* Deep navy background */
  color: #eaeaea;
  padding: 40px 20px;
  text-align: center;
}

h1 {
  margin-bottom: 40px;
  font-size: 2rem;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: #e0aaff;
}

.gallery {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 40px;
  max-width: 800px;
  margin: 0 auto;
}

.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
}

.card p {
  font-size: 0.9rem;
  color: #a0a0c0;
  letter-spacing: 1px;
}

/* All photo divs share base styles */
.photo {
  width: 300px;
  height: 300px;
  background-size: cover;
  background-position: center;
}
```

**Milestone output:** A clean dark-navy page with a 2×2 grid. Four empty squares are ready to receive their masks.

---

### Stage 3 — Apply the Masks

Add to `gallery.css`:

```css
/* Card 1: Circle SVG mask */
.circle-mask {
  mask-image: url(#mask-circle);
  -webkit-mask-image: url(#mask-circle);
}

/* Card 2: Gradient fade to the right */
.gradient-fade {
  -webkit-mask-image: linear-gradient(to right, black 40%, transparent 100%);
          mask-image: linear-gradient(to right, black 40%, transparent 100%);
}

/* Card 3: Star SVG mask */
.star-mask {
  mask-image: url(#mask-star);
  -webkit-mask-image: url(#mask-star);
}

/* Card 4: Radial spotlight */
.spotlight {
  -webkit-mask-image: radial-gradient(circle, black 40%, transparent 72%);
          mask-image: radial-gradient(circle, black 40%, transparent 72%);
}
```

**Milestone output:** Each photo now appears through its respective mask. The circle photo is cropped into a circle; the mountains fade to the right; the beach appears in a star; the cityscape has a spotlight effect.

---

### Stage 4 — Add a Fifth Card: Text-Through-Photo

Add a fifth card in the HTML:

```html
<!-- In the .gallery div, add: -->
<div class="card" style="grid-column: 1 / -1;">
  <!-- SVG mask for text -->
  <svg width="0" height="0" style="position:absolute">
    <defs>
      <mask id="mask-text">
        <rect width="100%" height="100%" fill="black"/>
        <text
          x="50%"
          y="65%"
          text-anchor="middle"
          dominant-baseline="middle"
          font-family="Arial Black, Impact, sans-serif"
          font-size="90"
          font-weight="900"
          fill="white">
          GALLERY
        </text>
      </mask>
    </defs>
  </svg>

  <div class="photo text-mask" style="background-image: url('abstract-colour.jpg'); width: 600px; height: 140px;"></div>
  <p>Text Cutout — SVG Text Mask</p>
</div>
```

Add to `gallery.css`:

```css
/* Card 5: Text cutout mask */
.text-mask {
  mask-image: url(#mask-text);
  -webkit-mask-image: url(#mask-text);
}
```

**Milestone output:** A wide banner spans the full width of the gallery. The colourful abstract photo shines through the bold letters "GALLERY" — everything else is hidden.

---

### Stage 5 — Reflection

After completing the project, reflect on these questions:

1. Which masking technique do you think creates the most visual impact? Why?
2. Can you change the `gradient-fade` card to fade from bottom to top instead?
3. What would happen if you set `mask-repeat: repeat` on the `star-mask` card and set `mask-size: 80px`?
4. Could you animate a gradient mask using CSS `@keyframes` to create a "wipe reveal" effect on the photo? What properties would you animate?

**Optional Enhancement:** Add a CSS `transition` on each `.photo` element and change the `mask-size` on hover to slowly grow the mask — creating an animated reveal effect!

---

## Part 8 — Common Beginner Mistakes

### Mistake 1: Forgetting the `-webkit-` Prefix

**Wrong:**
```css
.masked {
  mask-image: url("mask.png"); /* Works in Chrome/Firefox but not Safari */
}
```

**Correct:**
```css
.masked {
  -webkit-mask-image: url("mask.png"); /* Safari */
          mask-image: url("mask.png"); /* Standard */
}
```

**Rule:** Always write both. Apply the same rule to `mask-size`, `mask-repeat`, `mask-position`, and `mask-mode`.

---

### Mistake 2: Confusing Black and White in Masks

Many beginners expect white in the mask to mean "hide" (like a white wall blocking the view). The opposite is true.

**Wrong mental model:**
> "White = blocked/hidden, black = visible through"

**Correct mental model:**
> **White = fully visible. Black = fully hidden.**

Think of it as "white light reveals" — where light shines (white), you can see. Where there is darkness (black), you cannot.

---

### Mistake 3: Applying a Gradient Mask in the Wrong Direction

**Wrong (hides left side, reveals right — often not what you want):**
```css
mask-image: linear-gradient(to right, transparent, black);
/* Transparent on left = hidden, black on right = visible */
```

**Correct (if you want to reveal left and hide right):**
```css
mask-image: linear-gradient(to right, black, transparent);
/* Black on left = visible, transparent on right = hidden */
```

**Trick:** Always spell out which side should be `black` (visible) and which should be `transparent` (hidden). The gradient direction `to right` just tells CSS which way to travel.

---

### Mistake 4: Forgetting `mask-repeat: no-repeat`

When `mask-size` is smaller than the element, the mask will tile by default — creating a repeating pattern of shapes.

**Wrong (mask tiles unintentionally):**
```css
.masked {
  mask-image: url("circle.png");
  mask-size: 100px 100px; /* Small mask, big element → many circles! */
  /* Missing mask-repeat: no-repeat */
}
```

**Correct:**
```css
.masked {
  mask-image: url("circle.png");
  mask-size: cover;         /* OR keep small and add: */
  mask-repeat: no-repeat;   /* Prevent tiling */
  -webkit-mask-image: url("circle.png");
  -webkit-mask-size: cover;
  -webkit-mask-repeat: no-repeat;
}
```

---

### Mistake 5: Writing SVG Mask IDs Incorrectly in `mask-image`

**Wrong:**
```css
/* Missing the # (hash) — CSS thinks it is a URL to a file called "star-mask" */
mask-image: url(star-mask);
```

**Correct:**
```css
/* # means "look for an element with this ID in the current document" */
mask-image: url(#star-mask);
```

---

### Mistake 6: Using Colours in SVG Masks Instead of White/Black

**Wrong:**
```html
<!-- Using blue for "visible" — this does not work as expected -->
<mask id="my-mask">
  <circle cx="150" cy="150" r="100" fill="blue"/>
</mask>
```

**Correct:**
```html
<!-- SVG masks use WHITE for visible and BLACK for hidden -->
<mask id="my-mask">
  <circle cx="150" cy="150" r="100" fill="white"/>
</mask>
```

**Why?** In SVG masks, the browser calculates visibility from the luminance (brightness) of each pixel. Blue is dark → it will mostly hide. White is fully bright → it fully reveals.

---

### Mistake 7: Placing SVG Mask Definitions After the Elements That Use Them

Browsers generally require that an element referenced by `id` (like a `<mask>`) be defined in the document before or alongside the element that uses it. Placing the `<svg>` block at the end of the `<body>` can cause the mask not to apply.

**Best practice:** Place the `<svg>` with `<defs>` at the **very top of the `<body>`**, before any content elements.

---

## Part 9 — Reflection Questions

Think carefully about each of these before checking with experiments:

1. CSS masking and CSS `clip-path` both hide parts of an element. What is one key difference between them? (Hint: can `clip-path` create smooth semi-transparent edges?)

2. If you use `mask-mode: luminance` and your mask image is a bright red JPEG, which parts of the element will be visible — the light areas or the dark areas?

3. A gradient mask goes from `black 0%` to `black 60%` to `transparent 100%`. What percentage of the element is fully visible, and what percentage is partially or fully hidden?

4. You have a `div` that is `400px` wide and `200px` tall, and you apply a circular `mask-image` from a `200px × 200px` PNG with `mask-repeat: repeat`. How many circles would tile across the width?

5. Can you apply two different masks to the same element at once? (Hint: look up `mask-image` with comma-separated values — yes, this is possible!)

6. If you animate `mask-size` from `0% 0%` to `100% 100%` with a CSS `@keyframes` rule, what visual effect would you see? When would this be useful?

---

## Completion Checklist

Go through each item and confirm you can do it confidently:

- [ ] I can explain in plain English what CSS masking is and why it is useful
- [ ] I understand the rule: white in a mask = visible, black = hidden
- [ ] I can apply a PNG image as a mask using `mask-image: url()`
- [ ] I can control mask sizing with `mask-size: cover` and `mask-size: contain`
- [ ] I can prevent mask tiling with `mask-repeat: no-repeat`
- [ ] I can position a mask with `mask-position: center`
- [ ] I understand the difference between `mask-mode: alpha` and `mask-mode: luminance`
- [ ] I can create a left-fade effect using `linear-gradient(to right, black, transparent)`
- [ ] I can create a right-fade effect using `linear-gradient(to left, black, transparent)`
- [ ] I can create a spotlight effect using `radial-gradient(circle, black, transparent)`
- [ ] I can create a multi-stop gradient mask to hide both edges and show only the centre
- [ ] I can define an SVG `<mask>` inline in HTML and reference it in CSS
- [ ] I know that SVG mask shapes use `fill="white"` for visible and `fill="black"` for hidden
- [ ] I can create a text-through-photo effect using an SVG `<text>` element inside a mask
- [ ] I always include both `-webkit-mask-*` and `mask-*` properties
- [ ] I completed the four-technique masking gallery mini-project
- [ ] I can identify and fix the seven common beginner mistakes

---

## Lesson Summary

CSS masking is one of the most expressive and creative capabilities in modern CSS. It gives you pixel-level control over what is visible in any element — whether that is an image, a div, text, or any other HTML element.

Here is the complete picture of what you learned:

**The core concept:** A mask layer sits on top of your element. Where the mask is white (or opaque), the element shows through. Where the mask is black (or transparent), the element is hidden. Where the mask is grey (or semi-transparent), the element is partially visible.

**Three types of masks:**

The first type uses a **PNG image** — a graphic file with transparent and opaque pixels. You reference it with `mask-image: url("file.png")`, control its coverage with `mask-size`, prevent tiling with `mask-repeat: no-repeat`, and position it with `mask-position`. This is ideal for custom shapes defined by a graphic designer.

The second type uses a **CSS gradient** — no external file needed. A `linear-gradient` running from `black` to `transparent` creates beautiful fade effects. A `radial-gradient` creates spotlight or vignette effects. Multi-stop gradients let you control exactly where the visible, transitioning, and hidden zones are. This is the fastest technique to apply and the most common in production websites.

The third type uses an **SVG mask** — either an external `.svg` file or an inline `<mask>` element defined in your HTML. SVG masks offer unlimited shape flexibility: circles, stars, hexagons, polygons, text shapes, compound shapes with holes, and even gradient-filled shapes. The key rules for inline SVG masks are: use `fill="white"` to make areas visible, `fill="black"` to make areas hidden, and reference the mask using `mask-image: url(#id-name)`.

**Browser compatibility:** Always write every mask property twice — once with the `-webkit-` prefix for Safari, and once without for the modern standard.

**In professional web design**, masking is used for hero image fade effects, shaped profile photos, decorative section transitions, text image reveals, artistic image galleries, and animated content appearances. Mastering it will make your web designs dramatically more polished and distinctive.

---

*End of Lesson 60 — CSS Masking: PNG Images, Gradients, and SVG Masks*
