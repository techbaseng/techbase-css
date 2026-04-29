---
render_with_liquid: false
title: "Lesson 49: CSS Advanced Colors and Color Keywords"
nav_order: 49
---

# Lesson 49: CSS Advanced Colors and Color Keywords

---

## Introduction

You already know how to apply colour to a webpage using simple colour names like `red` or `blue`,
and using HEX codes like `#ff6600`. But CSS gives you several more powerful ways to describe
colour — ways that let you control **transparency**, **lightness**, **saturation**, and even
**inherit** colour intelligently from parent elements.

In this lesson you will master every advanced CSS colour system:

- **RGBA** — Red, Green, Blue + Alpha (transparency)
- **HSL** — Hue, Saturation, Lightness
- **HSLA** — HSL + Alpha (transparency)
- **CSS Color Keywords** — `currentcolor`, `transparent`, `inherit`, `initial`

By the end of this lesson, you will be able to build richly coloured, semi-transparent, and
professionally styled web pages — the kind you see on banking apps, news portals, and e-commerce
sites across Lagos and the wider web.

> 🗺️ **Lagos context:** Think of the colourful Eko Atlantic skyline, the bright yellows of
> danfo buses, the deep greens of Lagos Lagoon at dusk, and the vibrant ankara patterns worn
> at events. All of these real-world colours can be expressed precisely using the colour systems
> you are about to learn.

---

## Prerequisites — What You Need to Know First

Before this lesson, make sure you are comfortable with:

- **CSS syntax** — selectors, properties, and values (Lesson 40)
- **Basic CSS colours** — colour names, HEX codes, RGB values (earlier colour lessons)
- **HTML structure** — `<div>`, `<p>`, `<h1>`, and inline style or `<style>` blocks

If you have covered those lessons, you are ready. If any of those feel unfamiliar, revisit
them before continuing.

---

## Part 1 — Quick Recap: The Four CSS Colour Formats You Already Know

Before learning the advanced systems, let's quickly recall what you already know.

| Format         | Example               | What it means                       |
|----------------|-----------------------|--------------------------------------|
| Colour name    | `red`                 | Named colour, ~140 available         |
| HEX            | `#ff0000`             | Hexadecimal code for a colour        |
| RGB            | `rgb(255, 0, 0)`      | Red, Green, Blue each 0–255          |
| Short HEX      | `#f00`                | Shorthand for `#ff0000`              |

These all work fine, but they share one major limitation: **none of them let you control
transparency**. You cannot make a box semi-transparent with just `rgb()`. That is where
the advanced formats step in.

---

## Part 2 — RGBA Colours

### 2.1 — What Is RGBA and Why Does It Exist?

**Analogy:** Imagine painting a wall. With RGB, you choose the colour of paint. With RGBA, you
also choose how **thick** you apply the paint — from completely clear (like water) to fully
solid (like oil paint). The "A" in RGBA stands for **Alpha**, and it controls opacity.

### 2.2 — How RGBA Works

The syntax is:

```
rgba(red, green, blue, alpha)
```

- `red`, `green`, `blue` — each is a number from **0** to **255**
- `alpha` — a number from **0.0** (fully transparent / invisible) to **1.0** (fully solid / opaque)

Think of alpha like this:
- `0.0` = completely see-through (like clean glass)
- `0.5` = 50% transparent (like frosted glass)
- `1.0` = fully solid (like opaque paint)

### 2.3 — Simple RGBA Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Solid red — alpha = 1.0, fully opaque */
    .solid {
      background-color: rgba(255, 0, 0, 1.0);
      padding: 20px;
      color: white;
    }

    /* Half-transparent red — alpha = 0.5 */
    .half {
      background-color: rgba(255, 0, 0, 0.5);
      padding: 20px;
      color: white;
    }

    /* Nearly invisible red — alpha = 0.1 */
    .faint {
      background-color: rgba(255, 0, 0, 0.1);
      padding: 20px;
      color: black;
    }
  </style>
</head>
<body>
  <div class="solid">Fully solid red background</div>
  <br>
  <div class="half">Half-transparent red background</div>
  <br>
  <div class="faint">Faintly tinted red background</div>
</body>
</html>
```

**Expected output in browser:**

```
[A deeply red box with white text]
[A lighter, semi-transparent pink-red box with white text]
[A barely-there tinted box with black text]
```

> 💡 **Why does transparency matter?** In modern web design, semi-transparent overlays are used
> constantly — think of a dark overlay on a photo with text on top, or a frosted glass card
> effect on a dashboard.

### 2.4 — RGBA with Different Colours

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      background-image: linear-gradient(to right, #006400, #228B22);
      /* Deep Lagos Lagoon green background */
      padding: 30px;
    }

    .card {
      background-color: rgba(255, 255, 255, 0.2);
      /* White, 20% opaque — frosted glass look */
      padding: 20px;
      margin: 10px;
      color: white;
      border-radius: 8px;
    }

    .card-solid {
      background-color: rgba(255, 255, 255, 1.0);
      /* Fully opaque white */
      padding: 20px;
      margin: 10px;
      color: black;
      border-radius: 8px;
    }
  </style>
</head>
<body>
  <div class="card">Eko Atlantic Development Report (frosted glass)</div>
  <div class="card-solid">Lagos State Budget Summary (solid white card)</div>
</body>
</html>
```

**Expected output in browser:**

```
[A green gradient background]
[A semi-transparent frosted white card with white text]
[A fully white card with black text]
```

> 🤔 **Thinking prompt:** What happens if you set alpha to `0`? Try it and see. What happens to
> the text?

### 2.5 — Real-World Use of RGBA

RGBA is used in professional web development for:

- **Overlay effects** — dark semi-transparent layer over a background photo so text is readable
- **Modal pop-ups** — dimmed background behind dialog boxes
- **Hover effects** — buttons that become slightly transparent on hover
- **Glassmorphism** — the "frosted glass" card design trend popular in dashboards

---

## Part 3 — HSL Colours

### 3.1 — What Is HSL and Why Is It Powerful?

RGB and HEX describe colours the way a **computer** thinks: as numbers for Red, Green, and Blue
channels. HSL describes colours the way a **human** thinks: as a shade on a colour wheel,
how vivid it is, and how light or dark it is.

**HSL stands for:**
- **H** = Hue — the pure colour (where it sits on the colour wheel)
- **S** = Saturation — how vivid or grey the colour is
- **L** = Lightness — how light or dark the colour is

This makes HSL much more **intuitive for designers** because you can easily say things like:
"I want a dark teal" or "I want a pale yellow" using simple adjustments.

### 3.2 — Understanding Hue (The Colour Wheel)

Hue is measured in **degrees** from 0 to 360, going around a colour wheel:

| Degrees | Colour     |
|---------|-----------|
| 0°      | Red        |
| 30°     | Orange     |
| 60°     | Yellow     |
| 120°    | Green      |
| 180°    | Cyan       |
| 240°    | Blue       |
| 270°    | Violet     |
| 300°    | Magenta    |
| 360°    | Red again  |

Think of it like a clock, but instead of time it shows colour. 0 and 360 are both red because
the wheel wraps around.

> 🎨 **Lagos analogy:** Think of the hue value like choosing which colour of ankara fabric
> you want. 0° gives you that vibrant red, 120° gives you the rich Yoruba ceremonial green,
> and 240° gives you the royal blue of Lagos State's official colours.

### 3.3 — Understanding Saturation

Saturation is measured as a **percentage** from 0% to 100%:

- **100%** = full, vivid colour (like a fresh piece of ankara fabric)
- **50%** = washed-out, muted colour (like a faded fabric)
- **0%** = completely grey (no colour at all, just grey)

### 3.4 — Understanding Lightness

Lightness is also measured as a **percentage** from 0% to 100%:

- **0%** = completely black (no light at all)
- **50%** = the true, normal version of the colour
- **100%** = completely white (maximum light, colour disappears)

> 💡 **Simple rule to remember:**
> - 0% lightness = black
> - 50% lightness = the actual colour
> - 100% lightness = white

### 3.5 — HSL Syntax

```
hsl(hue, saturation%, lightness%)
```

### 3.6 — Simple HSL Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Pure red — hue=0, fully vivid, medium lightness */
    .red   { background-color: hsl(0, 100%, 50%);   padding: 15px; color: white; }

    /* Pure green — hue=120, fully vivid, medium lightness */
    .green { background-color: hsl(120, 100%, 50%); padding: 15px; color: white; }

    /* Pure blue — hue=240, fully vivid, medium lightness */
    .blue  { background-color: hsl(240, 100%, 50%); padding: 15px; color: white; }
  </style>
</head>
<body>
  <div class="red">Red — hsl(0, 100%, 50%)</div>
  <br>
  <div class="green">Green — hsl(120, 100%, 50%)</div>
  <br>
  <div class="blue">Blue — hsl(240, 100%, 50%)</div>
</body>
</html>
```

**Expected output in browser:**

```
[Vivid red box with white text]
[Vivid green box with white text]
[Vivid blue box with white text]
```

### 3.7 — Adjusting Saturation

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Same hue (120 = green), same lightness, different saturation */
    .vivid  { background-color: hsl(120, 100%, 40%); padding: 15px; color: white; }
    .muted  { background-color: hsl(120, 50%, 40%);  padding: 15px; color: white; }
    .grey   { background-color: hsl(120, 0%, 40%);   padding: 15px; color: white; }
  </style>
</head>
<body>
  <div class="vivid">Vivid green — saturation 100%</div>
  <br>
  <div class="muted">Muted green — saturation 50%</div>
  <br>
  <div class="grey">Grey (no saturation) — saturation 0%</div>
</body>
</html>
```

**Expected output in browser:**

```
[A bright vivid green box]
[A grey-green muted box]
[A plain grey box]
```

> 🤔 **Thinking prompt:** Why does 0% saturation always produce grey regardless of the hue value?
> (Answer: because without any colour vividness, you only have lightness left — which is always grey.)

### 3.8 — Adjusting Lightness

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Same hue (28 ≈ orange), same saturation, different lightness */
    .dark   { background-color: hsl(28, 100%, 20%); padding: 15px; color: white; }
    .normal { background-color: hsl(28, 100%, 50%); padding: 15px; color: white; }
    .light  { background-color: hsl(28, 100%, 80%); padding: 15px; color: black; }
  </style>
</head>
<body>
  <div class="dark">Dark burnt orange — lightness 20%</div>
  <br>
  <div class="normal">True orange — lightness 50%</div>
  <br>
  <div class="light">Pale peach orange — lightness 80%</div>
</body>
</html>
```

**Expected output in browser:**

```
[A very dark brownish-orange box with white text]
[A vivid orange box with white text]
[A pale peachy-orange box with black text]
```

> 🗺️ **Lagos context:** The orange tones above are very close to the signature colour of Lagos
> State's public branding materials and many popular aso-oke fabric designs.

### 3.9 — Why HSL Is Better for Design

When you use RGB or HEX, creating a "lighter version" of a colour requires completely changing
all three numbers. With HSL, you only change one number — the lightness percentage. This is why
professional designers love HSL for building colour systems (like brand palettes).

**Example — making a colour darker or lighter with HSL (easy):**

```css
/* A theme colour in HSL — easy to adjust */
.brand-normal  { background-color: hsl(200, 80%, 40%); } /* Normal teal */
.brand-light   { background-color: hsl(200, 80%, 65%); } /* Lighter teal — only lightness changed */
.brand-dark    { background-color: hsl(200, 80%, 20%); } /* Darker teal — only lightness changed */
```

**Equivalent in RGB (harder to reason about):**

```css
/* These numbers are hard to predict or adjust intuitively */
.brand-normal  { background-color: rgb(20, 122, 163); }
.brand-light   { background-color: rgb(102, 185, 214); }
.brand-dark    { background-color: rgb(8, 49, 65); }
```

---

## Part 4 — HSLA Colours

### 4.1 — What Is HSLA?

HSLA is simply **HSL + Alpha**. It adds transparency to the HSL system, exactly the same way
RGBA adds transparency to RGB.

```
hsla(hue, saturation%, lightness%, alpha)
```

The alpha channel works identically to RGBA:
- `0.0` = fully transparent
- `1.0` = fully opaque

### 4.2 — Simple HSLA Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      background-color: #1a1a2e; /* Dark navy background */
      padding: 20px;
    }

    /* Full opacity teal */
    .solid {
      background-color: hsla(180, 70%, 40%, 1.0);
      padding: 20px;
      color: white;
      margin: 10px 0;
    }

    /* 60% opaque teal */
    .semi {
      background-color: hsla(180, 70%, 40%, 0.6);
      padding: 20px;
      color: white;
      margin: 10px 0;
    }

    /* 20% opaque teal */
    .faint {
      background-color: hsla(180, 70%, 40%, 0.2);
      padding: 20px;
      color: white;
      margin: 10px 0;
    }
  </style>
</head>
<body>
  <div class="solid">Full opacity teal — HSLA alpha 1.0</div>
  <div class="semi">Semi-transparent teal — HSLA alpha 0.6</div>
  <div class="faint">Very faint teal — HSLA alpha 0.2</div>
</body>
</html>
```

**Expected output in browser:**

```
[Dark navy page background]
[Solid deep teal box with white text]
[Slightly transparent teal box, dark background shows through]
[Very faint teal tint box, dark background shows through clearly]
```

### 4.3 — HSLA for Overlays and Cards

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .hero {
      background-color: hsl(30, 90%, 55%); /* Warm orange */
      padding: 40px;
      position: relative;
    }

    /* Semi-transparent dark overlay on top of the orange */
    .overlay {
      background-color: hsla(0, 0%, 0%, 0.4); /* Black, 40% opacity */
      padding: 30px;
      color: white;
      text-align: center;
    }
  </style>
</head>
<body>
  <div class="hero">
    <div class="overlay">
      <h2>Eko Atlantic City — The Future of Lagos</h2>
      <p>Building a world-class waterfront city on the Atlantic coast.</p>
    </div>
  </div>
</body>
</html>
```

**Expected output in browser:**

```
[An orange background (the "hero" section)]
[A semi-transparent dark layer on top]
[White heading and paragraph text visible over the darkened orange]
```

> 💡 This "dark overlay over a coloured background" technique is used constantly on real
> websites — especially for hero sections, event banners, and product pages.

---

## Part 5 — CSS Color Keywords

So far you have learned colour **values** that describe specific colours using numbers. CSS also
has special **color keyword values** that describe colour in a relative, smart, or structural way
rather than with fixed numbers. These are called **CSS Color Keywords**.

There are four main keywords to understand: `currentcolor`, `transparent`, `inherit`,
and `initial`.

---

### 5.1 — The `currentcolor` Keyword

#### What Is It?

`currentcolor` is a special CSS keyword that means: **"use whatever color value is already
set on this element's `color` property."**

In other words, it lets other CSS properties (like `border-color`, `background-color`,
`box-shadow`, etc.) automatically pick up the text colour of the same element — without you
having to type the same colour twice.

#### Why Does It Exist?

Imagine you have a card where the text is blue. You also want the border to be blue. Without
`currentcolor` you would write:

```css
.card {
  color: #0044cc;          /* text is blue */
  border: 2px solid #0044cc; /* border is also blue — repeated! */
}
```

If you later change the colour to green, you have to update it in **two places**. With
`currentcolor`, you only update it once:

```css
.card {
  color: #0044cc;              /* text is blue */
  border: 2px solid currentcolor; /* border automatically becomes blue too */
}
```

#### Simple `currentcolor` Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .info-box {
      color: #006600;             /* text is dark green */
      border: 3px solid currentcolor; /* border automatically = dark green */
      padding: 15px;
      margin: 10px;
    }

    .warning-box {
      color: #cc5500;             /* text is orange */
      border: 3px solid currentcolor; /* border automatically = orange */
      padding: 15px;
      margin: 10px;
    }
  </style>
</head>
<body>
  <div class="info-box">
    Alaba International Market — Import prices updated today.
  </div>
  <div class="warning-box">
    Warning: Currency exchange rates are fluctuating. Check before trading.
  </div>
</body>
</html>
```

**Expected output in browser:**

```
[A box with dark green text AND a dark green border — automatically matched]
[A box with orange text AND an orange border — automatically matched]
```

> 💡 Notice: you never typed the colour value twice. The border colour was set by `currentcolor`
> inheriting from the `color` property.

#### Using `currentcolor` for SVG and Icons

`currentcolor` is especially useful with SVG icons (inline SVG drawings). If you set the SVG's
`fill` or `stroke` to `currentcolor`, the icon automatically takes the same colour as the
surrounding text — making icons easier to theme.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .icon-label {
      color: #c0392b; /* Set text to red */
      font-size: 18px;
    }

    .icon-label svg {
      fill: currentcolor; /* SVG icon automatically becomes red too */
      width: 20px;
      height: 20px;
      vertical-align: middle;
    }
  </style>
</head>
<body>
  <span class="icon-label">
    <!-- Simple circle SVG acting as an icon -->
    <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/></svg>
    Emergency Alert — Lagos State Traffic Authority
  </span>
</body>
</html>
```

**Expected output in browser:**

```
[A red circle icon followed by red text — both the same red automatically]
```

> 🤔 **Thinking prompt:** What would happen if you changed the `color` to blue? How many lines
> of CSS would you need to edit?

---

### 5.2 — The `transparent` Keyword

#### What Is It?

`transparent` is a keyword that makes a colour **completely invisible** — fully see-through.
It is exactly equal to `rgba(0, 0, 0, 0)` (black with 0% opacity = invisible).

#### Why Use `transparent` Instead of Just Removing the Property?

Some elements have default background colours or borders that you want to explicitly remove.
Writing `transparent` makes your intention crystal clear:

```css
button {
  background-color: transparent; /* Intentionally no background */
  border: 2px solid #333;
}
```

This is cleaner and more intentional than relying on an element's default state.

#### Simple `transparent` Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      background-color: #f0a500; /* Golden yellow background — like aso-oke gold */
    }

    .ghost-button {
      background-color: transparent;  /* No fill */
      border: 2px solid white;
      color: white;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
    }

    .solid-button {
      background-color: white;
      border: 2px solid white;
      color: #f0a500;
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <button class="ghost-button">Learn More (Ghost Button)</button>
  <button class="solid-button">Book Now (Solid Button)</button>
</body>
</html>
```

**Expected output in browser:**

```
[Golden yellow page]
[A button with no background fill — just a white outline and white text (ghost button)]
[A solid white button with golden yellow text]
```

> 🗺️ **Lagos context:** Ghost buttons (transparent with an outline) are commonly seen on
> Nigerian fintech apps and events websites — like Paystack's marketing pages and Lagos
> Fashion Week event sites.

#### `transparent` in Gradients

`transparent` is also very commonly used in gradients to create a fade-to-nothing effect:

```css
.fade-overlay {
  background: linear-gradient(to bottom, transparent, rgba(0, 0, 0, 0.8));
  /* Fades from completely see-through at the top to dark at the bottom */
}
```

---

### 5.3 — The `inherit` Keyword

#### What Is It?

`inherit` is a CSS keyword that tells a property: **"use the same value as my parent element."**

#### Why Does It Exist?

Most CSS properties either automatically inherit from the parent (like `color` and `font-size`)
or do not inherit automatically (like `background-color` and `border`). The `inherit` keyword
lets you **force** any property to inherit from the parent, even if it normally would not.

#### Quick Analogy

Imagine a parent (the `<div>`) who wears a green shirt. The child element is a `<p>` tag.
The child's text colour automatically matches the parent (text colour inherits). But the
child's background colour does NOT automatically match the parent — backgrounds don't inherit
by default. Using `inherit` on the child's `background-color` forces it to copy the parent's
background colour.

#### Simple `inherit` Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Parent element */
    .parent {
      background-color: #003366; /* Dark navy blue */
      color: #f0a500;            /* Golden text */
      padding: 20px;
    }

    /* Child WITHOUT inherit — gets its own white background */
    .child-no-inherit {
      background-color: white;
      padding: 10px;
      margin: 5px 0;
    }

    /* Child WITH inherit — copies parent's navy background */
    .child-inherit {
      background-color: inherit;  /* Forces navy background from parent */
      color: inherit;             /* Forces golden text from parent */
      border: 2px solid white;
      padding: 10px;
      margin: 5px 0;
    }
  </style>
</head>
<body>
  <div class="parent">
    Parent: Lagos State Government Portal (navy background, gold text)
    <div class="child-no-inherit">
      Child without inherit — white background, default text
    </div>
    <div class="child-inherit">
      Child with inherit — matches parent's navy background and gold text
    </div>
  </div>
</body>
</html>
```

**Expected output in browser:**

```
[A dark navy blue parent box with golden text]
  [Inside: a white child box with default dark text — does NOT match parent]
  [Inside: a navy blue child box with golden text — MATCHES parent exactly]
```

> 💡 `inherit` is powerful when you want deeply nested elements to pick up a colour theme
> from a parent without repeating the colour value at every level.

---

### 5.4 — The `initial` Keyword

#### What Is It?

`initial` is the opposite of `inherit`. It resets a property back to its **browser default
value** — ignoring any styles set by CSS rules higher up in the cascade.

#### Why Does It Exist?

Sometimes you apply a colour theme globally (e.g., all links are orange) and then want a
specific element to ignore that theme and go back to the browser's original default. That's
when `initial` is useful.

```css
a {
  color: #e67e22; /* All links are orange — set globally */
}

.reset-link {
  color: initial; /* This specific link goes back to browser default (usually blue) */
}
```

#### Simple `initial` Example

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    /* Global style — all paragraphs are deep green */
    p {
      color: #006400;
      font-size: 20px;
    }

    /* This paragraph ignores the global style — resets to browser default */
    .reset-text {
      color: initial;    /* Black (browser default text colour) */
      font-size: initial; /* Default font size (~16px) */
    }
  </style>
</head>
<body>
  <p>This paragraph follows the global green style.</p>
  <p>This one does too — it's also green and 20px.</p>
  <p class="reset-text">
    This paragraph uses initial — back to browser default (black, ~16px).
  </p>
</body>
</html>
```

**Expected output in browser:**

```
[Green paragraph, 20px]
[Green paragraph, 20px]
[Black paragraph, ~16px — reset to browser default]
```

---

### 5.5 — Summary Table: CSS Color Keywords

| Keyword          | What it does                                                             |
|------------------|--------------------------------------------------------------------------|
| `currentcolor`   | Uses the current `color` property value of the element                   |
| `transparent`    | Makes the colour fully invisible (same as `rgba(0,0,0,0)`)              |
| `inherit`        | Copies the value from the parent element                                 |
| `initial`        | Resets the value to the browser's default                                |

---

## Part 6 — Comparing All Four Advanced Colour Systems

| System  | Transparency? | Intuitive? | Best For                                   |
|---------|---------------|------------|--------------------------------------------|
| RGB     | No            | Medium     | Basic colour control                       |
| RGBA    | ✅ Yes         | Medium     | Overlays, cards, hover effects             |
| HSL     | No            | ✅ High     | Design systems, brand palettes             |
| HSLA    | ✅ Yes         | ✅ High     | Transparent design system colours          |

> 💡 **Professional tip:** Many experienced CSS developers use HSL for their entire colour
> palette because it's easier to reason about. They use HSLA when they need transparency.
> `currentcolor` reduces repetition in maintainable stylesheets.

---

## Part 7 — Guided Practice Exercises

### Exercise 1 — RGBA Overlay Card

**Objective:** Create a product card with a coloured semi-transparent background over a
vivid background.

**Scenario:** You are designing a product card for **Jollof Palace**, a Lagos restaurant
website. The page has an orange-red background. The product card should appear as a white
frosted-glass style panel.

**Steps:**
1. Create a `<div>` with class `page` that has a vivid orange background (`hsl(15, 90%, 55%)`)
2. Inside it, create a `<div>` with class `card`
3. Style `.card` with `background-color: rgba(255, 255, 255, 0.25)` (white, 25% opaque)
4. Add padding, border-radius, and white text

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .page {
      background-color: hsl(15, 90%, 55%);
      padding: 40px;
      min-height: 200px;
    }

    .card {
      background-color: rgba(255, 255, 255, 0.25);
      padding: 25px;
      border-radius: 12px;
      color: white;
      max-width: 350px;
    }

    .card h2 {
      margin: 0 0 10px;
    }

    .card p {
      margin: 0;
    }
  </style>
</head>
<body>
  <div class="page">
    <div class="card">
      <h2>Jollof Palace Special</h2>
      <p>Party Jollof Rice with Peppered Chicken</p>
      <p><strong>₦4,500</strong></p>
    </div>
  </div>
</body>
</html>
```

**Expected output in browser:**

```
[Vivid orange-red page background]
[A frosted/semi-transparent white card floating on the orange]
[White text: Jollof Palace Special, Party Jollof Rice with Peppered Chicken, ₦4,500]
```

**Self-check questions:**
- What happens if you change `0.25` to `0.9`?
- What happens if you change `rgba(255,255,255,...)` to `rgba(0,0,0,...)`?

---

### Exercise 2 — HSL Colour Palette

**Objective:** Use HSL to create a consistent colour palette for a fictional Lagos brand.

**Scenario:** You are building the colour system for **Ikeja Connect**, a tech startup
in Lagos. Their brand colour is a vivid indigo blue. You need to create a palette with
dark, normal, light, and very light versions of the same colour — all using HSL.

**Steps:**
1. Set the base hue to `240` (blue-indigo range)
2. Keep saturation at `70%`
3. Vary only the lightness: 20%, 40%, 60%, 85%
4. Show each colour in a box with a label

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .swatch {
      padding: 20px;
      margin: 8px 0;
      font-weight: bold;
    }

    .dark   { background-color: hsl(240, 70%, 20%); color: white; }
    .normal { background-color: hsl(240, 70%, 40%); color: white; }
    .light  { background-color: hsl(240, 70%, 60%); color: white; }
    .pale   { background-color: hsl(240, 70%, 85%); color: #333; }
  </style>
</head>
<body>
  <div class="swatch dark">Dark Indigo — hsl(240, 70%, 20%)</div>
  <div class="swatch normal">Normal Indigo — hsl(240, 70%, 40%)</div>
  <div class="swatch light">Light Indigo — hsl(240, 70%, 60%)</div>
  <div class="swatch pale">Pale Indigo — hsl(240, 70%, 85%)</div>
</body>
</html>
```

**Expected output in browser:**

```
[Very dark navy-indigo box — white text]
[Medium indigo box — white text]
[Lighter periwinkle-blue box — white text]
[Very pale lavender-blue box — dark text]
```

**Optional challenge:** Change the hue to `120` (green) and observe how the whole palette
shifts without changing any other numbers.

---

### Exercise 3 — `currentcolor` Self-Matching Border

**Objective:** Use `currentcolor` to make borders automatically match text colour.

**Scenario:** You are building a notification widget for a Lagos state civic alert system.
There are three types of notifications: info (blue), success (green), and danger (red).
The border of each card must always match its text colour — without repeating the colour value.

**Solution:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    .alert {
      border-left: 5px solid currentcolor; /* Auto-matches text colour */
      padding: 15px 20px;
      margin: 10px 0;
      background-color: #f9f9f9;
    }

    .info    { color: #1a73e8; }  /* Blue text + blue border */
    .success { color: #2e7d32; }  /* Green text + green border */
    .danger  { color: #c62828; }  /* Red text + red border */
  </style>
</head>
<body>
  <div class="alert info">
    ℹ️ Lagos State Ferry Services are operating normally today.
  </div>
  <div class="alert success">
    ✅ Your BRT card has been successfully recharged — ₦2,000 added.
  </div>
  <div class="alert danger">
    ⚠️ Traffic alert: Third Mainland Bridge is experiencing congestion from Adeniji to Adekunle.
  </div>
</body>
</html>
```

**Expected output in browser:**

```
[Light grey box] Blue left border | Blue text: Lagos State Ferry Services info
[Light grey box] Green left border | Green text: BRT card recharged
[Light grey box] Red left border | Red text: Third Mainland Bridge congestion
```

**Self-check:** What if you change the `.info` text colour to purple? How many lines of CSS
do you need to edit for both the text AND the border to become purple?
*(Answer: just one — `color: purple;` — because `currentcolor` follows automatically.)*

---

## Part 8 — Mini Project: Lagos City Services Dashboard Card System

You will build a complete card-based dashboard section for a fictional **Lagos City Services
Portal**, using all four advanced colour systems and color keywords you have learned.

### Project Goal

Create a web page with four service cards:
1. **Water Supply** (blue theme)
2. **Power / EKEDC** (yellow-orange theme)
3. **Traffic Alert** (red theme)
4. **Health Services** (green theme)

Each card must use:
- **HSL** for the main theme colour
- **HSLA** for a semi-transparent card background
- **`currentcolor`** for the card border (matching the icon/text colour)
- **`transparent`** for a ghost "details" button
- **`inherit`** for the card body text to inherit the card heading's colour

### Stage 1 — Set Up the Page Shell

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Lagos City Services Portal</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      font-family: Arial, sans-serif;
      background-color: hsl(220, 20%, 12%); /* Very dark navy background */
      padding: 30px;
      color: #eee;
    }

    h1 {
      text-align: center;
      font-size: 28px;
      margin-bottom: 8px;
      color: white;
    }

    .subtitle {
      text-align: center;
      font-size: 14px;
      color: hsl(220, 15%, 65%);
      margin-bottom: 30px;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 20px;
      max-width: 800px;
      margin: 0 auto;
    }
  </style>
</head>
<body>
  <h1>Lagos City Services Portal</h1>
  <p class="subtitle">Real-time Status Dashboard — April 2026</p>
  <div class="grid" id="cards-go-here">
    <!-- Cards will go here in Stage 2 -->
  </div>
</body>
</html>
```

**Milestone output:** A dark navy page with centred white heading and subtitle, and a 2-column
grid area ready.

---

### Stage 2 — Build the Card Component

Now add the card styles and HTML for all four cards:

```html
<!-- Add this inside <style> -->
<style>
  /* ... (previous styles above) ... */

  .card {
    background-color: hsla(0, 0%, 100%, 0.06); /* Very subtle white glass */
    border-radius: 14px;
    padding: 24px;
    border-top: 4px solid currentcolor; /* Auto-matches the card's text colour */
  }

  .card-icon {
    font-size: 36px;
    margin-bottom: 12px;
  }

  .card-title {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 6px;
  }

  .card-body {
    font-size: 13px;
    color: inherit;   /* Inherits colour from .card */
    opacity: 0.8;
    margin-bottom: 16px;
    line-height: 1.5;
  }

  .card-status {
    font-size: 12px;
    font-weight: bold;
    text-transform: uppercase;
    letter-spacing: 1px;
    margin-bottom: 14px;
  }

  .ghost-btn {
    background-color: transparent;         /* No fill */
    border: 1px solid currentcolor;        /* Border matches card colour */
    color: inherit;                        /* Text matches card colour */
    padding: 7px 16px;
    font-size: 13px;
    border-radius: 6px;
    cursor: pointer;
  }

  /* Individual card colour themes using HSL */
  .water   { color: hsl(200, 90%, 60%); } /* Sky blue */
  .power   { color: hsl(40, 100%, 60%); } /* Amber yellow */
  .traffic { color: hsl(0, 85%, 65%);   } /* Alert red */
  .health  { color: hsl(140, 70%, 55%); } /* Fresh green */
</style>
```

```html
<!-- Add this inside <div class="grid"> -->
<!-- Water Card -->
<div class="card water">
  <div class="card-icon">💧</div>
  <div class="card-title">Water Supply</div>
  <div class="card-body">
    Lagos Water Corporation supply is normal for Mainland zones.
    Lekki Phase 1 scheduled maintenance: Wednesday 06:00–10:00.
  </div>
  <div class="card-status">● Operational</div>
  <button class="ghost-btn">View Details</button>
</div>

<!-- Power Card -->
<div class="card power">
  <div class="card-icon">⚡</div>
  <div class="card-title">Power / EKEDC</div>
  <div class="card-body">
    Intermittent load shedding expected in Victoria Island and Surulere
    areas between 13:00–17:00 today.
  </div>
  <div class="card-status">⚠ Partial Outage</div>
  <button class="ghost-btn">Report Issue</button>
</div>

<!-- Traffic Card -->
<div class="card traffic">
  <div class="card-icon">🚦</div>
  <div class="card-title">Traffic Alert</div>
  <div class="card-body">
    Third Mainland Bridge: Heavy congestion from Adeniji end.
    Alternative: Carter Bridge or Eko Bridge via Lagos Island.
  </div>
  <div class="card-status">● High Congestion</div>
  <button class="ghost-btn">Live Map</button>
</div>

<!-- Health Card -->
<div class="card health">
  <div class="card-icon">🏥</div>
  <div class="card-title">Health Services</div>
  <div class="card-body">
    Lagos State General Hospitals operating normally. LASUTH OPD open
    Monday–Saturday. Free malaria testing this week at 12 community clinics.
  </div>
  <div class="card-status">● All Systems Normal</div>
  <button class="ghost-btn">Find Clinic</button>
</div>
```

**Milestone output:**

```
[Dark navy page]
[Two-column grid of four cards, each with a subtle glassy background]

Water card — sky blue text, blue top border, blue ghost button
Power card — amber yellow text, yellow top border, yellow ghost button
Traffic card — red text, red top border, red ghost button
Health card — green text, green top border, green ghost button

Each card shows an icon, title, description, status, and ghost button.
```

### Stage 3 — Optional Enhancements

Try adding these after completing the base project:

1. **Hover effect** — On card hover, increase the `hsla` background opacity to `0.12`
2. **Status dot pulse** — Use RGBA for a subtle glow behind the status indicator
3. **Dark/light mode toggle** — Use CSS variables so swapping the background to white changes
   all card colours intelligently (hint: this is where `currentcolor` and `inherit` really shine)

---

## Part 9 — Common Beginner Mistakes

### Mistake 1 — Forgetting the `%` in HSL

**Wrong:**
```css
background-color: hsl(120, 100, 50); /* Missing % signs — won't work */
```

**Correct:**
```css
background-color: hsl(120, 100%, 50%); /* Always include % for saturation and lightness */
```

---

### Mistake 2 — Using Alpha Values Greater Than 1

**Wrong:**
```css
background-color: rgba(255, 0, 0, 100); /* 100 is not a valid alpha! */
background-color: rgba(255, 0, 0, 50%); /* Also wrong in classic rgba — use 0–1 range */
```

**Correct:**
```css
background-color: rgba(255, 0, 0, 1.0); /* Fully opaque */
background-color: rgba(255, 0, 0, 0.5); /* 50% transparent */
```

> **Note:** Modern CSS (the newer `color()` function) allows percentage alpha, but classic
> `rgba()` uses the 0–1 decimal range. Stick to 0–1 to stay safe.

---

### Mistake 3 — Confusing `transparent` With `opacity: 0`

Both make things invisible, but they work differently:

```css
/* transparent on background — only the background disappears, text stays visible */
.box { background-color: transparent; }

/* opacity: 0 on the whole element — EVERYTHING disappears including text and children */
.box { opacity: 0; }
```

Use `transparent` when you want to remove a background colour while keeping content visible.
Use `opacity: 0` only when you want the entire element (and all its children) to become invisible.

---

### Mistake 4 — Using `currentcolor` Before Setting `color`

`currentcolor` reads the element's `color` property. If no `color` is set on that element,
it will inherit from the parent (which may produce an unexpected colour).

**Wrong (unpredictable):**
```css
.box {
  /* No color property defined! */
  border: 2px solid currentcolor; /* What colour will this be? Unpredictable. */
}
```

**Correct:**
```css
.box {
  color: #006400; /* Define color first */
  border: 2px solid currentcolor; /* Now reliably dark green */
}
```

---

### Mistake 5 — HSL Lightness at 0% or 100%

If you set lightness to `0%`, the colour is always pure black regardless of hue and saturation.
If you set it to `100%`, the colour is always pure white. Beginning designers sometimes wonder
why their colour "disappeared".

```css
background-color: hsl(240, 100%, 0%);   /* Always black — hue is irrelevant */
background-color: hsl(240, 100%, 100%); /* Always white — hue is irrelevant */
background-color: hsl(240, 100%, 50%);  /* Correct vivid blue */
```

---

### Mistake 6 — Confusing `inherit` and `currentcolor`

| Keyword         | Works on               | What it copies                              |
|-----------------|------------------------|---------------------------------------------|
| `currentcolor`  | Only colour values     | The element's own `color` property          |
| `inherit`       | Any CSS property       | The same property value from the parent element |

`currentcolor` is a colour value. `inherit` is a keyword you use in place of any value.

---

## Part 10 — Reflection Questions

1. If you wanted a box to be 40% transparent with a vivid teal colour, which colour format would
   you use — RGBA or HSLA? Why might HSLA be easier to work with?

2. A colleague sets `border-color: currentcolor;` on a button but the border comes out black —
   not the expected blue. What could have caused this?

3. What is the difference between a ghost button (using `transparent`) and hiding a button
   with `opacity: 0`?

4. When would you prefer `hsl()` over `hex` for a project's colour system? Give a real example.

5. If a child element uses `color: inherit;`, where does it look to find the colour it should use?

6. What does `color: initial;` do, and when would that be useful in a real project?

---

## Completion Checklist

Before moving to the next lesson, tick off each item:

- [ ] I understand what RGBA is and how to control transparency with the alpha channel (0–1)
- [ ] I understand HSL — what hue, saturation, and lightness each control
- [ ] I can create a full colour palette (dark, normal, light, pale) by only changing the lightness value in HSL
- [ ] I understand HSLA and can create transparent colours using the HSL system
- [ ] I know what `currentcolor` is and why it reduces repetition in CSS
- [ ] I can use `transparent` to create ghost buttons and overlay effects
- [ ] I understand the difference between `inherit` and `initial`
- [ ] I have completed the three guided exercises
- [ ] I have built the Lagos City Services Dashboard mini-project
- [ ] I know the six common mistakes and how to avoid them

---

## Lesson Summary

In this lesson, you learned that CSS offers four advanced colour systems and four smart color
keywords. Here is what each one does:

**RGBA** extends the RGB system by adding an alpha channel. The alpha value runs from 0.0
(completely transparent) to 1.0 (fully opaque). This is the go-to system for overlays, frosted
glass effects, and hover animations.

**HSL** describes colour the way humans think — by hue (which colour on the wheel), saturation
(how vivid), and lightness (how light or dark). It is particularly powerful for design systems
because you can create entire colour palettes just by adjusting one number.

**HSLA** is HSL with an added alpha channel, combining the intuitiveness of HSL with full
control over transparency.

**`currentcolor`** is a special keyword that automatically reads the element's `color` property
and uses it for other properties like `border-color`, `background-color`, or SVG `fill`. This
reduces duplication and makes theming much easier.

**`transparent`** is a keyword for a fully invisible colour — identical to `rgba(0,0,0,0)`.
It is used for ghost buttons, gradient fades, and removing default backgrounds.

**`inherit`** forces a CSS property to copy its value from the parent element, even for
properties that do not automatically inherit.

**`initial`** resets a CSS property to the browser's built-in default value, overriding
any styles set higher up in the cascade.

Together, these tools give you precise, expressive, and maintainable control over colour in
every CSS project you build.

---

*Next lesson: CSS Gradients — learn how to blend multiple colours smoothly using linear, radial,
and conic gradients.*
