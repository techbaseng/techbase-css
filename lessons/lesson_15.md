---
render_with_liquid: false
title: "CSS Icons – Font Awesome, Bootstrap, and Google Material Icons"
nav_order: 15
---

# Lesson 15: CSS Icons — Font Awesome, Bootstrap & Google Material Icons

---

## Lesson Introduction

Have you ever visited a website and noticed small pictures next to menu items — a magnifying glass for search, a shopping cart for checkout, a little bell for notifications? Those small pictures are called **icons**, and they are one of the most powerful and widely used tools in web design.

In this lesson, you will learn:

- What icons are and why they matter in web design
- The three most popular icon libraries: **Font Awesome**, **Bootstrap Icons**, and **Google Material Icons**
- How to add any of these icon libraries to your HTML page with a single line of code
- How to display icons using simple `<i>` or `<span>` tags with special class names
- How to style icons using CSS — change their size, colour, and appearance
- How to build real-world projects using icons

By the end of this lesson, you will be able to add professional-looking icons to any web page confidently and style them exactly the way you want.

> **No prior knowledge of icons is needed.** All you need is a basic understanding of HTML tags and CSS properties (like `color` and `font-size`). If you have completed the earlier lessons in this series, you are fully ready.

---

## Prerequisite Concepts

Before we begin, let's briefly review the ideas you already know that we will build on in this lesson.

### What Is an HTML Tag?

An HTML tag is a label that tells the browser how to display content. For example:

```html
<p>This is a paragraph.</p>
<h1>This is a heading.</h1>
```

### What Is a CSS Class?

A CSS class is a name you give to an HTML element so you can style it. You add it with the `class` attribute:

```html
<p class="intro-text">Welcome to my page.</p>
```

Then in your CSS:

```css
.intro-text {
  color: blue;
  font-size: 18px;
}
```

The dot (`.`) before `intro-text` tells CSS: "find every element with this class name."

### What Is a `<link>` Tag?

The `<link>` tag connects your HTML page to an external file — usually a CSS stylesheet:

```html
<link rel="stylesheet" href="styles.css">
```

You put this inside the `<head>` section of your HTML. We will use this exact same idea to connect icon libraries to our pages.

### What Is a CDN?

**CDN** stands for **Content Delivery Network**. It is simply a collection of servers spread around the world that store files (like stylesheets and fonts). When you link to a CDN, the user's browser downloads the icon library directly from the internet — you do not need to download or store any files on your computer.

Think of a CDN like a library. Instead of buying every book yourself, you go to the library and borrow what you need. The CDN provides the icon fonts/stylesheets for free, so your page can use them.

---

## Part 1: What Are CSS Icons?

### The Big Picture

An **icon** is a small image or symbol used to represent an idea, action, or object visually. You see icons everywhere:

- 🔍 Search bar → magnifying glass icon
- 🛒 Online shop → shopping cart icon
- ✉️ Email apps → envelope icon
- ☰ Mobile menus → hamburger (three lines) icon
- ♥ Social media → heart icon
- ⭐ Reviews → star icon

Icons communicate meaning instantly, without words. They also make websites look modern, clean, and professional.

### Why Use Icon Libraries Instead of Regular Images?

You might wonder: "Can't I just use an `<img>` tag and show a picture of a shopping cart?" Yes, you technically could — but icon libraries are far better for several reasons:

| Feature | Regular image (`<img>`) | Icon library |
|---|---|---|
| Resizing quality | Gets blurry when enlarged | Always sharp at any size |
| Changing colour | Must edit the image file | Change with one CSS line |
| File size | Larger, slows page down | Very small and fast |
| Adding to page | Need separate image files | Just add a class name |
| Hundreds of choices | Need hundreds of files | One library = thousands of icons |

Icon libraries work by loading a special **icon font**. Just like a regular font (like Arial or Times New Roman) has letters stored as shapes, an icon font has little pictures stored as shapes. Because they are fonts, they are:

- **Scalable** — they look sharp at any size
- **Styleable** — you can colour them with CSS just like text
- **Tiny** — they load very quickly

### The Three Icon Libraries We Will Learn

1. **Font Awesome** — The most popular icon library in the world. Has thousands of icons. Used on millions of websites.
2. **Bootstrap Icons** — Made by the Bootstrap team. Works perfectly with Bootstrap-based projects. Clean and modern.
3. **Google Material Icons** — Made by Google. Follows Google's "Material Design" style. Very clean and widely used in apps.

> **Thinking prompt:** Think of your favourite website. Can you spot any icons it uses? What do those icons communicate without any words?

---

## Part 2: Font Awesome Icons

### What Is Font Awesome?

Font Awesome is a free icon library that gives you access to hundreds (and in its paid version, thousands) of icons for your web pages. It is the most widely used icon library in the world. The free version alone has over 1,000 icons.

Font Awesome icons look like this when used on a page: a small, crisp, scalable image that you can colour and resize with CSS.

### Step 1 — How to Add Font Awesome to Your Page

You only need to add **one line** inside the `<head>` section of your HTML file. This line connects your page to Font Awesome's CDN:

```html
<head>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
</head>
```

Let's break down every part of this line:

- `<link>` — This is an HTML tag that connects your page to an external resource.
- `rel="stylesheet"` — Tells the browser: "The thing I am linking to is a CSS stylesheet."
- `href="..."` — The web address (URL) of the Font Awesome stylesheet, hosted on the CloudFlare CDN.

That is all you need! Once this line is added, you can use any Font Awesome icon on your entire page.

> **Important:** You must be connected to the internet for CDN links to work. If you are offline, the icons will not load.

### Step 2 — How to Display a Font Awesome Icon

To show an icon, you use an `<i>` tag with specific class names:

```html
<i class="fas fa-cloud"></i>
```

Let's understand every part:

- `<i>` — This is the HTML element used to display icons. Traditionally `<i>` meant "italic text", but the web community adopted it for icons because it is short and easy to type. You could also use `<span>` — both work.
- `class="fas fa-cloud"` — These are the two class names that Font Awesome uses to identify the icon:
  - `fas` — stands for **Font Awesome Solid**. This tells Font Awesome: "Show a solid (filled-in) version of this icon."
  - `fa-cloud` — this is the **specific icon name**. It tells Font Awesome: "Show the cloud icon."

**Output:** A small filled cloud symbol will appear on your page.

### Understanding Font Awesome Class Prefixes

Font Awesome uses different class prefixes for different icon styles:

| Class Prefix | Meaning | Example |
|---|---|---|
| `fas` | Font Awesome Solid (filled icons) | `fas fa-home` |
| `far` | Font Awesome Regular (outlined icons) | `far fa-heart` |
| `fab` | Font Awesome Brands (logos like Facebook, Twitter) | `fab fa-twitter` |

> **Analogy:** Think of the prefix like a clothing category, and the icon name like the specific item. `fas` is "solid clothes", `far` is "outlined clothes", `fab` is "brand-logo clothes". The icon name is the specific item you want from that category.

### Complete Beginner Example — Your First Font Awesome Icons

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My First Font Awesome Icons</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
</head>
<body>

  <h1>Font Awesome Icons</h1>

  <i class="fas fa-cloud"></i>
  <i class="fas fa-heart"></i>
  <i class="fas fa-car"></i>
  <i class="fas fa-file"></i>
  <i class="fas fa-bars"></i>

</body>
</html>
```

**Expected Output:**
A heading "Font Awesome Icons" followed by five small icons displayed in a row: a cloud, a heart, a car, a file, and three horizontal bars (hamburger menu icon).

### Sizing Icons with CSS

Because icons are treated as fonts, you resize them using `font-size` — the same property you use for text.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Icon Sizes</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <style>
    .small-icon  { font-size: 16px; }
    .medium-icon { font-size: 32px; }
    .large-icon  { font-size: 64px; }
    .huge-icon   { font-size: 96px; }
  </style>
</head>
<body>

  <i class="fas fa-star small-icon"></i>
  <i class="fas fa-star medium-icon"></i>
  <i class="fas fa-star large-icon"></i>
  <i class="fas fa-star huge-icon"></i>

</body>
</html>
```

**Expected Output:**
Four star icons in a row — each one noticeably larger than the previous. They all remain perfectly sharp (no blurring) regardless of size.

**Line-by-line explanation:**

- `.small-icon { font-size: 16px; }` — Sets the icon to 16 pixels (very small).
- `.medium-icon { font-size: 32px; }` — Sets the icon to 32 pixels (normal size).
- `.large-icon { font-size: 64px; }` — Sets the icon to 64 pixels (large).
- `.huge-icon { font-size: 96px; }` — Sets the icon to 96 pixels (very large).
- Each `<i>` element has two classes: one from Font Awesome (`fas fa-star`) and one from our own CSS (`.small-icon` etc.). An element can have as many classes as needed.

> **Why does `font-size` work on icons?** Because icon libraries load as **fonts**. The icons are literally characters in a font file, just like how "A" or "B" are characters in Arial. Since they are font characters, all font-related CSS properties work on them — including `font-size` and `color`.

### Colouring Icons with CSS

To change an icon's colour, use the `color` property — exactly the same as colouring text:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Coloured Icons</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <style>
    .red-icon    { color: red;    font-size: 40px; }
    .green-icon  { color: green;  font-size: 40px; }
    .blue-icon   { color: blue;   font-size: 40px; }
    .orange-icon { color: orange; font-size: 40px; }
    .purple-icon { color: purple; font-size: 40px; }
  </style>
</head>
<body>

  <i class="fas fa-heart red-icon"></i>
  <i class="fas fa-leaf green-icon"></i>
  <i class="fas fa-water blue-icon"></i>
  <i class="fas fa-fire orange-icon"></i>
  <i class="fas fa-star purple-icon"></i>

</body>
</html>
```

**Expected Output:**
Five icons in a row, each 40 pixels tall:
- A red heart
- A green leaf
- A blue water drop
- An orange fire flame
- A purple star

> **Thinking prompt:** What happens if you remove the `color` property from one of the icons? It inherits the colour from its parent element — likely black (the browser default). Try it!

### Using Icons Inline with Text

Icons shine brightest when used alongside text, making the content more visually clear:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Icons with Text</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <style>
    p {
      font-size: 20px;
    }
    i {
      color: steelblue;
      margin-right: 8px;
    }
  </style>
</head>
<body>

  <p><i class="fas fa-phone"></i> Call us: +1 800 555 0100</p>
  <p><i class="fas fa-envelope"></i> Email: hello@example.com</p>
  <p><i class="fas fa-map-marker-alt"></i> Address: 123 Main Street</p>

</body>
</html>
```

**Expected Output:**
Three lines of text, each preceded by a blue icon:
- A phone icon followed by a phone number
- An envelope icon followed by an email address
- A map pin icon followed by an address

**Line-by-line explanation:**

- `margin-right: 8px;` — Adds 8 pixels of space between the icon and the text next to it. Without this, the icon and text would touch each other directly.
- `color: steelblue;` — Colours all `<i>` elements with a nice steel blue colour.
- The text sits naturally to the right of each icon because `<i>` is an **inline element** — it flows naturally with text on the same line.

### Brand Icons with Font Awesome

Font Awesome also includes logos of popular brands and social media platforms. These use the `fab` (Font Awesome Brands) prefix:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Brand Icons</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <style>
    i {
      font-size: 40px;
      margin: 10px;
    }
    .twitter  { color: #1DA1F2; }
    .facebook { color: #1877F2; }
    .youtube  { color: #FF0000; }
    .github   { color: #333; }
    .instagram { color: #E4405F; }
  </style>
</head>
<body>

  <i class="fab fa-twitter twitter"></i>
  <i class="fab fa-facebook facebook"></i>
  <i class="fab fa-youtube youtube"></i>
  <i class="fab fa-github github"></i>
  <i class="fab fa-instagram instagram"></i>

</body>
</html>
```

**Expected Output:**
Five brand logos — Twitter (blue bird), Facebook (blue F), YouTube (red play button), GitHub (black cat), and Instagram (pink camera) — displayed in a row, each 40 pixels tall in their official brand colours.

> **Real-world use:** Social media icon strips like these appear on virtually every business website in the footer or contact section.

---

## Part 3: Bootstrap Icons

### What Are Bootstrap Icons?

**Bootstrap Icons** is an icon library created by the same team that makes Bootstrap (the popular CSS framework). Bootstrap Icons is completely free, open-source, and works on any web project — you do NOT need to use the Bootstrap framework to use Bootstrap Icons.

Bootstrap Icons currently has over 1,800 icons. They have a clean, geometric, modern style.

### How to Add Bootstrap Icons to Your Page

Just like Font Awesome, you add one `<link>` line in your `<head>`:

```html
<head>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css">
</head>
```

**What this line does:**

- Connects your HTML page to the Bootstrap Icons stylesheet hosted on the jsDelivr CDN.
- Once added, you can use every Bootstrap icon on your page instantly.

### How to Display a Bootstrap Icon

Bootstrap Icons uses `<i>` tags with class names that start with `bi-`:

```html
<i class="bi bi-cloud"></i>
```

- `bi` — The main Bootstrap Icons class (must always be included).
- `bi-cloud` — The specific icon name, always starting with `bi-`.

> **Pattern to remember:** Bootstrap Icons = `bi bi-iconname`. The first `bi` is the library class, and `bi-iconname` is the icon.

### Complete Beginner Example — Bootstrap Icons

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Bootstrap Icons</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css">
</head>
<body>

  <h1>Bootstrap Icons</h1>

  <i class="bi bi-house"></i>
  <i class="bi bi-person"></i>
  <i class="bi bi-envelope"></i>
  <i class="bi bi-camera"></i>
  <i class="bi bi-search"></i>

</body>
</html>
```

**Expected Output:**
A heading "Bootstrap Icons" followed by five icons: a house, a person silhouette, an envelope, a camera, and a magnifying glass.

### Sizing and Colouring Bootstrap Icons

Bootstrap Icons behave exactly like Font Awesome — use `font-size` and `color`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Styled Bootstrap Icons</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css">
  <style>
    .icon-styled {
      font-size: 48px;
      color: #0d6efd;   /* Bootstrap's primary blue colour */
      margin: 10px;
    }
  </style>
</head>
<body>

  <i class="bi bi-house icon-styled"></i>
  <i class="bi bi-cart icon-styled"></i>
  <i class="bi bi-heart icon-styled"></i>
  <i class="bi bi-bell icon-styled"></i>
  <i class="bi bi-gear icon-styled"></i>

</body>
</html>
```

**Expected Output:**
Five large (48px), Bootstrap-blue icons in a row: a house, shopping cart, heart, bell, and gear/settings icon.

### A Practical Bootstrap Example — Navigation Bar with Icons

Icons in navigation bars make it immediately clear what each link does:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Icon Navigation Bar</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css">
  <style>
    nav {
      background-color: #212529;
      padding: 15px 30px;
      display: flex;
      gap: 25px;
    }
    nav a {
      color: white;
      text-decoration: none;
      font-size: 18px;
      display: flex;
      align-items: center;
      gap: 6px;
    }
    nav a:hover {
      color: #0d6efd;
    }
    nav i {
      font-size: 20px;
    }
  </style>
</head>
<body>

  <nav>
    <a href="#"><i class="bi bi-house"></i> Home</a>
    <a href="#"><i class="bi bi-person"></i> Profile</a>
    <a href="#"><i class="bi bi-cart"></i> Shop</a>
    <a href="#"><i class="bi bi-envelope"></i> Messages</a>
    <a href="#"><i class="bi bi-gear"></i> Settings</a>
  </nav>

</body>
</html>
```

**Expected Output:**
A dark navigation bar with five white links. Each link has an icon followed by its label text. When hovered, each link turns blue.

**Line-by-line explanation of key CSS:**

- `display: flex; gap: 25px;` on `nav` — Makes all nav links sit side by side with 25 pixels of space between them.
- `display: flex; align-items: center; gap: 6px;` on `nav a` — Makes the icon and text inside each link sit on the same horizontal line, perfectly centred, with 6px space between them.
- `nav a:hover { color: #0d6efd; }` — When the user moves their mouse over a link, its colour changes to Bootstrap blue. The colour change applies to both the text and the icon because `color` is inherited by child elements.

> **Thinking prompt:** What happens if you remove `align-items: center`? The icon and text would no longer be vertically centred with each other — they would misalign depending on their sizes.

---

## Part 4: Google Material Icons

### What Are Google Material Icons?

**Google Material Icons** is an icon library created by Google, following its "Material Design" system — a design language used across all Google products (Gmail, Google Drive, YouTube, Android, etc.).

Google Material Icons have a clean, simple, geometric style. There are hundreds of icons available, all completely free.

### How to Add Google Material Icons

Google Material Icons are loaded from Google Fonts using a `<link>` tag:

```html
<head>
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</head>
```

> **Notice:** This URL uses `fonts.googleapis.com` — this is Google's own font and icon CDN. The `?family=Material+Icons` part is a query parameter telling Google: "I want the Material Icons font family."

### How to Display Google Material Icons — The Key Difference

This is where Google Material Icons differ from Font Awesome and Bootstrap Icons. Instead of using CSS class names to identify icons, you **write the icon's name as text content** inside a `<span>` element:

```html
<span class="material-icons">cloud</span>
```

- `<span>` — An inline HTML element. You could also use `<i>`.
- `class="material-icons"` — This class activates the Material Icons font, turning the text inside into an icon.
- `cloud` — The icon name, written as plain text between the tags. This is the **text content** of the element, not a class name.

> **Analogy:** Imagine you have a magic translator. You write a word in English (like "cloud"), and the translator automatically converts it into a beautiful symbol. That is exactly what the `material-icons` class does — it replaces the text with the corresponding icon symbol.

### Important: Icon Names Are the Actual Text Content

This is the most important thing to understand about Google Material Icons. The icon name goes **between the opening and closing tags**, not inside the `class` attribute:

```html
<!-- CORRECT - icon name is text content -->
<span class="material-icons">home</span>

<!-- WRONG - this shows an empty box, not an icon -->
<span class="material-icons mi-home"></span>
```

The text you write between the tags must exactly match the icon's name in the Google Material Icons library.

### Complete Beginner Example — Google Material Icons

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Google Material Icons</title>
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</head>
<body>

  <h1>Google Material Icons</h1>

  <span class="material-icons">home</span>
  <span class="material-icons">search</span>
  <span class="material-icons">favorite</span>
  <span class="material-icons">star</span>
  <span class="material-icons">settings</span>

</body>
</html>
```

**Expected Output:**
A heading "Google Material Icons" followed by five icons in a row: a house, a magnifying glass, a heart/favourite, a star, and a gear/settings icon. They appear in the clean Material Design style.

### Sizing and Colouring Google Material Icons

Exactly the same as the other libraries — use `font-size` and `color`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Styled Material Icons</title>
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
  <style>
    .icon-sm  { font-size: 18px; }
    .icon-md  { font-size: 36px; }
    .icon-lg  { font-size: 72px; }

    .colour-red    { color: #e53935; }
    .colour-blue   { color: #1e88e5; }
    .colour-green  { color: #43a047; }
  </style>
</head>
<body>

  <!-- Different sizes -->
  <span class="material-icons icon-sm">star</span>
  <span class="material-icons icon-md">star</span>
  <span class="material-icons icon-lg">star</span>

  <br><br>

  <!-- Different colours -->
  <span class="material-icons icon-md colour-red">favorite</span>
  <span class="material-icons icon-md colour-blue">info</span>
  <span class="material-icons icon-md colour-green">check_circle</span>

</body>
</html>
```

**Expected Output:**
- First row: three star icons in increasing sizes (small, medium, large).
- Second row: a red heart, a blue info circle, and a green checkmark circle.

> **Note about icon names:** Google Material Icon names sometimes use underscores for multi-word names, like `check_circle`, `arrow_back`, `thumb_up`. Write these exactly as shown — with underscores, in all lowercase.

### Google Material Icon Examples with Useful Names

Here are some commonly used Material Icons with their text-content names:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Common Material Icons</title>
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
  <style>
    .material-icons {
      font-size: 32px;
      margin: 8px;
      color: #555;
    }
  </style>
</head>
<body>

  <span class="material-icons">menu</span>
  <span class="material-icons">close</span>
  <span class="material-icons">add</span>
  <span class="material-icons">delete</span>
  <span class="material-icons">edit</span>
  <span class="material-icons">save</span>
  <span class="material-icons">share</span>
  <span class="material-icons">person</span>
  <span class="material-icons">phone</span>
  <span class="material-icons">email</span>
  <span class="material-icons">location_on</span>
  <span class="material-icons">shopping_cart</span>

</body>
</html>
```

**Expected Output:**
Twelve grey icons in a row: hamburger menu, X (close), plus sign, trash bin, pencil (edit), floppy disk (save), share arrows, person silhouette, phone, envelope, map pin, and shopping cart.

---

## Part 5: Comparing All Three Libraries

Now that you have learned all three icon libraries, let us compare them clearly:

### Side-by-Side Comparison

| Feature | Font Awesome | Bootstrap Icons | Google Material Icons |
|---|---|---|---|
| **Link tag** | `<link rel="stylesheet" href="https://cdnjs.cloudflare.com/...">` | `<link rel="stylesheet" href="https://cdn.jsdelivr.net/...">` | `<link href="https://fonts.googleapis.com/...">` |
| **Icon element** | `<i>` | `<i>` | `<span>` |
| **How to specify icon** | CSS class name (`fa-cloud`) | CSS class name (`bi-cloud`) | Text content (`cloud`) |
| **Example** | `<i class="fas fa-cloud"></i>` | `<i class="bi bi-cloud"></i>` | `<span class="material-icons">cloud</span>` |
| **Icon count (free)** | 1,000+ | 1,800+ | 900+ |
| **Style** | Varied (solid, regular, thin) | Clean geometric | Material Design |
| **Brand icons** | ✅ Yes (`fab` prefix) | ✅ Some | ❌ Limited |
| **Resize with** | `font-size` CSS | `font-size` CSS | `font-size` CSS |
| **Colour with** | `color` CSS | `color` CSS | `color` CSS |

### All Three Libraries in One Page

Here is a demonstration showing the same idea (a home icon, an envelope, and a star) using all three libraries side by side:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Three Libraries Compared</title>

  <!-- All three libraries loaded at once -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css">
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">

  <style>
    h3 { margin-top: 20px; }
    i, span.material-icons {
      font-size: 36px;
      margin: 8px;
      color: #444;
    }
  </style>
</head>
<body>

  <h3>Font Awesome</h3>
  <i class="fas fa-home"></i>
  <i class="fas fa-envelope"></i>
  <i class="fas fa-star"></i>

  <h3>Bootstrap Icons</h3>
  <i class="bi bi-house"></i>
  <i class="bi bi-envelope"></i>
  <i class="bi bi-star"></i>

  <h3>Google Material Icons</h3>
  <span class="material-icons">home</span>
  <span class="material-icons">email</span>
  <span class="material-icons">star</span>

</body>
</html>
```

**Expected Output:**
Three groups of three icons, each labelled by its library name. Each group shows a home icon, an envelope icon, and a star icon — but each in the distinct visual style of its library.

> **Observation:** All three icons represent the same ideas, but they look slightly different depending on the library. Font Awesome tends to be more detailed, Bootstrap Icons are clean and geometric, and Material Icons follow Google's flat Material Design style. Choosing which to use depends on your project's visual style.

---

## Part 6: Guided Practice Exercises

### Exercise 1 — Contact Card with Font Awesome Icons

**Objective:** Build a simple contact information card using Font Awesome icons.

**Scenario:** You are building a contact section for a small business website. Each piece of contact information (phone, email, address, website) should have an appropriate icon.

**Steps:**

1. Create a new HTML file called `contact-card.html`.
2. Add the Font Awesome CDN link in the `<head>`.
3. Create a `<div>` with a class of `contact-card`.
4. Inside, add four `<p>` elements — one each for phone, email, address, and website.
5. Inside each `<p>`, add an appropriate Font Awesome icon before the text.
6. Style the card with CSS: white background, border, rounded corners, padding.

**Hints:**
- Phone icon: `fas fa-phone`
- Email icon: `fas fa-envelope`
- Address icon: `fas fa-map-marker-alt`
- Website icon: `fas fa-globe`

**Solution:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Contact Card</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f0f2f5;
      display: flex;
      justify-content: center;
      padding: 40px;
    }

    .contact-card {
      background-color: white;
      border: 1px solid #ddd;
      border-radius: 10px;
      padding: 30px 40px;
      max-width: 350px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .contact-card h2 {
      margin-top: 0;
      color: #333;
    }

    .contact-card p {
      font-size: 16px;
      color: #555;
      margin: 12px 0;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .contact-card i {
      color: #4a90d9;
      font-size: 18px;
      width: 20px;
      text-align: center;
    }
  </style>
</head>
<body>

  <div class="contact-card">
    <h2>Contact Us</h2>
    <p><i class="fas fa-phone"></i> +1 800 555 0100</p>
    <p><i class="fas fa-envelope"></i> hello@mybusiness.com</p>
    <p><i class="fas fa-map-marker-alt"></i> 123 Main Street, Lagos</p>
    <p><i class="fas fa-globe"></i> www.mybusiness.com</p>
  </div>

</body>
</html>
```

**Expected Output:**
A centred white card with a subtle shadow. Inside: the heading "Contact Us" and four lines below it — each line has a blue icon on the left and contact information on the right. The icons are perfectly aligned with the text.

**Self-check Questions:**
- Why did we use `width: 20px; text-align: center;` on the icons?
  - *Answer: To keep all icons the same width so the text to the right of them aligns neatly in a column.*
- What happens if you change `color: #4a90d9` to `color: #e74c3c`?
  - *Answer: All icons turn red.*
- How would you add a fifth line for a social media handle?
  - *Hint: Use `fab fa-twitter` or `fab fa-instagram`.*

---

### Exercise 2 — Rating Stars with Bootstrap Icons

**Objective:** Display a product rating using Bootstrap Icons stars.

**Scenario:** You are building a product review widget. You need to show a 4-out-of-5 star rating using a mix of filled stars and an empty star.

**Steps:**

1. Create a new HTML file called `rating.html`.
2. Add the Bootstrap Icons CDN link.
3. Use `bi bi-star-fill` for filled stars and `bi bi-star` for an empty star.
4. Colour the filled stars gold/yellow and make them a comfortable reading size.

**Solution:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Product Rating</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css">
  <style>
    .rating {
      font-size: 28px;
    }
    .star-filled {
      color: #ffc107;   /* Amber/gold colour */
    }
    .star-empty {
      color: #ccc;      /* Light grey for unfilled star */
    }
    .rating-text {
      font-size: 16px;
      color: #555;
      margin-left: 8px;
      vertical-align: middle;
    }
  </style>
</head>
<body>

  <h3>Customer Rating</h3>

  <div class="rating">
    <i class="bi bi-star-fill star-filled"></i>
    <i class="bi bi-star-fill star-filled"></i>
    <i class="bi bi-star-fill star-filled"></i>
    <i class="bi bi-star-fill star-filled"></i>
    <i class="bi bi-star star-empty"></i>
    <span class="rating-text">4 out of 5 (128 reviews)</span>
  </div>

</body>
</html>
```

**Expected Output:**
Four solid gold stars followed by one grey empty star, then the text "4 out of 5 (128 reviews)" next to them.

**What-if challenges:**
- How would you show a 3.5-star rating? Try using `bi bi-star-half` for the half-star.
- How would you make the stars slightly larger or smaller? Change the `font-size` value.

---

### Exercise 3 — Feature Cards with Google Material Icons

**Objective:** Build a row of three "feature" cards, each with a large Material icon, a heading, and a short description.

**Scenario:** You are building a "Why Choose Us?" section for a company landing page.

**Solution:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Feature Cards</title>
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f5f5f5;
      padding: 40px;
    }

    .features {
      display: flex;
      gap: 20px;
      justify-content: center;
    }

    .card {
      background: white;
      border-radius: 10px;
      padding: 30px 20px;
      text-align: center;
      width: 220px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.08);
    }

    .card .material-icons {
      font-size: 56px;
      color: #4caf50;
      display: block;
      margin-bottom: 15px;
    }

    .card h3 {
      margin: 0 0 10px 0;
      color: #333;
      font-size: 18px;
    }

    .card p {
      color: #777;
      font-size: 14px;
      line-height: 1.5;
      margin: 0;
    }
  </style>
</head>
<body>

  <div class="features">
    <div class="card">
      <span class="material-icons">speed</span>
      <h3>Fast Delivery</h3>
      <p>We deliver your orders within 24 hours, every day of the week.</p>
    </div>

    <div class="card">
      <span class="material-icons">security</span>
      <h3>Secure Payments</h3>
      <p>All transactions are encrypted and fully protected.</p>
    </div>

    <div class="card">
      <span class="material-icons">support_agent</span>
      <h3>24/7 Support</h3>
      <p>Our team is always here to help you, any time of day.</p>
    </div>
  </div>

</body>
</html>
```

**Expected Output:**
Three white cards side by side on a light grey background. Each card has a large green icon at the top (a speedometer, a shield, and a headset), a bold heading, and a short description below.

**Self-check Questions:**
- How would you change all icons from green to orange? Change `color: #4caf50` to `color: #ff9800`.
- How would you add a fourth card for "Free Returns" with the `assignment_return` icon?

---

## Part 7: Mini Project — Personal Profile Card

### Project Goal

Build a complete personal profile card that uses icons from all three libraries together. This is a component you might actually use on a real portfolio website.

### Stage 1 — Setup the Structure

**Preview of what we are building:** A white card showing a person's name, job title, a short bio, and a row of contact/social icons.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Profile Card</title>

  <!-- Font Awesome for brand/social icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">

  <!-- Bootstrap Icons for general UI icons -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css">

  <!-- Google Material Icons for info section -->
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</head>
<body>
  <!-- Card structure goes here -->
</body>
</html>
```

**Milestone 1 Output:** A blank page that has all three icon libraries loaded and ready to use.

### Stage 2 — Build the Card Layout

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Profile Card</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css">
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">

  <style>
    /* Page background */
    body {
      background-color: #e8eaf6;
      font-family: 'Segoe UI', Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
    }

    /* The card itself */
    .profile-card {
      background-color: white;
      border-radius: 16px;
      padding: 40px 35px;
      max-width: 360px;
      width: 100%;
      box-shadow: 0 8px 30px rgba(0,0,0,0.12);
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="profile-card">
    <p>Card content coming next...</p>
  </div>
</body>
</html>
```

**Milestone 2 Output:** A centred white card with rounded corners and a soft shadow, sitting on a blue-grey background. The card says "Card content coming next..." as a placeholder.

### Stage 3 — Add the Avatar and Bio

```html
<!-- Replace the <p> placeholder with this content -->

<!-- Avatar placeholder (a person icon instead of an image) -->
<div class="avatar">
  <span class="material-icons">account_circle</span>
</div>

<!-- Name and job title -->
<h2 class="profile-name">Alex Johnson</h2>
<p class="profile-title">Web Developer & Designer</p>

<!-- Short bio -->
<p class="profile-bio">
  I build clean, fast, and accessible websites. Passionate about open-source software and teaching beginners.
</p>
```

```css
/* Add this to your <style> block */

.avatar .material-icons {
  font-size: 90px;
  color: #7986cb;
  display: block;
}

.profile-name {
  font-size: 24px;
  font-weight: bold;
  color: #222;
  margin: 10px 0 4px;
}

.profile-title {
  font-size: 14px;
  color: #888;
  margin: 0 0 16px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.profile-bio {
  font-size: 15px;
  color: #555;
  line-height: 1.6;
  margin: 0 0 24px;
}
```

**Milestone 3 Output:** The card now shows a large purple person avatar icon, a name in bold, a job title in smaller grey text, and a bio paragraph.

### Stage 4 — Add the Info Section with Material Icons

```html
<!-- Add this after the bio -->

<div class="info-section">
  <div class="info-item">
    <span class="material-icons">location_on</span>
    <span>Lagos, Nigeria</span>
  </div>
  <div class="info-item">
    <span class="material-icons">email</span>
    <span>alex@example.com</span>
  </div>
  <div class="info-item">
    <span class="material-icons">work</span>
    <span>Available for freelance</span>
  </div>
</div>
```

```css
.info-section {
  border-top: 1px solid #eee;
  padding-top: 20px;
  margin-bottom: 24px;
  text-align: left;
}

.info-item {
  display: flex;
  align-items: center;
  gap: 10px;
  margin: 10px 0;
  font-size: 14px;
  color: #555;
}

.info-item .material-icons {
  font-size: 20px;
  color: #7986cb;
}
```

**Milestone 4 Output:** Below the bio, a divider line appears, followed by three lines of information — each with a small purple Material icon on the left (a map pin, an envelope, and a briefcase) and information text on the right.

### Stage 5 — Add Social Icons with Font Awesome

```html
<!-- Add this at the bottom of the card -->

<div class="social-icons">
  <a href="#" class="social-link github"><i class="fab fa-github"></i></a>
  <a href="#" class="social-link linkedin"><i class="fab fa-linkedin"></i></a>
  <a href="#" class="social-link twitter"><i class="fab fa-twitter"></i></a>
  <a href="#" class="social-link codepen"><i class="fab fa-codepen"></i></a>
</div>
```

```css
.social-icons {
  display: flex;
  justify-content: center;
  gap: 14px;
  border-top: 1px solid #eee;
  padding-top: 20px;
}

.social-link {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 18px;
  text-decoration: none;
  color: white;
  transition: transform 0.2s, opacity 0.2s;
}

.social-link:hover {
  transform: scale(1.15);
  opacity: 0.9;
}

.github   { background-color: #24292e; }
.linkedin { background-color: #0077b5; }
.twitter  { background-color: #1da1f2; }
.codepen  { background-color: #131417; }
```

**Milestone 5 Output (Final):** The card is now complete. Below the info section, another divider line and then four circular coloured buttons appear — a black GitHub button, a blue LinkedIn button, a light blue Twitter button, and a dark CodePen button — each containing a white brand logo icon. When hovered, they scale up slightly.

### Complete Final Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Profile Card – Complete</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css">
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">

  <style>
    body {
      background-color: #e8eaf6;
      font-family: 'Segoe UI', Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
    }
    .profile-card {
      background-color: white;
      border-radius: 16px;
      padding: 40px 35px;
      max-width: 360px;
      width: 100%;
      box-shadow: 0 8px 30px rgba(0,0,0,0.12);
      text-align: center;
    }
    .avatar .material-icons {
      font-size: 90px;
      color: #7986cb;
      display: block;
    }
    .profile-name {
      font-size: 24px;
      font-weight: bold;
      color: #222;
      margin: 10px 0 4px;
    }
    .profile-title {
      font-size: 14px;
      color: #888;
      margin: 0 0 16px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }
    .profile-bio {
      font-size: 15px;
      color: #555;
      line-height: 1.6;
      margin: 0 0 24px;
    }
    .info-section {
      border-top: 1px solid #eee;
      padding-top: 20px;
      margin-bottom: 24px;
      text-align: left;
    }
    .info-item {
      display: flex;
      align-items: center;
      gap: 10px;
      margin: 10px 0;
      font-size: 14px;
      color: #555;
    }
    .info-item .material-icons {
      font-size: 20px;
      color: #7986cb;
    }
    .social-icons {
      display: flex;
      justify-content: center;
      gap: 14px;
      border-top: 1px solid #eee;
      padding-top: 20px;
    }
    .social-link {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 18px;
      text-decoration: none;
      color: white;
      transition: transform 0.2s, opacity 0.2s;
    }
    .social-link:hover { transform: scale(1.15); opacity: 0.9; }
    .github   { background-color: #24292e; }
    .linkedin { background-color: #0077b5; }
    .twitter  { background-color: #1da1f2; }
    .codepen  { background-color: #131417; }
  </style>
</head>
<body>

  <div class="profile-card">

    <div class="avatar">
      <span class="material-icons">account_circle</span>
    </div>

    <h2 class="profile-name">Alex Johnson</h2>
    <p class="profile-title">Web Developer & Designer</p>
    <p class="profile-bio">
      I build clean, fast, and accessible websites. Passionate about open-source software and teaching beginners.
    </p>

    <div class="info-section">
      <div class="info-item">
        <span class="material-icons">location_on</span>
        <span>Lagos, Nigeria</span>
      </div>
      <div class="info-item">
        <span class="material-icons">email</span>
        <span>alex@example.com</span>
      </div>
      <div class="info-item">
        <span class="material-icons">work</span>
        <span>Available for freelance</span>
      </div>
    </div>

    <div class="social-icons">
      <a href="#" class="social-link github"><i class="fab fa-github"></i></a>
      <a href="#" class="social-link linkedin"><i class="fab fa-linkedin"></i></a>
      <a href="#" class="social-link twitter"><i class="fab fa-twitter"></i></a>
      <a href="#" class="social-link codepen"><i class="fab fa-codepen"></i></a>
    </div>

  </div>

</body>
</html>
```

### Optional Advanced Extensions

Once you complete this project, try these enhancements:

- Add a "Download CV" button below the social icons, with a `fas fa-download` icon inside.
- Add a hover effect to the entire card using `box-shadow` and CSS `transition`.
- Replace the Material Icon avatar with a real `<img>` tag using a photo, styled as a circle with `border-radius: 50%`.
- Add a "Skills" section below the bio using Bootstrap Icons for each skill.

---

## Part 8: Common Beginner Mistakes

### Mistake 1 — Forgetting to Add the CDN Link

```html
<!-- WRONG: No CDN link. Icons will not appear at all. -->
<body>
  <i class="fas fa-home"></i>
</body>

<!-- CORRECT: CDN link must be in the <head> section. -->
<head>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
</head>
<body>
  <i class="fas fa-home"></i>
</body>
```

**Result of the mistake:** The icon element renders as empty — you see nothing or a broken-looking square box.

---

### Mistake 2 — Mixing Up Prefixes for Font Awesome

```html
<!-- WRONG: Using 'fa' instead of 'fas' or 'fab' -->
<i class="fa fa-twitter"></i>

<!-- CORRECT: Use 'fas' for solid icons, 'fab' for brand icons -->
<i class="fab fa-twitter"></i>
```

**Result of the mistake:** The icon may not appear at all, or it shows an incorrect version of the icon.

---

### Mistake 3 — Using CSS Class Names Instead of Text Content for Material Icons

```html
<!-- WRONG: Trying to use a class name like Font Awesome -->
<span class="material-icons mi-home"></span>

<!-- CORRECT: The icon name is the text content between the tags -->
<span class="material-icons">home</span>
```

**Result of the mistake:** A box with no icon inside appears, because Material Icons needs text content, not an extra class name.

---

### Mistake 4 — Forgetting Both Classes for Bootstrap Icons

```html
<!-- WRONG: Missing the first 'bi' class -->
<i class="bi-house"></i>

<!-- CORRECT: Both 'bi' and 'bi-house' are required -->
<i class="bi bi-house"></i>
```

**Result of the mistake:** The icon does not appear. Bootstrap Icons requires BOTH `bi` (the library activator class) AND `bi-iconname` (the specific icon class).

---

### Mistake 5 — Trying to Resize Icons with `width` and `height`

```css
/* WRONG: Using width/height on icon fonts */
.my-icon {
  width: 50px;
  height: 50px;
}
```

```css
/* CORRECT: Use font-size for icon fonts */
.my-icon {
  font-size: 50px;
}
```

**Result of the mistake:** The icon stays its default size because `width` and `height` do not control font characters.

---

### Mistake 6 — Offline Pages Cannot Load CDN Icons

```
Situation: You built a page with icons on your laptop.
You showed it to a friend whose laptop has no internet.
The icons are invisible!
```

**Why this happens:** CDN links require internet access. The browser downloads the icon fonts from the internet every time the page loads. Without internet, the fonts cannot be downloaded.

**Solution for offline use:** Download the icon library files and serve them locally from your own computer or server:

```html
<!-- Using locally hosted Font Awesome instead of CDN -->
<link rel="stylesheet" href="css/all.min.css">
```

---

## Part 9: Reflection Questions

Take a moment to think through these questions. Answering them will strengthen your understanding:

1. **Why are icon fonts preferred over regular image files for icons on websites?**
   *(Think about: sharpness at different sizes, ease of colouring, file size.)*

2. **What does the `fas` class prefix stand for in Font Awesome, and what does it do?**

3. **Why does Google Material Icons use text content to specify icons, while Font Awesome and Bootstrap Icons use CSS class names?**

4. **If a Font Awesome icon appears as an empty box on a page, what are the two most likely causes?**

5. **You want to display a Twitter logo next to your social media handle. Which Font Awesome prefix would you use — `fas`, `far`, or `fab`? Why?**

6. **A client asks you to build a website that must work even without internet access. Can you use CDN-hosted icon libraries? What would you do instead?**

7. **You notice that your icon looks too close to the text beside it. Which CSS property would you add to create space between them?**

8. **Looking at the profile card project, why did we use three different icon libraries instead of just one?**

---

## Completion Checklist

Before moving to the next lesson, make sure you can confidently check off every item below:

- [ ] I understand what CSS icons are and why they are used instead of regular image files.
- [ ] I can add Font Awesome to any HTML page using a single `<link>` CDN tag.
- [ ] I understand the Font Awesome class structure: `fas fa-iconname`, `far fa-iconname`, `fab fa-iconname`.
- [ ] I can display Font Awesome icons and resize/colour them with CSS.
- [ ] I can add Bootstrap Icons using the Bootstrap Icons CDN `<link>` tag.
- [ ] I understand the Bootstrap Icons class structure: `bi bi-iconname`.
- [ ] I can add Google Material Icons using the Google Fonts CDN `<link>` tag.
- [ ] I understand that Google Material Icons use **text content** (not extra classes) to specify the icon name.
- [ ] I can style icons from all three libraries using `font-size` and `color`.
- [ ] I can use icons alongside text, adjusting spacing with `margin`.
- [ ] I completed the Contact Card exercise (Exercise 1).
- [ ] I completed the Rating Stars exercise (Exercise 2).
- [ ] I completed the Feature Cards exercise (Exercise 3).
- [ ] I completed the Profile Card mini-project.
- [ ] I can identify and fix the six common beginner mistakes listed in this lesson.
- [ ] I understand why CDN-loaded icons do not work offline.

---

## Lesson Summary

In this lesson, you learned one of the most practical and commonly used tools in web development — **icon libraries**.

You now know that icons are loaded as **icon fonts** — special font files where each character is a picture instead of a letter. Because they are fonts, they are perfectly sharp at any size and can be coloured and sized using CSS properties (`color` and `font-size`).

You learned three leading icon libraries:

**Font Awesome** is the most popular, with thousands of icons. It uses `<i>` elements with two classes: a style prefix (`fas`, `far`, or `fab`) and the icon name (`fa-iconname`). The CDN is from CloudFlare/jsDelivr.

**Bootstrap Icons** is made by the Bootstrap team, with over 1,800 clean geometric icons. It also uses `<i>` elements with two classes: `bi` and `bi-iconname`. The CDN is from jsDelivr.

**Google Material Icons** follows Google's Material Design style. It differs from the other two: you use a `<span class="material-icons">` element and write the icon name as **text content** between the tags (not as a class name). The CDN is Google Fonts.

All three libraries are free, easy to add with one `<link>` tag, and can be styled the same way with CSS. You built a complete **profile card mini-project** combining all three libraries together, which mirrors a component you might find on a real professional portfolio website.

Icons are everywhere on the modern web. Now that you know how to use them, every page you build can look more professional, communicate meaning more clearly, and delight the people who visit it.

---

*Continue to Lesson 16 to learn about CSS Links — styling hyperlinks and building interactive link buttons.*
