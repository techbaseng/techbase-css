---
render_with_liquid: false
title: "CSS Border Images"
nav_order: 47
---

# Lesson 47 — CSS Border Images

---

## Lesson Introduction

Have you ever seen a beautifully decorated box, frame, or certificate where the edges have an artistic pattern — diamonds, flowers, geometric shapes — instead of just a plain coloured line? That is exactly what CSS Border Images allow you to do on a webpage.

Instead of the usual solid, dashed, or dotted borders you have already learned about, the **CSS `border-image` property** lets you take any image file and use it as the decorative border of any HTML element. The browser cleverly slices that image into nine zones (like a tic-tac-toe board) and maps each zone to the correct part of the element's border: corners go to corners, sides go to sides, and the middle section is either stretched or repeated to fill the available space.

By the end of this lesson you will be able to:
- Understand what the `border-image` property is and why it exists.
- Know all five sub-properties that make up `border-image`.
- Apply images as borders using pixel values and percentage values for slicing.
- Control whether border sides are stretched (`stretch`) or tiled (`round`).
- Avoid the most common beginner mistakes.
- Complete guided exercises and a mini-project using everything you have learned.

---

## Prerequisite Concepts

Before we dive in, let us make sure you are comfortable with a few ideas. If any of these feel new, read the short explanations below before moving on.

### What is a CSS Border?

A **border** is a decorative line drawn around the outside edge of an HTML element. You set it using the `border` property:

```css
/* selector { border: width style colour; } */
div {
  border: 5px solid black;
}
```

- `5px` → how thick the border is (the width)
- `solid` → the style (could also be `dashed`, `dotted`, etc.)
- `black` → the colour

**Important rule for this lesson:** The `border` property **must** be set on an element before `border-image` will work. Without it, the browser ignores your image border entirely.

### What is a CSS Property vs a Shorthand Property?

A **shorthand property** is a single property name that lets you set several related properties at once. Think of it like ordering a meal combo: instead of ordering a burger, fries, and drink separately, you say "Combo 1" and get all three.

`border-image` is a shorthand property — it combines five individual sub-properties into one line.

### What is a URL in CSS?

In CSS, `url()` is a function used to point to an image file. For example:

```css
url(border.png)        /* image in the same folder */
url(images/border.png) /* image inside an 'images' folder */
url(https://example.com/border.png) /* image from the internet */
```

---

## Conceptual Understanding

### What Exactly is `border-image`?

Imagine you have a square postage stamp with a decorative pattern. Now imagine cutting that stamp into **nine pieces** with two horizontal cuts and two vertical cuts — like a tic-tac-toe grid. You now have:

- **4 corners** (top-left, top-right, bottom-left, bottom-right)
- **4 sides** (top edge, right edge, bottom edge, left edge)
- **1 centre** (the middle piece — usually discarded)

The browser does exactly this when you use `border-image`. It:
1. Takes your image.
2. Slices it into those nine pieces.
3. Places the four corner pieces at the four corners of your element.
4. Takes the four side pieces and either **stretches** them or **tiles (repeats)** them along each side.
5. Ignores the centre piece by default.

This is brilliant because no matter how big or small your element is, the corners always look crisp and the sides fill perfectly.

### Why Does `border-image` Exist?

Before `border-image`, designers who wanted decorative borders had to use complex workarounds: multiple nested `<div>` elements, background images, or even tables. These approaches were messy and hard to maintain.

The `border-image` property (introduced in CSS3) solved this cleanly. One property, one image, any element.

**Real-world uses:**
- Decorative certificate or diploma frames on a webpage
- Artistic card or badge borders in a game or rewards system
- Custom-styled buttons with textured edges
- Patterned borders on photo galleries or portfolio sites
- Themed UI panels (e.g., a fantasy RPG game website)

---

## The Five Sub-Properties of `border-image`

The `border-image` shorthand brings together five individual properties. Let us understand each one before combining them.

---

### 1. `border-image-source` — The Image Path

**What it is:** This tells the browser which image file to use as the border.

**Syntax:**
```css
border-image-source: url(filename.png);
```

**Simple Example:**

```css
div {
  border: 10px solid transparent; /* required for border-image to show */
  border-image-source: url(border.png);
}
```

> **Why `transparent`?** The `border` property must be set. Using `transparent` as the colour means the solid colour does not show — only the image will be visible.

**What happens if the file path is wrong?** The border image will simply not appear. No error is shown to the user — the browser silently falls back to the regular solid border (or nothing if the colour is transparent). Always double-check your file path.

---

### 2. `border-image-slice` — How to Cut the Image

**What it is:** This is the most important sub-property. It tells the browser *where* to make the cuts when slicing the image into nine pieces.

Think of it as a knife measurement: "Cut 30 pixels in from each edge."

**Syntax options:**
```css
border-image-slice: 30;       /* 30 pixels from all four edges */
border-image-slice: 20%;      /* 20% of the image width/height from each edge */
border-image-slice: 10 20;    /* 10px top/bottom, 20px left/right */
border-image-slice: 10 20 30 40; /* top right bottom left (clockwise) */
```

**Key points:**
- The number you write is **not followed by `px`** when using pixel values (this is a quirk of this property only).
- You **can** use `%` for percentage-based slicing.
- Values are applied in clockwise order: top → right → bottom → left.

**Micro demo — pixel slice:**

```css
#box {
  border: 10px solid transparent;
  border-image-source: url(border.png);
  border-image-slice: 30;
}
```

**Micro demo — percentage slice:**

```css
#box {
  border: 10px solid transparent;
  border-image-source: url(border.png);
  border-image-slice: 20%;
}
```

> **Thinking prompt:** What do you think happens if you set the slice value very high, like 80%? The slices would overlap and the corners would take up most of the image, leaving very little for the sides. Try it!

---

### 3. `border-image-width` — The Width of the Image Border

**What it is:** This controls how wide the border image appears visually. It is similar to the `border-width` property but applies specifically to the image border.

**Syntax:**
```css
border-image-width: 1;       /* multiplier of the border-width value */
border-image-width: 20px;    /* absolute pixel width */
border-image-width: 10%;     /* percentage of element's width/height */
border-image-width: auto;    /* uses the slice size automatically */
```

**Simple Example:**

```css
#box {
  border: 10px solid transparent;
  border-image-source: url(border.png);
  border-image-slice: 30;
  border-image-width: 20px;
}
```

Here the image border will appear 20 pixels wide, regardless of the `border: 10px` value.

---

### 4. `border-image-outset` — Pushing the Border Outward

**What it is:** This property moves the border image *outside* the element's border box. Think of it as giving your frame a little extra breathing room beyond the element's edges.

**Syntax:**
```css
border-image-outset: 5px;   /* pushes 5px outward on all sides */
border-image-outset: 0;     /* default — no outward push */
```

**Simple Example:**

```css
#box {
  border: 10px solid transparent;
  border-image-source: url(border.png);
  border-image-slice: 30;
  border-image-outset: 5px;
}
```

The image border now extends 5 pixels beyond where the normal border would be.

> **Analogy:** Imagine a picture frame sitting on a table. Normally the frame sits flush with the edge of the canvas. `border-image-outset` is like sliding that frame slightly outward so it hangs over the table edge a little.

---

### 5. `border-image-repeat` — How the Sides Fill

**What it is:** After the four corners are placed, the browser needs to fill the four sides. This property tells the browser *how* to do it.

**Available values:**

| Value | Behaviour |
|-------|-----------|
| `stretch` | The side piece is stretched to fill the entire side. This is the default. |
| `round` | The side piece is tiled (repeated) and then rescaled slightly so that only whole tiles appear (no cut-off tiles). |
| `repeat` | The side piece is tiled from the middle outward. Tiles at the edges may be cut off. |
| `space` | The side piece is tiled and extra space is added between tiles to avoid cut-offs. |

**Simple Example with `stretch`:**

```css
#box {
  border: 10px solid transparent;
  border-image-source: url(border.png);
  border-image-slice: 30;
  border-image-repeat: stretch;
}
```

**Simple Example with `round`:**

```css
#box {
  border: 10px solid transparent;
  border-image-source: url(border.png);
  border-image-slice: 30;
  border-image-repeat: round;
}
```

> **When should you use which?**
> - Use `stretch` when your image is designed to scale (like a gradient or simple texture).
> - Use `round` when your image has a distinct repeating pattern (like diamonds or dots) and you want whole, uncut tiles.

---

## The Shorthand Property: `border-image`

Now that you understand each sub-property, you can combine them all into the shorthand `border-image` property.

**Full shorthand syntax:**
```css
border-image: source slice / width / outset repeat;
```

In practice, `width` and `outset` are often omitted since they have sensible defaults, and the most common usage is:

```css
border-image: url(border.png) 30 round;
/* source: url(border.png) */
/* slice: 30 */
/* repeat: round */
```

---

## Simple Standalone Examples

### Example 1 — Basic Image Border with `round`

This is the simplest possible usage:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    #borderimg {
      border: 10px solid transparent; /* REQUIRED */
      padding: 15px;
      border-image: url(border.png) 30 round;
    }
  </style>
</head>
<body>
  <div id="borderimg">An image as the border!</div>
</body>
</html>
```

**Expected visual output:**
The div will have a decorative image border where the pattern tiles (repeats) along the four sides, with the corners of the image placed at the element's corners. There will be 15 pixels of space between the text and the border due to `padding`.

**Code breakdown — line by line:**
- `border: 10px solid transparent;` → Sets up the required border. The colour is transparent so only the image shows.
- `padding: 15px;` → Adds 15px space inside the element so the text doesn't touch the border.
- `border-image: url(border.png) 30 round;` → The shorthand. File is `border.png`, sliced 30px from each edge, sides tiled with `round`.

---

### Example 2 — Basic Image Border with `stretch`

```css
#borderimg {
  border: 10px solid transparent;
  padding: 15px;
  border-image: url(border.png) 30 stretch;
}
```

**Expected visual output:**
The div will have the same corner image pieces, but the four side pieces are now stretched (squeezed or elongated) to fill each side instead of tiling.

> **Thinking prompt:** Look at both examples. When would `stretch` look bad? It looks bad when the image has a distinct repeating pattern (like diamonds), because stretching would distort the shapes. When would it look good? It looks great with gradients or simple textures.

---

### Example 3 — Different Slice Values Change the Entire Look

Changing the slice value dramatically changes the appearance:

```css
/* Example 1: Large slice value */
#borderimg1 {
  border: 10px solid transparent;
  padding: 15px;
  border-image: url(border.png) 50 round;
}

/* Example 2: Small percentage slice */
#borderimg2 {
  border: 10px solid transparent;
  padding: 15px;
  border-image: url(border.png) 20% round;
}

/* Example 3: Larger percentage slice */
#borderimg3 {
  border: 10px solid transparent;
  padding: 15px;
  border-image: url(border.png) 30% round;
}
```

**Expected visual output for each:**
- `50` → The corners take up a large 50×50 pixel area of the image, leaving a narrow middle section for the sides.
- `20%` → Corners take up 20% of the image from each edge — a moderate cut.
- `30%` → Corners take up 30% — slightly bigger corner zones than the 20% example.

> **Thinking prompt:** As the slice value increases, what do you think happens to the corners? They get bigger and more of the image is reserved for corner pieces. What happens to the side pieces? They have less image area to work with, so they may look thinner or more compressed.

---

### Example 4 — Using All Sub-Properties Separately

Instead of shorthand, you can write each property on its own line. This is often clearer for beginners:

```css
#borderimg {
  border: 10px solid transparent;
  padding: 15px;
  border-image-source: url(border.png);
  border-image-slice: 30;
  border-image-width: 15px;
  border-image-outset: 0;
  border-image-repeat: round;
}
```

**Expected visual output:**
Identical to Example 1 in appearance, but now the `border-image-width` is explicitly set to 15px and `border-image-outset` is confirmed as 0 (no outward extension).

---

### Example 5 — Percentage Slice with Stretch

```css
#borderimg {
  border: 10px solid transparent;
  padding: 15px;
  border-image: url(border.png) 15% stretch;
}
```

**Expected visual output:**
The image is sliced 15% from each edge. Corner zones are small. The side pieces are stretched across each side.

---

## Complete CSS Border Image Properties Reference

| Property | What it Does |
|----------|-------------|
| `border-image` | Shorthand for all five border-image properties combined |
| `border-image-source` | Specifies the path to the image file used as a border |
| `border-image-slice` | Specifies how to slice the image (pixel values or percentages) |
| `border-image-width` | Specifies the displayed width of the border image |
| `border-image-outset` | Specifies how far the border image extends beyond the border box |
| `border-image-repeat` | Specifies how sides are filled: `stretch`, `round`, `repeat`, or `space` |

---

## Guided Practice Exercises

### Exercise 1 — Your First Image Border (Warm-Up)

**Objective:** Apply a basic image border to a div.

**Scenario:** You are building a personal portfolio website. You want the header section to have a decorative border using an image file called `frame.png`.

**Steps:**

1. Create an HTML file with a `<div>` that has the id `header-box`.
2. Inside the div, add the text: "Welcome to My Portfolio".
3. In your CSS, write a rule for `#header-box` that:
   - Sets `border: 10px solid transparent;`
   - Sets `padding: 20px;`
   - Applies `border-image: url(frame.png) 30 round;`

**Hint:** Remember that `border` must come before `border-image` in your CSS. The browser reads properties in order.

**Expected output:**
A div with "Welcome to My Portfolio" surrounded by a decorative image border that tiles along the sides.

**Self-check questions:**
- What happens if you remove the `border` property? (The image border disappears entirely.)
- What happens if you change `round` to `stretch`? (The side pattern stretches instead of tiles.)
- What happens if you change the slice from `30` to `5`? (The corner pieces become tiny, taking only 5px of the image.)

---

### Exercise 2 — Comparing `round` and `stretch`

**Objective:** Visually compare the two most common `border-image-repeat` values.

**Scenario:** You are designing a greeting card website. You have a decorative pattern image and want to show two sample cards side-by-side.

**Steps:**

1. Create two `<div>` elements with ids `card-round` and `card-stretch`.
2. Give both divs the same padding (`20px`) and the same content text ("Happy Birthday!").
3. Apply these styles:

```css
#card-round {
  border: 15px solid transparent;
  padding: 20px;
  border-image: url(border.png) 30 round;
  margin-bottom: 20px;
}

#card-stretch {
  border: 15px solid transparent;
  padding: 20px;
  border-image: url(border.png) 30 stretch;
}
```

**Expected output:**
Two boxes. The first has a tiled border where the pattern repeats cleanly. The second has a stretched border where the pattern is squeezed or elongated along the sides.

**What-if challenge:** What if you changed `30` to `50` in both? How does the appearance change? (Larger corner zones, different amount of image area used for sides.)

**Professional connection:** In real UI design, `round` is preferred for patterns (icons, ornaments, geometric shapes), while `stretch` is used for gradients or simple textures that look fine when scaled.

---

### Exercise 3 — Playing with Slice Values

**Objective:** Understand how the slice value affects corner and side proportions.

**Scenario:** You are creating three example boxes for a CSS documentation page, each demonstrating a different slice value.

**Steps:**

Create three divs with ids `slice-a`, `slice-b`, and `slice-c`. Apply these styles:

```css
/* All three share this base setup */
#slice-a, #slice-b, #slice-c {
  border: 10px solid transparent;
  padding: 15px;
  margin: 10px 0;
  border-image-source: url(border.png);
  border-image-repeat: round;
}

/* Different slice values */
#slice-a {
  border-image-slice: 50;    /* large pixel slice */
}

#slice-b {
  border-image-slice: 20%;   /* moderate percentage slice */
}

#slice-c {
  border-image-slice: 30%;   /* larger percentage slice */
}
```

**Expected output:**
Three boxes, each with the same image but visually different because the slicing cuts the image at different points. The corner patterns will look noticeably different between the three boxes.

**Self-check questions:**
- Which slice value produces the largest corner areas? (`50` and `30%` will be larger corner zones than `20%`, depending on the image size.)
- Can you mix units? No — you must choose either unitless numbers (pixels) or percentages within a single `border-image-slice` value.

---

### Exercise 4 — Using Individual Sub-Properties

**Objective:** Write `border-image` using separate properties instead of shorthand.

**Scenario:** A teammate insists on writing CSS properties individually for readability. Rewrite the following shorthand as separate properties:

**Shorthand version (given):**
```css
#box {
  border: 10px solid transparent;
  border-image: url(border.png) 30 round;
}
```

**Your task:** Rewrite this using all five individual `border-image-*` properties. Use these values:
- Source: `border.png`
- Slice: `30`
- Width: `10px`
- Outset: `0`
- Repeat: `round`

**Answer:**

```css
#box {
  border: 10px solid transparent;
  border-image-source: url(border.png);
  border-image-slice: 30;
  border-image-width: 10px;
  border-image-outset: 0;
  border-image-repeat: round;
}
```

**Expected output:** Visually identical to the shorthand version.

**Self-check:** Is one approach better than the other? Neither is wrong. Shorthand is more concise; individual properties are more readable for beginners and easier to modify one at a time.

---

## Mini-Project: Decorative Profile Card

### Project Description

You will build a profile card component — similar to what you might see on a social media site, a gaming leaderboard, or a team directory page — with a decorative image border.

### Stage 1 — Setup: HTML Structure

Create a file called `profile-card.html`. Add this HTML structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Profile Card</title>
  <link rel="stylesheet" href="profile-card.css">
</head>
<body>

  <div class="card">
    <h2>Alex Johnson</h2>
    <p class="role">Frontend Developer</p>
    <p class="bio">Passionate about building beautiful and accessible web experiences.</p>
  </div>

</body>
</html>
```

**Milestone output:** An unstyled page showing the profile card text.

---

### Stage 2 — Core Logic: Adding the Image Border

Create a file called `profile-card.css`. Add the base styles and the image border:

```css
/* Reset and page background */
body {
  font-family: Arial, sans-serif;
  background-color: #f0f0f0;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  margin: 0;
}

/* Profile card container */
.card {
  background-color: white;
  padding: 30px 40px;
  max-width: 350px;
  text-align: center;

  /* REQUIRED: border must be set first */
  border: 15px solid transparent;

  /* Image border using shorthand */
  border-image: url(border.png) 30 round;
}
```

**Milestone output:** A white card centred on the page with a decorative image border.

---

### Stage 3 — Enhancements: Typography and Colour

Add these additional styles to `profile-card.css`:

```css
.card h2 {
  font-size: 24px;
  color: #333;
  margin-top: 0;
}

.card .role {
  font-size: 14px;
  color: #888;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin: 5px 0 15px;
}

.card .bio {
  font-size: 15px;
  color: #555;
  line-height: 1.6;
}
```

**Milestone output:** A polished card with styled text hierarchy and a decorative image border.

---

### Stage 4 — Experimenting: Try Different Border Styles

Now add three variant cards to see different effects:

```css
/* Variant A: stretch repeat */
.card-stretch {
  border: 15px solid transparent;
  border-image: url(border.png) 30 stretch;
  padding: 30px;
  margin: 20px auto;
  max-width: 350px;
  background: white;
  text-align: center;
}

/* Variant B: large pixel slice */
.card-large-slice {
  border: 15px solid transparent;
  border-image: url(border.png) 50 round;
  padding: 30px;
  margin: 20px auto;
  max-width: 350px;
  background: white;
  text-align: center;
}

/* Variant C: percentage-based slice */
.card-percent-slice {
  border: 15px solid transparent;
  border-image: url(border.png) 20% round;
  padding: 30px;
  margin: 20px auto;
  max-width: 350px;
  background: white;
  text-align: center;
}
```

Add corresponding divs to your HTML to compare all three.

**Final Output:** Three visually distinct profile card variants, each with the same image but different slicing and repeat settings.

---

### Reflection Questions for the Mini-Project

- Which card looked the most professional to you and why?
- What would happen if you used a photograph instead of a pattern image as the border source? (The corners would show parts of the photo, and the sides would show stretched or tiled strips of it.)
- How might you use `border-image-outset` to give the card frame a more "picture frame" feel?
- Could you use `border-image-repeat: space` instead of `round`? What would be different? (With `space`, gaps are added between tiles instead of rescaling them.)

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting the `border` Property

```css
/* ❌ WRONG — border-image will not show */
#box {
  padding: 15px;
  border-image: url(border.png) 30 round;
}
```

```css
/* ✅ CORRECT */
#box {
  border: 10px solid transparent; /* This line is required */
  padding: 15px;
  border-image: url(border.png) 30 round;
}
```

**Why this happens:** The `border-image` property only works when the element already has a `border` declared. Without `border`, the browser has no border area to paint the image into.

---

### Mistake 2 — Adding `px` to the Slice Value

```css
/* ❌ WRONG — px unit is invalid here */
border-image: url(border.png) 30px round;
```

```css
/* ✅ CORRECT — no unit for pixel slice */
border-image: url(border.png) 30 round;

/* ✅ ALSO CORRECT — percentage has % sign */
border-image: url(border.png) 20% round;
```

**Why this happens:** Unlike most CSS properties, `border-image-slice` pixel values are written as **plain numbers** without `px`. Using `px` makes the value invalid and the browser ignores it.

---

### Mistake 3 — Wrong File Path

```css
/* ❌ WRONG — file not found */
border-image: url(images/border.jpg) 30 round;
/* (if border.png is actually in the same folder as your CSS file) */
```

```css
/* ✅ CORRECT */
border-image: url(border.png) 30 round;
```

**Why this happens:** CSS file paths are relative to the CSS file's location, not the HTML file. Always check:
- Is the image file in the right folder?
- Is the extension correct (`.png` vs `.jpg`)?
- Is the filename spelled exactly right (case-sensitive on some servers)?

---

### Mistake 4 — Using a Colour Instead of `transparent`

```css
/* ❌ This will work but looks odd */
#box {
  border: 10px solid red; /* red colour shows behind/through the image */
  border-image: url(border.png) 30 round;
}
```

```css
/* ✅ Better: use transparent so only the image is visible */
#box {
  border: 10px solid transparent;
  border-image: url(border.png) 30 round;
}
```

**Why this matters:** Using a solid colour shows through parts of the image border that are semi-transparent (if your PNG has transparency). This creates unexpected colour blending. Use `transparent` unless you intentionally want a colour blended with the image.

---

### Mistake 5 — Expecting `border-image` to Work Without `padding`

```css
/* This works but the text may touch the border */
#box {
  border: 10px solid transparent;
  border-image: url(border.png) 30 round;
  /* no padding */
}
```

```css
/* Better: add padding so text doesn't overlap the border */
#box {
  border: 10px solid transparent;
  padding: 15px;
  border-image: url(border.png) 30 round;
}
```

**Why this matters:** `border-image` does not automatically create space between the content and the border. Always add `padding` when using `border-image` so your text or content has breathing room.

---

### Mistake 6 — Confusing `border-image-width` with `border-width`

```css
/* border-width (part of the shorthand 'border') */
border: 10px solid transparent; /* 10px = border-width */

/* border-image-width (separate property, controls image border display size) */
border-image-width: 20px;
```

These are two different things. `border-width` (in the `border` shorthand) sets up the space reserved for the border. `border-image-width` overrides how wide the image border is drawn visually. You can have different values for both.

---

## Reflection Questions

Test your understanding by thinking through these questions:

1. What would happen to a `border-image` if you set `border-image-slice: 0`? (All four slice lines would be at the very edge — no corner zones — so the entire image would be treated as a side piece. Results would look strange.)

2. If your `border-image-repeat` is set to `round` but the element is very wide, what does the browser do? (It adjusts the size of each tile slightly so that only whole, uncut tile copies fit along the side.)

3. Can you use a `linear-gradient` instead of `url()` as the `border-image-source`? Yes! CSS gradients can be used: `border-image: linear-gradient(red, blue) 1;` — this is a powerful advanced technique.

4. What happens if you set `border-image-outset` to a large value like `30px`? (The image border extends 30px beyond the element's border box, potentially overlapping surrounding content.)

5. Why might a designer prefer to write individual `border-image-*` properties rather than the shorthand? (It's clearer, easier to modify one value, and easier for teammates to read and understand each setting.)

---

## Completion Checklist

Before moving on, confirm you can do each of the following:

- [ ] Explain what `border-image` does in plain English
- [ ] Name all five `border-image` sub-properties and what each controls
- [ ] Write `border-image` using the shorthand syntax
- [ ] Write `border-image` using all five individual properties
- [ ] Explain why `border: solid transparent` must be set before `border-image`
- [ ] Apply a pixel slice value (e.g., `30`) correctly without adding `px`
- [ ] Apply a percentage slice value (e.g., `20%`) correctly
- [ ] Explain the difference between `round` and `stretch`
- [ ] Fix the six common beginner mistakes described in this lesson
- [ ] Complete the profile card mini-project

---

## Lesson Summary

The `border-image` property is a powerful CSS3 feature that lets you replace a plain border with any image file. Here is what you learned:

The **core concept** is the nine-slice technique: the browser cuts your image into a 3×3 grid and maps each piece to the correct part of the element's border — corners to corners, sides to sides.

The **five sub-properties** are:
- `border-image-source` — the image file path using `url()`
- `border-image-slice` — how deep to cut from each edge (no `px` unit for pixel values, `%` allowed)
- `border-image-width` — the visual display width of the image border
- `border-image-outset` — how far the border extends outside the element
- `border-image-repeat` — how side pieces fill: `stretch` (scale), `round` (tile with rescaling), `repeat` (tile from centre), or `space` (tile with spacing)

The **shorthand syntax** is: `border-image: url(file) slice repeat;`

The **golden rule** is: always set `border: Xpx solid transparent;` before `border-image` or the image border will not appear.

**Real-world applications** include decorative card frames, themed UI panels, certificate borders, textured button edges, and any place where a plain solid border is too plain.

---

*End of Lesson 47 — CSS Border Images*
