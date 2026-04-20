---
render_with_liquid: false
title: "CSS Height and Width — Setting, Limiting, and Controlling Element Size"
nav_order: 10
---

# Lesson 10 — CSS Height and Width

## `height` · `width` · `max-width` · `min-width` · `max-height` · `min-height`

---

## Lesson Introduction

Every element on a web page takes up a certain amount of space — it has a height and a width. Sometimes the browser decides that size automatically based on the content inside. Other times, **you** decide — by writing CSS.

This lesson teaches you everything about sizing HTML elements with CSS. You will learn:

- How to set a **fixed** height and width (an exact number of pixels)
- How to set a **flexible** height and width using percentages (so the element grows and shrinks with the screen)
- What happens when you **do not** set a height or width at all
- How to set **minimum** and **maximum** size limits so elements never get too small or too large
- Why these properties matter deeply for real-world, professional, and responsive web design

By the end of this lesson, you will be able to confidently size any element on any page, for any screen.

---

## What You Need to Know Before Starting

> **Prerequisite Check** — Briefly review these ideas if they feel unfamiliar.

### What is an HTML element?

An HTML element is anything you write between a pair of HTML tags. For example:

```html
<div>This is a div element</div>
<p>This is a paragraph element</p>
<img src="photo.jpg" alt="A photo">
```

Each element occupies a rectangular box on the screen. That box has a height (top to bottom) and a width (left to right).

### What is a CSS property and value?

A CSS declaration looks like this:

```css
property: value;
```

For example: `width: 300px;` — the property is `width`, and the value is `300px`.

### What are pixels (`px`)?

A pixel (`px`) is the smallest visible dot on a screen. It is a fixed unit — `200px` is always exactly 200 pixels, no matter what.

### What are percentages (`%`) in CSS?

A percentage like `50%` is relative — it means "50% of the parent element's size." If a parent `<div>` is 800px wide, a child element with `width: 50%` would be 400px wide. If the parent shrinks to 600px, the child becomes 300px. Percentages make layouts **flexible**.

### What is a block element?

In HTML, some elements automatically take up the full width of the page by default — these are called **block elements**. Examples include `<div>`, `<p>`, `<h1>`, `<section>`. Block elements are the most common targets for height and width settings.

### What is a `<div>`?

A `<div>` (short for "division") is a general-purpose container element with no built-in appearance. It is a blank rectangular box that you style entirely with CSS. Developers use `<div>` elements constantly to build layouts, cards, panels, and sections.

---

## Section 1 — The `height` and `width` Properties

### What Are They and Why Do They Exist?

By default, block elements like `<div>` and `<p>` automatically expand to fill the full width of the page and shrink to fit their content in height. This is fine for basic text, but as soon as you start building real layouts — image cards, buttons, sidebars, banners, columns — you need **precise control** over size.

The `height` and `width` CSS properties give you that control.

> **Analogy:** Imagine cutting pieces of cardboard for a craft project. Without measurement, each piece would be whatever size the sheet happens to be. With `height` and `width` in CSS, you are cutting each element to an exact size.

### Accepted Values

The `height` and `width` properties accept these types of values:

| Value | What it means | Example |
|-------|--------------|---------|
| `auto` | The browser decides the size (default behaviour) | `width: auto;` |
| `px` (pixels) | A fixed number of pixels — never changes | `width: 300px;` |
| `%` (percent) | A percentage of the **parent** element's width or height | `width: 50%;` |
| `em` | Relative to the current font size | `width: 10em;` |
| `rem` | Relative to the root font size | `width: 15rem;` |
| `vw` | Percentage of the viewport (screen) width | `width: 80vw;` |
| `vh` | Percentage of the viewport (screen) height | `height: 50vh;` |
| `initial` | Resets the property to its default value | `width: initial;` |
| `inherit` | Copies the value from the parent element | `width: inherit;` |

> **For beginners, focus on `px` and `%` first.** They cover the vast majority of everyday use cases.

---

## Section 2 — Setting a Fixed Width and Height

### Basic Example — Fixed Pixel Size

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      height: 200px;
      width: 500px;
      background-color: powderblue;
    }
  </style>
</head>
<body>
  <div>This div has a fixed height of 200px and width of 500px.</div>
</body>
</html>
```

**Expected Output:**

```
[A powderblue rectangle, exactly 500px wide and 200px tall, containing the text]
```

### Explaining Every Line

```css
div {
```
This targets every `<div>` element on the page.

```css
  height: 200px;
```
- `height` — the CSS property that controls how tall the element is (top to bottom)
- `200px` — the element will be exactly 200 pixels tall

```css
  width: 500px;
```
- `width` — the CSS property that controls how wide the element is (left to right)
- `500px` — the element will be exactly 500 pixels wide

```css
  background-color: powderblue;
```
This gives the box a light blue background colour so you can clearly see its shape and size. Without a background colour, an empty `<div>` is invisible because it has no visible content.

> **Thinking prompt:** What would happen if you removed `height: 200px;` and the `<div>` only contained a single short sentence? The div would shrink to just the height of that one line of text. That is the default `auto` behaviour — height adjusts to fit the content.

---

### Second Example — Making an Element 100% Wide

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      width: 100%;
      background-color: #4CAF50;
      color: white;
      padding: 10px;
    }
  </style>
</head>
<body>
  <div>This div stretches 100% across its parent.</div>
</body>
</html>
```

**Expected Output:**

```
[A green bar spanning the full width of the browser window, with white text inside]
```

`width: 100%` makes the element as wide as its parent container — in this case, the full browser window. This is a very common pattern for full-width banners, headers, and footers.

---

### Third Example — Height on a Paragraph

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p {
      height: 100px;
      width: 300px;
      background-color: lightyellow;
      border: 1px solid black;
    }
  </style>
</head>
<body>
  <p>This paragraph has a fixed height and width.</p>
</body>
</html>
```

**Expected Output:**

```
[A small light yellow box, 300px wide and 100px tall, with a black border and the text inside]
```

> **Important observation:** Notice that even though the text content is short, the box is still 100px tall. The `height` property creates a box of that size regardless of how much text is inside. If the text were longer, it might overflow beyond the box boundaries. You will learn how to handle overflow in a later lesson.

---

## Section 3 — Setting Width with a Percentage

### Why Use Percentages?

Fixed pixel widths work well when you know exactly how large a screen will be. But in the real world, people visit websites on phones with 375px screens, tablets with 768px screens, and desktop monitors with 1920px screens. A fixed `width: 800px` might look fine on a desktop but overflow badly on a phone.

**Percentage widths are flexible** — they scale automatically with the screen or parent container.

### Example — Percentage Width

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      width: 50%;
      background-color: lightcoral;
      padding: 15px;
    }
  </style>
</head>
<body>
  <div>This div takes up 50% of the page width.</div>
</body>
</html>
```

**Expected Output on a 1000px-wide screen:**

```
[A coral-coloured box that is 500px wide (50% of 1000px), with 15px internal padding]
```

**Expected Output on a 600px-wide screen:**

```
[Same coral-coloured box, but now 300px wide (50% of 600px)]
```

The box automatically resized! This is the power of percentages.

> **Thinking prompt:** If the screen is 1200px wide and you set `width: 75%`, how wide would the element be? (Answer: 900px — because 75% of 1200 is 900.)

---

## Section 4 — The `height` and `width` Properties Do NOT Include Padding and Border

### A Critical Concept: What Does "Width" Actually Measure?

This trips up almost every beginner at some point. Let's address it directly.

By default in CSS, when you write `width: 300px`, that 300px refers to the **content area only** — the space where your text or other content sits. It does **not** include:

- `padding` (internal space between the content and the border)
- `border` (the visible edge of the element)
- `margin` (external space outside the element)

> **Analogy:** Think of a picture frame. The `width` you set in CSS is the size of the picture itself, not the entire frame. The border is the frame around it, and padding is the white mat between the picture and the frame.

### Example to Show This Effect

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div.box-a {
      width: 300px;
      background-color: lightblue;
      border: 5px solid navy;
      padding: 20px;
    }
  </style>
</head>
<body>
  <div class="box-a">
    This box has width: 300px, but it is visually wider because of padding and border.
  </div>
</body>
</html>
```

**What actually renders:**

- Content area width: 300px
- Plus left padding: 20px
- Plus right padding: 20px
- Plus left border: 5px
- Plus right border: 5px
- **Total visible width: 350px**

> **The fix:** Use `box-sizing: border-box;` in your CSS to make `width` include padding and border. You will learn all about this in the **CSS Box Model** and **Box Sizing** lessons. For now, just be aware that `width` refers to the content area only by default.

---

## Section 5 — `auto` — The Default Behaviour

When you do **not** set `width` or `height`, both are set to `auto` by default. Here is what `auto` does:

- **`width: auto`** — Block elements (like `<div>` and `<p>`) expand to fill their parent container's full width by default.
- **`height: auto`** — The element grows as tall as it needs to be to fit all its content. If you add more text, the box gets taller.

### Example — `auto` in Action

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      background-color: lightgreen;
      padding: 10px;
      /* No width or height set — both are auto */
    }
  </style>
</head>
<body>
  <div>
    This div has no width or height set. It will stretch to fill the full width of
    the page, and its height will grow to fit this text content exactly.
  </div>
</body>
</html>
```

**Expected Output:**

```
[A green box spanning the full page width, just tall enough to contain the text]
```

---

## Section 6 — Setting Both Height and Width Together

### Example — A Square Box

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div.square {
      height: 150px;
      width: 150px;
      background-color: salmon;
    }
  </style>
</head>
<body>
  <div class="square">I am a square.</div>
</body>
</html>
```

**Expected Output:**

```
[A salmon-coloured square, 150px × 150px, with text inside]
```

### Example — A Wide Banner

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div.banner {
      height: 80px;
      width: 100%;
      background-color: darkslateblue;
      color: white;
      font-size: 24px;
      padding: 20px;
    }
  </style>
</head>
<body>
  <div class="banner">Welcome to My Website</div>
</body>
</html>
```

**Expected Output:**

```
[A dark purple banner spanning the full page width, 80px tall, with white text]
```

---

## Section 7 — CSS Min-Width and Max-Width

### The Problem with Fixed Widths

Imagine you build a content panel with `width: 800px`. On a large desktop screen, it looks perfect. But on a small phone screen, only 375px wide, the element overflows — the user has to scroll sideways to read the content. That is a terrible experience.

Now imagine you instead use `width: 100%`. On mobile it looks great. But on a huge 1920px monitor, the text stretches across the entire screen in one enormous line — hard to read, and visually poor.

**The solution:** use `max-width` and `min-width` to set **boundaries** — a minimum size and a maximum size. Between those boundaries, the element can flex freely.

---

### `max-width` — "Do Not Grow Larger Than This"

`max-width` sets a **ceiling** on how wide an element can become. The element can be smaller, but it can never exceed this width.

> **Analogy:** Think of `max-width` like a speed limiter on a car. The car can drive slower, but it cannot go faster than the limit.

#### Example — `max-width`

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      max-width: 500px;
      background-color: lightcyan;
      padding: 15px;
      border: 1px solid teal;
    }
  </style>
</head>
<body>
  <div>
    This div will never be wider than 500px, even if the browser window is 2000px wide.
    But it will shrink naturally if the window is smaller than 500px.
  </div>
</body>
</html>
```

**On a 1200px screen:** The div is 500px wide (it hit the maximum limit).

**On a 400px screen:** The div is 400px wide (smaller than max-width, so it fills the available space).

#### Why `max-width` is Better Than a Fixed `width` for Responsive Design

```css
/* Fixed width — bad on small screens */
div {
  width: 600px; /* Overflows on a 375px phone! */
}

/* Better — flexible but bounded */
div {
  max-width: 600px; /* Never exceeds 600px on large screens */
  width: 100%;      /* Fills available space on small screens */
}
```

This pattern — `width: 100%` combined with `max-width` — is one of the most important techniques in responsive web design. The element fills its container on small screens but caps at a readable width on large screens.

---

### `min-width` — "Do Not Shrink Smaller Than This"

`min-width` sets a **floor** on how narrow an element can become. No matter how small the screen or container, the element will never shrink below this width.

> **Analogy:** Think of `min-width` like a minimum wage — the element will always receive at least this much space.

#### Example — `min-width`

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      min-width: 200px;
      background-color: lavender;
      padding: 10px;
      border: 1px solid purple;
    }
  </style>
</head>
<body>
  <div>This div will always be at least 200px wide, even in a very narrow container.</div>
</body>
</html>
```

**On a 600px screen:** The div is 600px wide (no max-width set, so it fills available space).

**On a 150px screen:** The div is still 200px wide (min-width prevents it from going below 200px). The content may overflow its container, but the element itself holds its minimum size.

#### When to Use `min-width`

- Buttons that must always be wide enough to display their text
- Navigation links that must remain readable
- Form input fields that need a minimum usable size
- Table columns with minimum readability requirements

---

## Section 8 — CSS Min-Height and Max-Height

Just like width has minimum and maximum limits, so does height.

### `max-height` — "Do Not Grow Taller Than This"

`max-height` sets a ceiling on how tall an element can become. When content exceeds this height, it will overflow (which you can control with the `overflow` property, covered in a later lesson).

> **Analogy:** `max-height` is like a ceiling in a room — the room's contents can be shorter, but nothing can break through the roof.

#### Example — `max-height`

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      max-height: 100px;
      width: 300px;
      background-color: peachpuff;
      border: 1px solid orange;
      overflow: auto;
      padding: 10px;
    }
  </style>
</head>
<body>
  <div>
    This is line one of content.
    This is line two of content.
    This is line three of content.
    This is line four of content.
    This is line five — the box cannot grow past 100px, so a scrollbar appears here
    because of overflow: auto.
  </div>
</body>
</html>
```

**Expected Output:**

```
[A peach-coloured box, exactly 100px tall and 300px wide]
[Only the first few lines of text are visible]
[A scrollbar appears on the right so the user can scroll to see the rest]
```

> The `overflow: auto` tells the browser to add a scrollbar if content overflows the max-height. Without it, the content would overflow and spill outside the box visually.

#### Real-World Uses of `max-height`

- Collapsible dropdown menus that should not take over the whole screen
- Comment sections limited to a certain preview height
- Image thumbnails that should not exceed a fixed height
- Chat message bubbles with a reading cap

---

### `min-height` — "Do Not Shrink Shorter Than This"

`min-height` sets a floor on how short an element can become. Even if the element has no content at all, it will maintain this minimum height.

> **Analogy:** `min-height` is like a podium — even if nobody is standing on it, it still has a height.

#### Example — `min-height`

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      min-height: 200px;
      width: 400px;
      background-color: honeydew;
      border: 2px solid green;
      padding: 15px;
    }
  </style>
</head>
<body>
  <!-- First div: almost no content -->
  <div>Short content.</div>

  <!-- Second div: lots of content -->
  <div>
    This div has much more content. It has enough lines to easily exceed the
    min-height of 200px. Notice that this box grows taller than 200px to
    accommodate all the content. The min-height only prevents it from being
    SHORTER than 200px; it does not prevent it from being taller.
  </div>
</body>
</html>
```

**Expected Output:**

```
[First box: 200px tall (enforced by min-height), even though "Short content." only needs ~20px]
[Second box: taller than 200px because the content naturally requires more space]
```

#### Real-World Uses of `min-height`

- Page sections that should look substantial even when content is sparse
- Hero banners that must always be at least a certain height
- Sidebar panels that need to maintain a minimum visible height
- Card components that stay a consistent size even with minimal content

---

## Section 9 — Combining `min-width`, `max-width`, and `width`

The real power of these properties comes when you use them together. This is the foundation of responsive design.

### The Classic Responsive Width Pattern

```css
div.content {
  width: 100%;       /* Fill the available space on small screens */
  max-width: 900px;  /* But never exceed 900px on large screens */
}
```

### Worked Example — A Readable Content Column

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      background-color: #f0f0f0;
      margin: 0;
      padding: 0;
    }

    div.article {
      width: 100%;
      max-width: 700px;
      background-color: white;
      padding: 30px;
      margin: 20px auto; /* centers the box horizontally */
      border: 1px solid #ccc;
      line-height: 1.6;
    }

    h1 {
      color: #333;
    }
  </style>
</head>
<body>
  <div class="article">
    <h1>My Article Title</h1>
    <p>
      This content column uses a max-width of 700px. On small screens (like phones),
      it fills 100% of the available width. On large screens (like desktops),
      it stops growing at 700px and stays centred, keeping text at a
      comfortable reading width.
    </p>
    <p>
      Most readability research suggests that 60-75 characters per line is ideal.
      Using max-width to limit text columns achieves this automatically.
    </p>
  </div>
</body>
</html>
```

**On a 400px phone screen:** The article fills the full 400px.

**On a 1200px desktop:** The article is 700px wide and centred, with grey background on both sides.

> **This pattern is used by virtually every professional blog, news site, and documentation page in the world.** Wikipedia, Medium, and GitHub all use this exact technique.

---

### The Four-Property Guard Pattern

For elements that must work reliably across all screen sizes:

```css
div.card {
  width: 100%;       /* Flexible: fills container */
  min-width: 250px;  /* Floor: never too narrow */
  max-width: 600px;  /* Ceiling: never too wide */
  min-height: 150px; /* Always has visual presence */
}
```

This creates a size "corridor" — the element freely resizes between 250px and 600px depending on the screen.

---

## Section 10 — All Six Properties — Quick Reference

| Property | Controls | Sets a... | Behaviour |
|----------|----------|-----------|-----------|
| `width` | Horizontal size | Exact target width | Fixed or flexible size of content area |
| `height` | Vertical size | Exact target height | Fixed or flexible size of content area |
| `min-width` | Horizontal size | Minimum floor | Never shrinks below this |
| `max-width` | Horizontal size | Maximum ceiling | Never grows beyond this |
| `min-height` | Vertical size | Minimum floor | Never shrinks below this |
| `max-height` | Vertical size | Maximum ceiling | Never grows beyond this |

### Priority When Properties Conflict

What happens if `width` and `max-width` fight? CSS has clear rules:

- If `width` is larger than `max-width`, then `max-width` wins — the element shrinks to the maximum.
- If `width` is smaller than `min-width`, then `min-width` wins — the element grows to the minimum.
- `min-width` always overrides `max-width` if they conflict (minimum is the absolute floor).

**Example of priority in action:**

```css
div {
  width: 800px;    /* Trying to be 800px wide */
  max-width: 500px; /* But ceiling is 500px */
}
/* Result: the div is 500px wide. max-width wins. */
```

```css
div {
  width: 100px;    /* Trying to be 100px wide */
  min-width: 200px; /* But floor is 200px */
}
/* Result: the div is 200px wide. min-width wins. */
```

---

## Section 11 — Simple Standalone Examples

### Example 1 — A Profile Picture Placeholder

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div.avatar {
      width: 80px;
      height: 80px;
      background-color: steelblue;
      border-radius: 50%;  /* Makes it a circle */
      color: white;
      font-size: 30px;
      text-align: center;
      line-height: 80px;   /* Vertically centres the letter */
    }
  </style>
</head>
<body>
  <div class="avatar">A</div>
</body>
</html>
```

**Expected Output:**

```
[A blue circle, 80px × 80px, with the letter "A" centred inside it]
```

---

### Example 2 — A Progress Bar Shell

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div.progress-track {
      width: 400px;
      height: 20px;
      background-color: #e0e0e0;
      border-radius: 10px;
    }

    div.progress-fill {
      width: 60%;       /* Represents 60% completion */
      height: 20px;
      background-color: #4CAF50;
      border-radius: 10px;
    }
  </style>
</head>
<body>
  <div class="progress-track">
    <div class="progress-fill"></div>
  </div>
</body>
</html>
```

**Expected Output:**

```
[A grey rounded track, 400px wide]
[Inside it: a green bar filling 60% (240px) of that track]
```

> This is exactly how progress bars are built on real websites — a fixed-size outer track, and an inner element whose `width` percentage represents the progress value.

---

### Example 3 — Responsive Image Container

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div.image-container {
      width: 100%;
      max-width: 600px;
      min-height: 200px;
      background-color: #ddd;
      border: 2px dashed #999;
    }
  </style>
</head>
<body>
  <div class="image-container">
    [Image would appear here]
  </div>
</body>
</html>
```

**Expected Output on 800px screen:** A grey dashed box, 600px wide, at least 200px tall.

**Expected Output on 400px screen:** A grey dashed box, 400px wide (filling 100% of the screen), at least 200px tall.

---

### Example 4 — Card with Min and Max Height

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div.card {
      width: 250px;
      min-height: 100px;
      max-height: 300px;
      background-color: #fff3cd;
      border: 1px solid #ffc107;
      padding: 15px;
      overflow: auto;
    }
  </style>
</head>
<body>

  <!-- Card with very little content -->
  <div class="card">Short card.</div>

  <br>

  <!-- Card with a lot of content -->
  <div class="card">
    This card has a lot of content. Line after line after line. The card will grow,
    but only up to 300px in height. After that, a scrollbar will appear so the
    user can read the rest of the content without the card taking over the screen.
    Line six. Line seven. Line eight. Line nine. Still more content here.
  </div>

</body>
</html>
```

**Expected Output:**

```
[First card: 100px tall (min-height enforced), 250px wide, yellow tint]
[Second card: 300px tall (max-height enforced), 250px wide, with a scrollbar]
```

---

## Section 12 — Guided Practice Exercises

### Exercise 1 — Build a Simple Business Card

**Objective:** Create a styled business card element using fixed width and height.

**Scenario:** You are building a contacts page for a company. Each contact needs a card with a consistent size.

**Steps:**

1. Create a file called `business-card.html`.
2. Write the following code and style it as described:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div.card {
      width: 320px;
      height: 180px;
      background-color: #1a1a2e;
      color: white;
      border-radius: 12px;
      padding: 20px;
    }

    div.card h2 {
      margin: 0 0 5px 0;
      font-size: 20px;
    }

    div.card p {
      margin: 4px 0;
      font-size: 14px;
      color: #aaa;
    }
  </style>
</head>
<body>
  <div class="card">
    <h2>Ada Okafor</h2>
    <p>Senior Software Engineer</p>
    <p>ada.okafor@techcorp.com</p>
    <p>+234 801 234 5678</p>
  </div>
</body>
</html>
```

**Expected Output:**

```
[A dark navy card, exactly 320px × 180px]
[Name in white, job title and contact details in grey]
```

**Self-Check Questions:**

- What happens if you change `height: 180px` to `min-height: 180px`? Does the card look different with this small amount of content?
- What happens if you add ten more lines of contact information? Does the card handle it differently with `height: 180px` versus `min-height: 180px`?

**Optional What-If Challenge:** Try adding a second card below the first. Then wrap both in a parent `<div>` with `max-width: 400px`. What happens to the cards?

---

### Exercise 2 — A Responsive Hero Section

**Objective:** Create a page banner that works on any screen size using `min-height`, `width: 100%`, and `max-width`.

**Scenario:** You are building the top section of a landing page for a local restaurant. The hero banner must look great on both phones and desktop computers.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background-color: #f9f9f9;
    }

    div.hero {
      width: 100%;
      min-height: 300px;
      background-color: #b5451b;
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      padding: 40px 20px;
      box-sizing: border-box;
    }

    div.hero h1 {
      font-size: 2.5em;
      margin: 0 0 10px 0;
    }

    div.hero p {
      font-size: 1.1em;
      margin: 0;
    }

    div.content {
      width: 100%;
      max-width: 800px;
      margin: 40px auto;
      padding: 20px;
      background-color: white;
      border: 1px solid #ddd;
      box-sizing: border-box;
    }
  </style>
</head>
<body>

  <div class="hero">
    <div>
      <h1>Lagos Jollof Kitchen</h1>
      <p>Authentic Nigerian flavours since 1998</p>
    </div>
  </div>

  <div class="content">
    <h2>Our Story</h2>
    <p>
      Founded in Lagos Island, we have been serving the finest jollof rice,
      suya, and peppersoup to families and friends for over two decades.
      Our recipes have been passed down through three generations.
    </p>
  </div>

</body>
</html>
```

**Expected Output:**

```
[A full-width dark red hero banner, at least 300px tall, with centred white heading and tagline]
[Below it: a white content box, centred, max 800px wide, with the story text]
```

**Self-Check Questions:**

- Why is `width: 100%` used on the hero instead of a fixed pixel width?
- Why does the `.content` div use `max-width: 800px` instead of `width: 800px`?
- What happens to the content box on a screen that is only 400px wide?

---

### Exercise 3 — Practice All Six Properties

**Objective:** Create four boxes that each demonstrate a different sizing behaviour.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div.box {
      background-color: lightsteelblue;
      border: 2px solid steelblue;
      margin-bottom: 20px;
      padding: 10px;
      color: #333;
    }

    /* Box 1: Fixed size */
    div.fixed {
      width: 400px;
      height: 80px;
    }

    /* Box 2: Percentage width, auto height */
    div.percent {
      width: 60%;
    }

    /* Box 3: max-width prevents growing on large screens */
    div.maxed {
      width: 100%;
      max-width: 500px;
    }

    /* Box 4: min-height ensures visual presence even with little content */
    div.tall {
      width: 300px;
      min-height: 150px;
    }
  </style>
</head>
<body>

  <div class="box fixed">
    Box 1: Fixed — always 400px × 80px
  </div>

  <div class="box percent">
    Box 2: Percentage — always 60% of the page width
  </div>

  <div class="box maxed">
    Box 3: Max-width — fills 100% but stops at 500px
  </div>

  <div class="box tall">
    Box 4: Min-height — always at least 150px tall, even with little text.
  </div>

</body>
</html>
```

**Expected Output:**

```
[Box 1: exactly 400px wide, 80px tall]
[Box 2: 60% of whatever the screen is — try resizing the browser!]
[Box 3: full width on small screens, stops at 500px on large screens]
[Box 4: 300px wide, at least 150px tall — taller if you add more text]
```

**Self-Check Questions:**
- Resize your browser window. Which boxes change size and which stay fixed?
- Add a lot of text to Box 1. What happens? Does the box grow? Why or why not?
- Add a lot of text to Box 4. Does it grow past 150px? Why?

---

## Section 13 — Mini Project: A Product Card Grid

### Project Description

You will build a simple product listing section that contains three product cards side by side. Each card will use proper sizing so it looks good on different screen sizes.

### Project Goal

Create a product grid that:
- Uses fixed width and height on product cards for consistency
- Uses `min-height` to keep cards uniform even with varying content
- Uses `max-width` on the grid container for readability on large screens
- Uses percentage widths to allow flexible layout

---

### Stage 1 — HTML Structure

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="products.css">
</head>
<body>

  <h1 class="page-title">Our Products</h1>

  <div class="product-grid">

    <div class="product-card">
      <div class="product-image"></div>
      <h3>Wireless Earbuds</h3>
      <p>Crystal clear sound with 24-hour battery life.</p>
      <p class="price">₦15,000</p>
    </div>

    <div class="product-card">
      <div class="product-image"></div>
      <h3>Laptop Stand</h3>
      <p>Ergonomic aluminium stand. Adjustable to 6 heights.</p>
      <p class="price">₦8,500</p>
    </div>

    <div class="product-card">
      <div class="product-image"></div>
      <h3>USB-C Hub</h3>
      <p>7-in-1 hub. HDMI, USB 3.0, SD card, Ethernet, and more — all in one sleek device.</p>
      <p class="price">₦12,000</p>
    </div>

  </div>

</body>
</html>
```

---

### Stage 2 — CSS Stylesheet (`products.css`)

```css
/* ---- Page-level styling ---- */
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  margin: 0;
  padding: 20px;
}

.page-title {
  text-align: center;
  color: #333;
  margin-bottom: 30px;
}

/* ---- Grid container ---- */
.product-grid {
  display: flex;          /* Arranges cards side by side */
  gap: 20px;              /* Space between cards */
  flex-wrap: wrap;        /* Cards wrap to next line on small screens */
  max-width: 1100px;      /* Grid never wider than 1100px */
  margin: 0 auto;         /* Centre the grid on the page */
}

/* ---- Individual product card ---- */
.product-card {
  width: 300px;           /* Fixed card width */
  min-height: 350px;      /* Cards always at least 350px tall */
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 15px;
  box-sizing: border-box;
}

/* ---- Product image placeholder ---- */
.product-image {
  width: 100%;            /* Image fills card width */
  height: 180px;          /* Fixed image area height */
  background-color: #e0e0e0;
  border-radius: 4px;
  margin-bottom: 12px;
}

/* ---- Card text ---- */
.product-card h3 {
  margin: 0 0 8px 0;
  color: #222;
  font-size: 17px;
}

.product-card p {
  color: #555;
  font-size: 14px;
  line-height: 1.5;
  margin: 0 0 8px 0;
}

.price {
  font-size: 18px !important;
  font-weight: bold;
  color: #b5451b !important;
}
```

**Milestone Output:**

```
[Page heading: "Our Products" centred]
[Three product cards side by side, each 300px wide]
[Each card has a grey image placeholder (180px tall) and product details]
[Card 3 (USB-C Hub) has more description text — but min-height keeps all cards visually equal]
[On a narrow screen, the cards wrap to a new line]
```

---

### Stage 3 — Reflection

Answer these questions after completing the project:

1. The `.product-card` uses `width: 300px` (fixed). What would happen if you changed it to `width: 100%; max-width: 300px;` instead? Would the behaviour change on very small screens?

2. The `.product-image` uses `width: 100%` (percentage). Why is this better than `width: 280px` (fixed) for the image area?

3. The USB-C Hub card has more description text than the other two cards. The cards all look the same height. Which CSS property is responsible for that?

4. The `.product-grid` container uses `max-width: 1100px`. What would the grid look like on a 4K monitor without this max-width?

**Optional Extension:** Add a fourth product card. Give it a very long description — several sentences. Observe how `min-height` enforces a baseline, and how the card can grow taller when needed. Then add `max-height: 450px; overflow: auto;` to the card and see what happens with that long description.

---

## Section 14 — Common Beginner Mistakes

### Mistake 1 — Confusing `height` and `width` with Total Visual Size

```css
/* ❌ MISTAKE: Thinking 300px width means the box looks 300px wide */
div {
  width: 300px;
  padding: 30px;
  border: 5px solid black;
}
/* Actual visual width = 300 + 30 + 30 + 5 + 5 = 370px */

/* ✅ FIX: Use box-sizing: border-box to make width include padding and border */
div {
  width: 300px;
  padding: 30px;
  border: 5px solid black;
  box-sizing: border-box;
}
/* Now the visual width is exactly 300px */
```

---

### Mistake 2 — Using `height: 100%` Without a Parent Height

```css
/* ❌ MISTAKE: Expecting 100% height to fill the screen */
div {
  height: 100%;
  background-color: blue;
}
/* This does nothing visible! 100% of an undeclared parent height = nothing */

/* ✅ FIX: Set height on the parent (or use vh units) */
html, body {
  height: 100%; /* Give the parent a height first */
}
div {
  height: 100%;
  background-color: blue;
}

/* OR use viewport height: */
div {
  height: 100vh; /* 100% of the visible screen height */
  background-color: blue;
}
```

---

### Mistake 3 — Using Fixed `width` on Elements That Should Be Fluid

```css
/* ❌ MISTAKE: Fixed pixel width breaks on small screens */
div.sidebar {
  width: 350px; /* Overflows on a 320px phone screen! */
}

/* ✅ FIX: Use max-width with a flexible width */
div.sidebar {
  width: 100%;
  max-width: 350px;
}
```

---

### Mistake 4 — Forgetting That `height: auto` Is the Default

```css
/* ❌ MISTAKE: Setting height: auto thinking it does something special */
div {
  height: auto; /* This is already the default — redundant */
  width: 400px;
}

/* ✅ CORRECT understanding: Simply do not set height at all if you want auto behaviour */
div {
  width: 400px;
  /* height is auto by default */
}
```

---

### Mistake 5 — Setting `max-width` Without Considering Mobile

```css
/* ❌ MISTAKE: max-width alone can still overflow on very small screens */
div {
  max-width: 600px;
  /* If the screen is 400px, this div might still appear wider than expected
     because max-width only sets a ceiling, not a floor */
}

/* ✅ FIX: Combine with width: 100% */
div {
  width: 100%;
  max-width: 600px;
  /* Now: fills 100% on small screens, caps at 600px on large screens */
}
```

---

### Mistake 6 — Confusing `min-height` and `height` Behaviour With Content

```css
/* ❌ MISCONCEPTION: "min-height will keep my box at exactly 200px" */
div {
  min-height: 200px;
}
/* With a lot of content, the box WILL grow beyond 200px! */
/* min-height is a floor, not a fixed size */

/* ✅ UNDERSTAND: min-height means "at least this tall" */
/* Use height if you want a strict fixed height */
/* Use min-height if you want "at least this tall, but can grow" */
```

---

## Section 15 — Reflection Questions

Think carefully about each question. They review the key ideas from this lesson.

1. What is the difference between `width: 300px` and `width: 100%`? When would you use each?

2. A beginner sets `height: 200px` on a `<div>` that contains a long article. After adding more text, the text seems to spill out below the box. Why is this happening, and what might be a better approach?

3. You are building a website that people will view on phones AND on large desktop monitors. Explain why `max-width` combined with `width: 100%` is a better choice than just `width: 700px`.

4. What is the difference between `min-height` and `height`? Give a real-world example where `min-height` is more appropriate than `height`.

5. A card component has `min-height: 200px` and `max-height: 400px`. The user adds content that would naturally need 500px of height. What happens to the card? What does the user see?

6. True or False: "If I set `width: 400px` and `max-width: 500px`, the element will be 500px wide." Explain your answer.

7. True or False: "If I set `width: 600px` and `max-width: 400px`, the element will be 400px wide." Explain your answer.

8. You have an element with `min-width: 300px` and `max-width: 200px`. These values conflict. Which one wins?

---

## Section 16 — Completion Checklist

Go through this list and confirm you understand each item:

- [ ] I know what `width` and `height` do in CSS
- [ ] I understand the difference between `px` values (fixed) and `%` values (flexible)
- [ ] I know what `auto` means as a width or height value
- [ ] I know that `width` measures the content area, not including padding or border by default
- [ ] I can explain what `max-width` does and when to use it
- [ ] I can explain what `min-width` does and when to use it
- [ ] I can explain what `max-height` does and when to use it
- [ ] I can explain what `min-height` does and when to use it
- [ ] I understand why `width: 100%; max-width: X;` is better than just `width: X;` for responsive design
- [ ] I know that `min-height` sets a floor, meaning the element can be taller than the minimum
- [ ] I know that `max-height` sets a ceiling, and content may overflow if not handled
- [ ] I completed at least one guided practice exercise
- [ ] I completed Stages 1 and 2 of the Mini Project

---

## Lesson Summary

You have now mastered one of the most essential skill sets in CSS — controlling the size of elements.

**The Six Core Properties:**

| Property | Purpose | Sets a... |
|----------|---------|-----------|
| `width` | Exact horizontal size | Target (can be overridden by min/max) |
| `height` | Exact vertical size | Target (can be overridden by min/max) |
| `min-width` | Minimum horizontal size | Floor — element cannot shrink below this |
| `max-width` | Maximum horizontal size | Ceiling — element cannot grow beyond this |
| `min-height` | Minimum vertical size | Floor — element cannot shrink below this |
| `max-height` | Maximum vertical size | Ceiling — element cannot grow beyond this |

**The Most Important Values:**

- `px` — a fixed number of pixels, does not change with screen size
- `%` — a percentage of the parent's size, scales automatically
- `auto` — the browser decides; width fills parent, height fits content
- `vw` / `vh` — percentage of the visible screen (viewport) width or height

**The Professional Responsive Pattern:**

```css
.container {
  width: 100%;       /* Fills screen on mobile */
  max-width: 900px;  /* Caps at readable size on desktop */
  margin: 0 auto;    /* Centres horizontally */
}
```

**Key Rules to Remember:**

- `width` and `height` only measure the content area — padding and border add to the visual size unless you use `box-sizing: border-box`
- `min-height` is a floor — the element CAN be taller, just not shorter
- `max-height` is a ceiling — content can overflow if it exceeds this value
- Always combine `width: 100%` with `max-width` for elements that should look good on all screen sizes
- `min-width` overrides `max-width` if they conflict

**Real-World Connection:**

Every website you visit uses these properties constantly. Product cards, article columns, hero banners, navigation bars, buttons, images — all sized with `width`, `height`, `min-*`, and `max-*`. When professional developers write responsive layouts, the very first thing they consider is how these six properties interact across different screen sizes. You now have the foundation to do the same.

---

*End of Lesson 10 — You are now ready to move on to the CSS Box Model.*
