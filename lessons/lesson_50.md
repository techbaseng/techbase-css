---
render_with_liquid: false
title: "CSS Gradients – Linear, Radial, and Conic"
nav_order: 50
---

# Lesson 50 — CSS Gradients: Linear, Radial, and Conic

---

## Lesson Introduction

Have you ever looked at a beautiful website and noticed a background that smoothly changes from one colour into another — like a sunset going from orange to purple? That is called a **gradient**, and CSS makes it surprisingly easy to create them.

In this lesson you will learn all three types of CSS gradients:

- **Linear gradients** — colours flow in a straight line (top to bottom, left to right, or at any angle you choose)
- **Radial gradients** — colours radiate outward from a central point, like the glow of a lamp
- **Conic gradients** — colours rotate around a centre point, like the slices of a pie chart or the hands of a clock

By the end of this lesson you will be able to add rich, professional-looking colour effects to any webpage element — no images needed. You will also complete a mini-project that combines all three gradient types into a beautiful webpage card.

> 💡 **Why does this matter in the real world?**
> Gradients are everywhere: hero banners on landing pages, app icons, data visualisation backgrounds, button hover effects, and chart colour fills. Knowing how to create them with pure CSS means you never have to rely on an image file just for a colour effect — which makes your pages faster and easier to maintain.

---

## Prerequisite Concepts

Before we dive into gradients, make sure you understand these basic ideas. If any of them are new to you, read the short explanation below before continuing.

### What is CSS?

CSS stands for **Cascading Style Sheets**. It is the language used to style HTML elements — controlling their colours, sizes, fonts, positions, and much more.

### What is a CSS property?

A CSS property is an instruction you give to the browser. For example:

```css
color: red;
```

This tells the browser to make text red. The part before the colon (`color`) is the **property name**. The part after (`red`) is the **value**.

### What is `background-image`?

`background-image` is the CSS property used to set a background on an element. Normally you might point it at an image file:

```css
background-image: url("photo.jpg");
```

But CSS gradient functions are used **inside** `background-image` — they generate the colour pattern for you, with no image file needed:

```css
background-image: linear-gradient(red, yellow);
```

### What is a function in CSS?

A CSS function is a built-in tool that takes inputs inside parentheses `()` and produces an output. For example:

```css
background-image: linear-gradient(red, yellow);
/*               ^ function name  ^ inputs     */
```

The function `linear-gradient()` takes colour names (and other optional inputs) and produces a smooth colour transition.

### What is `rgba()`?

`rgba()` is a way to write a colour in CSS using Red, Green, Blue, and Alpha (transparency):

```css
rgba(255, 0, 0, 1)    /* fully opaque red   */
rgba(255, 0, 0, 0.5)  /* 50% transparent red */
rgba(255, 0, 0, 0)    /* fully transparent   */
```

The fourth number (the alpha) ranges from `0` (invisible) to `1` (fully visible).

---

## Part 1 — CSS Linear Gradients

### 1.1 What Is a Linear Gradient?

A **linear gradient** is a smooth colour transition that travels in a **straight line**. Think of it like painting a wall where your roller brush starts with one colour and gradually becomes another colour as it moves across the wall.

**The key rule:** a linear gradient must have **at least two colour stops**. A colour stop is simply a colour you want to include in the transition.

**Where does it go?** You put it inside the `background-image` property:

```css
background-image: linear-gradient(direction, color1, color2);
```

- `direction` — where the gradient flows (optional; default is top to bottom)
- `color1`, `color2` — the colours to blend between

---

### 1.2 Direction — Top to Bottom (the Default)

When you do not specify a direction, the gradient flows from the **top** of the element downward to the **bottom**. This is the default behaviour.

**Example 1 — Simplest possible linear gradient:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    #box {
      width: 300px;
      height: 150px;
      background-image: linear-gradient(red, yellow);
    }
  </style>
</head>
<body>
  <div id="box"></div>
</body>
</html>
```

**What you will see:** A rectangle that is red at the top, gradually blending into yellow at the bottom.

You can also write the direction explicitly as `to bottom`:

```css
background-image: linear-gradient(to bottom, red, yellow);
```

This produces exactly the same result as not specifying a direction.

> 🤔 **Thinking prompt:** What would happen if you swapped the colours — `linear-gradient(yellow, red)`? Try to predict it before experimenting!

---

### 1.3 Direction — Bottom to Top

To make the gradient flow upward, use `to top`:

```css
#box {
  background-image: linear-gradient(to top, red, yellow);
}
```

**What you will see:** The box starts red at the **bottom** and fades into yellow at the **top**.

Think of it like sunrise — the warm colour rises from the bottom.

---

### 1.4 Direction — Left to Right

```css
#box {
  background-image: linear-gradient(to right, red, yellow);
}
```

**What you will see:** Red on the left side, smoothly blending to yellow on the right — like a horizontal colour sweep.

---

### 1.5 Direction — Diagonal

You can make a gradient travel diagonally by combining two directions:

```css
#box {
  background-image: linear-gradient(to bottom right, red, yellow);
}
```

**What you will see:** The gradient flows from the **top-left** corner (red) toward the **bottom-right** corner (yellow).

Other diagonal options include `to top right`, `to top left`, and `to bottom left`.

---

### 1.6 Using Angles for Precise Control

Instead of words like `to right`, you can use a **degree angle** for exact control over the direction. Think of it like a clock:

| Angle value | Same as         |
|-------------|-----------------|
| `0deg`      | `to top`        |
| `90deg`     | `to right`      |
| `180deg`    | `to bottom`     |
| `270deg`    | `to left`       |
| `45deg`     | to top-right    |
| `135deg`    | to bottom-right |

**Syntax:**

```css
background-image: linear-gradient(angle, color1, color2);
```

**Example — 45-degree gradient:**

```css
#box {
  background-image: linear-gradient(45deg, red, yellow);
}
```

**What you will see:** A diagonal gradient flowing at 45 degrees from the bottom-left (red) to the top-right (yellow).

**Example — 180-degree gradient (same as default top-to-bottom):**

```css
#box {
  background-image: linear-gradient(180deg, red, yellow);
}
```

> 🤔 **Thinking prompt:** What angle would you use to make the gradient flow from right to left?

---

### 1.7 Multiple Colour Stops

You are not limited to just two colours. You can include **as many colour stops as you like**, separated by commas:

**Example — Three colours:**

```css
#box {
  background-image: linear-gradient(red, yellow, green);
}
```

**What you will see:** Red at the top → yellow in the middle → green at the bottom.

**Example — Rainbow gradient (seven colours, left to right):**

```css
#box {
  background-image: linear-gradient(
    to right,
    red, orange, yellow, green, blue, indigo, violet
  );
}
```

**What you will see:** A full rainbow flowing horizontally across the element.

The browser automatically spaces each colour evenly unless you specify positions manually (which we will cover in the exercise section).

---

### 1.8 Using Transparency in Gradients

CSS gradients support transparency. This is useful for **fading effects** — for example, having an element fade from invisible to a colour, or having a colour overlay that fades out.

You create transparency using `rgba()`:

```css
rgba(255, 0, 0, 0)   /* transparent red (invisible) */
rgba(255, 0, 0, 1)   /* fully opaque red */
```

**Example — Fade from transparent to red (left to right):**

```css
#box {
  background-image: linear-gradient(
    to right,
    rgba(255, 0, 0, 0),
    rgba(255, 0, 0, 1)
  );
}
```

**What you will see:** The left side is completely transparent (you see the element's default background or the page background), and the right side is fully red. This creates a beautiful fade-in effect.

**Real-world use:** This technique is used on websites to create image overlays, text-readable gradients over photos, and colour-blending effects in data dashboards.

---

### 1.9 Repeating Linear Gradients

The `repeating-linear-gradient()` function tiles your gradient pattern repeatedly across the element, like a striped wallpaper.

**Syntax:**

```css
background-image: repeating-linear-gradient(color1, color2 stop1, color3 stop2);
```

The numbers after the colours are **position stops** — they tell the browser where in the pattern that colour should be at (using percentages or pixels).

**Example — Repeating red, yellow, and green stripes:**

```css
#box {
  background-image: repeating-linear-gradient(
    red,
    yellow 10%,
    green 20%
  );
}
```

**What you will see:** A pattern of red → yellow → green → red → yellow → green → ... repeating all the way down the element, like candy stripes.

**Breaking down the code:**
- `red` — the pattern starts with red at 0%
- `yellow 10%` — yellow is reached at 10% of the element's size
- `green 20%` — green is reached at 20%
- After 20%, the whole pattern repeats from the beginning

---

## Part 2 — CSS Radial Gradients

### 2.1 What Is a Radial Gradient?

A **radial gradient** radiates outward from a **centre point**, like ripples in water when you drop a stone, or the glow of a light bulb.

Instead of colours moving in a straight line, they move outward in an **oval or circular shape**.

The CSS function is `radial-gradient()`.

**Basic syntax:**

```css
background-image: radial-gradient(shape size at position, color1, color2, ...);
```

At minimum, you just need two colours:

```css
background-image: radial-gradient(red, yellow);
```

**What you will see:** Red in the centre of the element, gradually blending to yellow at the edges.

---

### 2.2 Radial Gradient — Evenly Spaced Colour Stops

By default, multiple colours are spaced evenly in a radial gradient:

**Example — Three evenly spaced colours:**

```css
#box {
  background-image: radial-gradient(red, yellow, green);
}
```

**What you will see:** Red at the centre → yellow in the middle ring → green at the outer edges.

---

### 2.3 Radial Gradient — Differently Spaced Colour Stops

You can control **exactly where** each colour appears by giving it a percentage position:

**Example — Colour stops at specific positions:**

```css
#box {
  background-image: radial-gradient(red 5%, yellow 15%, green 60%);
}
```

**What you will see:**
- Red occupies only the very centre (up to 5% of the radius)
- Yellow appears from 5% to 15%
- Green fills from 15% all the way to 60%, then continues to the edges

Compare this with the evenly-spaced example — notice how much more red is visible when the stops are forced apart.

---

### 2.4 Shape — Circle vs Ellipse

By default, the radial gradient shape follows the shape of the element. If your element is wider than it is tall (a rectangle), the gradient will be **elliptical** (oval-shaped). If the element is perfectly square, it will be **circular**.

You can force the shape with the `circle` or `ellipse` keyword:

**Example — Forced circular gradient:**

```css
#box {
  background-image: radial-gradient(circle, red, yellow, green);
}
```

**What you will see:** Even if the box is a rectangle, the gradient radiates outward in a perfect circle from the centre.

**Example — Ellipse (default):**

```css
#box {
  background-image: radial-gradient(ellipse, red, yellow, green);
}
```

**What you will see:** The gradient spreads in an oval shape, stretching to match the element's proportions.

> 🤔 **Thinking prompt:** When would you use a circle vs. an ellipse? Hint: think about icon designs vs. banner backgrounds.

---

### 2.5 Size Keywords — Controlling How Far the Gradient Extends

You can control where the gradient "ends" relative to the element using these size keywords:

| Keyword           | Meaning                                                                 |
|-------------------|-------------------------------------------------------------------------|
| `closest-side`    | Gradient ends at the nearest side of the element from the centre        |
| `farthest-side`   | Gradient ends at the farthest side of the element from the centre       |
| `closest-corner`  | Gradient ends at the nearest corner of the element from the centre      |
| `farthest-corner` | Gradient ends at the farthest corner (this is the **default**)         |

**Example — Closest-side ellipse:**

```css
#box {
  background-image: radial-gradient(closest-side at 60% 55%, red, yellow, black);
}
```

**What this does:**
- `closest-side` — the gradient stops as soon as it hits the nearest side
- `at 60% 55%` — the centre of the gradient is placed 60% from the left and 55% from the top (off-centre)
- The gradient radiates: red → yellow → black

**Example — Farthest-side circle:**

```css
#box {
  background-image: radial-gradient(farthest-side at 60% 55%, red, yellow, black);
}
```

**What changes:** The gradient now extends all the way to the farthest side, making a larger visible spread of colour.

---

### 2.6 Changing the Position of the Centre Point

By default, the gradient radiates from the very **centre** of the element. You can move it anywhere using the `at` keyword followed by X and Y positions:

```css
background-image: radial-gradient(circle at x-position y-position, colors...);
```

**Example — Centre in the top-left corner:**

```css
#box {
  background-image: radial-gradient(circle at left top, red, yellow, green);
}
```

**What you will see:** The gradient originates from the top-left corner and radiates outward toward the bottom-right.

Other position keywords you can use: `right`, `left`, `top`, `bottom`, `center`, or percentages like `at 20% 80%`.

---

### 2.7 Repeating Radial Gradients

Just like linear gradients can repeat, so can radial gradients — the pattern tiles outward in concentric rings.

**Example — Repeating radial gradient:**

```css
#box {
  background-image: repeating-radial-gradient(red, yellow 10%, green 15%);
}
```

**What you will see:** Concentric rings of red → yellow → green → red → yellow → green → ... radiating outward from the centre, like a target or a bullseye pattern.

**Real-world use:** This is used for creating target graphics, ripple effects in backgrounds, and decorative pattern fills.

---

## Part 3 — CSS Conic Gradients

### 3.1 What Is a Conic Gradient?

A **conic gradient** is a colour transition that **rotates around a centre point**. Instead of colours spreading outward (like radial) or flowing in a line (like linear), colours sweep around in a circle — like the hands of a clock moving, or the slices of a pie chart.

The CSS function is `conic-gradient()`.

Imagine standing at the centre of a room and slowly turning around 360 degrees — the wall changes colour as you spin. That is exactly how a conic gradient works.

**Basic syntax:**

```css
background-image: conic-gradient(color1, color2, ...);
```

**Example — Simplest conic gradient:**

```css
#box {
  background-image: conic-gradient(red, yellow);
}
```

**What you will see:** Starting from the top (12 o'clock position), the colour sweeps clockwise from red all the way around to yellow, completing a full 360-degree rotation.

---

### 3.2 Conic Gradient — Multiple Colour Stops

You can include multiple colours, and they will be evenly distributed around the 360-degree circle:

**Example — Five colours:**

```css
#box {
  background-image: conic-gradient(red, yellow, green, blue, black);
}
```

**What you will see:** Five colour slices arranged in a full circle, like a colour wheel.

---

### 3.3 Conic Gradient — Adding a Starting Angle with `from`

By default, the gradient starts at the **top** (0 degrees = 12 o'clock). You can rotate the starting point using the `from` keyword:

```css
background-image: conic-gradient(from angle, colors...);
```

**Example — Starting at 90 degrees (3 o'clock position):**

```css
#box {
  background-image: conic-gradient(from 90deg, red, yellow, green);
}
```

**What you will see:** The gradient begins at the right side of the circle (3 o'clock) and sweeps clockwise through red → yellow → green.

---

### 3.4 Conic Gradient — Moving the Centre Point

Just like radial gradients, you can move the centre of a conic gradient away from the middle of the element using `at`:

```css
background-image: conic-gradient(from angle at x y, colors...);
```

**Example — Off-centre conic gradient:**

```css
#box {
  background-image: conic-gradient(from 90deg at 60% 45%, red, yellow, green);
}
```

**What you will see:** The sweeping gradient originates from a point slightly right of centre and above centre, creating an asymmetric, dynamic look.

---

### 3.5 Creating a Pie Chart with Conic Gradients

This is one of the most powerful real-world uses of conic gradients. By specifying **sharp stops** (two values at the same position), you can create a clean pie chart with no blending between slices.

**How sharp colour stops work:**

Normally, `conic-gradient(red 40%, blue 40%)` would mean:
- Red from 0° to 40% of the circle (144°)
- Blue picks up exactly where red ends (at 40%), so there is NO blur at the boundary

**Example — Simple pie chart (three sections):**

```css
#pie {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  background-image: conic-gradient(
    red    0%  40%,
    yellow 40% 70%,
    blue   70% 100%
  );
}
```

**What you will see:** A perfect pie chart divided into three slices — red (40%), yellow (30%), and blue (30%).

**Why `border-radius: 50%`?** This turns the square `div` into a circle, which is the typical shape for a pie chart.

---

### 3.6 Repeating Conic Gradients

The `repeating-conic-gradient()` function repeats the colour pattern around the circle.

**Example — Striped cone pattern:**

```css
#box {
  background-image: repeating-conic-gradient(red 10%, yellow 20%);
}
```

**What you will see:** Alternating red and yellow wedge slices rotating all the way around the circle — like a beach ball or a pinwheel.

**Example — Checkerboard pattern using conic gradients:**

```css
#checkerboard {
  background-image: repeating-conic-gradient(
    #000 0% 25%,
    #fff 25% 50%
  );
  background-size: 60px 60px;
}
```

**What you will see:** A black-and-white checkerboard — surprisingly, this is created using a repeating conic gradient tiled with `background-size`!

---

## Part 4 — Guided Practice Exercises

### Exercise 1 — Directional Linear Gradients

**Objective:** Practice applying linear gradients in different directions.

**Scenario:** You are styling a news website's article banner. Each article category has a different gradient theme.

**Steps:**

1. Create an HTML file with four `div` elements, each `300px` wide and `100px` tall.
2. Apply these gradients, one per div:

```css
/* Sports section */
.sports {
  background-image: linear-gradient(to right, #e96c00, #ffd700);
}

/* Technology section */
.tech {
  background-image: linear-gradient(135deg, #0052cc, #00aaff);
}

/* Health section */
.health {
  background-image: linear-gradient(to bottom, #2ecc71, #a8e6cf);
}

/* Entertainment section */
.entertainment {
  background-image: linear-gradient(45deg, #9b59b6, #e056fd);
}
```

**Expected output:** Four colourful banners showing gradients going in four different directions.

**Self-check questions:**
- Which direction does `135deg` flow? (Hint: imagine a clock hand pointing to 4:30)
- What would happen if you changed `to right` to `to left` in the sports banner?

**What-if challenge:** Try adding a third colour to the technology banner between blue and light blue.

---

### Exercise 2 — Fading Overlay Effect

**Objective:** Use transparency to create a text-readable overlay on a coloured element.

**Scenario:** A photography website wants a gradient overlay so that white text on the left side remains readable against a coloured image background.

**Steps:**

1. Create a `div` that is `400px` wide and `200px` tall with a coloured background.
2. Apply a gradient overlay that fades from a dark semi-transparent colour on the left to fully transparent on the right.

```html
<style>
  .photo-card {
    width: 400px;
    height: 200px;
    background-color: #3498db;  /* acts as the "photo" colour */
    background-image: linear-gradient(
      to right,
      rgba(0, 0, 0, 0.75),
      rgba(0, 0, 0, 0)
    );
    display: flex;
    align-items: center;
    padding: 20px;
  }
  .photo-card h2 {
    color: white;
    margin: 0;
  }
</style>

<div class="photo-card">
  <h2>Lagos at Dawn</h2>
</div>
```

**Expected output:** A blue box where the left side has a dark overlay (making the text readable), fading out to pure blue on the right.

**Self-check questions:**
- What does `rgba(0, 0, 0, 0.75)` mean in plain English?
- What would happen if you changed `0.75` to `0.2`?

---

### Exercise 3 — Radial Glow Effect

**Objective:** Create a glowing button using a radial gradient.

**Scenario:** You are designing a call-to-action button for a tech product page. The button should look like it glows from the centre.

```html
<style>
  .glow-button {
    width: 200px;
    height: 60px;
    border: none;
    border-radius: 30px;
    background-image: radial-gradient(
      circle at 50% 50%,
      #00ffcc,
      #007755
    );
    color: white;
    font-size: 18px;
    font-weight: bold;
    cursor: pointer;
  }
</style>

<button class="glow-button">Get Started</button>
```

**Expected output:** A pill-shaped button with a bright teal glow in the centre fading to a deep green at the edges.

**What-if challenge:** Move the glow centre to `20% 30%` and observe how it changes the button's appearance.

---

### Exercise 4 — Pie Chart

**Objective:** Build a simple data visualisation pie chart using a conic gradient.

**Scenario:** A school's data team wants to show how students spend their time: studying (40%), sleeping (30%), and leisure (30%).

```html
<style>
  .pie-chart {
    width: 220px;
    height: 220px;
    border-radius: 50%;
    background-image: conic-gradient(
      #e74c3c 0%   40%,   /* Studying - red    */
      #3498db 40%  70%,   /* Sleeping  - blue  */
      #2ecc71 70%  100%   /* Leisure   - green */
    );
  }
</style>

<div class="pie-chart"></div>
```

**Expected output:** A circular pie chart with three clearly defined colour sections — no blending between them.

**Self-check questions:**
- Why do we use `border-radius: 50%` to display a pie chart?
- If studying increases to 55%, what values would you use?

---

## Part 5 — Mini Project: Gradient Profile Card

In this project, you will build a stylish profile card that uses **all three gradient types** together.

**Project Overview:** A designer's personal card for a portfolio website.

### Stage 1 — Setup (HTML Structure)

Create a file called `gradient-card.html` with this structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Gradient Profile Card</title>
  <style>
    /* styles will go here */
  </style>
</head>
<body>
  <div class="card">
    <div class="card-header">
      <div class="avatar"></div>
      <h2>Amara Okafor</h2>
      <p>UI/UX Designer</p>
    </div>
    <div class="skills">
      <div class="skill-bar" data-skill="Design"></div>
      <div class="skill-bar" data-skill="Code"></div>
      <div class="skill-bar" data-skill="Strategy"></div>
    </div>
    <div class="stats">
      <div class="stat-icon"></div>
      <p>5 Years Experience</p>
    </div>
  </div>
</body>
</html>
```

**Milestone output:** An unstyled HTML skeleton. Open in browser — you should see plain text.

---

### Stage 2 — Card Header with Linear Gradient

Add this CSS inside the `<style>` tag:

```css
body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #1a1a2e;
  font-family: Arial, sans-serif;
}

.card {
  width: 320px;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.4);
}

.card-header {
  /* LINEAR GRADIENT - diagonal purple to blue header */
  background-image: linear-gradient(135deg, #667eea, #764ba2);
  padding: 30px;
  text-align: center;
  color: white;
}

.card-header h2 {
  margin: 10px 0 5px;
  font-size: 22px;
}

.card-header p {
  margin: 0;
  opacity: 0.85;
  font-size: 14px;
}
```

**Milestone output:** A purple-to-blue diagonal gradient card header with the designer's name and title.

---

### Stage 3 — Avatar with Radial Gradient

Add the avatar circle below `.card-header` in your CSS:

```css
.avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  margin: 0 auto;
  /* RADIAL GRADIENT - glowing avatar circle */
  background-image: radial-gradient(
    circle at 35% 35%,
    #ffd700,
    #ff6b35
  );
  border: 3px solid rgba(255, 255, 255, 0.5);
}
```

**Milestone output:** A glowing circular avatar that appears to have light hitting it from the top-left.

---

### Stage 4 — Skill Bars with Repeating Linear Gradient

Add the skills section:

```css
.skills {
  background-color: #16213e;
  padding: 20px;
}

.skill-bar {
  height: 12px;
  border-radius: 6px;
  margin-bottom: 12px;
  /* REPEATING LINEAR GRADIENT - animated stripe effect */
  background-image: repeating-linear-gradient(
    45deg,
    #00d2ff,
    #00d2ff 10px,
    #0096c7 10px,
    #0096c7 20px
  );
}
```

**Milestone output:** Three diagonal-striped skill bars, giving a dynamic, technical feel.

---

### Stage 5 — Stats Pie with Conic Gradient

Add the stats section at the bottom:

```css
.stats {
  background-color: #16213e;
  padding: 15px 20px;
  display: flex;
  align-items: center;
  gap: 15px;
  border-top: 1px solid #0f3460;
  color: #aaa;
  font-size: 14px;
}

.stat-icon {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  /* CONIC GRADIENT - experience completion ring */
  background-image: conic-gradient(
    #00d2ff 0% 80%,
    #16213e 80% 100%
  );
  flex-shrink: 0;
}
```

**Milestone output:** A small circular "progress ring" showing 80% completion using a conic gradient.

---

### Final Output

You now have a complete gradient profile card using:

- ✅ **Linear gradient** — diagonal header background
- ✅ **Radial gradient** — glowing avatar circle
- ✅ **Repeating linear gradient** — striped skill bars
- ✅ **Conic gradient** — progress ring in stats

**Reflection questions:**
- Which gradient type felt most intuitive to you?
- How could you make the card animate (hint: look up CSS transitions on gradients)?
- What other UI components could benefit from conic gradients? (hint: loading spinners, rating indicators)

---

## Part 6 — Common Beginner Mistakes

### Mistake 1 — Using `background-color` instead of `background-image`

```css
/* ❌ WRONG - gradient will NOT work here */
background-color: linear-gradient(red, yellow);

/* ✅ CORRECT */
background-image: linear-gradient(red, yellow);
```

**Why:** Gradient functions are values of `background-image`, not `background-color`. If you put them under `background-color`, the browser ignores them and may show no background at all.

---

### Mistake 2 — Forgetting commas between colours

```css
/* ❌ WRONG - missing comma between colours */
background-image: linear-gradient(red yellow green);

/* ✅ CORRECT */
background-image: linear-gradient(red, yellow, green);
```

**Why:** Each colour stop must be separated by a comma. Without commas, the browser cannot parse the values and will silently fail.

---

### Mistake 3 — Confusing the direction keyword syntax

```css
/* ❌ WRONG - 'right' alone is not valid */
background-image: linear-gradient(right, red, yellow);

/* ✅ CORRECT - must use 'to right' */
background-image: linear-gradient(to right, red, yellow);
```

**Why:** Direction keywords require the word `to` before them. The `right` alone is interpreted as a colour name (which fails), not a direction.

---

### Mistake 4 — Forgetting `border-radius: 50%` when making a pie chart

```css
/* ❌ This makes a square conic gradient, not a pie chart */
.pie {
  width: 200px;
  height: 200px;
  background-image: conic-gradient(red 40%, blue 40%);
}

/* ✅ Add border-radius to get the circular pie shape */
.pie {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  background-image: conic-gradient(red 40%, blue 40%);
}
```

---

### Mistake 5 — Confusing `from` (starting angle) with `at` (centre position)

```css
/* from = the starting angle of the sweep */
conic-gradient(from 90deg, red, yellow)

/* at = where the centre point is */
conic-gradient(at 20% 50%, red, yellow)

/* Both together */
conic-gradient(from 90deg at 20% 50%, red, yellow)
```

These are two separate, independent settings. You can use one or both.

---

### Mistake 6 — Using percentage positions in the wrong order

```css
/* ❌ WRONG - stops must go in increasing order */
background-image: linear-gradient(red 80%, yellow 20%);

/* ✅ CORRECT - always list positions smallest to largest */
background-image: linear-gradient(red 20%, yellow 80%);
```

**Why:** If position values decrease (go backward), the browser clips them to the previous value, which creates unexpected results.

---

## Reflection Questions

Think through these questions on your own to test your understanding:

1. What is the difference between `linear-gradient()` and `repeating-linear-gradient()`?
2. A friend says "I made the gradient go to the left by writing `to left` but it seems to go from blue to red and I expected red to blue." What does this mean? How would you explain it?
3. When would you choose a radial gradient over a linear gradient?
4. Why might you use `rgba()` transparency in a gradient instead of just plain colour names?
5. What real-life data visualisations can be represented using conic gradients?
6. You want a striped background on a webpage. Which gradient type would you use, and why?
7. How does `closest-side` differ from `farthest-corner` in a radial gradient?
8. Can you apply a gradient to text in CSS? (Research hint: `background-clip: text`)

---

## Completion Checklist

Before moving on, make sure you can check off each item:

- [ ] I understand what a CSS gradient is and why it is used in web design
- [ ] I can write a basic `linear-gradient()` with two colour stops
- [ ] I can control the direction of a linear gradient using keywords (`to right`, `to bottom right`) and angles (`45deg`, `180deg`)
- [ ] I can create multi-colour linear gradients with three or more stops
- [ ] I can use `rgba()` transparency to create fading effects
- [ ] I can use `repeating-linear-gradient()` to create stripe patterns
- [ ] I understand what a `radial-gradient()` is and how it differs from a linear gradient
- [ ] I can change the shape of a radial gradient (`circle` vs `ellipse`)
- [ ] I can use size keywords (`closest-side`, `farthest-corner`) in radial gradients
- [ ] I can reposition the centre of a radial gradient with `at`
- [ ] I can use `repeating-radial-gradient()` to create ring/bullseye patterns
- [ ] I understand what a `conic-gradient()` is and how it rotates around a point
- [ ] I can create a pie chart using a conic gradient with sharp colour stops
- [ ] I can use `from` to set a starting angle and `at` to set a centre position in conic gradients
- [ ] I can use `repeating-conic-gradient()` to create wedge/pinwheel patterns
- [ ] I completed the Gradient Profile Card mini-project using all three gradient types

---

## Lesson Summary

In this lesson, you learned about all three types of CSS gradients.

**Linear gradients** (`linear-gradient()`) create colour transitions that flow in a straight line. You can control the direction using keyword phrases like `to right` or `to bottom right`, or with precise degree angles from `0deg` to `360deg`. You can use as many colour stops as you need, and you can include transparency with `rgba()` to create fading effects. The `repeating-linear-gradient()` variant tiles the pattern to create stripes or repetitive patterns.

**Radial gradients** (`radial-gradient()`) radiate outward from a centre point. You can control the shape (`circle` or `ellipse`), the size (using keywords like `closest-side` and `farthest-corner`), and the position of the centre point using `at`. They are ideal for glow effects, spot-lighting, and any design where colour should emanate from a focal point. The `repeating-radial-gradient()` variant creates concentric ring patterns.

**Conic gradients** (`conic-gradient()`) rotate colour transitions around a centre point, making them perfect for pie charts, progress rings, colour wheels, and checkerboard patterns. You can set a starting angle with `from` and shift the pivot point with `at`. The `repeating-conic-gradient()` variant produces pinwheel and wedge-stripe effects.

All three gradient types are used as values of the `background-image` property. They require no external image files, making your websites faster and more flexible.

| Gradient Type | Movement            | Best Use                              |
|---------------|---------------------|---------------------------------------|
| Linear        | Straight line       | Banners, overlays, striped patterns   |
| Radial        | Outward from centre | Glows, spotlights, bullseye rings     |
| Conic         | Rotating around     | Pie charts, progress rings, pinwheels |

Gradients are one of the most versatile and visually impactful tools in CSS. Now that you have mastered all three types, you can create beautiful, professional-looking designs with nothing but code.
