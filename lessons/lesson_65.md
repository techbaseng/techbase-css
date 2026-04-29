---
render_with_liquid: false
title: "CSS Variables — The var() Function, Overriding, JavaScript, and Media Queries"
nav_order: 65
---

# Lesson 65 — CSS Variables: The var() Function, Overriding, JavaScript & Media Queries

---

## Lesson Introduction

Have you ever built a webpage and needed to use the same colour — say, a brand blue — in twenty different places? And then the client says "change it to green." Suddenly you are hunting through hundreds of lines of CSS making the same edit over and over.

CSS Variables (also called **CSS Custom Properties**) solve this problem completely. You store a value once, give it a name, and reuse that name everywhere. When you want to change the value, you change it in exactly one place and the whole page updates instantly.

In this lesson you will learn:

- What a CSS variable is and how to declare one
- How to use the `var()` function to insert variable values
- How global and local scope work
- How to override variables for specific sections of a page
- How to read and change CSS variables with JavaScript
- How to use CSS variables inside media queries to build responsive designs
- How to apply all of this in a real mini-project

No prior knowledge of CSS variables is required. If you know basic CSS (selectors, properties, values) you are ready.

---

## Prerequisite Concepts

Before we dive into CSS variables, let us quickly review two concepts you need to understand first.

### What is a CSS Property?

A CSS property is an instruction you give to the browser about how something should look. For example:

```css
p {
  color: red;
  font-size: 16px;
}
```

- `color` is a **property**
- `red` is its **value**

### What is a Selector?

A selector targets which HTML elements you want to style. `p` targets all paragraph elements, `.note` targets all elements with class `note`, and so on.

Now you are ready!

---

## Part 1 — CSS Variables and the var() Function

### What is a CSS Variable?

A CSS variable is a **named storage container** for a value you want to reuse. Think of it like a labelled jar in your kitchen. Instead of remembering that your favourite spice is "reddish-orange powder", you label the jar "paprika". Now whenever you need it you just say "grab the paprika jar."

In CSS:

- Instead of writing `#1e90ff` in twenty places, you store it in a variable named `--brand-color`.
- Whenever you need that colour, you write `var(--brand-color)` and CSS grabs the value from the jar.

### Why Do CSS Variables Exist? What Problem Do They Solve?

Without variables, large stylesheets suffer from three problems:

1. **Repetition** — the same colour code or font size written 50 times
2. **Hard maintenance** — change one value means editing 50 places (and missing some)
3. **Low readability** — `#1e90ff` means nothing; `--primary-color` is self-documenting

CSS variables solve all three at once.

### Naming Rules

A CSS variable name **must**:

- Begin with exactly **two dashes**: `--`
- Be followed by a descriptive name using letters, numbers, and hyphens
- Be **case-sensitive** — `--MyColor` and `--mycolor` are two different variables

```css
/* ✅ Valid variable names */
--primary-color: blue;
--font-size-large: 24px;
--spacing-unit: 8px;
--header-bg: #333333;

/* ❌ Invalid — missing the double dash */
-primary-color: blue;    /* wrong */
primary-color: blue;     /* wrong */
```

### Declaring a Variable

You declare a variable inside a CSS selector block, like any other property:

```css
selector {
  --variable-name: value;
}
```

There are two scopes — **global** and **local**. Let us learn them one at a time.

---

### Global Variables — The `:root` Selector

A **global variable** is available to every single element on the page. To make a variable global, declare it inside the `:root` selector.

**What is `:root`?**
`:root` is a special CSS selector that matches the very top of your HTML document — the `<html>` element. Because every other element on the page is a child of `<html>`, any variable declared in `:root` is visible everywhere on the page.

Analogy: `:root` is like the front lobby of a building. Anything placed in the lobby can be seen by everyone in the building.

```css
/* Declaring two global variables */
:root {
  --primary-color: #1e90ff;    /* a nice blue colour */
  --text-color: #ffffff;       /* white */
}
```

---

### Local Variables — Inside a Regular Selector

A **local variable** is only available to the selector where it is declared, and to any elements nested inside it. Elements outside that selector cannot see it.

```css
.card {
  --card-bg: lightyellow;    /* local — only .card and its children can use this */
}
```

Analogy: A local variable is like a note pinned to a specific desk. Only the person sitting at that desk (and anyone they share it with) can read it.

---

### The `var()` Function — Using Your Variables

Once you have declared a variable, you use the `var()` function to insert its value anywhere in your CSS.

**Syntax:**

```
var(--variable-name, fallback-value)
```

| Part | What it means |
|------|---------------|
| `--variable-name` | **Required.** The name of the variable you want to use. Must start with `--`. |
| `fallback-value` | **Optional.** If the variable is not found, CSS uses this value instead. |

**Simple Example 1 — Using a colour variable:**

```css
:root {
  --brand-color: tomato;
}

h1 {
  color: var(--brand-color);   /* h1 text becomes tomato red */
}
```

**Expected Result:** The `<h1>` heading will display in tomato red.

---

**Simple Example 2 — Using a fallback value:**

```css
:root {
  /* --missing-var is NOT declared */
}

p {
  color: var(--missing-var, black);   /* fallback kicks in → text is black */
}
```

**Expected Result:** Because `--missing-var` does not exist, CSS uses the fallback `black` instead.

> 💡 **Tip:** Always add a fallback for critical properties, especially when the variable might not always be defined.

---

### Full Global Variable Example

Here is a complete realistic example. Notice how `--primary-bg-color` and `--primary-color` are declared once but used in four different places.

```css
:root {
  --primary-bg-color: #1e90ff;   /* dodger blue background colour */
  --primary-color: #ffffff;      /* white text colour */
}

body {
  background-color: var(--primary-bg-color);   /* body background becomes blue */
}

.container {
  color: var(--primary-bg-color);              /* text inside container is blue */
  background-color: var(--primary-color);      /* container background is white */
  padding: 15px;
}

.container h2 {
  border-bottom: 2px solid var(--primary-bg-color);   /* blue underline on h2 */
}

.container .note {
  border: 1px solid var(--primary-bg-color);          /* blue border on .note */
  padding: 10px;
}
```

**Expected Visual Result:**

- The whole page body has a blue background
- The container has a white background with blue text
- The `h2` heading has a blue underline
- The `.note` box has a blue border
- All blue values come from the single variable `--primary-bg-color`

---

**Now for the magic — changing the entire look with 2 lines:**

```css
:root {
  --primary-bg-color: #8FBC8F;   /* ← changed from blue to soft green */
  --primary-color: #FFFAF0;      /* ← changed from white to floral white */
}
```

Without touching the `body`, `.container`, `h2`, or `.note` rules at all — every colour on the page updates automatically. That is the real power of CSS variables.

> 🤔 **Think About This:** What would have to change if you had NOT used variables, and needed to update the colour in all four selectors manually?

---

### Advantages of CSS Variables — Summary

Using `var()` gives you three key advantages:

1. **Easier maintenance** — change one value, everything updates
2. **Easier to read** — `--primary-bg-color` is far more meaningful than `#1e90ff`
3. **Easier to update colours across an entire page** with minimal effort

---

## Part 2 — Overriding CSS Variables

### What Does "Overriding a Variable" Mean?

Overriding means giving a variable a **different value in a specific context**, while keeping the original global value everywhere else.

Think of it this way: your company's brand colour is blue globally across the entire website. But one special "danger" section of the page needs to use red. You can override `--primary-color` just for that section, setting it to red, without changing the global blue definition.

This works because of a concept called **the cascade and inheritance**.

---

### How Variable Overriding Works — The Cascade Rule

When CSS looks up a variable inside `var()`, it travels **up the DOM tree** from the current element, searching for the nearest declaration of that variable. It uses whichever declaration it finds first — either on the element itself, on a parent, or eventually reaching `:root`.

This means:

- A variable declared closer to an element **wins over** the global `:root` version
- The more specific (closer) declaration **overrides** the more general one

---

### Example 1 — Simple Override

```css
/* STEP 1: Declare globally in :root */
:root {
  --button-color: #1e90ff;   /* default blue */
}

/* STEP 2: All buttons use the global variable */
button {
  background-color: var(--button-color);
  color: white;
  padding: 10px 20px;
}

/* STEP 3: Override ONLY for buttons inside .danger-zone */
.danger-zone {
  --button-color: #ff4444;   /* local override — red */
}
```

**Expected Result:**

- Buttons everywhere on the page → blue background
- Buttons inside `.danger-zone` → red background (because the local `--button-color` overrides the global one)

---

### Example 2 — Overriding for a Specific Element Class

Imagine a card design where most cards use a white background, but "featured" cards use gold.

```css
:root {
  --card-bg: white;           /* global default */
  --card-border: #cccccc;     /* grey border globally */
}

.card {
  background-color: var(--card-bg);
  border: 2px solid var(--card-border);
  padding: 20px;
  margin: 10px;
}

/* Override: featured cards get different colours */
.card.featured {
  --card-bg: gold;            /* local override */
  --card-border: orange;      /* local override */
}
```

**Expected Result:**

- `.card` → white background, grey border
- `.card.featured` → gold background, orange border
- No changes to the `.card` rule itself were needed

---

### Example 3 — Using Local Variables for Component Theming

This pattern is extremely common in professional web development. Each component declares its own local variables that can be customised without affecting other components.

```css
:root {
  --spacing: 10px;
  --text-color: #333;
}

/* Navigation uses its own overrides */
nav {
  --text-color: white;      /* nav text is white */
  --spacing: 20px;          /* nav spacing is bigger */
  color: var(--text-color);
  padding: var(--spacing);
  background-color: #222;
}

/* Footer uses different overrides */
footer {
  --text-color: #888;       /* footer text is grey */
  color: var(--text-color);
  padding: var(--spacing);  /* inherits global 10px spacing */
}

/* Main content uses the global defaults */
main {
  color: var(--text-color);   /* gets global #333 */
  padding: var(--spacing);    /* gets global 10px */
}
```

**Expected Result:**

- `nav` → white text, 20px padding
- `footer` → grey text, 10px padding (inherits global `--spacing` because footer didn't override it)
- `main` → dark grey text (#333), 10px padding

> 🤔 **Think About This:** What happens if you add `--text-color: red` inside `main p {}`? Which elements would become red?

---

### The Override Hierarchy — Visualised

```
:root { --color: blue }         ← global fallback (used by everything by default)
   └── .section { --color: green }  ← overrides for .section and all its children
         └── .highlight { --color: red }  ← overrides again, only for .highlight
```

An element inside `.highlight` will see red. An element inside `.section` but NOT `.highlight` will see green. Everything else sees blue.

---

### Common Mistake: Forgetting Variable Scope

```css
/* ❌ MISTAKE: Declaring a variable in a child, trying to use it in a parent */
.card-body {
  --card-accent: purple;
}

.card {
  border-color: var(--card-accent);  /* ❌ This won't work! .card cannot see .card-body's variable */
}
```

**Why it fails:** Variables only flow **downward** through child elements, not upward to parents.

**Fix:** Move the declaration to the parent (`.card`) or to `:root`.

```css
/* ✅ CORRECT */
.card {
  --card-accent: purple;
  border-color: var(--card-accent);  /* ✅ Works — declared in the same element */
}
```

---

## Part 3 — CSS Variables and JavaScript

### Why Use JavaScript with CSS Variables?

CSS by itself is static — it applies styles when the page loads and those styles stay the same. But real websites are dynamic. Users click buttons, toggle dark mode, adjust font sizes, or interact with controls. JavaScript lets you:

- **Read** the current value of a CSS variable
- **Change** a CSS variable's value at any time
- **React** to user actions and update the entire page's look instantly

Because CSS variables are part of the DOM (Document Object Model — the live, interactive version of your webpage), JavaScript can see and modify them directly.

---

### Key JavaScript Methods for CSS Variables

You need two browser built-in methods:

| Method | What it does |
|--------|-------------|
| `getPropertyValue('--name')` | Reads the current value of a CSS variable |
| `setProperty('--name', 'value')` | Sets or changes a CSS variable's value |

These methods work on a **style object**. To access `:root` variables from JavaScript, you use:

```javascript
document.documentElement.style
```

`document.documentElement` refers to the `<html>` element, which is the same element `:root` targets in CSS.

---

### Reading a CSS Variable with JavaScript

**Step-by-step breakdown:**

```javascript
// Step 1: Get a reference to the root element (the <html> element)
var root = document.querySelector(':root');

// Step 2: Get the computed styles of the root element
var rootStyles = getComputedStyle(root);

// Step 3: Read the value of a CSS variable
var value = rootStyles.getPropertyValue('--primary-color');

// Step 4: Do something with the value (e.g. show it)
alert(value);   // shows: " #1e90ff" (note there may be a leading space)
```

**Line-by-line explanation:**

- `document.querySelector(':root')` — finds the root HTML element
- `getComputedStyle(root)` — gets ALL the computed (final calculated) CSS styles applied to the root
- `.getPropertyValue('--primary-color')` — extracts just the value of `--primary-color`

> 💡 **Note:** `getPropertyValue` returns the value as a string. It may include leading or trailing spaces, so use `.trim()` if you need a clean value: `value.trim()`

---

### Changing a CSS Variable with JavaScript

```javascript
// Step 1: Get the root element
var root = document.querySelector(':root');

// Step 2: Set a new value for a CSS variable
root.style.setProperty('--primary-color', 'coral');
```

**What happens:** Every single element on the page that uses `var(--primary-color)` instantly updates to `coral` — no page reload needed.

---

### Complete Interactive Example — Colour Switcher

Here is a complete working example. When the user clicks a button, JavaScript changes the CSS variable and the whole page updates instantly.

**HTML:**
```html
<!DOCTYPE html>
<html>
<head>
  <style>
    :root {
      --page-bg: #1e90ff;       /* global background: blue */
      --page-text: #ffffff;     /* global text: white */
    }

    body {
      background-color: var(--page-bg);
      color: var(--page-text);
      font-family: Arial, sans-serif;
      padding: 30px;
      transition: background-color 0.5s;  /* smooth colour change */
    }

    button {
      padding: 10px 20px;
      margin: 5px;
      cursor: pointer;
      font-size: 16px;
    }
  </style>
</head>
<body>
  <h1>CSS Variables Demo</h1>
  <p>Click a button to change the page colour scheme.</p>

  <button onclick="setTheme('blue')">Blue Theme</button>
  <button onclick="setTheme('green')">Green Theme</button>
  <button onclick="setTheme('dark')">Dark Theme</button>

  <script>
    function setTheme(theme) {
      // Get the root element
      var root = document.querySelector(':root');

      // Set variables based on chosen theme
      if (theme === 'blue') {
        root.style.setProperty('--page-bg', '#1e90ff');
        root.style.setProperty('--page-text', '#ffffff');
      } else if (theme === 'green') {
        root.style.setProperty('--page-bg', '#2e8b57');
        root.style.setProperty('--page-text', '#f0fff0');
      } else if (theme === 'dark') {
        root.style.setProperty('--page-bg', '#1a1a2e');
        root.style.setProperty('--page-text', '#e0e0e0');
      }
    }
  </script>
</body>
</html>
```

**Expected Behaviour:**

- Page starts with a blue background and white text
- Click "Green Theme" → background instantly changes to dark green, text to mint
- Click "Dark Theme" → background changes to near-black, text to light grey
- Click "Blue Theme" → returns to the original blue

**Why this is powerful:** All the colour rules (`body`, any headings, paragraphs, borders, etc.) could all reference the same two variables. Changing just those two variables from JavaScript updates the entire page in one moment.

---

### Reading and Displaying a Variable Value

```html
<button onclick="showColor()">Show Current Background Color</button>

<script>
  function showColor() {
    var root = document.querySelector(':root');
    var styles = getComputedStyle(root);
    var color = styles.getPropertyValue('--page-bg').trim();
    alert('Current background color variable: ' + color);
  }
</script>
```

**Expected Behaviour:** Clicking the button shows an alert like: `Current background color variable: #1e90ff`

> 🤔 **Think About This:** If you call `setProperty` to change `--page-bg`, then call `getPropertyValue` to read it — will you get the new value or the old one? Try it!

---

## Part 4 — CSS Variables in Media Queries

### What is a Media Query? (Quick Prerequisite)

A **media query** is a CSS technique that lets you apply different styles depending on the screen size or device type. For example:

```css
/* Default styles for all screens */
p { font-size: 16px; }

/* Extra styles ONLY on screens narrower than 600px (mobile) */
@media screen and (max-width: 600px) {
  p { font-size: 14px; }
}
```

This is how websites adapt their layout for phones, tablets, and desktops.

---

### Why Use CSS Variables Inside Media Queries?

Without variables, making something responsive means repeating and changing dozens of individual property values inside every media query. With variables, you just redefine the variables at the breakpoint — and everything that uses those variables updates automatically.

**The pattern:**

1. Define your variables globally in `:root` (for large screens)
2. Inside a media query, override those variables with new values (for small screens)
3. All your element rules stay unchanged — they still just say `var(--name)`

---

### Simple Example 1 — Responsive Font Sizing

```css
/* ✅ GLOBAL: Large screen font sizes */
:root {
  --heading-size: 48px;
  --body-size: 18px;
}

h1 { font-size: var(--heading-size); }
p  { font-size: var(--body-size); }

/* 📱 MOBILE: Override the variables for small screens */
@media screen and (max-width: 600px) {
  :root {
    --heading-size: 28px;   /* smaller heading for phones */
    --body-size: 14px;      /* smaller body text for phones */
  }
}
```

**Expected Result:**

- On desktop (wider than 600px): `h1` = 48px, `p` = 18px
- On mobile (600px or narrower): `h1` = 28px, `p` = 14px
- The `h1` and `p` CSS rules themselves never changed — only the variables changed

---

### Simple Example 2 — Responsive Spacing

```css
:root {
  --page-padding: 40px;      /* comfortable spacing on large screens */
  --card-gap: 20px;
}

.page-wrapper {
  padding: var(--page-padding);
}

.card-grid {
  gap: var(--card-gap);
}

/* Override for small screens */
@media screen and (max-width: 768px) {
  :root {
    --page-padding: 15px;    /* tighter on mobile */
    --card-gap: 10px;
  }
}
```

**Expected Result:**

- Large screens: wrapper has 40px padding, grid has 20px gap
- Mobile screens: wrapper has 15px padding, grid has 10px gap — all from changing two variable values

---

### Full Responsive Colour Theme Example

This is a practical, real-world pattern where variables control both layout AND colours across breakpoints:

```css
/* ===== GLOBAL VARIABLES (Desktop defaults) ===== */
:root {
  /* Colors */
  --bg-color: #f5f5f5;
  --text-color: #333333;
  --accent-color: #1e90ff;
  --card-bg: #ffffff;

  /* Layout */
  --container-width: 1100px;
  --sidebar-width: 260px;
  --content-padding: 30px;
  --font-size-base: 18px;
}

/* ===== ELEMENT RULES (unchanged across breakpoints) ===== */
body {
  background-color: var(--bg-color);
  color: var(--text-color);
  font-size: var(--font-size-base);
}

.container {
  max-width: var(--container-width);
  padding: var(--content-padding);
}

.sidebar {
  width: var(--sidebar-width);
  background-color: var(--card-bg);
}

.accent-button {
  background-color: var(--accent-color);
  color: white;
  padding: 10px 20px;
}

/* ===== TABLET breakpoint (768px) ===== */
@media screen and (max-width: 768px) {
  :root {
    --sidebar-width: 200px;       /* narrower sidebar on tablet */
    --content-padding: 20px;      /* less padding */
    --font-size-base: 16px;       /* slightly smaller font */
  }
}

/* ===== MOBILE breakpoint (480px) ===== */
@media screen and (max-width: 480px) {
  :root {
    --sidebar-width: 100%;        /* full-width sidebar stacks on mobile */
    --content-padding: 12px;      /* minimal padding */
    --font-size-base: 14px;       /* compact font */
    --bg-color: #ffffff;          /* cleaner white background on mobile */
  }
}
```

**Expected Result:**

- Desktop: wide container, 260px sidebar, 30px padding, 18px font, grey background
- Tablet: 200px sidebar, 20px padding, 16px font
- Mobile: full-width sidebar, 12px padding, 14px font, white background

**The key insight:** The `.sidebar`, `body`, `.container`, and `.accent-button` rules never changed. Only the variable values at the top changed at each breakpoint.

> 💡 **Real-World Tip:** This pattern — variables in `:root`, overrides in media queries — is how professional CSS design systems like those used at large companies are built. Change the variables, and the entire system adapts.

---

## Part 5 — Guided Practice Exercises

### Exercise 1 — Brand Colour System (Beginner)

**Objective:** Practice declaring and using global CSS variables.

**Scenario:** You are styling a simple webpage for a fictional company called "LeafCo" whose brand colour is `#2e8b57` (sea green).

**Your Task:**

1. Declare two global variables in `:root`:
   - `--brand-color` set to `#2e8b57`
   - `--brand-text` set to `#ffffff`
2. Use `var(--brand-color)` as the `background-color` for the `header`
3. Use `var(--brand-text)` as the `color` for `header h1`
4. Use `var(--brand-color)` as the `border-left` colour for all `blockquote` elements (4px solid)
5. Use `var(--brand-color)` as the text `color` for all `a` links

**Starter HTML:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* YOUR CSS HERE */
  </style>
</head>
<body>
  <header>
    <h1>Welcome to LeafCo</h1>
  </header>
  <main>
    <blockquote>We grow the best plants in the city.</blockquote>
    <p>Visit our <a href="#">online store</a> today.</p>
  </main>
</body>
</html>
```

**Expected Result:**

- Header has a green background with white heading
- The blockquote has a green left border
- The link text is green
- Changing `--brand-color` to `#8B0000` (dark red) updates all four elements at once

**Self-Check Questions:**
- Where did you declare the variables? (Should be inside `:root`)
- Can you change the entire colour scheme by editing just one line?

---

### Exercise 2 — Section Colour Override (Intermediate)

**Objective:** Practice local overrides of global variables.

**Scenario:** A blog website has a default card style (white background, blue accent). But the "Featured Posts" section should have a gold accent.

**Your Task:**

```css
:root {
  --card-bg: #ffffff;
  --card-accent: #1e90ff;   /* blue */
  --card-border-radius: 8px;
}

.card {
  background-color: var(--card-bg);
  border-left: 5px solid var(--card-accent);
  border-radius: var(--card-border-radius);
  padding: 20px;
  margin-bottom: 15px;
}

/* TODO: Add a rule for .featured-section that overrides
   --card-accent to gold (#FFD700)
   and --card-bg to #fffde7 (light yellow) */
```

**Expected Result:**

- Regular `.card` → white background, blue left border
- `.card` inside `.featured-section` → light yellow background, gold left border

**Hints:**
- Override the variables on `.featured-section`, not on `.card` itself
- You do NOT need to duplicate the `.card` rule

---

### Exercise 3 — JavaScript Theme Toggle (Intermediate)

**Objective:** Use JavaScript to read and change CSS variables.

**Scenario:** Build a simple "light mode / dark mode" toggle button.

**Starter Code:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    :root {
      --bg: #ffffff;
      --text: #333333;
      --card-bg: #f0f0f0;
    }

    body {
      background-color: var(--bg);
      color: var(--text);
      font-family: Arial, sans-serif;
      padding: 20px;
      transition: all 0.3s;
    }

    .card {
      background-color: var(--card-bg);
      padding: 20px;
      border-radius: 8px;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <button id="toggle-btn" onclick="toggleMode()">Switch to Dark Mode</button>

  <div class="card">
    <h2>Sample Card</h2>
    <p>This card will change colours when you toggle the mode.</p>
  </div>

  <script>
    var isDark = false;

    function toggleMode() {
      var root = document.querySelector(':root');
      var btn = document.getElementById('toggle-btn');

      if (!isDark) {
        // TODO: Set dark mode variables
        // --bg should become #1a1a2e
        // --text should become #e0e0e0
        // --card-bg should become #16213e
        btn.textContent = 'Switch to Light Mode';
        isDark = true;
      } else {
        // TODO: Set light mode variables (back to original values)
        btn.textContent = 'Switch to Dark Mode';
        isDark = false;
      }
    }
  </script>
</body>
</html>
```

**Your Task:** Fill in the TODO comments with the correct `root.style.setProperty(...)` calls.

**Expected Behaviour:**

- Starts in light mode (white background)
- Clicking the button switches to dark mode (dark blue tones)
- Clicking again returns to light mode

---

## Part 6 — Mini Project: "StyleConfig" — A Fully Themeable Webpage

### Project Overview

You will build a simple single-page website for a fictional café called **"The Bean Scene"**. The page will:

- Use CSS variables for all colours, fonts, and spacing
- Override variables for different sections (hero, menu, footer)
- Include a JavaScript theme switcher (Day Mode / Night Mode)
- Update its layout variables for mobile screens via media queries

### Stage 1 — Setup: Define Your Design Tokens

In CSS, "design tokens" are just what professionals call the set of global variables that define your visual design system.

```css
:root {
  /* ===== COLOURS ===== */
  --color-primary: #6b4226;       /* coffee brown */
  --color-secondary: #d4a96a;     /* warm caramel */
  --color-bg: #fdf6ec;            /* creamy off-white */
  --color-text: #3e2723;          /* dark espresso */
  --color-text-light: #ffffff;
  --color-card-bg: #ffffff;
  --color-border: #e0c9a6;

  /* ===== TYPOGRAPHY ===== */
  --font-size-base: 16px;
  --font-size-large: 24px;
  --font-size-hero: 48px;

  /* ===== SPACING ===== */
  --padding-section: 60px 40px;
  --padding-card: 25px;
  --gap-cards: 20px;

  /* ===== SHAPES ===== */
  --border-radius: 10px;
}
```

**Milestone 1 Output:** `:root` block with all design token variables defined.

---

### Stage 2 — Core Layout and Sections

```css
/* ===== RESET ===== */
* { margin: 0; padding: 0; box-sizing: border-box; }

body {
  font-family: Georgia, serif;
  font-size: var(--font-size-base);
  background-color: var(--color-bg);
  color: var(--color-text);
  line-height: 1.7;
}

/* ===== NAVIGATION ===== */
nav {
  background-color: var(--color-primary);
  color: var(--color-text-light);
  padding: 15px 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

nav a {
  color: var(--color-secondary);
  text-decoration: none;
  font-size: 18px;
  margin-left: 20px;
}

/* ===== HERO SECTION — overrides for a dramatic look ===== */
.hero {
  --color-bg: var(--color-primary);           /* hero background: coffee brown */
  --color-text: var(--color-text-light);      /* hero text: white */
  background-color: var(--color-bg);
  color: var(--color-text);
  padding: var(--padding-section);
  text-align: center;
}

.hero h1 {
  font-size: var(--font-size-hero);
  color: var(--color-secondary);             /* caramel headline */
  margin-bottom: 15px;
}

/* ===== MENU CARDS ===== */
.menu-section {
  padding: var(--padding-section);
}

.menu-section h2 {
  font-size: var(--font-size-large);
  color: var(--color-primary);
  text-align: center;
  margin-bottom: 30px;
}

.menu-grid {
  display: flex;
  flex-wrap: wrap;
  gap: var(--gap-cards);
  justify-content: center;
}

.menu-card {
  background-color: var(--color-card-bg);
  border: 1px solid var(--color-border);
  border-radius: var(--border-radius);
  padding: var(--padding-card);
  width: 240px;
}

.menu-card h3 {
  color: var(--color-primary);
  margin-bottom: 10px;
}

.menu-card .price {
  color: var(--color-secondary);
  font-size: 20px;
  font-weight: bold;
}

/* ===== FOOTER — overrides for a dark footer ===== */
footer {
  --color-bg: var(--color-text);             /* dark espresso background */
  --color-text: var(--color-text-light);     /* white text in footer */
  background-color: var(--color-bg);
  color: var(--color-text);
  text-align: center;
  padding: 30px;
  font-size: 14px;
}

footer a {
  color: var(--color-secondary);
}
```

**Milestone 2 Output:** A styled café page with brown navigation, a dark hero, card-based menu, and a dark footer. Hero and footer colours are controlled by local variable overrides.

---

### Stage 3 — JavaScript Night Mode Switcher

Add a button to the `nav` and the following script:

```html
<!-- In your nav -->
<button id="night-toggle" onclick="toggleNight()">🌙 Night Mode</button>

<script>
  var nightMode = false;

  function toggleNight() {
    var root = document.querySelector(':root');
    var btn = document.getElementById('night-toggle');

    if (!nightMode) {
      /* Switch to night mode */
      root.style.setProperty('--color-bg', '#1a0a00');           /* very dark brown */
      root.style.setProperty('--color-text', '#f5deb3');         /* wheat colour */
      root.style.setProperty('--color-card-bg', '#2d1206');       /* dark card background */
      root.style.setProperty('--color-border', '#5a3010');
      btn.textContent = '☀️ Day Mode';
      nightMode = true;
    } else {
      /* Switch back to day mode */
      root.style.setProperty('--color-bg', '#fdf6ec');
      root.style.setProperty('--color-text', '#3e2723');
      root.style.setProperty('--color-card-bg', '#ffffff');
      root.style.setProperty('--color-border', '#e0c9a6');
      btn.textContent = '🌙 Night Mode';
      nightMode = false;
    }
  }
</script>
```

**Milestone 3 Output:** Clicking the button toggles the entire page between a warm light mode and a dark-roast night mode. Cards, text, background — everything updates because they all use variables.

---

### Stage 4 — Responsive Media Queries

Add this to the bottom of your CSS:

```css
/* ===== TABLET ===== */
@media screen and (max-width: 768px) {
  :root {
    --font-size-hero: 34px;
    --font-size-base: 15px;
    --padding-section: 40px 20px;
    --gap-cards: 15px;
  }
}

/* ===== MOBILE ===== */
@media screen and (max-width: 480px) {
  :root {
    --font-size-hero: 26px;
    --font-size-base: 14px;
    --padding-section: 25px 12px;
    --gap-cards: 10px;
  }

  .menu-card {
    width: 100%;    /* cards go full-width on mobile */
  }
}
```

**Milestone 4 Output:** The page gracefully shrinks text and padding on smaller screens, purely through variable overrides. The layout rules themselves never needed to change.

---

### Final Project Reflection Questions

1. If the café wanted to rebrand from coffee brown to ocean blue, how many lines of CSS would you need to change?
2. How does the night mode work — where exactly in the code does the colour change happen?
3. Why does the footer still look dark even in night mode? (Hint: look at the footer's local variable overrides)
4. What would break if you removed all the `var()` calls and hard-coded the values directly?

---

## Part 7 — Common Beginner Mistakes

### Mistake 1: Forgetting the Double Dash

```css
/* ❌ WRONG — only one dash */
:root {
  -my-color: blue;
}

/* ✅ CORRECT — two dashes */
:root {
  --my-color: blue;
}
```

**Why:** CSS custom property names MUST start with `--`. A single dash is valid CSS but means something else (it could be a vendor prefix).

---

### Mistake 2: Forgetting `var()` When Using the Variable

```css
/* ❌ WRONG — writing the variable name directly */
h1 {
  color: --my-color;    /* CSS does NOT do this */
}

/* ✅ CORRECT — using the var() function */
h1 {
  color: var(--my-color);
}
```

**Why:** CSS variables are not automatically expanded. You must explicitly call `var()` to insert the value.

---

### Mistake 3: Trying to Use a Variable Before Declaring It

```css
/* ❌ WRONG — using it before declaring it */
h1 {
  color: var(--brand);
}

:root {
  --brand: purple;    /* declared after use */
}
```

**Result:** This actually works in CSS because `:root` is processed first regardless of order, but it is bad practice and confusing. Always declare variables in `:root` at the TOP of your stylesheet.

---

### Mistake 4: Using a Variable in the Wrong Scope

```css
/* ❌ MISTAKE — variable declared in child, used in sibling or parent */
.card-footer {
  --footer-bg: lightgrey;
}

.card-header {
  background-color: var(--footer-bg);   /* ❌ .card-header cannot see .card-footer's variable */
}
```

**Fix:** Move the variable to the shared parent element, or to `:root`.

---

### Mistake 5: Wrong JavaScript Method Name

```javascript
/* ❌ WRONG */
root.setProperty('--color', 'red');          /* not a method on the element */
root.style.getProperty('--color');           /* wrong name — it's getPropertyValue */

/* ✅ CORRECT */
root.style.setProperty('--color', 'red');
getComputedStyle(root).getPropertyValue('--color');
```

---

### Mistake 6: Forgetting getComputedStyle When Reading Variables

```javascript
/* ❌ WRONG — this reads inline styles only, not :root CSS variables */
var color = root.style.getPropertyValue('--color');   /* likely returns empty string */

/* ✅ CORRECT — use getComputedStyle to read all applied styles */
var color = getComputedStyle(root).getPropertyValue('--color');
```

**Why:** `root.style` only contains inline styles. CSS variables declared in a stylesheet are only visible through `getComputedStyle`.

---

### Mistake 7: Media Query Override Not in `:root`

```css
/* ❌ WRONG — variable declared on body, but elements inherit from :root */
@media (max-width: 600px) {
  body {
    --font-size: 14px;    /* ⚠️ This might not reach all elements */
  }
}

/* ✅ CORRECT — override in :root for reliable global reach */
@media (max-width: 600px) {
  :root {
    --font-size: 14px;    /* ✅ All elements can see this */
  }
}
```

---

## Reflection Questions

Test your understanding by thinking through these questions:

1. You have a variable `--spacing` set to `20px` in `:root`. You also set `--spacing: 10px` inside `.sidebar`. A `<div>` inside `.sidebar` uses `padding: var(--spacing)`. What padding will it have?

2. What is the difference between declaring `--color: red` in `:root` versus declaring it inside `button {}`?

3. You call `root.style.setProperty('--bg', 'navy')` in JavaScript. Which elements will change? Only those with `var(--bg)`, or all elements?

4. Why is `var(--color, black)` better than just `var(--color)` for critical properties?

5. If you wanted the font sizes to change on phones but keep all other variables the same, where exactly would you add the new variable values?

6. Can you use `var()` inside another `var()`? For example: `var(--size, var(--default-size))`? (Answer: Yes! This is a valid and useful pattern for nested fallbacks.)

---

## Completion Checklist

Before moving on, make sure you can say "yes" to each item:

- [ ] I understand what a CSS variable is and why it is useful
- [ ] I can declare a global variable in `:root` using the `--name: value` syntax
- [ ] I can declare a local variable inside a specific selector
- [ ] I can use `var(--name)` to insert a variable's value into any CSS property
- [ ] I can use `var(--name, fallback)` to provide a fallback value
- [ ] I understand that local variables override global ones for their element and children
- [ ] I can use `getComputedStyle(root).getPropertyValue('--name')` to read a variable from JavaScript
- [ ] I can use `root.style.setProperty('--name', 'value')` to change a variable from JavaScript
- [ ] I can override `:root` variables inside a `@media` query to create responsive designs
- [ ] I completed the mini-project (or am confident I could)
- [ ] I know at least 3 common mistakes and how to avoid them

---

## Lesson Summary

CSS Variables (custom properties) are a modern CSS feature that lets you store reusable values under meaningful names beginning with `--`. They are declared inside any CSS selector using the `--name: value` syntax, and retrieved anywhere with the `var(--name)` function.

**Key rules to remember:**

- Variables declared in `:root` are **global** — visible to every element
- Variables declared inside a regular selector are **local** — visible only to that element and its children
- Local declarations **override** global ones for their scope
- The `var()` function accepts an optional **fallback**: `var(--color, black)`
- CSS variables have **DOM access**, meaning JavaScript can read them with `getComputedStyle(root).getPropertyValue('--name')` and write them with `root.style.setProperty('--name', 'value')`
- Variables can be overridden inside `@media` queries to create **responsive design systems** where a single `:root` variable change ripples across the entire layout

The professional pattern is: define all your design tokens (colours, spacing, font sizes) as variables in `:root`, use `var()` everywhere in your element rules, then override just the variables in media queries or via JavaScript — never the element rules themselves. This makes your entire stylesheet dramatically easier to maintain, update, and theme.

---

*End of Lesson 65 — CSS Variables: the var() Function, Overriding, JavaScript & Media Queries*
