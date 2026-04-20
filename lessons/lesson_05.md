---
render_with_liquid: false
title: "CSS Colors — Named Colors, RGB, RGBA, HEX, HSL, and HSLA"
nav_order: 5
---

# Lesson 05 — CSS Colors: Named Colors, RGB, RGBA, HEX, HSL, and HSLA

---

## Lesson Introduction

Color is one of the most powerful tools you have as a web designer. The right colors can make a webpage feel professional, welcoming, exciting, or calm. Without color, every webpage would look exactly the same — plain black text on a white background.

In this lesson, you will learn **every way CSS allows you to specify color**. There are five main color systems in CSS, and by the end of this lesson you will be able to use all of them with confidence.

**By the end of this lesson you will be able to:**

- Use color names like `red`, `DodgerBlue`, and `MediumSeaGreen`
- Use `rgb()` to mix colors from red, green, and blue light
- Use `rgba()` to make colors transparent
- Use `#hex` codes — the most common format in professional web work
- Use `hsl()` to describe colors by hue, saturation, and lightness
- Use `hsla()` for transparent HSL colors
- Apply color to text, backgrounds, and borders
- Choose the right color format for the right situation
- Complete real design exercises using all four formats

---

## Prerequisite Concepts — What You Need to Know First

Before we dive in, let us quickly recap two things from earlier lessons:

### CSS Color Properties

In CSS, you have already seen the `color` property (controls text color) and the `background-color` property (controls element background). Both of these accept color values. In this lesson you will learn all the different ways to *write* those values.

```css
h1 {
  color: red;               /* text color */
  background-color: yellow; /* background color */
}
```

### What Is a Color Value?

A **color value** is the specific code or name you write to tell CSS exactly which color to use. CSS supports several different formats for specifying color values — named keywords, RGB, HEX, and HSL. You can use any format in any color property. They are all equally valid.

---

## Section 1 — An Overview of CSS Color Formats

CSS offers five ways to specify colors. Think of them as five different "languages" for talking about the same colors:

| Format | Example | What it uses |
|--------|---------|-------------|
| Color Name | `red` | Plain English words |
| RGB | `rgb(255, 99, 71)` | Red, Green, Blue amounts (0–255) |
| RGBA | `rgba(255, 99, 71, 0.5)` | RGB + transparency level |
| HEX | `#ff6347` | Hexadecimal code |
| HSL | `hsl(9, 100%, 64%)` | Hue, Saturation, Lightness |
| HSLA | `hsla(9, 100%, 64%, 0.5)` | HSL + transparency level |

All six entries in the table above produce the same color — the famous CSS color called **Tomato**. They are just different ways of writing the same thing.

> 💡 **Key insight:** The color format you choose does not change what the color looks like on screen. `red`, `rgb(255,0,0)`, `#ff0000`, and `hsl(0, 100%, 50%)` all display the same pure red color. The difference is only in *how* you write the code and *which situations* each format is best suited for.

---

## Section 2 — Where You Can Apply Color in CSS

Before learning each format, let us understand the three main places you apply color on a webpage.

### 2.1 — Text Color

The `color` property controls the color of text inside an element.

```css
h1 {
  color: Tomato;
}
```

**HTML:**
```html
<h1>Hello World</h1>
```

**Expected output:** The heading "Hello World" appears in a reddish-orange Tomato color.

---

### 2.2 — Background Color

The `background-color` property fills the background of any element with a color.

```css
h1 {
  background-color: DodgerBlue;
}

p {
  background-color: Tomato;
}
```

**Expected output:**
- The `<h1>` heading has a bright blue background behind it
- The `<p>` paragraph has a tomato-red background behind it

> 💡 **Tip:** You can apply `background-color` to any HTML element — not just the `<body>`. Individual headings, paragraphs, divs, buttons — all of them can have their own background color.

---

### 2.3 — Border Color

The `border` property can include a color value. The format is: `border: [thickness] [style] [color]`

```css
h1 {
  border: 2px solid Tomato;
}

h2 {
  border: 2px solid DodgerBlue;
}

h3 {
  border: 2px solid Violet;
}
```

**Expected output:**
- The first heading has a 2-pixel solid red-orange border
- The second heading has a 2-pixel solid blue border
- The third heading has a 2-pixel solid violet border

Now that you know *where* to apply colors, let us learn each color format in detail.

---

## Section 3 — CSS Named Colors (Color Keywords)

### What Are Named Colors?

CSS includes **140 predefined color names** — plain English words that you can type directly as a color value. These are the easiest format to use because they require no numbers or codes.

### Examples of Named Colors

```css
p { color: Tomato; }
p { color: Orange; }
p { color: DodgerBlue; }
p { color: MediumSeaGreen; }
p { color: Gray; }
p { color: SlateBlue; }
p { color: Violet; }
p { color: LightGray; }
```

**Expected outputs (text colors):**
- `Tomato` → warm reddish-orange
- `Orange` → bright orange
- `DodgerBlue` → vivid medium blue
- `MediumSeaGreen` → soft medium green
- `Gray` → standard medium gray
- `SlateBlue` → blue-purple
- `Violet` → bright purple-pink
- `LightGray` → pale gray

### A Micro-Demo — Named Colors in Action

```css
body {
  background-color: LightGray;
}

h1 {
  color: DodgerBlue;
}

p {
  color: MediumSeaGreen;
}
```

```html
<body>
  <h1>Welcome to My Page</h1>
  <p>This text is sea green on a light gray background.</p>
</body>
```

**Expected output:** A light gray page background, with a blue heading and sea-green paragraph text.

### The 10 Most Common Named Colors for Beginners

| Color Name | What it looks like |
|-----------|-------------------|
| `white` | Pure white — standard page background |
| `black` | Pure black — standard text |
| `gray` / `grey` | Middle gray |
| `red` | Bright pure red |
| `blue` | Pure medium blue |
| `green` | Standard medium green |
| `orange` | Bright orange |
| `yellow` | Bright yellow |
| `purple` | Dark purple |
| `pink` | Light pink |

> 📌 **Important:** CSS color names are **case-insensitive**. `Red`, `red`, `RED`, and `rEd` all produce the same color. However, the convention is to write them in PascalCase (like `DodgerBlue`) or all lowercase (like `red`).

> 📌 **Note:** CSS supports both `gray` and `grey` (American and British spellings) for the same color. Either works.

### When to Use Named Colors

Named colors are ideal for:
- Quick prototyping and testing
- Simple projects where you do not need to match exact brand colors
- Learning and experimenting

However, they are **limited** — 140 colors is far fewer than the 16+ million colors your screen can display. For precise control, you need RGB, HEX, or HSL.

> 💡 **Thinking Prompt:** Can you think of why a company like Coca-Cola would NOT want to use a color name like `red` for their brand? Because `red` is a generic color, not their specific shade of red. They need an exact code — which is where HEX and RGB come in.

---

## Section 4 — RGB Colors

### What Does RGB Mean?

**RGB** stands for **Red, Green, Blue**. It is a color model based on mixing light. Your computer screen works by lighting up millions of tiny dots (pixels), and each pixel is made of three tiny lights — one red, one green, and one blue. By controlling how bright each of those three lights is, the screen can produce any color.

> 💡 **Analogy:** Think of a theatre spotlight. If you shine a red spotlight, a green spotlight, and a blue spotlight onto the same spot, you can mix them to create millions of different colors. RGB works exactly the same way — but with light from your screen's pixels.

### The RGB Syntax

```css
color: rgb(red, green, blue);
```

Each number inside `rgb()` is a value from **0 to 255**:
- `0` means that light is completely OFF (none of that color)
- `255` means that light is completely ON (maximum of that color)

### Understanding the Scale: 0 to 255

Why 0 to 255? Because computers store color data in **8 bits** per channel. With 8 bits, you can represent 256 different values (0 through 255). This gives you 256 × 256 × 256 = **16,777,216** possible colors — more than 16 million!

### The Three Primary RGB Colors

```css
/* Pure red — only red light is on */
color: rgb(255, 0, 0);

/* Pure green — only green light is on */
color: rgb(0, 255, 0);

/* Pure blue — only blue light is on */
color: rgb(0, 0, 255);
```

**Expected outputs:**
- `rgb(255, 0, 0)` → bright pure red
- `rgb(0, 255, 0)` → bright pure green (lime green)
- `rgb(0, 0, 255)` → bright pure blue

### Mixing Colors with RGB

The magic happens when you mix the channels together:

```css
/* Mix red + green light → yellow */
color: rgb(255, 255, 0);

/* Mix red + blue light → magenta (hot pink-purple) */
color: rgb(255, 0, 255);

/* Mix green + blue light → cyan (aqua) */
color: rgb(0, 255, 255);

/* All three lights at full → white */
color: rgb(255, 255, 255);

/* All three lights off → black */
color: rgb(0, 0, 0);
```

**Expected outputs:**
- `rgb(255, 255, 0)` → yellow
- `rgb(255, 0, 255)` → magenta
- `rgb(0, 255, 255)` → cyan/aqua
- `rgb(255, 255, 255)` → white
- `rgb(0, 0, 0)` → black

> 💡 **Thinking Prompt:** What color would `rgb(128, 128, 128)` produce? All three channels are set to the halfway point (128 out of 255), so this produces a **medium gray**. Equal amounts of red, green, and blue light always create shades of gray.

### Creating Shades of Gray with RGB

This is one of the most useful patterns in RGB: **any time all three values are equal, you get a shade of gray**.

```css
color: rgb(0, 0, 0);     /* black */
color: rgb(64, 64, 64);  /* very dark gray */
color: rgb(128, 128, 128); /* medium gray */
color: rgb(192, 192, 192); /* light gray */
color: rgb(255, 255, 255); /* white */
```

**Expected outputs:** A gradient from black through increasingly lighter grays to white.

### Recognising Famous Colors in RGB

```css
color: rgb(255, 99, 71);   /* Tomato */
color: rgb(255, 165, 0);   /* Orange */
color: rgb(30, 144, 255);  /* DodgerBlue */
color: rgb(60, 179, 113);  /* MediumSeaGreen */
```

### A Complete RGB Example

```css
body {
  background-color: rgb(240, 240, 240); /* very light gray background */
}

h1 {
  color: rgb(30, 144, 255); /* DodgerBlue text */
}

p {
  color: rgb(60, 60, 60); /* very dark gray, easier on eyes than pure black */
}
```

**Expected output:** A near-white page background, blue heading, and very dark gray body text — a clean, readable design.

### When to Use RGB

RGB is great when:
- You are working with colors from a design tool that provides RGB values
- You want precise programmatic control (especially when using JavaScript to change colors)
- You need to generate colors mathematically (e.g., a data visualization where brightness represents a data value)

---

## Section 5 — RGBA Colors (RGB with Transparency)

### What Is RGBA?

**RGBA** is exactly like RGB, but with a fourth value: **alpha** (A). The alpha value controls the **transparency** (see-through-ness) of the color.

```css
color: rgba(red, green, blue, alpha);
```

The alpha value is a decimal number from **0.0 to 1.0**:
- `0` or `0.0` = completely transparent (invisible)
- `0.5` = 50% transparent (half see-through)
- `1` or `1.0` = completely solid (no transparency)

> 💡 **Analogy:** Think of a stained-glass window. Solid stained glass is like `alpha: 1`. Frosted glass you can barely see through is like `alpha: 0.2`. And if the glass were completely clear (invisible), that would be `alpha: 0`. RGBA lets you put any level of transparency on your colors.

### RGBA in Action — Five Transparency Levels of Tomato

```css
/* All five produce Tomato (rgb 255, 99, 71) at different transparencies */

div.solid     { background-color: rgba(255, 99, 71, 1.0); }
div.most      { background-color: rgba(255, 99, 71, 0.8); }
div.half      { background-color: rgba(255, 99, 71, 0.5); }
div.quarter   { background-color: rgba(255, 99, 71, 0.2); }
div.invisible { background-color: rgba(255, 99, 71, 0.0); }
```

**Expected outputs:**
- `alpha: 1.0` → full solid tomato red-orange
- `alpha: 0.8` → tomato with a slight fade
- `alpha: 0.5` → tomato at half transparency — you can see what is behind it
- `alpha: 0.2` → very faint hint of tomato color
- `alpha: 0.0` → completely invisible (you see whatever is behind the element)

### A Practical Use Case for RGBA

RGBA transparency is widely used for overlays — a semi-transparent color layer placed on top of an image to make text more readable:

```css
/* An image with a dark semi-transparent overlay to make white text readable */
.hero-section {
  background-color: rgba(0, 0, 0, 0.5); /* 50% black overlay */
  color: white;
}
```

**Expected output:** White text appears on top of a semi-transparent dark overlay, making it readable even over a bright background image.

### Second Example — Blue with Various Transparencies

```css
h1 { background-color: rgba(30, 144, 255, 1.0); }  /* solid DodgerBlue */
h2 { background-color: rgba(30, 144, 255, 0.6); }  /* 60% DodgerBlue */
h3 { background-color: rgba(30, 144, 255, 0.3); }  /* 30% DodgerBlue */
```

**Expected outputs:** Three headings with progressively more transparent blue backgrounds.

> 💡 **Thinking Prompt:** What happens if you set `color: rgba(0, 0, 0, 0.0)` on your text? The text becomes completely invisible! This is a common mistake — be careful with low alpha values on text.

---

## Section 6 — HEX Colors (Hexadecimal)

### What Is a HEX Color?

A **HEX color** (short for hexadecimal color) is a color written as a 6-character code starting with a `#` symbol:

```css
color: #ff6347; /* This is Tomato in HEX */
```

HEX colors are the **most widely used color format in professional web development**. If you look at the CSS of any major website — Google, Amazon, Twitter — you will see HEX codes everywhere.

### Why Does It Start With `#`?

The `#` symbol tells CSS "what follows is a hexadecimal color code". It is simply a required prefix — always include it.

### Understanding Hexadecimal

**Hexadecimal** (hex for short) is a numbering system that uses 16 digits instead of the usual 10. While our normal decimal system uses digits 0–9, hexadecimal uses 0–9 **and** A–F:

| Decimal | Hex |
|---------|-----|
| 0 | 0 |
| 1 | 1 |
| 9 | 9 |
| 10 | A |
| 11 | B |
| 12 | C |
| 13 | D |
| 14 | E |
| 15 | F |
| 16 | 10 |
| 255 | FF |

> 💡 **Why use hex?** Two hex digits can represent exactly 256 values (0–255), the same range as one RGB channel. So the 6-character HEX code `#RRGGBB` is simply a compact way to write the same information as `rgb(R, G, B)`. The hex code is shorter and more commonly used in design tools.

### The Structure of a HEX Code

A HEX color code has 6 characters after the `#`, always split into three pairs:

```
# RR GG BB
  ↑  ↑  ↑
  |  |  └── Blue channel (00 to FF)
  |  └───── Green channel (00 to FF)
  └──────── Red channel (00 to FF)
```

Each pair is a two-digit hex number from `00` (= 0 in decimal = completely off) to `FF` (= 255 in decimal = completely on).

**Reading the Tomato HEX code `#ff6347`:**

```
# ff  63  47
  ↑   ↑   ↑
  |   |   └── Blue = 47 hex = 71 decimal
  |   └─────  Green = 63 hex = 99 decimal
  └─────────  Red = ff hex = 255 decimal
```

So `#ff6347` = `rgb(255, 99, 71)` — they are the exact same color!

### The Three Primary HEX Colors

```css
color: #ff0000; /* pure red   — same as rgb(255, 0, 0) */
color: #00ff00; /* pure green — same as rgb(0, 255, 0) */
color: #0000ff; /* pure blue  — same as rgb(0, 0, 255) */
```

**Expected outputs:**
- `#ff0000` → bright red
- `#00ff00` → bright green (lime)
- `#0000ff` → bright blue

### Black, White, and Grays in HEX

```css
color: #000000; /* black — all channels off */
color: #ffffff; /* white — all channels full */
color: #808080; /* medium gray — all channels at halfway (128 = 80 in hex) */
color: #cccccc; /* light gray */
color: #333333; /* very dark gray (popular for body text) */
```

> 💡 **Pattern:** Just like in RGB, **equal values in all three pairs produce gray shades**. `#333333`, `#666666`, `#999999`, `#cccccc` are all grays of increasing lightness.

### Shorthand HEX — 3-Character Codes

When each pair of a HEX code has **both characters the same** (like `#ff0000`, `#aabbcc`, `#336699`), you can shorten it to just 3 characters by writing each pair once:

```css
/* Full 6-digit form → Shortened 3-digit form */
#ff0000  →  #f00   /* red */
#00ff00  →  #0f0   /* green */
#0000ff  →  #00f   /* blue */
#ffffff  →  #fff   /* white */
#000000  →  #000   /* black */
#aabbcc  →  #abc   /* a dusty blue-gray */
```

The browser automatically doubles each digit: `#abc` becomes `#aabbcc`. **You can only use 3-digit shorthand when both characters in each pair are the same.** `#a1b2c3` cannot be shortened because `a1`, `b2`, and `c3` have different characters.

### A Complete HEX Color Example

```css
body {
  background-color: #f4f4f4; /* very light gray — near white */
}

h1 {
  color: #1a73e8;  /* Google-style blue */
}

p {
  color: #333333;  /* very dark gray for body text */
}

a {
  color: #e8451a;  /* a warm orange-red for links */
}
```

**Expected output:** A clean, professional-looking page with a near-white background, blue headings, very dark gray body text, and warm reddish link color.

### HEX Color Reference Cheat Sheet

| Color | HEX Code | Description |
|-------|----------|-------------|
| Black | `#000000` | Pure black |
| White | `#ffffff` | Pure white |
| Red | `#ff0000` | Pure red |
| Green | `#00ff00` | Pure lime green |
| Blue | `#0000ff` | Pure blue |
| Yellow | `#ffff00` | Pure yellow |
| Cyan | `#00ffff` | Blue-green |
| Magenta | `#ff00ff` | Pink-purple |
| Tomato | `#ff6347` | Warm red-orange |
| DodgerBlue | `#1e90ff` | Vivid sky blue |
| Dark Gray | `#333333` | Common body text |
| Light Gray | `#cccccc` | Subtle dividers |
| Off-white | `#f4f4f4` | Soft background |

### When to Use HEX

HEX is the best choice when:
- You are copying a color from a design tool (like Figma, Adobe XD, or Canva — these all output HEX)
- You are following a brand style guide (companies always specify brand colors in HEX)
- You want to write color codes in the most compact, industry-standard way
- You are reading tutorials, documentation, or design resources (HEX is the most commonly shown format)

> 💡 **Real-world tip:** If you ever need to find a HEX code for a color you see on a website, you can right-click the element in your browser → "Inspect" → look in the CSS panel. Most browser developer tools show colors in HEX by default.

---

## Section 7 — HSL Colors

### What Does HSL Mean?

**HSL** stands for **Hue, Saturation, Lightness**. It is a completely different way of thinking about color — instead of mixing light like RGB, HSL describes colors the way humans naturally think about them.

```css
color: hsl(hue, saturation%, lightness%);
```

### The Three HSL Components

#### Hue — "Which Color?"

**Hue** is a number from **0 to 360** that selects your color from the color wheel. Imagine a circle (the color wheel) where all the colors of the rainbow are arranged around it:

- **0 (or 360)** = Red
- **30** = Orange
- **60** = Yellow
- **120** = Green
- **180** = Cyan
- **240** = Blue
- **270** = Purple
- **300** = Magenta
- **360** = Red again (full circle)

> 💡 **Analogy:** Think of a clock. Instead of 12 hours, the color wheel has 360 degrees. Hue is like the hour hand position — it tells you which direction on the wheel to look, and that direction gives you your color family.

```css
color: hsl(0,   100%, 50%); /* Red */
color: hsl(30,  100%, 50%); /* Orange */
color: hsl(60,  100%, 50%); /* Yellow */
color: hsl(120, 100%, 50%); /* Green */
color: hsl(180, 100%, 50%); /* Cyan */
color: hsl(240, 100%, 50%); /* Blue */
color: hsl(300, 100%, 50%); /* Magenta */
```

**Expected outputs:** A full rainbow of vivid colors, each 60 degrees apart around the color wheel.

#### Saturation — "How Vivid or Washed Out?"

**Saturation** is a percentage from **0% to 100%** that controls how vivid or gray the color is:

- `100%` = fully vivid, pure color (maximum richness)
- `50%` = muted, somewhat washed out
- `0%` = completely gray (no color at all)

> 💡 **Analogy:** Think of paint. If you squeeze pure red paint straight from the tube, that is 100% saturation. If you mix a little red into a bucket of gray paint, you get a muted, grayish red — lower saturation. If you just use straight gray paint with no red, that is 0% saturation.

```css
/* Same hue (red = 0), different saturations */
color: hsl(0, 100%, 50%);  /* vivid bright red */
color: hsl(0, 75%,  50%);  /* slightly muted red */
color: hsl(0, 50%,  50%);  /* noticeably muted, grayish-red */
color: hsl(0, 25%,  50%);  /* mostly gray, barely any red */
color: hsl(0, 0%,   50%);  /* pure medium gray — no red at all */
```

**Expected outputs:** A series from vivid red fading progressively into medium gray.

> 💡 **Thinking Prompt:** What happens to the hue value when saturation is 0%? It does not matter at all! `hsl(0, 0%, 50%)`, `hsl(120, 0%, 50%)`, and `hsl(240, 0%, 50%)` all produce the exact same medium gray, because there is no color saturation to express.

#### Lightness — "How Light or Dark?"

**Lightness** is a percentage from **0% to 100%** that controls how light or dark the color is:

- `100%` = pure white (color disappears into white)
- `50%` = the "true" normal version of the color
- `0%` = pure black (color disappears into black)

> 💡 **Analogy:** Think of a room with a dimmer switch on the lights. At 100% brightness (lightness), everything is washed out in brilliant white light. At 50%, you see colors normally. At 0%, the room is completely dark — everything looks black.

```css
/* Same hue and saturation (blue), different lightness */
color: hsl(240, 100%, 0%);   /* black */
color: hsl(240, 100%, 25%);  /* very dark blue */
color: hsl(240, 100%, 50%);  /* normal blue */
color: hsl(240, 100%, 75%);  /* light blue */
color: hsl(240, 100%, 100%); /* white */
```

**Expected outputs:** A series from black through dark blue, normal blue, light blue, to white.

### Creating Grays with HSL

With HSL, creating gray is simple — just set saturation to 0%:

```css
color: hsl(0, 0%, 0%);    /* black */
color: hsl(0, 0%, 25%);   /* dark gray */
color: hsl(0, 0%, 50%);   /* medium gray */
color: hsl(0, 0%, 75%);   /* light gray */
color: hsl(0, 0%, 100%);  /* white */
```

The hue value does not matter when saturation is 0%.

### Recognising Famous Colors in HSL

```css
color: hsl(9,   100%, 64%);  /* Tomato */
color: hsl(39,  100%, 50%);  /* Orange */
color: hsl(209, 100%, 56%);  /* DodgerBlue */
color: hsl(146, 50%,  47%);  /* MediumSeaGreen */
```

### A Complete HSL Example

```css
body {
  background-color: hsl(0, 0%, 96%); /* very light gray — almost white */
}

h1 {
  color: hsl(210, 80%, 40%); /* a deep, rich blue */
}

p {
  color: hsl(0, 0%, 20%); /* near-black dark gray for body text */
}

.highlight {
  background-color: hsl(45, 100%, 70%); /* warm golden yellow highlight */
  color: hsl(0, 0%, 10%); /* almost black text on the highlight */
}
```

**Expected output:** A clean professional page with soft background, rich blue headings, dark gray text, and golden-highlighted sections.

### Why HSL Is Powerful for Designers

HSL is considered the most **intuitive** color format because it matches how humans actually think about color:

1. "I want a blue color" → set the hue around 240
2. "I want it quite vivid" → set saturation to 80%
3. "I want it a bit dark" → set lightness to 35%

With RGB or HEX, it is very hard to predict what you will get without a color picker tool. With HSL, you can reason about colors logically. This makes it especially powerful for:
- **Creating color themes:** Define one hue, then vary saturation and lightness to create lighter and darker versions
- **Accessibility work:** Adjusting lightness ensures sufficient contrast
- **Dark mode design:** Simply shift all lightness values up or down

**Example — A button color family using the same hue:**

```css
/* All three use hue 210 (blue) — only lightness changes */
.btn-dark    { background-color: hsl(210, 80%, 30%); } /* dark blue */
.btn-normal  { background-color: hsl(210, 80%, 50%); } /* normal blue */
.btn-light   { background-color: hsl(210, 80%, 70%); } /* light blue */
```

**Expected output:** Three buttons that are clearly the same "family" of blue, but at different brightness levels — very useful for hover states and disabled states.

---

## Section 8 — HSLA Colors (HSL with Transparency)

**HSLA** is HSL with a fourth alpha value for transparency — exactly the same concept as RGBA but written in the HSL format:

```css
color: hsla(hue, saturation%, lightness%, alpha);
```

The alpha value works identically to RGBA: 0 is transparent, 1 is solid, and decimals between give partial transparency.

### HSLA Examples

```css
/* Tomato at different transparencies in HSLA */
color: hsla(9, 100%, 64%, 1.0);   /* fully solid Tomato */
color: hsla(9, 100%, 64%, 0.8);   /* mostly solid */
color: hsla(9, 100%, 64%, 0.5);   /* half transparent */
color: hsla(9, 100%, 64%, 0.2);   /* very faint */
color: hsla(9, 100%, 64%, 0.0);   /* completely invisible */
```

**Expected outputs:** Five versions of tomato red from fully visible to completely transparent.

### A Practical HSLA Use Case — Card Overlay

```css
/* A modal/card overlay using a semi-transparent dark background */
.modal-backdrop {
  background-color: hsla(0, 0%, 0%, 0.6); /* 60% black overlay */
}

/* A "frosted glass" style panel */
.frosted-panel {
  background-color: hsla(210, 80%, 95%, 0.8); /* 80% very light blue */
}
```

**Expected output:**
- The modal backdrop is a dark, 60% transparent black, allowing the page behind it to show through dimly
- The frosted panel appears as a soft, slightly transparent light-blue panel

---

## Section 9 — Comparing All Color Formats

This table shows the same color — **Tomato** — written in every format:

| Format | Code | Notes |
|--------|------|-------|
| Color Name | `Tomato` | Easy to remember, limited options |
| RGB | `rgb(255, 99, 71)` | Good for programmatic use |
| RGBA | `rgba(255, 99, 71, 0.5)` | RGB + transparency |
| HEX | `#ff6347` | Most common in professional work |
| HEX (short) | Cannot shorten this one | `f` ≠ `f6`, so no shorthand here |
| HSL | `hsl(9, 100%, 64%)` | Most intuitive for designers |
| HSLA | `hsla(9, 100%, 64%, 0.5)` | HSL + transparency |

### Quick Decision Guide — Which Format Should I Use?

| Situation | Best format |
|-----------|------------|
| Learning and experimenting | Color names |
| Copying from a design tool (Figma, Sketch, etc.) | HEX |
| Following a brand style guide | HEX |
| Building a data visualization or JS-controlled colors | RGB |
| Need transparency | RGBA or HSLA |
| Creating design systems / color themes | HSL |
| Making accessible color palettes | HSL |
| Writing code you want to be readable and maintainable | HSL |

---

## Section 10 — Simple Standalone Examples

### Example 1 — Same Color, All Four Formats

These four rules all produce the exact same result — DodgerBlue text:

```css
/* Using a color name */
h1 { color: DodgerBlue; }

/* Using RGB */
h1 { color: rgb(30, 144, 255); }

/* Using HEX */
h1 { color: #1e90ff; }

/* Using HSL */
h1 { color: hsl(209, 100%, 56%); }
```

**Expected output:** All four produce exactly the same vivid sky blue text.

---

### Example 2 — Using Transparency on a Banner

```css
.banner {
  background-color: rgba(30, 144, 255, 0.3); /* transparent light blue */
  padding: 20px;
}

.banner h2 {
  color: rgb(0, 50, 100); /* dark navy blue */
}
```

```html
<div class="banner">
  <h2>Special Announcement</h2>
</div>
```

**Expected output:** A soft, transparent light-blue banner box with dark navy heading text inside it.

---

### Example 3 — Building a Color Palette with HSL

```css
/* A full color palette based on one hue: blue (hue = 210) */
.color-darkest  { background-color: hsl(210, 70%, 20%); } /* very dark navy */
.color-dark     { background-color: hsl(210, 70%, 35%); } /* dark blue */
.color-mid      { background-color: hsl(210, 70%, 50%); } /* standard blue */
.color-light    { background-color: hsl(210, 70%, 70%); } /* light sky blue */
.color-lightest { background-color: hsl(210, 70%, 90%); } /* very pale blue */
```

**Expected output:** Five harmonious shades of blue that form a coherent color scale — perfect for designing card shadows, hover states, and disabled buttons.

---

### Example 4 — The Gray Scale in All Three Formats

```css
/* Three ways to write medium gray */
p.rgb  { color: rgb(128, 128, 128); }
p.hex  { color: #808080; }
p.hsl  { color: hsl(0, 0%, 50%); }
```

**Expected output:** All three paragraphs display text in identical medium gray.

---

## Section 11 — Guided Practice Exercises

### Exercise 1 — Named Colors Warm-Up

**Objective:** Style a simple business card page using only named colors.

**Scenario:** You are creating a business card webpage for a florist shop. The design should feel fresh and natural.

**Specification:**
- Page background: `LightGreen`
- Business name heading (`h1`): `DarkGreen` text
- Tagline paragraph (`p`): `ForestGreen` text
- A highlight box (`div.card`): `White` background

**Your CSS:**

```css
body {
  background-color: LightGreen;
}

h1 {
  color: DarkGreen;
}

p {
  color: ForestGreen;
}

div.card {
  background-color: White;
}
```

**Expected output:** A green-themed florist card with progressively darker greens for heading and text, with the card content on a clean white background.

**Self-check:** Did you notice that named colors like `ForestGreen` always have no spaces? Named colors are single words (or compound words with no spaces).

---

### Exercise 2 — RGB Mixing Challenge

**Objective:** Predict and write the RGB values for these colors.

**Scenario:** You are a data scientist building a colour-coded visualization. You need to find the RGB values for specific key colors without using a color picker.

**Part A — Work out the RGB values for these colors from memory:**

1. Pure yellow (hint: yellow = red + green light)
2. Pure cyan (hint: cyan = green + blue light)
3. Pure white
4. Pure black
5. Very dark gray (hint: use low equal values)

**Answers:**

```css
/* Pure yellow */
color: rgb(255, 255, 0);

/* Pure cyan */
color: rgb(0, 255, 255);

/* Pure white */
color: rgb(255, 255, 255);

/* Pure black */
color: rgb(0, 0, 0);

/* Very dark gray */
color: rgb(30, 30, 30);
```

**Part B — Write CSS that gives a page:**
- A very light gray background (`rgb` with all values at 240)
- A heading in a warm medium red (`rgb` with red at 200, green at 50, blue at 50)
- Paragraph text in dark gray (`rgb` with all values at 60)

**Your CSS:**

```css
body {
  background-color: rgb(240, 240, 240);
}

h1 {
  color: rgb(200, 50, 50);
}

p {
  color: rgb(60, 60, 60);
}
```

**Expected output:** A soft gray page with a warm red heading and near-black gray body text.

---

### Exercise 3 — HEX Code Identification

**Objective:** Decode and apply HEX color codes.

**Scenario:** A design team has handed you a brand style guide with the following HEX codes. Your job is to apply them correctly in CSS.

**Brand guide:**
- Primary brand color: `#2563eb` (a medium-dark blue)
- Secondary accent: `#f59e0b` (a warm amber/gold)
- Background: `#f8fafc` (almost white, very light gray-blue)
- Body text: `#1e293b` (very dark navy gray)
- Muted text: `#64748b` (medium slate gray)

**Write the CSS:**

```css
body {
  background-color: #f8fafc;
  color: #1e293b;
}

h1, h2 {
  color: #2563eb;
}

.muted {
  color: #64748b;
}

.badge {
  background-color: #f59e0b;
  color: #1e293b;
}
```

**Expected output:** A clean, professional page with near-white background, very dark navy text, blue headings, muted slate paragraphs, and amber-gold badges.

**What-if challenge:** What is the shorthand for `#ffffff`? → `#fff`. Can you shorten `#2563eb`? → No, because `25`, `63`, and `eb` all have different characters in each pair.

---

### Exercise 4 — HSL Theme Builder

**Objective:** Build a complete color theme using only HSL, varying saturation and lightness from a single hue.

**Scenario:** You are building a "forest" themed website. The base hue is green (hue = 130).

**Requirements:**
- Page background: green, low saturation (20%), high lightness (95%) — very pale green
- Main headings: green, high saturation (60%), dark (30%) — dark forest green
- Sub-headings: green, medium saturation (50%), medium (45%) — medium green
- Body text: gray (saturation 0%), dark (25%) — dark gray
- Highlight color: orange (hue 30), high saturation (90%), medium lightness (55%) — warm orange

**Your CSS:**

```css
body {
  background-color: hsl(130, 20%, 95%);
  color: hsl(0, 0%, 25%);
}

h1 {
  color: hsl(130, 60%, 30%);
}

h2 {
  color: hsl(130, 50%, 45%);
}

.highlight {
  background-color: hsl(30, 90%, 55%);
  color: hsl(0, 0%, 10%);
}
```

**Expected output:** A beautiful, harmonious "forest" website theme with green tones throughout, readable dark gray body text, and warm orange accents.

**Self-check:** Notice how using HSL makes it easy to create a harmonious color family — you just pick one hue and vary the other two values!

---

### Exercise 5 — Transparency Overlay

**Objective:** Use RGBA to create a semi-transparent hero section overlay.

**Scenario:** You are building a website header that sits over a background image (you do not have the image yet, but the CSS needs to be ready). The hero section needs a dark overlay so white text is readable.

**Requirements:**
- Hero section background: 65% transparent black (`rgba`)
- Hero heading color: white
- Hero subtitle color: light gray (90% white in `rgba` so it is slightly softer)
- A decorative button: 40% transparent white background with white text

**Your CSS:**

```css
.hero {
  background-color: rgba(0, 0, 0, 0.65);
  padding: 60px 30px;
}

.hero h1 {
  color: rgb(255, 255, 255);
}

.hero p {
  color: rgba(255, 255, 255, 0.9);
}

.hero-btn {
  background-color: rgba(255, 255, 255, 0.4);
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.7);
}
```

**Expected output:** A dark, semi-transparent hero area with bright white heading, slightly softer white subtitle, and a frosted/glass-style button.

---

## Section 12 — Mini Project: Color a Full Web Page

Let us bring everything together in one complete project. You will apply all four color formats to style a full webpage.

### Project Brief

You are designing the homepage for a fictional tech startup called **"Lumina Tech"**. The brand identity is:
- Primary color: Blue (hue 220)
- Style: Modern, clean, professional
- Tone: Trustworthy but approachable

### Stage 1 — The HTML (Already Written For You)

```html
<!DOCTYPE html>
<html>
<head>
  <title>Lumina Tech</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header class="site-header">
    <h1>Lumina Tech</h1>
    <p class="tagline">Illuminating the future of software</p>
  </header>

  <nav class="navbar">
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Services</a>
    <a href="#">Contact</a>
  </nav>

  <main class="hero">
    <h2>We build brilliant software</h2>
    <p>Our team of engineers creates fast, reliable, and beautiful applications for businesses of every size.</p>
    <button class="cta-btn">Get Started</button>
  </main>

  <section class="features">
    <h3>Why Lumina?</h3>
    <p class="muted">Our clients trust us for three core reasons:</p>
    <p>Speed · Reliability · Design Excellence</p>
  </section>

  <footer class="site-footer">
    <p>© 2026 Lumina Tech. All rights reserved.</p>
  </footer>
</body>
</html>
```

### Stage 2 — Plan Your Colors

Before writing any CSS, plan the palette:

| Element | Color | Format | Reasoning |
|---------|-------|--------|-----------|
| Page background | Near-white | `#f0f4ff` | HEX — from brand guide |
| Header background | Deep blue | `hsl(220, 80%, 25%)` | HSL — easy to darken/lighten |
| Header text | White | `#ffffff` | HEX |
| Nav background | Slightly lighter blue | `hsl(220, 75%, 35%)` | HSL |
| Nav links | Light blue-white | `rgba(255,255,255,0.85)` | RGBA — slightly transparent |
| Hero heading | Dark navy | `rgb(15, 30, 80)` | RGB — precise dark navy |
| Hero paragraph | Dark gray | `#334155` | HEX |
| CTA button | Vivid blue | `hsl(220, 90%, 55%)` | HSL |
| Features background | Very light blue | `hsl(220, 40%, 97%)` | HSL |
| Muted text | Gray | `hsl(0, 0%, 55%)` | HSL |
| Footer background | Very dark | `#0f172a` | HEX |
| Footer text | Light gray | `rgba(255,255,255,0.7)` | RGBA — slightly transparent |

### Stage 3 — Write the CSS (Your Final Stylesheet)

```css
/* === Global Reset & Base === */
body {
  background-color: #f0f4ff;
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  color: #334155;
}

/* === Site Header === */
.site-header {
  background-color: hsl(220, 80%, 25%);
  padding: 30px 40px;
  text-align: center;
}

.site-header h1 {
  color: #ffffff;
  font-size: 40px;
  margin: 0;
}

.site-header .tagline {
  color: rgba(255, 255, 255, 0.75);
  font-size: 18px;
  margin: 8px 0 0 0;
}

/* === Navigation Bar === */
.navbar {
  background-color: hsl(220, 75%, 35%);
  padding: 12px 40px;
}

.navbar a {
  color: rgba(255, 255, 255, 0.85);
  margin-right: 24px;
  text-decoration: none;
  font-size: 16px;
}

/* === Hero Section === */
.hero {
  padding: 60px 40px;
  background-color: #f0f4ff;
}

.hero h2 {
  color: rgb(15, 30, 80);
  font-size: 32px;
}

.hero p {
  color: #334155;
  font-size: 18px;
  max-width: 600px;
}

/* === Call to Action Button === */
.cta-btn {
  background-color: hsl(220, 90%, 55%);
  color: #ffffff;
  border: none;
  padding: 14px 32px;
  font-size: 16px;
  cursor: pointer;
}

/* === Features Section === */
.features {
  background-color: hsl(220, 40%, 97%);
  padding: 40px 40px;
}

.features h3 {
  color: hsl(220, 80%, 30%);
  font-size: 24px;
}

.features .muted {
  color: hsl(0, 0%, 55%);
}

.features p {
  color: #334155;
}

/* === Footer === */
.site-footer {
  background-color: #0f172a;
  padding: 24px 40px;
  text-align: center;
}

.site-footer p {
  color: rgba(255, 255, 255, 0.7);
  font-size: 14px;
  margin: 0;
}
```

### Stage 4 — Milestone Outputs

After writing this CSS, your page should have:

- A deep navy blue header with a white company name and slightly transparent tagline
- A slightly lighter blue navigation bar with soft white links
- A clean near-white hero section with dark navy heading and dark gray body text
- A vivid blue call-to-action button
- A very light blue features section with muted gray secondary text
- A near-black footer with slightly transparent light gray text

### Reflection Questions

1. We used RGBA for the tagline and nav links. Why RGBA instead of just a color name like `lightgray`? (Hint: RGBA transparency is relative to the background, creating a natural relationship)
2. Why did we use HSL for the header, navbar, and features section? What is the benefit compared to using three separate HEX codes?
3. What color would `hsl(220, 80%, 50%)` produce? (Answer: a medium-bright blue — halfway between the header dark blue at 25% and a light blue at 75%)
4. If the brand decided to switch from blue to purple, how many values would need to change if the CSS was written in HSL? (Hint: only the hue number in each rule needs to change)
5. What is the difference between `rgba(0, 0, 0, 0.6)` and just `color: gray` for an overlay?

---

## Section 13 — Common Beginner Mistakes with CSS Colors

### Mistake 1 — Forgetting the `#` Before a HEX Code

**Wrong:**
```css
color: ff6347;
```

**Problem:** CSS does not know this is a HEX code without the `#`.

**Correct:**
```css
color: #ff6347;
```

---

### Mistake 2 — Writing a HEX Code With the Wrong Number of Characters

**Wrong:**
```css
color: #ff63; /* only 4 characters — not valid */
color: #ff63477a; /* 8 characters — valid only for HEX with alpha, but not standard CSS color */
```

**Problem:** HEX codes must be either **3 or 6 characters** (not counting the `#`).

**Correct:**
```css
color: #ff6347; /* 6 characters */
color: #f64;    /* 3 characters (shorthand) */
```

---

### Mistake 3 — Putting `%` Signs on RGB Values

**Wrong:**
```css
color: rgb(100%, 50%, 25%);
```

**Problem:** In the standard `rgb()` function, values are numbers 0–255, NOT percentages. (There is a lesser-known percentage form, but it is rarely used and easy to confuse.)

**Correct:**
```css
color: rgb(255, 128, 64);
```

---

### Mistake 4 — Forgetting `%` Signs on HSL Values

**Wrong:**
```css
color: hsl(120, 100, 50); /* missing % on saturation and lightness */
```

**Problem:** Saturation and lightness in `hsl()` **must** include the `%` symbol.

**Correct:**
```css
color: hsl(120, 100%, 50%);
```

---

### Mistake 5 — Alpha Value Greater Than 1

**Wrong:**
```css
color: rgba(255, 0, 0, 1.5); /* alpha greater than 1 */
```

**Problem:** The alpha value in `rgba()` and `hsla()` must be between 0 and 1. Values above 1 are treated as 1 by most browsers but are invalid.

**Correct:**
```css
color: rgba(255, 0, 0, 1.0); /* fully solid */
color: rgba(255, 0, 0, 0.5); /* half transparent */
```

---

### Mistake 6 — Using `colour` Instead of `color`

**Wrong:**
```css
p { colour: red; } /* British English spelling */
```

**Problem:** CSS uses American English. `colour` is not a valid CSS property.

**Correct:**
```css
p { color: red; }
```

---

### Mistake 7 — Trying to Use a Color Name That Does Not Exist

**Wrong:**
```css
color: lightnavy;     /* not a valid color name */
color: darkblue2;     /* not a valid color name */
color: #brandblue;    /* not a valid HEX code */
```

**Problem:** CSS only recognises 140 specific named colors. You cannot invent new names.

**Correct:**
```css
color: navy;          /* a valid dark blue name */
color: #003366;       /* a custom dark blue in HEX */
color: hsl(220, 80%, 20%); /* a custom dark blue in HSL */
```

---

### Mistake 8 — Confusing HSL Hue With RGB Channels

**Wrong thinking:** "For HSL green, I should write `hsl(0, 255, 0)`"

**Problem:** HSL and RGB work completely differently. HSL hue is a degree on the color wheel (0–360), not a channel value (0–255). Green in HSL is at hue `120`, not `0`.

**Correct:**
```css
/* Green in HSL */
color: hsl(120, 100%, 50%);

/* Green in RGB */
color: rgb(0, 255, 0);
```

---

## Section 14 — Reflection Questions

1. Name the five CSS color formats. Give one example of each.
2. What does the "A" stand for in RGBA and HSLA, and what values can it take?
3. What color does `rgb(0, 0, 0)` produce? What about `rgb(255, 255, 255)`?
4. In HSL, what does the hue value represent? Give the approximate hue number for red, yellow, green, and blue.
5. What is the difference between `hsl(200, 100%, 50%)` and `hsl(200, 0%, 50%)`?
6. Convert `rgb(255, 255, 0)` to a description: what color is it and why?
7. Can the HEX code `#336699` be shortened? If yes, what is the shorthand? If no, why not?
8. Can the HEX code `#aa33ff` be shortened? If yes, what is the shorthand?
9. Why would a company specify their brand color as `#1DA1F2` rather than just `blue`?
10. Write a CSS rule using HSLA that applies a 40% transparent red overlay to a `.warning` class.

---

## Completion Checklist

Before moving to Lesson 06, tick off each item:

- [ ] I understand that CSS has multiple color formats and they all produce the same visual result
- [ ] I can apply color to text, backgrounds, and borders using `color` and `background-color`
- [ ] I know at least 10 CSS color names and can use them
- [ ] I understand that RGB mixes Red, Green, Blue light with values 0–255
- [ ] I can write `rgb()` values for primary colors, black, white, and gray
- [ ] I understand what the alpha value does in `rgba()` and can write transparent colors
- [ ] I understand the structure of a HEX code: `#RRGGBB` (two characters per channel)
- [ ] I can decode a HEX code and identify whether it is reddish, bluish, greenish, etc.
- [ ] I know when I can and cannot use HEX shorthand
- [ ] I understand that HSL uses Hue (0–360), Saturation (0–100%), Lightness (0–100%)
- [ ] I can use HSL to create shades and tints of a color by varying lightness
- [ ] I can use HSL to create grays by setting saturation to 0%
- [ ] I understand `hsla()` transparency the same way I understand `rgba()`
- [ ] I have completed all 5 guided exercises
- [ ] I have completed the Lumina Tech mini-project
- [ ] I know the 8 common color mistakes and how to avoid them

---

## Lesson Summary

**CSS provides six color formats:**

1. **Named colors** — `red`, `DodgerBlue`, `MediumSeaGreen` — 140 predefined English words. Easy but limited.

2. **RGB** — `rgb(255, 99, 71)` — Mixes red, green, and blue light. Each channel is 0–255. Equal values = gray. All 255 = white. All 0 = black.

3. **RGBA** — `rgba(255, 99, 71, 0.5)` — RGB plus alpha transparency. Alpha goes from 0 (invisible) to 1 (solid).

4. **HEX** — `#ff6347` — A 6-character code (or 3-character shorthand) starting with `#`. Split into two-character pairs for Red (`RR`), Green (`GG`), Blue (`BB`). Most common in professional work.

5. **HSL** — `hsl(9, 100%, 64%)` — Hue (color wheel position, 0–360°), Saturation (vivid to gray, 0–100%), Lightness (dark to light, 0–100%). Most intuitive for designers.

6. **HSLA** — `hsla(9, 100%, 64%, 0.5)` — HSL plus alpha transparency.

**Where you apply color:**
- `color` → text color
- `background-color` → element background
- `border: 2px solid red` → border color

**Key rules to remember:**
- HEX always starts with `#`
- HEX must be 3 or 6 characters
- RGB values are 0–255 (no `%`)
- HSL saturation and lightness **require** `%`
- Alpha is 0.0 to 1.0 (not 0 to 100)
- CSS uses `color` not `colour`

---

*End of Lesson 05 — You are now ready to move on to Lesson 06: CSS Backgrounds*
