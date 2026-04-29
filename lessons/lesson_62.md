---
render_with_liquid: false
title: "CSS Pagination — Building & Styling Page Navigation from Scratch"
nav_order: 62
---

# Lesson 62 — CSS Pagination: Building & Styling Page Navigation from Scratch

---

## Lesson Introduction

Have you ever visited a website with lots of articles, products, or search results and noticed a row of numbered buttons at the bottom of the page? Something like this:

```
« 1  2  3  4  5 »
```

That is called **pagination**. It is one of the most common navigation patterns on the web. In this lesson, you will learn exactly what pagination is, why every content-heavy website needs it, and how to build it yourself using only HTML and CSS — from a bare skeleton to a polished, interactive design.

By the end of this lesson you will be able to:

- Explain what pagination is and why it matters
- Build basic pagination HTML structure using lists and links
- Style page numbers with borders, colours, padding, and rounded corners
- Mark the currently active page
- Disable a button when needed
- Add hover effects and smooth transition animations
- Build breadcrumb navigation as an alternative pagination style
- Control pagination size and alignment
- Build a complete blog-style pagination component as a mini-project

---

## Prerequisite Concepts

Before we dive in, let's make sure you understand a few CSS ideas that pagination relies on heavily.

### What Is an Unordered List (`<ul>`)?

An **unordered list** is an HTML element that holds a group of items. Each item is wrapped in a `<li>` (list item) tag. By default, the browser shows a bullet point before each item.

```html
<ul>
  <li>Apple</li>
  <li>Banana</li>
  <li>Cherry</li>
</ul>
```

**Expected output in browser:**
```
• Apple
• Banana
• Cherry
```

We use `<ul>` for pagination because page numbers are naturally a list of choices.

---

### What Is `display: inline` and `display: flex`?

By default, `<li>` items stack **vertically** (one below the other). For pagination we want them side by side **horizontally**. We have two common solutions:

**Option A — `display: inline` on `<li>`:**
```css
ul li {
  display: inline; /* each item sits beside the next */
}
```

**Option B — `display: flex` on the `<ul>`:**
```css
ul {
  display: flex; /* all items line up in a row */
}
```

Think of `flex` as giving the container a magic ruler — it lines all its children up in a neat row automatically.

---

### What Is `padding`?

Padding is the **breathing room inside** an element, between its content and its border.

```css
a {
  padding: 8px 16px;
  /* 8px top/bottom, 16px left/right */
}
```

This makes your links look more like clickable buttons rather than tiny text.

---

### What Is `text-decoration: none`?

By default, links (`<a>` tags) have an underline. For pagination we want clean buttons — so we remove the underline:

```css
a {
  text-decoration: none; /* removes the underline */
}
```

---

### What Is `border-radius`?

`border-radius` rounds the corners of an element.

```css
a {
  border-radius: 5px;   /* slightly rounded */
}
a {
  border-radius: 50%;   /* fully circular (for icons) */
}
```

Think of `border-radius` as a tiny circular eraser rubbing away the sharp corners of a rectangle.

---

## Part 1 — What Is Pagination and Why Does It Exist?

### The Problem Pagination Solves

Imagine a news website with 500 articles. If you tried to show all 500 articles on one page, the page would take forever to load and be impossible to scroll through. Pagination solves this by splitting content into separate pages and giving users numbered links to navigate between them.

**Real-world examples of pagination:**
- Google Search results — "Page 1 of about 4,230,000 results"
- Amazon product listings — page 1, 2, 3...
- Blog archives — "Older posts" / "Newer posts"
- Database admin tools — showing 50 rows per page

### The Anatomy of a Pagination Bar

A complete pagination bar has these parts:

```
«  1  2  3  4  5  »
↑                  ↑
Previous           Next
button             button
      ↑
   Page numbers
   (currently active = highlighted)
```

The `«` symbol is the "previous page" arrow and `»` is the "next page" arrow. These are called **HTML entities** — special codes for symbols.

| Symbol | HTML Entity | Meaning |
|--------|-------------|---------|
| `«`    | `&laquo;`   | Previous arrow (double left chevron) |
| `»`    | `&raquo;`   | Next arrow (double right chevron) |
| `‹`    | `&lsaquo;`  | Single left arrow |
| `›`    | `&rsaquo;`  | Single right arrow |

---

## Part 2 — Building the HTML Structure

### Step 1: The Bare HTML Skeleton

Pagination is built using an **unordered list** (`<ul>`) where each **list item** (`<li>`) holds a **link** (`<a>`).

```html
<ul class="pagination">
  <li><a href="#">&laquo;</a></li>
  <li><a href="#">1</a></li>
  <li><a href="#">2</a></li>
  <li><a href="#">3</a></li>
  <li><a href="#">4</a></li>
  <li><a href="#">5</a></li>
  <li><a href="#">&raquo;</a></li>
</ul>
```

**Line-by-line explanation:**

- `<ul class="pagination">` — Creates an unordered list. The class `pagination` lets us target it with CSS.
- `<li>` — Each list item holds one page button.
- `<a href="#">` — A link. The `#` means "go nowhere" for now. In a real site this would be `page2.html` etc.
- `&laquo;` — The `«` left-arrow symbol (previous button).
- `&raquo;` — The `»` right-arrow symbol (next button).

**What this looks like without CSS:**
```
• «
• 1
• 2
• 3
• 4
• 5
• »
```

It's vertical and boring — that's normal. CSS will transform it completely.

---

### Step 2: Adding the Base CSS

Now let's style it so the items sit in a row and look like buttons.

```css
/* The container — row layout, centred, no bullets */
.pagination {
  display: flex;            /* line all items in a row */
  justify-content: center;  /* centre the whole bar on the page */
  list-style: none;         /* remove bullet points */
  padding: 0px;             /* remove default list padding */
}

/* Each page link */
.pagination li a {
  display: block;           /* let the link fill the entire list item */
  padding: 8px 12px;        /* space inside each button */
  text-decoration: none;    /* remove underline */
  border: 1px solid gray;   /* thin gray border around each button */
  color: black;             /* black text */
  margin: 0 4px;            /* small gap between buttons */
  border-radius: 5px;       /* slightly rounded corners */
}
```

**Complete example to test:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .pagination {
      display: flex;
      justify-content: center;
      list-style: none;
      padding: 0px;
    }
    .pagination li a {
      display: block;
      padding: 8px 12px;
      text-decoration: none;
      border: 1px solid gray;
      color: black;
      margin: 0 4px;
      border-radius: 5px;
    }
  </style>
</head>
<body>
  <ul class="pagination">
    <li><a href="#">&laquo;</a></li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#">3</a></li>
    <li><a href="#">4</a></li>
    <li><a href="#">5</a></li>
    <li><a href="#">&raquo;</a></li>
  </ul>
</body>
</html>
```

**Expected output:**
```
[ « ]  [ 1 ]  [ 2 ]  [ 3 ]  [ 4 ]  [ 5 ]  [ » ]
```

All buttons are in a horizontal row, centred, with rounded borders and equal spacing.

> **Thinking Prompt:** What happens if you remove `list-style: none`? Try it and observe the bullet points appearing inside the buttons!

---

## Part 3 — Marking the Active Page

### What Is the Active Page?

When a user is currently on page 3, page 3's button should look different — highlighted in a special colour — so the user always knows where they are. This is the **active page**.

We use a CSS class called `.active` to mark it.

### Adding the Active Class in HTML

Add `class="active"` to the `<a>` tag of the current page:

```html
<ul class="pagination">
  <li><a href="#">&laquo;</a></li>
  <li><a href="#">1</a></li>
  <li><a href="#">2</a></li>
  <li><a href="#" class="active">3</a></li>  <!-- CURRENT PAGE -->
  <li><a href="#">4</a></li>
  <li><a href="#">5</a></li>
  <li><a href="#">&raquo;</a></li>
</ul>
```

### Styling the Active Page in CSS

```css
.pagination li a.active {
  background-color: #4CAF50;  /* green background */
  color: white;               /* white text */
}
```

**Complete Example with Active Page:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .pagination {
      display: flex;
      justify-content: center;
      list-style: none;
      padding: 0px;
    }
    .pagination li a {
      display: block;
      padding: 8px 12px;
      text-decoration: none;
      border: 1px solid gray;
      color: black;
      margin: 0 4px;
      border-radius: 5px;
    }
    .pagination li a.active {
      background-color: #4CAF50;
      color: white;
    }
  </style>
</head>
<body>
  <ul class="pagination">
    <li><a href="#">&laquo;</a></li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#" class="active">3</a></li>
    <li><a href="#">4</a></li>
    <li><a href="#">5</a></li>
    <li><a href="#">&raquo;</a></li>
  </ul>
</body>
</html>
```

**Expected output:**
```
[ « ]  [ 1 ]  [ 2 ]  [ 3 (green) ]  [ 4 ]  [ 5 ]  [ » ]
```

Page 3 is now visually highlighted in green with white text.

> **Thinking Prompt:** What would happen if you gave the `.active` class to two pages at once? When would that make sense?

---

## Part 4 — The Disabled State

### What Is a Disabled Button?

When the user is on the **last page**, the "Next »" button should not be clickable — because there is no next page. We visually grey it out using a `.disabled` class.

### The Three Properties for Disabled State

```css
.pagination li a.disabled {
  color: #dddddd;         /* light grey text — looks faded */
  cursor: not-allowed;    /* shows a "no" cursor icon when hovering */
  pointer-events: none;   /* completely blocks all mouse clicks */
}
```

**Explanation of each property:**
- `color: #dddddd` — Makes the text nearly invisible, signalling "this is inactive".
- `cursor: not-allowed` — When the user hovers over the button, their cursor changes to a circle with a line through it (🚫), visually communicating "you can't click this".
- `pointer-events: none` — Completely disables all mouse interaction — clicking does absolutely nothing.

### Full Example with Both Active and Disabled:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .pagination {
      display: flex;
      justify-content: center;
      list-style: none;
      padding: 0px;
    }
    .pagination li a {
      display: block;
      padding: 8px 12px;
      text-decoration: none;
      border: 1px solid gray;
      color: black;
      margin: 0 4px;
      border-radius: 5px;
    }
    .pagination li a.active {
      background-color: #4CAF50;
      color: white;
    }
    .pagination li a.disabled {
      color: #dddddd;
      cursor: not-allowed;
      pointer-events: none;
    }
  </style>
</head>
<body>
  <ul class="pagination">
    <li><a href="#">&laquo;</a></li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#">3</a></li>
    <li><a href="#">4</a></li>
    <li><a href="#" class="active">5</a></li>
    <li><a href="#" class="disabled">&raquo;</a></li>  <!-- DISABLED -->
  </ul>
</body>
</html>
```

**Expected output:**
```
[ « ]  [ 1 ]  [ 2 ]  [ 3 ]  [ 4 ]  [ 5 (green) ]  [ » (grey, unclickable) ]
```

The user is on the last page (page 5), so the Next button is greyed out and cannot be clicked.

---

## Part 5 — Hover Effects

### Why Hover Effects Matter

A good hover effect gives the user instant visual feedback when they move their mouse over a button. Without it, the user isn't sure if they can click or what will happen. With it, the interface feels alive and responsive.

### The `:hover` Selector

The `:hover` pseudo-class applies styles when the mouse is over an element.

```css
.pagination li a:hover {
  background-color: #ddd;   /* light grey on hover */
}
```

### Hover Only on Non-Active Links

We don't want the active page button to change colour when hovered — it should always keep its active green colour. We use `:not(.active)` to exclude it:

```css
.pagination li a:hover:not(.active) {
  background-color: #ddd;
}
```

**Reading this like English:** "Apply this background colour when hovering, BUT NOT if the element also has the `.active` class."

### Complete Hover Example:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .pagination {
      display: flex;
      justify-content: center;
      list-style: none;
      padding: 0px;
    }
    .pagination li a {
      display: block;
      padding: 8px 12px;
      text-decoration: none;
      border: 1px solid gray;
      color: black;
      margin: 0 4px;
      border-radius: 5px;
    }
    .pagination li a.active {
      background-color: #4CAF50;
      color: white;
    }
    /* Hover: grey background on all NON-active links */
    .pagination li a:hover:not(.active) {
      background-color: #ddd;
    }
  </style>
</head>
<body>
  <ul class="pagination">
    <li><a href="#">&laquo;</a></li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#" class="active">3</a></li>
    <li><a href="#">4</a></li>
    <li><a href="#">5</a></li>
    <li><a href="#">&raquo;</a></li>
  </ul>
</body>
</html>
```

**Expected behaviour:**
- Hovering over pages 1, 2, 4, 5, «, or » → grey background appears.
- Hovering over page 3 (active) → no change. It stays green.

---

## Part 6 — Smooth Transitions

### What Is a CSS Transition?

A **transition** makes a style change happen gradually over time instead of instantly. Without a transition, clicking or hovering causes an instant "snap". With a transition, the colour fades in smoothly — which looks much more professional.

### The `transition` Property

```css
a {
  transition: background-color 1s;
  /* property   duration */
}
```

- `background-color` — What property to animate (the background colour change).
- `1s` — How long the animation takes (1 second). You can also use `0.3s` for a quicker, snappier feel.

### Example with Hover + Transition:

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .pagination {
      display: flex;
      justify-content: center;
      list-style: none;
      padding: 0px;
    }
    .pagination li a {
      display: block;
      padding: 8px 12px;
      text-decoration: none;
      border: 1px solid gray;
      color: black;
      margin: 0 4px;
      border-radius: 5px;
      transition: background-color 0.3s;  /* smooth 0.3-second colour change */
    }
    .pagination li a.active {
      background-color: #4CAF50;
      color: white;
    }
    .pagination li a:hover:not(.active) {
      background-color: #ddd;
    }
  </style>
</head>
<body>
  <ul class="pagination">
    <li><a href="#">&laquo;</a></li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#" class="active">3</a></li>
    <li><a href="#">4</a></li>
    <li><a href="#">5</a></li>
    <li><a href="#">&raquo;</a></li>
  </ul>
</body>
</html>
```

**Expected behaviour:** Hovering over any non-active button causes the background to smoothly fade to grey over 0.3 seconds. Moving the mouse away fades it back.

> **Thinking Prompt:** What happens if you change `0.3s` to `3s`? Try it — does the slow fade feel comfortable or annoying for a navigation element?

---

## Part 7 — Pagination Size

### Changing the Size with `font-size`

You can make your entire pagination bar larger or smaller just by adjusting the `font-size` on the link elements:

```css
.pagination li a {
  font-size: 20px;    /* larger text = larger buttons */
}
```

Since `padding` is measured in `px`, you may also want to increase that for larger buttons:

```css
.pagination li a {
  font-size: 22px;
  padding: 12px 20px;
}
```

### Example — Large Pagination:

```html
<style>
  .pagination {
    display: flex;
    justify-content: center;
    list-style: none;
    padding: 0;
  }
  .pagination li a {
    display: block;
    padding: 12px 20px;
    font-size: 22px;
    text-decoration: none;
    border: 1px solid gray;
    color: black;
    margin: 0 4px;
    border-radius: 5px;
  }
  .pagination li a.active {
    background-color: #4CAF50;
    color: white;
  }
  .pagination li a:hover:not(.active) {
    background-color: #ddd;
  }
</style>
```

**Expected output:**
Larger, more touch-friendly buttons — great for mobile designs.

---

## Part 8 — Centring the Pagination Bar

### Two Methods for Centring

**Method 1 — `justify-content: center` on the flex container (already covered):**

This works when `display: flex` is used on the `<ul>`.

**Method 2 — Wrap in a container and use `text-align: center`:**

If you use `display: inline-block` on the pagination instead of flex, wrap it in a `<div>` and set `text-align: center`:

```html
<div class="center">
  <ul class="pagination">
    <!-- page links here -->
  </ul>
</div>
```

```css
div.center {
  text-align: center;
}

.pagination {
  display: inline-block;
  padding: 0;
  margin: 0;
}

.pagination li {
  display: inline;
}
```

Both methods achieve the same visual result — a centred pagination bar.

---

## Part 9 — Adding Spacing Between Buttons

By default, when using `display: flex`, pagination buttons might appear grouped together with no gap. The `margin` property adds space around each button.

```css
.pagination li a {
  margin: 0 4px;
  /* 0px top/bottom spacing, 4px left/right spacing */
}
```

- `0` — No space above or below.
- `4px` — 4 pixels of space to the left and right of each button.

This creates clear visual separation between each page number, making it much easier to click individual buttons.

---

## Part 10 — The Breadcrumb: A Different Kind of Pagination

### What Is a Breadcrumb?

A **breadcrumb** is a trail of links showing the user's location within a website's hierarchy. It takes its name from the Hansel and Gretel fairy tale, where the children left bread crumbs on the path to find their way home.

Example breadcrumb trail:
```
Home / Shop / Electronics / Phones / iPhone 15
```

Each step shows where you are in the site structure. Clicking any step takes you back up to that level.

### When to Use Breadcrumbs

- Online shops with categories and sub-categories (e.g. Clothing > Men > Jackets)
- Documentation sites with sections and sub-sections
- Photo galleries (e.g. Gallery > Summer 2024 > Paris)

### Building a CSS Breadcrumb

The HTML structure is the same as pagination — a `<ul>` with `<li>` items. The difference is in the CSS styling.

```html
<ul class="breadcrumb">
  <li><a href="#">Home</a></li>
  <li><a href="#">Blog</a></li>
  <li><a href="#">Technology</a></li>
  <li>CSS Pagination</li>  <!-- current page — no link needed -->
</ul>
```

```css
ul.breadcrumb {
  padding: 8px 16px;           /* inner space */
  list-style: none;            /* no bullet points */
  background-color: #eee;      /* light grey bar */
}

ul.breadcrumb li {
  display: inline;             /* all items in a row */
}

ul.breadcrumb li a {
  color: green;                /* green link colour */
  text-decoration: none;       /* no underline */
}

/* Add a "/" separator between each item (except the first) */
ul.breadcrumb li + li::before {
  padding: 8px;
  color: black;
  content: "/\00a0";           /* "/" followed by a non-breaking space */
}
```

**Breaking down the separator selector:**

```css
ul.breadcrumb li + li::before
```

- `li + li` — Target every `<li>` that immediately follows another `<li>` (i.e., every item except the first).
- `::before` — Insert content BEFORE this element.
- `content: "/\00a0"` — The slash `/` plus `\00a0` which is the Unicode code for a non-breaking space (prevents the space from collapsing).

**Complete Breadcrumb Example:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    ul.breadcrumb {
      padding: 8px 16px;
      list-style: none;
      background-color: #eee;
    }
    ul.breadcrumb li {
      display: inline;
    }
    ul.breadcrumb li a {
      color: green;
      text-decoration: none;
    }
    ul.breadcrumb li + li::before {
      padding: 8px;
      color: black;
      content: "/\00a0";
    }
  </style>
</head>
<body>
  <ul class="breadcrumb">
    <li><a href="#">Home</a></li>
    <li><a href="#">Blog</a></li>
    <li><a href="#">Technology</a></li>
    <li>CSS Pagination</li>
  </ul>
</body>
</html>
```

**Expected output:**
```
Home / Blog / Technology / CSS Pagination
```

The items appear on a light grey bar, separated by slashes, with green links.

> **Thinking Prompt:** What would happen if you changed the `/` separator to `>` or `→`? Try modifying `content: "/\00a0"` to `content: "> "` and see the result.

---

## Part 11 — Previous / Next Navigation Only

Sometimes instead of numbered pages, a website simply uses "Previous" and "Next" buttons — common on blogs or articles where you just go one step at a time.

```html
<ul class="pagination">
  <li><a href="#">&laquo; Previous</a></li>
  <li><a href="#">Next &raquo;</a></li>
</ul>
```

```css
.pagination {
  display: flex;
  list-style: none;
  padding: 0;
}

.pagination li a {
  display: block;
  padding: 10px 18px;
  text-decoration: none;
  border: 1px solid gray;
  color: black;
  border-radius: 5px;
  margin: 0 4px;
  transition: background-color 0.3s;
}

.pagination li a:hover {
  background-color: #ddd;
}
```

**Expected output:**
```
[ « Previous ]  [ Next » ]
```

A clean two-button navigation bar suitable for single articles or blog posts.

---

## Guided Practice Exercises

### Exercise 1 — Build a Simple 5-Page Pagination

**Objective:** Create a basic pagination bar showing pages 1–5 with previous and next arrows.

**Scenario:** You are building a blog that has 5 pages. Page 2 is currently active.

**Steps:**
1. Create a new HTML file called `pagination_exercise1.html`.
2. Add a `<ul class="pagination">` with 7 list items: `«`, `1`, `2`, `3`, `4`, `5`, `»`.
3. Give page 2's link the class `active`.
4. Style with `display: flex`, centred, with borders and rounded corners.
5. Add a hover effect.

**Hints:**
- The `<ul>` needs `display: flex` and `justify-content: center` and `list-style: none`.
- Each `<a>` needs `display: block`, `padding`, `border`, `border-radius`, `text-decoration: none`.
- The active class needs `background-color` and `color: white`.

**Expected Output:**
```
[ « ]  [ 1 ]  [ 2 (green) ]  [ 3 ]  [ 4 ]  [ 5 ]  [ » ]
```

**Self-check questions:**
- Does page 2 look visually different from the rest?
- Do all buttons have equal spacing?
- Does the bar appear centred on the page?

---

### Exercise 2 — Last Page with Disabled Next Button

**Objective:** Show a 5-page pagination where the user is on page 5, so the "Next" button is disabled.

**Scenario:** A student record system shows 5 pages. The user reached the last page.

**Steps:**
1. Build the same 5-page pagination as Exercise 1.
2. Move the `.active` class to page 5.
3. Add class `disabled` to the `»` link.
4. Style `.disabled` with `color: #ddd`, `cursor: not-allowed`, and `pointer-events: none`.

**Expected Output:**
```
[ « ]  [ 1 ]  [ 2 ]  [ 3 ]  [ 4 ]  [ 5 (green) ]  [ » (greyed, unclickable) ]
```

**Optional What-If Challenge:** What if the user is on page 1? Which button should be disabled then?

---

### Exercise 3 — Breadcrumb Navigation

**Objective:** Build a breadcrumb trail for a university website.

**Scenario:** A student is navigating: `Home > Courses > Computer Science > CSS Fundamentals`.

**Steps:**
1. Create a `<ul class="breadcrumb">` with 4 items.
2. Give the first three items `<a>` tags (they are clickable links).
3. The fourth item (current page) has no link — just plain text.
4. Style using the breadcrumb CSS from Part 10.

**Expected Output:**
```
Home / Courses / Computer Science / CSS Fundamentals
```

**Self-check questions:**
- Do the slashes appear automatically between items?
- Does the first item have NO slash before it?
- Is the last item (current page) not a hyperlink?

---

### Exercise 4 — Pagination with Transition

**Objective:** Add a smooth transition effect to your pagination hover.

**Steps:**
1. Start with your Exercise 1 pagination.
2. Add `transition: background-color 0.3s;` to the `<a>` element styles.
3. Test in a browser — hover over different page numbers and observe the smooth colour fade.

**Optional What-If Challenge:** Change `0.3s` to `2s`. Is the effect still pleasant? What's the "sweet spot" for UI transitions?

---

## Mini Project — Blog Pagination Component

### Project Goal

Build a complete, ready-to-use blog pagination component that includes:
- Numbered page buttons (1–8)
- An active page marker
- A disabled Next button (because we're on the last page)
- Hover effects with smooth transitions
- A breadcrumb trail above the pagination

---

### Stage 1: Setup — The HTML Skeleton

Create a file called `blog_pagination.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Blog Pagination</title>
  <style>
    /* CSS will go here */
  </style>
</head>
<body>
  <h2>My Tech Blog</h2>

  <!-- BREADCRUMB -->
  <ul class="breadcrumb">
    <li><a href="#">Home</a></li>
    <li><a href="#">Blog</a></li>
    <li>Page 8</li>
  </ul>

  <!-- ARTICLE PREVIEWS (placeholder) -->
  <p>... article summaries would appear here ...</p>

  <!-- PAGINATION BAR -->
  <ul class="pagination">
    <li><a href="#">&laquo;</a></li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#">3</a></li>
    <li><a href="#">4</a></li>
    <li><a href="#">5</a></li>
    <li><a href="#">6</a></li>
    <li><a href="#">7</a></li>
    <li><a href="#" class="active">8</a></li>
    <li><a href="#" class="disabled">&raquo;</a></li>
  </ul>

</body>
</html>
```

**Milestone 1 Output:** Plain unstyled HTML — vertical list with bullets. This is expected at this stage.

---

### Stage 2: Core Logic — Styling the Pagination

Inside the `<style>` block, add:

```css
/* ---- BREADCRUMB ---- */
ul.breadcrumb {
  padding: 8px 16px;
  list-style: none;
  background-color: #f0f0f0;
  border-radius: 4px;
  margin-bottom: 20px;
  font-size: 14px;
}
ul.breadcrumb li {
  display: inline;
}
ul.breadcrumb li a {
  color: #0066cc;
  text-decoration: none;
}
ul.breadcrumb li a:hover {
  text-decoration: underline;
}
ul.breadcrumb li + li::before {
  padding: 0 6px;
  color: #555;
  content: "/\00a0";
}

/* ---- PAGINATION ---- */
.pagination {
  display: flex;
  justify-content: center;
  list-style: none;
  padding: 20px 0;
  margin: 0;
}
.pagination li a {
  display: block;
  padding: 9px 14px;
  text-decoration: none;
  border: 1px solid #ccc;
  color: #333;
  margin: 0 3px;
  border-radius: 4px;
  font-size: 16px;
  transition: background-color 0.25s, color 0.25s;
}
.pagination li a.active {
  background-color: #2c7be5;
  color: white;
  border-color: #2c7be5;
}
.pagination li a:hover:not(.active) {
  background-color: #e8f0fe;
  color: #2c7be5;
  border-color: #2c7be5;
}
.pagination li a.disabled {
  color: #ccc;
  cursor: not-allowed;
  pointer-events: none;
  border-color: #eee;
}
```

**Milestone 2 Output:**
```
Home / Blog / Page 8

... article summaries would appear here ...

[ « ]  [ 1 ]  [ 2 ]  [ 3 ]  [ 4 ]  [ 5 ]  [ 6 ]  [ 7 ]  [ 8 (blue) ]  [ » (grey) ]
```

---

### Stage 3: Enhancements — Body Styling

Add these styles to make the overall page look polished:

```css
body {
  font-family: Arial, sans-serif;
  max-width: 800px;
  margin: 40px auto;
  padding: 0 20px;
  color: #333;
  background-color: #fafafa;
}
h2 {
  color: #1a1a2e;
  border-bottom: 2px solid #2c7be5;
  padding-bottom: 8px;
}
```

**Milestone 3 Output:** A centred, clean blog layout with a professional-looking pagination bar.

---

### Stage 4: Final Output — Complete Code

Here is the entire finished component:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Blog Pagination</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: 40px auto;
      padding: 0 20px;
      color: #333;
      background-color: #fafafa;
    }
    h2 {
      color: #1a1a2e;
      border-bottom: 2px solid #2c7be5;
      padding-bottom: 8px;
    }
    ul.breadcrumb {
      padding: 8px 16px;
      list-style: none;
      background-color: #f0f0f0;
      border-radius: 4px;
      margin-bottom: 20px;
      font-size: 14px;
    }
    ul.breadcrumb li {
      display: inline;
    }
    ul.breadcrumb li a {
      color: #0066cc;
      text-decoration: none;
    }
    ul.breadcrumb li a:hover {
      text-decoration: underline;
    }
    ul.breadcrumb li + li::before {
      padding: 0 6px;
      color: #555;
      content: "/\00a0";
    }
    .pagination {
      display: flex;
      justify-content: center;
      list-style: none;
      padding: 20px 0;
      margin: 0;
    }
    .pagination li a {
      display: block;
      padding: 9px 14px;
      text-decoration: none;
      border: 1px solid #ccc;
      color: #333;
      margin: 0 3px;
      border-radius: 4px;
      font-size: 16px;
      transition: background-color 0.25s, color 0.25s;
    }
    .pagination li a.active {
      background-color: #2c7be5;
      color: white;
      border-color: #2c7be5;
    }
    .pagination li a:hover:not(.active) {
      background-color: #e8f0fe;
      color: #2c7be5;
      border-color: #2c7be5;
    }
    .pagination li a.disabled {
      color: #ccc;
      cursor: not-allowed;
      pointer-events: none;
      border-color: #eee;
    }
  </style>
</head>
<body>

  <h2>My Tech Blog</h2>

  <ul class="breadcrumb">
    <li><a href="#">Home</a></li>
    <li><a href="#">Blog</a></li>
    <li>Page 8</li>
  </ul>

  <p>Showing articles 71–80 of 80 total articles...</p>

  <ul class="pagination">
    <li><a href="#">&laquo;</a></li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#">3</a></li>
    <li><a href="#">4</a></li>
    <li><a href="#">5</a></li>
    <li><a href="#">6</a></li>
    <li><a href="#">7</a></li>
    <li><a href="#" class="active">8</a></li>
    <li><a href="#" class="disabled">&raquo;</a></li>
  </ul>

</body>
</html>
```

**Final Milestone Output:**
- Centred blog page with heading and blue underline
- Breadcrumb trail: `Home / Blog / Page 8`
- Pagination bar with pages 1–8 centred at bottom
- Page 8 highlighted in blue
- Next button greyed and unclickable
- Smooth hover transitions on all other page buttons

---

### Reflection Questions

- What would you change if the user was on page 4 instead of page 8?
- How would you update this pagination if the blog grew to 20 pages?
- What property controls how smooth the hover animation feels?

### Optional Extensions

- Try making the first and last buttons (« and ») rounded differently from the number buttons using `:first-child` and `:last-child`.
- Try making the pagination bar full-width on mobile using a media query.
- Try changing the active button colour from blue to your favourite colour.

---

## Common Beginner Mistakes

### Mistake 1 — Forgetting `list-style: none`

If you forget to remove the bullet points, they appear inside or near your buttons.

```css
/* WRONG — bullets appear */
.pagination {
  display: flex;
}

/* CORRECT — bullets removed */
.pagination {
  display: flex;
  list-style: none;
  padding: 0;
}
```

---

### Mistake 2 — Putting the `.active` class on `<li>` instead of `<a>`

Since we target `.pagination li a.active`, the class must be on the `<a>` tag, not the `<li>`.

```html
<!-- WRONG — class on <li> -->
<li class="active"><a href="#">3</a></li>

<!-- CORRECT — class on <a> -->
<li><a href="#" class="active">3</a></li>
```

---

### Mistake 3 — Forgetting `display: block` on `<a>` Links

Without `display: block`, the padding on `<a>` tags won't fill the entire list item — the clickable area will be smaller than it looks.

```css
/* WRONG — padding doesn't fill the button properly */
.pagination li a {
  padding: 8px 12px;
}

/* CORRECT — display block makes the link fill its container */
.pagination li a {
  display: block;
  padding: 8px 12px;
}
```

---

### Mistake 4 — Using `cursor: not-allowed` Without `pointer-events: none`

`cursor: not-allowed` only changes the visual cursor — the link is still clickable! You need `pointer-events: none` to truly block the click.

```css
/* WRONG — cursor changes but link still works */
.disabled {
  cursor: not-allowed;
}

/* CORRECT — both visual AND functional disabled state */
.disabled {
  cursor: not-allowed;
  pointer-events: none;
  color: #ddd;
}
```

---

### Mistake 5 — Missing Hover Exclusion for Active Page

Without `:not(.active)`, the hover effect will change the active button's colour too — making it look like it's no longer active when hovered.

```css
/* WRONG — hover changes the active button's appearance */
.pagination li a:hover {
  background-color: #ddd;
}

/* CORRECT — active button is excluded from hover */
.pagination li a:hover:not(.active) {
  background-color: #ddd;
}
```

---

### Mistake 6 — Not Adding `padding: 0` to `<ul>`

Browsers have default padding on `<ul>` elements. If you don't reset it, your pagination may have unexpected left spacing.

```css
/* CORRECT */
.pagination {
  list-style: none;
  padding: 0;
  margin: 0;
}
```

---

## Reflection Questions

1. What is pagination and what real-world problem does it solve?
2. Why do we use a `<ul>` list for pagination instead of plain `<div>` elements?
3. What does `display: block` on an `<a>` tag achieve for pagination?
4. What is the difference between `cursor: not-allowed` and `pointer-events: none`?
5. How does `transition: background-color 0.3s` improve the user experience?
6. What is a breadcrumb and how is it different from numbered pagination?
7. What does the CSS selector `li + li::before` mean, and what does it add to a breadcrumb?
8. How would you make the pagination bar appear on the right side of the page instead of the centre?
9. What happens if you apply the `.active` class to two different page buttons at the same time?
10. How would you change the separator in a breadcrumb from `/` to `→`?

---

## Completion Checklist

Check each item off as you complete it:

- [ ] I can explain what pagination is and why websites use it
- [ ] I can write the HTML structure for a pagination bar using `<ul>` and `<li>`
- [ ] I can apply `display: flex` and `list-style: none` to create a horizontal bar
- [ ] I understand what `&laquo;` and `&raquo;` HTML entities produce
- [ ] I can add and style an `.active` class to highlight the current page
- [ ] I can add and style a `.disabled` class to grey out an unavailable button
- [ ] I can add hover effects using the `:hover` pseudo-class
- [ ] I can exclude the active button from hover using `:not(.active)`
- [ ] I can add smooth hover transitions using the `transition` property
- [ ] I can resize pagination using `font-size`
- [ ] I can centre pagination using `justify-content: center`
- [ ] I can add spacing between buttons using `margin`
- [ ] I can build a breadcrumb using `<ul>` and the `li + li::before` CSS selector
- [ ] I have completed all 4 guided exercises
- [ ] I have built the blog pagination mini-project from scratch

---

## Lesson Summary

In this lesson you learned how to create and style CSS pagination — the numbered navigation system used on almost every content-heavy website.

You started with the **HTML structure**: a `<ul class="pagination">` holding `<li>` items, each containing an `<a>` link for a page number. You learned that browsers show these vertically by default, and you used `display: flex` with `list-style: none` to transform them into a clean horizontal bar.

You then built progressively more advanced features. The **active class** highlights the current page in a distinct colour. The **disabled class** uses `color`, `cursor: not-allowed`, and `pointer-events: none` to fully neutralise a button when no more pages exist. **Hover effects** using `:hover:not(.active)` provide instant visual feedback, and **CSS transitions** make those colour changes smooth and polished.

You also learned that **`font-size`** controls button size, **`margin`** controls spacing between buttons, and wrapping in a container with `text-align: center` or using `justify-content: center` centres the whole bar.

Finally, you explored **breadcrumb navigation** — a trail of links showing hierarchy — using `li + li::before` with a `content` property to automatically insert slash separators.

All of these skills came together in the **blog pagination mini-project**, giving you a real, production-ready component you can use in any web project.

---

*Lesson 62 — CSS Pagination | Source: W3Schools CSS Pagination & Pagination Styles Tutorials*
