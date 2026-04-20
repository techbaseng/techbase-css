---
render_with_liquid: false
title: "CSS Attribute Selectors"
nav_order: 35
---

# Lesson 35: CSS Attribute Selectors

---

## Lesson Introduction

So far in your CSS journey, you have selected elements using their **tag name** (`p`, `div`, `img`), their **class** (`.menu-item`), or their **ID** (`#header`). These are great — but what if you need to style elements based on something more specific, like:

- All links that open in a new browser tab?
- All text input fields (but not checkbox inputs or button inputs)?
- All images whose file path ends in `.png`?
- All elements whose class name **starts with** the word "btn"?

For situations like these, CSS gives you a powerful tool called **attribute selectors**. Instead of selecting elements by their tag or class name, attribute selectors let you target elements based on the **attributes they carry** — and even on the **value** of those attributes, or **parts** of those values.

In this lesson, you will learn:

- What HTML attributes are and why they matter for CSS selection
- How to use the six core CSS attribute selectors
- The difference between exact-match and partial-match attribute selectors
- How to combine attribute selectors with element type selectors
- A critical real-world use case: styling form inputs by type
- How to apply these selectors confidently in your own projects

By the end, you will be writing powerful, precise CSS rules that require zero extra classes or IDs in your HTML.

---

## Prerequisite Concepts

### What Is an HTML Attribute?

An **attribute** is extra information attached to an HTML element, written inside the opening tag. Attributes always come in **name="value"** pairs.

```html
<!-- The word "href" is the attribute NAME. "https://example.com" is the VALUE. -->
<a href="https://example.com">Visit site</a>

<!-- "type" is the attribute. "text" is the value. -->
<input type="text" placeholder="Enter your name">

<!-- "target" is the attribute. "_blank" is the value. -->
<a href="page.html" target="_blank">Open in new tab</a>

<!-- "class" is the attribute. "btn-primary" is the value. -->
<button class="btn-primary">Submit</button>

<!-- "disabled" is an attribute with NO value — it is a "boolean" attribute. -->
<input type="text" disabled>
```

Every HTML element can carry one or more attributes. CSS attribute selectors let you use these attributes as selection criteria.

### What Do Attribute Selectors Look Like?

All CSS attribute selectors use **square brackets `[ ]`** around the attribute condition. You place them after the tag name (or alone, to match any tag):

```css
/* General pattern */
element[attribute]           /* Has the attribute */
element[attribute="value"]   /* Attribute equals exactly "value" */
element[attribute~="value"]  /* Attribute contains "value" as a whole word */
element[attribute|="value"]  /* Attribute equals "value" or starts with "value-" */
element[attribute^="value"]  /* Attribute starts with "value" */
element[attribute$="value"]  /* Attribute ends with "value" */
element[attribute*="value"]  /* Attribute contains "value" anywhere */
```

There are **seven** attribute selectors in total — four basic ones and three advanced ones. We will learn each one, one at a time.

---

## Section 1: The Basic Attribute Selectors

### 1.1 `[attribute]` — Select Elements That Have a Specific Attribute

**What it does:** Selects every element that has a particular attribute present, regardless of what the attribute's value is. Even elements with an empty attribute value will be selected.

**Why it exists:** Sometimes you just want to know whether an attribute exists on an element, not what its value is. For example, all `<a>` tags that have a `target` attribute — regardless of whether that target is `_blank` or `_self` or `_parent`.

**Syntax:**
```css
element[attribute] {
  /* styles */
}
```

**Real example from W3Schools — style all links that have a `target` attribute:**

```html
<!-- HTML: Three links, only two have target attribute -->
<a href="page1.html">Link without target</a>
<a href="page2.html" target="_blank">Link with target="_blank"</a>
<a href="page3.html" target="_self">Link with target="_self"</a>
```

```css
/* CSS */
a[target] {
  background-color: yellow;
}
```

**Expected Output:**
```
Link without target        ← no yellow background (no target attribute)
Link with target="_blank"  ← YELLOW background (has target attribute)
Link with target="_self"   ← YELLOW background (has target attribute)
```

**Line-by-line explanation:**
- `a` — We are targeting `<a>` (anchor/link) elements
- `[target]` — But only those that **have** the `target` attribute
- The first link has no `target` attribute at all, so it is NOT selected
- The second and third both have `target`, so they ARE selected — regardless of the value

> **Thinking prompt:** What if you wrote just `[target]` without the `a` in front? That would select **any** element that has a `target` attribute — not just links. You can omit the element type to cast a wider net.

---

**Second example — select all inputs that have a `placeholder` attribute:**

```html
<!-- HTML -->
<input type="text" placeholder="Your name">
<input type="text">
<input type="email" placeholder="Your email">
<input type="submit" value="Submit">
```

```css
/* CSS */
input[placeholder] {
  border: 2px solid green;
  padding: 5px;
}
```

**Expected Output:**
```
[ Your name  ] ← green border (has placeholder)
[            ] ← no green border (no placeholder)
[ Your email ] ← green border (has placeholder)
[ Submit     ] ← no green border (no placeholder)
```

---

### 1.2 `[attribute="value"]` — Select Elements with an Exact Attribute Value

**What it does:** Selects elements that have a specific attribute set to **exactly** the value you specify. The entire attribute value must match perfectly — not just part of it.

**Why it exists:** The previous selector finds all elements with an attribute. This one narrows it down to only those where the attribute has a specific exact value. The most common use: styling different types of form inputs differently.

**Syntax:**
```css
element[attribute="value"] {
  /* styles */
}
```

**Real example — style only links that open in a new tab:**

```html
<!-- HTML -->
<a href="home.html">Home</a>
<a href="docs.html" target="_blank">Documentation (new tab)</a>
<a href="about.html" target="_self">About (same tab)</a>
```

```css
/* CSS */
a[target="_blank"] {
  background-color: yellow;
}
```

**Expected Output:**
```
Home                        ← no yellow (no target attribute)
Documentation (new tab)     ← YELLOW (target="_blank" exactly matches)
About (same tab)            ← no yellow (target="_self" does NOT equal "_blank")
```

> **Key point:** `target="_self"` does NOT match `[target="_blank"]` because the value `_self` is not equal to `_blank`. This selector requires an **exact, complete match**.

---

**Second example — the most famous practical use: styling form inputs by type:**

```html
<!-- HTML: A simple registration form -->
<form>
  <input type="text"     placeholder="Full name">
  <input type="email"    placeholder="Email address">
  <input type="password" placeholder="Password">
  <input type="checkbox">
  <label>Remember me</label>
  <input type="submit"   value="Register">
</form>
```

```css
/* CSS: Style different input types differently — no class names needed! */
input[type="text"] {
  width: 200px;
  padding: 8px;
  background-color: lightyellow;
  border: 1px solid #aaa;
}

input[type="email"] {
  width: 200px;
  padding: 8px;
  background-color: lightblue;
  border: 1px solid blue;
}

input[type="password"] {
  width: 200px;
  padding: 8px;
  background-color: lightpink;
  border: 1px solid red;
}

input[type="submit"] {
  background-color: green;
  color: white;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
}
```

**Expected Output (visual):**
```
[ Full name     ]   ← lightyellow background (type="text")
[ Email address ]   ← lightblue background  (type="email")
[ Password      ]   ← lightpink background  (type="password")
[ ] Remember me     ← default checkbox style (type="checkbox" has no special rule)
[ Register      ]   ← green button          (type="submit")
```

> **Real-world use:** This technique is used constantly in web forms. Instead of adding class="text-input" or class="email-input" to every input element, attribute selectors let you target them based on what they already are.

---

### 1.3 `[attribute~="value"]` — Select Elements Whose Attribute Value Contains a Specific **Whole Word**

**What it does:** Selects elements where the attribute value is a **space-separated list of words** and the list contains the specified word. This is perfect for attributes that can hold multiple space-separated values — like the HTML `class` attribute or a `title` attribute with multiple words.

**The key rule:** The specified value must be a **complete word** in the list. It will NOT match partial words or words joined by hyphens.

**Syntax:**
```css
element[attribute~="value"] {
  /* styles */
}
```

**Real example — select elements whose `title` attribute contains the word "flower":**

```html
<!-- HTML -->
<p title="flower">Paragraph 1 — title is exactly "flower"</p>
<p title="summer flower">Paragraph 2 — title contains "flower" as a word</p>
<p title="flower new">Paragraph 3 — title starts with "flower"</p>
<p title="my-flower">Paragraph 4 — title is "my-flower" (hyphenated)</p>
<p title="flowers">Paragraph 5 — title is "flowers" (not the whole word "flower")</p>
```

```css
/* CSS */
p[title~="flower"] {
  background-color: yellow;
}
```

**Expected Output:**
```
Paragraph 1  ← YELLOW (title="flower" — "flower" is the whole value)
Paragraph 2  ← YELLOW (title="summer flower" — "flower" is one of the space-separated words)
Paragraph 3  ← YELLOW (title="flower new" — "flower" is the first word)
Paragraph 4  ← no yellow (title="my-flower" — "flower" is not a standalone word, it is joined by a hyphen)
Paragraph 5  ← no yellow (title="flowers" — "flowers" ≠ "flower", it is a different word)
```

> **Important distinction:** `[title~="flower"]` matches "flower" as a **standalone word** in a space-separated list. It does NOT match "my-flower" (hyphenated) or "flowers" (plural — a different word entirely). This behaviour is very similar to how the `class` selector `.flower` works.

---

**Second example — the class attribute with multiple values:**

```html
<!-- HTML: Elements with multiple classes (space-separated) -->
<div class="card featured product">Featured Product Card</div>
<div class="card product">Regular Product Card</div>
<div class="card sidebar featured">Featured Sidebar Card</div>
<div class="widget featured">Featured Widget</div>
```

```css
/* CSS: Select elements where class list contains the word "featured" */
[class~="featured"] {
  border: 3px solid gold;
  background-color: lightyellow;
}
```

**Expected Output:**
```
[ Featured Product Card  ]  ← gold border (class list contains "featured")
[ Regular Product Card   ]  ← no gold border (no "featured" in class list)
[ Featured Sidebar Card  ]  ← gold border (class list contains "featured")
[ Featured Widget        ]  ← gold border (class list contains "featured")
```

> **Thinking prompt:** Notice that `[class~="featured"]` does exactly the same thing as the class selector `.featured`. This helps you understand how the `~=` operator works — it matches whole words in a space-separated list.

---

### 1.4 `[attribute|="value"]` — Select Elements Whose Attribute Value Is Exactly the Value, or Starts with the Value Followed by a Hyphen

**What it does:** Selects elements where the attribute value is either:
- **Exactly** the specified value (e.g., `"top"`), OR
- The specified value **followed immediately by a hyphen** (`-`) (e.g., `"top-text"` or `"top-section"`)

**Why it exists:** This selector was specifically designed for language codes, which use hyphen notation. For example, `lang="en"` (English), `lang="en-US"` (American English), `lang="en-GB"` (British English). The `|=` selector lets you match `lang="en"` AND `lang="en-US"` AND `lang="en-GB"` all at once with `[lang|="en"]`.

**The critical rule:** The value must be a **whole word** — not a substring inside a longer word. `"top-text"` matches `[class|="top"]`, but `"topping"` does NOT.

**Syntax:**
```css
element[attribute|="value"] {
  /* styles */
}
```

**Real example — select all elements whose class is "top" or starts with "top-":**

```html
<!-- HTML -->
<p class="top">Class is exactly "top"</p>
<p class="top-text">Class starts with "top-"</p>
<p class="top-section">Class starts with "top-"</p>
<p class="topper">Class starts with "top" but NOT followed by a hyphen</p>
<p class="my-top">Class contains "top" but doesn't START with it</p>
```

```css
/* CSS */
[class|="top"] {
  background-color: yellow;
}
```

**Expected Output:**
```
Class is exactly "top"                           ← YELLOW (exact match)
Class starts with "top-"                         ← YELLOW ("top" + hyphen)
Class starts with "top-"                         ← YELLOW ("top" + hyphen)
Class starts with "top" but NOT followed by a hyphen  ← no yellow ("topper" has no hyphen after "top")
Class contains "top" but doesn't START with it   ← no yellow (doesn't start with "top")
```

**Language code example — the original purpose of this selector:**

```html
<!-- HTML: paragraphs in different English variants -->
<p lang="en">Hello!</p>
<p lang="en-US">Howdy, y'all!</p>
<p lang="en-GB">Cheerio!</p>
<p lang="fr">Bonjour!</p>
```

```css
/* CSS: Select all English language paragraphs (any variant) */
p[lang|="en"] {
  font-style: italic;
  color: navy;
}
```

**Expected Output:**
```
Hello!         ← navy italic (lang="en" — exact match)
Howdy, y'all!  ← navy italic (lang="en-US" — "en" + hyphen)
Cheerio!       ← navy italic (lang="en-GB" — "en" + hyphen)
Bonjour!       ← normal style (lang="fr" — not "en" or "en-*")
```

---

## Section 2: The Advanced Attribute Selectors (Partial-Value Matching)

The first four selectors all require either exact matches or whole-word matches. The next three are more flexible — they match **any part** of the attribute value. These are called **partial-value matching selectors** or **substring selectors**.

> **Quick analogy:** Think of these like the "search and find" functions in a text editor. `^=` is like searching from the start of a word. `$=` is like searching the end. `*=` is like searching anywhere in the text.

---

### 2.1 `[attribute^="value"]` — Attribute Value **Starts With** the Specified Value

**What it does:** Selects elements where the attribute value **begins with** the specified string. Unlike `|=`, the value does NOT need to be a whole word — it can be any starting substring.

**Syntax:**
```css
element[attribute^="value"] {
  /* styles */
}
```

**Real example — select all elements whose class value starts with "top":**

```html
<!-- HTML -->
<p class="top">Exactly "top"</p>
<p class="top-text">Starts with "top-"</p>
<p class="topper">Starts with "top" (no hyphen needed!)</p>
<p class="my-top-class">Contains "top" but doesn't START with it</p>
<p class="bottom-top">Ends with "top", doesn't start with it</p>
```

```css
/* CSS */
[class^="top"] {
  background-color: yellow;
}
```

**Expected Output:**
```
Exactly "top"                          ← YELLOW (starts with "top")
Starts with "top-"                     ← YELLOW (starts with "top")
Starts with "top" (no hyphen needed!)  ← YELLOW (starts with "top")
Contains "top" but doesn't START with it  ← no yellow (starts with "my", not "top")
Ends with "top", doesn't start with it    ← no yellow (starts with "bottom")
```

> **Compare with `|=`:** The key difference is that `^="top"` matches `"topper"` (starts with "top" even without a hyphen), while `|="top"` would NOT match `"topper"` (requires "top" to be a whole word). The `^=` operator is purely about string position — is this text at the very beginning?

---

**Practical use — style all external links (those whose href starts with "https"):**

```html
<!-- HTML -->
<a href="https://google.com">Google (external)</a>
<a href="https://github.com">GitHub (external)</a>
<a href="about.html">About page (internal)</a>
<a href="contact.html">Contact page (internal)</a>
```

```css
/* CSS: Mark all external links with a special colour */
a[href^="https"] {
  color: green;
  font-weight: bold;
}
```

**Expected Output:**
```
Google (external)      ← GREEN + bold (href starts with "https")
GitHub (external)      ← GREEN + bold (href starts with "https")
About page (internal)  ← normal (href starts with "about", not "https")
Contact page (internal) ← normal (href starts with "contact", not "https")
```

> **Real-world use:** Many websites use `a[href^="https"]` or `a[href^="http"]` to automatically style external links differently from internal ones — adding an external link icon, a different colour, or an underline style.

---

### 2.2 `[attribute$="value"]` — Attribute Value **Ends With** the Specified Value

**What it does:** Selects elements where the attribute value **ends with** the specified string. Again, it does not need to be a whole word — any ending substring works.

**Syntax:**
```css
element[attribute$="value"] {
  /* styles */
}
```

**Real example — select elements whose class ends with "test":**

```html
<!-- HTML -->
<p class="unit-test">Ends with "test"</p>
<p class="integration-test">Ends with "test"</p>
<p class="testing">Contains "test" but ends with "ing"</p>
<p class="protest">Ends with "test" but is "protest"</p>
<p class="best">Ends with "est" not "test"</p>
```

```css
/* CSS */
[class$="test"] {
  background-color: yellow;
}
```

**Expected Output:**
```
Ends with "test"               ← YELLOW (class ends with "test")
Ends with "test"               ← YELLOW (class ends with "test")
Contains "test" but ends with "ing" ← no yellow (ends with "ing")
Ends with "test" but is "protest"  ← YELLOW (ends with "test")
Ends with "est" not "test"         ← no yellow (ends with "est" not "test")
```

---

**Practical use — style all PDF links differently from other links:**

```html
<!-- HTML -->
<a href="report-2024.pdf">Annual Report (PDF)</a>
<a href="brochure.pdf">Company Brochure (PDF)</a>
<a href="terms.html">Terms of Service</a>
<a href="contact.html">Contact Us</a>
```

```css
/* CSS: Highlight all links ending in .pdf */
a[href$=".pdf"] {
  color: darkred;
  font-weight: bold;
  text-decoration: underline;
}

/* Optional: Add a small PDF label after each PDF link */
a[href$=".pdf"]::after {
  content: " [PDF]";
  font-size: 0.8em;
  color: grey;
}
```

**Expected Output:**
```
Annual Report (PDF) [PDF]      ← dark red, bold (href ends with ".pdf")
Company Brochure (PDF) [PDF]   ← dark red, bold (href ends with ".pdf")
Terms of Service               ← normal style (href ends with ".html")
Contact Us                     ← normal style (href ends with ".html")
```

> **Real-world use:** The `$=` selector is incredibly useful for automatically distinguishing file types in navigation links — PDF downloads, ZIP archives, external documents — without adding any extra classes.

---

### 2.3 `[attribute*="value"]` — Attribute Value **Contains** the Specified Value Anywhere

**What it does:** Selects elements where the attribute value **contains** the specified string anywhere — at the beginning, middle, or end. It does not need to be a whole word.

**Syntax:**
```css
element[attribute*="value"] {
  /* styles */
}
```

**Real example — select elements whose class contains "te" anywhere:**

```html
<!-- HTML -->
<p class="unite">Contains "te" inside</p>
<p class="internet">Contains "te" inside</p>
<p class="technology">Contains "te" at start</p>
<p class="rate">Contains "te" at end</p>
<p class="testing">Contains "te" at start</p>
<p class="box">Contains no "te"</p>
```

```css
/* CSS */
[class*="te"] {
  background-color: yellow;
}
```

**Expected Output:**
```
unite       ← YELLOW ("te" is inside "unite")
internet    ← YELLOW ("te" is inside "internet")
technology  ← YELLOW ("te" is at the start)
rate        ← YELLOW ("te" is at the end)
testing     ← YELLOW ("te" is at the start)
box         ← no yellow (no "te" anywhere in "box")
```

---

**Practical use — style all links pointing to any Google property:**

```html
<!-- HTML -->
<a href="https://google.com">Google Search</a>
<a href="https://maps.google.com">Google Maps</a>
<a href="https://docs.google.com/document">Google Docs</a>
<a href="https://github.com">GitHub (not Google)</a>
<a href="https://youtube.com">YouTube</a>
```

```css
/* CSS: Style any link that contains "google" anywhere in the href */
a[href*="google"] {
  color: #4285F4;   /* Google's blue colour */
  font-weight: bold;
}
```

**Expected Output:**
```
Google Search    ← Google blue + bold ("google" in "google.com")
Google Maps      ← Google blue + bold ("google" in "maps.google.com")
Google Docs      ← Google blue + bold ("google" in "docs.google.com")
GitHub (not Google) ← normal (no "google" in "github.com")
YouTube          ← normal (no "google" in "youtube.com")
```

---

## Section 3: Complete Reference Table

Here is a summary of all seven attribute selectors in one place:

| Selector | What It Matches | Example |
|----------|----------------|---------|
| `[attr]` | Elements that **have** the attribute (any value) | `a[target]` — all links with a target attribute |
| `[attr="val"]` | Attribute value is **exactly** "val" | `input[type="text"]` — only text inputs |
| `[attr~="val"]` | Attribute is a space-separated list containing **whole word** "val" | `[title~="flower"]` — title contains "flower" as a word |
| `[attr\|="val"]` | Attribute is **exactly** "val" **or** starts with "val-" (hyphen) | `[lang\|="en"]` — English language variants |
| `[attr^="val"]` | Attribute value **starts with** "val" | `[class^="btn"]` — classes beginning with "btn" |
| `[attr$="val"]` | Attribute value **ends with** "val" | `a[href$=".pdf"]` — links to PDF files |
| `[attr*="val"]` | Attribute value **contains** "val" anywhere | `[class*="icon"]` — any class containing "icon" |

> **Memory trick:** Think of the operators as:
> - `~=` → word in a **~**list (tilde = list/wave/many)
> - `|=` → value or "value**|**hyphen" (pipe = divider, like a hyphen)
> - `^=` → **^**top / starts (caret points UP — to the beginning)
> - `$=` → en**$** / ends (dollar sign closes things — the end)
> - `*=` → **\*** = wildcard = anywhere (asterisk = "anything goes")

---

## Section 4: Combining Attribute Selectors

### Combining with an Element Type

You can always narrow an attribute selector by placing a tag name in front of it. This targets only elements of that type that also match the attribute condition.

```css
/* Any element with target attribute */
[target] { color: red; }

/* Only <a> elements with a target attribute */
a[target] { color: red; }

/* Only <input> elements with type="text" */
input[type="text"] { background: yellow; }

/* Any element with class containing "icon" */
[class*="icon"] { width: 24px; }

/* Only <img> elements whose src ends with ".png" */
img[src$=".png"] { border: 2px solid blue; }
```

---

### Combining Multiple Attribute Selectors

You can chain multiple attribute selectors together to create very precise rules. Just write them one after another with no space between them:

```css
/* Select input elements that are BOTH type="text" AND have a placeholder attribute */
input[type="text"][placeholder] {
  border: 2px solid green;
}
```

```html
<!-- HTML -->
<input type="text" placeholder="Your name">  ← GREEN border (both match)
<input type="text">                          ← no green (no placeholder)
<input type="email" placeholder="Email">     ← no green (type is "email" not "text")
```

---

**Another multi-selector example — style only HTTPS links that also open in a new tab:**

```html
<!-- HTML -->
<a href="https://google.com" target="_blank">Google (HTTPS + new tab)</a>
<a href="https://github.com">GitHub (HTTPS only)</a>
<a href="http://oldsite.com" target="_blank">Old site (new tab, not HTTPS)</a>
<a href="about.html">About (internal)</a>
```

```css
/* CSS: Only links that are BOTH https AND open in a new tab */
a[href^="https"][target="_blank"] {
  color: green;
  font-weight: bold;
}
```

**Expected Output:**
```
Google (HTTPS + new tab)    ← GREEN + bold (both conditions met)
GitHub (HTTPS only)         ← normal (target attribute missing)
Old site (new tab, not HTTPS) ← normal (href doesn't start with "https")
About (internal)            ← normal (neither condition met)
```

---

## Section 5: Styling Forms with Attribute Selectors — A Practical Deep Dive

One of the most common and important real-world uses of attribute selectors is **styling HTML forms**. Forms contain many different `<input>` types — text, email, password, checkbox, radio, range, file, submit, and more. Without attribute selectors, you would need a separate class for each type. With attribute selectors, you can target them precisely using what they already have.

### Complete Styled Form Example

```html
<!-- HTML: A full registration form -->
<form class="registration-form">
  <label>Full Name:</label>
  <input type="text" placeholder="Enter your full name">

  <label>Email:</label>
  <input type="email" placeholder="Enter your email">

  <label>Password:</label>
  <input type="password" placeholder="Create a password">

  <label>Age:</label>
  <input type="number" placeholder="Your age" min="18" max="120">

  <label>
    <input type="checkbox"> I agree to the terms
  </label>

  <input type="reset" value="Clear Form">
  <input type="submit" value="Create Account">
</form>
```

```css
/* CSS: Style each input type differently using attribute selectors */

/* Base styles for all text-like inputs */
input[type="text"],
input[type="email"],
input[type="password"],
input[type="number"] {
  width: 280px;
  padding: 10px 12px;
  margin-bottom: 12px;
  border-radius: 4px;
  font-size: 1em;
  display: block;
}

/* Text input — soft yellow */
input[type="text"] {
  background-color: #fffde7;
  border: 1px solid #f9a825;
}

/* Email input — soft blue */
input[type="email"] {
  background-color: #e3f2fd;
  border: 1px solid #1565c0;
}

/* Password input — soft red */
input[type="password"] {
  background-color: #fce4ec;
  border: 1px solid #c62828;
}

/* Number input — soft green */
input[type="number"] {
  background-color: #e8f5e9;
  border: 1px solid #2e7d32;
}

/* Checkbox — slightly larger */
input[type="checkbox"] {
  width: 18px;
  height: 18px;
  cursor: pointer;
}

/* Reset button — grey */
input[type="reset"] {
  background-color: #9e9e9e;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-right: 10px;
}

/* Submit button — green */
input[type="submit"] {
  background-color: #2e7d32;
  color: white;
  padding: 10px 25px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}

input[type="submit"]:hover {
  background-color: #1b5e20;
}
```

**Expected Output:**
```
Full Name: [ __________________ ]  ← yellow background, orange border
Email:     [ __________________ ]  ← blue background, blue border
Password:  [ __________________ ]  ← pink background, red border
Age:       [ __________________ ]  ← green background, green border
[ ] I agree to the terms           ← slightly larger checkbox
[ Clear Form ]  [ Create Account ] ← grey / green buttons
```

> **Real-world insight:** Notice there are **zero class attributes** on any of the input elements! All the styling is done purely through attribute selectors. This is clean, readable HTML and clean, maintainable CSS. Many professional CSS frameworks use this exact pattern for form styling.

---

## Section 6: Guided Practice Exercises

### Exercise 1: Warm-Up — Target by Attribute Presence

**Objective:** Use the `[attribute]` selector to identify required form fields.

**Scenario:** You have a form where some fields are marked as `required`. You want to give all required inputs a red left border to signal to users that these fields must be filled in.

**Starter HTML:**
```html
<form>
  <input type="text" placeholder="Full name" required>
  <input type="text" placeholder="Nickname">
  <input type="email" placeholder="Email" required>
  <input type="tel" placeholder="Phone number">
  <input type="submit" value="Submit">
</form>
```

**Your task:** Write a CSS rule using `[required]` to give all required inputs:
- A `3px solid red` left border
- A light red background: `#fff5f5`
- `8px` padding

**Expected Output:**
```
[ Full name  ] ← red left border + light red bg (has required)
[ Nickname   ] ← default border (no required)
[ Email      ] ← red left border + light red bg (has required)
[ Phone      ] ← default border (no required)
[ Submit     ] ← default (no required)
```

**Self-check Questions:**
- Does the submit button get the red border? Why or why not?
- What would happen if you changed `[required]` to `input[required]`? Would anything look different?
- Add `required` to the phone number input — does it automatically get the red border?

---

### Exercise 2: Exact Match — Style Link Destinations

**Objective:** Use `[attribute="value"]` to differentiate where links go.

**Scenario:** A news website navigation has links that either stay on the same page or open a new tab. You want all "new tab" links to have a distinct colour.

**HTML to work with:**
```html
<nav>
  <a href="home.html">Home</a>
  <a href="about.html" target="_self">About</a>
  <a href="https://twitter.com" target="_blank">Twitter</a>
  <a href="https://facebook.com" target="_blank">Facebook</a>
  <a href="contact.html">Contact</a>
</nav>
```

**Your task:** Write a CSS rule that:
- Targets all `<a>` elements with `target="_blank"`
- Sets their colour to `#e65100` (orange)
- Sets `font-weight: bold`

**Expected Output:**
```
Home     ← default colour (no target attribute)
About    ← default colour (target="_self", not "_blank")
Twitter  ← ORANGE + bold (target="_blank")
Facebook ← ORANGE + bold (target="_blank")
Contact  ← default colour (no target attribute)
```

---

### Exercise 3: Partial Match — File Type Indicators

**Objective:** Use `$=` to automatically style links by file type.

**Scenario:** A school resources page has links to different file types. You want each file type to look visually different so students know what they are downloading before clicking.

**HTML:**
```html
<ul>
  <li><a href="chapter1.pdf">Chapter 1 Notes</a></li>
  <li><a href="worksheet.pdf">Worksheet</a></li>
  <li><a href="slides.pptx">Presentation Slides</a></li>
  <li><a href="data.xlsx">Grade Data</a></li>
  <li><a href="home.html">Go to Homepage</a></li>
</ul>
```

**Your task:**
- Style links ending in `.pdf` → `color: darkred`
- Style links ending in `.pptx` → `color: darkorange`
- Style links ending in `.xlsx` → `color: darkgreen`
- All styled links should also have `font-weight: bold`

**Expected Output:**
```
Chapter 1 Notes      ← DARK RED + bold (.pdf)
Worksheet            ← DARK RED + bold (.pdf)
Presentation Slides  ← DARK ORANGE + bold (.pptx)
Grade Data           ← DARK GREEN + bold (.xlsx)
Go to Homepage       ← normal (it's a .html file)
```

**What-If Challenge:** Add this rule too:
```css
a[href$=".pdf"]::after {
  content: " 📄";
}
```
What does it add after every PDF link? Why is `::after` useful here?

---

### Exercise 4: Contains Selector — Icon Classes

**Objective:** Use `*=` to target elements that belong to a broad category.

**Scenario:** Your icon library uses class names like `icon-home`, `icon-user`, `icon-settings`, `icon-bell`. You want all icon elements to share the same base size without touching the HTML.

**HTML:**
```html
<span class="icon-home">🏠</span>
<span class="icon-user">👤</span>
<span class="btn-primary">Submit</span>
<span class="icon-settings">⚙️</span>
<span class="icon-bell">🔔</span>
<span class="label-warning">Warning!</span>
```

**Your task:** Write ONE CSS rule using `[class*="icon"]` that gives all icon elements:
- `font-size: 24px`
- `margin: 0 8px`
- `cursor: pointer`

**Expected Output:**
```
🏠  👤  Submit  ⚙️  🔔  Warning!
↑ ↑ styled   ↑ ↑   ↑ not styled
```
(The "Submit" button and "Warning!" label are NOT targeted because their class does not contain "icon".)

---

## Section 7: Mini Project — Auto-Styled Resource Directory

In this project, you will build a complete resource directory page that uses **only attribute selectors** to apply all its link and input styling — no class attributes needed on the elements being styled.

### Project Overview

You are building a resources page for a web development course. The page has:
- A search bar and filter input
- Navigation links (some external, some internal)
- A file download list with mixed file types
- A contact form with multiple input types

All styling will be achieved using attribute selectors.

---

### Stage 1 — HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Course Resources</title>
  <link rel="stylesheet" href="resources.css">
</head>
<body>

  <header>
    <h1>Web Development Resources</h1>
    <!-- Search bar — has a placeholder and type="search" -->
    <input type="search" placeholder="Search resources...">
  </header>

  <!-- Navigation: mix of internal and external links -->
  <nav>
    <a href="index.html">Home</a>
    <a href="lessons.html">Lessons</a>
    <a href="https://developer.mozilla.org" target="_blank">MDN Docs</a>
    <a href="https://css-tricks.com" target="_blank">CSS-Tricks</a>
    <a href="contact.html">Contact</a>
  </nav>

  <!-- Downloads: mix of file types -->
  <section class="downloads">
    <h2>Downloads</h2>
    <ul>
      <li><a href="css-cheatsheet.pdf">CSS Cheat Sheet</a></li>
      <li><a href="html-reference.pdf">HTML Reference Guide</a></li>
      <li><a href="project-template.zip">Starter Project Template</a></li>
      <li><a href="grade-tracker.xlsx">Grade Tracker</a></li>
      <li><a href="lesson-slides.pptx">Lesson Slides</a></li>
      <li><a href="extra-notes.html">Extra Notes</a></li>
    </ul>
  </section>

  <!-- Contact form: multiple input types -->
  <section class="contact">
    <h2>Contact Instructor</h2>
    <form>
      <input type="text"     placeholder="Your name"    required>
      <input type="email"    placeholder="Your email"   required>
      <input type="tel"      placeholder="Phone (optional)">
      <input type="number"   placeholder="Student ID"   required>
      <textarea placeholder="Your message..." rows="4"></textarea>
      <div>
        <input type="checkbox" id="notify">
        <label for="notify">Notify me by email</label>
      </div>
      <input type="reset"  value="Clear">
      <input type="submit" value="Send Message">
    </form>
  </section>

</body>
</html>
```

---

### Stage 2 — CSS (resources.css)

```css
/* resources.css — ALL element styling uses attribute selectors */

/* === RESET & BASE === */
* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: Arial, sans-serif;
  max-width: 860px;
  margin: 0 auto;
  padding: 20px;
  background: #f5f5f5;
  color: #333;
}

h1, h2 { margin-bottom: 12px; color: #1a237e; }
header, nav, section { margin-bottom: 30px; }
ul { list-style: none; padding: 0; }
li { margin-bottom: 6px; }
form { display: flex; flex-direction: column; gap: 10px; max-width: 420px; }
textarea { padding: 10px; border-radius: 4px; border: 1px solid #aaa; font-size: 1em; }

/* ================================================
   1. SEARCH INPUT — target by exact type
   ================================================ */
input[type="search"] {
  width: 100%;
  padding: 10px 14px;
  border: 2px solid #1a237e;
  border-radius: 20px;       /* Pill shape for the search bar */
  font-size: 1em;
  margin-top: 8px;
  outline: none;
}

/* ================================================
   2. NAVIGATION LINKS
   ================================================ */

/* All nav links — base style */
nav a {
  display: inline-block;
  margin-right: 12px;
  padding: 6px 12px;
  border-radius: 4px;
  text-decoration: none;
  color: #333;
  background: #e0e0e0;
}

/* External links (those that START with http) */
nav a[href^="http"] {
  background-color: #e3f2fd;
  color: #1565c0;
  font-weight: bold;
}

/* External links that also open in a new tab */
nav a[href^="http"][target="_blank"]::after {
  content: " ↗";            /* Arrow icon to signal new tab */
  font-size: 0.75em;
}

/* ================================================
   3. DOWNLOAD LINKS — by file extension
   ================================================ */

/* PDF links — dark red */
a[href$=".pdf"] {
  color: #b71c1c;
  font-weight: bold;
}
a[href$=".pdf"]::before { content: "📄 "; }

/* ZIP files — purple */
a[href$=".zip"] {
  color: #6a1b9a;
  font-weight: bold;
}
a[href$=".zip"]::before { content: "📦 "; }

/* Excel files — dark green */
a[href$=".xlsx"] {
  color: #1b5e20;
  font-weight: bold;
}
a[href$=".xlsx"]::before { content: "📊 "; }

/* PowerPoint files — dark orange */
a[href$=".pptx"] {
  color: #e65100;
  font-weight: bold;
}
a[href$=".pptx"]::before { content: "📑 "; }

/* ================================================
   4. FORM INPUTS — by type
   ================================================ */

/* All text-like inputs — shared base */
input[type="text"],
input[type="email"],
input[type="tel"],
input[type="number"] {
  padding: 10px;
  border-radius: 4px;
  font-size: 1em;
  width: 100%;
}

/* Text inputs — light yellow */
input[type="text"] {
  background-color: #fffde7;
  border: 1px solid #f9a825;
}

/* Email inputs — light blue */
input[type="email"] {
  background-color: #e3f2fd;
  border: 1px solid #1565c0;
}

/* Tel inputs — light purple */
input[type="tel"] {
  background-color: #f3e5f5;
  border: 1px solid #7b1fa2;
}

/* Number inputs — light green */
input[type="number"] {
  background-color: #e8f5e9;
  border: 1px solid #2e7d32;
}

/* All required inputs — red left accent */
input[required] {
  border-left: 4px solid #c62828;
}

/* Checkbox */
input[type="checkbox"] {
  width: 18px;
  height: 18px;
  cursor: pointer;
  vertical-align: middle;
}

/* Reset button */
input[type="reset"] {
  background: #9e9e9e;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

/* Submit button */
input[type="submit"] {
  background: #1a237e;
  color: white;
  padding: 10px 25px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  font-size: 1em;
}

input[type="submit"]:hover {
  background: #0d1757;
}
```

---

### Stage 3 — Milestone Output

When you open this in a browser, you should see:

```
Web Development Resources

[ Search resources...                              ]  ← pill-shaped search bar

[Home] [Lessons] [MDN Docs ↗] [CSS-Tricks ↗] [Contact]
         ↑ grey        ↑ blue bg, arrow icon (external + new tab)

Downloads
  📄 CSS Cheat Sheet            ← dark red (PDF)
  📄 HTML Reference Guide       ← dark red (PDF)
  📦 Starter Project Template   ← purple (ZIP)
  📊 Grade Tracker              ← dark green (XLSX)
  📑 Lesson Slides              ← dark orange (PPTX)
  Extra Notes                   ← normal (HTML link — no special style)

Contact Instructor
  [ Your name     ] ← yellow bg + red left border (text, required)
  [ Your email    ] ← blue bg + red left border (email, required)
  [ Phone...      ] ← purple bg, no red border (tel, optional)
  [ Student ID    ] ← green bg + red left border (number, required)
  [ Your message  ] ← textarea
  [ ] Notify me by email
  [ Clear ]  [ Send Message ]   ← grey / navy buttons
```

---

### Stage 4 — Reflection Questions

1. In the CSS file, we never wrote `class="..."` on any link or input element. How did the CSS know which elements to style?
2. The rule `input[required]` gives a red left border. What exactly does `required` mean in HTML — is it an attribute with a value, or a boolean attribute?
3. The selector `nav a[href^="http"][target="_blank"]::after` is a long chain. Break it down piece by piece — what does each part do?
4. Why did the "Extra Notes" (`.html`) link get no special styling, while the other downloads did?
5. Could you rewrite `input[type="text"]`, `input[type="email"]` etc. using a class selector instead? What would be the trade-offs?

### Optional Enhancements

- Add `a[href*="mdn"]` to give MDN links a special orange glow border
- Add a tooltip-like style using `[title]` — whenever any element has a title attribute, give it a dashed underline as a hint that hovering will show a tooltip
- Add case-insensitive matching using the `i` flag: `a[href$=".PDF" i]` — this matches both `.pdf` and `.PDF` file extensions
- Add `input[type="text"]:focus` and `input[type="email"]:focus` to change the border colour when a field is clicked/focused

---

## Section 8: Common Beginner Mistakes

### Mistake 1: Forgetting the Square Brackets

**The Problem:**
```css
/* WRONG — this is NOT an attribute selector */
input type="text" {
  background: yellow;
}
```

**The Fix:**
```css
/* CORRECT — always wrap in square brackets */
input[type="text"] {
  background: yellow;
}
```

---

### Mistake 2: Using `=` When You Need `~=` (or vice versa)

**The Problem:**
```css
/* WRONG — if title="summer flower", this WON'T match because
   "summer flower" is not exactly equal to "flower" */
p[title="flower"] { color: red; }
```

**The Fix:**
```css
/* CORRECT — use ~= to match "flower" as a whole word within the value */
p[title~="flower"] { color: red; }
```

---

### Mistake 3: Confusing `^=` (starts with) and `|=` (starts with hyphen variant)

Both match values that start with a specific string, but they work differently:

```css
/* |= "top" matches: "top" exactly OR "top-anything" (hyphen required!) */
/* DOES NOT match "topper" */
[class|="top"] { background: yellow; }

/* ^= "top" matches: anything that STARTS with "top" — "top", "topper", "top-text", all match */
[class^="top"] { background: yellow; }
```

> **Rule of thumb:** If you need to match language codes or hyphenated naming conventions, use `|=`. For everything else (just "starts with"), use `^=`.

---

### Mistake 4: Thinking `*=` Requires Whole Words

**The misconception:** Some beginners think `[class*="te"]` only matches if "te" is a whole word.

**The truth:** `*=` matches any substring, including partial words:

```css
/* This matches: "rate", "internet", "technology", "unite", "testing"
   — because ALL of them contain "te" as a substring, even inside other words */
[class*="te"] { background: yellow; }
```

If you want whole words only, use `~=` instead.

---

### Mistake 5: Putting a Space Between the Tag and the Bracket

**The Problem:**
```css
/* WRONG — the space means "a descendant with [target]",
   NOT "an <a> that has [target]" */
a [target] { color: red; }
```

**The Fix:**
```css
/* CORRECT — no space means the <a> itself has the target attribute */
a[target] { color: red; }
```

> **Critical rule:** `a[target]` (no space) = select `<a>` elements that HAVE a `target` attribute. `a [target]` (with space) = select any element with `target` that is a DESCENDANT of an `<a>` element. These are completely different!

---

### Mistake 6: Forgetting That Attribute Selectors Are Case-Sensitive by Default

```css
/* This will NOT match href="HTTPS://google.com" (uppercase HTTPS) */
a[href^="https"] { color: green; }

/* Use the 'i' flag for case-insensitive matching */
a[href^="https" i] { color: green; }
```

The `i` flag makes the value comparison case-insensitive. It is supported in all modern browsers.

---

## Section 9: Reflection Questions

Test your understanding:

1. What is an HTML attribute? Give three examples of attributes used in everyday HTML.
2. What do all attribute selectors have in common in terms of their CSS syntax?
3. What is the difference between `[type]` and `[type="text"]`?
4. Write a selector that targets all `<img>` elements that have an `alt` attribute.
5. Write a selector that targets all `<a>` elements whose `href` starts with `"mailto:"` (for email links).
6. Write a selector that targets all elements whose class attribute contains the word `"disabled"` as a standalone word.
7. What is the difference between `[class~="icon"]` and `[class*="icon"]`? Give an example where one matches but the other does not.
8. You want to style all links that end in `.docx` with a blue border. Write that CSS rule.
9. What does the `i` flag do in an attribute selector like `[href$=".PDF" i]`?
10. Why might a developer prefer attribute selectors over class selectors for styling form inputs?

---

## Section 10: Completion Checklist

Use this to confirm you have mastered this lesson:

- [ ] I understand what HTML attributes are and how they appear in HTML tags
- [ ] I know that all attribute selectors use square brackets `[ ]`
- [ ] I can use `[attr]` to select elements that have a specific attribute
- [ ] I can use `[attr="val"]` to match elements with an exact attribute value
- [ ] I can use `[attr~="val"]` to match a whole word in a space-separated list
- [ ] I can use `[attr|="val"]` to match exact value or value followed by a hyphen
- [ ] I can use `[attr^="val"]` to match attribute values that start with a string
- [ ] I can use `[attr$="val"]` to match attribute values that end with a string
- [ ] I can use `[attr*="val"]` to match attribute values that contain a string anywhere
- [ ] I know how to combine attribute selectors with element type selectors
- [ ] I know how to chain multiple attribute selectors together
- [ ] I can style form inputs by type using `input[type="..."]`
- [ ] I understand the difference between `^=` and `|=`
- [ ] I understand the difference between `~=` and `*=`
- [ ] I know NOT to put a space between a tag name and an attribute selector
- [ ] I know about the `i` flag for case-insensitive matching

---

## Lesson Summary

You have just mastered one of the most powerful precision tools in CSS — attribute selectors. Here is a complete recap:

**CSS attribute selectors** let you target HTML elements based on their attributes (or attribute values), without needing to add any extra class or ID to your HTML. They are enclosed in square brackets `[ ]`.

The **seven attribute selectors** are:

- `[attr]` — Has the attribute (any value is fine)
- `[attr="val"]` — Attribute is exactly `val`
- `[attr~="val"]` — Attribute is a space-separated word list containing `val` as a whole word
- `[attr|="val"]` — Attribute is exactly `val` or starts with `val-` (hyphen variant — great for language codes)
- `[attr^="val"]` — Attribute starts with `val` (great for external links, class prefixes)
- `[attr$="val"]` — Attribute ends with `val` (great for file type detection)
- `[attr*="val"]` — Attribute contains `val` anywhere (great for broad substring matching)

**Combining selectors:** You can combine a tag name with an attribute selector (`a[href$=".pdf"]`) and chain multiple attribute selectors together (`input[type="text"][required]`) for maximum precision.

**Form styling** is one of the most practical uses: `input[type="text"]`, `input[type="email"]`, `input[type="submit"]`, and `input[required]` let you style every kind of form field without adding a single class to your HTML.

**Key distinctions to remember:**
- `~=` requires the value to be a complete standalone word; `*=` does not
- `|=` requires a hyphen after the value for non-exact matches; `^=` does not
- A space between a tag and `[...]` changes the meaning completely — no space means "this element has this attribute"

> **What comes next?** Now that you can target elements by their attributes, you are ready to explore **CSS pseudo-classes** and **CSS pseudo-elements** — which let you select elements based on their state (like `:hover`, `:focus`, `:first-child`) and create virtual elements with `::before` and `::after`. Attribute selectors and pseudo-classes together give you incredible targeting power with zero extra HTML markup!

---

*Lesson 35 Complete — CSS Attribute Selectors*
