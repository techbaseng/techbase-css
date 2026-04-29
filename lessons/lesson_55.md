---
render_with_liquid: false
title: "CSS Transitions — Making Elements Move Smoothly"
nav_order: 55
---

# Lesson 55 — CSS Transitions: Making Elements Move Smoothly

---

## Lesson Introduction

Have you ever visited a website where a button gently changed colour when you hovered over it, or a menu item smoothly grew bigger as your mouse approached it? Those smooth, flowing effects are called **CSS Transitions**. They make websites feel alive, polished, and professional.

Without transitions, style changes happen **instantly** — like a light switch that flips on and off with no dimming. With transitions, those same style changes happen **gradually over time** — like a dimmer switch that slowly brightens the room.

In this lesson, you will learn:
- What a CSS transition is and why it exists
- The four key transition properties and how to use them
- How to control the **speed curve** (how fast or slow different parts of the transition move)
- How to add a **delay** before a transition starts
- How to apply transitions to **multiple properties** at once
- How to combine transitions with **CSS transforms** for dramatic effects
- How to write transitions using the shorthand `transition` property

By the end, you will build a fully working interactive card component that uses everything you have learned.

> **Who is this lesson for?** Complete beginners who know basic HTML and CSS (selectors, properties, values, `:hover`). No JavaScript knowledge is needed.

---

## Prerequisite Concepts

Before diving into transitions, let us make sure two foundational ideas are crystal clear.

### What is a CSS Property?

A **CSS property** is an instruction that tells the browser how an element should look. For example:

- `width` — how wide an element is
- `background-color` — what colour fills the background
- `transform` — whether the element is rotated, scaled, or moved

### What is `:hover`?

`:hover` is a **pseudo-class** — a special CSS selector that only applies styles when the user's mouse pointer is sitting on top of an element.

```css
/* This rule ONLY applies when the mouse is over the button */
button:hover {
  background-color: blue;
}
```

Without a transition, clicking on or hovering over an element changes its style **immediately**. With a transition, that change happens **smoothly** over a set duration of time.

> **Think of it this way:** Imagine two rooms, Room A (normal state) and Room B (hover state). Without a transition you teleport between them. With a transition, you walk through a connecting hallway — and you can control how long that hallway is, and whether you run or stroll through it.

---

## Section 1 — What Are CSS Transitions?

### What Is a Transition?

A **CSS transition** lets you change a CSS property's value smoothly over a period of time, instead of the change happening instantly.

**Without a transition:**

```
Mouse hovers → colour changes INSTANTLY from red to blue
```

**With a transition:**

```
Mouse hovers → colour SLOWLY fades from red to blue over 2 seconds
```

### Why Do Transitions Exist?

Instant style changes can feel jarring and unprofessional. Smooth transitions:
- Make websites feel polished and trustworthy
- Give users visual feedback that something is responding to their actions
- Improve the overall experience of buttons, menus, cards, and form elements
- Are used in every professional website and web application you have ever visited

### Real-World Uses of CSS Transitions

| Where You See It | What Transitions | Effect |
|---|---|---|
| Navigation menus | `background-color`, `color` | Smooth colour change on hover |
| Buttons | `transform`, `background-color` | Gently grows or changes colour |
| Cards (product listings) | `box-shadow`, `transform` | Lifts up with a shadow on hover |
| Image galleries | `opacity` | Fades in overlay text |
| Form inputs | `border-color`, `box-shadow` | Glows blue when clicked |
| Dropdown menus | `height`, `opacity` | Smoothly slides open |

---

## Section 2 — The Four Transition Properties

CSS transitions are made up of four individual properties. You can write them separately or combine them using the shorthand `transition` property.

Here is a map of all four:

```
transition-property        → WHICH CSS property to animate
transition-duration        → HOW LONG the animation takes
transition-timing-function → HOW FAST different parts of the animation move
transition-delay           → HOW LONG to WAIT before starting
```

Let us learn each one in detail.

---

## Section 3 — `transition-property`

### What Is It?

`transition-property` tells the browser **which CSS property** should be animated (smoothly changed).

### Why Does It Exist?

Without specifying a property, the browser would not know what to animate. You might have 20 different CSS properties on an element — you usually only want one or two of them to animate.

### Syntax

```css
transition-property: width;          /* animate only width */
transition-property: background-color; /* animate only background-color */
transition-property: all;             /* animate ALL properties */
```

### Simple Example

```css
div {
  width: 100px;
  height: 100px;
  background-color: red;
  transition-property: width;   /* only animate the width */
  transition-duration: 2s;      /* over 2 seconds */
}

div:hover {
  width: 300px;   /* this is the new value that will animate */
}
```

**What happens:** When you hover over the `div`, its width slowly grows from 100px to 300px over 2 seconds. When the mouse leaves, it slowly shrinks back to 100px.

> **Thinking prompt:** What would happen if you changed `transition-property: width` to `transition-property: background-color` but still only changed the width on hover?

**Answer:** The width would still change, but it would change **instantly** because `background-color` is the animated property, not `width`.

---

## Section 4 — `transition-duration`

### What Is It?

`transition-duration` tells the browser **how long** the animation should take to complete.

### Why Does It Exist?

Without a duration, the transition would happen in 0 seconds (instantly), which defeats the purpose. You must always provide a duration.

### Syntax

```css
transition-duration: 2s;      /* 2 seconds */
transition-duration: 500ms;   /* 500 milliseconds = 0.5 seconds */
transition-duration: 0.3s;    /* 0.3 seconds = 300 milliseconds */
```

- `s` means **seconds**
- `ms` means **milliseconds** (1000 ms = 1 second)

### Simple Example

```css
div {
  width: 100px;
  height: 100px;
  background-color: tomato;
  transition-property: width;
  transition-duration: 2s;    /* takes 2 seconds to complete */
}

div:hover {
  width: 300px;
}
```

**Expected behaviour:** Width grows from 100px → 300px over exactly 2 seconds.

### Second Example (Faster)

```css
div {
  width: 100px;
  background-color: steelblue;
  transition-property: width;
  transition-duration: 0.5s;   /* only half a second — much faster! */
}

div:hover {
  width: 300px;
}
```

**Expected behaviour:** Width grows from 100px → 300px very quickly, in just 0.5 seconds.

> **Thinking prompt:** What happens if you set `transition-duration: 0s`? Try it and see!

---

## Section 5 — The `transition` Shorthand Property

Instead of writing all four properties separately, you can use the **shorthand** `transition` property to write them all in one line.

### Shorthand Syntax

```css
transition: [property] [duration] [timing-function] [delay];
```

### Example — Shorthand for Width Transition

```css
/* Long way (separate properties): */
div {
  transition-property: width;
  transition-duration: 2s;
  transition-timing-function: linear;
  transition-delay: 1s;
}

/* Short way (shorthand): */
div {
  transition: width 2s linear 1s;
}
```

Both of these do exactly the same thing. The shorthand is preferred in real projects because it is shorter and easier to read.

### Minimal Shorthand (Most Common Use)

The timing function and delay are optional in the shorthand. The two required pieces are the **property** and the **duration**:

```css
div {
  transition: width 2s;   /* property + duration — minimum required */
}
```

---

## Section 6 — The Foundational Example (Putting It Together)

Now let us write a complete, working example with HTML and CSS.

### Complete Code

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Step 1: Style the element in its NORMAL state */
    div {
      width: 100px;
      height: 100px;
      background-color: red;
      transition: width 2s;   /* animate the width over 2 seconds */
    }

    /* Step 2: Define what it looks like in the HOVER state */
    div:hover {
      width: 300px;   /* the NEW value that will be animated to */
    }
  </style>
</head>
<body>

  <div>Hover me!</div>

</body>
</html>
```

### Line-by-Line Explanation

| Line | What It Does |
|---|---|
| `width: 100px;` | The div starts at 100 pixels wide |
| `height: 100px;` | The div is 100 pixels tall |
| `background-color: red;` | The div is red |
| `transition: width 2s;` | When the `width` value changes, animate that change over 2 seconds |
| `div:hover { width: 300px; }` | When the mouse hovers over the div, change the width to 300px |

**What the user sees:** A red square. As they hover over it, it slowly expands to the right until it is 300px wide. When they move the mouse away, it slowly shrinks back to 100px.

> **Key insight:** The transition is defined on the **original state** (the `div` rule), NOT on the `:hover` rule. This is how CSS transitions work — you define the animation behaviour on the element, and then the `:hover` (or other trigger) provides the new values to animate toward.

---

## Section 7 — Transitioning Multiple Properties

You can animate several properties at once by separating them with **commas** in the `transition` property. Each property can have its own duration.

### Syntax

```css
transition: property1 duration1, property2 duration2, property3 duration3;
```

### Example — Width, Height, and Background Colour

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      width: 100px;
      height: 100px;
      background-color: red;
      /* Three properties, each with their own duration */
      transition: width 2s, height 4s, background-color 3s;
    }

    div:hover {
      width: 300px;           /* animates over 2 seconds */
      height: 300px;          /* animates over 4 seconds */
      background-color: blue; /* animates over 3 seconds */
    }
  </style>
</head>
<body>

  <div>Hover me!</div>

</body>
</html>
```

### What You Will See

When you hover over the div:
- **Width** grows from 100px → 300px (completes in 2 seconds — fastest)
- **Background colour** fades from red → blue (completes in 3 seconds — medium)
- **Height** grows from 100px → 300px (completes in 4 seconds — slowest)

All three are happening at the same time, but at different speeds!

> **Real-world use case:** Product cards on an e-commerce website often transition their `box-shadow` (to look elevated) and their `transform` (to zoom slightly) at different rates for a dramatic but natural effect.

---

## Section 8 — `transition-timing-function` (The Speed Curve)

### What Is It?

The `transition-timing-function` property controls **how the speed of the transition changes over time**. Does it start slow and speed up? Start fast and slow down? Stay the same speed throughout?

### Why Does It Exist?

Real-world objects rarely move at a perfectly constant speed. A ball thrown into the air slows down as it rises and speeds up as it falls. A drawer you pull open slows down at the end. CSS timing functions let you mimic these natural movement patterns, making animations feel more realistic and satisfying.

### The Six Timing Function Values

| Value | What It Does | Analogy |
|---|---|---|
| `ease` | Starts slow, gets fast in the middle, ends slow | **(Default)** Like a car accelerating then braking |
| `linear` | Same speed the entire time | A conveyor belt at a factory |
| `ease-in` | Starts slow, then speeds up | A rocket launching |
| `ease-out` | Starts fast, then slows down | A car coasting to a stop |
| `ease-in-out` | Slow start AND slow end, fast in the middle | A swing on a playground |
| `cubic-bezier(n,n,n,n)` | Your own custom curve | A mathematician's playground |

### Visualising the Difference

Think of each value as a description of a runner's pace across a 100-metre track:

```
linear:      ▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬  (constant pace)
ease:        ▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬       (slow-fast-slow)
ease-in:               ▬▬▬▬▬▬▬▬▬▬▬▬  (starts slow)
ease-out:    ▬▬▬▬▬▬▬▬▬▬▬▬            (ends slow)
ease-in-out:     ▬▬▬▬▬▬▬▬▬▬          (slow both ends)
```

### Simple Example — Comparing Timing Functions

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .box {
      width: 100px;
      height: 50px;
      background-color: steelblue;
      color: white;
      text-align: center;
      line-height: 50px;
      margin: 10px 0;
    }

    /* Each box has a DIFFERENT timing function */
    #box1 { transition: width 3s linear; }
    #box2 { transition: width 3s ease; }
    #box3 { transition: width 3s ease-in; }
    #box4 { transition: width 3s ease-out; }
    #box5 { transition: width 3s ease-in-out; }

    /* All boxes get wider on hover */
    .box:hover {
      width: 400px;
    }
  </style>
</head>
<body>

  <div class="box" id="box1">linear</div>
  <div class="box" id="box2">ease (default)</div>
  <div class="box" id="box3">ease-in</div>
  <div class="box" id="box4">ease-out</div>
  <div class="box" id="box5">ease-in-out</div>

</body>
</html>
```

**What you will see:** All five boxes grow from 100px to 400px when hovered, but they all move at different rhythms. Hover over each one slowly and notice how the animation feels different.

> **Thinking prompt:** Which timing function feels most natural to you? Most designers prefer `ease` or `ease-in-out` for UI elements because they feel more natural than `linear`.

---

## Section 9 — `cubic-bezier()` — Custom Timing

### What Is It?

`cubic-bezier()` lets you create a completely custom speed curve by providing four numbers. It is named after a mathematical concept called a Bézier curve.

### Syntax

```css
transition-timing-function: cubic-bezier(x1, y1, x2, y2);
```

The four numbers are control points that define the shape of the speed curve. Values between 0 and 1 represent typical transitions, but you can go beyond 1 for bouncing effects.

### Example — Custom Cubic Bezier

```css
div {
  width: 100px;
  transition: width 2s cubic-bezier(0.25, 0.1, 0.25, 1.0);
}
```

The pre-defined values `ease`, `linear`, `ease-in`, `ease-out`, and `ease-in-out` are actually shortcuts for specific `cubic-bezier()` values:

| Keyword | Equivalent `cubic-bezier()` |
|---|---|
| `ease` | `cubic-bezier(0.25, 0.1, 0.25, 1.0)` |
| `linear` | `cubic-bezier(0.0, 0.0, 1.0, 1.0)` |
| `ease-in` | `cubic-bezier(0.42, 0, 1.0, 1.0)` |
| `ease-out` | `cubic-bezier(0, 0, 0.58, 1.0)` |
| `ease-in-out` | `cubic-bezier(0.42, 0, 0.58, 1.0)` |

> **Tip for beginners:** You do not need to memorise `cubic-bezier` values. There are free online tools like **cubic-bezier.com** that let you drag points on a graph and generate the numbers for you automatically.

---

## Section 10 — `transition-delay`

### What Is It?

`transition-delay` specifies **how long to wait before the transition starts**. The element will not begin moving until this delay has passed.

### Why Does It Exist?

Sometimes you want one thing to happen, then after a short pause, another thing happens. For example, in a cascading menu, you might want each item to start its entrance animation slightly after the previous one.

### Syntax

```css
transition-delay: 1s;     /* wait 1 second before starting */
transition-delay: 500ms;  /* wait half a second */
transition-delay: 0s;     /* no delay (default) */
```

### Simple Example — 1-Second Delay

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      width: 100px;
      height: 100px;
      background-color: coral;
      /* Animate width over 2 seconds, but wait 1 second before starting */
      transition: width 2s 1s;
      /* shorthand format: property  duration  delay */
    }

    div:hover {
      width: 300px;
    }
  </style>
</head>
<body>

  <p>Hover over the box below. Notice the 1-second pause before it starts moving.</p>
  <div></div>

</body>
</html>
```

**What you will see:** You hover → one second passes with nothing happening → then the box slowly expands over 2 seconds.

### Second Example — No Delay vs With Delay

```css
/* Box 1: starts immediately */
#instant {
  transition: width 2s;           /* no delay */
}

/* Box 2: waits 2 seconds first */
#delayed {
  transition: width 2s 2s;       /* 2s duration, 2s delay */
}
```

> **Real-world use:** Delays are used in dropdown menus so they don't snap open and closed too quickly when the mouse accidentally passes over them. A small delay (e.g., `0.1s` to `0.3s`) prevents the menu from flashing.

---

## Section 11 — Combining Transition and Transform

CSS Transitions work beautifully with **CSS Transforms**. A transform is an operation that moves (`translate`), rotates (`rotate`), or scales (`scale`) an element without affecting the normal page layout.

> **Prerequisite note:** If you have not studied CSS Transforms yet, here is a brief explanation. `transform: scale(1.2)` makes an element 20% bigger. `transform: rotate(45deg)` rotates it 45 degrees. `transform: translateX(50px)` moves it 50 pixels to the right.

### Example 1 — Transition + Transform on a `<div>`

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      width: 100px;
      height: 100px;
      background-color: mediumseagreen;
      /* Animate multiple properties including transform */
      transition: width 2s, height 2s, background-color 2s, transform 2s;
    }

    div:hover {
      width: 200px;
      height: 200px;
      background-color: darkslateblue;
      transform: rotate(180deg);   /* also rotates as it grows! */
    }
  </style>
</head>
<body>

  <div></div>

</body>
</html>
```

**What you will see:** A green square. When hovered, it smoothly grows bigger, turns dark purple, AND rotates 180 degrees — all at the same time!

### Example 2 — Transition + Transform on a Button

This is one of the most common real-world uses: a button that slightly lifts up when hovered.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    button {
      padding: 15px 30px;
      font-size: 16px;
      background-color: royalblue;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      /* Animate colour AND transform */
      transition: background-color 1s ease-out, transform 1s ease-out;
    }

    button:hover {
      background-color: darkblue;     /* darker colour */
      transform: scale(1.1);          /* 10% bigger */
    }
  </style>
</head>
<body>

  <button>Hover Over Me</button>

</body>
</html>
```

**What you will see:** A blue button. When hovered, it slowly gets darker AND gently grows 10% larger. This gives the impression that the button is "lifting" towards the user — a classic hover effect seen on countless websites.

> **Why is `ease-out` used here?** A button hover should feel like something responding to your action. `ease-out` (starts fast, slows down) feels more responsive and natural than `linear` or `ease-in`, because the initial movement is quick (feels reactive) and the settling is gentle (feels smooth).

---

## Section 12 — The Longhand vs Shorthand Methods

You have learned two ways to write transitions. Here they are side by side:

### Longhand (Separate Properties)

```css
div {
  transition-property: width;
  transition-duration: 2s;
  transition-timing-function: linear;
  transition-delay: 1s;
}
```

### Shorthand (One Line)

```css
div {
  transition: width 2s linear 1s;
}
```

### Order in the Shorthand

The shorthand follows this order:

```
transition: [property] [duration] [timing-function] [delay];
```

- `property` — which CSS property to animate (required)
- `duration` — how long (required)
- `timing-function` — the speed curve (optional, defaults to `ease`)
- `delay` — how long to wait before starting (optional, defaults to `0s`)

### Multiple Properties in Shorthand

```css
div {
  transition: width 2s linear 1s, background-color 3s ease 0s;
}
```

This animates `width` (linear, 2s, 1s delay) and `background-color` (ease, 3s, no delay) separately.

---

## Section 13 — Complete Properties Reference Table

| Property | Values | Description |
|---|---|---|
| `transition` | `property duration timing-function delay` | Shorthand for all four properties |
| `transition-property` | `none`, `all`, or a specific property name like `width` | Which CSS property to animate |
| `transition-duration` | `2s`, `500ms`, etc. | How long the transition takes |
| `transition-timing-function` | `ease`, `linear`, `ease-in`, `ease-out`, `ease-in-out`, `cubic-bezier()` | The speed curve |
| `transition-delay` | `1s`, `200ms`, etc. | How long to wait before starting |

---

## Guided Practice Exercises

### Exercise 1 — Your First Transition (Warm-Up)

**Objective:** Make a `div` change its background colour when hovered, with a smooth 2-second transition.

**Scenario:** You are building a card for a website. When a user hovers over a card, its background should smoothly change from light grey to soft blue.

**Steps:**
1. Create a `div` that is 200px wide and 150px tall
2. Give it a background colour of `lightgrey`
3. Add a `transition` on `background-color` for 2 seconds
4. On `:hover`, change the background colour to `cornflowerblue`

**Expected Output:**
```
Normal state:  ┌─────────────────────┐
               │     Light grey box  │
               └─────────────────────┘

Hover state:   ┌─────────────────────┐
               │   Cornflower blue   │
               └─────────────────────┘
               (changes smoothly over 2 seconds)
```

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .card {
      width: 200px;
      height: 150px;
      background-color: lightgrey;
      transition: background-color 2s;
    }

    .card:hover {
      background-color: cornflowerblue;
    }
  </style>
</head>
<body>
  <div class="card"></div>
</body>
</html>
```

**Self-check Questions:**
- Does the colour change gradually, or instantly?
- What happens when you move the mouse OFF the card?
- What would happen if you removed the `transition` line?

---

### Exercise 2 — Multiple Properties

**Objective:** Transition width, height, and background colour simultaneously, each with a different duration.

**Scenario:** You are building an interactive banner. On hover, it should grow wider (fast), grow taller (medium), and change colour (slow).

**Steps:**
1. Create a `div` that is 150px wide, 80px tall, with background colour `tomato`
2. Add transitions: `width 1s`, `height 2s`, `background-color 3s`
3. On hover: set width to 350px, height to 200px, background to `teal`

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .banner {
      width: 150px;
      height: 80px;
      background-color: tomato;
      transition: width 1s, height 2s, background-color 3s;
    }

    .banner:hover {
      width: 350px;
      height: 200px;
      background-color: teal;
    }
  </style>
</head>
<body>
  <div class="banner"></div>
</body>
</html>
```

**Self-check Questions:**
- Which property finishes changing first?
- Which takes the longest?
- What if you made all three durations the same? How would it look different?

---

### Exercise 3 — Comparing Timing Functions

**Objective:** Create five identical boxes and apply a different timing function to each, so you can visually compare how they feel.

**Steps:**
1. Create five `div` elements with the class `box`
2. Style them: 100px wide, 60px tall, coloured boxes in a column
3. On hover, change each width to 400px
4. Apply `linear`, `ease`, `ease-in`, `ease-out`, and `ease-in-out` to each respectively

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .box {
      width: 100px;
      height: 60px;
      color: white;
      font-family: sans-serif;
      font-size: 14px;
      display: flex;
      align-items: center;
      padding-left: 10px;
      margin-bottom: 8px;
      background-color: steelblue;
    }

    #b1 { transition: width 3s linear; }
    #b2 { transition: width 3s ease; }
    #b3 { transition: width 3s ease-in; }
    #b4 { transition: width 3s ease-out; }
    #b5 { transition: width 3s ease-in-out; }

    .box:hover {
      width: 400px;
    }
  </style>
</head>
<body>
  <div class="box" id="b1">linear</div>
  <div class="box" id="b2">ease</div>
  <div class="box" id="b3">ease-in</div>
  <div class="box" id="b4">ease-out</div>
  <div class="box" id="b5">ease-in-out</div>
</body>
</html>
```

**Self-check Questions:**
- Which timing function feels most natural when you hover?
- Which feels most mechanical?
- For a button that users click, which would you choose and why?

---

### Exercise 4 — Adding a Delay

**Objective:** Create a tooltip-like effect using `transition-delay`, where a colour change only begins after a 1-second pause.

**Steps:**
1. Create a box with background `lightcoral`
2. On hover, change background to `darkgreen`
3. Make the transition duration 2 seconds
4. Add a delay of 1 second before the transition starts

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .delayed-box {
      width: 200px;
      height: 100px;
      background-color: lightcoral;
      /* duration 2s, delay 1s */
      transition: background-color 2s 1s;
    }

    .delayed-box:hover {
      background-color: darkgreen;
    }
  </style>
</head>
<body>
  <p>Hover over the box and notice the delay before the colour changes.</p>
  <div class="delayed-box"></div>
</body>
</html>
```

**Self-check Questions:**
- How long does the user wait before anything happens?
- What is the total time from hover start to transition complete?
- Try setting the delay to `3s` — how does the experience change?

---

## Mini Project — Interactive Profile Card

Now let us combine everything into a realistic project: an interactive profile card like you might see on a team page of a company website.

### Project Overview

We will build a card that:
- Shows a name, job title, and a coloured background
- On hover: the card lifts up slightly (transform), the background darkens slightly, and a border appears (multiple transitions)
- Each transition uses an appropriate timing function and duration

### Stage 1 — Setup and Basic Card

**Preview:**

```
┌──────────────────────────────────┐
│                                  │
│            Ada Lovelace          │
│         Software Engineer        │
│                                  │
└──────────────────────────────────┘
```

**Code:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: sans-serif;
      display: flex;
      justify-content: center;
      padding-top: 60px;
      background-color: #f0f4f8;
    }

    .profile-card {
      width: 250px;
      padding: 30px;
      background-color: #4a90d9;
      color: white;
      text-align: center;
      border-radius: 12px;
    }

    .profile-card h2 {
      margin: 0 0 10px 0;
      font-size: 22px;
    }

    .profile-card p {
      margin: 0;
      font-size: 14px;
      opacity: 0.9;
    }
  </style>
</head>
<body>
  <div class="profile-card">
    <h2>Ada Lovelace</h2>
    <p>Software Engineer</p>
  </div>
</body>
</html>
```

**Milestone output:** A centred blue card with white text showing a name and job title. No hover effect yet.

---

### Stage 2 — Adding Transitions

Now we add the hover effects with transitions:

```css
.profile-card {
  width: 250px;
  padding: 30px;
  background-color: #4a90d9;
  color: white;
  text-align: center;
  border-radius: 12px;

  /* ADD THESE TRANSITIONS */
  transition:
    transform 0.3s ease-out,
    background-color 0.4s ease,
    box-shadow 0.3s ease-out;
}

.profile-card:hover {
  transform: translateY(-8px);          /* move up 8 pixels */
  background-color: #2c6fad;           /* darker blue */
  box-shadow: 0 12px 24px rgba(0,0,0,0.2); /* shadow appears below */
}
```

**What each transition does:**
- `transform 0.3s ease-out` — Card lifts up quickly, then settles gently
- `background-color 0.4s ease` — Background darkens with a natural rhythm
- `box-shadow 0.3s ease-out` — Shadow appears quickly, matching the card's upward movement

---

### Stage 3 — Complete Final Code

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      display: flex;
      justify-content: center;
      gap: 30px;
      padding-top: 60px;
      background-color: #f0f4f8;
    }

    .profile-card {
      width: 220px;
      padding: 30px 20px;
      background-color: #4a90d9;
      color: white;
      text-align: center;
      border-radius: 12px;
      cursor: pointer;

      /* All transitions defined here */
      transition:
        transform 0.3s ease-out,
        background-color 0.4s ease,
        box-shadow 0.3s ease-out;
    }

    .profile-card:hover {
      transform: translateY(-10px);
      background-color: #2c6fad;
      box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25);
    }

    .profile-card .avatar {
      width: 70px;
      height: 70px;
      border-radius: 50%;
      background-color: rgba(255,255,255,0.3);
      margin: 0 auto 15px auto;
      font-size: 30px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .profile-card h2 {
      margin: 0 0 6px 0;
      font-size: 18px;
    }

    .profile-card p {
      margin: 0;
      font-size: 13px;
      opacity: 0.85;
    }
  </style>
</head>
<body>

  <!-- Card 1 -->
  <div class="profile-card">
    <div class="avatar">👩‍💻</div>
    <h2>Ada Lovelace</h2>
    <p>Software Engineer</p>
  </div>

  <!-- Card 2 -->
  <div class="profile-card" style="background-color: #e06c47; transition: transform 0.3s ease-out, background-color 0.4s ease, box-shadow 0.3s ease-out;">
    <div class="avatar">👨‍🔬</div>
    <h2>Alan Turing</h2>
    <p>AI Researcher</p>
  </div>

  <!-- Card 3 -->
  <div class="profile-card" style="background-color: #4ab87a; transition: transform 0.3s ease-out, background-color 0.4s ease, box-shadow 0.3s ease-out;">
    <div class="avatar">👩‍🎨</div>
    <h2>Grace Hopper</h2>
    <p>UX Designer</p>
  </div>

</body>
</html>
```

**Milestone output:** Three team cards side by side. When you hover any card, it smoothly lifts upwards, darkens slightly, and gains a drop shadow — a polished, professional effect.

**Reflection Questions:**
- Try changing `ease-out` to `linear` on the transform. How does the card's movement feel different?
- What happens if you increase the delay from `0s` to `0.5s`?
- Can you add another property to transition, like `border-radius`?

**Optional Advanced Extensions:**
- Add a fourth transition to animate the `color` of the text from white to light yellow on hover
- Add a `transition-delay` of `0.1s` to the `box-shadow` so the shadow appears just slightly after the card starts lifting
- Try using `cubic-bezier(0.34, 1.56, 0.64, 1)` for the transform to create a subtle "bounce" as the card lifts

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting `transition-duration`

```css
/* WRONG — no duration means the transition happens instantly */
div {
  transition-property: width;
  /* missing transition-duration! */
}

/* CORRECT */
div {
  transition: width 2s;
}
```

**Rule:** The `transition-duration` is required. Without it, the default is `0s`, which means no animation.

---

### Mistake 2 — Putting the Transition on the `:hover` Rule Instead of the Base Rule

```css
/* WRONG — transition is on :hover, so it only applies on the way IN */
div { width: 100px; }
div:hover {
  width: 300px;
  transition: width 2s;  /* ← WRONG position */
}

/* CORRECT — transition is on the base element */
div {
  width: 100px;
  transition: width 2s;  /* ← CORRECT position */
}
div:hover {
  width: 300px;
}
```

**Why it matters:** If you put `transition` only on `:hover`, the animation plays when you hover IN, but the change back to the original state happens instantly when you hover OUT. Placing the transition on the base rule makes it smooth in both directions.

---

### Mistake 3 — Trying to Transition a Non-Animatable Property

Not all CSS properties can be transitioned. For example, `display` cannot be transitioned.

```css
/* This WON'T animate — display cannot be transitioned */
div {
  display: block;
  transition: display 1s;
}
div:hover {
  display: none;
}

/* Instead, use opacity or height */
div {
  opacity: 1;
  transition: opacity 1s;
}
div:hover {
  opacity: 0;
}
```

**Animatable properties include:** `width`, `height`, `color`, `background-color`, `opacity`, `transform`, `border-radius`, `box-shadow`, `padding`, `margin`, `font-size`, and many more.

---

### Mistake 4 — Forgetting the Unit on Duration

```css
/* WRONG — missing 's' for seconds */
div {
  transition: width 2;   /* ← WRONG — '2' is not a valid value */
}

/* CORRECT */
div {
  transition: width 2s;  /* or 2000ms */
}
```

---

### Mistake 5 — Using `transition: all` Without Care

```css
/* This might cause performance issues on complex pages */
div {
  transition: all 0.5s;
}
```

`transition: all` animates every CSS property. This can cause unexpected behaviour and slow down your page. It is better to name the specific properties you want to animate.

---

## Reflection Questions

Think about these questions after completing the lesson:

1. **Why** would you use a transition delay on a navigation menu hover effect?
2. In what way is `ease-out` better than `linear` for a button hover effect? What feeling does each one create?
3. If you put `transition: all 1s` on an element, what happens when ANY of its CSS properties change?
4. Why is it important to put the `transition` property on the **base state** of an element rather than on the `:hover` state?
5. Can you think of three real websites where you have noticed smooth CSS transitions? What was being transitioned?
6. What is the difference between a CSS **transition** and a CSS **animation**? (Hint: transitions are triggered by state changes; animations can run automatically.)

---

## Completion Checklist

Go through this checklist to confirm you have mastered this lesson:

- [ ] I understand what a CSS transition is and why it is used
- [ ] I can write a `transition` using the shorthand property
- [ ] I know the four sub-properties: `transition-property`, `transition-duration`, `transition-timing-function`, `transition-delay`
- [ ] I know the six timing function keywords: `ease`, `linear`, `ease-in`, `ease-out`, `ease-in-out`, `cubic-bezier()`
- [ ] I can add transitions to multiple properties at once using commas
- [ ] I understand what `transition-delay` does and when to use it
- [ ] I can combine transitions with CSS transforms (`scale`, `translateY`, etc.)
- [ ] I know that `transition` belongs on the **base element rule**, not on `:hover`
- [ ] I have completed all four guided exercises
- [ ] I have completed the mini project (interactive profile cards)
- [ ] I know which CSS properties can and cannot be transitioned

---

## Lesson Summary

CSS Transitions allow you to smoothly animate the change between two states of a CSS property. Instead of an instant jump from one value to another, the browser gradually animates the change over a specified time.

The `transition` shorthand property takes up to four values in this order:

```css
transition: property  duration  timing-function  delay;
/*  e.g.:  width     2s        ease-out         0.5s; */
```

The **timing function** controls the rhythm of the animation. `ease` (the default) feels the most natural for most UI elements. `linear` is perfectly consistent. `ease-in` starts slow, `ease-out` ends slow, and `ease-in-out` does both. `cubic-bezier()` lets you create fully custom curves.

You can animate **multiple properties** at once by separating them with commas, each with their own duration and timing:

```css
transition: width 1s ease, background-color 2s linear, transform 0.5s ease-out;
```

Combining transitions with CSS `transform` properties (like `scale()`, `translateY()`, `rotate()`) creates the polished, professional hover effects seen on modern websites — including the classic "card lift" effect in our mini project.

> **Next lesson:** CSS Animations — where you will learn to create multi-step, automatically repeating animations using `@keyframes`, taking your CSS motion skills even further.
