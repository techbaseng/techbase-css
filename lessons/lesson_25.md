---
render_with_liquid: false
title: "CSS Float, Clear, and Clearfix"
nav_order: 25
---

# Lesson 25: CSS Float, Clear, and Clearfix

---

## Lesson Introduction

Have you ever looked at a magazine page or a newspaper and noticed how an image sits to the side while text flows nicely around it? Or how web pages have content boxes lined up side by side horizontally — like product cards in an online shop?

That kind of layout is exactly what the CSS `float` property was designed to create!

In this lesson, you will learn:

- What the `float` property is and why it was created
- The different float values and what each one does
- How to use the `clear` property to stop floats from affecting nearby elements
- What the "clearfix hack" is and why it is so important
- How to build real-world layouts using floats — including equal-width boxes, image galleries, navigation menus, and full webpage layouts

By the end of this lesson, you will be able to use floats confidently to control how elements are positioned side by side on a web page.

---

## Prerequisite Concepts

Before we dive into floats, let's quickly review a few ideas that will help you understand how float works.

### Block Elements vs. Inline Elements

In HTML and CSS, every element behaves as either a **block** element or an **inline** element.

- **Block elements** always start on a new line and stretch across the full available width. Examples: `<div>`, `<p>`, `<h1>`
- **Inline elements** sit within the flow of text, side by side. Examples: `<span>`, `<img>`, `<a>`

**Why this matters for float:** By default, block elements like `<div>` stack vertically — one on top of the other. The `float` property is one way to make block elements appear side by side instead of stacking.

### What is "Normal Document Flow"?

When you write HTML without any special CSS, elements appear in the order you wrote them, from top to bottom. This is called the **normal document flow**. When you apply `float`, you take an element *out* of this normal flow, which affects how everything else on the page is arranged.

---

## Section 1: The CSS `float` Property

### What Is `float`?

The `float` CSS property specifies how an element should be positioned within its container. When an element is floated, it is moved to either the **left** or the **right** side of its container. Text and other inline elements then **wrap around it** automatically.

**Real-world analogy:** Think of a bookshelf where you are putting things on a shelf. Normally, everything lines up from left to right in a straight row. If you pick up one item and push it to the far right corner, all the other items shift to fill the space on the left — that is very similar to what `float` does to elements on a webpage.

### Why Does `float` Exist?

The `float` property was originally introduced to allow text to wrap around images — just like in a printed magazine. Over time, developers also found creative ways to use it to create multi-column layouts and navigation bars.

> **Note for beginners:** Modern CSS now has Flexbox and CSS Grid, which are more powerful layout tools. However, floats are still widely used, still supported everywhere, and still appear in many real-world projects — so understanding them is essential.

### The float Property Values

The `float` property can take one of four values:

| Value | What It Does |
|-------|-------------|
| `left` | Moves the element to the **left** side of its container. Text and other content flows on the **right** side. |
| `right` | Moves the element to the **right** side of its container. Text and other content flows on the **left** side. |
| `none` | The element does **not** float. This is the **default** value — normal document flow. |
| `inherit` | The element inherits the float value from its **parent** element. |

---

## Section 2: Understanding Each Float Value with Examples

### 2.1 `float: none` — The Default

Let's start with the default behaviour so you can see the difference clearly.

**What it does:** The element stays exactly where it is placed in the page flow. No floating occurs.

```html
<!-- HTML -->
<div class="container">
  <img src="image.jpg" alt="Sample image" style="float: none;">
  <p>This is some sample text. It appears BELOW the image, not beside it.
     That is because the image has no float applied. It is in the normal
     document flow.</p>
</div>
```

```css
/* CSS */
img {
  float: none;    /* Default - no floating */
  width: 150px;
}
```

**Expected Output (visual):**
```
[ Image ]
This is some sample text. It appears BELOW the image,
not beside it...
```

> **Key observation:** Without float, the image takes up its full line and the text starts on the next line.

---

### 2.2 `float: right` — Move Element to the Right

**What it does:** The element jumps to the right side of its container. All text and inline content wraps around the element on the **left** side.

```html
<!-- HTML -->
<div class="container">
  <img src="pineapple.jpg" alt="Pineapple" class="img-right">
  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.
     Phasellus imperdiet, nulla et dictum interdum, nisi lorem
     egestas odio, vitae scelerisque enim ligula venenatis dolor.
     Maecenas nisl est, ultrices nec congue eget, auctor vitae
     massa. The text flows on the LEFT of the image.</p>
</div>
```

```css
/* CSS */
.img-right {
  float: right;   /* Pushes the image to the RIGHT */
  width: 150px;
  margin: 0 0 10px 15px;  /* Adds some space around the image */
}
```

**Expected Output (visual):**
```
Lorem ipsum dolor sit amet,              [ Image ]
consectetur adipiscing elit.
Phasellus imperdiet, nulla et
dictum interdum...
```

> **Thinking prompt:** What would happen if the text is shorter than the image height? The text would end before the image does, and the image would still extend downward. This is actually a common problem beginners face — we will fix it later using `clear` and `clearfix`!

---

### 2.3 `float: left` — Move Element to the Left

**What it does:** The element jumps to the left side of its container. All text and inline content wraps around the element on the **right** side.

```html
<!-- HTML -->
<div class="container">
  <img src="pineapple.jpg" alt="Pineapple" class="img-left">
  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.
     Phasellus imperdiet, nulla et dictum interdum, nisi lorem
     egestas odio. The text flows on the RIGHT of the image.</p>
</div>
```

```css
/* CSS */
.img-left {
  float: left;    /* Pushes the image to the LEFT */
  width: 150px;
  margin: 0 15px 10px 0;  /* Adds spacing on the right of the image */
}
```

**Expected Output (visual):**
```
[ Image ]  Lorem ipsum dolor sit amet,
           consectetur adipiscing elit.
           Phasellus imperdiet, nulla et
           dictum interdum...
```

> **Comparison:** Notice how `float: left` and `float: right` are mirrors of each other — they both cause text to wrap, just from opposite directions.

---

### 2.4 Floating Multiple `<div>` Elements Side by Side

One of the most powerful uses of float is making block elements sit **next to each other** horizontally, instead of stacking vertically.

Remember: by default, `<div>` elements are block elements — they always start on a new line. But with `float: left`, we can force them to appear side by side!

```html
<!-- HTML: Three coloured boxes -->
<div class="box div1">Box 1 - Red</div>
<div class="box div2">Box 2 - Yellow</div>
<div class="box div3">Box 3 - Green</div>
```

```css
/* CSS */
.box {
  float: left;       /* All divs float to the left, lining up side by side */
  padding: 15px;
  width: 100px;
  text-align: center;
}

.div1 { background-color: red; }
.div2 { background-color: yellow; }
.div3 { background-color: green; }
```

**Expected Output (visual):**
```
[ Box 1 - Red ] [ Box 2 - Yellow ] [ Box 3 - Green ]
```

**Line-by-line explanation:**
- `float: left;` — Each box floats to the left. The first box takes the leftmost position. The second box floats up to sit right next to the first. The third sits next to the second.
- `padding: 15px;` — Adds space inside each box.
- `width: 100px;` — Gives each box a fixed width.
- `background-color: red/yellow/green;` — Different colours so you can visually distinguish each box.

> **Thinking prompt:** What would happen if you used `float: right` on all three boxes? They would still appear on the same row, but the order would be reversed — Box 3 would appear on the far left, and Box 1 on the far right! Try it!

---

## Section 3: The CSS `clear` Property

### The Problem Float Creates

Floated elements are taken out of the normal document flow. This means elements that come **after** a floated element may end up overlapping it or wrapping around it in unexpected ways.

**Example of the problem:**

```html
<!-- HTML -->
<div class="floated-box">I am floated left</div>
<p>This paragraph appears right next to the floated box because
   float removes the box from normal flow. This might NOT be
   what we want!</p>
<p>This second paragraph ALSO wraps around the floated box,
   even though we might want it to start BELOW the box!</p>
```

```css
/* CSS */
.floated-box {
  float: left;
  width: 150px;
  background: lightblue;
  padding: 10px;
}
```

**Expected Output (problem):**
```
[ Floated  ]  This paragraph appears right next to the
[ Box      ]  floated box... This second paragraph ALSO
              wraps around the floated box...
```

This is the problem. Sometimes you want the next element to start **below** the floated element, not beside it. That is what `clear` solves!

---

### What Is the `clear` Property?

The `clear` property specifies that an element should **not** wrap around floated elements. Instead, it forces the element to **move below** any floated elements.

**The `clear` property values:**

| Value | What It Does |
|-------|-------------|
| `none` | The element is allowed to float on both sides (default) |
| `left` | The element will move below any element floated to the **left** |
| `right` | The element will move below any element floated to the **right** |
| `both` | The element will move below elements floated in **either** direction |
| `inherit` | Inherits the clear value from the parent |

> **Tip:** The most commonly used value is `clear: both` — it handles any floated element regardless of direction, so it works in every situation.

---

### Simple `clear` Example

```html
<!-- HTML -->
<div class="floated-box">I am floated left</div>
<p class="cleared-paragraph">I use clear: left, so I move BELOW the floated box.
   I do NOT wrap around it.</p>
```

```css
/* CSS */
.floated-box {
  float: left;
  width: 150px;
  background: lightblue;
  padding: 10px;
}

.cleared-paragraph {
  clear: left;   /* This paragraph will NOT wrap around the left-floated box */
}
```

**Expected Output (fixed):**
```
[ Floated Box ]

I use clear: left, so I move BELOW the floated box.
I do NOT wrap around it.
```

---

### `clear: both` — The Safe and Common Choice

Using `clear: both` ensures an element moves below **any** floated element — whether it was floated left or right. This is the most commonly used clearing technique.

```html
<!-- HTML -->
<div class="float-left">Left floated box</div>
<div class="float-right">Right floated box</div>
<div class="cleared">I use clear: both, so I appear below ALL floated boxes.</div>
```

```css
/* CSS */
.float-left {
  float: left;
  width: 150px;
  background: lightblue;
  padding: 10px;
}

.float-right {
  float: right;
  width: 150px;
  background: lightcoral;
  padding: 10px;
}

.cleared {
  clear: both;    /* Appears below BOTH left and right floated elements */
  background: lightyellow;
  padding: 10px;
}
```

**Expected Output (visual):**
```
[ Left floated box ]          [ Right floated box ]

I use clear: both, so I appear below ALL floated boxes.
```

---

## Section 4: The Clearfix Hack — Fixing Collapsed Containers

### The Dreaded Collapsed Container Problem

Here is one of the most frustrating problems beginners encounter with floats: **when all children of a container are floated, the container collapses to zero height.**

**Why does this happen?**

When elements are floated, they are removed from the normal document flow. The parent container no longer "sees" them when calculating its height — so it shrinks to nothing.

**Example of the problem:**

```html
<!-- HTML -->
<div class="container">
  <img src="image.jpg" alt="Photo" class="floated-img">
  <!-- If the paragraph is short, the container collapses! -->
</div>
<p>This paragraph appears INSIDE the collapsed container's area,
   causing layout problems.</p>
```

```css
/* CSS - THE PROBLEM */
.container {
  border: 3px solid red;
  /* The container collapses because the image inside is floated! */
}

.floated-img {
  float: right;
  width: 200px;
}
```

**Expected Output (problem):**
```
[Red border - collapsed, zero height!]
                              [ Image floats out ]
This paragraph appears where the container should be!
```

This completely breaks the layout. The red border container appears to have no height, and the image sticks out of it.

---

### Solution 1: Add `overflow: auto` to the Container

One way to fix the collapsed container is to add `overflow: auto` (or `overflow: hidden`) to the parent container. This forces the container to recalculate and include the floated children in its height.

```css
/* CSS - FIX #1 */
.container {
  border: 3px solid red;
  overflow: auto;    /* Forces container to wrap around floated children */
}

.floated-img {
  float: right;
  width: 200px;
}
```

**Expected Output (fixed):**
```
[Red border - now wraps around the image!         ]
[                                      [ Image ]  ]
[                                                 ]
```

> **Caveat:** `overflow: auto` can sometimes add unwanted scroll bars on the container. A cleaner solution is the **clearfix hack**.

---

### Solution 2: The Clearfix Hack (The Professional Solution)

The **clearfix hack** is a clever and widely-used CSS technique that fixes the collapsed container problem without any side effects. It works by inserting an invisible empty element **after** the floated content using the `::after` pseudo-element, and then applying `clear: both` to it.

**Here is the standard clearfix class:**

```css
/* THE CLEARFIX HACK */
.clearfix::after {
  content: "";          /* Creates an invisible empty element */
  display: table;       /* Makes it behave as a block-level element */
  clear: both;          /* Clears all floats */
}
```

**How to use it — just add the `clearfix` class to the parent container:**

```html
<!-- HTML: Add class="clearfix" to the container -->
<div class="container clearfix">
  <img src="image.jpg" alt="Photo" class="floated-img">
  <p>Some text beside the image.</p>
</div>
<p>This paragraph now correctly appears BELOW the container.</p>
```

```css
/* CSS */
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

.container {
  border: 3px solid red;
  /* No overflow needed! The clearfix handles it. */
}

.floated-img {
  float: right;
  width: 200px;
  margin-left: 15px;
}
```

**Expected Output (fixed):**
```
[Red border - correctly wraps around content!           ]
[                                            [ Image ]  ]
[ Some text beside the image.                           ]
[                                                       ]

This paragraph now correctly appears BELOW the container.
```

**Line-by-line breakdown of the clearfix:**
- `.clearfix::after` — Targets a virtual element added **after** the content of any element with the `clearfix` class
- `content: "";` — Creates a blank, invisible element (required for `::after` to work)
- `display: table;` — Makes the invisible element take up space like a block element
- `clear: both;` — Tells this invisible element to push past all floated elements

> **Real-world use:** The clearfix is one of the most common CSS patterns used by professional developers. You will see it in virtually every major CSS framework and project that uses floats.

---

## Section 5: Practical Float Examples

Now let's put everything together and build some real-world layouts!

### Example 1: Equal Width Boxes in a Row

This is the foundation for many grid-style layouts you see on websites.

```html
<!-- HTML -->
<div class="row clearfix">
  <div class="column">
    <h3>Feature One</h3>
    <p>This box takes up one third of the width.</p>
  </div>
  <div class="column">
    <h3>Feature Two</h3>
    <p>This box also takes up one third of the width.</p>
  </div>
  <div class="column">
    <h3>Feature Three</h3>
    <p>And this box takes the final third.</p>
  </div>
</div>
```

```css
/* CSS */
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

.row {
  background-color: #f4f4f4;
  padding: 10px;
}

.column {
  float: left;             /* All columns float left, creating a row */
  width: 33.33%;           /* Each column takes exactly 1/3 of the width */
  padding: 15px;
  box-sizing: border-box;  /* Ensures padding doesn't add to the width */
  background-color: white;
  border: 1px solid #ddd;
}
```

**Expected Output (visual):**
```
[ Feature One          ][ Feature Two          ][ Feature Three        ]
[ This box takes up    ][ This box also takes  ][ And this box takes   ]
[ one third of the     ][ up one third of the  ][ the final third.     ]
[ width.               ][ width.               ]                        ]
```

> **Thinking prompt:** What would happen if you changed the width from `33.33%` to `50%`? Only two columns would fit per row, and the third would wrap to the next line!

---

### Example 2: Image Gallery Using Float

Float is commonly used to create simple image galleries where images line up in a grid.

```html
<!-- HTML -->
<div class="gallery clearfix">
  <div class="gallery-item">
    <img src="photo1.jpg" alt="Photo 1">
    <p>Photo Caption 1</p>
  </div>
  <div class="gallery-item">
    <img src="photo2.jpg" alt="Photo 2">
    <p>Photo Caption 2</p>
  </div>
  <div class="gallery-item">
    <img src="photo3.jpg" alt="Photo 3">
    <p>Photo Caption 3</p>
  </div>
  <div class="gallery-item">
    <img src="photo4.jpg" alt="Photo 4">
    <p>Photo Caption 4</p>
  </div>
</div>
```

```css
/* CSS */
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

.gallery {
  padding: 5px;
}

.gallery-item {
  float: left;             /* Items float left to form a row */
  width: 170px;
  margin: 5px;
  text-align: center;
  border: 1px solid #ccc;
  padding: 5px;
}

.gallery-item img {
  width: 160px;
  height: 120px;
  object-fit: cover;       /* Makes images fill their space without distortion */
}
```

**Expected Output (visual):**
```
[ Photo 1  ] [ Photo 2  ] [ Photo 3  ] [ Photo 4  ]
[ Caption1 ] [ Caption2 ] [ Caption3 ] [ Caption4 ]
```

---

### Example 3: Horizontal Navigation Menu Using Float

Float can also create navigation bars where links appear side by side horizontally.

```html
<!-- HTML -->
<nav class="navbar clearfix">
  <ul>
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Services</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

```css
/* CSS */
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

.navbar {
  background-color: #333;
  overflow: auto;          /* Also works as a clearfix alternative here */
}

.navbar ul {
  list-style: none;        /* Remove bullet points */
  margin: 0;
  padding: 0;
}

.navbar li {
  float: left;             /* Each menu item floats left, creating a horizontal bar */
}

.navbar a {
  display: block;          /* Makes the whole area clickable */
  color: white;
  text-decoration: none;
  padding: 14px 16px;
}

.navbar a:hover {
  background-color: #555;  /* Highlight on hover */
}
```

**Expected Output (visual):**
```
[ Home ] [ About ] [ Services ] [ Contact ]    (all on one horizontal line, dark bar)
```

> **Real-world use:** Horizontal navigation menus like this are used on almost every website! While modern developers often use Flexbox for this now, float-based navbars are still very common in older projects.

---

### Example 4: Full Web Page Layout (Header, Content, Sidebar, Footer)

This is one of the most important uses of float — building a complete page layout!

```html
<!-- HTML -->
<div class="page-wrapper">

  <div class="header">
    <h1>My Website</h1>
  </div>

  <div class="content-area clearfix">
    <div class="main-content">
      <h2>Main Article Title</h2>
      <p>This is the main content area. It takes up about 70% of the width.
         Articles, blog posts, and primary information go here.</p>
      <p>More content here...</p>
    </div>
    <div class="sidebar">
      <h3>Sidebar</h3>
      <p>Links, ads, or extra info go here. The sidebar is 30% wide.</p>
    </div>
  </div>

  <div class="footer">
    <p>Footer - Copyright 2024</p>
  </div>

</div>
```

```css
/* CSS */
* {
  box-sizing: border-box;   /* Makes width calculations easier */
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

.page-wrapper {
  max-width: 900px;
  margin: 0 auto;           /* Centers the whole page */
}

.header {
  background-color: #2c3e50;
  color: white;
  padding: 20px;
  text-align: center;
}

.content-area {
  padding: 10px;
  background-color: #f9f9f9;
}

.main-content {
  float: left;              /* Main content floats left */
  width: 70%;               /* Takes 70% of the width */
  padding: 20px;
  background-color: white;
  border: 1px solid #ddd;
}

.sidebar {
  float: right;             /* Sidebar floats right */
  width: 28%;               /* Takes 28% of the width (2% gap between them) */
  padding: 20px;
  background-color: #ecf0f1;
  border: 1px solid #ddd;
}

.footer {
  background-color: #2c3e50;
  color: white;
  padding: 15px;
  text-align: center;
  clear: both;              /* Footer MUST clear both floats to appear below */
}
```

**Expected Output (visual):**
```
┌─────────────────────────────────────────┐
│             My Website                  │  ← Header
└─────────────────────────────────────────┘
┌────────────────────────┐ ┌─────────────┐
│  Main Article Title    │ │   Sidebar   │
│  This is the main      │ │  Links, ads │
│  content area. It      │ │  or extra   │
│  takes up about 70%... │ │  info here  │
└────────────────────────┘ └─────────────┘
┌─────────────────────────────────────────┐
│    Footer - Copyright 2024              │  ← clear: both!
└─────────────────────────────────────────┘
```

> **Key insight:** Notice that the footer uses `clear: both`. Without this, the footer would attempt to wrap around the sidebar and appear next to it — which would completely break the layout!

---

## Section 6: Guided Practice Exercises

### Exercise 1: Warm-Up — Simple Image Float

**Objective:** Practice floating a single image.

**Scenario:** You are creating a blog post page. You want a profile photo to float to the right, with the author's biography wrapping to the left of it.

**Steps:**

1. Create an HTML file with a `<div>` container
2. Inside the container, add an `<img>` tag with `src="profile.jpg"` and `alt="Author Photo"`
3. Add a `<p>` tag with 3–4 sentences of biography text
4. Apply `float: right` and a `width` of `180px` to the image
5. Add a `margin-left` of `15px` to give the image some breathing room

**Starter code:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* YOUR CSS HERE */
    .profile-img {
      /* Add: float, width, margin */
    }

    .bio-container {
      border: 1px solid #ddd;
      padding: 15px;
      max-width: 600px;
    }
  </style>
</head>
<body>

  <div class="bio-container">
    <img class="profile-img" src="profile.jpg" alt="Author Photo">
    <p>Jane Smith is a software developer with 10 years of experience.
       She specialises in frontend development and UI design. In her spare
       time, she enjoys hiking and photography. She has spoken at several
       international tech conferences.</p>
  </div>

</body>
</html>
```

**Expected Output:**
```
Bio Container:
[ Bio text appears here... Jane Smith is a     ] [ Profile ]
[ software developer with 10 years of          ] [ Photo   ]
[ experience. She specialises in frontend...   ]           ]
```

**Self-check Questions:**
- Does the image appear to the right?
- Does the text wrap to the left of the image?
- Is there a small gap between the image and the text?
- What happens when you change `float: right` to `float: left`?

---

### Exercise 2: Three-Column Layout

**Objective:** Create a three-column layout using `float: left`.

**Scenario:** You are building a product features section for a website. It needs three equal columns side by side: "Speed", "Security", and "Reliability".

**Steps:**

1. Create a wrapper `<div>` with the class `features-row` and `clearfix`
2. Inside it, create three `<div>` elements each with class `feature-col`
3. Each column should contain an `<h3>` heading and a `<p>` description
4. Style `.feature-col` with `float: left`, `width: 33.33%`, and a background colour
5. Apply the clearfix on `.clearfix::after`

**Expected Output:**
```
[ ⚡ Speed           ] [ 🔒 Security        ] [ ✅ Reliability     ]
[ Load pages in      ] [ Enterprise-grade   ] [ 99.9% uptime      ]
[ milliseconds...    ] [ encryption...      ] [ guaranteed...     ]
```

**Hints:**
- Remember `box-sizing: border-box` so padding doesn't push columns out of the row
- Add `padding: 20px` inside each column for nice spacing
- Add different background colours to clearly see the three columns

**Optional What-If Challenge:** What happens if you change the width of each column to `25%`? How many columns would fit per row? Why does the fourth column wrap to the next line?

---

### Exercise 3: Clear in Action

**Objective:** See the difference `clear` makes.

**Scenario:** You have a page with two floated boxes and a section that should appear BELOW both. Without `clear`, the section wraps awkwardly. With `clear: both`, it correctly appears below.

**Step 1 — Without clear (observe the problem):**

```html
<div class="box-left">Left Box</div>
<div class="box-right">Right Box</div>
<div class="below-section">I should be below BOTH boxes!</div>
```

```css
.box-left  { float: left;  width: 200px; background: lightblue;  padding: 20px; }
.box-right { float: right; width: 200px; background: lightcoral; padding: 20px; }
.below-section { background: lightyellow; padding: 20px; }
```

**Observe:** The "below-section" div appears wedged between the two boxes, not below them.

**Step 2 — With clear (fix the problem):**

```css
/* Add this to fix it */
.below-section {
  clear: both;   /* NOW it appears below both floated boxes */
  background: lightyellow;
  padding: 20px;
}
```

**Expected Output (fixed):**
```
[ Left Box ]                              [ Right Box ]

I should be below BOTH boxes! (now it IS!)
```

---

## Section 7: Mini Project — Build a Blog Page Layout

In this mini-project, you will build a simple but realistic blog page that uses floats for the layout, an image float in the article, and a clearfix to keep everything tidy.

### Project Overview

You will create a page with:
- A site header
- A blog article (with a floated image inside)
- A sidebar (floated to the right of the article)
- A footer that clears everything

---

### Stage 1 — HTML Structure Setup

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My Float Blog</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- Site Header -->
  <header class="site-header">
    <h1>The Float Times</h1>
    <p>Your daily dose of web design news</p>
  </header>

  <!-- Main Page Wrapper -->
  <div class="page-wrapper clearfix">

    <!-- Article Section -->
    <main class="article-section">
      <h2>Understanding CSS Float</h2>
      <img src="float-image.jpg" alt="Float illustration" class="article-img">
      <p>CSS Float is a powerful property that controls how elements
         are positioned relative to their container. When you float
         an element, it moves to the left or right of its container,
         and text naturally wraps around it.</p>
      <p>The float property was originally designed to allow text to
         wrap around images, similar to how text wraps around photos
         in newspapers and magazines.</p>
      <p>Over time, developers discovered they could use floats to
         create multi-column layouts, horizontal navigation bars,
         and all kinds of creative page structures.</p>
    </main>

    <!-- Sidebar Section -->
    <aside class="sidebar">
      <h3>Related Articles</h3>
      <ul>
        <li><a href="#">CSS Position Explained</a></li>
        <li><a href="#">Flexbox for Beginners</a></li>
        <li><a href="#">CSS Grid Layout</a></li>
      </ul>
      <h3>Tags</h3>
      <p>CSS, Layout, Float, Web Design</p>
    </aside>

  </div>

  <!-- Footer -->
  <footer class="site-footer">
    <p>The Float Times &copy; 2024. All rights reserved.</p>
  </footer>

</body>
</html>
```

---

### Stage 2 — CSS Styling

```css
/* style.css */

/* Reset and Base */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, sans-serif;
  font-size: 16px;
  color: #333;
  background-color: #f0f0f0;
}

/* ---- Clearfix ---- */
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

/* ---- Site Header ---- */
.site-header {
  background-color: #2c3e50;
  color: white;
  padding: 25px 20px;
  text-align: center;
}

.site-header h1 {
  font-size: 2em;
  margin-bottom: 5px;
}

.site-header p {
  font-size: 0.9em;
  opacity: 0.8;
}

/* ---- Page Wrapper ---- */
.page-wrapper {
  max-width: 960px;
  margin: 20px auto;
  padding: 0 10px;
}

/* ---- Article Section ---- */
.article-section {
  float: left;           /* Article floats left */
  width: 68%;            /* Takes about 2/3 of the space */
  background-color: white;
  padding: 25px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.article-section h2 {
  margin-bottom: 15px;
  color: #2c3e50;
}

.article-section p {
  line-height: 1.7;
  margin-bottom: 12px;
}

/* ---- Article Image Float ---- */
.article-img {
  float: right;          /* Image floats right INSIDE the article */
  width: 220px;
  margin: 0 0 15px 20px; /* Space on left and bottom of the image */
  border-radius: 4px;
  border: 2px solid #ddd;
}

/* ---- Sidebar ---- */
.sidebar {
  float: right;          /* Sidebar floats right */
  width: 29%;            /* Takes about 1/3 of the space */
  background-color: white;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.sidebar h3 {
  color: #2c3e50;
  margin-bottom: 10px;
  border-bottom: 2px solid #2c3e50;
  padding-bottom: 5px;
}

.sidebar ul {
  list-style: none;
  padding: 0;
}

.sidebar li {
  margin-bottom: 8px;
}

.sidebar a {
  color: #2980b9;
  text-decoration: none;
}

.sidebar a:hover {
  text-decoration: underline;
}

/* ---- Site Footer ---- */
.site-footer {
  background-color: #2c3e50;
  color: white;
  text-align: center;
  padding: 15px;
  clear: both;           /* CRITICAL: Clears all floats so footer appears below */
  margin-top: 20px;
}
```

---

### Stage 3 — Milestone Output

When you open this in a browser, you should see:

```
┌─────────────────────────────────────────────────────┐
│               The Float Times                        │  ← Header
│         Your daily dose of web design news           │
└─────────────────────────────────────────────────────┘
┌──────────────────────────────────┐ ┌───────────────┐
│  Understanding CSS Float         │ │ Related       │
│                    [ Image  ]    │ │ Articles      │
│  CSS Float is a powerful         │ │ - CSS Position│
│  property that controls...       │ │ - Flexbox     │
│                                  │ │ - CSS Grid    │
│  The float property was          │ │               │
│  originally designed to...       │ │ Tags          │
│                                  │ │ CSS, Layout.. │
└──────────────────────────────────┘ └───────────────┘
┌─────────────────────────────────────────────────────┐
│    The Float Times © 2024. All rights reserved.      │  ← Footer
└─────────────────────────────────────────────────────┘
```

### Stage 4 — Reflection Questions

1. What would happen to the layout if you removed the `clearfix` class from `.page-wrapper`?
2. What would happen if the footer did NOT have `clear: both`?
3. What would happen to the article image if you changed `float: right` to `float: left`?
4. How would you add a second article below the first? What CSS would you need?

### Optional Enhancements

- Add a navigation bar above the header with 4 links using `float: left`
- Add a second row with two equal-width related posts below the main layout
- Make the image inside the article responsive by adding `max-width: 100%`
- Add a hover effect on the sidebar links

---

## Section 8: Common Beginner Mistakes

### Mistake 1: Forgetting the Clearfix on the Parent Container

**The Problem:**
```html
<!-- WRONG: No clearfix on parent -->
<div class="container">
  <div class="float-box">Floated</div>
</div>
<p>I appear where the container should be!</p>
```

The container collapses to zero height because its only child is floated.

**The Fix:**
```html
<!-- CORRECT: Add clearfix class to parent -->
<div class="container clearfix">
  <div class="float-box">Floated</div>
</div>
<p>I now appear correctly below the container.</p>
```

---

### Mistake 2: Forgetting `clear: both` on the Footer

**The Problem:**
```css
/* WRONG: Footer has no clear */
.footer {
  background: #333;
  color: white;
  padding: 20px;
  /* Footer wraps beside the sidebar! */
}
```

**The Fix:**
```css
/* CORRECT: Footer clears all floats */
.footer {
  background: #333;
  color: white;
  padding: 20px;
  clear: both;    /* ALWAYS add this to footers and section breaks */
}
```

---

### Mistake 3: Column Widths Adding Up to More Than 100%

**The Problem:**
```css
/* WRONG: 33.33% + 33.33% + 33.33% + padding = MORE than 100%! */
.column {
  float: left;
  width: 33.33%;
  padding: 20px;   /* This adds EXTRA width, pushing the third column to the next row! */
}
```

**The Fix:**
```css
/* CORRECT: Use box-sizing: border-box */
.column {
  float: left;
  width: 33.33%;
  padding: 20px;
  box-sizing: border-box;  /* Padding is now INCLUDED in the 33.33% width */
}
```

> **What is `box-sizing: border-box`?** By default, CSS adds padding and border ON TOP of the stated width. With `box-sizing: border-box`, the padding and border are included INSIDE the width — so `width: 33.33%` means the whole box is 33.33% wide, including padding.

---

### Mistake 4: Using `float` When You Mean `position`

Float and position are different tools. Float makes content flow around an element. Position lets you place an element at an exact coordinate on the screen. Do not use float to try to achieve the effect of `position: absolute` or `position: fixed` — they are different tools for different situations.

---

### Mistake 5: Not Using `box-sizing: border-box` Globally

Many beginners forget to set `box-sizing: border-box` for all elements. A great habit is to always add this at the top of your CSS:

```css
/* Put this at the very top of every CSS file */
* {
  box-sizing: border-box;
}
```

This ensures that padding and borders are always included in element widths — making float-based layouts much easier to calculate.

---

## Section 9: Reflection Questions

Take a moment to test your understanding:

1. What is the default value of the `float` property?
2. What is the difference between `clear: left` and `clear: both`?
3. Why does a parent container collapse when all its children are floated?
4. What does the clearfix hack do, and why do we use `::after`?
5. Why must we add `clear: both` to the footer of a float-based layout?
6. What does `box-sizing: border-box` do and why is it important with floated columns?
7. If you have three `<div>` elements each floated left with `width: 33.33%`, what happens if one of them has `width: 34%` instead?
8. What `clear` value would you use if you only have left-floated elements and no right-floated elements?
9. Can an image inside a floated container itself be floated? (Hint: Yes! We demonstrated this in the project.)
10. When would you choose `overflow: auto` over the clearfix hack?

---

## Section 10: Completion Checklist

Use this checklist to confirm you have mastered this lesson:

- [ ] I understand what the `float` property does and why it exists
- [ ] I can use `float: left` and `float: right` to position elements
- [ ] I understand what `float: none` means and that it is the default
- [ ] I know what happens when multiple block elements are floated left
- [ ] I understand why parent containers collapse when children are floated
- [ ] I can use `clear: both` to prevent elements from wrapping around floated content
- [ ] I know and can write the clearfix hack from memory
- [ ] I can build a three-column layout using `float: left` and `width: 33.33%`
- [ ] I can create an image gallery using floats
- [ ] I can build a horizontal navigation menu using `float: left`
- [ ] I can build a full page layout with header, article, sidebar, and footer
- [ ] I understand why `box-sizing: border-box` is important for float layouts
- [ ] I can identify and fix common float mistakes

---

## Lesson Summary

Congratulations! In this lesson, you have learned one of the foundational CSS layout techniques: **the `float` property**.

Here is a quick recap of everything you covered:

**The `float` property** positions an element to the left or right of its container, allowing text and other content to wrap around it. Its values are `left`, `right`, `none` (default), and `inherit`.

**The `clear` property** stops an element from wrapping around floated content. Use `clear: both` to push an element below any floated element — this is critical for footers and section breaks.

**The collapsed container problem** occurs when all children of a container are floated. The container shrinks to zero height because floated elements are removed from normal flow.

**The clearfix hack** solves this with a simple reusable CSS class:
```css
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

**Real-world uses of float** include text-wrapping around images, equal-width column layouts, image galleries, horizontal navigation menus, and full page layouts (header + content + sidebar + footer).

**Key reminders:**
- Always add the clearfix class to containers with floated children
- Always use `clear: both` on footers
- Always use `box-sizing: border-box` when working with floated columns
- Float widths must add up to 100% (or less) to stay on one row

> **What comes next?** Now that you understand floats, you are ready to explore modern layout alternatives: **CSS Flexbox** and **CSS Grid** — which are even more powerful and flexible. The concepts you learned here (how elements flow, how to control side-by-side placement) will help you understand those tools much faster!

---

*Lesson 25 Complete — CSS Float, Clear, and Clearfix*
