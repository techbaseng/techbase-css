---
render_with_liquid: false
title: "CSS @property Rule – Defining and Animating Custom CSS Properties"
nav_order: 66
---

# Lesson 66 – CSS `@property` Rule: Defining and Animating Custom CSS Properties

---

## Lesson Introduction

Imagine you are painting a room and you want to be able to smoothly fade the wall colour from white to deep blue at the click of a button. With normal CSS variables (which you may have learned before), that smooth fade — called an **animation** — is impossible. The colour would just jump instantly.

The **CSS `@property` rule** was invented to solve exactly this problem. It lets you create your own custom CSS properties that the browser fully understands: what type of value they hold, what their default is, and whether they can be smoothly animated. This makes your pages far more dynamic, readable, and powerful.

By the end of this lesson you will be able to:
- Explain what the `@property` rule is and why it was created.
- Write a complete `@property` declaration with all required fields.
- Use your registered custom property anywhere in your CSS.
- Animate custom properties smoothly using CSS transitions and keyframe animations.
- Apply `@property` to real-world design tasks like animated gradients, colour themes, and UI effects.

---

## Prerequisite Concepts

Before diving in, you need to be comfortable with a few ideas. If any of these are new, read the short explanation given here — then carry on.

### What is a CSS Variable (Custom Property)?

A CSS variable is a name you create yourself, starting with two dashes `--`, that stores a value you can reuse.

```css
/* Storing a colour in a variable */
:root {
  --brand-colour: tomato;
}

/* Using it */
h1 {
  color: var(--brand-colour);
}
```

**Output (visual):** The `<h1>` heading appears in the colour tomato (a vivid red-orange).

The problem: The browser treats regular CSS variables as **plain text strings** — it just does a find-and-replace. It has no idea the value is a colour, a number, or a length. This means it cannot smoothly transition between two variable values during an animation.

### What is a CSS Transition?

A CSS transition smoothly changes a property from one value to another over a set time.

```css
div {
  background-color: blue;
  transition: background-color 1s ease;
}

div:hover {
  background-color: red;
}
```

**Output (visual):** When you hover over the `div`, the background slowly fades from blue to red over 1 second.

> **Key idea:** Transitions only work when the browser understands the *type* of value (colour, length, number, etc.). CSS variables without `@property` are opaque text — the browser cannot animate them.

### What is a CSS Animation (Keyframes)?

An animation plays a sequence of style changes automatically.

```css
@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}

p {
  animation: fadeIn 2s ease;
}
```

**Output (visual):** The paragraph fades in from invisible to fully visible over 2 seconds.

Now you are ready for `@property`.

---

## Conceptual Understanding

### What is the `@property` Rule?

The `@property` rule is a special CSS instruction that lets you **register** a custom CSS property (a variable) with the browser. When you register a property, you tell the browser three important things:

1. **What type of value it holds** — for example, is it a colour, a length, a number, or a percentage?
2. **Whether it inherits** from parent elements — like how `font-size` passes down to children.
3. **What its initial (default) value is** — so if no value is set, the browser still knows what to display.

**Analogy:** Think of a CSS variable as an unmarked box. The browser does not know if the box contains a colour, a word, or a number — it just passes the box around. `@property` is like labelling the box: "This box contains a COLOUR. Its default is red. It passes down to children." Now the browser can treat the contents intelligently — including animating between values.

### Why Does `@property` Exist?

The problem it solves is **animating custom properties**. Before `@property`, you could not smoothly animate a CSS variable value because the browser treated it as plain text. With `@property`, the browser understands the value type and can smoothly interpolate (calculate intermediate steps) between two values during an animation.

This was a feature that previously required JavaScript to achieve. Now it is pure CSS.

### The Syntax of `@property`

```css
@property --property-name {
  syntax: '<type>';
  inherits: true | false;
  initial-value: value;
}
```

Let's break down every single part of this:

| Part | What it means |
|---|---|
| `@property` | The at-rule keyword that starts a custom property registration. |
| `--property-name` | The name of your custom property. Must start with two dashes `--`. |
| `syntax` | The **type** of value this property holds, written as a CSS data type string. |
| `inherits` | Whether child elements automatically receive this property's value from a parent. `true` = yes, `false` = no. |
| `initial-value` | The default value used when no other value is set. |

> **Important:** All three descriptors — `syntax`, `inherits`, and `initial-value` — are **required**. If any one is missing, the `@property` rule is invalid.

### The `syntax` Descriptor — Data Types

The `syntax` field tells the browser what kind of data the property holds. Here are the most common types:

| Syntax value | What it means | Example value |
|---|---|---|
| `'<color>'` | A CSS colour | `red`, `#ff0000`, `rgb(255,0,0)` |
| `'<length>'` | A CSS measurement | `20px`, `3rem`, `50%` |
| `'<number>'` | A plain number (no unit) | `0.5`, `10`, `-3` |
| `'<percentage>'` | A percentage value | `50%`, `100%` |
| `'<integer>'` | A whole number | `0`, `5`, `100` |
| `'<angle>'` | A rotation angle | `45deg`, `1.5rad` |
| `'<length-percentage>'` | Either a length or percentage | `20px` or `50%` |
| `'*'` | Any value (no type checking) | anything |

---

## Simple Standalone Examples

### Example 1 – Registering a Simple Colour Property

This is the most minimal, isolated example. We register a custom colour property, give it a default value, and use it on a box.

```css
/* Step 1: Register the property */
@property --box-colour {
  syntax: '<color>';
  inherits: false;
  initial-value: lightblue;
}

/* Step 2: Use the property */
div {
  background-color: var(--box-colour);
  width: 200px;
  height: 100px;
}
```

```html
<div></div>
```

**Expected output:** A rectangle 200px wide and 100px tall with a light blue background.

**What happened:**
- `@property --box-colour` registered a new custom property named `--box-colour`.
- `syntax: '<color>'` told the browser it holds a colour value.
- `inherits: false` means child elements inside the `div` do not automatically get this value.
- `initial-value: lightblue` sets the default — so even without a `--box-colour` value anywhere in the CSS, the box shows light blue.
- `var(--box-colour)` reads the variable value just like a normal CSS variable.

> **Thinking prompt:** What happens if you remove the `initial-value` line? The `@property` rule becomes invalid and the property is ignored entirely!

---

### Example 2 – Overriding the Registered Property's Value

Now we set a different value on an element, overriding the `initial-value`.

```css
@property --box-colour {
  syntax: '<color>';
  inherits: false;
  initial-value: lightblue;
}

.card {
  --box-colour: coral;   /* Override the default */
  background-color: var(--box-colour);
  width: 200px;
  height: 100px;
}

.plain {
  background-color: var(--box-colour);
  width: 200px;
  height: 100px;
}
```

```html
<div class="card"></div>
<div class="plain"></div>
```

**Expected output:**
- `.card` shows a **coral** (salmon-orange) background.
- `.plain` shows a **light blue** background (falls back to `initial-value`).

**Why this matters:** The `.plain` div never sets `--box-colour`, so the browser uses the registered `initial-value` of `lightblue`. This is much safer than a regular CSS variable which would produce nothing (invalid value) if not set.

> **Thinking prompt:** What would `.plain` look like if `--box-colour` were a regular CSS variable with no default? It would have no background colour at all — transparent!

---

### Example 3 – Registering a Number Property

Numbers (without units) are useful for controlling transparency, scale, or counters.

```css
@property --opacity-level {
  syntax: '<number>';
  inherits: false;
  initial-value: 1;
}

.box {
  background-color: steelblue;
  width: 150px;
  height: 150px;
  opacity: var(--opacity-level);
}

.faded {
  --opacity-level: 0.3;
}
```

```html
<div class="box">Normal</div>
<div class="box faded">Faded</div>
```

**Expected output:**
- First box: Fully opaque steelblue square.
- Second box: Same square at 30% opacity (very light/transparent).

---

### Example 4 – The Power of `@property`: Animating a Custom Colour (The Big Moment!)

This is the key example — the reason `@property` exists. Notice how the colour smoothly animates. Without `@property`, this would **not** work.

```css
/* Register with @property so the browser can animate it */
@property --bg-colour {
  syntax: '<color>';
  inherits: false;
  initial-value: orange;
}

.animated-box {
  --bg-colour: orange;
  background-color: var(--bg-colour);
  width: 200px;
  height: 200px;
  transition: --bg-colour 1s ease;   /* Animate the custom property */
}

.animated-box:hover {
  --bg-colour: purple;
}
```

```html
<div class="animated-box"></div>
```

**Expected output:**
- Box starts as **orange**.
- When you hover over it, the colour **smoothly transitions** to purple over 1 second.
- When you move the mouse away, it smoothly returns to orange.

**Why this is remarkable:** The `transition` is applied directly to the custom property `--bg-colour`. Because `@property` registered it as a `<color>` type, the browser can calculate all the intermediate colour steps during the 1-second animation. Without `@property`, the box would just **jump** instantly from orange to purple — no smooth transition.

> **Thinking prompt:** What if you changed `syntax: '<color>'` to `syntax: '*'` (any value)? Try it — the transition would break and the colour would jump again, because `'*'` means no type information.

---

### Example 5 – Animating a Number Property (Gradient Rotation)

A very popular real-world use of `@property` is animating the angle of a gradient.

```css
@property --gradient-angle {
  syntax: '<angle>';
  inherits: false;
  initial-value: 0deg;
}

@keyframes spin-gradient {
  to {
    --gradient-angle: 360deg;
  }
}

.gradient-box {
  width: 250px;
  height: 250px;
  background: linear-gradient(var(--gradient-angle), red, blue);
  animation: spin-gradient 4s linear infinite;
}
```

```html
<div class="gradient-box"></div>
```

**Expected output:** A box with a red-to-blue gradient that **continuously rotates** in a 360° loop every 4 seconds.

**Line-by-line explanation:**

| Line | Explanation |
|---|---|
| `@property --gradient-angle` | Register a custom property named `--gradient-angle`. |
| `syntax: '<angle>'` | Tell the browser this is a CSS angle (like `45deg`, `360deg`). |
| `initial-value: 0deg` | Default starting angle is 0 degrees. |
| `@keyframes spin-gradient` | Define a named animation. |
| `to { --gradient-angle: 360deg; }` | At the end of the animation, the angle is 360 degrees. |
| `linear-gradient(var(--gradient-angle), red, blue)` | The gradient uses the angle from the variable. |
| `animation: spin-gradient 4s linear infinite` | Play the animation continuously, 4 seconds per loop. |

Because `--gradient-angle` is registered as `<angle>`, the browser smoothly steps through 0°, 45°, 90°, 180°... all the way to 360°, creating a smooth spin effect.

---

### Example 6 – Animating a Percentage (Animated Progress Bar)

```css
@property --progress {
  syntax: '<percentage>';
  inherits: false;
  initial-value: 0%;
}

@keyframes load {
  to { --progress: 80%; }
}

.progress-bar {
  width: var(--progress);
  height: 20px;
  background-color: green;
  animation: load 2s ease forwards;
}

.track {
  width: 300px;
  background-color: lightgrey;
  border-radius: 10px;
  overflow: hidden;
}
```

```html
<div class="track">
  <div class="progress-bar"></div>
</div>
```

**Expected output:** A grey track bar. Inside it, a green bar animates from 0% width to 80% width over 2 seconds — like a loading bar filling up.

---

## Complete `@property` Reference Table

| Descriptor | Required? | Allowed values | Purpose |
|---|---|---|---|
| `syntax` | Yes | `'<color>'`, `'<length>'`, `'<number>'`, `'<percentage>'`, `'<angle>'`, `'<integer>'`, `'<length-percentage>'`, `'*'` | Declares the value type |
| `inherits` | Yes | `true` or `false` | Controls value inheritance to child elements |
| `initial-value` | Yes (if syntax is not `'*'`) | Any valid value matching the declared syntax | Sets the default/fallback value |

---

## Guided Practice Exercises

### Exercise 1 – Register and Use a Length Property

**Objective:** Practice registering a `<length>` type custom property and using it to control a box's border radius.

**Scenario:** You are building a UI card. You want to control the corner roundness with a custom property so it can be easily changed or animated.

**Steps:**

1. Open a new HTML file and add a `<div class="card">Hello!</div>`.
2. In your CSS, register a property called `--corner-round` of type `<length>` with a default of `0px`.
3. Apply it to `.card` as `border-radius: var(--corner-round)`.
4. Add a width of `200px`, height of `100px`, and a background colour of `salmon`.
5. Override the variable on `.card` to `20px` and observe the rounded corners.

**Hint:** The `@property` block goes at the top of your stylesheet, before any selectors.

**Expected output:** A salmon-coloured card with 20px rounded corners.

**Solution:**

```css
@property --corner-round {
  syntax: '<length>';
  inherits: false;
  initial-value: 0px;
}

.card {
  --corner-round: 20px;
  border-radius: var(--corner-round);
  width: 200px;
  height: 100px;
  background-color: salmon;
  padding: 10px;
}
```

**Self-check questions:**
- What would happen if you removed `--corner-round: 20px` from `.card`? (It falls back to `0px` — no rounding.)
- What would happen if you wrote `initial-value: hello` — is `hello` a valid length? (No — the `@property` would be invalid.)

---

### Exercise 2 – Create a Hover Colour Transition Using `@property`

**Objective:** Use `@property` to enable a smooth colour transition on hover.

**Scenario:** You are building a button for a web app. The button should smoothly change colour when hovered.

**Steps:**

1. Create a `<button class="btn">Click Me</button>`.
2. Register `--btn-bg` as a `<color>` type with initial value `royalblue`.
3. Style `.btn` with `background-color: var(--btn-bg)`, some padding, white text, and `transition: --btn-bg 0.5s ease`.
4. On `.btn:hover`, set `--btn-bg: crimson`.
5. Hover over the button — observe the smooth fade.

**Expected output:** A blue button that smoothly fades to crimson red on hover.

**Solution:**

```css
@property --btn-bg {
  syntax: '<color>';
  inherits: false;
  initial-value: royalblue;
}

.btn {
  --btn-bg: royalblue;
  background-color: var(--btn-bg);
  transition: --btn-bg 0.5s ease;
  color: white;
  padding: 12px 24px;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
}

.btn:hover {
  --btn-bg: crimson;
}
```

**Self-check questions:**
- Why do you also write `--btn-bg: royalblue` in `.btn` even though the initial-value is already `royalblue`? (This ensures the transition starts from this value correctly on the element level.)
- What if you removed the `@property` block entirely? (The transition would fail — the colour would jump instead of fade.)

---

### Exercise 3 – Animate a Number to Control Scale

**Objective:** Use `@property` with a `<number>` to animate an element's scale via a CSS custom property.

**Steps:**

1. Register `--scale-factor` as `<number>` with initial value `1`.
2. Create `@keyframes grow` going from the default to `--scale-factor: 1.5`.
3. Apply the animation to a `.icon` box — use `transform: scale(var(--scale-factor))`.
4. Run the animation on hover.

**Expected output:** On hover, the element smoothly grows to 1.5× its size.

**Solution:**

```css
@property --scale-factor {
  syntax: '<number>';
  inherits: false;
  initial-value: 1;
}

@keyframes grow {
  to { --scale-factor: 1.5; }
}

.icon {
  width: 80px;
  height: 80px;
  background-color: gold;
  border-radius: 50%;
}

.icon:hover {
  animation: grow 0.4s ease forwards;
}
```

---

## Mini Project – Animated Gradient Hero Banner

**Goal:** Build a full webpage hero section where the background gradient angle continuously rotates, using `@property` to make it animatable.

### Stage 1 – Setup the HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Animated Hero</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <section class="hero">
    <h1>Welcome to My Site</h1>
    <p>Built with the power of CSS @property</p>
    <a href="#" class="cta-btn">Get Started</a>
  </section>
</body>
</html>
```

**Milestone output:** A plain page with a heading, paragraph, and link.

---

### Stage 2 – Register the Gradient Angle Property

```css
@property --hero-angle {
  syntax: '<angle>';
  inherits: false;
  initial-value: 0deg;
}
```

**Why:** This registers `--hero-angle` so the browser knows it's an angle type and can smoothly animate between angle values.

---

### Stage 3 – Build the Hero Section Styles

```css
body {
  margin: 0;
  font-family: 'Segoe UI', sans-serif;
}

.hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  background: linear-gradient(
    var(--hero-angle),
    #6a11cb,
    #2575fc,
    #6a11cb
  );
  color: white;
  padding: 40px;
  animation: rotate-gradient 6s linear infinite;
}

@keyframes rotate-gradient {
  to {
    --hero-angle: 360deg;
  }
}

.hero h1 {
  font-size: 3rem;
  margin-bottom: 16px;
}

.hero p {
  font-size: 1.25rem;
  margin-bottom: 32px;
  opacity: 0.9;
}
```

**Milestone output:** A full-screen hero section with a purple-to-blue gradient that slowly rotates in a circle.

---

### Stage 4 – Add the Animated CTA Button

```css
@property --btn-colour {
  syntax: '<color>';
  inherits: false;
  initial-value: white;
}

.cta-btn {
  --btn-colour: white;
  background-color: var(--btn-colour);
  color: #6a11cb;
  padding: 14px 36px;
  border-radius: 50px;
  text-decoration: none;
  font-size: 1.1rem;
  font-weight: bold;
  transition: --btn-colour 0.4s ease, color 0.4s ease;
}

.cta-btn:hover {
  --btn-colour: #6a11cb;
  color: white;
}
```

**Milestone output:** A white pill-shaped button. On hover, it smoothly transitions to purple with white text.

---

### Stage 5 – Final Result

Put it all together. Your final page should show:
- A rotating purple-blue gradient background filling the entire viewport height.
- A large white heading and paragraph.
- A button that smoothly changes colour on hover.

**Reflection questions:**
- What would happen if you replaced `@property --hero-angle` with a regular CSS variable `--hero-angle: 0deg` in `:root`?  
  (The gradient rotation animation would not work — the angle would jump to 360deg instantly.)
- Could you add a second `@property` to animate the gradient colours themselves? Try it!
- How could you use `@property` on a dark-mode toggle?

**Optional extensions:**
- Add a second animated element (a pulsing circle) using `@property --pulse-size` of type `<length>`.
- Try animating a text shadow colour using `@property --glow-colour`.

---

## `@property` vs Regular CSS Variables — Side-by-Side Comparison

| Feature | Regular CSS Variable | `@property` Registered Variable |
|---|---|---|
| Syntax | `--name: value` in a ruleset | `@property --name { ... }` at-rule |
| Type checking | No — it's just text | Yes — you declare the type |
| Can be animated/transitioned | No — jumps instantly | Yes — smooth interpolation |
| Inheritance control | Always inherits by default | You choose `true` or `false` |
| Default value | Not guaranteed | Guaranteed via `initial-value` |
| Browser support | Universal | Modern browsers (Chrome 85+, Firefox 128+, Safari 16.4+) |

---

## Common Beginner Mistakes

### Mistake 1 – Missing a Required Descriptor

**Wrong:**
```css
@property --my-colour {
  syntax: '<color>';
  initial-value: red;
  /* MISSING: inherits */
}
```

**Problem:** All three descriptors are required. Missing `inherits` makes the entire `@property` block invalid and ignored.

**Correct:**
```css
@property --my-colour {
  syntax: '<color>';
  inherits: false;
  initial-value: red;
}
```

---

### Mistake 2 – Wrong Syntax Value Format (Forgetting Quotes)

**Wrong:**
```css
@property --my-colour {
  syntax: <color>;       /* Missing quotes! */
  inherits: false;
  initial-value: red;
}
```

**Problem:** The `syntax` value MUST be inside single quotes `'<color>'`. Without quotes, it is invalid.

**Correct:**
```css
@property --my-colour {
  syntax: '<color>';
  inherits: false;
  initial-value: red;
}
```

---

### Mistake 3 – `initial-value` Doesn't Match the `syntax` Type

**Wrong:**
```css
@property --my-size {
  syntax: '<length>';
  inherits: false;
  initial-value: blue;   /* 'blue' is a colour, not a length! */
}
```

**Problem:** The initial value must be a valid value for the declared syntax type. `blue` is not a CSS length.

**Correct:**
```css
@property --my-size {
  syntax: '<length>';
  inherits: false;
  initial-value: 0px;
}
```

---

### Mistake 4 – Forgetting to Set the Variable on the Element Before Transitioning

**Wrong (transition may not work as expected):**
```css
@property --bg {
  syntax: '<color>';
  inherits: false;
  initial-value: blue;
}

.box {
  background-color: var(--bg);
  transition: --bg 1s ease;
}

.box:hover {
  --bg: red;
}
```

The transition from `initial-value` to the hover value may work, but it is best practice to explicitly set the starting value on the element itself for predictable results.

**Better:**
```css
.box {
  --bg: blue;              /* Explicitly set */
  background-color: var(--bg);
  transition: --bg 1s ease;
}
```

---

### Mistake 5 – Trying to Animate with `syntax: '*'`

**Wrong:**
```css
@property --my-value {
  syntax: '*';             /* No type info */
  inherits: false;
  initial-value: red;
}

.box {
  background-color: var(--my-value);
  transition: --my-value 1s ease;   /* Will NOT animate */
}
```

**Problem:** `syntax: '*'` means "any type" — the browser still cannot interpolate (animate) because it does not know if it is a colour, number, or something else.

**Correct:** Use a specific type like `syntax: '<color>'`.

---

### Mistake 6 – Using `@property` Without Browser Support Fallback

`@property` is a newer feature. Older browsers (especially older Firefox and Safari) may not support it.

**Safe approach — always provide a fallback:**
```css
/* Fallback for browsers that don't support @property */
.box {
  background-color: orange;
}

/* Modern browsers will use @property + var() */
@property --box-bg {
  syntax: '<color>';
  inherits: false;
  initial-value: orange;
}

.box {
  background-color: var(--box-bg);
  transition: --box-bg 0.5s ease;
}

.box:hover {
  --box-bg: purple;
}
```

---

## Real-World Use Cases

`@property` is used in professional web development for:

- **Animated gradient backgrounds** — rotating or shifting gradients on hero banners (as in the mini project).
- **Theme switchers** — smoothly transitioning between light and dark themes.
- **Animated loaders and progress bars** — using `<percentage>` or `<length>` types.
- **Hover effects on buttons and cards** — smooth colour transitions on interactive components.
- **Data visualisations** — animating chart bars, pie segments, or gauges using custom numeric properties.
- **CSS-only animations** that previously required JavaScript to achieve.

---

## Reflection Questions

1. What is the fundamental difference between a regular CSS variable and a property registered with `@property`?
2. Why are all three descriptors (`syntax`, `inherits`, `initial-value`) required in a `@property` declaration?
3. What does `syntax: '<angle>'` tell the browser, and why is it necessary for animating a rotating gradient?
4. When would you choose `inherits: true` vs `inherits: false`?
5. What would happen if you used `syntax: '*'` and tried to animate the property with a transition?
6. Can you think of a UI element on a popular website that might be using `@property` behind the scenes?

---

## Completion Checklist

Before moving on, make sure you can do all of the following:

- [ ] Write a complete `@property` block with all three required descriptors.
- [ ] Register a custom property as type `<color>`, `<length>`, `<number>`, `<percentage>`, and `<angle>`.
- [ ] Use a registered custom property with `var()` in a CSS rule.
- [ ] Apply a `transition` to a registered custom property so it animates smoothly.
- [ ] Use a registered custom property inside `@keyframes` for a keyframe animation.
- [ ] Explain the difference between `inherits: true` and `inherits: false`.
- [ ] Identify and fix the five most common `@property` mistakes.
- [ ] Build a rotating animated gradient using `--gradient-angle` of type `<angle>`.
- [ ] Create a smooth hover colour effect on a button using `@property`.

---

## Lesson Summary

The **CSS `@property` rule** is a powerful modern CSS feature that allows you to register custom CSS properties (variables) with full type information. Here is what you have learned:

The syntax for declaring a registered property is:
```css
@property --property-name {
  syntax: '<type>';
  inherits: true | false;
  initial-value: value;
}
```

The three required descriptors are `syntax` (the value type), `inherits` (whether it passes to children), and `initial-value` (the default value).

The most important benefit of `@property` over regular CSS variables is **animatability** — by declaring the value type, the browser can smoothly transition and animate custom property values, which is impossible with plain CSS variables.

Common types include `<color>` for colours, `<length>` for measurements, `<number>` for plain numbers, `<percentage>` for percentages, and `<angle>` for rotation angles.

Real-world uses include animated gradients, smooth hover effects, animated progress bars, and theme transitions — all without any JavaScript.

`@property` is supported in all modern browsers (Chrome 85+, Firefox 128+, Safari 16.4+). Always provide a static CSS fallback for older browser compatibility.

---

*Sources: W3Schools CSS @property Tutorial — css3_property.asp | W3Schools CSS @property Code Challenge — css_challenges_css3_property.asp*
