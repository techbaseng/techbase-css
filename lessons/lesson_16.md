---
render_with_liquid: false
title: "Lesson 16: CSS Links — Styling, States, and Button-Style Links"
nav_order: 16
---

# Lesson 16: CSS Links — Styling, States, and Button-Style Links

---

## Lesson Introduction

Every website you have ever visited has links. The blue underlined words you click to move between pages — those are links. But have you noticed that on professional websites, links look very different? Some are coloured differently, some change colour when you hover over them, some look like buttons, and some have no underline at all.

All of that visual control comes from **CSS**. In this lesson, you will learn exactly how CSS can style links — from their normal state all the way to interactive hover effects and full button-style designs. By the end, you will be able to create a navigation bar of styled link buttons, just like the ones you see on real websites.

This lesson covers three source topics in order:
1. **Styling Links** — the four link states and how to style each one
2. **Link Buttons** — turning a link into a clickable button
3. **Code Challenges** — applying everything to reinforce your understanding

---

## Prerequisite Concepts

Before we begin, let's make sure we understand three things you will need for this lesson.

### What is a Link in HTML?

A **link** in HTML is created with the `<a>` tag (the "anchor" tag). It lets a visitor click to go somewhere else — another page, a section of the page, or a website.

```html
<a href="https://www.example.com">Click here</a>
```

- `<a>` — opens the anchor tag
- `href="..."` — this attribute tells the browser WHERE to go when clicked. "href" stands for **hypertext reference**.
- `Click here` — this is the visible clickable text
- `</a>` — closes the anchor tag

**Expected output in browser:** The words "Click here" appear as blue underlined text. Clicking it takes you to example.com.

### What is a CSS Selector?

A CSS selector tells the browser WHICH element to style. We already know:

```css
a {
  color: red;
}
```

This makes ALL link text red. But links have **states** — different moments in their life (normal, hovered, clicked, visited). CSS lets you style each state separately using something called **pseudo-classes**.

### What is a Pseudo-Class?

A **pseudo-class** is a special keyword added to a selector using a colon `:`. It targets an element only when it is in a specific condition or state.

Think of it like this: imagine a traffic light. It is always the same physical object, but its state changes — green, yellow, red. Pseudo-classes let you style an element differently depending on its "state" at any moment.

```css
a:hover {
  color: orange;
}
```

This only applies `color: orange` when the user is hovering the mouse over the link — not at any other time.

---

## Part 1 — The Four Link States

### What are Link States?

Every `<a>` tag (link) can exist in four different states depending on what the user has done:

| State | Meaning | CSS Pseudo-class |
|---|---|---|
| Unvisited | A link the user has never clicked | `a:link` |
| Visited | A link the user has already clicked before | `a:visited` |
| Hover | The user's mouse is currently sitting over the link | `a:hover` |
| Active | The exact moment the user is clicking the link | `a:active` |

> **Real-world analogy:** Think of a library book. A "new" book is like an unvisited link. A book with your checkout stamp is like a visited link. Flipping through a book is like hovering. Signing your name to borrow it is like the active state.

---

### Styling Unvisited Links — `a:link`

By default, browsers show unvisited links in blue with an underline. You can change this completely.

```html
<!-- HTML -->
<a href="https://www.example.com">Go to Example</a>
```

```css
/* CSS */
a:link {
  color: green;
  text-decoration: none;
}
```

**Line by line:**
- `a:link` — selects links that have **not** been visited yet
- `color: green;` — changes the text colour to green
- `text-decoration: none;` — removes the underline (the default underline on all links)

**Expected output in browser:**  
The link text "Go to Example" appears in **green with no underline**.

> **What happens if you remove `text-decoration: none`?**  
> The link will still have its default underline. Try it — this is how you understand the difference.

---

### Styling Visited Links — `a:visited`

When a user has already clicked a link, the browser remembers it. By default, visited links turn purple. You can customise this too.

```css
a:visited {
  color: darkred;
  text-decoration: none;
}
```

**Line by line:**
- `a:visited` — selects links the user has already clicked
- `color: darkred;` — shows the link in dark red to indicate it has been visited
- `text-decoration: none;` — keeps the underline removed

**Expected output:** After you click the link and come back, the link text becomes **dark red**.

> **Why does this matter?** It helps users know which pages they have already visited, so they do not click the same links repeatedly. This improves the user experience.

---

### Styling Hovered Links — `a:hover`

Hover is the most interactive state. When the user moves their mouse over a link, `:hover` applies immediately.

```css
a:hover {
  color: hotpink;
  text-decoration: underline;
}
```

**Line by line:**
- `a:hover` — applies ONLY when the mouse is over the link
- `color: hotpink;` — changes the text to hotpink
- `text-decoration: underline;` — adds an underline back when hovering

**Expected output:** While the mouse is over the link, it turns **hotpink with an underline**. When the mouse moves away, it returns to its normal style.

> **Thinking prompt:** What do you think happens if you also add `background-color: yellow;` to the hover rule? Try it!

---

### Styling Active Links — `a:active`

The active state is the moment the user is physically pressing (clicking) the link — a very brief flash.

```css
a:active {
  color: blue;
  font-weight: bold;
}
```

**Line by line:**
- `a:active` — applies only during the click (mouse button pressed down)
- `color: blue;` — flashes blue during the click
- `font-weight: bold;` — makes the text bold at the moment of clicking

**Expected output:** A brief flash of **bold blue text** the instant you click the link.

---

### All Four States Together — Complete Example

Here is the standard pattern used on real websites — all four states styled together:

```html
<!-- HTML -->
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Unvisited link */
    a:link {
      color: #0066cc;
      text-decoration: none;
    }

    /* Visited link */
    a:visited {
      color: #8b008b;
      text-decoration: none;
    }

    /* Hovered link */
    a:hover {
      color: #ff6600;
      text-decoration: underline;
    }

    /* Active (being clicked) link */
    a:active {
      color: #cc0000;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <p><a href="https://www.example.com">Visit Example Website</a></p>
  <p><a href="https://www.w3schools.com">Visit W3Schools</a></p>
</body>
</html>
```

**Expected output:**
- The two links start as `#0066cc` (medium blue), no underline
- After visiting one, it turns `#8b008b` (dark purple)
- When mouse hovers, it turns `#ff6600` (orange) and underlines
- At the exact click moment, it flashes `#cc0000` (red and bold)

> **Important rule:** Always write these in this order: `a:link`, `a:visited`, `a:hover`, `a:active`. If you write them in the wrong order, some states may not work. This is because CSS reads rules from top to bottom, and later rules can overwrite earlier ones for the same element.
>
> A helpful way to remember the order: **L**o**V**e **HA**te → Link, Visited, Hover, Active

---

### Changing Text Decoration on Links

The `text-decoration` property is very commonly used on links. Here are all the values you can use:

```css
a:link {
  text-decoration: none;       /* No underline */
}

a:hover {
  text-decoration: underline;  /* Underline */
}
```

Other values:
- `text-decoration: overline;` — line above text
- `text-decoration: line-through;` — strikethrough text

**Example with all three decorations:**

```html
<style>
  .link-none    { text-decoration: none; }
  .link-over    { text-decoration: overline; }
  .link-through { text-decoration: line-through; }
  .link-under   { text-decoration: underline; }
</style>

<p><a href="#" class="link-none">No underline</a></p>
<p><a href="#" class="link-over">Overline</a></p>
<p><a href="#" class="link-through">Line-through</a></p>
<p><a href="#" class="link-under">Underline</a></p>
```

> **Tip:** `href="#"` is a common trick in demos — it means "link to nowhere." It creates a valid link without navigating anywhere, so you can test styles.

---

### Changing Background Colour on Links

Links are inline elements — they sit inside text. But you can still give them a background colour:

```css
a:link {
  background-color: yellow;
}

a:hover {
  background-color: lightgreen;
}
```

**Expected output:** The link text has a yellow background normally, and switches to light green on hover.

This is useful for highlight-style links, or links inside a dark background.

---

### Using Multiple Properties Together

You can combine as many properties as you want in each state. Here is a creative example:

```css
a:link {
  color: white;
  background-color: navy;
  padding: 4px 8px;
  border-radius: 4px;
  text-decoration: none;
}

a:hover {
  color: navy;
  background-color: white;
  border: 1px solid navy;
}
```

**Expected output:** Links look like small navy-coloured tags. On hover, the colours invert — white becomes navy and navy becomes white. This is called a "colour inversion hover effect" and is very popular in web design.

---

## Part 2 — Link Buttons

So far, we have styled the text colour and decoration of links. But many websites use links that look like **buttons** — with a box, background colour, padding, rounded corners, and hover effects.

### Why Would You Style a Link as a Button?

A `<a>` link is normally inline text. A `<button>` is a form element. But in navigation menus, call-to-action sections, and UI toolbars, designers want button-like **visual appearance** while still having normal link **behaviour** (clicking goes somewhere). The solution: style the `<a>` tag to look like a button using CSS.

> **Real-world example:** The "Sign Up", "Learn More", and "Get Started" links on most websites are simply `<a>` tags styled to look like buttons.

---

### Step 1 — Basic Link Button

Let's transform a plain link into a button step by step.

**Start — plain link:**

```html
<a href="#">Click Me</a>
```

**Add CSS to make it a button:**

```css
a {
  display: inline-block;
  background-color: #4CAF50;
  color: white;
  padding: 14px 25px;
  text-align: center;
  text-decoration: none;
  font-size: 16px;
}
```

**Line by line:**
- `display: inline-block;` — normally, `<a>` is an "inline" element. Inline elements cannot have padding applied vertically. Changing it to `inline-block` allows us to add height, width, and padding in all directions, making it block-like while still flowing with text.
- `background-color: #4CAF50;` — gives the button a green background
- `color: white;` — makes the text white (for contrast against green)
- `padding: 14px 25px;` — adds space inside the button: 14px top/bottom, 25px left/right. This is what makes the button large enough to click comfortably.
- `text-align: center;` — centres the text horizontally inside the button
- `text-decoration: none;` — removes the underline
- `font-size: 16px;` — sets the text size

**Expected output:** A green rectangular button with white text "Click Me".

---

### Step 2 — Add Hover Effect to the Button

Now let's make the button respond when the user hovers over it:

```css
a:hover {
  background-color: #45a049;
  cursor: pointer;
}
```

**Line by line:**
- `background-color: #45a049;` — a slightly darker green appears on hover, giving visual feedback
- `cursor: pointer;` — changes the mouse cursor to the hand-pointer icon (even though `<a>` already does this by default, adding it explicitly ensures clarity)

**Expected output:** When the mouse is over the button, it darkens slightly. When the mouse moves away, it returns to the brighter green.

> **Design principle:** Hover effects give the user feedback that the element is interactive. Without any visual change on hover, users may not know if they are hovering over a clickable element.

---

### Step 3 — Full Styled Button with All States

Here is a complete, professional-looking button with all states properly handled:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    a.button {
      display: inline-block;
      background-color: #008CBA;  /* Blue */
      color: white;
      padding: 15px 32px;
      text-align: center;
      text-decoration: none;
      font-size: 16px;
      border-radius: 8px;
      font-family: Arial, sans-serif;
      transition: background-color 0.3s ease;
    }

    a.button:hover {
      background-color: #005f7f;  /* Darker blue */
    }

    a.button:active {
      background-color: #003d52;  /* Even darker on click */
    }
  </style>
</head>
<body>

  <a href="#" class="button">Get Started</a>

</body>
</html>
```

**Line by line — new things introduced:**
- `a.button` — this selector targets only `<a>` tags that also have the class `button`. This is important: if you style ALL `<a>` tags as buttons, every text link on your page would look like a button. Using a class lets you choose which links become buttons.
- `border-radius: 8px;` — rounds the corners of the button, giving it a softer, modern look
- `font-family: Arial, sans-serif;` — ensures the button text uses Arial font
- `transition: background-color 0.3s ease;` — this creates a smooth colour change animation when hovering. Without this, the colour change is instant. With `0.3s`, it fades over 0.3 seconds. `ease` means it starts and ends gently.

**Expected output:** A blue, rounded-corner button that smoothly fades to a darker blue on hover, then darker still when clicked.

> **Thinking prompt:** What if you changed `border-radius: 8px` to `border-radius: 50px`? What shape would the button become?

---

### Different Button Styles

Here are four common button style variations used in real websites:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Base button style for all */
    a.btn {
      display: inline-block;
      padding: 12px 28px;
      font-size: 15px;
      text-decoration: none;
      border-radius: 5px;
      margin: 8px;
      font-family: Arial, sans-serif;
      font-weight: bold;
    }

    /* Style 1: Solid Green */
    a.btn-green {
      background-color: #4CAF50;
      color: white;
    }

    a.btn-green:hover {
      background-color: #367a38;
    }

    /* Style 2: Solid Red */
    a.btn-red {
      background-color: #f44336;
      color: white;
    }

    a.btn-red:hover {
      background-color: #b71c1c;
    }

    /* Style 3: Outlined (Border Only, No Fill) */
    a.btn-outline {
      background-color: transparent;
      color: #4CAF50;
      border: 2px solid #4CAF50;
    }

    a.btn-outline:hover {
      background-color: #4CAF50;
      color: white;
    }

    /* Style 4: Grey / Disabled look */
    a.btn-grey {
      background-color: #9e9e9e;
      color: white;
      cursor: not-allowed;
    }
  </style>
</head>
<body>

  <a href="#" class="btn btn-green">Confirm</a>
  <a href="#" class="btn btn-red">Delete</a>
  <a href="#" class="btn btn-outline">Subscribe</a>
  <a href="#" class="btn btn-grey">Disabled</a>

</body>
</html>
```

**What is new here:**

- Multiple classes on one element: `class="btn btn-green"` means the element gets styles from BOTH `a.btn` AND `a.btn-green`. The base `a.btn` handles shared properties like `padding` and `font-size`, while `a.btn-green` handles the specific colour.
- `background-color: transparent;` — on the outline button, the background is invisible. Only the border is visible. On hover, it fills in — this is the classic "outline button hover" technique used everywhere.
- `cursor: not-allowed;` — shows a "forbidden" cursor icon to visually indicate the grey button is disabled or inactive.

**Expected output:** Four buttons side by side: green solid, red solid, green outlined (fills on hover), and grey "disabled-looking".

---

### Making a Full-Width Button

Sometimes you want a button that stretches across its container (like a "Submit" button in a form):

```css
a.btn-fullwidth {
  display: block;          /* block takes the full width automatically */
  width: 100%;             /* optional: makes 100% of its parent container */
  background-color: #333;
  color: white;
  padding: 16px;
  text-align: center;
  text-decoration: none;
  font-size: 18px;
  box-sizing: border-box;  /* ensures padding doesn't overflow the width */
}
```

**`display: block` vs `display: inline-block`:**
- `inline-block` — the button only takes as much width as its content + padding
- `block` — the button expands to fill the full width of its container

---

### Adding a Border and Box Shadow

Professional-looking buttons often have a subtle border and shadow:

```css
a.btn-premium {
  display: inline-block;
  background-color: #e7e7e7;
  color: black;
  padding: 12px 28px;
  text-decoration: none;
  font-size: 15px;
  border: 1px solid #9e9e9e;        /* thin grey border */
  box-shadow: 2px 2px 5px #aaaaaa;  /* horizontal offset, vertical offset, blur, colour */
  border-radius: 4px;
}

a.btn-premium:hover {
  background-color: #d5d5d5;
  box-shadow: 3px 3px 8px #888888;  /* slightly larger shadow on hover */
}
```

**`box-shadow` breakdown:**
`box-shadow: 2px 2px 5px #aaaaaa;`
- `2px` — horizontal shadow offset (moves shadow 2px to the right)
- `2px` — vertical shadow offset (moves shadow 2px downward)
- `5px` — blur radius (how soft/blurry the shadow edge is)
- `#aaaaaa` — shadow colour (medium grey)

**Expected output:** A grey button with a visible soft shadow. On hover, the shadow grows slightly, making the button appear to "lift" slightly — a popular material design effect.

---

## Part 3 — Code Challenges Applied

The W3Schools code challenges for CSS links test whether you can correctly apply the four link states, button styling, and hover effects. Let's work through the types of challenges you would encounter.

---

### Challenge Type 1: Style a Specific Link State

**Task:** Make all unvisited links have the colour `coral` and remove the underline.

```css
/* Solution */
a:link {
  color: coral;
  text-decoration: none;
}
```

---

### Challenge Type 2: Add Hover Behaviour

**Task:** When hovering over a link, change its background colour to `#f1f1f1`.

```css
/* Solution */
a:hover {
  background-color: #f1f1f1;
}
```

---

### Challenge Type 3: Create a Button Link

**Task:** Style the link with class `btn` to look like a button: green background, white text, padding `10px 20px`, no underline.

```html
<a href="#" class="btn">Click Me</a>
```

```css
/* Solution */
a.btn {
  display: inline-block;
  background-color: green;
  color: white;
  padding: 10px 20px;
  text-decoration: none;
}
```

---

## Guided Practice Exercises

### Exercise 1 — Style a Navigation Menu with Link States

**Objective:** Create a horizontal navigation bar with three links, each styled with all four states.

**Scenario:** You are building the header navigation for a student club website. The links should be dark and professional: dark navy when unvisited, dark grey when visited, orange when hovered, and deep red when active.

**Steps:**

1. Create an HTML file with a `<nav>` section containing three links: Home, About, and Contact.
2. Style all links with a base dark navy colour and no underline.
3. Style the visited state with dark grey.
4. Style the hover state with orange and an underline.
5. Style the active state with deep red.

**Starter template:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Write your CSS here */

  </style>
</head>
<body>
  <nav>
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Contact</a>
  </nav>
</body>
</html>
```

**Hint:** Don't forget the LVHA order — Link, Visited, Hover, Active.

**Expected output:**
- Links are dark navy, no underline
- Visited links turn dark grey
- Hovering turns them orange with underline
- Clicking flashes deep red

**Solution:**

```css
a:link {
  color: #1a237e;       /* dark navy */
  text-decoration: none;
}

a:visited {
  color: #424242;       /* dark grey */
  text-decoration: none;
}

a:hover {
  color: #e65100;       /* orange */
  text-decoration: underline;
}

a:active {
  color: #b71c1c;       /* deep red */
  text-decoration: underline;
}
```

**Self-check questions:**
- Does the hover effect work when you move your mouse over a link?
- If you click a link and go back, does it show in dark grey?
- Did the order of your CSS rules follow LVHA?

---

### Exercise 2 — Create a Button Bar

**Objective:** Build a row of three styled button links: "Buy Now" (blue), "Learn More" (outlined blue), and "Cancel" (grey).

**Scenario:** You are building a product page for an online store. You need three action buttons at the bottom of the product description.

**Steps:**

1. Create three `<a>` links with classes `btn-buy`, `btn-learn`, and `btn-cancel`.
2. Style `btn-buy` as a solid blue button.
3. Style `btn-learn` as an outlined blue button (transparent background, blue border).
4. Style `btn-cancel` as a grey button.
5. Add hover effects to each.

**Expected output:**
- Three buttons side by side
- "Buy Now" is solid blue; on hover it darkens
- "Learn More" has a blue border only; on hover it fills blue
- "Cancel" is grey; on hover it darkens

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Shared base */
    a.btn {
      display: inline-block;
      padding: 12px 24px;
      font-size: 15px;
      text-decoration: none;
      border-radius: 6px;
      margin-right: 10px;
      font-weight: bold;
      transition: all 0.2s ease;
    }

    /* Buy Now - solid blue */
    a.btn-buy {
      background-color: #1565C0;
      color: white;
    }

    a.btn-buy:hover {
      background-color: #0d47a1;
    }

    /* Learn More - outlined */
    a.btn-learn {
      background-color: transparent;
      color: #1565C0;
      border: 2px solid #1565C0;
    }

    a.btn-learn:hover {
      background-color: #1565C0;
      color: white;
    }

    /* Cancel - grey */
    a.btn-cancel {
      background-color: #9e9e9e;
      color: white;
    }

    a.btn-cancel:hover {
      background-color: #616161;
    }
  </style>
</head>
<body>

  <a href="#" class="btn btn-buy">Buy Now</a>
  <a href="#" class="btn btn-learn">Learn More</a>
  <a href="#" class="btn btn-cancel">Cancel</a>

</body>
</html>
```

**Optional What-If Challenge:** What if you wanted the "Cancel" button to show `cursor: not-allowed` on hover, making it look like it is disabled? Add that property to `a.btn-cancel:hover` and observe the result.

---

## Mini Project — Personal Portfolio Navigation Bar

### Project Overview

You will build the **navigation bar** for a personal portfolio website. It will contain five links: Home, About Me, Projects, Blog, and Contact. The links will be styled as buttons in the navigation bar with hover effects.

### Stage 1 — Setup the HTML Structure

```html
<!DOCTYPE html>
<html>
<head>
  <title>My Portfolio</title>
  <style>
    /* CSS goes here */
  </style>
</head>
<body>

  <nav class="navbar">
    <a href="#" class="nav-link">Home</a>
    <a href="#" class="nav-link">About Me</a>
    <a href="#" class="nav-link">Projects</a>
    <a href="#" class="nav-link">Blog</a>
    <a href="#" class="nav-link">Contact</a>
  </nav>

</body>
</html>
```

**Milestone output:** Five plain, default-styled links appear in a row.

---

### Stage 2 — Style the Navbar Background

```css
.navbar {
  background-color: #1a1a2e;   /* very dark navy, almost black */
  padding: 10px 20px;
  overflow: hidden;             /* keeps floated elements inside */
}
```

**Milestone output:** A dark navy horizontal bar appears at the top of the page.

---

### Stage 3 — Style the Navigation Links as Buttons

```css
a.nav-link {
  display: inline-block;
  color: #e0e0e0;               /* light grey text */
  background-color: transparent;
  padding: 10px 18px;
  text-decoration: none;
  font-size: 15px;
  font-family: Arial, sans-serif;
  border-radius: 4px;
  margin-right: 4px;
  transition: background-color 0.25s ease, color 0.25s ease;
}
```

**Milestone output:** Five evenly spaced light grey labels appear inside the dark navbar. They do not look like interactive links yet — but now they fill the space properly.

---

### Stage 4 — Add Hover and Active States

```css
a.nav-link:hover {
  background-color: #e94560;   /* bright red-pink */
  color: white;
}

a.nav-link:active {
  background-color: #c0112e;
  color: white;
}

a.nav-link:visited {
  color: #b0b0b0;               /* slightly dimmer grey for visited */
}
```

**Milestone output:** Moving your mouse over any nav link makes it glow red-pink. The active flash works on click. Visited links appear dimmer grey.

---

### Stage 5 — Final Output and Enhancements

Your final navbar should look like a modern, professional navigation header. Here is the complete code:

```html
<!DOCTYPE html>
<html>
<head>
  <title>My Portfolio</title>
  <style>
    /* Reset default browser margin/padding */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
    }

    /* Navbar container */
    .navbar {
      background-color: #1a1a2e;
      padding: 12px 24px;
      display: flex;
      align-items: center;
    }

    /* Base nav link */
    a.nav-link {
      display: inline-block;
      color: #e0e0e0;
      background-color: transparent;
      padding: 10px 18px;
      text-decoration: none;
      font-size: 15px;
      border-radius: 4px;
      margin-right: 6px;
      transition: background-color 0.25s ease, color 0.25s ease;
    }

    /* Hover state */
    a.nav-link:hover {
      background-color: #e94560;
      color: white;
    }

    /* Active (click) state */
    a.nav-link:active {
      background-color: #c0112e;
      color: white;
    }

    /* Visited state */
    a.nav-link:visited {
      color: #b0b0b0;
    }

    /* Hero section below navbar */
    .hero {
      background-color: #16213e;
      color: white;
      text-align: center;
      padding: 80px 20px;
    }

    .hero h1 {
      font-size: 40px;
      margin-bottom: 20px;
    }

    .hero p {
      font-size: 18px;
      color: #aaaaaa;
      margin-bottom: 30px;
    }

    /* Call-to-action button in the hero section */
    a.cta-button {
      display: inline-block;
      background-color: #e94560;
      color: white;
      padding: 14px 36px;
      font-size: 16px;
      text-decoration: none;
      border-radius: 30px;
      font-weight: bold;
      transition: background-color 0.3s ease, transform 0.2s ease;
    }

    a.cta-button:hover {
      background-color: #c0112e;
      transform: scale(1.05);   /* slightly enlarges button on hover */
    }
  </style>
</head>
<body>

  <!-- Navigation Bar -->
  <nav class="navbar">
    <a href="#" class="nav-link">Home</a>
    <a href="#" class="nav-link">About Me</a>
    <a href="#" class="nav-link">Projects</a>
    <a href="#" class="nav-link">Blog</a>
    <a href="#" class="nav-link">Contact</a>
  </nav>

  <!-- Hero Section -->
  <div class="hero">
    <h1>Hello, I'm Alex 👋</h1>
    <p>A web developer passionate about creating beautiful, accessible websites.</p>
    <a href="#" class="cta-button">View My Work</a>
  </div>

</body>
</html>
```

**New things introduced in the final version:**
- `display: flex;` and `align-items: center;` on `.navbar` — these are flexbox properties that horizontally align all the nav links and vertically center them within the bar.
- `transform: scale(1.05);` on the CTA button hover — this slightly enlarges the button on hover, creating a "pop" effect.
- `border-radius: 30px;` on the CTA button — this creates a pill-shaped button (fully round ends), which is a very popular modern button style.

**Milestone output:** A complete, polished portfolio header with: dark navbar + red-pink hover links + hero section + pill-shaped call-to-action button.

---

**Reflection Questions:**
1. What would happen if you applied the nav-link styles to ALL `<a>` tags instead of using the class `nav-link`?
2. How would you add a "currently active page" indicator — making one link appear permanently highlighted?
3. Why is `transition` important for user experience?

**Optional Extension:** Add a "currently active page" indicator. Create an additional class `active-page` and style it like the hover effect permanently. Then add it to the "Home" link: `<a href="#" class="nav-link active-page">Home</a>`.

---

## Common Beginner Mistakes

### Mistake 1: Wrong Order of Link Pseudo-Classes

**Wrong:**
```css
a:hover { color: orange; }
a:link  { color: blue; }
```

**Problem:** CSS applies rules from top to bottom. `a:link` comes after `a:hover`, so it overrides the hover colour for unvisited links. The hover will never be orange for unvisited links.

**Correct:**
```css
a:link    { color: blue; }
a:visited { color: purple; }
a:hover   { color: orange; }
a:active  { color: red; }
```

Always use the LVHA order.

---

### Mistake 2: Forgetting `display: inline-block` on Button Links

**Wrong:**
```css
a.button {
  padding: 20px 40px;   /* padding won't work correctly */
  background-color: green;
  color: white;
}
```

**Problem:** `<a>` is an inline element. Padding applied vertically to inline elements does not push other content away — it overlaps. The button will not have the correct height.

**Correct:**
```css
a.button {
  display: inline-block;   /* REQUIRED for proper padding */
  padding: 20px 40px;
  background-color: green;
  color: white;
}
```

---

### Mistake 3: Not Removing the Underline from Button Links

**Wrong:**
```css
a.button {
  display: inline-block;
  background-color: purple;
  color: white;
  padding: 12px 24px;
  /* MISSING: text-decoration: none; */
}
```

**Problem:** The link will still show its default underline, which looks unprofessional on a button.

**Correct:**
```css
a.button {
  display: inline-block;
  background-color: purple;
  color: white;
  padding: 12px 24px;
  text-decoration: none;   /* Remove the underline */
}
```

---

### Mistake 4: Styling `a` Without a State and Expecting It to Override States

**Wrong thinking:** "I styled `a { color: black; }` but my visited links are still purple!"

**Explanation:** Browser default stylesheets include pseudo-class rules for `a:visited` and `a:link`. If you only write `a { color: black; }`, the browser's specific `a:visited { color: purple; }` rule can still win because it is more specific.

**Correct:** Always explicitly set ALL four states if you want complete control:
```css
a:link    { color: black; }
a:visited { color: black; }
a:hover   { color: grey; }
a:active  { color: darkgrey; }
```

---

### Mistake 5: Using `:hover` Before `:link` or `:visited`

```css
/* Wrong Order */
a:hover   { color: red; }
a:link    { color: blue; }
a:visited { color: purple; }
```

The hover will be overridden by `:link` and `:visited` for links that have those states. The LVHA mnemonic saves you: **L**ink → **V**isited → **H**over → **A**ctive.

---

## Reflection Questions

1. What is the difference between `a:link` and just `a`? When would you use each?

2. If you want a button to be the full width of its container, which `display` value should you use — `inline-block` or `block`? Why?

3. What does `transition: background-color 0.3s ease` do, and why is it better than no transition?

4. What does `text-decoration: none` do on a link? What would the link look like without it?

5. What does `cursor: pointer` do? What cursor type does a normal `<a>` already use by default?

6. If a link button shows an underline, which property would you add to remove it?

7. Why might you use a class like `class="btn btn-green"` instead of directly styling all `<a>` tags as buttons?

8. What are the four link states and what event in the user's behaviour triggers each one?

---

## Completion Checklist

Before you move on to the next lesson, check that you can confidently do each of these:

- [ ] I can explain the four link pseudo-classes: `:link`, `:visited`, `:hover`, `:active`
- [ ] I know the correct LVHA order and why it matters
- [ ] I can style each link state with a different colour
- [ ] I can remove or add an underline from a link using `text-decoration`
- [ ] I can add a background colour to a link
- [ ] I understand why `display: inline-block` is needed for link buttons
- [ ] I can create a solid-colour button from a link
- [ ] I can create an outlined (transparent background + border) button
- [ ] I can add a hover colour change to a button
- [ ] I can add a smooth `transition` effect to a button
- [ ] I can use multiple classes on one element (e.g., `class="btn btn-green"`)
- [ ] I can create a full navigation bar with styled link buttons
- [ ] I understand common mistakes (LVHA order, missing `inline-block`, etc.)

---

## Lesson Summary

In this lesson, you learned how CSS can control the appearance of links — one of the most important and most visible interactive elements on any web page.

**Key takeaways:**

Links have four states — unvisited (`:link`), visited (`:visited`), hovered (`:hover`), and active (`:active`) — and each can be styled independently. The LVHA order (Link, Visited, Hover, Active) must always be followed to prevent CSS rules from cancelling each other out.

The most important properties for styling links are `color`, `text-decoration`, and `background-color`. Together with `padding`, `border-radius`, and `display: inline-block`, you can transform any link into a professional-looking button. Adding `transition` smooths out the visual change between states, improving the user experience.

Button-style links are used everywhere in real web design — for navigation menus, call-to-action sections, product pages, and dashboards. The skills you practised in the mini-project directly mirror what front-end developers do in real jobs every day.

In the next lesson, you will build on this foundation by exploring CSS Lists — how to style bullet points, numbered lists, and use list items as building blocks for navigation menus.

---

*Sources: W3Schools CSS Links Tutorial (https://www.w3schools.com/css/css_link.asp), CSS Link Buttons (https://www.w3schools.com/css/css_link_buttons.asp), CSS Link Code Challenges (https://www.w3schools.com/css/css_challenges_link.asp)*
