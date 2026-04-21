---
render_with_liquid: false
title: "CSS Form Styling — Inputs, Focus, Icons, and Form Elements"
nav_order: 36
---

# Lesson 36: CSS Form Styling — Inputs, Focus, Icons, and Form Elements

---

## Lesson Introduction

Every website you use — whether you are logging into your email, signing up for a service, placing an order, or filling in a contact form — uses **HTML forms** behind the scenes. But raw, unstyled HTML forms look plain, clunky, and unprofessional. That is where **CSS form styling** comes in.

In this lesson, you will learn how to take a basic HTML form and transform it into a polished, professional-looking interface that feels good to use. You will style text fields, dropdowns, buttons, checkboxes, labels, textareas, and more. You will learn how to give inputs a highlight when a user clicks on them (called **focus**), how to add little icons inside input fields, and how to style all the different pieces of a form to work together beautifully.

By the end of this lesson, you will have built a real, styled registration form from scratch — the kind you see on real websites every day.

---

## Prerequisite Concepts

Before we begin styling forms, let us make sure you understand the building blocks. If any of these feel unfamiliar, read each mini-explanation carefully before continuing.

### What is an HTML Form?

An **HTML form** is a section of a webpage that collects information from a user. Think of it like a paper questionnaire — it has blank spaces for you to fill in, options to choose from, and a button to submit your answers.

```html
<form>
  <label for="name">Your Name:</label>
  <input type="text" id="name" name="name">
  <button type="submit">Submit</button>
</form>
```

**Output (unstyled):** A plain text box with a label and a button — no colours, no spacing, no padding.

### What is `<input>`?

The `<input>` element is the most common form element. It can be many different things depending on its `type` attribute:

- `type="text"` → a text box for typing
- `type="password"` → a text box that hides characters
- `type="email"` → a text box for email addresses
- `type="submit"` → a clickable submit button
- `type="checkbox"` → a small square you can tick
- `type="radio"` → a small circle for selecting one option from many
- `type="file"` → a button for uploading a file

### What is `<label>`?

A `<label>` is the text description that tells the user what to type into an input. The `for` attribute of a `<label>` must match the `id` of the `<input>` it describes — this links them together.

```html
<label for="email">Email Address:</label>
<input type="email" id="email" name="email">
```

### What is `<select>` and `<option>`?

A `<select>` element creates a **dropdown menu**. Each `<option>` inside it is one choice in that dropdown.

```html
<select name="country">
  <option value="ng">Nigeria</option>
  <option value="gh">Ghana</option>
  <option value="za">South Africa</option>
</select>
```

### What is `<textarea>`?

A `<textarea>` is a bigger text area for typing multiple lines of text — like a message box or a comments section.

```html
<textarea name="message" rows="4" cols="40"></textarea>
```

### What CSS Properties Will We Use?

You will use many CSS properties throughout this lesson. Here is a quick preview of the most important ones:

| Property | What It Does |
|---|---|
| `width` | Controls how wide the input is |
| `padding` | Adds space inside the input box |
| `margin` | Adds space outside the input box |
| `border` | Adds a line around the input |
| `border-radius` | Rounds the corners of the box |
| `background-color` | Sets the fill colour of the input |
| `color` | Sets the text colour inside the input |
| `font-size` | Controls how big the text is |
| `outline` | The glow or ring that appears when focused |
| `box-sizing` | Controls how padding affects the total width |
| `position` | Allows you to place icons inside inputs |

---

## Part 1 — Conceptual Understanding: Why Style Forms at All?

Imagine you visit a website and the signup form looks like this: plain black-and-white boxes with no spacing, text crammed right to the edge, and a tiny submit button. You would probably leave immediately.

Now imagine the same form but with soft rounded corners, pleasant colours, breathing room (padding), and a glowing highlight when you click on a field. That feels much better — and you are more likely to trust it and fill it in.

**Good form design matters because:**
1. It builds trust with your users.
2. It guides users visually through the steps.
3. It reduces errors (clear labels, good sizing).
4. It makes your website look professional and polished.

CSS form styling is used in:
- Login and signup pages (every social media site)
- E-commerce checkout pages
- Contact and feedback forms
- Survey and quiz tools
- Job application forms
- Medical patient intake forms

---

## Part 2 — Styling Form Input Fields

### 2.1 The Key CSS Properties for Inputs

The most commonly styled CSS properties for input fields are `width`, `padding`, `margin`, `border`, `border-radius`, `background-color`, `color`, and `font-size`.

Let us start with the most basic example and build from there.

#### Simple Example 1: Bare input vs. styled input

**Without CSS (plain HTML):**

```html
<input type="text" placeholder="Type your name">
```

**Output:** A tiny, plain grey box — barely noticeable on the page.

**With basic CSS:**

```html
<style>
  input[type="text"] {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 16px;
  }
</style>

<input type="text" placeholder="Type your name">
```

**Output:** A wide, comfortably padded input box with a light grey border and rounded corners. Much more readable and clickable.

### Line-by-Line Explanation

Let us break down every single part of the CSS above:

```css
input[type="text"] {
```
This is an **attribute selector**. It means: "target only `<input>` elements that have `type="text"`." This is important because styling plain `input` would also affect buttons and checkboxes.

```css
  width: 100%;
```
Makes the input stretch to fill 100% of the width of its container. This means if the container is 400px wide, the input is 400px wide. Think of it like a rubber band that stretches to fit.

```css
  padding: 12px 20px;
```
Adds 12px of breathing room above and below the text, and 20px of breathing room on the left and right. Without padding, text would be jammed right against the edge of the box.

```css
  margin: 8px 0;
```
Adds 8px of space above and below the input (outside the box), so inputs don't stack directly on top of each other.

```css
  border: 1px solid #ccc;
```
Draws a thin (1px), solid, light grey (`#ccc`) border around the input box.

```css
  border-radius: 4px;
```
Gently rounds the four corners of the input. The higher the value, the more rounded. `4px` gives a subtle but modern look.

```css
  font-size: 16px;
```
Sets the text inside the input to 16px. This is important — many browsers default to a small font that can be hard to read.

> 💡 **Tip:** Always set a font-size on inputs. Browsers often display text inside inputs in a different, smaller size than your page text unless you set it explicitly.

---

### 2.2 The `box-sizing` Property — A Critical Detail

Here is a common beginner confusion. Look at this:

```css
input {
  width: 100%;
  padding: 12px 20px;
  border: 1px solid #ccc;
}
```

You might expect the input to be exactly 100% wide. But actually, it would overflow! Why? Because by default, CSS calculates width **without** including padding and border. So:

- Your `width: 100%` means the inner content area is 100% wide.
- Then padding (20px left + 20px right = 40px) and border (1px + 1px = 2px) are **added on top**.
- Total actual width = 100% + 42px. That overflows!

**The fix: `box-sizing: border-box`**

```css
input {
  box-sizing: border-box; /* Now padding and border are included INSIDE the width */
  width: 100%;
  padding: 12px 20px;
  border: 1px solid #ccc;
}
```

**Output:** The input is now exactly 100% wide — the padding and border are absorbed into that 100%, not added on top. Think of it like packing things inside a box: `border-box` means the lid still fits, no overflow.

> 💡 **Best practice:** Many developers put `box-sizing: border-box` on every element at the top of their CSS to avoid this confusion:
> ```css
> * {
>   box-sizing: border-box;
> }
> ```

---

### 2.3 Styling Specific Input Types

You do not have to style all inputs the same way. You can target each type specifically.

#### Example: Different styles for text and password inputs

```html
<style>
  input[type="text"],
  input[type="email"],
  input[type="password"] {
    width: 100%;
    padding: 10px 15px;
    margin-bottom: 12px;
    border: 2px solid #ddd;
    border-radius: 6px;
    font-size: 15px;
    background-color: #f9f9f9;
    color: #333;
  }

  input[type="submit"] {
    width: 100%;
    padding: 12px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 6px;
    font-size: 16px;
    cursor: pointer;
  }
</style>

<input type="text" placeholder="Full Name">
<input type="email" placeholder="Email Address">
<input type="password" placeholder="Password">
<input type="submit" value="Create Account">
```

**Output:**
- Text, email, and password fields: wide, padded, light grey background, dark text, rounded.
- Submit button: full-width, green background, white text — clearly a button.

**What `cursor: pointer` does:** When the user hovers over the submit button, the mouse cursor changes to a hand (pointing finger), signalling it is clickable. Without this, the cursor stays as an arrow, which feels wrong on a button.

> 🤔 **Thinking Prompt:** What would happen if you removed `background-color: #f9f9f9` from the inputs? Try picturing it — the background would revert to the browser's default (usually white or light grey). The form would still work, but it would feel less custom.

---

### 2.4 Styling `<select>` Dropdowns

Select elements are often tricky because they look very different across browsers by default. You can bring them under control with CSS.

```html
<style>
  select {
    width: 100%;
    padding: 10px 15px;
    border: 2px solid #ddd;
    border-radius: 6px;
    font-size: 15px;
    background-color: #f9f9f9;
    color: #333;
    appearance: none; /* Removes default browser arrow styling */
  }
</style>

<select name="country">
  <option>Nigeria</option>
  <option>Ghana</option>
  <option>South Africa</option>
</select>
```

**Output:** A clean dropdown that matches your other input fields, with consistent padding, border, and colours.

**What `appearance: none` does:** By default, every browser adds its own style to `<select>` elements — custom arrows, backgrounds, colours. `appearance: none` strips all of that away, giving you a clean slate to style from scratch.

---

### 2.5 Styling `<textarea>` (Multi-line Input)

A textarea is like a bigger version of a text input. It should be styled consistently with your other inputs.

```html
<style>
  textarea {
    width: 100%;
    padding: 12px 15px;
    border: 2px solid #ddd;
    border-radius: 6px;
    font-size: 15px;
    resize: vertical; /* Only allows resizing up and down, not sideways */
    font-family: inherit; /* Matches the font of the rest of the page */
  }
</style>

<textarea rows="5" placeholder="Write your message here..."></textarea>
```

**Output:** A multi-line input box that matches your other fields and can only be resized vertically.

**What `resize: vertical` does:** By default, textareas can be resized by the user in any direction — up, down, left, right. This can break your layout. `resize: vertical` restricts resizing to up and down only, which is almost always what you want.

**What `font-family: inherit` does:** Inputs and textareas have their own default font (often a system monospace font). `inherit` means "use the same font as the rest of the page." This makes everything look consistent.

---

## Part 3 — Styling Labels

Labels are just as important as inputs! If labels look bad, the whole form suffers.

```html
<style>
  label {
    display: block;          /* Makes label take its own line */
    margin-bottom: 5px;      /* Space between label and input */
    font-weight: bold;        /* Makes the label text bold */
    font-size: 14px;
    color: #333;
  }
</style>

<label for="name">Full Name</label>
<input type="text" id="name" name="name" placeholder="e.g. Amara Okafor">
```

**Output:** A bold, dark label sits on its own line above the input.

**Why `display: block`?** By default, `<label>` is an inline element — it sits on the same line as the input. `display: block` forces it onto its own line, stacking the label above the input. This is the most common form layout.

> 💡 **Tip:** Always pair a label's `for` attribute with the input's `id`. This is not just good practice — it makes the label clickable! Clicking the label automatically focuses (activates) the input. This greatly improves accessibility.

---

## Part 4 — The `:focus` Pseudo-Class: Highlighting Active Inputs

### What is Focus?

When you click on an input field to start typing, that field is said to have **focus**. It is the active element. By default, browsers show a basic blue ring around focused elements.

The `:focus` pseudo-class lets you completely control what happens when a user clicks on (focuses) an input.

**Why does focus styling matter?**
- It tells the user: "this is the field you are currently typing in"
- It improves accessibility for keyboard navigation
- It makes forms feel polished and interactive

Think of it like a spotlight: when an actor steps into the spotlight on stage, the audience knows exactly where to look. Focus styling is your spotlight.

### Simple Example: Blue glow on focus

```html
<style>
  input[type="text"] {
    width: 100%;
    padding: 10px 15px;
    border: 2px solid #ccc;
    border-radius: 6px;
    font-size: 15px;
    transition: border-color 0.3s ease; /* Smooth colour change */
  }

  input[type="text"]:focus {
    border-color: #4a90e2;
    outline: none;
  }
</style>

<input type="text" placeholder="Click me to see focus styling">
```

**Output (before clicking):** A plain input with a light grey border.
**Output (after clicking):** The border turns blue — the input glows visually to show it is active.

### Line-by-Line Explanation

```css
input[type="text"]:focus {
```
The `:focus` pseudo-class. This CSS only applies **when the input is currently active** (clicked or tabbed into). At all other times, it is ignored.

```css
  border-color: #4a90e2;
```
Changes the border colour from light grey to a pleasant blue. This is the "glow" effect — the border colour switches when focused.

```css
  outline: none;
```
This removes the default browser focus ring (the blue ring that browsers add automatically). We remove it because we are replacing it with our own, better-looking border colour change. 

> ⚠️ **Important Warning:** Never use `outline: none` without providing your own visible focus indicator! If you remove the default focus ring and add nothing back, users who navigate by keyboard (including people with disabilities) will have no idea which element is active. Always replace the outline with something visible — a changed border colour, a box shadow, or a different background.

### Example: Using `box-shadow` for a glowing ring

```html
<style>
  input[type="text"]:focus {
    border-color: #4a90e2;
    outline: none;
    box-shadow: 0 0 8px rgba(74, 144, 226, 0.6);
  }
</style>
```

**Output:** When clicked, the input gets a soft blue glowing ring around it, like a soft halo. This is a very popular modern design technique.

**Breaking down `box-shadow: 0 0 8px rgba(74, 144, 226, 0.6)`:**
- `0` → no horizontal shadow offset
- `0` → no vertical shadow offset
- `8px` → how spread/blurry the shadow is
- `rgba(74, 144, 226, 0.6)` → blue colour at 60% opacity (the glow colour)

### The `transition` Property for Smooth Animations

Notice the `transition: border-color 0.3s ease` in the base style. This is what makes the colour change feel smooth instead of instant.

```css
transition: border-color 0.3s ease;
```

- `border-color` → which property to animate (the border colour)
- `0.3s` → how long the animation takes (0.3 seconds — fast but visible)
- `ease` → starts slowly, speeds up in the middle, slows at the end (natural feeling)

Without `transition`, the border would snap instantly from grey to blue. With it, it smoothly fades. Always add transitions to focus effects for a polished feel.

> 🤔 **Thinking Prompt:** What do you think would happen if you changed `0.3s` to `2s`? The colour change would take 2 full seconds — very slow and annoying. Transitions should be quick. 0.2s–0.4s is the sweet spot for form interactions.

---

## Part 5 — Adding Icons Inside Input Fields

A very popular modern UI pattern is adding small icons inside input fields — like a magnifying glass icon inside a search box, an envelope icon in an email field, or a lock icon in a password field. These make forms immediately recognisable and professional-looking.

### How Do Icons Inside Inputs Work?

HTML inputs cannot directly contain other elements like icons. Instead, the technique uses:
1. A wrapping `<div>` that is styled as `position: relative`
2. An icon element placed inside that `<div>` with `position: absolute`
3. The input is padded on the left to make room for the icon

Think of it like this: the wrapper is a picture frame. The input fills the frame. The icon is a sticker placed precisely on top of the frame corner using `position: absolute`.

### Example: Input with an icon using Font Awesome

First, you need a free icon library. Font Awesome is one of the most popular. To use it, include this line in your HTML `<head>`:

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
```

Now here is the full example:

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <style>
    .input-wrapper {
      position: relative;  /* Makes this the reference point for the icon */
      margin-bottom: 15px;
    }

    .input-wrapper i {
      position: absolute;   /* Positions icon relative to the wrapper */
      left: 12px;           /* 12px from the left edge */
      top: 50%;             /* Vertically centre */
      transform: translateY(-50%);  /* Fine-tune the vertical centring */
      color: #888;          /* Light grey icon colour */
    }

    .input-wrapper input {
      width: 100%;
      padding: 10px 10px 10px 40px; /* Extra left padding = space for icon */
      border: 2px solid #ddd;
      border-radius: 6px;
      font-size: 15px;
      box-sizing: border-box;
    }
  </style>
</head>
<body>

  <div class="input-wrapper">
    <i class="fa fa-envelope"></i>
    <input type="email" placeholder="Enter your email">
  </div>

  <div class="input-wrapper">
    <i class="fa fa-lock"></i>
    <input type="password" placeholder="Enter your password">
  </div>

</body>
</html>
```

**Output:** An email field with a small grey envelope icon inside the left side, and a password field with a grey lock icon. The text starts after the icon, keeping everything neat.

### Step-by-Step Breakdown

**Step 1 — The wrapper `<div>`:**
```html
<div class="input-wrapper">
```
This container holds both the icon and the input. It has `position: relative`, which is essential. Without it, `position: absolute` on the icon would not work correctly.

**Step 2 — The icon:**
```html
<i class="fa fa-envelope"></i>
```
Font Awesome uses `<i>` tags with class names like `fa fa-envelope` to display icons. The `fa` prefix tells Font Awesome to render the icon.

**Step 3 — Positioning the icon:**
```css
.input-wrapper i {
  position: absolute;
  left: 12px;
  top: 50%;
  transform: translateY(-50%);
}
```
- `position: absolute` → takes the icon out of normal flow, allows precise placement
- `left: 12px` → places icon 12px from the left edge of the wrapper
- `top: 50%` → moves icon 50% down from the top of the wrapper
- `transform: translateY(-50%)` → shifts it back up by half its own height, perfectly centring it vertically

**Step 4 — Making room for the icon:**
```css
padding: 10px 10px 10px 40px; /* Top Right Bottom Left */
```
The left padding is 40px — much larger than the other sides. This pushes the typed text to the right, starting after the icon. Without this, text would overlap the icon.

> 💡 **Tip:** Always make the left padding at least as wide as the icon plus a little gap. If your icon is 20px wide and you want 10px of space, use `40px` of left padding.

---

## Part 6 — Styling Other Form Elements

### 6.1 Styling `<button>` and Submit Inputs

Buttons are a critical part of any form. A well-styled button clearly signals "click here to complete the action."

```html
<style>
  button,
  input[type="submit"] {
    background-color: #4CAF50;   /* Green */
    color: white;
    padding: 14px 20px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 16px;
    width: 100%;
    transition: background-color 0.3s ease;
  }

  button:hover,
  input[type="submit"]:hover {
    background-color: #45a049;   /* Slightly darker green on hover */
  }
</style>

<button type="submit">Submit Form</button>
```

**Output:** A wide green button. When you hover over it, it darkens slightly — giving visual feedback that it's interactive.

**What `:hover` does:** This pseudo-class activates when the mouse hovers over the element. The background colour changes, giving the user a clear signal the button is clickable.

**Why `border: none`?** Buttons have a default browser border. Removing it gives you a clean, flat modern look.

### 6.2 Styling Checkboxes and Radio Buttons

Native checkboxes and radio buttons are very difficult to style with CSS alone because browsers control most of their appearance. However, you can make small adjustments, and for full custom styling, we often use a label trick.

**Basic sizing and cursor:**

```css
input[type="checkbox"],
input[type="radio"] {
  width: 16px;
  height: 16px;
  cursor: pointer;
  accent-color: #4CAF50;  /* Changes the tick/fill colour in modern browsers */
}
```

**Output:** Slightly larger checkboxes and radio buttons with a green tick/dot when checked.

**What `accent-color` does:** This modern CSS property (supported in all major browsers since 2022) lets you change the colour of form control accents — the tick in a checkbox, the dot in a radio button, the fill of a range slider. It is the easiest way to colour checkboxes without complex custom code.

### 6.3 Styling the Form Container

The form itself should be contained in a styled box to look polished.

```html
<style>
  .form-container {
    background-color: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);  /* Soft drop shadow */
    max-width: 500px;
    margin: 40px auto;  /* Centres the form on the page */
  }
</style>

<div class="form-container">
  <!-- Your form goes here -->
</div>
```

**Output:** A white card with rounded corners, a soft shadow, centred on the page with margins. This is the standard "card" form style used on most modern websites.

**Breaking down `box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1)`:**
- `0` → no horizontal shadow
- `4px` → shadow is 4px lower than the element (like light coming from above)
- `15px` → how blurry/spread the shadow is
- `rgba(0, 0, 0, 0.1)` → black at 10% opacity — very subtle shadow

### 6.4 Full Styled Form Container Example

Putting it all together:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      background-color: #f0f2f5;
      font-family: Arial, sans-serif;
    }

    .form-container {
      background-color: white;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
      max-width: 450px;
      margin: 40px auto;
    }

    h2 {
      text-align: center;
      margin-bottom: 20px;
      color: #333;
    }

    label {
      display: block;
      margin-bottom: 5px;
      font-weight: bold;
      font-size: 14px;
      color: #555;
    }

    input[type="text"],
    input[type="email"],
    input[type="password"],
    select,
    textarea {
      width: 100%;
      padding: 10px 15px;
      margin-bottom: 15px;
      border: 2px solid #ddd;
      border-radius: 6px;
      font-size: 15px;
      box-sizing: border-box;
      transition: border-color 0.3s ease;
    }

    input:focus,
    select:focus,
    textarea:focus {
      border-color: #4a90e2;
      outline: none;
    }

    input[type="submit"] {
      width: 100%;
      padding: 12px;
      background-color: #4a90e2;
      color: white;
      border: none;
      border-radius: 6px;
      font-size: 16px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    input[type="submit"]:hover {
      background-color: #357abd;
    }
  </style>
</head>
<body>

  <div class="form-container">
    <h2>Create Account</h2>

    <label for="fullname">Full Name</label>
    <input type="text" id="fullname" placeholder="e.g. Amara Okafor">

    <label for="email">Email Address</label>
    <input type="email" id="email" placeholder="e.g. amara@email.com">

    <label for="password">Password</label>
    <input type="password" id="password" placeholder="At least 8 characters">

    <label for="country">Country</label>
    <select id="country">
      <option>Nigeria</option>
      <option>Ghana</option>
      <option>Kenya</option>
      <option>South Africa</option>
    </select>

    <input type="submit" value="Create Account">
  </div>

</body>
</html>
```

**Expected Output:**
- A white card form, centred on a soft grey page background
- All inputs are wide, padded, with rounded corners and a soft grey border
- Clicking any input turns its border blue
- The submit button is blue and darkens when hovered

---

## Part 7 — Guided Practice Exercises

### Exercise 1: Style a Login Form

**Objective:** Create a fully styled login form with email, password, and submit button.

**Scenario:** You are building the login page for a student portal at a university.

**Steps:**

1. Create an HTML file called `login.html`
2. Add a `<div>` container with a `.form-box` class
3. Style `.form-box` with white background, padding, shadow, and max-width
4. Add a heading: "Student Portal Login"
5. Add `label` + `input[type="email"]` pair for email
6. Add `label` + `input[type="password"]` pair for password
7. Add `input[type="submit"]` styled as a button
8. Add `:focus` styling to inputs

**Hints:**
- Use `box-shadow: 0 4px 15px rgba(0,0,0,0.1)` for the card shadow
- Use `border-color` change on `:focus`
- Use `cursor: pointer` on the submit button

**Expected Output:** A clean, centred login card with polished inputs and a visible focus effect.

**Self-check Questions:**
- Does clicking the email field change the border colour?
- Is the submit button wide enough to feel clickable?
- Does the form sit in the centre of the page?

**Optional Challenge:** Add a "Forgot Password?" text link below the submit button styled in a lighter colour.

---

### Exercise 2: Style a Contact Form

**Objective:** Style a contact form with name, email, subject (dropdown), and message (textarea).

**Scenario:** You are styling the contact page for a small business website.

**Steps:**

1. Create a form with four fields: name (text), email (email), subject (select), message (textarea)
2. Style all fields consistently with the same border, padding, and font-size
3. Make the textarea have 5 rows and be `resize: vertical`
4. Add a green submit button
5. Add `:hover` and `:focus` states

**Expected Output:** A consistent four-field form where all elements look visually identical in style, only differing in shape (textarea is taller).

**Self-check Questions:**
- Does the select dropdown match the styling of the text inputs?
- Can the textarea only be resized vertically?
- Does the button change colour on hover?

---

## Part 8 — Mini Project: Professional Registration Form

In this project, you will build a complete registration form from scratch — the kind used on actual websites for account creation.

### Project Overview

**Goal:** Build a styled registration form for a fictional learning platform called **"LearnPath"**.

**Fields needed:**
- First Name and Last Name (side by side)
- Email Address (with envelope icon)
- Password (with lock icon)
- Confirm Password
- Country (dropdown)
- Course of Interest (dropdown)
- Short Bio (textarea)
- Terms of Service checkbox
- Submit button

### Stage 1 — Setup

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LearnPath Registration</title>
  <link rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <style>
    /* Reset and base */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: #eef2f7;
      font-family: 'Segoe UI', Arial, sans-serif;
      color: #333;
    }
  </style>
</head>
<body>
  <!-- Stage 2 content goes here -->
</body>
</html>
```

**Milestone Output:** A clean page with a grey background and no content yet.

### Stage 2 — Form Container

Add this CSS to your `<style>` block, and the container HTML to `<body>`:

```css
    /* Form card container */
    .register-card {
      max-width: 580px;
      margin: 40px auto;
      background-color: white;
      padding: 40px;
      border-radius: 12px;
      box-shadow: 0 6px 25px rgba(0, 0, 0, 0.1);
    }

    .register-card h1 {
      text-align: center;
      margin-bottom: 8px;
      color: #2c3e50;
      font-size: 26px;
    }

    .register-card p.subtitle {
      text-align: center;
      color: #777;
      margin-bottom: 28px;
      font-size: 14px;
    }
```

```html
<div class="register-card">
  <h1>Join LearnPath</h1>
  <p class="subtitle">Create your free account and start learning today</p>
  <!-- Form goes here in Stage 3 -->
</div>
```

**Milestone Output:** A white card appears centred on the grey page with the heading and subtitle.

### Stage 3 — Form Fields

Add all labels, inputs, select, and textarea:

```css
    /* Labels */
    label {
      display: block;
      font-size: 13px;
      font-weight: 600;
      color: #555;
      margin-bottom: 5px;
    }

    /* All standard inputs, select, and textarea */
    input[type="text"],
    input[type="email"],
    input[type="password"],
    select,
    textarea {
      width: 100%;
      padding: 11px 14px;
      border: 2px solid #ddd;
      border-radius: 8px;
      font-size: 15px;
      color: #333;
      background-color: #fafafa;
      transition: border-color 0.25s ease, box-shadow 0.25s ease;
      margin-bottom: 18px;
    }

    /* Focus state */
    input[type="text"]:focus,
    input[type="email"]:focus,
    input[type="password"]:focus,
    select:focus,
    textarea:focus {
      outline: none;
      border-color: #5b8dee;
      box-shadow: 0 0 0 3px rgba(91, 141, 238, 0.2);
      background-color: white;
    }

    /* Side-by-side name fields */
    .name-row {
      display: flex;
      gap: 15px;
    }

    .name-row > div {
      flex: 1;
    }

    /* Input with icon wrapper */
    .input-icon-wrapper {
      position: relative;
      margin-bottom: 18px;
    }

    .input-icon-wrapper i {
      position: absolute;
      left: 13px;
      top: 50%;
      transform: translateY(-50%);
      color: #aaa;
      font-size: 14px;
    }

    .input-icon-wrapper input {
      padding-left: 38px;
      margin-bottom: 0;
    }

    /* Textarea */
    textarea {
      resize: vertical;
      min-height: 100px;
      font-family: inherit;
    }

    /* Checkbox row */
    .checkbox-row {
      display: flex;
      align-items: center;
      gap: 10px;
      margin-bottom: 20px;
    }

    .checkbox-row input[type="checkbox"] {
      width: 18px;
      height: 18px;
      accent-color: #5b8dee;
      cursor: pointer;
    }

    .checkbox-row label {
      margin: 0;
      font-weight: normal;
      font-size: 14px;
    }

    /* Submit button */
    input[type="submit"] {
      width: 100%;
      padding: 14px;
      background-color: #5b8dee;
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      font-weight: 600;
      cursor: pointer;
      transition: background-color 0.3s ease, transform 0.1s ease;
    }

    input[type="submit"]:hover {
      background-color: #4a7de0;
    }

    input[type="submit"]:active {
      transform: scale(0.98);  /* Slight shrink when clicked */
    }
```

```html
<form>
  <!-- First and Last Name side by side -->
  <div class="name-row">
    <div>
      <label for="firstname">First Name</label>
      <input type="text" id="firstname" placeholder="e.g. Amara">
    </div>
    <div>
      <label for="lastname">Last Name</label>
      <input type="text" id="lastname" placeholder="e.g. Okafor">
    </div>
  </div>

  <!-- Email with icon -->
  <label for="email">Email Address</label>
  <div class="input-icon-wrapper">
    <i class="fa fa-envelope"></i>
    <input type="email" id="email" placeholder="amara@example.com">
  </div>

  <!-- Password with icon -->
  <label for="password">Password</label>
  <div class="input-icon-wrapper">
    <i class="fa fa-lock"></i>
    <input type="password" id="password" placeholder="Min. 8 characters">
  </div>

  <!-- Confirm Password -->
  <label for="confirm">Confirm Password</label>
  <div class="input-icon-wrapper">
    <i class="fa fa-check-circle"></i>
    <input type="password" id="confirm" placeholder="Repeat your password">
  </div>

  <!-- Country dropdown -->
  <label for="country">Country</label>
  <select id="country">
    <option value="">-- Select your country --</option>
    <option>Nigeria</option>
    <option>Ghana</option>
    <option>Kenya</option>
    <option>South Africa</option>
    <option>Senegal</option>
    <option>Ethiopia</option>
  </select>

  <!-- Course dropdown -->
  <label for="course">Course of Interest</label>
  <select id="course">
    <option value="">-- Select a course --</option>
    <option>Web Development</option>
    <option>Data Science</option>
    <option>UI/UX Design</option>
    <option>Mobile App Development</option>
    <option>Cybersecurity</option>
  </select>

  <!-- Bio textarea -->
  <label for="bio">Short Bio (Optional)</label>
  <textarea id="bio" rows="4"
    placeholder="Tell us a little about yourself and your learning goals..."></textarea>

  <!-- Terms checkbox -->
  <div class="checkbox-row">
    <input type="checkbox" id="terms">
    <label for="terms">I agree to the Terms of Service and Privacy Policy</label>
  </div>

  <!-- Submit button -->
  <input type="submit" value="Create My Account">
</form>
```

**Final Expected Output:** A polished, professional registration form that includes:
- Two name fields side by side
- Email with envelope icon, passwords with lock icons
- Consistent dropdown styling
- A resizable textarea
- A styled checkbox with terms text
- A blue button that darkens on hover and slightly shrinks when clicked

### Stage 4 — Reflection Questions

1. Why did we use `position: relative` on `.input-icon-wrapper` and `position: absolute` on the icon?
2. What does `flex: 1` on `.name-row > div` do? (Hint: it makes both halves share space equally.)
3. What would happen if you removed `box-sizing: border-box` from the `*` selector?
4. Why do we use `transition` on the focus styles?
5. Why is it important that our `:focus` style still shows something even after removing `outline: none`?

### Optional Advanced Extensions

- Add a "Show/Hide Password" toggle button next to the password field using JavaScript
- Make the form responsive — on mobile screens, the name fields should stack vertically (use `@media` query)
- Add a colour-coded strength indicator below the password field
- Add a profile picture upload with `input[type="file"]`

---

## Common Beginner Mistakes

### Mistake 1: Forgetting `box-sizing: border-box`

**Wrong:**
```css
input {
  width: 100%;
  padding: 15px;
  border: 2px solid #ccc;
}
```
**Problem:** The input overflows its container because padding and border add to the total width.

**Correct:**
```css
* { box-sizing: border-box; }

input {
  width: 100%;
  padding: 15px;
  border: 2px solid #ccc;
}
```

---

### Mistake 2: Removing `outline` Without a Replacement

**Wrong:**
```css
input:focus {
  outline: none;
}
```
**Problem:** Users who navigate by keyboard cannot see which field is active. This breaks accessibility.

**Correct:**
```css
input:focus {
  outline: none;
  border-color: #4a90e2;  /* Visible replacement focus indicator */
  box-shadow: 0 0 0 3px rgba(74, 144, 226, 0.3);
}
```

---

### Mistake 3: Not Using `font-family: inherit` on Inputs

**Wrong:**
```css
textarea {
  width: 100%;
  padding: 10px;
}
```
**Problem:** Textarea might use a monospace or system font that doesn't match your page.

**Correct:**
```css
textarea {
  width: 100%;
  padding: 10px;
  font-family: inherit;  /* Use same font as the rest of the page */
}
```

---

### Mistake 4: Using `input` Instead of `input[type="text"]`

**Wrong:**
```css
input {
  border-radius: 8px;
  padding: 10px;
}
```
**Problem:** This styles ALL inputs — including checkboxes and submit buttons. Checkboxes with `border-radius` and padding look very strange.

**Correct:**
```css
input[type="text"],
input[type="email"],
input[type="password"] {
  border-radius: 8px;
  padding: 10px;
}
```

---

### Mistake 5: Forgetting `cursor: pointer` on Buttons

**Wrong:**
```css
input[type="submit"] {
  background-color: green;
  color: white;
}
```
**Problem:** When hovering, the cursor remains an arrow — it doesn't feel like a clickable button.

**Correct:**
```css
input[type="submit"] {
  background-color: green;
  color: white;
  cursor: pointer;
}
```

---

### Mistake 6: Not Linking Labels to Inputs

**Wrong:**
```html
<label>Email</label>
<input type="email">
```
**Problem:** The label is not linked to the input. Clicking the label won't focus the input. Screen readers cannot associate them.

**Correct:**
```html
<label for="email">Email</label>
<input type="email" id="email">
```

---

## Reflection Questions

1. What is the difference between `padding` and `margin` when applied to an input field?
2. Why would you use `input[type="text"]:focus` instead of just `input:focus`?
3. You want to add a search icon to the right side of an input instead of the left. What CSS changes would you need to make to the icon and input padding?
4. What problem does `appearance: none` solve on `<select>` elements?
5. Why is `transition` important for good UX on form focus effects?
6. When would you use a `<textarea>` instead of `<input type="text">`?
7. What is the purpose of the `for` attribute on a `<label>` element?
8. If you set `resize: none` on a textarea, what does that do?

---

## Completion Checklist

Before moving to the next lesson, confirm you can do all of the following:

- [ ] Style `<input>` fields with `width`, `padding`, `border`, `border-radius`, and `font-size`
- [ ] Use `box-sizing: border-box` to prevent overflow
- [ ] Style specific input types using `input[type="text"]`, `input[type="email"]`, etc.
- [ ] Apply `:focus` styling with a visible focus indicator (border colour or box-shadow)
- [ ] Remove the default `outline` safely (only when replacing with something visible)
- [ ] Use `transition` to animate focus changes smoothly
- [ ] Add icons inside inputs using `position: relative/absolute` technique
- [ ] Style `<select>` dropdowns and `<textarea>` consistently with inputs
- [ ] Style `<button>` and `input[type="submit"]` with `:hover` effects
- [ ] Use `accent-color` for basic checkbox/radio button styling
- [ ] Build a complete styled form card with container, labels, inputs, and submit button
- [ ] Link labels to inputs using `for` and `id`
- [ ] Identify and fix the six common beginner mistakes listed above

---

## Lesson Summary

In this lesson, you went from raw, unstyled HTML form elements to a professionally designed, interactive form. Here is a recap of everything you learned:

**Styling inputs:** Use `width`, `padding`, `margin`, `border`, `border-radius`, `background-color`, `color`, and `font-size` to control the appearance of input fields. Target specific input types with `input[type="text"]` to avoid accidentally styling checkboxes and buttons.

**`box-sizing: border-box`:** Always apply this to prevent inputs from overflowing their container when padding and borders are added.

**Focus styling (`:focus`):** The `:focus` pseudo-class lets you change how an input looks when the user clicks on it. Always provide a visible focus indicator — change the border colour, add a box-shadow glow, or both. Never just remove `outline` without a replacement.

**Smooth transitions:** Add `transition: border-color 0.3s ease` (or similar) to make focus effects animate smoothly instead of snapping instantly.

**Icons inside inputs:** Use a wrapper `<div>` with `position: relative`, an icon with `position: absolute`, and extra `padding-left` on the input to make room. This technique is used on nearly every modern web form.

**Other elements:** Style `<select>` dropdowns with `appearance: none` and your own CSS. Style `<textarea>` with `resize: vertical` and `font-family: inherit`. Style buttons with `:hover` and `:active` states. Style checkboxes easily with `accent-color`.

**Form container:** Wrap your form in a styled card with `background-color`, `padding`, `border-radius`, `box-shadow`, and `max-width` to create the clean "card form" look used on professional websites worldwide.

With all of these tools, you can now build and style beautiful, functional forms that look great, work correctly for all users, and create a great first impression on any website.

---

*Sources: W3Schools CSS Forms, CSS Form Inputs, CSS Form Focus, CSS Form Elements, and CSS Form Challenges — rewritten as a comprehensive beginner lesson.*
