---
render_with_liquid: false
title: "CSS Animations"
nav_order: 56
---

# Lesson 56: CSS Animations

---

## Lesson Introduction

Welcome to one of the most exciting topics in CSS! In this lesson, you will learn how to bring your web pages to life using **CSS Animations** — a powerful feature that lets elements move, change colour, grow, shrink, fade, and spin right inside your browser, all without writing a single line of JavaScript.

Think about the Shoprite website banner that slides in, or the MTN loading spinner you see before a page loads. Those effects are often built with CSS animations. By the end of this lesson, you will be able to create those kinds of effects yourself.

### What You Will Learn

By the end of this lesson, you will be able to:

- Understand what CSS animations are and how they work
- Write `@keyframes` rules to define animation steps
- Use `animation-name` and `animation-duration` to attach animations to elements
- Control animation delay, repetition, direction, and fill behaviour
- Fine-tune animation speed using timing functions (ease, linear, cubic-bezier, steps)
- Use the `animation` shorthand property confidently
- Use `animation-play-state` to pause and resume animations
- Build a complete animated Nigerian market badge mini-project

---

## Prerequisite Concepts Recap

Before we dive in, make sure you are comfortable with the following ideas from earlier lessons:

- **CSS properties and values** — you write `property: value;` inside a selector block
- **CSS selectors** — how you target HTML elements like `div`, `.box`, `#header`
- **CSS transitions** (Lesson 55) — transitions animate a change between two states triggered by an event like `:hover`. Animations are different: they run automatically and can loop through many stages without needing a trigger.

---

## Section 1 — What Is a CSS Animation?

### Why Does It Exist?

Before CSS animations existed, developers had to use JavaScript or Flash just to make a box slide across a screen. This was slow, complicated, and required extra files. CSS animations solve this problem completely. You can now make any element animate entirely inside your CSS stylesheet.

### What Is It?

A **CSS animation** is a set of instructions that tells the browser how an element should gradually change its appearance over a period of time. The browser handles all the in-between steps automatically — you just define the start and end (or multiple stages along the way).

### Real-World Analogy

Think of a Nollywood film scene: the director gives the actor instructions — *"Start at the door, walk to the table, pick up the cup, sit down."* The actor fills in all the movements between those instructions. CSS animations work the same way: you give the keyframe instructions, and the browser fills in every tiny step in between.

### Two Parts of Every CSS Animation

Every CSS animation requires exactly two things:

1. **The `@keyframes` rule** — this is where you define what the animation looks like at each stage
2. **The animation properties** — these are applied to the element you want to animate, telling it which `@keyframes` to use and how long the animation should run

---

## Section 2 — The `@keyframes` Rule

### What Is a Keyframe?

A **keyframe** is a moment in time during an animation. Think of it like chapters in a book — at chapter 1 the element looks one way, at chapter 5 it looks different, at chapter 10 it looks completely different again. The browser smoothly draws all the pages in between.

### Simple `from` and `to` Syntax

The simplest form uses `from` (start) and `to` (end):

```css
@keyframes moveRight {
  from {
    margin-left: 0px;
  }
  to {
    margin-left: 300px;
  }
}
```

**Reading this line by line:**
- `@keyframes` — this keyword tells CSS you are creating a set of animation frames
- `moveRight` — this is the **name** you give your animation (you choose the name)
- `from { ... }` — defines the style at the very start (0% of the animation)
- `to { ... }` — defines the style at the very end (100% of the animation)
- `margin-left: 0px;` — at the start, the element has no left margin
- `margin-left: 300px;` — at the end, the element has shifted 300 pixels to the right

### Colour-Change Example

```css
@keyframes colourFade {
  from { background-color: green; }
  to   { background-color: yellow; }
}
```

**Expected output in browser:** The element smoothly changes its background from green to yellow over the animation duration.

> 💡 **Thinking Prompt:** What do you think will happen if you swap the `from` and `to` values?

---

## Section 3 — `animation-name` and `animation-duration`

### Connecting an Animation to an Element

Writing `@keyframes` alone does nothing visible. You must attach the animation to an HTML element using two properties:

| Property              | What It Does                                             |
|-----------------------|----------------------------------------------------------|
| `animation-name`      | Names the `@keyframes` block to use                      |
| `animation-duration`  | Sets how long one full cycle of the animation takes      |

### Example 1 — Simple Slide

```css
/* Step 1: Define the animation */
@keyframes slideIn {
  from { margin-left: -200px; }
  to   { margin-left: 0px; }
}

/* Step 2: Attach it to an element */
div {
  width: 200px;
  height: 80px;
  background-color: #009900;  /* Nigerian green */
  animation-name: slideIn;
  animation-duration: 2s;
}
```

```html
<div>Welcome to Lagos!</div>
```

**Expected output in browser:** The green box slides in from the left over 2 seconds, settling into its normal position.

> ⚠️ **Important:** If you forget `animation-duration`, the animation will **not run** because its default value is `0s` (zero seconds). Nothing can animate in zero time!

### Example 2 — Colour Change on a Heading

```css
@keyframes nijaColours {
  from { color: green; }
  to   { color: white; }
}

h1 {
  background-color: green;
  animation-name: nijaColours;
  animation-duration: 3s;
}
```

```html
<h1>Naija No Dey Carry Last!</h1>
```

**Expected output in browser:** The heading text smoothly changes from green to white over 3 seconds.

---

## Section 4 — Using Percentage Keyframes

### Why Percentages?

`from` and `to` only give you two stages. What if you need three, four, or ten different stages? You use **percentages**.

- `0%` means the very start (same as `from`)
- `50%` means halfway through
- `100%` means the very end (same as `to`)
- You can add any percentage in between

### Example — Three-Stage Animation

```css
@keyframes trafficLight {
  0%   { background-color: red; }
  50%  { background-color: yellow; }
  100% { background-color: green; }
}

.light {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  animation-name: trafficLight;
  animation-duration: 4s;
}
```

```html
<div class="light"></div>
```

**Expected output in browser:** The circle starts red, transitions to yellow at the halfway point, then becomes green by the end — like a traffic light on Eko Bridge.

### Example — Multi-Stage Text Animation

```css
@keyframes marketCallout {
  0%   { transform: scale(1);    color: black; }
  25%  { transform: scale(1.2);  color: red; }
  50%  { transform: scale(1);    color: black; }
  75%  { transform: scale(0.8);  color: blue; }
  100% { transform: scale(1);    color: black; }
}

.promo {
  font-size: 24px;
  animation-name: marketCallout;
  animation-duration: 2s;
}
```

**Expected output in browser:** The text grows, turns red, shrinks, turns blue, then returns to normal — mimicking an attention-grabbing market advertisement.

> 💡 **Thinking Prompt:** What would happen if you add a keyframe at `30%`? Try inserting one and observe the change.

---

## Section 5 — Animation Delay

### What Is `animation-delay`?

Sometimes you want an animation to wait before it starts. The `animation-delay` property sets how long the browser should wait before beginning the animation.

```css
animation-delay: 2s;
```

This means: *"Wait 2 seconds, then start the animation."*

### Example

```css
@keyframes popIn {
  from { opacity: 0; transform: scale(0); }
  to   { opacity: 1; transform: scale(1); }
}

.badge {
  width: 150px;
  height: 150px;
  background-color: #008000;
  animation-name: popIn;
  animation-duration: 1s;
  animation-delay: 3s;   /* Wait 3 seconds before starting */
}
```

**Expected output in browser:** For the first 3 seconds, the badge is invisible. Then it suddenly pops into full visibility over 1 second.

### Negative Delay Values

You can use a **negative** delay to make an animation appear to have already started:

```css
animation-delay: -1s;
```

This means: *"Act as if the animation already started 1 second ago."* The animation will begin at the 1-second mark instead of the 0-second mark.

---

## Section 6 — Animation Iteration Count

### Making an Animation Repeat

By default, an animation runs only **once** and then stops. To make it repeat, use `animation-iteration-count`.

```css
animation-iteration-count: 3;      /* Runs exactly 3 times */
animation-iteration-count: infinite; /* Runs forever */
```

### Example — Pulsing Button

```css
@keyframes pulse {
  0%   { transform: scale(1); }
  50%  { transform: scale(1.1); }
  100% { transform: scale(1); }
}

.buy-btn {
  padding: 15px 30px;
  background-color: #ff6600;
  color: white;
  border: none;
  animation-name: pulse;
  animation-duration: 0.8s;
  animation-iteration-count: infinite;
}
```

**Expected output in browser:** The button gently pulsates non-stop — a common effect used on "Buy Now" or "Order" buttons on Nigerian e-commerce sites like Jumia.

---

## Section 7 — Animation Direction

### What Is `animation-direction`?

By default, animations always play **forwards** (from start to end). The `animation-direction` property lets you control the direction of playback.

| Value               | What It Does                                                  |
|---------------------|---------------------------------------------------------------|
| `normal`            | Plays forwards (default). Resets and replays from the start  |
| `reverse`           | Plays backwards (from `to` back to `from`)                   |
| `alternate`         | Plays forwards, then backwards on the next iteration         |
| `alternate-reverse` | Plays backwards, then forwards on the next iteration         |

### Example — Bouncing Ball Effect

```css
@keyframes bounce {
  from { margin-top: 0px; }
  to   { margin-top: 150px; }
}

.ball {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background-color: #006400;
  animation-name: bounce;
  animation-duration: 0.5s;
  animation-iteration-count: infinite;
  animation-direction: alternate;  /* Goes down, then back up, forever */
}
```

**Expected output in browser:** The ball moves down 150px, then immediately moves back up, creating a smooth, continuous bouncing effect.

> 💡 **Thinking Prompt:** What would happen if you changed `alternate` to `reverse`? Would the ball still bounce?

---

## Section 8 — Animation Fill Mode

### The Problem Fill Mode Solves

What happens to an element *before* an animation starts or *after* it ends? By default, it snaps back to its original styling. This can look jarring. `animation-fill-mode` solves this.

| Value       | What It Does                                                             |
|-------------|--------------------------------------------------------------------------|
| `none`      | Element returns to original style before and after animation (default)   |
| `forwards`  | Element keeps the style from the **last** keyframe after animation ends  |
| `backwards` | Element gets the style from the **first** keyframe during the delay      |
| `both`      | Applies both `forwards` and `backwards` rules                            |

### Example — Button That Stays Highlighted

```css
@keyframes highlight {
  from { background-color: white; }
  to   { background-color: #ffcc00; }  /* Yellow like suya wrapper */
}

.promo-tag {
  padding: 10px;
  animation-name: highlight;
  animation-duration: 1.5s;
  animation-fill-mode: forwards;  /* Stay yellow after animation ends */
}
```

**Expected output in browser:** The element animates from white to yellow, then permanently remains yellow. Without `forwards`, it would snap back to white.

---

## Section 9 — Animation Play State

### Pausing and Resuming an Animation

The `animation-play-state` property lets you pause or resume an animation:

```css
animation-play-state: running;  /* Default — animation plays */
animation-play-state: paused;   /* Animation is frozen */
```

This is extremely useful combined with `:hover` — pause an animation when the user hovers over an element:

### Example — Pause on Hover

```css
@keyframes spin {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}

.spinner {
  width: 80px;
  height: 80px;
  background-color: green;
  animation-name: spin;
  animation-duration: 2s;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
}

.spinner:hover {
  animation-play-state: paused;  /* Freeze the spin on hover */
}
```

**Expected output in browser:** The green square rotates continuously. When you hover your mouse over it, it freezes. When you move your mouse away, it continues spinning.

---

## Section 10 — Animation Timing Functions

### Why Does Timing Matter?

Imagine throwing a ball. It doesn't move at a constant speed — it starts slow, speeds up, and slows down again as it lands. CSS timing functions let you control this **acceleration pattern** of your animations, making them feel natural or mechanical.

### The `animation-timing-function` Property

This property controls the speed curve of an animation **within each keyframe interval**.

| Value                        | What It Does                                                      |
|------------------------------|-------------------------------------------------------------------|
| `ease`                       | Starts slow, speeds up, slows down at end (default)               |
| `linear`                     | Same speed throughout — mechanical, like a conveyor belt          |
| `ease-in`                    | Starts slow, then speeds up — like a car accelerating             |
| `ease-out`                   | Starts fast, then slows down — like a car braking                 |
| `ease-in-out`                | Starts slow, speeds up in the middle, slows at end                |
| `cubic-bezier(n,n,n,n)`      | Fully custom speed curve — advanced                               |
| `steps(n, start\|end)`       | Jumps in fixed steps — good for sprite animations                 |

### Example — Comparing Timing Functions

```html
<div class="box linear">linear</div>
<div class="box ease">ease</div>
<div class="box ease-in">ease-in</div>
<div class="box ease-out">ease-out</div>
```

```css
@keyframes slideAcross {
  from { transform: translateX(0); }
  to   { transform: translateX(400px); }
}

.box {
  width: 100px;
  height: 40px;
  background-color: green;
  color: white;
  text-align: center;
  line-height: 40px;
  margin: 10px 0;
  animation-name: slideAcross;
  animation-duration: 3s;
  animation-fill-mode: forwards;
}

.linear   { animation-timing-function: linear; }
.ease     { animation-timing-function: ease; }
.ease-in  { animation-timing-function: ease-in; }
.ease-out { animation-timing-function: ease-out; }
```

**Expected output in browser:** All four boxes slide to the right over 3 seconds. The `linear` box moves at the same speed the whole way. The `ease` box starts and ends slowly. The `ease-in` box starts slow. The `ease-out` box ends slowly. Watch carefully — you can feel the difference!

### The `cubic-bezier()` Function

This gives you full control over the timing curve. It takes four numbers between 0 and 1 that define two control points of a Bézier curve.

```css
animation-timing-function: cubic-bezier(0.25, 0.1, 0.25, 1.0);
/* This is exactly equivalent to 'ease' */
```

Some useful custom curves:

```css
/* Very fast start, dramatic slowdown */
animation-timing-function: cubic-bezier(0.9, 0.1, 1.0, 0.1);

/* Smooth bounce-like effect */
animation-timing-function: cubic-bezier(0.34, 1.56, 0.64, 1);
```

### The `steps()` Function

Instead of a smooth curve, `steps()` makes the animation **jump** in discrete steps — like a flip-book animation.

```css
animation-timing-function: steps(4);  /* Jump in 4 equal steps */
```

```css
@keyframes blink {
  from { opacity: 1; }
  to   { opacity: 0; }
}

.cursor {
  animation-name: blink;
  animation-duration: 1s;
  animation-timing-function: steps(1);  /* One abrupt jump */
  animation-iteration-count: infinite;
}
```

**Expected output in browser:** The element blinks on and off sharply — like a text cursor in a terminal.

### Setting Timing Per Keyframe

You can also set different timing functions inside each keyframe:

```css
@keyframes multiTiming {
  0%   { 
    transform: translateX(0); 
    animation-timing-function: ease-in;    /* Start this segment slowly */
  }
  50%  { 
    transform: translateX(200px); 
    animation-timing-function: ease-out;   /* End this segment slowly */
  }
  100% { transform: translateX(0); }
}
```

---

## Section 11 — The `animation` Shorthand Property

### Why Use Shorthand?

Writing all animation properties separately can be verbose. CSS gives you a single `animation` shorthand property that combines everything into one line.

### Syntax

```css
animation: name duration timing-function delay iteration-count direction fill-mode play-state;
```

### Full Example

```css
/* Long form */
.box {
  animation-name: slideIn;
  animation-duration: 2s;
  animation-timing-function: ease-in-out;
  animation-delay: 0.5s;
  animation-iteration-count: 3;
  animation-direction: alternate;
  animation-fill-mode: forwards;
  animation-play-state: running;
}

/* Shorthand — exactly equivalent */
.box {
  animation: slideIn 2s ease-in-out 0.5s 3 alternate forwards running;
}
```

> ⚠️ **Order matters!** In the shorthand, the browser distinguishes `duration` from `delay` purely by position — `duration` must come before `delay`.

### Minimum Required Values

You must always supply at least `animation-name` and `animation-duration`:

```css
animation: fadeIn 1s;
```

Everything else uses its default value.

### Multiple Animations on One Element

You can attach multiple animations to the same element by separating them with commas:

```css
.element {
  animation:
    slideIn  1s ease 0s 1,
    colourFade 2s linear 1s infinite;
}
```

**Expected output in browser:** The element first slides in (once), then immediately begins cycling through colour changes (forever) starting one second later.

---

## Section 12 — Complete Reference: All Animation Properties

Here is every animation property in one table:

| Property                    | What It Controls                          | Default Value |
|-----------------------------|-------------------------------------------|---------------|
| `animation-name`            | Name of the `@keyframes` to use           | `none`        |
| `animation-duration`        | How long one cycle takes                  | `0s`          |
| `animation-timing-function` | Speed curve within each keyframe          | `ease`        |
| `animation-delay`           | Wait time before animation starts         | `0s`          |
| `animation-iteration-count` | How many times to repeat                  | `1`           |
| `animation-direction`       | Forward, reverse, or alternating          | `normal`      |
| `animation-fill-mode`       | Styles applied before/after animation     | `none`        |
| `animation-play-state`      | Pause or resume the animation             | `running`     |
| `animation` (shorthand)     | All of the above in one declaration       | —             |

---

## Guided Exercises

---

### Exercise 1 — The Suya Sign (Beginner)

**Scenario:** You are building a website for a suya spot in Ibadan. The owner wants an animated sign that catches the eye.

**Objective:** Create a div that fades in from invisible to fully visible.

**Steps:**

1. Create an HTML file with a `<div class="suya-sign">` containing the text "Fresh Suya — Oluwole Street, Ibadan"
2. In your CSS, create a `@keyframes` rule called `fadeIn`
3. At `from`, set `opacity: 0` (fully invisible)
4. At `to`, set `opacity: 1` (fully visible)
5. Apply the animation to `.suya-sign` with a duration of `2s`

**Hints:**
- Remember `opacity` goes from 0 (invisible) to 1 (visible)
- You need both `animation-name` and `animation-duration`

**Solution:**

```css
@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}

.suya-sign {
  background-color: #cc4400;
  color: white;
  padding: 20px;
  font-size: 22px;
  animation-name: fadeIn;
  animation-duration: 2s;
}
```

```html
<div class="suya-sign">Fresh Suya — Oluwole Street, Ibadan</div>
```

**Expected output in browser:** The sign starts completely invisible and smoothly becomes fully visible over 2 seconds.

**Self-check Questions:**
- What would happen if you set `animation-duration: 0.5s`?
- What would happen if you forgot `animation-name`?

---

### Exercise 2 — The Danfo Bus (Intermediate)

**Scenario:** You are building a Lagos transit app. You want to show a bus icon moving across the screen, and it should loop forever.

**Objective:** Animate a div from left to right, repeating infinitely, with an alternate direction so it goes back and forth.

**Steps:**

1. Create a `<div class="danfo">` with a yellow background and "🚌 Danfo" as text
2. Create a `@keyframes` called `driveDanfo`
3. At `0%`, set `transform: translateX(0px)`
4. At `100%`, set `transform: translateX(500px)`
5. Apply the animation with `animation-duration: 3s`, `animation-iteration-count: infinite`, `animation-direction: alternate`, and `animation-timing-function: ease-in-out`

**Solution:**

```css
@keyframes driveDanfo {
  0%   { transform: translateX(0px); }
  100% { transform: translateX(500px); }
}

.danfo {
  display: inline-block;
  background-color: #ffcc00;
  color: black;
  font-size: 20px;
  font-weight: bold;
  padding: 10px 20px;
  border-radius: 8px;
  animation-name: driveDanfo;
  animation-duration: 3s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
  animation-timing-function: ease-in-out;
}
```

```html
<div class="danfo">🚌 Danfo</div>
```

**Expected output in browser:** The yellow danfo moves to the right smoothly, then automatically slides back to the left, repeating forever.

**Self-check Questions:**
- Why does `alternate` make it go back and forth without extra keyframes?
- What would happen if you changed `ease-in-out` to `linear`?

---

### Exercise 3 — The Loading Spinner (Advanced)

**Scenario:** You are building the Konga.ng website clone. While products are loading, you want to show a rotating spinner.

**Objective:** Create a circular spinning loader with a delay and pause on hover.

**Steps:**

1. Create a `<div class="spinner">` in your HTML
2. Style it as a circle with `border-radius: 50%`, `width: 80px`, `height: 80px`
3. Give it a thick green border but make the top border transparent to create the "incomplete circle" effect
4. Create `@keyframes spin` that rotates from `0deg` to `360deg`
5. Apply: `animation-duration: 1s`, `animation-timing-function: linear`, `animation-iteration-count: infinite`, `animation-delay: 0.5s`
6. On hover, pause the animation

**Solution:**

```css
@keyframes spin {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}

.spinner {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  border: 8px solid #008000;
  border-top-color: transparent;   /* Creates the gap in the circle */
  animation-name: spin;
  animation-duration: 1s;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
  animation-delay: 0.5s;
}

.spinner:hover {
  animation-play-state: paused;
}
```

```html
<div class="spinner"></div>
<p>Loading products from Konga...</p>
```

**Expected output in browser:** After half a second, a green ring begins spinning continuously. Hovering over it freezes the spin. Moving away resumes it.

**Self-check Questions:**
- Why is `linear` the best timing function for a spinner rather than `ease`?
- Why does making `border-top-color: transparent` create the spinner effect?

---

## Code Challenges

---

### Challenge 1 — Growing Box

**Task:** Create a blue box that smoothly grows from `100px × 100px` to `300px × 300px`, then stays at its final size permanently.

**Hint:** Use `animation-fill-mode: forwards`.

**Solution:**

```css
@keyframes grow {
  from {
    width: 100px;
    height: 100px;
  }
  to {
    width: 300px;
    height: 300px;
  }
}

.growing-box {
  background-color: #003399;
  animation-name: grow;
  animation-duration: 2s;
  animation-fill-mode: forwards;
}
```

---

### Challenge 2 — Colour Carousel

**Task:** Create a `div` that cycles through the colours of the Nigerian flag and more. Go from green → white → red → yellow → green, repeating infinitely.

**Solution:**

```css
@keyframes colourCarousel {
  0%   { background-color: green; }
  25%  { background-color: white; }
  50%  { background-color: red; }
  75%  { background-color: yellow; }
  100% { background-color: green; }
}

.carousel {
  width: 200px;
  height: 200px;
  animation-name: colourCarousel;
  animation-duration: 4s;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
}
```

---

### Challenge 3 — Text Typing Effect

**Task:** Create a "typing" effect where text appears to be typed out letter by letter using `steps()`.

**Solution:**

```css
@keyframes typing {
  from { width: 0; }
  to   { width: 20ch; }  /* ch = width of the '0' character; set to match text length */
}

.typing-text {
  font-family: monospace;
  font-size: 20px;
  white-space: nowrap;
  overflow: hidden;
  border-right: 2px solid black;  /* Fake cursor */
  width: 0;
  animation-name: typing;
  animation-duration: 3s;
  animation-timing-function: steps(20, end);  /* 20 steps = 20 characters */
  animation-fill-mode: forwards;
}
```

```html
<p class="typing-text">E kaabo si Ibadan!</p>
```

**Expected output in browser:** The text "E kaabo si Ibadan!" appears to be typed out one character at a time over 3 seconds, with a blinking cursor.

---

### Challenge 4 — Delayed Entrance Sequence

**Task:** Create three boxes that slide in one after another, with a 0.5s delay between each.

**Solution:**

```css
@keyframes slideDown {
  from { 
    transform: translateY(-100px); 
    opacity: 0; 
  }
  to   { 
    transform: translateY(0); 
    opacity: 1; 
  }
}

.card {
  width: 200px;
  height: 60px;
  background-color: #008000;
  color: white;
  text-align: center;
  line-height: 60px;
  margin: 10px;
  animation-name: slideDown;
  animation-duration: 0.6s;
  animation-fill-mode: both;   /* Apply start-frame styles during delay too */
}

.card:nth-child(1) { animation-delay: 0s; }
.card:nth-child(2) { animation-delay: 0.5s; }
.card:nth-child(3) { animation-delay: 1s; }
```

```html
<div class="card">Eba</div>
<div class="card">Egusi Soup</div>
<div class="card">Ofe Akwu</div>
```

**Expected output in browser:** The three menu cards drop in one after another: Eba first, then Egusi Soup, then Ofe Akwu — each separated by half a second.

---

## Mini Project — The Animated Nigerian Market Badge

### Project Overview

You will build an animated product badge for a Nigerian online market stall. The badge will pulse, shimmer, and display a "Hot Deal!" message — all using CSS animations.

---

### Stage 1 — Setup the HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mama Nkechi's Online Market</title>
  <link rel="stylesheet" href="market-badge.css">
</head>
<body>

  <div class="market-wrapper">
    <div class="badge">
      <p class="stall-name">Mama Nkechi's Stall</p>
      <p class="deal-label">🔥 Hot Deal!</p>
      <p class="price">₦2,500 <span class="old-price">₦4,000</span></p>
      <p class="product">Premium Ofada Rice — 1kg</p>
    </div>
  </div>

</body>
</html>
```

**Milestone 1 output:** You should see a plain unstyled page with four lines of text.

---

### Stage 2 — Style the Base Badge

```css
/* market-badge.css */

body {
  background-color: #f4f0e8;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  margin: 0;
  font-family: 'Arial', sans-serif;
}

.badge {
  background-color: #006400;    /* Deep Nigerian green */
  color: white;
  width: 280px;
  padding: 30px;
  border-radius: 16px;
  text-align: center;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.stall-name {
  font-size: 14px;
  text-transform: uppercase;
  letter-spacing: 2px;
  margin: 0 0 10px;
  opacity: 0.8;
}

.deal-label {
  font-size: 32px;
  font-weight: bold;
  margin: 0 0 10px;
}

.price {
  font-size: 28px;
  font-weight: bold;
  margin: 0 0 8px;
}

.old-price {
  font-size: 16px;
  text-decoration: line-through;
  opacity: 0.6;
}

.product {
  font-size: 14px;
  margin: 0;
  opacity: 0.9;
}
```

**Milestone 2 output:** A clean, dark-green badge is centred on the page with all text styled but no animation yet.

---

### Stage 3 — Add the Pulse Animation

```css
@keyframes pulseBadge {
  0%   { transform: scale(1); box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3); }
  50%  { transform: scale(1.05); box-shadow: 0 15px 40px rgba(0, 100, 0, 0.6); }
  100% { transform: scale(1); box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3); }
}

.badge {
  /* Add these lines to the existing .badge rule */
  animation-name: pulseBadge;
  animation-duration: 2s;
  animation-timing-function: ease-in-out;
  animation-iteration-count: infinite;
}
```

**Milestone 3 output:** The badge now gently pulses — growing slightly larger and casting a deeper green glow, then returning to normal, repeating forever.

---

### Stage 4 — Animate the Deal Label

```css
@keyframes flickerFire {
  0%   { transform: scale(1)    rotate(-3deg); color: #ffcc00; }
  25%  { transform: scale(1.15) rotate(3deg);  color: #ff6600; }
  50%  { transform: scale(1)    rotate(-2deg); color: #ffcc00; }
  75%  { transform: scale(1.1)  rotate(2deg);  color: #ff3300; }
  100% { transform: scale(1)    rotate(-3deg); color: #ffcc00; }
}

.deal-label {
  /* Add these to the existing .deal-label rule */
  display: inline-block;   /* Required for transform to work on inline elements */
  animation-name: flickerFire;
  animation-duration: 0.8s;
  animation-timing-function: ease-in-out;
  animation-iteration-count: infinite;
}
```

**Milestone 4 output:** The 🔥 Hot Deal! text flickers and wobbles in red-orange-yellow colours like a real flame, making the badge feel urgent and exciting.

---

### Stage 5 — Entrance Animation + Pause on Hover

```css
@keyframes entranceDrop {
  0%   { transform: translateY(-80px) scale(0.8); opacity: 0; }
  60%  { transform: translateY(10px)  scale(1.05); opacity: 1; }
  100% { transform: translateY(0)     scale(1); opacity: 1; }
}

.market-wrapper {
  animation-name: entranceDrop;
  animation-duration: 0.9s;
  animation-timing-function: ease-out;
  animation-fill-mode: both;
}

.badge:hover {
  animation-play-state: paused;
}
```

**Milestone 5 (Final) output:** When the page loads, the badge drops in with a satisfying bounce effect. It then pulses continuously. The flame label flickers. When the user hovers over the badge, everything freezes — giving the user time to read the deal clearly.

---

## Common Beginner Mistakes

---

### Mistake 1 — Forgetting `animation-duration`

**Wrong:**
```css
.box {
  animation-name: fadeIn;
  /* No animation-duration! */
}
```

**Problem:** The default duration is `0s`. The animation completes instantly and appears to do nothing.

**Correct:**
```css
.box {
  animation-name: fadeIn;
  animation-duration: 2s;   /* Always specify this! */
}
```

---

### Mistake 2 — Misspelling the `@keyframes` Name

**Wrong:**
```css
@keyframes FadeIn { ... }   /* Capital F */

.box {
  animation-name: fadein;   /* Lowercase — does NOT match! */
}
```

**Problem:** `animation-name` is case-sensitive. `FadeIn` and `fadein` are different names.

**Correct:**
```css
@keyframes fadeIn { ... }

.box {
  animation-name: fadeIn;   /* Exact same spelling and capitalisation */
}
```

---

### Mistake 3 — Using `transform` on Inline Elements

**Wrong:**
```css
@keyframes wobble {
  from { transform: rotate(0deg); }
  to   { transform: rotate(10deg); }
}

span {
  animation-name: wobble;
  animation-duration: 1s;
}
```

**Problem:** `<span>` is an inline element. `transform` has no effect on inline elements.

**Correct:**
```css
span {
  display: inline-block;   /* Makes transform work on inline elements */
  animation-name: wobble;
  animation-duration: 1s;
}
```

---

### Mistake 4 — Confusing `animation-duration` and `animation-delay` in Shorthand

**Wrong:**
```css
/* Trying to set delay=1s and duration=2s */
animation: fadeIn 1s 2s;
/* This is actually: duration=1s delay=2s — the OPPOSITE! */
```

**Correct:**
```css
/* Duration ALWAYS comes before delay in shorthand */
animation: fadeIn 2s ease 1s;
/*                 ↑  ↑   ↑
             duration  |  delay
                  timing-fn */
```

---

### Mistake 5 — Expecting `forwards` to Stop an Infinite Animation

**Wrong thinking:** "I want the animation to stop after the first cycle and stay at its final frame."

```css
animation-iteration-count: infinite;
animation-fill-mode: forwards;
```

**Problem:** `forwards` only takes effect when the animation *finishes*. An infinite animation never finishes, so `forwards` has no effect.

**Correct:** If you want it to run once and stay, use `iteration-count: 1`:

```css
animation-iteration-count: 1;
animation-fill-mode: forwards;
```

---

### Mistake 6 — Swapping `animation-timing-function` Values

**Wrong:**
```css
@keyframes slide {
  from { transform: translateX(0); }
  to   { transform: translateX(200px); }
}

.box { animation-timing-function: begin-fast; }  /* NOT a valid value! */
```

**Correct valid values:** `ease`, `linear`, `ease-in`, `ease-out`, `ease-in-out`, `cubic-bezier(...)`, `steps(...)`

```css
.box { animation-timing-function: ease-in; }
```

---

## Reflection Questions

Think through these questions carefully before moving to the next lesson:

1. What is the difference between a CSS animation and a CSS transition? When would you choose one over the other?
2. If an animation has `animation-delay: 2s` and `animation-fill-mode: backwards`, what does the element look like during those 2 seconds?
3. Why does a spinner need `animation-timing-function: linear` instead of `ease`?
4. If you set `animation-direction: alternate` and `animation-iteration-count: 4`, how many times does the animation play forwards and how many times backwards?
5. Can two completely different `@keyframes` animations run on the same element at the same time? How?

---

## Completion Checklist

Before marking this lesson complete, confirm that you can do the following:

- [ ] I can write a `@keyframes` rule using both `from/to` and `%` syntax
- [ ] I can attach an animation to an element using `animation-name` and `animation-duration`
- [ ] I can add a delay with `animation-delay`
- [ ] I can make an animation loop using `animation-iteration-count: infinite`
- [ ] I can control direction using `animation-direction` (including `alternate`)
- [ ] I can use `animation-fill-mode: forwards` to hold the final state
- [ ] I can pause an animation with `animation-play-state: paused`
- [ ] I can explain the difference between `ease`, `linear`, `ease-in`, and `ease-out`
- [ ] I can use `steps()` for a frame-by-frame effect
- [ ] I can write the `animation` shorthand correctly with the right order
- [ ] I can animate multiple elements with staggered delays
- [ ] I completed the Animated Nigerian Market Badge mini-project

---

## Lesson Summary

In this lesson, you learned one of the most powerful visual tools in CSS — **CSS Animations**. Here is a quick recap of everything covered:

**Foundations:** An animation requires a `@keyframes` rule (which defines what the element looks like at each stage) and animation properties applied to the element (which control timing, repetition, and behaviour).

**`@keyframes`:** Use `from`/`to` for simple two-stage animations or `0%`/`50%`/`100%` (and any percentages in between) for complex multi-stage animations.

**Core properties:** `animation-name`, `animation-duration`, `animation-delay`, `animation-iteration-count`, `animation-direction`, `animation-fill-mode`, and `animation-play-state` give you complete control over how an animation behaves.

**Timing functions:** `ease`, `linear`, `ease-in`, `ease-out`, `ease-in-out`, `cubic-bezier()`, and `steps()` control the speed curve of the animation, making it feel natural, mechanical, bouncy, or snappy.

**Shorthand:** The `animation` property lets you write all properties in a single line: `animation: name duration timing delay iterations direction fill-mode;`

**Multiple animations:** Separate multiple animation declarations with commas to run several animations on a single element simultaneously.

---

## Quick-Reference Card

```
@keyframes myAnim {
  0%   { /* start styles */ }
  50%  { /* mid styles */ }
  100% { /* end styles */ }
}

.element {
  animation-name:             myAnim;
  animation-duration:         2s;
  animation-timing-function:  ease-in-out;  /* ease | linear | ease-in | ease-out | cubic-bezier() | steps() */
  animation-delay:            0.5s;
  animation-iteration-count:  infinite;     /* or a number */
  animation-direction:        alternate;    /* normal | reverse | alternate | alternate-reverse */
  animation-fill-mode:        forwards;     /* none | forwards | backwards | both */
  animation-play-state:       running;      /* running | paused */

  /* OR all in one line: */
  animation: myAnim 2s ease-in-out 0.5s infinite alternate forwards running;
}

/* Pause on hover */
.element:hover {
  animation-play-state: paused;
}

/* Multiple animations */
.element {
  animation: slideIn 1s ease, pulse 2s linear infinite;
}
```

---

*End of Lesson 56 — CSS Animations*
