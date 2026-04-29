---
render_with_liquid: false
title: "CSS Tooltips and Tooltip Arrows"
nav_order: 57
---

# Lesson 57: CSS Tooltips and Tooltip Arrows

---

## Lesson Introduction

Have you ever hovered your mouse over a button on a website and seen a little box pop up with some extra information? That little pop-up box is called a **tooltip**. Tooltips are one of the most practical and polished features you can add to any website. They help users understand what a button, icon, or piece of text does — without cluttering the page with extra text that is always visible.

In this lesson, you will learn:

- What a tooltip is and why it exists
- How to build a basic tooltip using only HTML and CSS
- How to position tooltips above, below, to the left, and to the right of any element
- How to make tooltips appear and disappear smoothly with a fade animation
- How to add a **small arrow** to tooltips to make them look professional and point at the element they belong to
- How to apply your knowledge by completing a full mini-project: a CSS-only help icon tooltip system

No JavaScript is needed for any of this. Pure CSS is all you need!

---

## Prerequisite Concepts

Before we dive into tooltips, let us make sure you understand the building blocks we will use. Do not worry — everything is explained from scratch below.

### What is `position: relative` and `position: absolute`?

Think of `position: relative` like telling an element: *"Stay where you are, but you are now the reference point for any children positioned inside you."*

Think of `position: absolute` like telling an element: *"Leave your normal place in the page and stick yourself to a specific spot inside your nearest positioned parent."*

```html
<div style="position: relative; width: 200px; height: 100px; background: lightblue;">
  Parent (relative)
  <div style="position: absolute; bottom: 0; right: 0; background: coral;">
    Child (absolute)
  </div>
</div>
```

**Expected visual result:** The coral child box sticks to the bottom-right corner of the light blue parent box.

This is exactly the technique we use to position tooltips — the tooltip is the `absolute` child, and the trigger element (button, word, icon) is the `relative` parent.

---

### What is `visibility: hidden` vs `display: none`?

Both hide an element, but they behave differently:

- `visibility: hidden` — hides the element visually, but it **still takes up space** on the page.
- `display: none` — hides the element AND removes it from the page layout (as if it does not exist).

For tooltips, we use `visibility: hidden` by default and `visibility: visible` on hover, because this lets CSS transitions and animations work smoothly.

---

### What is `opacity`?

`opacity` controls how transparent an element is, from `0` (completely invisible) to `1` (completely visible). We use `opacity: 0` along with `visibility: hidden` at the start, and `opacity: 1` along with `visibility: visible` on hover. This combination gives us a beautiful fade-in effect.

---

### What is `:hover`?

`:hover` is a CSS **pseudo-class**. It means "apply these styles only when the user's mouse is hovering over this element."

```css
/* Normal state */
p {
  color: black;
}

/* When mouse is on top of the paragraph */
p:hover {
  color: red;
}
```

**Expected result:** The text is black normally. It turns red when you hover over it.

---

### What is the `::after` pseudo-element?

`::after` lets you insert a small piece of visual content **after** an element's real content, using only CSS — no extra HTML needed. We use this trick to draw the tiny triangle arrows on tooltips.

```css
p::after {
  content: " ← I appear after the text!";
  color: green;
}
```

**Expected result:** Every `<p>` element gets that green text appended visually after its content, without any change to the HTML.

---

## Part 1 — Understanding CSS Tooltips

### What Is a Tooltip?

A **tooltip** is a small pop-up label that appears when a user hovers over an element. It is used to provide extra information without permanently occupying space on the page.

**Real-world examples:**
- Hovering over a save icon in a document editor shows "Save File"
- Hovering over a disabled button shows "You do not have permission to do this"
- Hovering over an abbreviated term shows its full meaning
- Hovering over social media share icons shows "Share on Twitter"

Tooltips improve **user experience** (UX) by making interfaces self-explanatory.

---

### The Core HTML Structure of a Tooltip

Every CSS tooltip needs exactly **two elements**:

1. A **trigger element** — the thing the user hovers over (a button, a word, a div)
2. A **tooltip box** — the pop-up that appears on hover

They are wrapped together in a parent container that uses `position: relative`.

```html
<!-- The trigger and tooltip live together inside one parent -->
<div class="tooltip-container">
  Hover over me           <!-- This is the trigger -->
  <span class="tooltip">I am the tooltip!</span>  <!-- This is the pop-up -->
</div>
```

**Why wrap them?** Because when we set the tooltip's position to `absolute`, it positions itself relative to its nearest `position: relative` ancestor. By making the wrapper `relative`, the tooltip always knows exactly where to place itself — right next to the trigger.

---

### The Core CSS of a Basic Tooltip

Let us look at the CSS step-by-step:

```css
/* STEP 1: Make the wrapper the reference point */
.tooltip-container {
  position: relative;   /* All absolute children will position relative to this */
  display: inline-block; /* Makes the container shrink-wrap around its content */
  cursor: help;          /* Show a ? cursor to hint that more info is available */
}

/* STEP 2: Style and hide the tooltip by default */
.tooltip {
  visibility: hidden;    /* Hidden until hover — but still in the document */
  background-color: #333; /* Dark grey background */
  color: #fff;            /* White text for contrast */
  text-align: center;     /* Centre the text inside the tooltip */
  padding: 5px 10px;      /* Add some breathing room around the text */
  border-radius: 6px;     /* Rounded corners look modern */
  width: 160px;           /* Fixed width so the tooltip doesn't stretch too wide */

  /* STEP 3: Position it absolutely above the trigger */
  position: absolute;
  z-index: 1;             /* Make sure tooltip appears on top of other content */
  bottom: 125%;           /* Push it 125% of the trigger's height above it */
  left: 50%;              /* Start from the centre of the trigger */
  margin-left: -80px;     /* Pull it back left by half of width (160/2=80) to centre it */
}

/* STEP 4: Show the tooltip when hovering over the WRAPPER */
.tooltip-container:hover .tooltip {
  visibility: visible;    /* Make it appear */
}
```

Let us trace through what happens when you hover:

1. Mouse enters `.tooltip-container` → the `:hover` state activates
2. CSS sees `.tooltip-container:hover .tooltip` → targets the child `.tooltip`
3. Changes `visibility` from `hidden` to `visible`
4. The tooltip appears above the trigger!

---

### Full Working Example — Basic Tooltip

```html
<!DOCTYPE html>
<html>
<head>
<style>
  body {
    font-family: Arial, sans-serif;
    padding: 100px;  /* Give room so tooltip doesn't clip at screen edge */
  }

  .tooltip-container {
    position: relative;
    display: inline-block;
    cursor: help;
  }

  .tooltip {
    visibility: hidden;
    background-color: #333;
    color: #fff;
    text-align: center;
    padding: 5px 10px;
    border-radius: 6px;
    width: 160px;

    position: absolute;
    z-index: 1;
    bottom: 125%;
    left: 50%;
    margin-left: -80px;
  }

  .tooltip-container:hover .tooltip {
    visibility: visible;
  }
</style>
</head>
<body>

<div class="tooltip-container">
  Hover over me
  <span class="tooltip">This is the tooltip text!</span>
</div>

</body>
</html>
```

**Expected output when you hover:**
```
+---------------------------+
| This is the tooltip text! |
+---------------------------+
        ▲
  Hover over me
```

A dark tooltip box with white text appears above the words "Hover over me."

> 💡 **Thinking Prompt:** What happens if you remove `position: relative` from `.tooltip-container`? The tooltip will position itself relative to the `<body>` instead, and will likely appear somewhere completely unexpected on the page!

---

## Part 2 — Positioning Tooltips in Four Directions

You are not limited to showing tooltips above the trigger. You can show them below, to the left, or to the right. Each direction uses a different combination of `top`, `bottom`, `left`, and `right` values.

---

### Tooltip on Top (Default)

We already covered this. Here is the summary:

```css
.tooltip-top {
  bottom: 125%;   /* Push up above the trigger */
  left: 50%;
  margin-left: -80px;  /* Centre horizontally */
}
```

---

### Tooltip Below the Trigger

Instead of `bottom`, use `top` to push the tooltip down below the trigger:

```css
.tooltip-bottom {
  top: 125%;    /* Push DOWN below the trigger */
  left: 50%;
  margin-left: -80px;  /* Centre horizontally */
}
```

**Visual result:**
```
  Hover over me
        ▼
+---------------------------+
| This is the tooltip text! |
+---------------------------+
```

---

### Tooltip to the Left of the Trigger

For a left tooltip, push it to the left using `right` and vertically centre it using `top`:

```css
.tooltip-left {
  top: -5px;          /* Align vertically with the trigger */
  right: 105%;        /* Push it to the LEFT of the trigger */
}
```

**Visual result:**
```
+---------------------------+
| This is the tooltip text! |  ← Hover over me
+---------------------------+
```

---

### Tooltip to the Right of the Trigger

For a right tooltip, push it to the right using `left`:

```css
.tooltip-right {
  top: -5px;         /* Align vertically */
  left: 105%;        /* Push it to the RIGHT of the trigger */
}
```

**Visual result:**
```
Hover over me →  +---------------------------+
                 | This is the tooltip text! |
                 +---------------------------+
```

---

### Full Example — All Four Directions

```html
<!DOCTYPE html>
<html>
<head>
<style>
  body {
    font-family: Arial, sans-serif;
    display: flex;
    gap: 40px;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .tooltip-container {
    position: relative;
    display: inline-block;
    cursor: help;
    background: #e0e0e0;
    padding: 10px 15px;
    border-radius: 4px;
  }

  /* Shared tooltip styles */
  .tooltip {
    visibility: hidden;
    background-color: #333;
    color: #fff;
    text-align: center;
    padding: 6px 10px;
    border-radius: 6px;
    width: 140px;
    position: absolute;
    z-index: 1;
  }

  /* TOP */
  .tooltip-top {
    bottom: 125%;
    left: 50%;
    margin-left: -70px;
  }

  /* BOTTOM */
  .tooltip-bottom {
    top: 125%;
    left: 50%;
    margin-left: -70px;
  }

  /* LEFT */
  .tooltip-left {
    top: -5px;
    right: 105%;
  }

  /* RIGHT */
  .tooltip-right {
    top: -5px;
    left: 105%;
  }

  /* Show on hover */
  .tooltip-container:hover .tooltip {
    visibility: visible;
  }
</style>
</head>
<body>

  <div class="tooltip-container">
    Top
    <span class="tooltip tooltip-top">I appear above!</span>
  </div>

  <div class="tooltip-container">
    Bottom
    <span class="tooltip tooltip-bottom">I appear below!</span>
  </div>

  <div class="tooltip-container">
    Left
    <span class="tooltip tooltip-left">I appear left!</span>
  </div>

  <div class="tooltip-container">
    Right
    <span class="tooltip tooltip-right">I appear right!</span>
  </div>

</body>
</html>
```

**Expected output:** Four grey pill-shaped trigger elements. Hovering each one reveals a dark tooltip in the corresponding direction.

---

## Part 3 — Adding a Fade-In Animation to Tooltips

Right now, tooltips snap into view instantly. That feels a little abrupt. We can make them fade in smoothly using CSS `opacity` and `transition`.

### Why Fade-In Feels Better

Think of a light switch (no fade) vs. a dimmer switch (smooth fade). A smooth fade-in feels more natural and polished.

### The Fade-In Technique

Add these two properties to the `.tooltip` default style:

```css
.tooltip {
  /* ... all your existing styles ... */

  opacity: 0;           /* Start completely invisible */
  transition: opacity 0.4s;  /* Take 0.4 seconds to animate opacity changes */
}
```

Then, on hover, set `opacity` to `1`:

```css
.tooltip-container:hover .tooltip {
  visibility: visible;
  opacity: 1;   /* Fade IN to fully visible */
}
```

### Why Do We Need Both `visibility` AND `opacity`?

Good question! Here is the reason:

- `opacity: 0` makes the element invisible, **but it still captures mouse events** (you can accidentally hover over it)
- `visibility: hidden` makes the element completely inert — clicks and hovers pass through it

By combining both, we get:
- Default: `visibility: hidden` + `opacity: 0` → tooltip is invisible AND does not interfere
- On hover: `visibility: visible` + `opacity: 1` → tooltip fades in AND is fully interactive

The `transition` only animates `opacity` (because `visibility` cannot be animated smoothly). The `visibility` change happens instantly, which is fine — it just enables the element to exist, while `opacity` handles the visual fade.

### Full Example with Fade-In

```html
<!DOCTYPE html>
<html>
<head>
<style>
  body {
    font-family: Arial, sans-serif;
    padding: 120px;
  }

  .tooltip-container {
    position: relative;
    display: inline-block;
    cursor: help;
  }

  .tooltip {
    visibility: hidden;
    opacity: 0;                  /* Start invisible */
    transition: opacity 0.4s;   /* Smooth 0.4 second fade */

    background-color: #333;
    color: #fff;
    text-align: center;
    padding: 6px 12px;
    border-radius: 6px;
    width: 160px;

    position: absolute;
    z-index: 1;
    bottom: 125%;
    left: 50%;
    margin-left: -80px;
  }

  .tooltip-container:hover .tooltip {
    visibility: visible;
    opacity: 1;   /* Fade to fully visible */
  }
</style>
</head>
<body>

<p>Hover over the text below to see the fade-in tooltip:</p>

<div class="tooltip-container">
  ✨ Hover me!
  <span class="tooltip">I fade in smoothly 😊</span>
</div>

</body>
</html>
```

**Expected result:** When you hover over "✨ Hover me!", the tooltip gently fades in over 0.4 seconds.

> 💡 **Thinking Prompt:** What happens if you change `transition: opacity 0.4s` to `transition: opacity 2s`? The fade will take 2 full seconds — very slow!

---

## Part 4 — Tooltip Arrows

Now let us level up. Real-world tooltips usually have a **small triangle arrow** that points from the tooltip box to the element it is describing. This makes it clearer which element the tooltip is referring to.

### What Is a "CSS Arrow" Made Of?

Here is the clever trick: CSS arrows are made from a **zero-size element with only a border**.

When an element has zero width and zero height, its borders form four triangles that meet in the middle. By making three of those borders transparent and one coloured, you get a single triangle pointing in one direction.

Let us visualise this:

```
border-left (transparent)   border-right (transparent)
         \                    /
          \                  /
           \________________/
           /                \
          /                  \
         /                    \
border-bottom (coloured)    → This forms a DOWN-pointing triangle
```

In CSS:

```css
/* A downward-pointing arrow using borders */
.arrow {
  width: 0;
  height: 0;
  border-left: 10px solid transparent;   /* Left side of triangle (invisible) */
  border-right: 10px solid transparent;  /* Right side of triangle (invisible) */
  border-top: 10px solid #333;           /* Top = the visible part = points DOWN */
}
```

**Expected visual result:** A small solid dark triangle pointing downward.

By changing which border is coloured and which are transparent, you control which direction the arrow points:

| Arrow Direction | Coloured Border | Effect |
|---|---|---|
| Down | `border-top: solid` | Triangle points downward |
| Up | `border-bottom: solid` | Triangle points upward |
| Right | `border-left: solid` | Triangle points rightward |
| Left | `border-right: solid` | Triangle points leftward |

---

### Adding Arrows with `::after`

We use the `::after` pseudo-element to attach the arrow to the tooltip box — no extra HTML needed! The arrow is purely decorative CSS.

The `::after` pseudo-element acts like an invisible child element placed right after the tooltip's content. We position it with `absolute` to place it exactly where we want.

---

### Arrow for a Top Tooltip (Arrow Points Down)

When the tooltip is **above** the trigger, the arrow should point **downward** (toward the trigger below it).

```css
/* The tooltip box — same as before */
.tooltip {
  visibility: hidden;
  background-color: #333;
  color: #fff;
  text-align: center;
  padding: 6px 10px;
  border-radius: 6px;
  width: 160px;
  position: absolute;
  z-index: 1;
  bottom: 125%;
  left: 50%;
  margin-left: -80px;
}

/* The arrow — appears BELOW the tooltip box, points DOWN */
.tooltip::after {
  content: "";               /* Required — without this, ::after doesn't exist */
  position: absolute;        /* Position it relative to the tooltip box */
  top: 100%;                 /* Place it at the BOTTOM edge of the tooltip */
  left: 50%;                 /* Start from the middle */
  margin-left: -5px;         /* Centre the 10px-wide arrow (10/2 = 5) */
  border-width: 5px;         /* Size of the triangle */
  border-style: solid;
  border-color: #333 transparent transparent transparent;
  /* Top border = dark (visible), rest = transparent → arrow points DOWN */
}

.tooltip-container:hover .tooltip {
  visibility: visible;
}
```

Let us decode `border-color: #333 transparent transparent transparent`:

The four values map to: **top, right, bottom, left** (clockwise from top). So:
- `top` = `#333` → the dark coloured side → this forms the arrow pointing downward
- `right` = `transparent`
- `bottom` = `transparent`
- `left` = `transparent`

**Visual result:**
```
+---------------------------+
|   This is the tooltip!    |
+---------------------------+
             ▼    ← arrow points down to the trigger
      [Trigger element]
```

---

### Arrow for a Bottom Tooltip (Arrow Points Up)

When the tooltip is **below** the trigger, the arrow should point **upward** (toward the trigger above it).

```css
.tooltip-bottom {
  top: 125%;
  left: 50%;
  margin-left: -80px;
}

.tooltip-bottom::after {
  content: "";
  position: absolute;
  bottom: 100%;    /* Place it at the TOP edge of the tooltip */
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: transparent transparent #333 transparent;
  /* Bottom border = dark → arrow points UP */
}
```

**Visual result:**
```
      [Trigger element]
             ▲    ← arrow points up to the trigger
+---------------------------+
|   This is the tooltip!    |
+---------------------------+
```

---

### Arrow for a Left Tooltip (Arrow Points Right)

When the tooltip is to the **left** of the trigger, the arrow should point **rightward** (toward the trigger).

```css
.tooltip-left {
  top: -5px;
  right: 105%;
}

.tooltip-left::after {
  content: "";
  position: absolute;
  top: 50%;              /* Vertically centre the arrow */
  left: 100%;            /* Place at the RIGHT edge of the tooltip */
  margin-top: -5px;      /* Adjust for the 10px-tall arrow */
  border-width: 5px;
  border-style: solid;
  border-color: transparent transparent transparent #333;
  /* Left border = dark → arrow points RIGHT */
}
```

**Visual result:**
```
+---------------------------+
|   This is the tooltip!    | → [Trigger element]
+---------------------------+
```

---

### Arrow for a Right Tooltip (Arrow Points Left)

When the tooltip is to the **right** of the trigger, the arrow should point **leftward** (toward the trigger).

```css
.tooltip-right {
  top: -5px;
  left: 105%;
}

.tooltip-right::after {
  content: "";
  position: absolute;
  top: 50%;              /* Vertically centre */
  right: 100%;           /* Place at the LEFT edge of the tooltip */
  margin-top: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: transparent #333 transparent transparent;
  /* Right border = dark → arrow points LEFT */
}
```

**Visual result:**
```
[Trigger element] ← +---------------------------+
                     |   This is the tooltip!    |
                     +---------------------------+
```

---

### Quick Summary: Arrow Direction Table

| Tooltip Position | Arrow Points | `border-color` (top right bottom left) | Arrow `position` on tooltip |
|---|---|---|---|
| Top | Down | `#333 transparent transparent transparent` | `top: 100%`, `left: 50%` |
| Bottom | Up | `transparent transparent #333 transparent` | `bottom: 100%`, `left: 50%` |
| Left | Right | `transparent transparent transparent #333` | `top: 50%`, `left: 100%` |
| Right | Left | `transparent #333 transparent transparent` | `top: 50%`, `right: 100%` |

---

## Part 5 — Guided Practice Exercises

### Exercise 1 — Simple Hover Tooltip

**Objective:** Build your first working tooltip from scratch.

**Scenario:** You are building a settings page for an app. There is a checkbox labelled "Enable notifications." You want a tooltip to explain what this does when users hover over it.

**Steps:**

1. Create a new HTML file.
2. Add a checkbox input with a label.
3. Wrap the label in a `div` with class `tooltip-container`.
4. Inside that div, also add a `span` with class `tooltip` containing the text: "You will receive email and push notifications for all updates."
5. Write the CSS to hide the tooltip by default.
6. Write the CSS to show it on hover (position it above the label).

**Expected Output:**

When you hover over the label text, a dark grey tooltip box appears above it with the explanation text.

**Hint:** Remember the two key CSS rules:
- `.tooltip-container` needs `position: relative` and `display: inline-block`
- `.tooltip` needs `position: absolute`, `visibility: hidden`, and positioning with `bottom: 125%`

**Self-check Questions:**
- Does your tooltip disappear when you move the mouse away?
- Is the tooltip text readable (white on dark background)?
- Is the tooltip positioned above (not overlapping) the trigger?

---

### Exercise 2 — Four-Direction Tooltips for Icons

**Objective:** Create a row of four icon buttons, each with a tooltip in a different direction.

**Scenario:** You are designing a text editor toolbar. There are four action icons: Bold (B), Italic (I), Underline (U), and Link (🔗). Each icon needs a descriptive tooltip.

**Setup:**

```html
<div class="toolbar">
  <div class="tooltip-container">
    <button>B</button>
    <!-- Add top tooltip: "Bold text" -->
  </div>

  <div class="tooltip-container">
    <button>I</button>
    <!-- Add bottom tooltip: "Italic text" -->
  </div>

  <div class="tooltip-container">
    <button>U</button>
    <!-- Add left tooltip: "Underline text" -->
  </div>

  <div class="tooltip-container">
    <button>🔗</button>
    <!-- Add right tooltip: "Insert link" -->
  </div>
</div>
```

**Steps:**
1. Add the tooltip `<span>` elements inside each `.tooltip-container`.
2. Add unique classes for each direction (e.g., `tooltip-top`, `tooltip-bottom`, etc.).
3. Write CSS for each direction class with the correct `top`, `bottom`, `left`, `right` positioning.
4. Show all tooltips on hover.

**Expected Output:** Four buttons in a row. Hovering each shows a tooltip in its designated direction.

**What-if Challenge:** What happens if you try giving the "B" button tooltip a width of `300px` but the trigger is only `40px` wide? How do you keep it centred? (Hint: adjust `margin-left` to be negative half of the width.)

---

### Exercise 3 — Fade Tooltip with Arrow

**Objective:** Build a tooltip with both a fade animation AND a downward-pointing arrow.

**Scenario:** You are building a product page. There is a price with a small ⓘ (info) icon next to it. Hovering the icon should fade in a tooltip explaining the price includes tax, with an arrow pointing to the icon.

**Steps:**
1. Create the HTML with a `span` containing the ⓘ character as the trigger.
2. Inside it, add the tooltip span.
3. Set `opacity: 0` and `transition: opacity 0.5s` on the tooltip.
4. Set `opacity: 1` and `visibility: visible` on hover.
5. Add `::after` to the tooltip with the correct border trick to make a downward arrow.

**Expected Output:** Hovering the ⓘ fades in a tooltip above it with a small downward arrow pointing at the icon.

---

## Part 6 — Mini Project: Interactive Glossary Card with Tooltips

In this mini-project, you will build a complete, professional-looking **CSS glossary card** for a technical topic. Hovering over specialised words will reveal tooltip definitions. Each tooltip will have an arrow, a fade-in animation, and a different position depending on where the word sits on the card.

### Project Overview

You will create a card about "Web Development Concepts" with three technical terms that reveal definitions when hovered.

---

### Stage 1 — Setup the Card Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Web Dev Glossary</title>
  <link rel="stylesheet" href="glossary.css">
</head>
<body>

<div class="card">
  <h2>Web Development Concepts</h2>
  <p>
    When you write a web page, you use
    <span class="term">HTML
      <span class="tooltip tooltip-top">
        HyperText Markup Language — the skeleton structure of every web page.
      </span>
    </span>
    to define the structure. You style it with
    <span class="term">CSS
      <span class="tooltip tooltip-right">
        Cascading Style Sheets — controls colours, fonts, and layout.
      </span>
    </span>
    and add interactivity with
    <span class="term">JavaScript
      <span class="tooltip tooltip-bottom">
        A programming language that makes web pages dynamic and interactive.
      </span>
    </span>.
  </p>
</div>

</body>
</html>
```

**Milestone output after Stage 1:** You see a card with the three terms — HTML, CSS, JavaScript — underlined to indicate they are hoverable.

---

### Stage 2 — The Core CSS

Create `glossary.css`:

```css
/* Page layout */
body {
  font-family: 'Segoe UI', Tahoma, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: #f0f4f8;
  margin: 0;
}

/* The card */
.card {
  background: white;
  border-radius: 12px;
  padding: 30px 40px;
  max-width: 500px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.1);
  line-height: 1.8;
}

.card h2 {
  color: #2c3e50;
  margin-bottom: 16px;
}

/* The hoverable term */
.term {
  position: relative;
  display: inline-block;
  color: #2980b9;
  text-decoration: underline dotted;
  cursor: help;
  font-weight: bold;
}
```

**Milestone output after Stage 2:** A clean white card on a soft blue-grey background. The three terms (HTML, CSS, JavaScript) appear in blue with dotted underlines.

---

### Stage 3 — Tooltip Styles and Animations

Add this to `glossary.css`:

```css
/* Base tooltip styles — hidden by default */
.tooltip {
  visibility: hidden;
  opacity: 0;
  transition: opacity 0.3s ease;

  background-color: #2c3e50;
  color: #ecf0f1;
  text-align: left;
  padding: 8px 12px;
  border-radius: 6px;
  width: 200px;
  font-size: 13px;
  font-weight: normal;
  line-height: 1.5;

  position: absolute;
  z-index: 10;
}

/* Show tooltip on hover */
.term:hover .tooltip {
  visibility: visible;
  opacity: 1;
}
```

**Milestone output after Stage 3:** Hovering over any term now fades in a dark tooltip. It appears but may not be positioned correctly yet — we fix that next.

---

### Stage 4 — Position Each Tooltip Differently

Add to `glossary.css`:

```css
/* TOP tooltip for HTML */
.tooltip-top {
  bottom: 130%;
  left: 50%;
  margin-left: -100px;
}

/* Arrow: points DOWN */
.tooltip-top::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: #2c3e50 transparent transparent transparent;
}

/* RIGHT tooltip for CSS */
.tooltip-right {
  top: -8px;
  left: 105%;
}

/* Arrow: points LEFT */
.tooltip-right::after {
  content: "";
  position: absolute;
  top: 50%;
  right: 100%;
  margin-top: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: transparent #2c3e50 transparent transparent;
}

/* BOTTOM tooltip for JavaScript */
.tooltip-bottom {
  top: 130%;
  left: 50%;
  margin-left: -100px;
}

/* Arrow: points UP */
.tooltip-bottom::after {
  content: "";
  position: absolute;
  bottom: 100%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: transparent transparent #2c3e50 transparent;
}
```

**Milestone output after Stage 4:** Each term shows its tooltip in the designated direction, with a small arrow pointing at the term. Tooltips fade in smoothly.

---

### Stage 5 — Reflection and Optional Enhancements

**Reflection Questions:**
- What does the `z-index: 10` on `.tooltip` prevent? (Answer: It stops other content from appearing on top of the tooltip)
- Why is `display: inline-block` on `.term` important? (Answer: `position: relative` only creates a reference box for block and inline-block elements, not pure inline elements in all browsers)
- What would happen if two tooltips overlapped? How could you prevent that?

**Optional Enhancements to Try:**
- Change the tooltip background colour to match each term's colour: blue for HTML, orange for CSS, yellow for JavaScript
- Add a second line to each tooltip definition with an example sentence
- Make the card title also have a tooltip that says "Hover any blue term to see its definition"
- Try changing `transition: opacity 0.3s ease` to `transition: opacity 0.3s ease, transform 0.3s ease` and add `transform: translateY(4px)` to the default tooltip and `transform: translateY(0)` on hover — the tooltip will now slide in slightly from below!

---

## Part 7 — Common Beginner Mistakes

### Mistake 1: Forgetting `position: relative` on the parent

**Wrong:**
```css
.tooltip-container {
  display: inline-block;
  /* Missing position: relative! */
}

.tooltip {
  position: absolute;
  bottom: 125%;
  /* This will be positioned relative to the nearest positioned ancestor,
     which could be the body — causing the tooltip to appear far away! */
}
```

**Correct:**
```css
.tooltip-container {
  position: relative;  /* ← This is essential! */
  display: inline-block;
}
```

---

### Mistake 2: Using `display: none` instead of `visibility: hidden`

**Wrong:**
```css
.tooltip {
  display: none;  /* Cannot transition from display: none to display: block */
}

.tooltip-container:hover .tooltip {
  display: block;  /* This pops in instantly — no fade is possible */
}
```

**Correct:**
```css
.tooltip {
  visibility: hidden;  /* Hidden but animatable */
  opacity: 0;
  transition: opacity 0.3s;
}

.tooltip-container:hover .tooltip {
  visibility: visible;
  opacity: 1;
}
```

---

### Mistake 3: Wrong selector for showing the tooltip

**Wrong:**
```css
/* This only shows the tooltip when hovering the tooltip ITSELF,
   not when hovering the parent trigger */
.tooltip:hover {
  visibility: visible;
}
```

**Correct:**
```css
/* Hover the CONTAINER → show the child tooltip */
.tooltip-container:hover .tooltip {
  visibility: visible;
}
```

---

### Mistake 4: Forgetting `content: ""` on `::after`

**Wrong:**
```css
.tooltip::after {
  /* Missing content property! */
  position: absolute;
  border-width: 5px;
  /* Nothing will appear at all */
}
```

**Correct:**
```css
.tooltip::after {
  content: "";  /* Empty string — required for pseudo-elements to render */
  position: absolute;
  border-width: 5px;
  border-style: solid;
  border-color: #333 transparent transparent transparent;
}
```

---

### Mistake 5: Misaligning the tooltip (not centring it)

**Wrong:**
```css
.tooltip {
  position: absolute;
  bottom: 125%;
  left: 0;  /* This aligns the tooltip's LEFT edge with the trigger's LEFT edge */
}
```

**Correct:**
```css
.tooltip {
  width: 160px;
  position: absolute;
  bottom: 125%;
  left: 50%;           /* Move the tooltip's left edge to the trigger's centre */
  margin-left: -80px;  /* Pull it back left by half its width (160 / 2 = 80) */
}
```

---

### Mistake 6: Applying `::after` to the wrong element

**Wrong:**
```css
/* Arrow is added to the container, not the tooltip */
.tooltip-container::after {
  content: "";
  /* This creates an arrow on the outer wrapper, not on the tooltip box */
}
```

**Correct:**
```css
/* Arrow belongs to the tooltip box */
.tooltip::after {
  content: "";
  /* Positioned relative to the tooltip box */
}
```

---

## Part 8 — Reflection Questions

Think carefully about each question. Try to answer before checking by experimenting in your browser:

1. If you increase `border-width` from `5px` to `15px` in the `::after` arrow, what happens to the arrow's size?

2. The tooltip has `z-index: 1` (or `z-index: 10`). Why is this necessary? What would happen without it?

3. What would happen if you removed `width: 160px` from the tooltip? How would the tooltip look?

4. Can you use the same tooltip technique on an `<img>` element, not just text? What would the HTML look like?

5. Why do you need `display: inline-block` on `.tooltip-container` rather than just leaving it as a default `inline` element?

6. The fade-in uses `transition: opacity 0.3s`. What would happen if the user's browser had animations disabled (e.g., for accessibility preferences)? Should you handle this case?

---

## Completion Checklist

Go through each item. Tick it mentally when you are confident you can do it:

- [ ] I can explain what a tooltip is and give three real-world examples of where they are used
- [ ] I understand why we use `position: relative` on the parent and `position: absolute` on the tooltip
- [ ] I can build a basic tooltip that appears above its trigger element on hover
- [ ] I can position a tooltip in all four directions: top, bottom, left, right
- [ ] I understand the difference between `visibility: hidden` and `display: none` for tooltips
- [ ] I can add a smooth fade-in effect using `opacity` and `transition`
- [ ] I understand how CSS border tricks create triangles for tooltip arrows
- [ ] I can add an arrow to a tooltip pointing in any of the four directions
- [ ] I can explain which border colour value creates which arrow direction
- [ ] I completed the glossary card mini-project with positioned, animated, arrowed tooltips
- [ ] I can identify and fix the six common beginner mistakes covered in this lesson

---

## Lesson Summary

In this lesson, you learned how to create fully functional, visually polished CSS tooltips — without a single line of JavaScript.

Here is what you now know:

**Core tooltip technique:** Wrap a trigger element and a tooltip element together in a `position: relative` parent. Set the tooltip to `position: absolute`, `visibility: hidden`, and use `bottom: 125%` (plus horizontal centring) to position it above the trigger. Show it with `.container:hover .tooltip { visibility: visible; }`.

**Four positions:** Change between `bottom: 125%` (top), `top: 125%` (bottom), `right: 105%` (left), and `left: 105%` (right) to place tooltips in any direction.

**Fade animation:** Add `opacity: 0` and `transition: opacity 0.3s` to the default tooltip, then set `opacity: 1` on hover for smooth appearance.

**Arrows via border tricks:** Use the `::after` pseudo-element with `content: ""`, zero width/height, and a combination of transparent and coloured borders to create a pure CSS triangle arrow. The direction of the arrow is controlled by which border receives the coloured value (top, right, bottom, or left), following the pattern: the coloured border is the side opposite the direction you want the arrow to point.

**In professional web development**, CSS tooltips are used everywhere — in dashboards, data tables, form field descriptions, icon labels, navigation menus, pricing cards, and accessibility helpers. Mastering them makes your interfaces dramatically more usable and polished.

---

*End of Lesson 57 — CSS Tooltips and Tooltip Arrows*
