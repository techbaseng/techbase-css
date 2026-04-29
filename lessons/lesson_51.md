---
render_with_liquid: false
title: "CSS Shadow Effects — Text Shadows and Box Shadows"
nav_order: 51
---

# Lesson 51 — CSS Shadow Effects: Text Shadows and Box Shadows

---

## Lesson Introduction

Have you ever looked at a professional website and noticed how text seems to glow, or how buttons and cards appear to float above the page with a soft shadow underneath? That three-dimensional, polished feel is created using **CSS Shadow Effects**.

In this lesson you will learn two powerful CSS tools:

- **`text-shadow`** — adds a shadow behind text characters
- **`box-shadow`** — adds a shadow around any HTML element (a box, a card, a button, an image)

By the end of this lesson, you will be able to build beautiful, professional-looking components like raised cards, glowing headings, layered buttons, and depth-rich profile boxes — all with just a few lines of CSS.

> **Real-world use cases:**
> Shadows are used on almost every modern website — product cards on e-commerce sites, dashboard widgets, chat message bubbles, login form panels, blog post thumbnails, and navigation buttons all commonly use shadow effects to create visual depth and hierarchy.

---

## Prerequisite Concepts

Before we dive in, let's make sure you understand a few terms that will appear throughout this lesson. If you already know these, feel free to skim.

### What is CSS?

**CSS** stands for **Cascading Style Sheets**. It is the language used to style and decorate HTML elements on a webpage. While HTML creates the structure (headings, paragraphs, images), CSS controls how those elements look — their colours, sizes, fonts, and shadows.

### What is a CSS Property?

A **property** is the specific aspect of an element you want to change. Examples: `color`, `font-size`, `background-color`. In this lesson our two properties are `text-shadow` and `box-shadow`.

### What is a CSS Value?

A **value** is what you set that property to. For example, if the property is `color`, a value might be `red` or `#ff0000`.

### What is a pixel (px)?

A **pixel** is the smallest unit of display on a screen. When we write `5px`, we mean "5 pixels". Pixels are used to set sizes, distances, and blur amounts in shadow effects.

### What is an HTML element?

An **HTML element** is any building block of a webpage — a paragraph `<p>`, a heading `<h1>`, a div `<div>`, a button `<button>`, an image `<img>`, etc.

### What is rgba() colour?

`rgba(red, green, blue, alpha)` is a way to specify a colour in CSS where:
- `red`, `green`, `blue` are numbers from 0–255 controlling colour intensity
- `alpha` is a number from 0 (completely transparent) to 1 (completely opaque)

Example: `rgba(0, 0, 0, 0.5)` is a semi-transparent black shadow.

---

## Part 1 — CSS Text Shadow

### What Is Text Shadow?

Imagine shining a light on the letters of a sign. The light hits the front of each letter and casts a shadow behind it. That is exactly what `text-shadow` does in CSS — it projects a copy of the text slightly offset behind the original, creating a shadow effect.

**Why is this useful?**
- It makes text easier to read on busy or colourful backgrounds
- It gives headings a dramatic, eye-catching style
- It can simulate glowing neon text (popular in gaming and entertainment sites)
- It adds depth and professionalism to a design

### The text-shadow Property: Syntax

```css
selector {
  text-shadow: horizontal-offset vertical-offset blur-radius color;
}
```

Let's break down each part:

| Part | What It Means | Example |
|---|---|---|
| `horizontal-offset` | How far the shadow moves **left or right** (positive = right, negative = left) | `2px` |
| `vertical-offset` | How far the shadow moves **up or down** (positive = down, negative = up) | `2px` |
| `blur-radius` | How blurry/soft the shadow edges are (0 = sharp, larger = softer) | `5px` |
| `color` | The colour of the shadow | `grey` |

> **Analogy:** Think of `horizontal-offset` and `vertical-offset` as moving a torch (flashlight) to the right and downward — the shadow it casts on a wall moves left and upward from the object. In CSS, positive values move the shadow right and down.

---

### Simple Example 1 — Basic Text Shadow

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    h1 {
      text-shadow: 2px 2px grey;
    }
  </style>
</head>
<body>
  <h1>Hello World</h1>
</body>
</html>
```

**What each line does:**
- `text-shadow:` — tells the browser we want a text shadow
- `2px` (first value) — move the shadow **2 pixels to the right**
- `2px` (second value) — move the shadow **2 pixels downward**
- `grey` — the shadow colour is grey

**Expected Output:**
The heading "Hello World" appears with a grey shadow slightly to the right and below the letters, making the text look slightly raised.

> **Thinking prompt:** What happens if you change both values to `0px`? Try to predict before you test. (The shadow sits directly behind the text — you would barely see it unless it's a different colour!)

---

### Simple Example 2 — Text Shadow with Blur

```html
<style>
  h1 {
    text-shadow: 2px 2px 5px red;
  }
</style>
<h1>Warning Message</h1>
```

**What's new: the third value `5px`**
This is the **blur radius**. The higher this number, the more spread out and soft the shadow becomes.
- `0px` blur = a sharp, crisp shadow (like a shadow on a sunny day)
- `5px` blur = a soft, feathered shadow (like a shadow on a cloudy day)

**Expected Output:**
"Warning Message" with a soft, blurry red shadow extending 2px to the right and 2px down, with edges fading out.

---

### Simple Example 3 — White Text with Dark Shadow (Classic Readable Style)

```css
h1 {
  color: white;
  text-shadow: 2px 2px 4px black;
}
```

**Expected Output:**
White text with a sharp black shadow — this combination is very common in website headers placed over images, because it makes the text readable no matter what the background looks like.

> **Real-world use:** News websites and blog hero sections frequently use white text with a black text-shadow on top of background images.

---

### Simple Example 4 — Neon Glow Effect

```css
h1 {
  color: white;
  text-shadow: 0 0 3px #ff0000, 0 0 5px #ff0000, 0 0 10px #ff0000, 0 0 40px #ff0000;
  background-color: black;
}
```

**What's happening here?**
- Both offset values are `0 0` — the shadow sits directly behind the text, not shifted
- Multiple shadows are stacked (separated by commas — we'll learn this shortly)
- Each layer has a larger blur, creating a glowing halo effect

**Expected Output:**
White text on a black background with a red glow radiating outward — like a neon sign.

---

### Multiple Text Shadows

You can stack as many shadows as you want on the same text by separating them with **commas**.

**Syntax:**
```css
selector {
  text-shadow: shadow1, shadow2, shadow3;
}
```

**Example — Text with Two Shadows:**

```html
<style>
  h1 {
    color: white;
    text-shadow: 1px 1px 2px black, 0 0 25px blue, 0 0 5px darkblue;
  }
</style>
<h1>CSS Shadows</h1>
```

**Breaking down each shadow:**
- `1px 1px 2px black` → a small dark offset shadow for depth
- `0 0 25px blue` → a wide blue glow around the whole text
- `0 0 5px darkblue` → a tighter dark blue inner glow for richness

**Expected Output:**
White text with a layered combination of a dark drop shadow plus a vivid blue-purple glow effect.

---

### The text-shadow Property — Full Reference

| Value | Description | Example |
|---|---|---|
| `h-shadow` | Horizontal offset (required). Positive = right, Negative = left | `3px` or `-3px` |
| `v-shadow` | Vertical offset (required). Positive = down, Negative = up | `3px` or `-3px` |
| `blur-radius` | Optional. 0 = sharp edges. Higher = softer. Default is 0. | `5px` |
| `color` | Optional. Default is the text colour. | `grey`, `rgba(0,0,0,0.5)` |
| `none` | No shadow (default) | `text-shadow: none;` |

> **Tip:** The blur-radius and color values are optional. The minimum valid text-shadow only needs `h-shadow` and `v-shadow`. However, always include a colour so your shadow is intentional and predictable.

---

## Part 2 — CSS Box Shadow

### What Is Box Shadow?

Every HTML element in CSS is treated as a rectangle — a **box**. The `box-shadow` property adds a shadow around the outside (or inside) of that box.

**Why is box-shadow so powerful?**
- It makes cards, panels, and modals appear to "float" above the page
- It adds depth to buttons so they look clickable and physical
- It can draw the user's attention to an important element
- It can simulate a pressed/clicked effect on buttons
- Combined with `:hover`, it creates smooth interactive animations

### The box-shadow Property: Syntax

```css
selector {
  box-shadow: horizontal-offset vertical-offset blur-radius spread-radius color;
}
```

There are **5 values** for box-shadow — two more than text-shadow:

| Value | Description | Example |
|---|---|---|
| `h-shadow` | Horizontal offset. Positive = right, Negative = left (Required) | `2px` |
| `v-shadow` | Vertical offset. Positive = down, Negative = up (Required) | `2px` |
| `blur-radius` | How blurry the shadow edges are. Optional. Default 0 = sharp. | `5px` |
| `spread-radius` | How much larger/smaller the shadow is than the element. Optional. Default 0. | `3px` |
| `color` | The colour of the shadow. Optional but recommended. | `grey` |
| `inset` | Optional keyword. Makes shadow appear **inside** the element instead of outside. | `inset` |
| `none` | Removes all shadows. | `box-shadow: none;` |

---

### Simple Example 1 — Basic Box Shadow

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      width: 300px;
      height: 100px;
      background-color: lightblue;
      box-shadow: 10px 10px grey;
    }
  </style>
</head>
<body>
  <div>I have a shadow!</div>
</body>
</html>
```

**What each value does:**
- `10px` — shadow is **10 pixels to the right** of the box
- `10px` — shadow is **10 pixels below** the box
- `grey` — the shadow colour is grey

**Expected Output:**
A light blue rectangle with a solid grey shadow visible on the bottom-right, like the box is floating over a grey surface beneath it.

---

### Simple Example 2 — Box Shadow with Blur

```css
div {
  box-shadow: 10px 10px 8px grey;
}
```

**What's new:** The third value `8px` is the blur radius. The shadow edges become soft and feathered.

**Expected Output:**
A box with a blurry, diffused grey shadow — much more natural and realistic looking than the sharp version.

> **Analogy:** A sharp shadow (`blur: 0`) looks like you're outside at high noon with harsh sunlight. A blurry shadow looks like indirect or indoor lighting — softer and more natural.

---

### Simple Example 3 — Box Shadow with Spread

```css
div {
  box-shadow: 0px 0px 0px 10px red;
}
```

**Understanding spread radius:**
- The fourth value `10px` is the **spread radius**
- A positive spread makes the shadow **expand larger** than the element
- A negative spread makes the shadow **contract smaller** than the element
- With `0 0 0` for offsets and blur, but a large spread, you get a **solid colour border-like effect** all around

**Expected Output:**
A box surrounded by a thick red border-like shadow on all sides — without any offset or blur, just a uniform expansion.

---

### Simple Example 4 — Realistic Card Shadow

```css
.card {
  width: 280px;
  padding: 20px;
  background-color: white;
  box-shadow: 2px 4px 15px rgba(0, 0, 0, 0.2);
}
```

**Breaking this down:**
- `2px` horizontal offset — shadow shifts slightly right
- `4px` vertical offset — shadow shifts slightly down
- `15px` blur — very soft, spread-out shadow
- `rgba(0, 0, 0, 0.2)` — a semi-transparent black (20% opacity), which looks more natural than solid grey

**Expected Output:**
A white card that appears to hover gently above the background — the standard "material design" card effect used by Google, Twitter, and most modern web apps.

---

### Simple Example 5 — Inset Shadow

The keyword `inset` turns the shadow **inward** — it appears inside the element rather than outside it.

```css
div {
  background-color: lightblue;
  box-shadow: inset 5px 5px 10px rgba(0, 0, 0, 0.3);
}
```

**What inset does:**
- Without `inset` → shadow is outside the box (appears to float above the page)
- With `inset` → shadow is inside the box (appears to be a depression or recessed area)

**Expected Output:**
A light blue box that looks like it is sunken into the page — as if it were a pit rather than a raised surface. This is commonly used for text inputs, search bars, and pressed button states.

---

### Multiple Box Shadows

Like text-shadow, you can stack multiple box shadows on one element using commas.

```css
div {
  box-shadow: 5px 5px 10px grey, -5px -5px 10px blue;
}
```

**What this does:**
- First shadow: grey, bottom-right
- Second shadow: blue, top-left
- Combined: the element appears lit from two directions at once

**Expected Output:**
A box glowing grey on its bottom-right and blue on its top-left simultaneously.

---

### Practical Example — Hover Effect on a Button

This is one of the most common real-world uses of box-shadow: making buttons look interactive.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .btn {
      padding: 12px 24px;
      background-color: #4CAF50;
      color: white;
      border: none;
      cursor: pointer;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
      transition: box-shadow 0.3s ease;
    }

    .btn:hover {
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4);
    }
  </style>
</head>
<body>
  <button class="btn">Click Me</button>
</body>
</html>
```

**Line-by-line explanation:**

- `.btn { box-shadow: 0 4px 6px rgba(0,0,0,0.3); }` — the button has a gentle shadow at rest, making it look slightly raised
- `transition: box-shadow 0.3s ease;` — any change to the box-shadow will animate smoothly over 0.3 seconds
- `.btn:hover { box-shadow: 0 8px 20px rgba(0,0,0,0.4); }` — when you hover, the shadow gets bigger and more intense, making the button appear to lift up

**Expected Output:**
A green button. When your mouse hovers over it, the shadow expands smoothly, giving the illusion the button is rising toward you.

---

### Multiple Box Shadows — Advanced Technique

You can create very elaborate shadow effects by layering shadows. Each layer adds to the visual complexity.

```css
.card {
  width: 300px;
  padding: 20px;
  background: white;
  box-shadow:
    0 1px 3px rgba(0,0,0,0.12),
    0 1px 2px rgba(0,0,0,0.24);
  transition: box-shadow 0.3s ease;
}

.card:hover {
  box-shadow:
    0 14px 28px rgba(0,0,0,0.25),
    0 10px 10px rgba(0,0,0,0.22);
}
```

**What this achieves:**
- At rest: a subtle, natural-looking shadow (2 layers, very subtle)
- On hover: a dramatic, high-elevation shadow (the card appears to float much higher)

This technique is directly inspired by **Google's Material Design** system, which defines specific shadow layers for each "elevation level" from 0 (flat) to 24 (dialog/modal).

---

## Part 3 — Code Challenges & Guided Practice

### Exercise 1 — Add a Basic Text Shadow

**Objective:** Practice the fundamentals of `text-shadow`.

**Scenario:** You are building a website for a music event. The main heading needs a dramatic dark shadow to make it pop.

**Steps:**

1. Create an HTML file with the following structure:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Your CSS goes here */
    body {
      background-color: #1a1a2e;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    h1 {
      color: white;
      font-size: 48px;
      /* ADD YOUR TEXT SHADOW HERE */
    }
  </style>
</head>
<body>
  <h1>NIGHT FESTIVAL 2025</h1>
</body>
</html>
```

2. Add a `text-shadow` to the `h1` that:
   - Moves the shadow 3 pixels right
   - Moves the shadow 3 pixels down
   - Has a blur radius of 10 pixels
   - Is coloured `rgba(0, 200, 255, 0.8)` (a glowing cyan)

**Hint:** The syntax is `text-shadow: h v blur color;`

**Expected Output:**
White heading text on a dark navy background, with a soft glowing cyan shadow — an effect typical of event/festival websites.

**Answer:**
```css
h1 {
  color: white;
  font-size: 48px;
  text-shadow: 3px 3px 10px rgba(0, 200, 255, 0.8);
}
```

**Self-check questions:**
- What happens if you increase the blur from 10px to 50px? (The glow spreads much wider, text feels hazier)
- What happens if you use a negative horizontal value like `-3px`? (The shadow moves to the left)

---

### Exercise 2 — Create a Floating Product Card

**Objective:** Build a product card using `box-shadow` to make it look elevated.

**Scenario:** You are building an online shop. Product cards should look clean and professional, as if they are floating above the page.

**Starter code:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      background-color: #f0f2f5;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .product-card {
      width: 250px;
      padding: 20px;
      background-color: white;
      border-radius: 8px;
      /* ADD YOUR BOX SHADOW HERE */
    }
    .product-card h2 {
      margin: 0 0 10px 0;
    }
    .product-card p {
      color: #666;
    }
    .product-card .price {
      font-size: 24px;
      font-weight: bold;
      color: #4CAF50;
    }
  </style>
</head>
<body>
  <div class="product-card">
    <h2>Wireless Headphones</h2>
    <p>Premium sound quality with active noise cancellation.</p>
    <div class="price">$89.99</div>
  </div>
</body>
</html>
```

**Task:** Add a `box-shadow` to `.product-card` that:
- Has no horizontal or vertical offset (centered shadow)
- Has a blur of 20px
- Has a spread of 0
- Is a semi-transparent black at 15% opacity

**Hint:** Use `rgba(0, 0, 0, 0.15)` for the colour.

**Expected Output:**
A white card centered on a grey background with a soft shadow around all sides, looking professional and elevated.

**Answer:**
```css
.product-card {
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.15);
}
```

**Optional challenge:** Add a `:hover` state that increases the shadow to `0 8px 30px rgba(0,0,0,0.25)` with a smooth transition. What does the card feel like when you hover?

---

### Exercise 3 — Inset Shadow for a Search Bar

**Objective:** Use `inset` box-shadow to make a text input look like a recessed field.

```html
<style>
  input[type="text"] {
    width: 300px;
    padding: 10px 15px;
    border: 1px solid #ccc;
    border-radius: 25px;
    font-size: 16px;
    outline: none;
    /* ADD INSET SHADOW HERE */
  }

  input[type="text"]:focus {
    /* ADD FOCUSED INSET SHADOW HERE */
    border-color: #4A90E2;
  }
</style>

<input type="text" placeholder="Search...">
```

**Task:**
1. Add `box-shadow: inset 2px 2px 6px rgba(0, 0, 0, 0.15);` to the normal state
2. Add `box-shadow: inset 3px 3px 8px rgba(0, 0, 0, 0.2);` to the `:focus` state

**Expected Output:**
A rounded search bar that looks slightly sunken. When you click inside it, it deepens slightly and gets a blue border — a polished, modern UI element.

---

## Part 4 — Mini Project: Profile Card with Full Shadow Styling

In this mini-project you will bring together `text-shadow` and `box-shadow` to build a complete, professional-looking profile card.

### Project Goal

Build a user profile card that includes:
- A name heading with a subtle text shadow
- A card container with a multi-layer box shadow
- An avatar placeholder with an inset shadow
- A button with a hover shadow effect

### Stage 1 — Setup: HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Profile Card</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="card">
    <div class="avatar">AJ</div>
    <h2 class="name">Amara Johnson</h2>
    <p class="role">Senior UI Designer</p>
    <p class="bio">Crafting beautiful digital experiences with 6 years of expertise in user-centred design.</p>
    <button class="btn">View Portfolio</button>
  </div>
</body>
</html>
```

**Milestone 1 Output:** A plain, unstyled card with text stacked vertically. No shadows yet.

---

### Stage 2 — Core Layout and Base Styles

Create `style.css`:

```css
/* Reset and body */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background-color: #eef2f7;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  font-family: Arial, sans-serif;
}

/* Card container */
.card {
  width: 300px;
  padding: 30px 24px;
  background-color: #ffffff;
  border-radius: 16px;
  text-align: center;
}

/* Avatar circle */
.avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background-color: #4A90E2;
  color: white;
  font-size: 28px;
  font-weight: bold;
  line-height: 80px;
  margin: 0 auto 16px auto;
}

/* Name */
.name {
  font-size: 22px;
  margin-bottom: 4px;
  color: #1a1a2e;
}

/* Role */
.role {
  font-size: 14px;
  color: #4A90E2;
  margin-bottom: 12px;
  text-transform: uppercase;
  letter-spacing: 1px;
}

/* Bio */
.bio {
  font-size: 14px;
  color: #666;
  line-height: 1.6;
  margin-bottom: 20px;
}

/* Button */
.btn {
  padding: 10px 24px;
  background-color: #4A90E2;
  color: white;
  border: none;
  border-radius: 25px;
  font-size: 14px;
  cursor: pointer;
}
```

**Milestone 2 Output:** A clean, centred white card with a blue avatar circle, but it still looks flat and lacks depth.

---

### Stage 3 — Adding Shadows (The Magic!)

Now add the shadow effects to bring the card to life:

```css
/* Card - multi-layer box shadow for depth */
.card {
  /* (add to existing .card rule) */
  box-shadow:
    0 2px 4px rgba(0, 0, 0, 0.08),
    0 8px 24px rgba(0, 0, 0, 0.12);
  transition: box-shadow 0.3s ease, transform 0.3s ease;
}

/* Card hover - elevate the card */
.card:hover {
  box-shadow:
    0 4px 8px rgba(0, 0, 0, 0.1),
    0 16px 40px rgba(0, 0, 0, 0.2);
  transform: translateY(-4px);
}

/* Avatar - inset shadow to look like a photo well */
.avatar {
  /* (add to existing .avatar rule) */
  box-shadow:
    inset 0 2px 6px rgba(0, 0, 0, 0.2),
    0 4px 10px rgba(74, 144, 226, 0.4);
}

/* Name - subtle text shadow for polish */
.name {
  /* (add to existing .name rule) */
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
}

/* Button - shadow and hover effect */
.btn {
  /* (add to existing .btn rule) */
  box-shadow: 0 4px 12px rgba(74, 144, 226, 0.4);
  transition: box-shadow 0.3s ease, transform 0.2s ease;
}

.btn:hover {
  box-shadow: 0 6px 20px rgba(74, 144, 226, 0.6);
  transform: translateY(-2px);
}

.btn:active {
  box-shadow: inset 0 2px 6px rgba(0, 0, 0, 0.2);
  transform: translateY(0);
}
```

**Milestone 3 Output:**
- The card appears to float over the background
- Hovering raises the card with a more dramatic shadow
- The avatar has depth (inset shadow inside + coloured outer glow)
- The name has a barely-there text shadow for crispness
- The button glows blue and rises on hover, then appears pressed (inset) on click

---

### Stage 4 — Complete Combined File

Here is the complete, final version:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Profile Card</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      background-color: #eef2f7;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      font-family: Arial, sans-serif;
    }

    .card {
      width: 300px;
      padding: 30px 24px;
      background-color: #ffffff;
      border-radius: 16px;
      text-align: center;
      box-shadow:
        0 2px 4px rgba(0, 0, 0, 0.08),
        0 8px 24px rgba(0, 0, 0, 0.12);
      transition: box-shadow 0.3s ease, transform 0.3s ease;
    }

    .card:hover {
      box-shadow:
        0 4px 8px rgba(0, 0, 0, 0.1),
        0 16px 40px rgba(0, 0, 0, 0.2);
      transform: translateY(-4px);
    }

    .avatar {
      width: 80px;
      height: 80px;
      border-radius: 50%;
      background-color: #4A90E2;
      color: white;
      font-size: 28px;
      font-weight: bold;
      line-height: 80px;
      margin: 0 auto 16px auto;
      box-shadow:
        inset 0 2px 6px rgba(0, 0, 0, 0.2),
        0 4px 10px rgba(74, 144, 226, 0.4);
    }

    .name {
      font-size: 22px;
      margin-bottom: 4px;
      color: #1a1a2e;
      text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
    }

    .role {
      font-size: 14px;
      color: #4A90E2;
      margin-bottom: 12px;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    .bio {
      font-size: 14px;
      color: #666;
      line-height: 1.6;
      margin-bottom: 20px;
    }

    .btn {
      padding: 10px 24px;
      background-color: #4A90E2;
      color: white;
      border: none;
      border-radius: 25px;
      font-size: 14px;
      cursor: pointer;
      box-shadow: 0 4px 12px rgba(74, 144, 226, 0.4);
      transition: box-shadow 0.3s ease, transform 0.2s ease;
    }

    .btn:hover {
      box-shadow: 0 6px 20px rgba(74, 144, 226, 0.6);
      transform: translateY(-2px);
    }

    .btn:active {
      box-shadow: inset 0 2px 6px rgba(0, 0, 0, 0.2);
      transform: translateY(0);
    }
  </style>
</head>
<body>
  <div class="card">
    <div class="avatar">AJ</div>
    <h2 class="name">Amara Johnson</h2>
    <p class="role">Senior UI Designer</p>
    <p class="bio">Crafting beautiful digital experiences with 6 years of expertise in user-centred design.</p>
    <button class="btn">View Portfolio</button>
  </div>
</body>
</html>
```

**Final Output:** A polished, interactive profile card with depth, hover animations, and professional shadow styling — the kind of component you would find on a real portfolio or team directory page.

**Reflection Questions:**
- Which shadow had the biggest visual impact on the design?
- How does `transform: translateY(-4px)` on hover combine with `box-shadow` to create a rising effect?
- What would happen if you removed the `transition` property? (Changes would be instant/jerky instead of smooth)
- Can you extend this card to include social media icon buttons, each with their own coloured shadow?

---

## Common Beginner Mistakes

### Mistake 1 — Missing Required Values

```css
/* ❌ WRONG — color provided but both offsets are missing */
h1 {
  text-shadow: grey;
}

/* ✅ CORRECT — both horizontal and vertical offsets are required */
h1 {
  text-shadow: 2px 2px grey;
}
```

`text-shadow` and `box-shadow` both require at least the two offset values. Providing only a colour will not work.

---

### Mistake 2 — Wrong Value Order

```css
/* ❌ WRONG — color listed before blur */
div {
  box-shadow: 5px 5px grey 10px;
}

/* ✅ CORRECT — order is: h-offset v-offset blur spread color */
div {
  box-shadow: 5px 5px 10px 0px grey;
}
```

CSS properties are position-sensitive. The values must appear in the correct order.

---

### Mistake 3 — Using text-shadow on a div Instead of text-shadow on Text Elements

```css
/* ❌ Applies shadow to the box, not the text */
div {
  text-shadow: 2px 2px black; /* This affects text INSIDE the div */
  box-shadow: 2px 2px black; /* This affects the BOX itself */
}
```

`text-shadow` does affect text inside any element (paragraphs, divs, buttons), but remember the difference:
- `text-shadow` → shadows the **characters/letters**
- `box-shadow` → shadows the **rectangular container**

---

### Mistake 4 — Forgetting `inset` Goes First

```css
/* ❌ WRONG — inset is at the end */
div {
  box-shadow: 5px 5px 10px rgba(0,0,0,0.3) inset;
}

/* ✅ CORRECT — inset keyword goes at the beginning or end, but conventionally first */
div {
  box-shadow: inset 5px 5px 10px rgba(0,0,0,0.3);
}
```

While `inset` technically works at either end, it is conventional and most readable at the start.

---

### Mistake 5 — Too Many Heavy Shadows Slow Down Performance

```css
/* ⚠️ Avoid on many elements — each shadow is re-rendered on every repaint */
.many-cards {
  box-shadow:
    0 1px 2px black,
    0 2px 4px black,
    0 4px 8px black,
    0 8px 16px black,
    0 16px 32px black,
    0 32px 64px black;
}
```

Multiple heavy shadows on many elements can affect page scroll performance, especially on mobile. Use 1–3 shadow layers maximum for best practice.

---

### Mistake 6 — Using Harsh Opaque Black Instead of Transparent Shadow

```css
/* ❌ Looks unnatural — harsh and heavy */
.card {
  box-shadow: 5px 5px 10px black;
}

/* ✅ Natural and subtle — semi-transparent */
.card {
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.2);
}
```

Real-world shadows are never fully opaque. Using `rgba` with 10–30% opacity creates much more professional and natural-looking results.

---

### Mistake 7 — Confusing blur and spread

```css
/* blur-radius = how fuzzy the edges are */
/* spread-radius = how large the shadow is */

div {
  box-shadow: 0 0 20px 0 red;  /* Large blur, normal size shadow */
}

div {
  box-shadow: 0 0 0 20px red;  /* No blur, very large shadow (like a border) */
}
```

These two values do very different things. Blur makes edges soft. Spread makes the shadow physically larger.

---

## Reflection Questions

1. What is the difference between `text-shadow` and `box-shadow`?
2. If you set `blur-radius` to `0`, what does the shadow look like?
3. What does the `inset` keyword do to a box shadow?
4. What is the purpose of the `spread-radius` in `box-shadow`?
5. How would you create a glowing neon text effect using `text-shadow`?
6. Why is `rgba(0, 0, 0, 0.15)` often preferred over `grey` for shadows?
7. How do you add multiple shadows to one element?
8. In what order must `box-shadow` values appear?
9. What is the difference between blur and spread in box-shadow?
10. How can you use `:hover` and `transition` with `box-shadow` to create an interactive button?

---

## Completion Checklist

Before moving to the next lesson, confirm you can do each of the following:

- [ ] I understand what `text-shadow` does and how to write it
- [ ] I can identify all four parts of a text-shadow value (h-offset, v-offset, blur, colour)
- [ ] I understand what `box-shadow` does and how it differs from text-shadow
- [ ] I can identify all six parts of a box-shadow value (inset, h-offset, v-offset, blur, spread, colour)
- [ ] I know what `blur-radius` controls (softness/feathering of edges)
- [ ] I know what `spread-radius` controls (size of the shadow relative to the element)
- [ ] I know what `inset` does (turns the shadow inward)
- [ ] I can write multiple shadows on one element using commas
- [ ] I understand why `rgba()` is preferred over solid colours for shadows
- [ ] I completed Exercise 1 (text-shadow on an event heading)
- [ ] I completed Exercise 2 (box-shadow on a product card)
- [ ] I completed Exercise 3 (inset shadow on a search bar)
- [ ] I built the Profile Card mini-project
- [ ] I understand the common mistakes and how to avoid them
- [ ] I can explain how shadows + transitions create interactive hover effects

---

## Lesson Summary

In this lesson you mastered **CSS Shadow Effects** — one of the most widely used styling techniques in modern web design.

**Text Shadow (`text-shadow`):**
- Adds a shadow behind letter characters
- Takes 2 required values (h-offset, v-offset) and 2 optional values (blur, colour)
- Multiple shadows are separated by commas
- Used for stylised headings, readable text over images, glow effects

**Box Shadow (`box-shadow`):**
- Adds a shadow around the rectangular box of any HTML element
- Takes 2 required values (h-offset, v-offset) and up to 4 optional values (blur, spread, colour, inset)
- `inset` places the shadow inside the element
- Multiple shadows are separated by commas
- Used for cards, buttons, modals, inputs, panels

**Key professional techniques you learned:**
- Using `rgba()` for natural, realistic shadow colours
- Layering multiple shadows for depth and complexity
- Combining `box-shadow` with `:hover` and `transition` for smooth interactive effects
- Using `inset` for recessed inputs and pressed-button states
- Creating glow effects with zero-offset shadows and large blur values

**Real-world applications:**
Shadows are used in e-commerce product cards, login panels, dashboard widgets, navigation buttons, form inputs, mobile app UI, chat bubbles, popup modals, and virtually every modern web interface.

> You now have the skills to add professional, polished depth to any web design. In the next lesson, you will continue building your advanced CSS toolkit.

---

*Sources: W3Schools CSS Shadow Effects (https://www.w3schools.com/css/css3_shadows.asp) and W3Schools CSS Box Shadow (https://www.w3schools.com/css/css3_shadows_box.asp)*
