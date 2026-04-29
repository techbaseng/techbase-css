---
render_with_liquid: false
title: "Lesson 73: Sass Built-In Functions — String, Numeric, List, Map, Selector, Introspection & Color"
nav_order: 73
---

# Lesson 73: Sass Built-In Functions — The Complete Reference

## Lesson Introduction

Welcome to one of the most powerful lessons in your Sass journey! So far you have learned how to write Sass variables, use nesting, create mixins, and extend styles. But Sass also ships with a large library of **built-in functions** — tools that are ready to use immediately, without you having to write any logic yourself.

Think of Sass functions the way you think of the buttons on a calculator. You do not build a calculator every time you want to add numbers — you just press the `+` button. Sass built-in functions are those buttons. They let you manipulate text, perform maths, work with colours, handle lists, and much more, all from inside your `.scss` files.

This lesson covers all seven categories of Sass built-in functions:

1. **String Functions** — manipulate and inspect text
2. **Numeric Functions** — perform mathematical operations on numbers
3. **List Functions** — work with ordered collections of values
4. **Map Functions** — work with key/value data stores
5. **Selector Functions** — inspect and manipulate CSS selectors
6. **Introspection Functions** — check what types and things exist in your Sass code
7. **Color Functions** — create, read, and transform colours

By the end of this lesson you will be able to use all of these functions confidently, understand why each one exists, and apply them to build real, professional Sass stylesheets.

---

## Learning Objectives

By the end of this lesson, you will be able to:

- Explain what a Sass built-in function is and why it is useful
- Use all Sass string functions to manipulate text values
- Apply numeric functions to perform calculations and rounding
- Work with list functions to read and combine lists
- Use map functions to store and retrieve design tokens
- Understand selector functions and their use in advanced mixins
- Apply introspection functions to debug and inspect Sass code
- Use color functions to create, read, and transform color values programmatically

---

## Prerequisite Concepts

Before continuing, make sure you understand these from earlier lessons:

- **Sass Variables** — storing values in `$variable-name`
- **Sass Mixins** — reusable blocks of CSS written with `@mixin`
- **Sass Nesting** — writing selectors inside other selectors
- **Sass @extend** — sharing styles between selectors

If any of these feel unfamiliar, go back and review the relevant lessons before proceeding.

---

## What Is a Sass Function?

A **function** is a piece of code that takes some input, does something with it, and returns a result.

> **Analogy:** Think of a market trader in Lagos who sells suya. You give the trader a piece of meat (the input), the trader roasts it with spices (the processing), and you get back suya (the output). A function works the same way — you give it values, it processes them, and gives you back a result.

In Sass, a function looks like this:

```scss
// Pattern:
function-name(argument1, argument2)

// Real example:
to-upper-case("hello lagos")
// Returns: "HELLO LAGOS"
```

Sass built-in functions are grouped into seven categories based on what kind of data they work with. Let us explore each category one at a time.

---

## Part 1: Sass String Functions

### What Is a String?

A **string** is a sequence of characters — basically text. In Sass, strings can be quoted (surrounded by `" "`) or unquoted. Examples of strings in CSS/Sass:

- `"Arial"` — a font name
- `"Hello World"` — some text
- `solid` — an unquoted CSS keyword

**Important rule:** Sass strings are **1-based** — meaning the first character in a string is at position **1**, not 0. This is different from some programming languages like JavaScript where counting starts at 0.

### Why String Functions Matter

Imagine you are building a design system for a bank in Abuja. You store font family names as variables:

```scss
$font-family: "Roboto Condensed";
```

Sometimes you need to check how long a font name is, find part of it, or change its case. String functions make this possible.

---

### 1.1 `quote(string)` — Add quotes to a string

**What it does:** Takes an unquoted string and wraps it in quotation marks.

**Why it exists:** Some Sass operations or CSS properties need quoted strings. If your value is unquoted, this function quotes it for you.

```scss
// Input:
quote(Hello Lagos!)

// Output:
"Hello Lagos!"
```

**Example in real Sass:**

```scss
$city: Lagos;
$quoted-city: quote($city);

.header::after {
  content: $quoted-city;  // content: "Lagos"
}
```

> **Expected output in browser:** The `::after` pseudo-element will show the text: Lagos

---

### 1.2 `unquote(string)` — Remove quotes from a string

**What it does:** The opposite of `quote()` — it strips quotation marks from a quoted string.

**Why it exists:** Some CSS properties need unquoted values. If you have a quoted variable but need the bare value, use `unquote()`.

```scss
unquote("Hello Lagos!")
// Returns: Hello Lagos!

unquote("solid")
// Returns: solid
```

**Thinking prompt:** What would happen if you applied `unquote()` to a string that has no quotes? Try it mentally!

---

### 1.3 `str-length(string)` — Count characters in a string

**What it does:** Returns the number of characters (letters, spaces, punctuation) in a string.

```scss
str-length("Hello world!")
// Returns: 12

str-length("Abuja")
// Returns: 5
```

**Real-world use:** You can use this to validate that a CSS class name is not too long, or to dynamically size something based on a text length.

```scss
$brand-name: "NaijaTech";
$name-length: str-length($brand-name);  // 9

.logo {
  width: $name-length * 10px;  // 90px — 10px per character
}
```

**Expected output in browser:** `.logo` element is 90px wide.

---

### 1.4 `str-index(string, substring)` — Find where text appears in a string

**What it does:** Returns the position (index) of the first occurrence of a smaller piece of text (`substring`) inside a larger text (`string`). Returns `null` if not found.

Remember: Sass counts from **1**, not 0.

```scss
str-index("Hello world!", "H")
// Returns: 1      (H is the 1st character)

str-index("Hello world!", "world")
// Returns: 7      (world starts at position 7)

str-index("Hello world!", "Lagos")
// Returns: null   (Lagos is not in the string)
```

**Example:**

```scss
$font-stack: "Roboto, Arial, sans-serif";
$pos: str-index($font-stack, "Arial");

// $pos is 9 (Arial starts at position 9)
```

---

### 1.5 `str-insert(string, insert, index)` — Insert text at a position

**What it does:** Takes a string, inserts a new piece of text at a specified position number, and returns the new combined string.

```scss
str-insert("Hello world!", " wonderful", 6)
// Returns: "Hello wonderful world!"
//           ^^^^^^ inserted at position 6
```

**Breaking it down:**
- `"Hello world!"` — the original string
- `" wonderful"` — the text we want to insert
- `6` — insert it starting at position 6

---

### 1.6 `str-slice(string, start, end)` — Extract part of a string

**What it does:** Pulls out a portion of a string, from the `start` position to the `end` position (inclusive).

```scss
str-slice("Hello world!", 2, 5)
// Returns: "ello"
// Characters at positions 2, 3, 4, 5
```

**Real-world use:** Extract the first few characters of a CSS class name, or get the file extension from a filename stored in a Sass variable.

```scss
$filename: "logo.png";
$extension: str-slice($filename, 6, 8);
// $extension = "png"
```

---

### 1.7 `to-upper-case(string)` — Convert to ALL CAPS

**What it does:** Returns a copy of the string with every letter converted to uppercase.

```scss
to-upper-case("Hello World!")
// Returns: "HELLO WORLD!"

to-upper-case("lagos")
// Returns: "LAGOS"
```

---

### 1.8 `to-lower-case(string)` — Convert to lowercase

**What it does:** Returns a copy of the string with every letter converted to lowercase.

```scss
to-lower-case("Hello World!")
// Returns: "hello world!"

to-lower-case("ABUJA")
// Returns: "abuja"
```

---

### 1.9 `unique-id()` — Generate a unique random string

**What it does:** Returns a randomly generated, unique string each time it is called. This is guaranteed to be unique within the current Sass compilation session. The string is unquoted.

```scss
unique-id()
// Returns something like: tyghefnsv   (random each time)
```

**Real-world use:** Useful for generating unique CSS animation names or keyframe identifiers programmatically.

---

### String Functions Quick Reference

| Function | What it does | Example Result |
|---|---|---|
| `quote(str)` | Adds quotes | `"Hello"` |
| `unquote(str)` | Removes quotes | `Hello` |
| `str-length(str)` | Counts characters | `5` |
| `str-index(str, sub)` | Finds position | `3` |
| `str-insert(str, ins, pos)` | Inserts text | `"He_llo"` |
| `str-slice(str, start, end)` | Extracts part | `"ell"` |
| `to-upper-case(str)` | ALL CAPS | `"HELLO"` |
| `to-lower-case(str)` | all lowercase | `"hello"` |
| `unique-id()` | Random unique string | `xkjr8af` |

---

## Part 2: Sass Numeric Functions

### What Are Numeric Functions?

Numeric functions let you do mathematical operations on numbers in Sass — rounding, finding maximum and minimum values, calculating percentages, and generating random numbers.

**Why this matters:** When you are building a responsive layout or a spacing scale, you often need to calculate sizes programmatically rather than writing every value by hand.

---

### 2.1 `abs(number)` — Absolute value

**What it does:** Returns the **positive** version of any number. A negative becomes positive; a positive stays positive.

> **Analogy:** Think of it as distance. Whether you walk 5 steps forward or 5 steps back, the distance is still 5 steps. `abs()` gives you that distance.

```scss
abs(15)    // Returns: 15
abs(-15)   // Returns: 15
abs(-8px)  // Returns: 8px
```

**Real use:** When calculating offsets or shadows where you might accidentally have negative values, `abs()` ensures you always get a positive number.

---

### 2.2 `ceil(number)` — Round UP to nearest whole number

**What it does:** Always rounds a decimal number **up** to the next whole number, even if the decimal part is small.

> **Analogy:** Imagine you are ordering akara from a Lagos hawker. If you need 15.2 servings, you cannot order a fraction — you order 16. `ceil()` works exactly like this.

```scss
ceil(15.20)   // Returns: 16
ceil(15.80)   // Returns: 16  (always goes UP)
ceil(4.01)    // Returns: 5
ceil(-4.5)    // Returns: -4  (goes UP toward zero)
```

---

### 2.3 `floor(number)` — Round DOWN to nearest whole number

**What it does:** Always rounds a decimal number **down** to the previous whole number.

```scss
floor(15.80)   // Returns: 15
floor(15.20)   // Returns: 15  (always goes DOWN)
floor(4.99)    // Returns: 4
```

> **Thinking prompt:** `ceil(15.80)` returns 16 and `floor(15.80)` returns 15. Why? Because `ceil` always goes up and `floor` always goes down, no matter how close to the next whole number you are.

---

### 2.4 `round(number)` — Round to nearest whole number

**What it does:** Rounds normally — below 0.5 rounds down, at 0.5 or above rounds up.

```scss
round(15.20)   // Returns: 15  (0.20 is below 0.5, rounds down)
round(15.80)   // Returns: 16  (0.80 is above 0.5, rounds up)
round(15.50)   // Returns: 16  (0.50 rounds up)
```

---

### 2.5 `max(number...)` — Find the largest value

**What it does:** Accepts multiple numbers and returns the largest one.

```scss
max(5, 7, 9, 0, -3, -7)
// Returns: 9
```

**Real use:**

```scss
$spacing-sm: 8px;
$spacing-md: 16px;
$spacing-lg: 24px;

.container {
  padding: max($spacing-sm, $spacing-md);  // 16px
}
```

---

### 2.6 `min(number...)` — Find the smallest value

**What it does:** Accepts multiple numbers and returns the smallest one.

```scss
min(5, 7, 9, 0, -3, -7)
// Returns: -7
```

---

### 2.7 `percentage(number)` — Convert to a percentage

**What it does:** Multiplies a number by 100 to convert it into a percentage. Useful when converting decimal values (like ratios) to CSS percentages.

```scss
percentage(1.2)    // Returns: 120%
percentage(0.5)    // Returns: 50%
percentage(0.333)  // Returns: 33.3%
```

**Real use:** Converting grid column fractions to percentages:

```scss
$columns: 12;
$my-col: 4;

.col-4 {
  width: percentage($my-col / $columns);
  // width: percentage(0.333...) → width: 33.333...%
}
```

---

### 2.8 `comparable(num1, num2)` — Check if two numbers can be compared

**What it does:** Returns `true` if two numbers use compatible units that can be compared or combined mathematically, and `false` if they cannot.

```scss
comparable(15px, 10px)   // Returns: true  (both px)
comparable(20mm, 1cm)    // Returns: true  (both length units)
comparable(35px, 2em)    // Returns: false (px and em cannot be compared)
```

**Why it matters:** In responsive design, mixing `px` with `em` in the same math expression causes errors. `comparable()` lets you check first.

---

### 2.9 `random()` and `random(number)` — Generate random numbers

**`random()`** — Returns a random decimal between 0 and 1.

```scss
random()   // Returns something like: 0.45673
```

**`random(number)`** — Returns a random integer between 1 and the number you provide.

```scss
random(6)   // Returns a random number from 1 to 6 (like rolling a die)
random(100) // Returns a random number from 1 to 100
```

**Real use:** Generating slightly varied animation delays or positions for a decorative particle system in CSS.

---

### Numeric Functions Quick Reference

| Function | What it does | Example |
|---|---|---|
| `abs(n)` | Absolute value | `abs(-5)` → `5` |
| `ceil(n)` | Round up | `ceil(4.1)` → `5` |
| `floor(n)` | Round down | `floor(4.9)` → `4` |
| `round(n)` | Round normally | `round(4.5)` → `5` |
| `max(...)` | Largest value | `max(3,7,2)` → `7` |
| `min(...)` | Smallest value | `min(3,7,2)` → `2` |
| `percentage(n)` | Multiply by 100 | `percentage(0.5)` → `50%` |
| `comparable(a, b)` | Check unit compatibility | `comparable(1px, 1em)` → `false` |
| `random()` | Random 0–1 decimal | `0.73241` |
| `random(n)` | Random 1–n integer | `random(6)` → `4` |

---

## Part 3: Sass List Functions

### What Is a Sass List?

In Sass, a **list** is a collection of values separated by spaces or commas. You already use lists every day in CSS without knowing it:

```css
font-family: Arial, Helvetica, sans-serif;   /* comma-separated list */
margin: 10px 20px 10px 20px;                  /* space-separated list */
```

In Sass, you can store these lists in variables:

```scss
$font-stack: Arial, Helvetica, sans-serif;
$margins: 10px 20px 10px 20px;
```

**Important rules about Sass lists:**

1. **Lists are immutable** — you cannot change a list once it exists. List functions that "modify" a list actually return a *brand new list* and leave the original unchanged.
2. **Lists are 1-based** — the first item is at index 1, not 0.

---

### 3.1 `length(list)` — Count items in a list

**What it does:** Returns the number of items in the list.

```scss
length(a b c)       // Returns: 3
length(1px 2px 3px) // Returns: 3
length(a, b, c, d)  // Returns: 4
```

**Real use:**

```scss
$breakpoints: 320px, 768px, 1024px, 1440px;

// How many breakpoints do we have?
$count: length($breakpoints);  // 4
```

---

### 3.2 `nth(list, n)` — Get the item at position n

**What it does:** Returns the item at position `n` in the list.

```scss
nth(a b c, 3)   // Returns: c   (3rd item)
nth(a b c, 1)   // Returns: a   (1st item)
```

**Real use:**

```scss
$colors: red, green, blue, yellow;
$second-color: nth($colors, 2);  // green
```

---

### 3.3 `index(list, value)` — Find where a value is in a list

**What it does:** Returns the position number of `value` inside `list`. Returns `null` if the value is not found.

```scss
index(a b c, b)    // Returns: 2   (b is at position 2)
index(a b c, f)    // Returns: null (f is not in the list)
```

---

### 3.4 `list-separator(list)` — Check how a list is separated

**What it does:** Returns `"space"` if the list items are space-separated, or `"comma"` if they are comma-separated.

```scss
list-separator(a b c)    // Returns: "space"
list-separator(a, b, c)  // Returns: "comma"
```

---

### 3.5 `is-bracketed(list)` — Check if a list has square brackets

**What it does:** Returns `true` if the list is wrapped in square brackets `[ ]`, and `false` otherwise.

```scss
is-bracketed([a b c])   // Returns: true
is-bracketed(a b c)     // Returns: false
```

**Why square brackets?** In CSS Grid, the bracket syntax has a special meaning for naming grid lines. Sass supports this notation.

---

### 3.6 `append(list, value, separator)` — Add one item to the end

**What it does:** Adds a single value to the end of a list and returns the new list. The original list is NOT changed.

The optional `separator` parameter controls how items are joined: `auto` (default — uses the existing list's separator), `comma`, or `space`.

```scss
append((a b c), d)            // Returns: a b c d
append((a b c), (d), comma)   // Returns: a, b, c, d
append((a, b, c), d)          // Returns: a, b, c, d  (keeps comma)
```

**Real use:**

```scss
$base-classes: btn btn-primary;
$full-classes: append($base-classes, btn-lg);
// $full-classes = btn btn-primary btn-lg
```

---

### 3.7 `join(list1, list2, separator, bracketed)` — Combine two lists

**What it does:** Joins two lists together end-to-end and returns one combined list.

Parameters:
- `separator` — `auto` (default, uses first list's separator), `comma`, or `space`
- `bracketed` — `auto` (default), `true`, or `false`

```scss
join(a b c, d e f)                       // Returns: a b c d e f
join((a b c), (d e f), comma)            // Returns: a, b, c, d, e, f
join(a b c, d e f, $bracketed: true)     // Returns: [a b c d e f]
```

---

### 3.8 `set-nth(list, n, value)` — Replace item at position n

**What it does:** Returns a new list where the item at position `n` has been replaced with `value`.

```scss
set-nth(a b c, 2, x)   // Returns: a x c
set-nth(a b c, 1, z)   // Returns: z b c
```

---

### 3.9 `zip(lists...)` — Combine lists into a multidimensional list

**What it does:** Takes several lists and merges them together "column by column", creating a single list where each item groups one value from each of the source lists.

```scss
zip(1px 2px 3px, solid dashed dotted, red green blue)
// Returns: 1px solid red, 2px dashed green, 3px dotted blue
```

> **Analogy:** Imagine three rows of market stalls — one selling fabrics, one selling thread, one selling needles. `zip()` pairs them up: fabric + thread + needle = one sewing kit, repeated three times.

**Real use — creating shorthand `border` values:**

```scss
$widths: 1px 2px 3px;
$styles: solid dashed dotted;
$colors: red green blue;

$borders: zip($widths, $styles, $colors);
// $borders = 1px solid red, 2px dashed green, 3px dotted blue
```

---

## Part 4: Sass Map Functions

### What Is a Sass Map?

A **map** is a collection of **key/value pairs** — like a small database or a dictionary. Each key has one corresponding value.

```scss
// Syntax:
$map-name: (key1: value1, key2: value2, key3: value3);

// Real example — a typography scale:
$font-sizes: ("small": 12px, "normal": 18px, "large": 24px);
```

> **Analogy:** Think of a Suya spice chart at a Lagos market. Each spice name (the key) has a price per gram (the value). `$prices: ("ginger": 50, "pepper": 30, "garlic": 40);`

**Important rules about maps:**

1. Maps are **immutable** — map functions return new maps, not modified originals.
2. Keys and values can be any Sass data type.

---

### 4.1 `map-get(map, key)` — Get a value by its key

**What it does:** Looks up a key in the map and returns its value.

```scss
$font-sizes: ("small": 12px, "normal": 18px, "large": 24px);

map-get($font-sizes, "small")    // Returns: 12px
map-get($font-sizes, "normal")   // Returns: 18px
map-get($font-sizes, "large")    // Returns: 24px
```

**Real use:**

```scss
$brand-colors: ("primary": #006400, "secondary": #FFD700, "danger": #CC0000);

.btn-primary {
  background-color: map-get($brand-colors, "primary");  // #006400
}
```

**Expected output in browser:** `.btn-primary` has a dark green background.

---

### 4.2 `map-has-key(map, key)` — Check if a key exists

**What it does:** Returns `true` if the map contains the given key, and `false` if it does not.

```scss
$font-sizes: ("small": 12px, "normal": 18px, "large": 24px);

map-has-key($font-sizes, "normal")    // Returns: true
map-has-key($font-sizes, "big")       // Returns: false
```

**Real use:** Before trying to get a value, check if the key exists to prevent errors:

```scss
@if map-has-key($brand-colors, "accent") {
  .accent {
    color: map-get($brand-colors, "accent");
  }
}
```

---

### 4.3 `map-keys(map)` — Get all keys as a list

**What it does:** Returns a comma-separated list of all the keys in the map.

```scss
$font-sizes: ("small": 12px, "normal": 18px, "large": 24px);

map-keys($font-sizes)
// Returns: "small", "normal", "large"
```

---

### 4.4 `map-values(map)` — Get all values as a list

**What it does:** Returns a comma-separated list of all the values in the map.

```scss
$font-sizes: ("small": 12px, "normal": 18px, "large": 24px);

map-values($font-sizes)
// Returns: 12px, 18px, 24px
```

---

### 4.5 `map-merge(map1, map2)` — Combine two maps

**What it does:** Appends all key/value pairs from `map2` to the end of `map1` and returns the combined map. If a key exists in both maps, the value from `map2` wins.

```scss
$font-sizes:  ("small": 12px, "normal": 18px, "large": 24px);
$font-sizes2: ("x-large": 30px, "xx-large": 36px);

map-merge($font-sizes, $font-sizes2)
// Returns:
// "small": 12px, "normal": 18px, "large": 24px, "x-large": 30px, "xx-large": 36px
```

---

### 4.6 `map-remove(map, keys...)` — Remove keys from a map

**What it does:** Returns a new map with the specified key(s) removed.

```scss
$font-sizes: ("small": 12px, "normal": 18px, "large": 24px);

map-remove($font-sizes, "small")
// Returns: ("normal": 18px, "large": 24px)

map-remove($font-sizes, "small", "large")
// Returns: ("normal": 18px)
```

---

### Practical Map Example — Design Tokens

Maps are perfect for storing design system tokens (like colours, spacing values, and font sizes in one place):

```scss
// _tokens.scss

$colors: (
  "green-dark":    #006400,
  "green-light":   #90EE90,
  "gold":          #FFD700,
  "white":         #FFFFFF,
  "black":         #000000
);

$spacing: (
  "xs": 4px,
  "sm": 8px,
  "md": 16px,
  "lg": 32px,
  "xl": 64px
);

// Usage:
.hero {
  background-color: map-get($colors, "green-dark");
  padding: map-get($spacing, "lg");
}
```

**Expected output in browser:** `.hero` has dark green background and 32px padding.

---

## Part 5: Sass Selector Functions

### What Are Selector Functions?

Selector functions let you inspect, build, and manipulate **CSS selectors** programmatically inside Sass. They are most useful when writing advanced mixins that need to work with or understand the selectors they are applied to.

---

### 5.1 `is-superselector(super, sub)` — Does one selector cover another?

**What it does:** Returns `true` if the `super` selector would match **at least all the elements** that the `sub` selector matches. In other words, is `super` broader than or equal to `sub`?

```scss
is-superselector("div", "div.myInput")   // Returns: true
// Because "div" matches all divs, including div.myInput

is-superselector("div.myInput", "div")   // Returns: false
// Because "div.myInput" only matches divs with class myInput — not ALL divs

is-superselector("div", "div")           // Returns: true
// Same selector — identical match
```

---

### 5.2 `selector-append(selectors...)` — Join selectors without a space

**What it does:** Combines selectors by joining them directly together (no space or combinator between them), returning a new compound selector.

```scss
selector-append("div", ".myInput")
// Returns: div.myInput
// (An element that is both a div AND has class myInput)

selector-append(".warning", "__a")
// Returns: .warning__a
// (Useful for BEM modifier patterns)
```

---

### 5.3 `selector-nest(selectors...)` — Build nested selectors

**What it does:** Creates a new selector list representing nested CSS selectors, as if you had written them inside a Sass nesting block.

```scss
selector-nest("ul", "li")
// Returns: ul li   (li elements inside a ul)

selector-nest(".warning", "alert", "div")
// Returns: .warning div, alert div
// (div inside .warning, OR div inside alert)
```

---

### 5.4 `selector-parse(selector)` — Break a selector into parts

**What it does:** Parses a selector string and returns a structured list showing the individual pieces of that selector.

```scss
selector-parse("h1 .myInput .warning")
// Returns: ('h1' '.myInput' '.warning')
```

---

### 5.5 `selector-replace(selector, original, replacement)` — Swap part of a selector

**What it does:** Returns a new selector where occurrences of `original` are replaced with `replacement`.

```scss
selector-replace("p.warning", "p", "div")
// Returns: div.warning
// (Changed the element from p to div)
```

---

### 5.6 `selector-unify(selector1, selector2)` — Find the overlap of two selectors

**What it does:** Returns a new selector that matches **only elements matched by BOTH** selectors. Returns `null` if no overlap is possible.

```scss
selector-unify("myInput", ".disabled")
// Returns: myInput.disabled
// (Must be both a myInput AND have class disabled)

selector-unify("p", "h1")
// Returns: null
// (An element cannot be both a p and an h1 simultaneously)
```

---

### 5.7 `simple-selectors(selectors)` — List the individual parts of a compound selector

**What it does:** Returns a comma-separated list of the individual simple selectors that make up a compound selector.

```scss
simple-selectors("div.myInput")
// Returns: div, .myInput

simple-selectors("div.myInput:before")
// Returns: div, .myInput, :before
```

---

## Part 6: Sass Introspection Functions

### What Are Introspection Functions?

**Introspection** means "looking inward" — examining something to understand its own nature. Sass introspection functions let you ask questions about your Sass code itself:

- What type is this value?
- Does this variable exist?
- Does this mixin exist?
- What unit does this number use?

> **Analogy:** Imagine you are a Lagos building inspector. Before approving a building plan, you check: Is this material steel or wood? Does this structure have a foundation? Introspection functions are the inspector tools for your Sass code.

These functions are rarely needed for everyday styling, but they are extremely valuable for debugging and for writing reusable mixins and functions that need to be "smart" about the data they receive.

---

### 6.1 `type-of(value)` — What type is this value?

**What it does:** Returns a string describing the data type of the given value. Possible return values are: `number`, `string`, `color`, `list`, `map`, `bool`, `null`, `function`, `arglist`.

```scss
type-of(15px)      // Returns: number
type-of(#ff0000)   // Returns: color
type-of("hello")   // Returns: string
type-of(true)      // Returns: bool
type-of(null)      // Returns: null
type-of(a b c)     // Returns: list
```

**Real use — safe mixins:**

```scss
@mixin set-font-size($size) {
  @if type-of($size) == number {
    font-size: $size;
  } @else {
    @warn "set-font-size expects a number, got: #{type-of($size)}";
  }
}
```

---

### 6.2 `unit(number)` — What unit does this number use?

**What it does:** Returns the unit associated with a number as a string.

```scss
unit(15px)    // Returns: "px"
unit(2em)     // Returns: "em"
unit(100%)    // Returns: "%"
unit(15)      // Returns: ""  (no unit)
```

---

### 6.3 `unitless(number)` — Does this number have no unit?

**What it does:** Returns `true` if the number has no unit, and `false` if it has a unit.

```scss
unitless(15px)   // Returns: false   (has unit px)
unitless(15)     // Returns: true    (no unit)
```

---

### 6.4 `variable-exists(variablename)` — Does this local variable exist?

**What it does:** Checks whether a variable with the given name exists in the **current scope** (local or global). Returns `true` or `false`.

```scss
$primary-color: #006400;

variable-exists(primary-color)   // Returns: true
variable-exists(secondary-color) // Returns: false (not declared)
```

---

### 6.5 `global-variable-exists(variablename)` — Does this global variable exist?

**What it does:** Checks whether a variable with the given name exists as a **global** (top-level) variable. Returns `true` or `false`.

```scss
$theme: "light";

global-variable-exists(theme)   // Returns: true
global-variable-exists(width)   // Returns: false
```

---

### 6.6 `function-exists(functionname)` — Does this function exist?

**What it does:** Returns `true` if the named function is available (either a Sass built-in or a user-defined function), and `false` if it does not exist.

```scss
function-exists("round")       // Returns: true   (built-in function)
function-exists("nonsense")    // Returns: false  (does not exist)
```

---

### 6.7 `mixin-exists(mixinname)` — Does this mixin exist?

**What it does:** Returns `true` if the named mixin has been defined, and `false` otherwise.

```scss
@mixin important-text {
  color: red;
  font-weight: bold;
}

mixin-exists("important-text")   // Returns: true
mixin-exists("fancy-border")     // Returns: false
```

---

### 6.8 `feature-exists(feature)` — Is this Sass feature supported?

**What it does:** Checks whether the current Sass implementation supports a named feature. Useful when writing cross-compatible stylesheets.

```scss
feature-exists("at-error")    // Returns: true
```

---

### 6.9 `inspect(value)` — Get a string representation of any value

**What it does:** Returns a string that represents the given value in a human-readable form. Works on any data type, including maps and lists that might not normally be printable.

```scss
inspect(1px 2px 3px)   // Returns: "1px 2px 3px"
inspect(null)          // Returns: "null"
```

---

### 6.10 `content-exists()` — Was `@content` passed to this mixin?

**What it does:** Inside a mixin, returns `true` if the mixin was called with a `@content` block, and `false` otherwise. Only works inside a `@mixin` body.

```scss
@mixin wrap-content {
  @if content-exists() {
    .wrapper {
      @content;
    }
  }
}
```

---

### 6.11 `call(function, arguments...)` — Call a function by name

**What it does:** Calls a Sass function (obtained with `get-function()`) and passes arguments to it. Used for dynamic function calls.

---

## Part 7: Sass Color Functions

### Why Color Functions?

Colors are at the heart of web design. Sass color functions let you:

- Create colors using different color models (RGB, HSL)
- Read individual color components (how red is this? how bright?)
- Automatically generate lighter, darker, more saturated, or more transparent versions of any color

Instead of manually picking 10 shades of green for your design system, Sass can generate them for you programmatically.

The color functions are divided into three groups: **Set** (create), **Get** (read), and **Manipulate** (change).

---

## 7A: Set Color Functions — Create Colors

### `rgb(red, green, blue)` — Create a color from RGB values

**What it does:** Creates a color by specifying how much Red, Green, and Blue light to mix. Each value is a number from 0 to 255 (or a percentage from 0% to 100%).

```scss
rgb(0, 0, 255)      // Returns: pure blue   (max blue, no red/green)
rgb(255, 0, 0)      // Returns: pure red
rgb(0, 255, 0)      // Returns: pure green
rgb(128, 128, 128)  // Returns: medium gray
```

**Real use:**

```scss
$naija-green: rgb(0, 100, 0);   // Nigeria flag green
.flag { background-color: $naija-green; }
```

---

### `rgba(red, green, blue, alpha)` — RGB color with transparency

**What it does:** Same as `rgb()` but with an extra `alpha` parameter for opacity. Alpha ranges from `0.0` (fully transparent) to `1.0` (fully opaque).

```scss
rgba(0, 0, 255, 0.3)    // Blue at 30% opacity
rgba(0, 0, 255, 1)      // Blue at 100% opacity (fully visible)
rgba(0, 0, 0, 0.5)      // Semi-transparent black overlay
```

**Real use:**

```scss
.modal-overlay {
  background-color: rgba(0, 0, 0, 0.6);  // Dark 60% transparent overlay
}
```

---

### `hsl(hue, saturation, lightness)` — Create a color using HSL

**What it does:** Creates a color using the HSL (Hue, Saturation, Lightness) color model, which is often more intuitive than RGB.

- **Hue** — the actual color, as a degree on the color wheel (0–360). 0/360 = red, 120 = green, 240 = blue.
- **Saturation** — how vivid the color is. 0% = gray, 100% = full color.
- **Lightness** — how light or dark. 0% = black, 100% = white, 50% = normal.

```scss
hsl(120, 100%, 50%)   // Returns: vivid green
hsl(120, 100%, 75%)   // Returns: light green
hsl(120, 100%, 25%)   // Returns: dark green
hsl(120, 60%, 70%)    // Returns: pastel green
hsl(0, 100%, 50%)     // Returns: red
hsl(240, 100%, 50%)   // Returns: blue
```

> **Why HSL is great for theming:** It is much easier to think "I want a dark version of green" (`hsl(120, 100%, 20%)`) than to figure out the RGB numbers for it.

---

### `hsla(hue, saturation, lightness, alpha)` — HSL with transparency

**What it does:** Same as `hsl()` but with an alpha channel for transparency.

```scss
hsla(120, 100%, 50%, 0.3)    // Green at 30% opacity
hsla(120, 100%, 75%, 0.5)    // Light green at 50% opacity
```

---

### `grayscale(color)` — Convert a color to its gray equivalent

**What it does:** Returns a gray color that has the same lightness value as the input color (essentially desaturating it to 0% saturation).

```scss
grayscale(#7fffd4)   // Returns: #c6c6c6
grayscale(red)       // Returns: #808080
```

---

### `complement(color)` — Get the opposite color on the color wheel

**What it does:** Returns the complementary color — the color exactly 180 degrees opposite on the color wheel.

```scss
complement(#7fffd4)   // Returns: #ff7faa
complement(red)       // Returns: cyan
```

**Real use:** Complementary colors are often used for high-contrast button or link colors.

---

### `invert(color, weight)` — Get the negative of a color

**What it does:** Returns the inverted (negative) version of a color. White becomes black, green becomes magenta, etc. The optional `weight` (0%–100%) controls how strong the inversion is.

```scss
invert(white)           // Returns: black
invert(black)           // Returns: white
invert(#7fffd4)         // Returns: #800029
invert(white, 50%)      // Returns: gray (halfway between white and black)
```

---

## 7B: Get Color Functions — Read Color Components

These functions let you extract individual parts of an existing color.

### `red(color)` — Extract the red channel

```scss
red(#7fffd4)   // Returns: 127   (hex 7F = decimal 127)
red(red)       // Returns: 255
red(blue)      // Returns: 0
```

### `green(color)` — Extract the green channel

```scss
green(#7fffd4)   // Returns: 255   (hex FF = 255)
green(blue)      // Returns: 0
```

### `blue(color)` — Extract the blue channel

```scss
blue(#7fffd4)   // Returns: 212   (hex D4 = 212)
blue(blue)      // Returns: 255
```

### `hue(color)` — Extract the hue in degrees

```scss
hue(#7fffd4)   // Returns: 160deg
```

### `saturation(color)` — Extract the HSL saturation percentage

```scss
saturation(#7fffd4)   // Returns: 100%
```

### `lightness(color)` — Extract the HSL lightness percentage

```scss
lightness(#7fffd4)   // Returns: 74.9%
```

### `alpha(color)` — Get the opacity (alpha value)

```scss
alpha(#7fffd4)                    // Returns: 1   (fully opaque)
alpha(rgba(127, 255, 212, 0.5))   // Returns: 0.5
```

### `opacity(color)` — Same as alpha()

`opacity()` works identically to `alpha()`.

```scss
opacity(rgba(127, 255, 212, 0.5))  // Returns: 0.5
```

---

## 7C: Manipulate Color Functions — Transform Colors

These are the most powerful color functions — they let you programmatically create variations of any color.

### `lighten(color, amount)` — Make a color lighter

**What it does:** Increases the HSL lightness of a color by a given percentage amount.

```scss
lighten(#006400, 20%)   // Makes dark green lighter by 20%
lighten(#3498db, 10%)   // Makes blue 10% lighter
```

**Real use — generating hover states automatically:**

```scss
$btn-color: #006400;  // Dark green

.btn {
  background-color: $btn-color;
}

.btn:hover {
  background-color: lighten($btn-color, 10%);  // Lighter green on hover
}
```

---

### `darken(color, amount)` — Make a color darker

**What it does:** Decreases the HSL lightness of a color by the given amount.

```scss
darken(#7fffd4, 20%)    // Makes aquamarine darker by 20%
darken(#3498db, 15%)    // Makes blue 15% darker
```

---

### `saturate(color, amount)` — Make a color more vivid

**What it does:** Increases the HSL saturation of a color, making it more vibrant.

```scss
saturate(#7fffd4, 20%)   // More vivid aquamarine
```

---

### `desaturate(color, amount)` — Make a color less vivid (toward gray)

**What it does:** Decreases the HSL saturation, making the color appear more washed out or muted.

```scss
desaturate(#7fffd4, 30%)   // More muted, grayish aquamarine
```

---

### `mix(color1, color2, weight)` — Blend two colors together

**What it does:** Creates a new color that is a blend of `color1` and `color2`. The `weight` (0%–100%) controls how much of `color1` to use. A weight of 50% (the default) produces an even blend.

```scss
mix(red, blue, 50%)    // Returns: purple (equal blend)
mix(red, blue, 75%)    // Returns: mostly red, slightly blue
mix(#006400, white, 50%)  // Nigeria green blended with white
```

**Real use — generating a tint palette:**

```scss
$brand-green: #006400;

$tints: (
  "100": mix($brand-green, white, 10%),
  "200": mix($brand-green, white, 20%),
  "300": mix($brand-green, white, 30%),
  "400": mix($brand-green, white, 40%),
  "500": $brand-green,
);
```

---

### `adjust-hue(color, degrees)` — Rotate the color on the wheel

**What it does:** Shifts the hue of a color by a given number of degrees (positive or negative) around the HSL color wheel.

```scss
adjust-hue(#7fffd4, 80deg)    // Returns: #8080ff (shifted 80 degrees)
adjust-hue(#7fffd4, -90deg)   // Shifted 90 degrees backward
```

---

### `adjust-color(color, properties...)` — Fine-tune individual color channels

**What it does:** Adjusts one or more color parameters by **adding or subtracting** the specified amount from the existing channel value.

```scss
adjust-color(#7fffd4, blue: 25)    // Adds 25 to the blue channel
adjust-color(#7fffd4, red: -50)    // Subtracts 50 from the red channel
adjust-color(#7fffd4, lightness: 10%, saturation: -20%)
```

---

### `change-color(color, properties...)` — Replace individual channel values

**What it does:** Similar to `adjust-color()`, but instead of adding/subtracting, it **replaces** the channel value entirely with the new value you provide.

```scss
change-color(#7fffd4, red: 255)
// Returns: #ffffd4   (red channel replaced with 255, other channels unchanged)

change-color(#7fffd4, hue: 240deg)
// Changes hue to 240 (blue) keeping saturation and lightness the same
```

---

### `scale-color(color, properties...)` — Scale channels proportionally

**What it does:** Scales color channels by a percentage relative to their current value (rather than adding a fixed amount like `adjust-color()`).

```scss
scale-color(#7fffd4, lightness: 50%)   // Increase lightness by 50% of the remaining distance to 100%
scale-color(#7fffd4, alpha: -30%)      // Reduce alpha by 30% of its current value
```

---

### `opacify(color, amount)` / `fade-in(color, amount)` — Make more opaque

**What it does:** Increases the alpha channel of a color, making it less transparent. `opacify()` and `fade-in()` do the same thing.

```scss
opacify(rgba(0, 0, 0, 0.5), 0.3)    // Returns: rgba(0, 0, 0, 0.8)
fade-in(rgba(0, 0, 0, 0.2), 0.5)    // Returns: rgba(0, 0, 0, 0.7)
```

---

### `transparentize(color, amount)` / `fade-out(color, amount)` — Make more transparent

**What it does:** Decreases the alpha channel, making the color more transparent. `transparentize()` and `fade-out()` do the same thing.

```scss
transparentize(rgba(0, 0, 0, 0.8), 0.3)   // Returns: rgba(0, 0, 0, 0.5)
fade-out(black, 0.5)                        // Returns: rgba(0, 0, 0, 0.5)
```

---

### `rgba(color, alpha)` — Change just the alpha of an existing color

**What it does:** A shortcut to create a new color from an existing color value with a new alpha (opacity) level.

```scss
rgba(#7fffd4, 30%)    // Returns: rgba(127, 255, 212, 0.3)
rgba(green, 0.5)      // Returns: rgba(0, 128, 0, 0.5)
```

---

## Guided Practice Exercises

### Exercise 1 — String Functions (Beginner)

**Scenario:** You are building a design system for NaijaShop, an e-commerce platform in Lagos. You have a product name stored as a variable and need to manipulate it in several ways.

**Setup:**

```scss
$product-name: "Ankara Fabric";
```

**Tasks:**

1. Find how many characters are in `$product-name` using `str-length()`.
2. Convert `$product-name` to all capitals using `to-upper-case()`.
3. Find the position of the word "Fabric" using `str-index()`.
4. Extract just the word "Ankara" using `str-slice()` (positions 1 to 6).
5. Insert the word " Premium" after "Ankara" using `str-insert()`.

**Solutions:**

```scss
$product-name: "Ankara Fabric";

$length:    str-length($product-name);        // 13
$upper:     to-upper-case($product-name);     // "ANKARA FABRIC"
$pos:       str-index($product-name, "Fabric"); // 8
$first-word: str-slice($product-name, 1, 6);  // "Ankara"
$new-name:  str-insert($product-name, " Premium", 7);
// Returns: "Ankara Premium Fabric"
```

**Self-check:** Can you explain why position 7 inserts a word between "Ankara" and "Fabric"?

---

### Exercise 2 — Numeric Functions (Beginner–Intermediate)

**Scenario:** You are designing a grid system for a Lagos newspaper website. The page is 1200px wide with a 24px gutter between 12 columns.

**Tasks:**

1. Calculate one column width: `(1200 - 11 * 24) / 12`. Then `ceil()` the result.
2. What is the maximum of: 16px, 24px, 12px?
3. What is the minimum of: 16px, 24px, 12px?
4. Convert `4/12` (a 4-column span ratio) to a percentage using `percentage()`.

**Solutions:**

```scss
$page-width: 1200px;
$gutter:     24px;
$col-count:  12;
$gutters:    ($col-count - 1) * $gutter;          // 264px
$col-raw:    ($page-width - $gutters) / $col-count; // 78px

$col-width: ceil($col-raw);  // 78px (already whole, stays 78)

$max-val: max(16px, 24px, 12px);  // 24px
$min-val: min(16px, 24px, 12px);  // 12px

$four-col-pct: percentage(4 / 12);  // 33.3333%
```

---

### Exercise 3 — Map Functions (Intermediate)

**Scenario:** You are building a theming system for AbujaTech's website. All design tokens are stored in maps.

**Setup:**

```scss
$palette: (
  "brand-primary":   #1A6B3C,
  "brand-secondary": #FFD700,
  "neutral-100":     #F5F5F5,
  "neutral-900":     #111111
);
```

**Tasks:**

1. Get the value for `"brand-primary"`.
2. Check if `"brand-tertiary"` exists in the map.
3. Get a list of all keys.
4. Merge `$palette` with a new map `$alerts` that contains `("success": #28a745, "danger": #dc3545)`.
5. Remove `"neutral-100"` from `$palette`.

**Solutions:**

```scss
$primary:         map-get($palette, "brand-primary");    // #1A6B3C
$tertiary-exists: map-has-key($palette, "brand-tertiary"); // false
$all-keys:        map-keys($palette);
// "brand-primary", "brand-secondary", "neutral-100", "neutral-900"

$alerts: ("success": #28a745, "danger": #dc3545);
$full-palette: map-merge($palette, $alerts);

$slim-palette: map-remove($palette, "neutral-100");
```

---

## Mini Project: NaijaPalette — A Dynamic Color System

In this project you will build a complete color theming system for a fictional Nigerian startup called **GreenGold Digital**, using Sass color functions to generate an entire palette from just two seed colors.

### Project Brief

GreenGold Digital uses two brand colors: deep green (#006400) and gold (#FFD700). Your task is to generate a full design system palette from those two colors using Sass functions.

---

### Stage 1 — Seed Colors and Primary Map

```scss
// _palette.scss

// Seed colors
$green: #006400;
$gold:  #FFD700;

// Generate 5 green tints
$green-palette: (
  "green-100": mix($green, white, 10%),
  "green-200": mix($green, white, 20%),
  "green-300": mix($green, white, 40%),
  "green-400": mix($green, white, 60%),
  "green-500": $green,
  "green-600": darken($green, 10%),
  "green-700": darken($green, 20%),
);
```

**Milestone 1 output:** 7 green shades from near-white to very dark green, all generated from a single seed.

---

### Stage 2 — Utility Colors

```scss
// Generate complementary and status colors
$complement-green: complement($green);   // A pinkish-red

$status-colors: (
  "success":  $green,
  "warning":  $gold,
  "danger":   adjust-hue($gold, 30deg), // warm orange-red
  "info":     mix($green, #0000ff, 50%) // blue-green
);
```

**Milestone 2 output:** A status color set that harmonizes with the brand.

---

### Stage 3 — Typography Colors

```scss
// Text colors derived from brand colors
$text-colors: (
  "on-light":    darken($green, 20%),          // Very dark green for body text
  "on-dark":     lighten($gold, 30%),           // Light gold for text on dark
  "muted":       desaturate(lighten($green, 40%), 50%),  // Muted gray-green
  "link":        $green,
  "link-hover":  lighten($green, 15%),
);
```

---

### Stage 4 — Composing the Final Stylesheet

```scss
// styles.scss

.btn-primary {
  background-color: map-get($green-palette, "green-500");
  color: map-get($text-colors, "on-dark");

  &:hover {
    background-color: map-get($green-palette, "green-400");
  }

  &:active {
    background-color: map-get($green-palette, "green-600");
  }
}

.alert-success {
  background-color: rgba(map-get($status-colors, "success"), 0.15);
  border-left: 4px solid map-get($status-colors, "success");
  color: darken(map-get($status-colors, "success"), 10%);
}

.body-text {
  color: map-get($text-colors, "on-light");
  font-size: map-get($font-sizes, "normal");
}
```

**Final milestone output:** A complete, professional, coherent color system generated from just two seed colors.

---

## Common Beginner Mistakes

### Mistake 1 — Using 0-based index instead of 1-based

```scss
// WRONG (this is how JavaScript works, not Sass):
$first: nth(a b c, 0);   // Error! Index 0 is invalid

// CORRECT (Sass starts at 1):
$first: nth(a b c, 1);   // Returns: a
```

---

### Mistake 2 — Expecting `map-remove()` to change the original map

```scss
$colors: ("red": red, "blue": blue, "green": green);

map-remove($colors, "red");
// This does NOT change $colors!

// CORRECT — capture the result:
$colors: map-remove($colors, "red");
// Now $colors = ("blue": blue, "green": green)
```

---

### Mistake 3 — Passing incompatible units to numeric functions

```scss
// WRONG — cannot compare px and em:
$bigger: max(16px, 2em);   // Error!

// CORRECT — use the same unit:
$bigger: max(16px, 32px);  // Returns: 32px

// Or check first:
@if comparable(16px, 2em) {
  $bigger: max(16px, 2em);
}
```

---

### Mistake 4 — Using color manipulation functions with wrong value ranges

```scss
// WRONG — lighten amount must be 0%–100%:
lighten(#006400, 150%)   // Error — amount too large

// WRONG — alpha must be 0–1 for opacify:
opacify(rgba(0,0,0,0.5), 2)   // Error — amount too large

// CORRECT:
lighten(#006400, 30%)     // Fine
opacify(rgba(0,0,0,0.5), 0.3)  // Fine — result is 0.8
```

---

### Mistake 5 — Confusing `adjust-color()` and `change-color()`

```scss
$color: hsl(120, 80%, 50%);  // A green with 80% saturation

// adjust-color ADDS to the existing value:
adjust-color($color, saturation: 10%)
// Result: saturation becomes 80% + 10% = 90%

// change-color REPLACES the value:
change-color($color, saturation: 10%)
// Result: saturation becomes 10% (ignores the existing 80%)
```

---

## Reflection Questions

1. In your own words, explain the difference between `ceil()`, `floor()`, and `round()`. When would you use each?

2. Why are Sass lists and maps **immutable**? What does this mean for how you must write code that "changes" them?

3. A designer tells you: "Make the button slightly more transparent when disabled." Which color function would you use, and what value would you pass for the amount?

4. You have a variable `$spacing` but you are not sure if it is a number (like `16px`) or a string (like `"auto"`). Which introspection function would you use to check?

5. What is the relationship between `lighten()` / `darken()` and the **Lightness** channel of the HSL color model?

---

## Completion Checklist

Before moving to the next lesson, confirm that you can:

- [ ] Use `str-length()`, `str-slice()`, `str-index()`, `str-insert()`, `to-upper-case()`, `to-lower-case()`
- [ ] Explain the difference between `ceil()`, `floor()`, and `round()`
- [ ] Use `max()`, `min()`, `abs()`, `percentage()`, and `random()`
- [ ] Access list items with `nth()`, find positions with `index()`, add items with `append()`, and join lists with `join()`
- [ ] Create a Sass map and retrieve values with `map-get()`
- [ ] Use `map-merge()` and `map-remove()` correctly
- [ ] Explain what `is-superselector()` checks
- [ ] Use `type-of()` to inspect a value's data type
- [ ] Use `unit()` and `unitless()` to inspect numbers
- [ ] Create colors with `rgb()`, `rgba()`, `hsl()`, and `hsla()`
- [ ] Read color channels with `red()`, `green()`, `blue()`, `hue()`, `saturation()`, `lightness()`
- [ ] Transform colors with `lighten()`, `darken()`, `mix()`, `transparentize()`, `opacify()`
- [ ] Complete the mini project color system

---

## Lesson Summary

In this lesson you have explored all seven categories of Sass built-in functions:

**String functions** let you manipulate text values: measuring length, changing case, finding and extracting substrings, and inserting text. All Sass strings count from index 1.

**Numeric functions** give you mathematical tools: rounding with `ceil()`, `floor()`, and `round()`; finding extremes with `max()` and `min()`; converting with `percentage()`; and generating randomness with `random()`.

**List functions** work with ordered collections of values. Because lists are immutable, functions like `append()` and `join()` return new lists. The first item in a list is always at index 1.

**Map functions** work with key/value stores that are perfect for storing design tokens. `map-get()` retrieves values, `map-has-key()` checks existence, and `map-merge()` combines maps.

**Selector functions** inspect and manipulate CSS selectors, most useful inside advanced mixins. They let you check selector relationships with `is-superselector()` and build new selectors with `selector-append()` and `selector-replace()`.

**Introspection functions** are debugging and safety tools. `type-of()` tells you what kind of value you have, `unit()` reveals a number's unit, and `variable-exists()` / `mixin-exists()` / `function-exists()` check whether named things are available.

**Color functions** are the most powerful category. You can create colors with `rgb()`, `hsl()`, and their alpha variants; read channels with `red()`, `hue()`, `saturation()`, etc.; and transform colors with `lighten()`, `darken()`, `mix()`, `adjust-hue()`, and many more.

---

## Quick Reference Card

### String Functions
| Function | Returns |
|---|---|
| `quote(str)` | Quoted string |
| `unquote(str)` | Unquoted string |
| `str-length(str)` | Character count |
| `str-index(str, sub)` | Position of substring |
| `str-insert(str, ins, n)` | String with insertion |
| `str-slice(str, start, end)` | Extracted substring |
| `to-upper-case(str)` | UPPERCASE string |
| `to-lower-case(str)` | lowercase string |
| `unique-id()` | Random unique string |

### Numeric Functions
| Function | Returns |
|---|---|
| `abs(n)` | Positive value |
| `ceil(n)` | Rounded up |
| `floor(n)` | Rounded down |
| `round(n)` | Rounded normally |
| `max(n...)` | Largest number |
| `min(n...)` | Smallest number |
| `percentage(n)` | n × 100% |
| `comparable(a, b)` | true/false |
| `random()` | 0–1 decimal |
| `random(n)` | 1–n integer |

### Color Functions (Key Ones)
| Function | Returns |
|---|---|
| `rgb(r, g, b)` | Color value |
| `rgba(r, g, b, a)` | Color with opacity |
| `hsl(h, s, l)` | Color value |
| `lighten(color, %)` | Lighter color |
| `darken(color, %)` | Darker color |
| `mix(c1, c2, %)` | Blended color |
| `transparentize(c, n)` | More transparent |
| `opacify(c, n)` | More opaque |
| `red(c) / green(c) / blue(c)` | Channel value (0–255) |
| `hue(c) / saturation(c) / lightness(c)` | HSL component |
| `type-of(v)` | Data type name |
| `unit(n)` | Unit string |
| `map-get(map, key)` | Map value |
| `nth(list, n)` | List item |
