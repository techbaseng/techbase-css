---
render_with_liquid: false
title: "CSS Custom Fonts – The @font-face Rule"
nav_order: 53
---

# Lesson 53 — CSS Custom Fonts: The `@font-face` Rule

---

## Lesson Introduction

Have you ever visited a website and noticed that the text looked absolutely unique — not like any font you have seen in a word processor before? That is almost certainly a **custom font** loaded using CSS.

By default, browsers can only display fonts that are already installed on the user's computer. This is a very small, predictable list sometimes called **web-safe fonts** — think Arial, Times New Roman, or Courier. These fonts are reliable, but they are also generic. Every website that uses them looks similar.

The `@font-face` rule, introduced as part of modern CSS, completely solves this problem. It lets you point the browser at a font file of your choosing — stored on your own server — and the browser downloads and uses that font automatically. This gives you total typographic freedom: you can use elegant serif typefaces, geometric sans-serifs, handwritten scripts, monospaced coding fonts, and everything in between.

This lesson covers the entire `@font-face` rule from scratch — what it is, why it matters, every descriptor inside it, how to handle bold and italic variants, which font file formats exist and which to use today, and how to put everything together in a real-world project.

> 💡 **Real-world relevance:**
> Typography is one of the single biggest factors in how professional a website looks and feels. Companies spend enormous budgets on brand typefaces. `@font-face` is the CSS tool that lets you bring any of those typefaces to the web — and it is used on virtually every professional site built today.

---

## Prerequisite Concepts

Before starting, make sure you are comfortable with the following. If any of these are new, read the short explanation provided.

### What is a CSS property vs. a CSS at-rule?

A **CSS property** is a single styling instruction inside a selector block:

```css
p {
  color: red;        /* ← CSS property */
  font-size: 16px;   /* ← CSS property */
}
```

A **CSS at-rule** starts with the `@` symbol and is a higher-level instruction to the browser — it is not tied to a selector. It gives the browser configuration information:

```css
@font-face { ... }    /* ← CSS at-rule */
@media { ... }        /* ← CSS at-rule */
```

`@font-face` is an at-rule. It tells the browser "here is a font definition — remember this for later use."

### What is `font-family` in regular CSS?

You already know you can set a font on an element like this:

```css
p {
  font-family: Arial, sans-serif;
}
```

`font-family` tells the browser which font to use. With `@font-face`, you will define your own custom name, and then use it inside `font-family` exactly the same way.

### What is a font file?

A font file is a file on your computer or server that contains the shapes (called **glyphs**) of every letter, number, and symbol in that typeface. Different file formats encode those shapes in different ways. Common extensions include `.woff2`, `.woff`, `.ttf`, `.otf`, and `.eot`.

---

## Part 1 — Understanding the Problem `@font-face` Solves

### 1.1 The Web-Safe Font Problem

Before `@font-face`, web designers were stuck with a tiny set of fonts that came pre-installed on Windows and Mac computers. This included: Arial, Helvetica, Times New Roman, Georgia, Courier New, Verdana, and a few others.

**The problem:** every website using these fonts looked similar. There was no way to match a company's unique brand font on the web.

**The analogy:** Imagine you are a chef who can only cook using ingredients that every household already owns — salt, flour, eggs, and sugar. You could make bread, but you could never create the signature dish that makes your restaurant memorable. `@font-face` is like gaining access to the full market — you can import any ingredient you need.

### 1.2 What `@font-face` Does

`@font-face` allows you to:

1. **Define** a custom font by giving it a name and pointing to its file
2. **Describe** that font's weight (light, regular, bold) and style (normal, italic)
3. **Use** that font name anywhere in your CSS, just like any built-in font

The browser will then **download the font file** when someone visits your page and apply it to your text.

---

## Part 2 — Font File Formats You Need to Know

Before writing any code, you need to understand font file formats, because the `@font-face` rule requires you to specify the file path and its format.

### 2.1 The Main Font File Formats

| Format | Extension | Description |
|--------|-----------|-------------|
| **WOFF2** | `.woff2` | Web Open Font Format 2 — the best, most modern format. Smallest file size, widest support. **Recommended.** |
| **WOFF** | `.woff` | Web Open Font Format — older version of WOFF2. Good fallback for slightly older browsers. |
| **TTF** | `.ttf` | TrueType Font — works on many devices and older browsers. Larger file. |
| **OTF** | `.otf` | OpenType Font — similar to TTF. Supports advanced typographic features. |
| **EOT** | `.eot` | Embedded OpenType — used only by very old versions of Internet Explorer. No longer needed. |
| **SVG** | `.svg` | SVG Font — used by very old versions of Safari on iOS. No longer needed. |

### 2.2 Which Format Should You Use Today?

For modern web development (2024+), the advice is simple:

```
Use WOFF2 as your primary format.
Add WOFF as a fallback for slightly older browsers.
```

WOFF2 is supported by all modern browsers (Chrome, Firefox, Safari, Edge) and produces the smallest file sizes — meaning faster page loads. You typically do not need TTF, OTF, EOT, or SVG anymore.

**Practical pattern:**

```css
@font-face {
  font-family: "MyFont";
  src: url("myfont.woff2") format("woff2"),
       url("myfont.woff")  format("woff");
}
```

The browser reads the `src` list from top to bottom and uses the **first format it supports**. So always list WOFF2 first.

> 🤔 **Thinking prompt:** Why do you think WOFF2 produces smaller files than TTF? (Hint: WOFF2 uses compression, similar to how ZIP files make large files smaller.)

---

## Part 3 — The `@font-face` Rule: Full Anatomy

### 3.1 The Simplest Possible `@font-face`

Here is the absolute minimum you need to define and use a custom font:

```css
/* Step 1: Define the font */
@font-face {
  font-family: "Sansation";
  src: url(sansation_light.woff);
}

/* Step 2: Use the font */
div {
  font-family: "Sansation";
}
```

**Line-by-line breakdown:**

```css
@font-face {
```
This opens the font definition block. It tells the browser: "I am about to describe a font."

```css
  font-family: "Sansation";
```
This is the **name** you are assigning to this font. You invent this name — it can be anything you want (but it must be consistent between the `@font-face` block and wherever you use it). Wrap names containing spaces in quotes.

```css
  src: url(sansation_light.woff);
```
This is the **file path** to the font file. `url()` is a CSS function that takes a path as input. Here, `sansation_light.woff` must be a real file in the same folder as your CSS file (or you provide a full path like `fonts/sansation_light.woff`).

```css
}
```
Closes the `@font-face` block.

```css
div {
  font-family: "Sansation";
}
```
Now you use the font exactly like any other — by writing its name as the value of `font-family`. Every `<div>` element will now display in Sansation.

**Complete working example:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    @font-face {
      font-family: "Sansation";
      src: url(sansation_light.woff);
    }

    body {
      font-family: "Sansation", sans-serif;
      font-size: 20px;
    }
  </style>
</head>
<body>
  <p>This paragraph uses the Sansation custom font!</p>
  <p>Every character here is loaded from a font file.</p>
</body>
</html>
```

**Expected output:** Both paragraphs display in the Sansation typeface (assuming the font file exists at the correct path). If the file cannot be found, the browser falls back to `sans-serif`.

---

### 3.2 The `src` Descriptor in Detail

The `src` descriptor is the most important part of `@font-face`. It tells the browser **where to find** the font file. You can provide one location or multiple locations separated by commas:

**Single source (simple):**

```css
src: url("sansation_light.woff2");
```

**Multiple sources with format hints (recommended):**

```css
src: url("sansation_light.woff2") format("woff2"),
     url("sansation_light.woff")  format("woff");
```

**Why list multiple sources?** Because different browsers support different formats. By listing WOFF2 first and WOFF second, you ensure:
- Modern browsers use the better WOFF2 (smaller, faster)
- Older browsers fall back to WOFF

**What does `format("woff2")` do?** It is a **hint** telling the browser what type of file this is. This lets the browser skip downloading a file it cannot use, saving bandwidth.

**Example with TTF fallback (for maximum compatibility):**

```css
@font-face {
  font-family: "OpenSans";
  src: url("OpenSans-Regular.woff2") format("woff2"),
       url("OpenSans-Regular.woff")  format("woff"),
       url("OpenSans-Regular.ttf")   format("truetype");
}
```

The format strings and their matching file types:

| Format string     | File type |
|-------------------|-----------|
| `"woff2"`         | `.woff2`  |
| `"woff"`          | `.woff`   |
| `"truetype"`      | `.ttf`    |
| `"opentype"`      | `.otf`    |
| `"embedded-opentype"` | `.eot` |
| `"svg"`           | `.svg`    |

---

### 3.3 The `font-weight` Descriptor

**The problem:** what happens when someone bolds text that uses your custom font? By default, the browser tries to fake bold by making the letters thicker — called **faux bold**. This looks bad. The proper solution is to provide a **real bold font file** (which the font designer has crafted specifically for bold use).

You do this by adding a **second `@font-face` block** with the same `font-family` name, but pointing to the bold font file, and adding `font-weight: bold`:

```css
/* Regular weight */
@font-face {
  font-family: "Sansation";
  src: url("sansation_light.woff2") format("woff2");
  font-weight: normal;
}

/* Bold weight — separate file, same font-family name */
@font-face {
  font-family: "Sansation";
  src: url("sansation_bold.woff2") format("woff2");
  font-weight: bold;
}
```

**How the browser uses this:**

```css
p {
  font-family: "Sansation";
  /* font-weight is normal by default — uses sansation_light.woff2 */
}

strong {
  font-family: "Sansation";
  font-weight: bold;
  /* Matches the bold @font-face — uses sansation_bold.woff2 */
}
```

**What you will see:** Regular paragraphs use the proper light-weight Sansation file. Bold text (inside `<strong>` tags or with `font-weight: bold`) uses the proper bold Sansation file. No fake bolding.

You can also use numeric weights:

```css
@font-face {
  font-family: "MyFont";
  src: url("myfont-light.woff2") format("woff2");
  font-weight: 300;   /* Light */
}

@font-face {
  font-family: "MyFont";
  src: url("myfont-regular.woff2") format("woff2");
  font-weight: 400;   /* Regular (same as "normal") */
}

@font-face {
  font-family: "MyFont";
  src: url("myfont-bold.woff2") format("woff2");
  font-weight: 700;   /* Bold (same as "bold") */
}
```

The standard numeric weight scale:

| Value | Meaning           |
|-------|-------------------|
| `100` | Thin              |
| `200` | Extra Light       |
| `300` | Light             |
| `400` | Normal (Regular)  |
| `500` | Medium            |
| `600` | Semi Bold         |
| `700` | Bold              |
| `800` | Extra Bold        |
| `900` | Black (Heavy)     |

> 🤔 **Thinking prompt:** Why does providing a real bold font file produce better results than letting the browser fake bold? Think about the difference between a font designed by a professional typographer and a computer simply thickening every stroke.

---

### 3.4 The `font-style` Descriptor

Just like bold, italic text needs its own font file. Italics in quality fonts are not simply slanted versions of the regular font — they are often redesigned characters with different letterforms.

You add an italic variant with another `@font-face` block, this time with `font-style: italic`:

```css
/* Regular (upright) */
@font-face {
  font-family: "Sansation";
  src: url("sansation_light.woff2") format("woff2");
  font-style: normal;
  font-weight: normal;
}

/* Italic variant — separate file */
@font-face {
  font-family: "Sansation";
  src: url("sansation_italic.woff2") format("woff2");
  font-style: italic;
  font-weight: normal;
}

/* Bold italic — yet another file */
@font-face {
  font-family: "Sansation";
  src: url("sansation_bold_italic.woff2") format("woff2");
  font-style: italic;
  font-weight: bold;
}
```

**How the browser uses this:**

```css
em {
  font-family: "Sansation";
  font-style: italic;  /* Uses sansation_italic.woff2 */
}
```

The browser matches the `font-weight` and `font-style` values in the `@font-face` blocks to the values on the element, and picks the right file automatically.

---

### 3.5 The `font-stretch` Descriptor (Optional)

Some font families include **condensed** (narrower) or **expanded** (wider) versions. You can register these with `font-stretch`:

```css
@font-face {
  font-family: "MyFont";
  src: url("myfont-condensed.woff2") format("woff2");
  font-stretch: condensed;
}

@font-face {
  font-family: "MyFont";
  src: url("myfont-expanded.woff2") format("woff2");
  font-stretch: expanded;
}
```

Valid `font-stretch` values include: `ultra-condensed`, `extra-condensed`, `condensed`, `semi-condensed`, `normal`, `semi-expanded`, `expanded`, `extra-expanded`, `ultra-expanded`.

---

### 3.6 The `unicode-range` Descriptor (Optional)

The `unicode-range` descriptor tells the browser which specific characters (Unicode code points) are in this font file. This is a performance optimisation: the browser only downloads the font file if the webpage actually uses characters in that range.

**Example — A font only for Latin characters:**

```css
@font-face {
  font-family: "MyFont";
  src: url("myfont-latin.woff2") format("woff2");
  unicode-range: U+0000-00FF;  /* Basic Latin + Latin-1 Supplement */
}
```

**Example — A font only for Cyrillic characters:**

```css
@font-face {
  font-family: "MyFont";
  src: url("myfont-cyrillic.woff2") format("woff2");
  unicode-range: U+0400-04FF;  /* Cyrillic block */
}
```

This is especially useful for multilingual sites where you might load one font file for Latin text and another for Arabic, Chinese, or other scripts. The browser only downloads the file it actually needs for the content on the page.

---

### 3.7 Complete `@font-face` Descriptor Reference Table

Here is every descriptor you can use inside `@font-face`, sourced from the W3Schools reference:

| Descriptor | Values | Description |
|---|---|---|
| `font-family` | Any name | **Required.** The name you give this font for use in CSS. |
| `src` | `url(path) format(hint)` | **Required.** The location of the font file(s). |
| `font-weight` | `normal`, `bold`, `100`–`900` | Optional. The weight this file covers. Default: `normal`. |
| `font-style` | `normal`, `italic`, `oblique` | Optional. The style this file covers. Default: `normal`. |
| `font-stretch` | `condensed`, `normal`, `expanded`, etc. | Optional. The stretch (width) this file covers. Default: `normal`. |
| `unicode-range` | Unicode code point range | Optional. Which characters are in this file. Default: all characters (`U+0-10FFFF`). |

---

## Part 4 — Building a Complete Font Family

This section walks you through registering a full font family with multiple weights and styles — exactly how it is done in professional projects.

### 4.1 The Goal

Imagine you have downloaded the "Open Sans" font (a popular, free font from Google Fonts) and saved these files in a `fonts/` folder:

```
fonts/
  OpenSans-Regular.woff2
  OpenSans-Bold.woff2
  OpenSans-Italic.woff2
  OpenSans-BoldItalic.woff2
```

### 4.2 Registering All Four Variants

```css
/* 1. Regular */
@font-face {
  font-family: "Open Sans";
  src: url("fonts/OpenSans-Regular.woff2") format("woff2"),
       url("fonts/OpenSans-Regular.woff")  format("woff");
  font-weight: normal;   /* or 400 */
  font-style: normal;
}

/* 2. Bold */
@font-face {
  font-family: "Open Sans";
  src: url("fonts/OpenSans-Bold.woff2") format("woff2"),
       url("fonts/OpenSans-Bold.woff")  format("woff");
  font-weight: bold;     /* or 700 */
  font-style: normal;
}

/* 3. Italic */
@font-face {
  font-family: "Open Sans";
  src: url("fonts/OpenSans-Italic.woff2") format("woff2"),
       url("fonts/OpenSans-Italic.woff")  format("woff");
  font-weight: normal;   /* or 400 */
  font-style: italic;
}

/* 4. Bold Italic */
@font-face {
  font-family: "Open Sans";
  src: url("fonts/OpenSans-BoldItalic.woff2") format("woff2"),
       url("fonts/OpenSans-BoldItalic.woff")  format("woff");
  font-weight: bold;     /* or 700 */
  font-style: italic;
}
```

### 4.3 Using the Font Family

Now that all four variants are registered under the name `"Open Sans"`, you apply it using regular CSS `font-family`:

```css
/* Set the base font on the whole page */
body {
  font-family: "Open Sans", Arial, sans-serif;
  font-size: 16px;
}

/* Headings use bold automatically */
h1, h2, h3 {
  font-weight: bold;
  /* Browser matches @font-face with font-weight:bold → OpenSans-Bold.woff2 */
}

/* Emphasis uses italic automatically */
em {
  font-style: italic;
  /* Browser matches @font-face with font-style:italic → OpenSans-Italic.woff2 */
}

/* Bold AND italic */
strong em {
  font-weight: bold;
  font-style: italic;
  /* Browser uses OpenSans-BoldItalic.woff2 */
}
```

**Expected output:** Your entire page uses Open Sans. Headings are properly bold. Emphasised text is properly italic. Bold italic works correctly. All without any faux styling.

> 🤔 **Thinking prompt:** What would happen if you only registered the regular variant but used `font-weight: bold` on a heading? The browser would attempt to simulate bold by thickening the strokes — but the result would look inferior to a real bold font file.

---

## Part 5 — Where to Get Custom Fonts

You cannot invent font files yourself — you obtain them. Here are the main legitimate sources:

### 5.1 Google Fonts (Free)

Google Fonts provides hundreds of high-quality open-source fonts at `fonts.google.com`. You can download the font files for free and use them with `@font-face`, or use Google's hosted version with a simple `<link>` tag.

**Option A — Self-host (use `@font-face`):**

1. Go to `fonts.google.com`
2. Select your font, click "Download family"
3. Place the `.ttf` files in your project (or convert to WOFF2 using an online tool like `transfonter.org`)
4. Write your `@font-face` rules pointing to those files

**Option B — Use Google's CDN (no font files needed):**

```html
<link href="https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;700&display=swap" rel="stylesheet">
```

Then use it in CSS directly:

```css
body {
  font-family: "Open Sans", sans-serif;
}
```

### 5.2 Other Free Sources

- **Font Squirrel** (`fontsquirrel.com`) — free fonts with web font kits already prepared
- **DaFont** (`dafont.com`) — large collection, check licensing carefully
- **The League of Moveable Type** (`theleagueofmoveabletype.com`) — open-source typefaces

### 5.3 Paid Fonts

- **Adobe Fonts** (included with Creative Cloud)
- **Fonts.com**, **MyFonts.com** — commercial font libraries

> ⚠️ **Important:** Always check the font's **licence**. Some fonts are free for personal use only, not commercial use. Others require attribution. Google Fonts are all licensed for free use on websites.

---

## Part 6 — Guided Practice Exercises

### Exercise 1 — Your First Custom Font

**Objective:** Write a complete `@font-face` rule and apply it to a webpage.

**Scenario:** You are building a personal portfolio page and want to use the Sansation font for the body text.

**Steps:**

1. Assume you have downloaded `sansation_light.woff2` and placed it next to your CSS file.
2. Write the `@font-face` rule to define the font.
3. Apply it to the `<body>` element with a fallback to `sans-serif`.

**Expected code:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    @font-face {
      font-family: "Sansation";
      src: url("sansation_light.woff2") format("woff2"),
           url("sansation_light.woff")  format("woff");
      font-weight: normal;
      font-style: normal;
    }

    body {
      font-family: "Sansation", sans-serif;
      font-size: 18px;
      line-height: 1.6;
    }
  </style>
</head>
<body>
  <h1>Amara Okafor — Portfolio</h1>
  <p>Welcome to my design portfolio. I create beautiful, accessible digital experiences.</p>
</body>
</html>
```

**Expected output:** The heading and paragraph render in the Sansation typeface (light weight) instead of the browser's default.

**Self-check questions:**
- What would happen if you left out the fallback `sans-serif`?
- What would happen if the font file path was wrong?

---

### Exercise 2 — Adding a Bold Variant

**Objective:** Register both the regular and bold versions of a custom font and apply them correctly.

**Scenario:** You want headings on your portfolio to use the properly designed bold Sansation file.

**Expected code:**

```html
<style>
  /* Regular */
  @font-face {
    font-family: "Sansation";
    src: url("sansation_light.woff2") format("woff2");
    font-weight: normal;
    font-style: normal;
  }

  /* Bold */
  @font-face {
    font-family: "Sansation";
    src: url("sansation_bold.woff2") format("woff2");
    font-weight: bold;
    font-style: normal;
  }

  body {
    font-family: "Sansation", sans-serif;
    font-weight: normal;
  }

  h1 {
    font-weight: bold;   /* Triggers bold @font-face */
  }
</style>
```

**Expected output:** Body text is in light Sansation. The `<h1>` heading is in real bold Sansation (from the bold font file), not a browser-faked bold.

**Self-check questions:**
- Why do both `@font-face` blocks share the same `font-family` name?
- What distinguishes them from each other?

---

### Exercise 3 — Building a Full Font Stack

**Objective:** Register regular, bold, italic, and bold-italic variants of a font and use them all on one page.

**Scenario:** A school newsletter website uses the "NewsFont" typeface throughout.

```css
/* STEP 1: Register all four variants */
@font-face {
  font-family: "NewsFont";
  src: url("newsfont-regular.woff2") format("woff2");
  font-weight: 400;
  font-style: normal;
}

@font-face {
  font-family: "NewsFont";
  src: url("newsfont-bold.woff2") format("woff2");
  font-weight: 700;
  font-style: normal;
}

@font-face {
  font-family: "NewsFont";
  src: url("newsfont-italic.woff2") format("woff2");
  font-weight: 400;
  font-style: italic;
}

@font-face {
  font-family: "NewsFont";
  src: url("newsfont-bolditalic.woff2") format("woff2");
  font-weight: 700;
  font-style: italic;
}

/* STEP 2: Use the font family */
body {
  font-family: "NewsFont", Georgia, serif;
  font-size: 16px;
}

h2 {
  font-weight: 700;   /* → newsfont-bold.woff2 */
}

blockquote {
  font-style: italic; /* → newsfont-italic.woff2 */
}

.byline {
  font-weight: 700;
  font-style: italic; /* → newsfont-bolditalic.woff2 */
}
```

**HTML to test it:**

```html
<body>
  <h2>School Science Fair Results</h2>
  <p>The annual science fair attracted 42 student projects this year.</p>
  <blockquote>Science is not a subject — it is a way of thinking.</blockquote>
  <p class="byline">— Mrs Adeyemi, Science Department Head</p>
</body>
```

**Expected output:** Headings in bold, blockquote in italic, byline in bold italic — all using the correct font files, with no faux styling.

**What-if challenge:** What if you add `font-weight: 300` to a paragraph? Which file will the browser use? (The browser will use the closest available weight — in this case, 400/regular, since 300 is not registered.)

---

### Exercise 4 — Using `unicode-range` for Performance

**Objective:** Understand and apply `unicode-range` to split a font into language-specific files.

**Scenario:** You are building a bilingual (English + Greek) website. You only want to download the Greek font file on pages that actually contain Greek text.

```css
/* Latin characters */
@font-face {
  font-family: "MultiFont";
  src: url("multifont-latin.woff2") format("woff2");
  font-weight: normal;
  unicode-range: U+0000-00FF;  /* Basic Latin */
}

/* Greek characters */
@font-face {
  font-family: "MultiFont";
  src: url("multifont-greek.woff2") format("woff2");
  font-weight: normal;
  unicode-range: U+0370-03FF;  /* Greek and Coptic block */
}

body {
  font-family: "MultiFont", serif;
}
```

**Expected behaviour:** On a page with only English text, only `multifont-latin.woff2` is downloaded. On a page with Greek text, both files are downloaded. This saves bandwidth on pages that do not need all the characters.

**Self-check questions:**
- Why is `unicode-range` considered a performance feature?
- What happens on a page that uses neither Latin nor Greek characters?

---

## Part 7 — Mini Project: Custom-Branded Blog Page

In this project, you will build a simple blog article page that uses a custom font loaded with `@font-face`. The font will have regular, bold, and italic variants, all properly registered and used.

### Stage 1 — Project Structure

Create a project folder:

```
my-blog/
  index.html
  style.css
  fonts/
    playfair-regular.woff2
    playfair-bold.woff2
    playfair-italic.woff2
```

> **Note:** For this exercise, you can download the free Playfair Display font from Google Fonts (`fonts.google.com/specimen/Playfair+Display`), or any other font you prefer. Rename the files to match the paths above for simplicity.

---

### Stage 2 — CSS: Register the Font Family

In `style.css`:

```css
/* ===== CUSTOM FONT REGISTRATION ===== */

/* Regular */
@font-face {
  font-family: "Playfair";
  src: url("fonts/playfair-regular.woff2") format("woff2");
  font-weight: 400;
  font-style: normal;
}

/* Bold */
@font-face {
  font-family: "Playfair";
  src: url("fonts/playfair-bold.woff2") format("woff2");
  font-weight: 700;
  font-style: normal;
}

/* Italic */
@font-face {
  font-family: "Playfair";
  src: url("fonts/playfair-italic.woff2") format("woff2");
  font-weight: 400;
  font-style: italic;
}
```

**Milestone output:** The font definitions are ready. Nothing visible yet — definitions are not visual.

---

### Stage 3 — CSS: Style the Page

```css
/* ===== BASE STYLES ===== */

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Playfair", Georgia, serif;
  font-size: 18px;
  line-height: 1.8;
  color: #2c2c2c;
  background-color: #faf8f5;
  padding: 40px 20px;
}

/* ===== ARTICLE LAYOUT ===== */

article {
  max-width: 680px;
  margin: 0 auto;
}

/* ===== TYPOGRAPHY ===== */

/* Main headline — bold Playfair */
h1 {
  font-weight: 700;
  font-size: 2.4em;
  line-height: 1.3;
  margin-bottom: 8px;
}

/* Subheading — italic Playfair */
.subtitle {
  font-style: italic;
  font-size: 1.1em;
  color: #777;
  margin-bottom: 24px;
}

/* Byline — small, slightly muted */
.byline {
  font-size: 0.85em;
  color: #999;
  border-bottom: 1px solid #ddd;
  padding-bottom: 20px;
  margin-bottom: 30px;
}

/* Body text */
p {
  margin-bottom: 20px;
}

/* Pull quote — italic, larger, accented */
blockquote {
  font-style: italic;
  font-size: 1.2em;
  border-left: 4px solid #c0392b;
  padding-left: 20px;
  margin: 30px 0;
  color: #555;
}

/* Section heading — bold */
h2 {
  font-weight: 700;
  font-size: 1.5em;
  margin: 30px 0 10px;
}
```

**Milestone output:** A clean, typographically refined layout with clear hierarchy.

---

### Stage 4 — HTML: The Blog Content

In `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Custom Font Blog</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <article>
    <h1>Why Typography Is the Secret Language of Design</h1>
    <p class="subtitle">How the fonts you choose speak louder than the words they carry</p>
    <p class="byline">By Chidinma Obi &nbsp;|&nbsp; April 25, 2026</p>

    <p>
      Before a visitor reads a single word on your website, they have already
      formed an impression — and typography is the primary reason why. The
      typeface you choose communicates personality, credibility, and mood in the
      fraction of a second before cognition kicks in.
    </p>

    <blockquote>
      "Type is a beautiful group of letters, not a group of beautiful letters."
    </blockquote>

    <p>
      Consider two hospitals. One uses a rigid, monospaced font on their homepage.
      Another uses a clean, humanist sans-serif with generous line spacing. You
      feel the difference before you process it — trust, warmth, and clarity come
      from the letterforms themselves.
    </p>

    <h2>The Problem with System Fonts</h2>

    <p>
      For most of the web's early life, designers were trapped. The only fonts
      available were the handful pre-installed on users' computers: Arial, Times
      New Roman, Verdana, Courier. Every website looked generic because every
      website used the same half-dozen typefaces.
    </p>

    <p>
      The CSS <code>@font-face</code> rule changed everything. By pointing the
      browser at a font file on your server, you can use any typeface ever
      designed — and your visitor's computer never needs to have it installed.
    </p>

    <h2>Choosing the Right Custom Font</h2>

    <p>
      The best typeface is not the most decorative one — it is the one that
      best serves the content and the audience. A children's book needs warmth
      and friendliness. A legal firm needs authority and clarity. A fashion brand
      needs elegance and restraint.
    </p>

    <p>
      Modern web fonts, loaded via <code>@font-face</code> with WOFF2 format,
      add as little as 20–50 kilobytes per variant — a worthwhile trade for
      a distinctive, brand-consistent reading experience.
    </p>
  </article>
</body>
</html>
```

**Final output:** A beautifully typeset blog article where:
- The headline is in real bold Playfair Display
- The subtitle is in real italic Playfair Display
- Body text is in regular Playfair Display
- All loaded with `@font-face`, no external dependency

**Reflection questions:**
- Open your browser's developer tools (F12) and look at the Network tab. Can you see the font files being downloaded?
- What fallback font appears if the Playfair files cannot be found? (`Georgia` — the second value in your `font-family` stack)
- How would you add a light-weight (300) variant to this blog? What file would you need?

---

## Part 8 — Common Beginner Mistakes

### Mistake 1 — Wrong font file path

```css
/* ❌ WRONG — file is in a fonts/ subfolder but path doesn't include it */
@font-face {
  font-family: "MyFont";
  src: url("myfont.woff2") format("woff2");
}

/* ✅ CORRECT — path matches the actual file location */
@font-face {
  font-family: "MyFont";
  src: url("fonts/myfont.woff2") format("woff2");
}
```

**Symptom:** The browser falls back to the default font silently. Open your browser's console (F12 → Console) to see a 404 error for the font file.

---

### Mistake 2 — Inconsistent `font-family` name

```css
/* ❌ WRONG — defined as "MyFont" but used as "my-font" */
@font-face {
  font-family: "MyFont";
  src: url("myfont.woff2") format("woff2");
}

p {
  font-family: "my-font"; /* ← does not match! */
}

/* ✅ CORRECT — exact same name in both places */
p {
  font-family: "MyFont";
}
```

**Why:** Font family names are case-sensitive and must match exactly between `@font-face` and the usage site.

---

### Mistake 3 — Not adding a fallback font

```css
/* ❌ RISKY — if the font fails to load, the browser uses whatever it wants */
body {
  font-family: "Sansation";
}

/* ✅ SAFE — if the custom font fails, fall back to a sensible system font */
body {
  font-family: "Sansation", Arial, sans-serif;
}
```

**Why:** Network problems, server downtime, or incorrect file paths can prevent font loading. Always provide a fallback so your text remains readable.

---

### Mistake 4 — Using the wrong `format()` hint

```css
/* ❌ WRONG — file is WOFF2 but format says "woff" */
src: url("myfont.woff2") format("woff");

/* ✅ CORRECT — format matches the actual file type */
src: url("myfont.woff2") format("woff2");
```

**Why:** An incorrect format hint causes the browser to skip or mishandle the font file.

---

### Mistake 5 — Registering bold and italic without separate @font-face blocks

```css
/* ❌ WRONG — trying to handle all weights in one block */
@font-face {
  font-family: "MyFont";
  src: url("myfont.woff2") format("woff2");
  font-weight: normal bold;  /* ← this is not valid syntax */
}

/* ✅ CORRECT — one @font-face block per weight/style combination */
@font-face {
  font-family: "MyFont";
  src: url("myfont-regular.woff2") format("woff2");
  font-weight: normal;
}

@font-face {
  font-family: "MyFont";
  src: url("myfont-bold.woff2") format("woff2");
  font-weight: bold;
}
```

---

### Mistake 6 — Putting `@font-face` inside a selector

```css
/* ❌ WRONG — @font-face cannot go inside a selector */
.article {
  @font-face {
    font-family: "MyFont";
    src: url("myfont.woff2") format("woff2");
  }
  font-family: "MyFont";
}

/* ✅ CORRECT — @font-face must be at the top level of the stylesheet */
@font-face {
  font-family: "MyFont";
  src: url("myfont.woff2") format("woff2");
}

.article {
  font-family: "MyFont";
}
```

**Why:** `@font-face` is an at-rule, not a property. It defines a font globally for the entire stylesheet and cannot be scoped to a selector.

---

### Mistake 7 — Forgetting to include the format hint

```css
/* ❌ Not recommended — browser has to guess the format */
src: url("myfont.woff2");

/* ✅ Better — browser knows immediately what type of file this is */
src: url("myfont.woff2") format("woff2");
```

**Why:** Without the format hint, the browser may download the file before discovering it cannot parse it, wasting bandwidth. The hint allows the browser to skip files it cannot use without downloading them.

---

## Reflection Questions

Think through these questions to reinforce your understanding:

1. What is the difference between registering a font with `@font-face` and using a Google Fonts `<link>` tag? What are the advantages and disadvantages of each?
2. Why is it important to always include a fallback font in your `font-family` declaration?
3. You have one font file (`OpenSans-Regular.woff2`) but your `h1` has `font-weight: bold`. What will the browser do?
4. A colleague says "I'll just use one `@font-face` block and set `font-weight: normal bold`." What mistake are they making?
5. Why is WOFF2 preferred over TTF for web use?
6. What does `unicode-range` do, and when would you use it?
7. If a font file is hosted on a different server (a CDN), what extra consideration applies? (Hint: look up CORS — Cross-Origin Resource Sharing)
8. What is "faux bold" and why is it undesirable?

---

## Completion Checklist

Before moving on, confirm you can check off every item:

- [ ] I understand what `@font-face` is and why it exists
- [ ] I can explain the problem that web-safe fonts created for designers
- [ ] I know the five main font file formats (WOFF2, WOFF, TTF, OTF, EOT) and which to use today
- [ ] I can write a basic `@font-face` rule with `font-family` and `src`
- [ ] I understand the `format()` hint and why it matters in the `src` descriptor
- [ ] I can register a bold variant of a font with a second `@font-face` block
- [ ] I can register an italic variant of a font with a third `@font-face` block
- [ ] I understand how the browser matches `font-weight` and `font-style` to the right font file
- [ ] I know what `font-stretch` does and when to use it
- [ ] I understand `unicode-range` and its purpose for multilingual sites
- [ ] I know all the descriptors in the `@font-face` rule and their defaults
- [ ] I can write a full four-variant font family (regular, bold, italic, bold-italic)
- [ ] I know where to find free, legitimate font files (Google Fonts, Font Squirrel, etc.)
- [ ] I know the 7 common beginner mistakes and how to avoid them
- [ ] I completed the Custom-Branded Blog Page mini-project

---

## Lesson Summary

The CSS `@font-face` rule gives web designers complete typographic freedom. Before it, the web was limited to a small set of pre-installed "web-safe" fonts like Arial and Times New Roman. With `@font-face`, you can load any font file from your own server and apply it throughout your stylesheet.

A minimal `@font-face` rule requires two things: a `font-family` descriptor (the name you choose for the font) and a `src` descriptor (the path to the font file). The browser downloads the file and makes the font available by that name.

For production use, always provide multiple `src` entries — WOFF2 first (smallest, best supported), WOFF second as a fallback. Include the `format()` hint so the browser can skip incompatible files without downloading them.

To register bold and italic variants, you write **additional `@font-face` blocks** with the same `font-family` name but different `font-weight` and `font-style` values, each pointing to the appropriate font file. When the browser encounters text that needs bold or italic styling, it automatically picks the correct file. This avoids "faux bold" and "faux italic" — the poor-quality simulations produced when only one font file is registered.

Optional descriptors include `font-stretch` (for condensed or expanded variants) and `unicode-range` (to split a font into language-specific files, downloading only what the page actually needs).

| Descriptor | Required? | Purpose |
|---|---|---|
| `font-family` | ✅ Yes | The name to use in CSS |
| `src` | ✅ Yes | Path(s) to the font file(s) |
| `font-weight` | Optional | Weight this file covers |
| `font-style` | Optional | Style this file covers |
| `font-stretch` | Optional | Width variant |
| `unicode-range` | Optional | Character range for this file |

With `@font-face`, you have the tools to implement any brand typeface, ensure typographic consistency across operating systems, and build web pages that look exactly as designed — on every device, for every visitor.
