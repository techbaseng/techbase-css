---
render_with_liquid: false
title: "Lesson 64: CSS User Interface – Resize and Outline Offset"
nav_order: 64
---

# Lesson 64: CSS User Interface – Resize and Outline Offset

---

## Lesson Introduction

Have you ever visited a website and noticed that a comment box could be stretched larger by dragging its corner? Or noticed that a focused input field had a glowing ring slightly separated from the element itself — not touching it, but floating just outside? Both of those effects are controlled by CSS User Interface properties.

In this lesson, you will learn two powerful CSS properties that directly improve the experience of people using your webpage:

- **`resize`** — lets you control whether a user can manually resize an element on the screen
- **`outline-offset`** — lets you control how far an outline sits from the edge of an element

These are small but mighty properties. Knowing them gives your web forms and interactive elements a polished, professional look and feel — exactly the kind of detail that separates beginner projects from professional ones.

---

### What You Will Learn

By the end of this lesson, you will be able to:

1. Explain what the `resize` property does and why it exists
2. Use `resize` to allow horizontal-only, vertical-only, or both-direction resizing
3. Disable resizing entirely on a `<textarea>` element
4. Explain what `outline-offset` does and how it differs from the `outline` property itself
5. Set an outline that floats away from an element's edge
6. Use both properties together in a real-world form design

---

## Prerequisite Concepts

Before diving into this lesson, make sure you are comfortable with these ideas. If anything feels unfamiliar, take a moment to review the earlier lesson linked to each concept.

**CSS Outlines (Lesson 39–40):** An outline is a line drawn *outside* an element's border. Unlike borders, outlines do not take up space in the page layout. The `outline` property controls the style, width, and colour of that line.

**The `overflow` property:** When an element is resized by the user, its content may overflow its original boundaries. Setting `overflow: auto` or `overflow: scroll` ensures the element handles that extra content gracefully by showing a scrollbar when needed.

**Block-level elements and `<textarea>`:** A `<div>` is a generic block-level element — a rectangular box on the page. A `<textarea>` is an HTML form element where users can type multiple lines of text. Both can have the `resize` property applied to them.

---

## Part 1: The `resize` Property

### 1.1 — What Is It and Why Does It Exist?

Imagine you are filling in a feedback form on a Nigerian government portal. The comment box is tiny — barely two lines tall — but you have a lot to say. Frustrating, right?

The `resize` property was created to solve exactly that problem. It lets the web designer give users the ability to manually drag the corner of an element to make it bigger (or smaller). Think of it like the resize handle in the bottom-right corner of a window on your computer.

**Why does this matter?**

- **Better user experience** — users can expand text areas as needed
- **Flexible forms** — feedback boxes, address fields, and message areas all benefit
- **Design control** — you can restrict resizing to only one direction (width or height), preventing your page layout from breaking

---

### 1.2 — The Four Values of `resize`

The `resize` property accepts four possible values:

| Value | What It Does |
|---|---|
| `horizontal` | User can drag to change the **width** only |
| `vertical` | User can drag to change the **height** only |
| `both` | User can drag to change **both** width and height |
| `none` | User **cannot** resize the element at all |

> **Important Rule:** The `resize` property only works on elements that also have `overflow` set to something *other than* `visible`. You must set `overflow: auto`, `overflow: scroll`, or `overflow: hidden` alongside `resize` for it to work on most elements. A `<textarea>` is naturally resizable in most browsers without needing `overflow`, but it is still good practice to include it.

---

### 1.3 — Example 1: Resize Width Only (`horizontal`)

**The scenario:** You want a search filter box on your market price comparison site for Lagos traders. The box should expand sideways if the user needs more space, but the height must stay fixed.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* This div can only be made wider by the user */
    div {
      border: 2px solid #2c7a2c;   /* Green border */
      padding: 15px;
      width: 300px;
      height: 80px;
      overflow: auto;              /* Required for resize to work */
      resize: horizontal;          /* Allow width resizing only */
      background-color: #f0fff0;
      font-family: Arial, sans-serif;
    }
  </style>
</head>
<body>
  <h2>Lagos Market Price Filter</h2>
  <div>Drag the right edge to make this box wider. The height will not change.</div>
</body>
</html>
```

**Expected output in browser:**
A green-bordered box appears. The user can grab the bottom-right corner handle and drag it **to the right** to make the box wider. Dragging **downward** has no effect — the height stays fixed at 80px.

> **Think about this:** What happens if you remove `overflow: auto` from the code above? Try it and observe whether the resize handle appears.

---

### 1.4 — Example 2: Resize Height Only (`vertical`)

**The scenario:** A student registration form on a university site in Abuja wants to let users expand the "Additional Notes" box taller, but the width must stay aligned with the rest of the form.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      border: 2px solid #1a3c6e;   /* Dark blue border */
      padding: 15px;
      width: 350px;
      height: 80px;
      overflow: auto;
      resize: vertical;            /* Allow height resizing only */
      background-color: #f0f4ff;
      font-family: Arial, sans-serif;
    }
  </style>
</head>
<body>
  <h2>Student Registration – Additional Notes</h2>
  <div>Drag the bottom edge downward to make this box taller. The width stays the same.</div>
</body>
</html>
```

**Expected output in browser:**
A blue-bordered box appears. The user can drag the bottom handle **downward** to increase the height. The width stays locked at 350px no matter how the user drags.

---

### 1.5 — Example 3: Resize Both Width and Height (`both`)

**The scenario:** A general-purpose notes widget on a productivity app used by Nigerian professionals should allow full freedom — users can reshape it however they like.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      border: 2px solid #8b4513;   /* Brown border */
      padding: 15px;
      width: 300px;
      height: 100px;
      overflow: auto;
      resize: both;                /* Allow both width and height resizing */
      background-color: #fff8f0;
      font-family: Arial, sans-serif;
    }
  </style>
</head>
<body>
  <h2>My Notes (Drag to Resize)</h2>
  <div>You can drag this box to make it wider, taller, or both. Try it!</div>
</body>
</html>
```

**Expected output in browser:**
A brown-bordered box with a resize handle in the bottom-right corner. The user can drag in any direction — sideways, downward, or diagonally — to reshape the box freely.

---

### 1.6 — Example 4: Disable Resizing on a `<textarea>` (`none`)

This is one of the most commonly used applications of `resize`. By default, most browsers let users drag and resize a `<textarea>`. This can break carefully designed form layouts. The fix is simple:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Without this, users can resize the textarea in most browsers */
    textarea {
      width: 100%;
      height: 120px;
      padding: 10px;
      font-size: 14px;
      border: 2px solid #999;
      resize: none;                /* Disable all resizing */
      font-family: Arial, sans-serif;
    }
  </style>
</head>
<body>
  <h2>Leave a Comment</h2>
  <textarea placeholder="Write your thoughts about the Jollof Rice festival here..."></textarea>
</body>
</html>
```

**Expected output in browser:**
A text area appears where the user can type freely. However, the resize handle in the bottom-right corner is gone — the box stays exactly the same size no matter what.

> **Real-world use:** Every professional contact form or feedback form you see on major Nigerian websites — from banks to e-commerce platforms — disables textarea resizing to keep the layout neat.

---

### 1.7 — Second Example of `resize: none` — Confirming the Concept

Let us see the same idea applied to a `<div>` so you understand that this is not textarea-specific:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .fixed-box {
      width: 280px;
      height: 100px;
      border: 2px dashed tomato;
      padding: 10px;
      overflow: auto;
      resize: none;                /* No resizing allowed */
      background-color: #fff5f5;
    }
  </style>
</head>
<body>
  <h2>Fixed Announcement Box</h2>
  <div class="fixed-box">
    This box is locked in size. Users cannot resize it. Perfect for fixed-size widgets like announcement panels.
  </div>
</body>
</html>
```

**Expected output in browser:**
A dashed red-bordered box with no resize handle visible at all. The size is completely locked.

---

## Part 2: The `outline-offset` Property

### 2.1 — What Is It and Why Does It Exist?

You already know what an `outline` is — a line drawn *outside* an element's border. But by default, that outline sits right up against the element, touching its edge.

`outline-offset` lets you push that outline *away* from the element — creating a visible gap or breathing room between the element's edge and its outline ring.

**A simple analogy:** Imagine a framed painting on a wall in a Lagos art gallery. The frame itself is the outline. Now imagine the gallery puts a small gap of space between the painting's edge and the frame — the painting floats inside the frame rather than pressing against it. That floating space is the `outline-offset`.

**Why does this matter?**

- Creates elegant focus rings on form inputs and buttons
- Makes interactive elements visually distinct without using a border
- Gives your UI a modern, polished feel
- Improves accessibility — clearly shows which element has keyboard focus

---

### 2.2 — Syntax and How It Works

```css
selector {
  outline: [width] [style] [color];
  outline-offset: [distance];
}
```

The `outline-offset` value is a **length** — you can use `px`, `em`, or `rem`. It can even be **negative** (which pulls the outline *inside* the element).

Positive value → outline moves *away* from the element (outward gap)
Negative value → outline moves *into* the element (inside the element's boundary)

---

### 2.3 — Example 1: Basic `outline-offset` on a `<div>`

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    div {
      width: 250px;
      padding: 20px;
      margin: 40px;             /* Room for the outline to be visible */
      background-color: #e8f4e8;
      border: 2px solid #2c7a2c;
      outline: 3px solid red;   /* The outline itself */
      outline-offset: 10px;     /* Push outline 10px away from the border */
      font-family: Arial, sans-serif;
    }
  </style>
</head>
<body>
  <h2>Outline Offset Demo</h2>
  <div>This box has a red outline floating 10px outside its green border.</div>
</body>
</html>
```

**Expected output in browser:**
A green-bordered box with a red outline ring. The red ring floats 10 pixels away from the green border — there is a visible gap of white/transparent space between them. The outline does not touch the box.

> **Notice:** The `margin: 40px` gives the outline room to be fully visible. If the margin were zero, the outline could be clipped by the edge of the screen.

---

### 2.4 — Example 2: `outline-offset` on a Focused Input (Real-World Use)

The most practical use of `outline-offset` is on form elements when they receive focus (when the user clicks or tabs into them).

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    input {
      width: 280px;
      padding: 10px 14px;
      font-size: 15px;
      border: 2px solid #aaa;
      border-radius: 6px;
      outline: none;              /* Remove default browser outline */
    }

    /* When the user clicks or tabs into the input */
    input:focus {
      border-color: #1a5c9e;
      outline: 3px solid #5b9bd5;  /* Blue glow outline */
      outline-offset: 4px;         /* Float 4px from the border */
    }
  </style>
</head>
<body>
  <h2>Student Login – University of Lagos</h2>
  <p>Click inside the field below and observe the outline:</p>
  <input type="text" placeholder="Enter your matric number">
</body>
</html>
```

**Expected output in browser:**
An input field appears. When the user clicks inside it, a blue outline ring appears, floating 4 pixels outside the input's border — a clean "halo" effect. This is a common pattern in modern, accessible web forms.

> **Thinking prompt:** What happens if you change `outline-offset: 4px` to `outline-offset: 0px`? What about `outline-offset: -4px`?

---

### 2.5 — Example 3: Negative `outline-offset`

A negative value pulls the outline *inside* the element, which creates a completely different visual effect — useful for decorative inset rings.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .card {
      width: 280px;
      padding: 30px 20px;
      margin: 20px;
      background-color: #1a3c6e;
      color: white;
      text-align: center;
      outline: 3px dashed #f0c040;  /* Gold dashed outline */
      outline-offset: -12px;        /* Pull outline INSIDE the element */
      font-family: Arial, sans-serif;
      font-size: 18px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <h2>Award Certificate Preview</h2>
  <div class="card">
    Chidinma Okafor<br>
    Best Student — Computer Science 2024
  </div>
</body>
</html>
```

**Expected output in browser:**
A dark blue card with white text. A gold dashed ring appears *inside* the card (inset), creating a decorative border frame effect. This is a common trick for certificate designs, VIP cards, and styled announcement panels.

---

### 2.6 — Second Example of `outline-offset` — Confirming the Concept

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    button {
      padding: 12px 28px;
      font-size: 16px;
      background-color: #008000;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      outline: none;
    }

    button:focus {
      outline: 3px solid #90ee90;  /* Light green focus ring */
      outline-offset: 6px;         /* Float 6px away from button edge */
    }
  </style>
</head>
<body>
  <h2>Submit Application</h2>
  <p>Press Tab to focus the button and see the outline:</p>
  <button>Submit</button>
</body>
</html>
```

**Expected output in browser:**
A green button. When keyboard-focused (Tab key), a light green outline ring appears, floating 6 pixels away from the button's edges on all sides — a modern, accessible focus indicator.

---

## Part 3: Using Both Properties Together

### 3.1 — Combined Example: A Nigerian Contact Form

Let us now combine `resize` and `outline-offset` in a realistic scenario — a styled contact form for a Lagos-based tech company.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 500px;
      margin: 30px auto;
      padding: 20px;
    }

    h2 {
      color: #1a3c6e;
    }

    label {
      display: block;
      margin-top: 16px;
      font-weight: bold;
      color: #333;
    }

    input, textarea {
      width: 100%;
      padding: 10px;
      margin-top: 6px;
      border: 2px solid #aaa;
      border-radius: 5px;
      font-size: 14px;
      box-sizing: border-box;
      outline: none;               /* Remove browser default outline */
    }

    /* Custom focus style using outline-offset */
    input:focus, textarea:focus {
      border-color: #2c7a2c;
      outline: 3px solid #90ee90;
      outline-offset: 3px;
    }

    /* The message textarea can only be resized vertically */
    textarea {
      height: 120px;
      resize: vertical;            /* Let users make it taller only */
    }

    button {
      margin-top: 20px;
      width: 100%;
      padding: 12px;
      background-color: #1a3c6e;
      color: white;
      border: none;
      border-radius: 5px;
      font-size: 16px;
      cursor: pointer;
      outline: none;
    }

    button:focus {
      outline: 3px solid #5b9bd5;
      outline-offset: 4px;
    }
  </style>
</head>
<body>
  <h2>Contact Eko Digital Solutions</h2>
  <p>Located in Victoria Island, Lagos. Fill the form below:</p>

  <label>Full Name</label>
  <input type="text" placeholder="e.g. Adaeze Nwosu">

  <label>Email Address</label>
  <input type="email" placeholder="e.g. adaeze@example.com">

  <label>Your Message</label>
  <textarea placeholder="Type your message here. Drag the bottom edge to expand this area..."></textarea>

  <button>Send Message</button>
</body>
</html>
```

**Expected output in browser:**
A clean, styled contact form. Each field shows a green outline ring floating 3px away from its border when clicked. The textarea can be dragged taller but not wider. The button shows a blue floating outline when tab-focused. The form looks polished and professional.

---

## Part 4: Guided Practice Exercises

### Exercise 1 — Resize a Product Description Box

**Objective:** Create a product listing box where users can resize it in both directions.

**Scenario:** You are building a product page for an online supermarket selling Nigerian food items. Each product has a description box that users can reshape as they prefer.

**Steps:**
1. Create an HTML file
2. Add a `<div>` with a class of `product-box`
3. Give it a width of `320px`, height of `100px`, padding of `15px`, and a border
4. Set `overflow: auto` and `resize: both`
5. Place the text "Indomie Noodles – Chicken Flavour. A quick and tasty meal ready in 3 minutes. Available in cartons of 40 packs." inside the div
6. Add a heading above the box

**Full Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .product-box {
      width: 320px;
      height: 100px;
      padding: 15px;
      border: 2px solid #cc6600;
      background-color: #fff9f0;
      overflow: auto;
      resize: both;
      font-family: Arial, sans-serif;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <h2>Naija Supermart – Product Details</h2>
  <div class="product-box">
    Indomie Noodles – Chicken Flavour. A quick and tasty meal ready in 3 minutes. Available in cartons of 40 packs.
  </div>
</body>
</html>
```

**Expected output in browser:**
A small orange-bordered box with product text. Users can grab the bottom-right corner and drag it in any direction to resize the box.

**Self-check questions:**
- Does the resize handle appear in the bottom-right corner of the box?
- What happens to the text when you make the box very small?
- Does `overflow: auto` show a scrollbar when the content is bigger than the box?

---

### Exercise 2 — Fixed Feedback Form with Offset Outline

**Objective:** Build a feedback form where the textarea cannot be resized (to protect layout), and focused fields show a floating outline.

**Scenario:** A bank in Abuja wants a clean feedback form. The textarea must not be resizable. Focused fields must show a clear but elegant blue outline ring floating 5px away.

**Steps:**
1. Create an HTML file with a form structure
2. Add an `<input>` for name and a `<textarea>` for comments
3. Apply `resize: none` to the textarea
4. Apply `outline: 3px solid #1a5c9e` and `outline-offset: 5px` to the `:focus` state of both elements
5. Remove default browser outline on the elements themselves

**Full Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 420px;
      margin: 30px auto;
    }

    label {
      display: block;
      margin-top: 14px;
      font-weight: bold;
    }

    input, textarea {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: 2px solid #ccc;
      font-size: 14px;
      box-sizing: border-box;
      outline: none;
    }

    input:focus, textarea:focus {
      border-color: #1a5c9e;
      outline: 3px solid #1a5c9e;
      outline-offset: 5px;
    }

    textarea {
      height: 130px;
      resize: none;     /* Prevent user from resizing */
    }
  </style>
</head>
<body>
  <h2>First Bank of Nigeria – Customer Feedback</h2>
  <label>Your Name</label>
  <input type="text" placeholder="e.g. Emeka Eze">
  <label>Your Feedback</label>
  <textarea placeholder="Tell us about your recent banking experience..."></textarea>
</body>
</html>
```

**Expected output in browser:**
A two-field form. When either field is clicked, a dark blue outline ring appears floating 5px outside the field border. The textarea has no resize handle — it is completely fixed in size.

---

### Exercise 3 — Award Certificate with Negative Outline Offset

**Objective:** Style a certificate card using a negative `outline-offset` to create an inset decorative ring.

**Scenario:** The Computer Science Department of a Nigerian university wants a simple digital certificate preview card.

**Steps:**
1. Create a `<div>` with class `certificate`
2. Give it a dark background, white text, and generous padding
3. Add an outline with a **negative** offset to create an inset ring effect
4. Include recipient name, achievement, and institution

**Full Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .certificate {
      width: 380px;
      padding: 50px 30px;
      margin: 40px auto;
      background-color: #1a3c6e;
      color: white;
      text-align: center;
      font-family: Georgia, serif;
      outline: 4px solid gold;
      outline-offset: -18px;      /* Inset decorative ring */
    }

    .certificate h1 {
      font-size: 22px;
      margin-bottom: 10px;
      letter-spacing: 2px;
    }

    .certificate p {
      font-size: 15px;
      line-height: 1.8;
    }

    .certificate .name {
      font-size: 26px;
      font-weight: bold;
      color: gold;
      margin: 12px 0;
    }
  </style>
</head>
<body>
  <div class="certificate">
    <h1>CERTIFICATE OF EXCELLENCE</h1>
    <p>This is to certify that</p>
    <div class="name">Funmilayo Adeyemi</div>
    <p>has successfully completed the<br>
    <strong>Web Development Bootcamp 2024</strong><br>
    at the University of Ibadan,<br>
    Department of Computer Science.</p>
  </div>
</body>
</html>
```

**Expected output in browser:**
A dark blue certificate card with white and gold text. A gold outline ring appears *inside* the card boundary, creating an elegant decorative inner frame effect. The text is centred within the ring.

---

## Part 5: Code Challenges

These challenges are adapted from the W3Schools CSS User Interface challenge set. Try each one on your own before checking the solution.

---

### Challenge 1

**Task:** Make a `<div>` element resizable only in the **horizontal** (width) direction.

```html
<!-- Starting code -->
<style>
  div {
    border: 2px solid black;
    padding: 15px;
    width: 300px;
    overflow: auto;
    /* Add your resize property here */
  }
</style>
<div>Resize me horizontally!</div>
```

**Solution:**

```html
<style>
  div {
    border: 2px solid black;
    padding: 15px;
    width: 300px;
    overflow: auto;
    resize: horizontal;
  }
</style>
<div>Resize me horizontally!</div>
```

---

### Challenge 2

**Task:** Disable resizing on the `<textarea>` element below.

```html
<!-- Starting code -->
<style>
  textarea {
    width: 100%;
    height: 100px;
    /* Add your resize property here */
  }
</style>
<textarea>This textarea should not be resizable.</textarea>
```

**Solution:**

```html
<style>
  textarea {
    width: 100%;
    height: 100px;
    resize: none;
  }
</style>
<textarea>This textarea should not be resizable.</textarea>
```

---

### Challenge 3

**Task:** Give the `<div>` below an outline that is offset **15px** from the element's edge.

```html
<!-- Starting code -->
<style>
  div {
    border: 2px solid black;
    padding: 20px;
    width: 250px;
    margin: 30px;
    outline: 4px dashed red;
    /* Add your outline-offset property here */
  }
</style>
<div>I should have a floating outline!</div>
```

**Solution:**

```html
<style>
  div {
    border: 2px solid black;
    padding: 20px;
    width: 250px;
    margin: 30px;
    outline: 4px dashed red;
    outline-offset: 15px;
  }
</style>
<div>I should have a floating outline!</div>
```

---

### Challenge 4

**Task:** Make a button that shows a floating green outline ring (3px solid, offset 8px) when it is focused.

```html
<!-- Starting code -->
<style>
  button {
    padding: 10px 24px;
    font-size: 15px;
    cursor: pointer;
    outline: none;
    /* Add focus styles below */
  }
</style>
<button>Click or Tab to me</button>
```

**Solution:**

```html
<style>
  button {
    padding: 10px 24px;
    font-size: 15px;
    cursor: pointer;
    outline: none;
  }

  button:focus {
    outline: 3px solid green;
    outline-offset: 8px;
  }
</style>
<button>Click or Tab to me</button>
```

---

## Part 6: Mini Project — Styled Application Form

**Project name:** Eko Tech Academy — Course Application Form

**Goal:** Build a complete, styled application form that uses both `resize` and `outline-offset` together to create a polished, professional result.

---

### Stage 1: Setup — Page and Form Shell

Create the HTML structure and basic styling.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #f5f7fa;
      margin: 0;
      padding: 30px;
    }

    .form-container {
      max-width: 520px;
      margin: 0 auto;
      background: white;
      border-radius: 8px;
      padding: 35px;
      box-shadow: 0 2px 12px rgba(0,0,0,0.1);
    }

    h2 {
      color: #1a3c6e;
      margin-bottom: 5px;
    }

    .subtitle {
      color: #666;
      margin-bottom: 24px;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <div class="form-container">
    <h2>Eko Tech Academy</h2>
    <p class="subtitle">Course Application Form – Lagos Campus</p>
    <!-- Form fields will go here in next stages -->
  </div>
</body>
</html>
```

**Milestone 1 output:** A clean white card with a shadow appears in the centre of a light grey page, with the academy name and subtitle.

---

### Stage 2: Add the Form Fields

Now add the input fields and textarea.

```html
<!-- Add inside .form-container after the subtitle paragraph -->

<label style="display:block; font-weight:bold; margin-bottom:5px;">Full Name</label>
<input type="text" class="field" placeholder="e.g. Tunde Bakare">

<label style="display:block; font-weight:bold; margin-top:16px; margin-bottom:5px;">Email Address</label>
<input type="email" class="field" placeholder="e.g. tunde@gmail.com">

<label style="display:block; font-weight:bold; margin-top:16px; margin-bottom:5px;">Course of Interest</label>
<input type="text" class="field" placeholder="e.g. Full-Stack Web Development">

<label style="display:block; font-weight:bold; margin-top:16px; margin-bottom:5px;">Why Do You Want to Join?</label>
<textarea class="field message-field" placeholder="Tell us about your goals and background..."></textarea>

<button class="submit-btn">Submit Application</button>
```

**Add this CSS for the fields:**

```css
.field {
  width: 100%;
  padding: 11px 14px;
  margin-bottom: 4px;
  font-size: 14px;
  border: 2px solid #ccc;
  border-radius: 5px;
  outline: none;
  transition: border-color 0.2s;
}

.field:focus {
  border-color: #1a3c6e;
  outline: 3px solid #5b9bd5;
  outline-offset: 4px;
}

.message-field {
  height: 140px;
  resize: vertical;    /* Users can expand the message area downward */
}

.submit-btn {
  margin-top: 22px;
  width: 100%;
  padding: 13px;
  background-color: #1a3c6e;
  color: white;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  outline: none;
}

.submit-btn:focus,
.submit-btn:hover {
  background-color: #2c5fa5;
  outline: 3px solid #5b9bd5;
  outline-offset: 4px;
}
```

**Milestone 2 output:** All four fields and the submit button appear. Clicking any field shows a blue outline floating 4px outside the field border. The message textarea can be dragged taller.

---

### Stage 3: Complete the Full Project File

Here is the complete, combined project code:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    * { box-sizing: border-box; }

    body {
      font-family: Arial, sans-serif;
      background-color: #f5f7fa;
      margin: 0;
      padding: 30px;
    }

    .form-container {
      max-width: 520px;
      margin: 0 auto;
      background: white;
      border-radius: 8px;
      padding: 35px;
      box-shadow: 0 2px 12px rgba(0,0,0,0.1);
    }

    h2 { color: #1a3c6e; margin-bottom: 5px; }

    .subtitle {
      color: #666;
      margin-bottom: 24px;
      font-size: 14px;
    }

    label {
      display: block;
      font-weight: bold;
      margin-top: 16px;
      margin-bottom: 5px;
      color: #333;
    }

    .field {
      width: 100%;
      padding: 11px 14px;
      font-size: 14px;
      border: 2px solid #ccc;
      border-radius: 5px;
      outline: none;
      transition: border-color 0.2s;
    }

    .field:focus {
      border-color: #1a3c6e;
      outline: 3px solid #5b9bd5;
      outline-offset: 4px;
    }

    .message-field {
      height: 140px;
      resize: vertical;
    }

    .submit-btn {
      margin-top: 22px;
      width: 100%;
      padding: 13px;
      background-color: #1a3c6e;
      color: white;
      border: none;
      border-radius: 5px;
      font-size: 16px;
      cursor: pointer;
      outline: none;
    }

    .submit-btn:focus,
    .submit-btn:hover {
      background-color: #2c5fa5;
      outline: 3px solid #5b9bd5;
      outline-offset: 4px;
    }
  </style>
</head>
<body>
  <div class="form-container">
    <h2>Eko Tech Academy</h2>
    <p class="subtitle">Course Application Form – Lagos Campus</p>

    <label>Full Name</label>
    <input type="text" class="field" placeholder="e.g. Tunde Bakare">

    <label>Email Address</label>
    <input type="email" class="field" placeholder="e.g. tunde@gmail.com">

    <label>Course of Interest</label>
    <input type="text" class="field" placeholder="e.g. Full-Stack Web Development">

    <label>Why Do You Want to Join?</label>
    <textarea class="field message-field"
      placeholder="Tell us about your goals and background..."></textarea>

    <button class="submit-btn">Submit Application</button>
  </div>
</body>
</html>
```

**Final milestone output:** A professional-looking application form. All inputs show a floating blue focus ring. The textarea can be made taller (but not wider). The submit button highlights on hover and focus. The entire form looks ready to ship on a real website.

---

### Optional Extensions

Try these enhancements to push your skills further:
- Add `resize: none` to the textarea and observe the difference in user experience — when is it better to disable resizing?
- Change `outline-offset` from `4px` to `10px` on the focused fields and observe how it affects the visual weight of the form
- Use a **negative** `outline-offset` on the form container card to add a decorative inset ring

---

## Common Beginner Mistakes

### Mistake 1 — Using `resize` Without `overflow`

**Wrong:**
```css
div {
  resize: both;
  /* Missing overflow! */
}
```

**Why it fails:** On most elements (not textarea), the browser ignores `resize` unless `overflow` is set to something other than `visible`.

**Correct:**
```css
div {
  resize: both;
  overflow: auto;  /* This activates the resize handle */
}
```

---

### Mistake 2 — Forgetting `margin` When Using `outline-offset`

**Wrong:**
```css
div {
  outline: 3px solid red;
  outline-offset: 15px;
  margin: 0;  /* The outline may be clipped at the screen edge */
}
```

**Why it fails:** The outline floats *outside* the element. If there is no margin, the outer part of the outline may be clipped by the screen or the parent container edge.

**Correct:**
```css
div {
  outline: 3px solid red;
  outline-offset: 15px;
  margin: 25px;   /* Give the floating outline room to breathe */
}
```

---

### Mistake 3 — Thinking `outline-offset` Changes the Element's Size

**Misconception:** "If I add `outline-offset: 20px`, will it push the other elements on the page further apart?"

**Reality:** No. Outlines — including their offsets — never affect the page layout or push other elements around. Only `border`, `margin`, and `padding` affect layout. An outline with an offset floats visually but takes up zero layout space.

---

### Mistake 4 — Applying `resize` to Inline Elements

**Wrong:**
```css
span {
  resize: both;
  overflow: auto;
}
```

**Why it fails:** `resize` only works on **block-level** elements and replaced elements (like `<textarea>`). A `<span>` is inline — it has no resizable dimensions by default.

**Correct:**
```css
span {
  display: block;  /* Convert to block first */
  resize: both;
  overflow: auto;
}
```

---

### Mistake 5 — Removing Browser Outline Without Providing a Replacement

**Wrong:**
```css
input:focus {
  outline: none;  /* User now has NO visual focus indicator */
}
```

**Why it fails:** This is an **accessibility problem**. Users navigating by keyboard (or users with visual needs) rely on the focus ring to know which element is active. Removing it without replacing it is harmful.

**Correct:**
```css
input:focus {
  outline: none;                      /* Remove browser default */
  border-color: green;                /* Add your own custom focus style */
  box-shadow: 0 0 0 3px lightgreen;   /* Or use box-shadow as a ring */
}
```

Or better still, use `outline-offset` to keep a ring but style it beautifully:

```css
input:focus {
  outline: 3px solid green;
  outline-offset: 3px;
}
```

---

## Reflection Questions

1. You are building a form for a Nigerian food delivery app. The comment/special instructions field is often used extensively by customers. Should you use `resize: vertical`, `resize: horizontal`, `resize: both`, or `resize: none`? Explain your choice.

2. A designer asks you to put a gold outline ring floating 12px outside a product card. Which two properties do you need? Write the CSS.

3. A teammate removes `outline: none` from all input fields without adding any replacement focus style. What problem does this create? Who is most affected?

4. What is the difference between `border` and `outline` in CSS? Name at least two differences.

5. If `outline-offset` is set to a **negative** value, where does the outline appear? Describe what you would see and suggest one creative use case.

6. Why must you include `overflow: auto` when using `resize` on a `<div>` but not necessarily on a `<textarea>`?

---

## Completion Checklist

Before moving on, confirm that you can do all of the following:

- [ ] I can explain what the `resize` property does in simple language
- [ ] I know the four values of `resize`: `horizontal`, `vertical`, `both`, `none`
- [ ] I understand that `overflow: auto` is required alongside `resize` on most elements
- [ ] I can disable textarea resizing using `resize: none`
- [ ] I can explain what `outline-offset` does and how it differs from `border`
- [ ] I know that a positive `outline-offset` pushes the outline outward
- [ ] I know that a negative `outline-offset` pulls the outline inward
- [ ] I understand that outlines and their offsets do not affect page layout
- [ ] I can apply `outline-offset` on `:focus` states for accessible form design
- [ ] I completed all exercises and the mini project
- [ ] I understand why removing `outline: none` without a replacement is an accessibility issue

---

## Lesson Summary

In this lesson, you learned two CSS User Interface properties that directly control how users interact with and visually perceive your web elements.

**`resize`** gives users the ability to manually drag and resize an element. You control the direction — horizontal only, vertical only, both, or none at all. The most practical application is enabling vertical resizing on message textareas in contact forms, while disabling it on layout-sensitive forms where a fixed textarea size is needed. Remember to always include `overflow: auto` when applying `resize` to block elements.

**`outline-offset`** controls the spacing between an element and its outline. A positive value floats the outline outward — commonly used for elegant, accessible focus rings on buttons and inputs. A negative value pulls the outline inside the element — useful for decorative inset rings on cards and certificates. Unlike borders, outlines never affect page layout — they are purely visual.

Together, these two properties are building blocks of professional, accessible, and polished web UI design.

---

## Quick Reference Card

| Property | Values | Notes |
|---|---|---|
| `resize` | `horizontal` | Width only |
| `resize` | `vertical` | Height only |
| `resize` | `both` | Width and height |
| `resize` | `none` | No resizing |
| `resize` | Requires `overflow: auto` | On block elements |
| `outline-offset` | Positive `px` | Outline moves outward |
| `outline-offset` | Negative `px` | Outline moves inward |
| `outline-offset` | No layout effect | Purely visual |
| Best practice | `outline-offset` on `:focus` | Accessible focus rings |

---

*End of Lesson 64 — CSS User Interface*
