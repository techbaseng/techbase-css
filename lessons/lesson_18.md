---
render_with_liquid: false
title: "Lesson 18: CSS Tables — Borders, Size, Alignment, Styling & Responsive Design"
nav_order: 18
---

# Lesson 18: CSS Tables — Borders, Size, Alignment, Styling & Responsive Design

---

## Lesson Introduction

Tables are one of the most powerful tools for presenting information on a webpage. Think of every report you've read, every pricing comparison chart, every sports leaderboard, every bank statement — they all use tables. A table organises data into **rows** and **columns** so readers can quickly find, compare, and understand information.

Without CSS, HTML tables look extremely plain — thin borders, cramped cells, and no visual structure. With CSS, you can turn the exact same table into something polished, professional, and even responsive (usable on a small phone screen).

By the end of this lesson, you will be able to:

- Add and style **borders** around table cells and around the whole table
- Control **table width and column height**
- **Align** text and content inside table cells (horizontally and vertically)
- Apply **background colours**, **zebra striping**, and **hover effects** for readability
- Style the **caption** of a table
- Make a table **responsive** so it works on mobile screens

> **Real-world connection:** If you've ever looked at a class schedule, a sports fixture list, a product comparison page (like comparing phone models), or a data dashboard — you've seen styled CSS tables in action.

---

## Prerequisite Concepts

Before we begin, let's be crystal clear on how HTML tables are structured. If you already know this, skim quickly. If you're not sure, read carefully — you will need this to understand the CSS.

### How an HTML Table Is Built

An HTML table is made of several elements that work together:

| Element | What It Represents |
|---|---|
| `<table>` | The outer container — the whole table |
| `<tr>` | A **table row** — one horizontal row of cells |
| `<th>` | A **table header** cell — bold and centred by default |
| `<td>` | A **table data** cell — normal text by default |
| `<caption>` | A title/label for the whole table |
| `<thead>` | Groups the header rows |
| `<tbody>` | Groups the body (data) rows |
| `<tfoot>` | Groups the footer rows |

### A Basic Table Before Any CSS

```html
<table>
  <caption>Student Results</caption>
  <thead>
    <tr>
      <th>Name</th>
      <th>Subject</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Amara</td>
      <td>Mathematics</td>
      <td>88</td>
    </tr>
    <tr>
      <td>Kelechi</td>
      <td>Physics</td>
      <td>74</td>
    </tr>
    <tr>
      <td>Fatima</td>
      <td>Chemistry</td>
      <td>92</td>
    </tr>
  </tbody>
</table>
```

**Expected Output (no CSS):**

Without any styles, this table will appear as plain text in rows — no visible borders, no spacing, very hard to read. It might look like:

```
Student Results
Name     Subject      Score
Amara    Mathematics  88
Kelechi  Physics      74
Fatima   Chemistry    92
```

Now, let's fix that with CSS — step by step.

---

## Part 1: CSS Table Borders

### What Are Table Borders?

A **border** in CSS is a visible line drawn around or between elements. For tables, you can add borders around:

- The entire `<table>` element
- Each `<th>` (header) cell
- Each `<td>` (data) cell

### The `border` Property

You already know the CSS `border` property from previous lessons. On a table, you apply it just like you would on any other element:

```css
table, th, td {
  border: 1px solid black;
}
```

This selector targets THREE elements at once: the `<table>`, every `<th>`, and every `<td>`. All three get a 1-pixel solid black border.

### Example 1: Basic Border

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      table, th, td {
        border: 1px solid black;
      }
    </style>
  </head>
  <body>
    <table>
      <tr>
        <th>Name</th>
        <th>Score</th>
      </tr>
      <tr>
        <td>Amara</td>
        <td>88</td>
      </tr>
      <tr>
        <td>Kelechi</td>
        <td>74</td>
      </tr>
    </table>
  </body>
</html>
```

**Expected Output:** A table where every cell has its own black border — but notice that between adjacent cells, you will see **double borders** (two separate lines right next to each other). This looks a bit odd.

> **Why double borders?** Each cell draws its own border. The right border of one cell sits right beside the left border of the next cell, making it look doubled.

---

### The `border-collapse` Property

`border-collapse` is one of the most important table-specific CSS properties. It tells the browser how to handle borders between adjacent cells.

| Value | What Happens |
|---|---|
| `separate` | Each cell has its own distinct border — double borders appear (this is the **default**) |
| `collapse` | Adjacent borders are merged into a single shared border — clean, single lines |

**Think of it this way:** `collapse` is like folding two pieces of paper together at the edge so only one edge shows. `separate` is like placing them side by side so both edges are visible.

### Example 2: Collapsed Borders (Clean Look)

```html
<style>
  table {
    border-collapse: collapse;
  }

  table, th, td {
    border: 1px solid black;
  }
</style>

<table>
  <tr>
    <th>Name</th>
    <th>Score</th>
  </tr>
  <tr>
    <td>Amara</td>
    <td>88</td>
  </tr>
  <tr>
    <td>Kelechi</td>
    <td>74</td>
  </tr>
</table>
```

**Expected Output:** A clean, professional table where each border is a single line — no double borders anywhere. This is the standard look for most data tables.

> **Key Rule:** Always add `border-collapse: collapse` on the `<table>` element if you want single borders. This is one of the most commonly used table CSS rules in professional web development.

---

### The `border-spacing` Property

When `border-collapse` is set to `separate` (or when you don't collapse), you can control the gap between individual cells using `border-spacing`:

```css
table {
  border-spacing: 10px;        /* equal spacing on all sides */
  border-spacing: 5px 15px;   /* 5px horizontal, 15px vertical */
}
```

### Example 3: Border Spacing

```html
<style>
  table {
    border-spacing: 10px;
  }

  table, th, td {
    border: 2px solid steelblue;
  }
</style>

<table>
  <tr>
    <th>Product</th>
    <th>Price</th>
  </tr>
  <tr>
    <td>Laptop</td>
    <td>₦250,000</td>
  </tr>
  <tr>
    <td>Phone</td>
    <td>₦85,000</td>
  </tr>
</table>
```

**Expected Output:** A table where each cell floats in its own "island" with visible gaps between them — like tiles on a floor with grout between them.

---

### Border on Individual Sides Only

Just like any HTML element, you can border only specific sides of a table or its cells. A common professional style is the "lines only" look — horizontal lines between rows but no outer box:

```html
<style>
  table {
    border-collapse: collapse;
    width: 100%;
  }

  th, td {
    border-bottom: 1px solid #ddd;
    padding: 8px;
  }
</style>

<table>
  <tr>
    <th>Name</th>
    <th>Score</th>
  </tr>
  <tr>
    <td>Amara</td>
    <td>88</td>
  </tr>
  <tr>
    <td>Kelechi</td>
    <td>74</td>
  </tr>
</table>
```

**Expected Output:** A clean table with only horizontal lines between rows — no box around the outside, no vertical lines. This is one of the most popular modern table styles, used in Google Sheets, GitHub, and many dashboards.

---

## Part 2: CSS Table Size (Width and Height)

### Why Control Table Size?

By default, a table is only as wide as its content. A table with very short data will be very narrow. A table with many columns might overflow off the screen. Controlling width and height lets you:

- Make a table span the full page width (100%)
- Give rows a minimum height so they look consistent
- Control specific column widths

### Setting Table Width

The `width` property on the `<table>` element controls the full table width:

```html
<style>
  table {
    width: 100%;
    border-collapse: collapse;
  }

  th, td {
    border: 1px solid black;
    padding: 8px;
  }
</style>

<table>
  <tr>
    <th>Country</th>
    <th>Capital</th>
    <th>Population</th>
  </tr>
  <tr>
    <td>Nigeria</td>
    <td>Abuja</td>
    <td>220 million</td>
  </tr>
  <tr>
    <td>Kenya</td>
    <td>Nairobi</td>
    <td>55 million</td>
  </tr>
</table>
```

**Expected Output:** A table that stretches to fill the entire width of its parent container — useful for dashboards, reports, and data pages.

> **Tip:** `width: 100%` means "use all available horizontal space." `width: 500px` would fix the table at exactly 500 pixels wide.

### Setting Row Height

Use the `height` property on `<tr>`, `<th>`, or `<td>` to control row height:

```html
<style>
  table {
    border-collapse: collapse;
  }

  th {
    height: 60px;
    background-color: #2c3e50;
    color: white;
  }

  td {
    height: 40px;
    border: 1px solid #ccc;
  }
</style>

<table>
  <tr>
    <th>Item</th>
    <th>Quantity</th>
  </tr>
  <tr>
    <td>Rice (5kg)</td>
    <td>3 bags</td>
  </tr>
  <tr>
    <td>Beans (2kg)</td>
    <td>5 bags</td>
  </tr>
</table>
```

**Expected Output:** A table where the header row is taller (60px) than the data rows (40px).

### Setting Specific Column Widths

You control column widths by setting `width` on individual `<th>` or `<td>` elements:

```html
<style>
  table {
    border-collapse: collapse;
    width: 100%;
  }

  th, td {
    border: 1px solid #ccc;
    padding: 8px;
  }

  th:first-child {
    width: 200px;   /* First column is 200px wide */
  }

  th:nth-child(2) {
    width: 100px;   /* Second column is 100px wide */
  }
</style>

<table>
  <tr>
    <th>Student Name</th>
    <th>Score</th>
    <th>Grade</th>
  </tr>
  <tr>
    <td>Chidinma Okonkwo</td>
    <td>91</td>
    <td>A</td>
  </tr>
</table>
```

**Expected Output:** The first column is wider (for long names), the second is fixed narrower (scores are short), and the third takes the remaining space.

> **Important:** The width you set on the first `<th>` in a column sets that column's width for the WHOLE column — all `<td>` cells below it will follow the same width.

---

## Part 3: CSS Table Alignment

Alignment controls **where content sits inside a cell** — both horizontally (left, right, centre) and vertically (top, middle, bottom).

### Horizontal Alignment with `text-align`

By default:
- `<th>` (header cells) are **centre-aligned**
- `<td>` (data cells) are **left-aligned**

You can override these defaults with `text-align`:

```html
<style>
  table {
    border-collapse: collapse;
    width: 100%;
  }

  th, td {
    border: 1px solid #ccc;
    padding: 10px;
  }

  th {
    text-align: left;     /* Override default centre to left */
  }

  td.amount {
    text-align: right;    /* Numbers are often right-aligned */
  }

  td.status {
    text-align: center;   /* Status badges look nice centred */
  }
</style>

<table>
  <tr>
    <th>Invoice</th>
    <th>Amount (₦)</th>
    <th>Status</th>
  </tr>
  <tr>
    <td>INV-001</td>
    <td class="amount">45,000</td>
    <td class="status">Paid</td>
  </tr>
  <tr>
    <td>INV-002</td>
    <td class="amount">12,500</td>
    <td class="status">Pending</td>
  </tr>
</table>
```

**Expected Output:** Invoice names are left-aligned, amounts are right-aligned (as is standard for numbers/money), and statuses are centred.

> **Why right-align numbers?** When numbers are right-aligned, the units column, tens column, and hundreds column all line up vertically — making it much easier to compare values at a glance. This is standard practice in accounting, spreadsheets, and financial tables.

### Vertical Alignment with `vertical-align`

`vertical-align` controls where content sits **top-to-bottom** within a cell. This matters most when cells have varying amounts of content and different heights.

| Value | Content Position |
|---|---|
| `top` | Content sits at the top of the cell |
| `middle` | Content is centred vertically (default for `<th>` and `<td>`) |
| `bottom` | Content sits at the bottom of the cell |

```html
<style>
  table {
    border-collapse: collapse;
    width: 100%;
  }

  th, td {
    border: 1px solid #ccc;
    padding: 10px;
    height: 80px;   /* Make cells tall to see alignment differences */
  }

  .top-align    { vertical-align: top; }
  .middle-align { vertical-align: middle; }
  .bottom-align { vertical-align: bottom; }
</style>

<table>
  <tr>
    <td class="top-align">Top aligned</td>
    <td class="middle-align">Middle aligned</td>
    <td class="bottom-align">Bottom aligned</td>
  </tr>
</table>
```

**Expected Output:** Three cells of equal height, but the text in each sits at a different vertical position — top, middle, and bottom respectively.

### Combining Horizontal and Vertical Alignment

You will often use both together, especially for header cells:

```css
th {
  text-align: center;     /* horizontal */
  vertical-align: middle; /* vertical */
}
```

---

## Part 4: CSS Table Styling

This is where your tables truly come to life. Let's explore all the visual styling techniques used on real websites.

### 4.1 — Padding Inside Cells

Without padding, cell content is crammed right against the borders, making the table very hard to read. `padding` adds breathing room inside each cell:

```html
<style>
  table {
    border-collapse: collapse;
  }

  th, td {
    border: 1px solid #ccc;
    padding: 12px 16px;   /* 12px top/bottom, 16px left/right */
  }
</style>

<table>
  <tr>
    <th>Name</th>
    <th>Department</th>
  </tr>
  <tr>
    <td>Grace</td>
    <td>Engineering</td>
  </tr>
</table>
```

**Expected Output:** A table where the text inside each cell has comfortable space around it — no cramming against the borders.

> **Think of padding like the margins in a notebook.** Without margins, you'd write right to the edge of the paper. Padding gives content room to breathe.

---

### 4.2 — Styling the Header Row

Making header cells visually distinct from data cells greatly improves readability. You do this by targeting the `<th>` element or the `<thead>` group:

```html
<style>
  table {
    border-collapse: collapse;
    width: 100%;
  }

  th {
    background-color: #2c3e50;
    color: white;
    padding: 12px;
    text-align: left;
    font-size: 14px;
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  td {
    padding: 10px 12px;
    border-bottom: 1px solid #ddd;
  }
</style>

<table>
  <tr>
    <th>Product</th>
    <th>Category</th>
    <th>Price (₦)</th>
  </tr>
  <tr>
    <td>Wireless Mouse</td>
    <td>Electronics</td>
    <td>8,500</td>
  </tr>
  <tr>
    <td>Notebook A4</td>
    <td>Stationery</td>
    <td>650</td>
  </tr>
</table>
```

**Expected Output:** A professional-looking table with a dark header row containing white text, and clean data rows below separated by light grey horizontal lines.

---

### 4.3 — Zebra Striping (Alternating Row Colours)

**Zebra striping** means alternating background colours on rows (light, dark, light, dark...) — like a zebra's stripes. This makes it much easier for the human eye to follow a row across a wide table without losing track.

To do this in CSS, we use the `:nth-child()` pseudo-class:

- `tr:nth-child(even)` — selects row 2, 4, 6, 8... (even-numbered rows)
- `tr:nth-child(odd)` — selects row 1, 3, 5, 7... (odd-numbered rows)

```html
<style>
  table {
    border-collapse: collapse;
    width: 100%;
  }

  th {
    background-color: #34495e;
    color: white;
    padding: 12px;
    text-align: left;
  }

  td {
    padding: 10px 12px;
  }

  /* Every EVEN row gets a light grey background */
  tr:nth-child(even) {
    background-color: #f2f2f2;
  }

  /* Every ODD row stays white (default background) */
  tr:nth-child(odd) {
    background-color: #ffffff;
  }
</style>

<table>
  <tr>
    <th>Name</th>
    <th>Score</th>
    <th>Grade</th>
  </tr>
  <tr>
    <td>Amara</td>
    <td>92</td>
    <td>A</td>
  </tr>
  <tr>
    <td>Kelechi</td>
    <td>74</td>
    <td>B</td>
  </tr>
  <tr>
    <td>Fatima</td>
    <td>88</td>
    <td>A</td>
  </tr>
  <tr>
    <td>Emeka</td>
    <td>61</td>
    <td>C</td>
  </tr>
</table>
```

**Expected Output:** Row 1 (Amara) — white background. Row 2 (Kelechi) — light grey. Row 3 (Fatima) — white. Row 4 (Emeka) — light grey. This pattern repeats automatically.

> **Why does this help?** Imagine tracking across a table with 10 columns. Your eye can easily drift from one row to another by accident. Alternating colours act like a guide rail, keeping your eye on the right row.

> **Thinking Prompt:** What happens if you change `tr:nth-child(even)` to `tr:nth-child(3n)`? What rows would that select?

---

### 4.4 — Hover Effect on Table Rows

A hover effect highlights a row when the user moves their mouse over it. This is incredibly useful for interactive data tables — it shows the user exactly which row they are looking at.

```html
<style>
  table {
    border-collapse: collapse;
    width: 100%;
  }

  th {
    background-color: #2c3e50;
    color: white;
    padding: 12px;
    text-align: left;
  }

  td {
    padding: 10px 12px;
    border-bottom: 1px solid #ddd;
  }

  tr:nth-child(even) {
    background-color: #f9f9f9;
  }

  /* This adds the hover highlight */
  tr:hover {
    background-color: #d5e8fa;
  }
</style>

<table>
  <tr>
    <th>Name</th>
    <th>Score</th>
  </tr>
  <tr>
    <td>Amara</td>
    <td>92</td>
  </tr>
  <tr>
    <td>Kelechi</td>
    <td>74</td>
  </tr>
  <tr>
    <td>Fatima</td>
    <td>88</td>
  </tr>
</table>
```

**Expected Output:** As you hover your mouse over any data row, it lights up with a blue highlight. Move the mouse away and it returns to normal.

> **Important:** The `:hover` pseudo-class also applies to the header row `<tr>`. If you want to exclude the header from highlighting, you can be more specific: `tbody tr:hover` (only affects rows inside the `<tbody>`).

---

### 4.5 — Background Colour on Individual Cells

You can highlight specific cells — for example, to show a "best value" column or a failing grade:

```html
<style>
  table {
    border-collapse: collapse;
    width: 100%;
  }

  th, td {
    border: 1px solid #ccc;
    padding: 10px;
  }

  .fail    { background-color: #fadbd8; color: #922b21; }   /* red tint */
  .pass    { background-color: #d5f5e3; color: #1e8449; }   /* green tint */
  .warning { background-color: #fef9e7; color: #b7950b; }   /* yellow tint */
</style>

<table>
  <tr>
    <th>Student</th>
    <th>Score</th>
    <th>Result</th>
  </tr>
  <tr>
    <td>Amara</td>
    <td>92</td>
    <td class="pass">Pass</td>
  </tr>
  <tr>
    <td>Kelechi</td>
    <td>48</td>
    <td class="fail">Fail</td>
  </tr>
  <tr>
    <td>Fatima</td>
    <td>55</td>
    <td class="warning">Borderline</td>
  </tr>
</table>
```

**Expected Output:** A table where the "Result" column cells are colour-coded — green for Pass, red for Fail, yellow for Borderline.

---

### 4.6 — Styling the Table Caption

The `<caption>` element adds a title to the table. By default, it appears above the table and is centre-aligned. You can style it like any text:

```html
<style>
  table {
    border-collapse: collapse;
    width: 100%;
  }

  caption {
    caption-side: top;           /* 'top' or 'bottom' */
    font-size: 20px;
    font-weight: bold;
    color: #2c3e50;
    text-align: left;
    padding: 10px 0;
    letter-spacing: 1px;
  }

  th, td {
    border: 1px solid #ccc;
    padding: 10px;
  }
</style>

<table>
  <caption>Q1 Sales Report — 2026</caption>
  <tr>
    <th>Product</th>
    <th>Units Sold</th>
    <th>Revenue (₦)</th>
  </tr>
  <tr>
    <td>Laptop</td>
    <td>45</td>
    <td>11,250,000</td>
  </tr>
</table>
```

**Expected Output:** A bold, dark-coloured caption "Q1 Sales Report — 2026" appears above the table, left-aligned.

The `caption-side` property controls position:
- `caption-side: top` → caption above the table (default)
- `caption-side: bottom` → caption below the table

---

### 4.7 — A Complete Professional Table Style

Let's now combine everything we've learned into one polished, professional table:

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      body {
        font-family: Arial, sans-serif;
        background: #f5f6fa;
        padding: 30px;
      }

      table {
        border-collapse: collapse;
        width: 100%;
        background-color: white;
        box-shadow: 0 2px 10px rgba(0,0,0,0.08);
        border-radius: 8px;
        overflow: hidden;
      }

      caption {
        font-size: 22px;
        font-weight: bold;
        color: #2c3e50;
        text-align: left;
        padding: 16px 0 12px 0;
      }

      th {
        background-color: #2c3e50;
        color: white;
        padding: 14px 16px;
        text-align: left;
        font-size: 13px;
        text-transform: uppercase;
        letter-spacing: 1px;
      }

      td {
        padding: 12px 16px;
        border-bottom: 1px solid #ecf0f1;
        color: #333;
        font-size: 15px;
      }

      tr:nth-child(even) td {
        background-color: #f8f9fa;
      }

      tbody tr:hover td {
        background-color: #d6eaf8;
        cursor: pointer;
      }

      td:last-child {
        text-align: right;
        font-weight: bold;
      }

      th:last-child {
        text-align: right;
      }
    </style>
  </head>
  <body>
    <table>
      <caption>Employee Salary Report — April 2026</caption>
      <thead>
        <tr>
          <th>Employee</th>
          <th>Department</th>
          <th>Role</th>
          <th>Salary (₦)</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Amara Okonkwo</td>
          <td>Engineering</td>
          <td>Senior Developer</td>
          <td>850,000</td>
        </tr>
        <tr>
          <td>Kelechi Eze</td>
          <td>Design</td>
          <td>UI/UX Designer</td>
          <td>620,000</td>
        </tr>
        <tr>
          <td>Fatima Sule</td>
          <td>Marketing</td>
          <td>Brand Manager</td>
          <td>700,000</td>
        </tr>
        <tr>
          <td>Emeka Chukwu</td>
          <td>Engineering</td>
          <td>DevOps Engineer</td>
          <td>780,000</td>
        </tr>
        <tr>
          <td>Grace Adeyemi</td>
          <td>Finance</td>
          <td>Analyst</td>
          <td>590,000</td>
        </tr>
      </tbody>
    </table>
  </body>
</html>
```

**Expected Output:** A fully polished employee salary table with:
- Dark header row with white uppercase text
- Alternating light grey/white rows
- Blue highlight when hovering over any row
- Right-aligned salary column
- Subtle shadow giving the table a card-like appearance

---

## Part 5: Responsive Tables

### What Does "Responsive" Mean?

A **responsive** design adapts to different screen sizes — it looks good on a laptop AND on a small phone screen. This is critical because a huge portion of web traffic comes from mobile devices.

Tables are notoriously difficult on small screens. A wide table with many columns will simply overflow off the right edge of a phone screen. Users then have to scroll sideways, which is very frustrating.

### The Problem: Tables on Mobile

Imagine a 6-column table on a phone that is only 380px wide. The table content might need 800px+ to display properly. The phone cannot shrink the columns enough to show everything — the table "breaks out" of the screen boundary.

### The Solution: `overflow-x: auto`

The standard responsive table technique is to wrap the `<table>` in a `<div>` and allow that div to scroll horizontally on small screens:

```html
<style>
  .table-container {
    overflow-x: auto;    /* allows horizontal scrolling */
    -webkit-overflow-scrolling: touch;  /* smooth scrolling on iOS */
  }

  table {
    border-collapse: collapse;
    width: 100%;
    min-width: 500px;   /* ensures table doesn't shrink too much */
  }

  th, td {
    border: 1px solid #ccc;
    padding: 10px 14px;
    white-space: nowrap;  /* prevents text from wrapping into multiple lines */
  }

  th {
    background-color: #2c3e50;
    color: white;
    text-align: left;
  }

  tr:nth-child(even) {
    background-color: #f5f5f5;
  }
</style>

<div class="table-container">
  <table>
    <tr>
      <th>Name</th>
      <th>Email</th>
      <th>Phone</th>
      <th>City</th>
      <th>Department</th>
      <th>Status</th>
    </tr>
    <tr>
      <td>Amara Okonkwo</td>
      <td>amara@company.ng</td>
      <td>080-1234-5678</td>
      <td>Lagos</td>
      <td>Engineering</td>
      <td>Active</td>
    </tr>
    <tr>
      <td>Kelechi Eze</td>
      <td>kelechi@company.ng</td>
      <td>080-9876-5432</td>
      <td>Abuja</td>
      <td>Design</td>
      <td>Active</td>
    </tr>
    <tr>
      <td>Fatima Sule</td>
      <td>fatima@company.ng</td>
      <td>070-1111-2222</td>
      <td>Kano</td>
      <td>Marketing</td>
      <td>On Leave</td>
    </tr>
  </table>
</div>
```

**Expected Output:**
- On a wide screen (desktop/laptop): The table displays fully, all columns visible
- On a narrow screen (phone): The table can be scrolled left and right to reveal hidden columns — instead of overflowing and breaking the layout

> **Why does this work?** The `<div class="table-container">` acts like a "viewport window" for the table. The div itself stays within the screen width. When the table is wider than the div, the `overflow-x: auto` property adds a scrollbar to the div — keeping the page layout intact while still allowing all table data to be accessed.

### Key Properties Explained

| Property | Where Applied | Purpose |
|---|---|---|
| `overflow-x: auto` | `.table-container` div | Adds horizontal scrollbar when content is wider than the container |
| `-webkit-overflow-scrolling: touch` | `.table-container` div | Makes scrolling smooth on iOS devices |
| `min-width: 500px` | `table` | Prevents table from collapsing to an unreadably narrow width |
| `white-space: nowrap` | `th, td` | Prevents cell text from line-wrapping (which looks bad in tables) |

### Alternative: Making Tables Stack on Mobile

A more advanced technique (using CSS media queries) can transform a multi-column table into a stacked vertical list on small screens. Here is a simplified version:

```html
<style>
  /* Default table style (desktop) */
  table {
    border-collapse: collapse;
    width: 100%;
  }

  th, td {
    padding: 10px;
    border: 1px solid #ccc;
    text-align: left;
  }

  th {
    background-color: #34495e;
    color: white;
  }

  /* On screens narrower than 600px — stack the cells */
  @media (max-width: 600px) {
    table, thead, tbody, th, td, tr {
      display: block;   /* convert table elements to block layout */
    }

    thead tr {
      display: none;    /* hide the header row on mobile */
    }

    td {
      position: relative;
      padding-left: 50%;  /* make room for the label on the left */
      border: none;
      border-bottom: 1px solid #eee;
    }

    /* Add a data label before each cell using a data attribute */
    td::before {
      content: attr(data-label);
      position: absolute;
      left: 10px;
      font-weight: bold;
      color: #555;
    }
  }
</style>

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>City</th>
      <th>Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-label="Name">Amara</td>
      <td data-label="City">Lagos</td>
      <td data-label="Score">92</td>
    </tr>
    <tr>
      <td data-label="Name">Kelechi</td>
      <td data-label="City">Abuja</td>
      <td data-label="Score">74</td>
    </tr>
  </tbody>
</table>
```

**Expected Output:**
- On desktop: Normal table with 3 columns
- On phone (screen under 600px wide): Each row becomes a stacked vertical card. Each cell shows its label ("Name", "City", "Score") on the left side and the value on the right — like a mini form

> **This technique uses `data-label` attributes**, which are custom attributes you add to HTML elements to store extra information. The CSS `::before` pseudo-element then reads that attribute using `attr()` and displays it as a label.

---

## Guided Practice Exercises

### Exercise 1: Grade Book Table

**Objective:** Practise borders, padding, zebra striping, and header styling.

**Scenario:** You are a school teacher and need a digital grade book table.

**Steps:**
1. Create a table with 5 students
2. Columns: Name, Subject, Score (out of 100), Grade
3. Add a caption
4. Style the header row with a dark background and white text
5. Add zebra striping on the data rows
6. Add a hover effect

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      body { font-family: sans-serif; padding: 20px; }

      table {
        border-collapse: collapse;
        width: 100%;
      }

      caption {
        font-size: 20px;
        font-weight: bold;
        text-align: left;
        padding-bottom: 10px;
        color: #2c3e50;
      }

      th {
        background-color: #27ae60;
        color: white;
        padding: 12px;
        text-align: left;
        text-transform: uppercase;
        font-size: 13px;
      }

      td {
        padding: 10px 12px;
        border-bottom: 1px solid #ddd;
      }

      tr:nth-child(even) td {
        background-color: #eafaf1;
      }

      tbody tr:hover td {
        background-color: #a9dfbf;
      }
    </style>
  </head>
  <body>
    <table>
      <caption>JSS 3 — Term 1 Results</caption>
      <thead>
        <tr>
          <th>Name</th>
          <th>Subject</th>
          <th>Score (/100)</th>
          <th>Grade</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Amara Okonkwo</td>
          <td>Mathematics</td>
          <td>88</td>
          <td>A</td>
        </tr>
        <tr>
          <td>Kelechi Eze</td>
          <td>English</td>
          <td>74</td>
          <td>B</td>
        </tr>
        <tr>
          <td>Fatima Sule</td>
          <td>Physics</td>
          <td>92</td>
          <td>A</td>
        </tr>
        <tr>
          <td>Emeka Chukwu</td>
          <td>Chemistry</td>
          <td>61</td>
          <td>C</td>
        </tr>
        <tr>
          <td>Grace Adeyemi</td>
          <td>Biology</td>
          <td>79</td>
          <td>B</td>
        </tr>
      </tbody>
    </table>
  </body>
</html>
```

**Expected Output:** A professional grade book with a green header, alternating green-tinted and white rows, and a deeper green highlight on hover.

**Self-check Questions:**
- What would happen if you removed `border-collapse: collapse`?
- How would you change the zebra colouring so odd rows have the colour instead of even rows?
- How would you highlight students with a score below 70 in red?

---

### Exercise 2: Product Price Comparison Table

**Objective:** Practise text alignment, column width control, and cell background colours.

**Scenario:** You're building a pricing page for a software product with three tiers.

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      body { font-family: Arial, sans-serif; padding: 20px; background: #f0f4f8; }

      table {
        border-collapse: collapse;
        width: 700px;
        background: white;
        border-radius: 8px;
        overflow: hidden;
        box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      }

      caption {
        font-size: 24px;
        font-weight: bold;
        padding: 20px 0 10px;
        color: #1a252f;
        text-align: center;
      }

      th {
        padding: 16px;
        text-align: center;
        font-size: 18px;
        text-transform: uppercase;
      }

      th:nth-child(1) { background-color: #85c1e9; }  /* Basic */
      th:nth-child(2) { background-color: #2980b9; color: white; } /* Pro */
      th:nth-child(3) { background-color: #1a252f; color: white; } /* Enterprise */

      td {
        padding: 12px 16px;
        text-align: center;
        border-bottom: 1px solid #eee;
        font-size: 15px;
      }

      td:first-child {
        text-align: left;
        font-weight: bold;
        background-color: #f8f9fa;
        color: #555;
      }

      .price-row td {
        font-size: 22px;
        font-weight: bold;
        color: #2c3e50;
        padding: 20px;
      }
    </style>
  </head>
  <body>
    <table>
      <caption>Choose Your Plan</caption>
      <thead>
        <tr>
          <th>Feature</th>
          <th>Basic</th>
          <th>Pro</th>
          <th>Enterprise</th>
        </tr>
      </thead>
      <tbody>
        <tr class="price-row">
          <td>Monthly Price</td>
          <td>₦5,000</td>
          <td>₦15,000</td>
          <td>₦45,000</td>
        </tr>
        <tr>
          <td>Users</td>
          <td>1</td>
          <td>5</td>
          <td>Unlimited</td>
        </tr>
        <tr>
          <td>Storage</td>
          <td>5 GB</td>
          <td>50 GB</td>
          <td>500 GB</td>
        </tr>
        <tr>
          <td>Customer Support</td>
          <td>Email only</td>
          <td>Email + Chat</td>
          <td>24/7 Phone</td>
        </tr>
        <tr>
          <td>API Access</td>
          <td>✗</td>
          <td>✓</td>
          <td>✓</td>
        </tr>
      </tbody>
    </table>
  </body>
</html>
```

**Expected Output:** A polished pricing comparison table with colour-coded plan headers and clear data rows. The price row is visually prominent with larger text.

---

### Exercise 3: Responsive Contact Directory

**Objective:** Practise the responsive table technique using `overflow-x: auto`.

**Scenario:** A contact directory that must work on both desktop and mobile.

```html
<!DOCTYPE html>
<html>
  <head>
    <style>
      body { font-family: sans-serif; padding: 16px; }

      .table-wrapper {
        overflow-x: auto;
        border: 1px solid #ddd;
        border-radius: 6px;
      }

      table {
        border-collapse: collapse;
        width: 100%;
        min-width: 600px;
      }

      th {
        background-color: #8e44ad;
        color: white;
        padding: 12px 16px;
        text-align: left;
        white-space: nowrap;
      }

      td {
        padding: 10px 16px;
        border-bottom: 1px solid #eee;
        white-space: nowrap;
      }

      tr:last-child td {
        border-bottom: none;
      }

      tbody tr:hover td {
        background-color: #f3e5f5;
      }
    </style>
  </head>
  <body>
    <div class="table-wrapper">
      <table>
        <thead>
          <tr>
            <th>Full Name</th>
            <th>Email Address</th>
            <th>Phone</th>
            <th>City</th>
            <th>Department</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Amara Okonkwo</td>
            <td>amara@company.ng</td>
            <td>080-1234-5678</td>
            <td>Lagos</td>
            <td>Engineering</td>
          </tr>
          <tr>
            <td>Kelechi Eze</td>
            <td>kelechi@company.ng</td>
            <td>070-9876-5432</td>
            <td>Abuja</td>
            <td>Design</td>
          </tr>
          <tr>
            <td>Fatima Sule</td>
            <td>fatima@company.ng</td>
            <td>090-1111-3333</td>
            <td>Kano</td>
            <td>Marketing</td>
          </tr>
        </tbody>
      </table>
    </div>
  </body>
</html>
```

**Expected Output:** On desktop, a full directory table. On mobile, the table is scrollable horizontally so no data is hidden or cut off.

---

## Mini Project: Student Scorecard Dashboard

**Goal:** Build a complete, professional student results dashboard using all the CSS table techniques you've learned.

### Project Description

You will build a multi-table results page for an imaginary school. It will contain:

1. A **summary statistics table** (collapsed, striped, hoverable)
2. A **full results table** (colour-coded scores, right-aligned numbers, styled caption)
3. A **responsive wrapper** so it works on mobile

### Stage 1: Setup and HTML Structure

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Student Scorecard Dashboard</title>
    <style>
      /* Styles go in Stages 2-4 */
    </style>
  </head>
  <body>

    <h1>Lagos Academy — Term 1 Results Dashboard</h1>

    <!-- Summary Table -->
    <h2>Class Summary</h2>
    <table class="summary-table">
      <caption>Class Statistics</caption>
      <tbody>
        <tr><td>Total Students</td><td>25</td></tr>
        <tr><td>Highest Score</td><td>97</td></tr>
        <tr><td>Lowest Score</td><td>42</td></tr>
        <tr><td>Class Average</td><td>74.3</td></tr>
        <tr><td>Pass Rate</td><td>88%</td></tr>
      </tbody>
    </table>

    <!-- Full Results Table -->
    <h2>Full Results</h2>
    <div class="table-container">
      <table class="results-table">
        <caption>JSS 3A — Term 1 Full Results</caption>
        <thead>
          <tr>
            <th>#</th>
            <th>Student Name</th>
            <th>Maths</th>
            <th>English</th>
            <th>Science</th>
            <th>Social</th>
            <th>Total</th>
            <th>Grade</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>1</td>
            <td>Amara Okonkwo</td>
            <td>92</td><td>88</td><td>95</td><td>85</td>
            <td class="total">360</td>
            <td class="grade-a">A</td>
          </tr>
          <tr>
            <td>2</td>
            <td>Kelechi Eze</td>
            <td>74</td><td>70</td><td>68</td><td>72</td>
            <td class="total">284</td>
            <td class="grade-b">B</td>
          </tr>
          <tr>
            <td>3</td>
            <td>Fatima Sule</td>
            <td>88</td><td>91</td><td>84</td><td>90</td>
            <td class="total">353</td>
            <td class="grade-a">A</td>
          </tr>
          <tr>
            <td>4</td>
            <td>Emeka Chukwu</td>
            <td>55</td><td>60</td><td>48</td><td>52</td>
            <td class="total">215</td>
            <td class="grade-c">C</td>
          </tr>
          <tr>
            <td>5</td>
            <td>Grace Adeyemi</td>
            <td>42</td><td>50</td><td>44</td><td>48</td>
            <td class="total">184</td>
            <td class="grade-f">F</td>
          </tr>
        </tbody>
      </table>
    </div>

  </body>
</html>
```

### Stage 2: Base Styles and Summary Table

```css
body {
  font-family: Arial, sans-serif;
  background-color: #f0f4f8;
  padding: 24px;
  color: #333;
}

h1 {
  color: #2c3e50;
  border-bottom: 3px solid #2980b9;
  padding-bottom: 8px;
}

h2 {
  color: #34495e;
  margin-top: 28px;
}

/* Summary Table */
.summary-table {
  border-collapse: collapse;
  width: 320px;
  background: white;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}

.summary-table caption {
  text-align: left;
  font-weight: bold;
  padding: 8px 0;
  color: #7f8c8d;
  font-size: 13px;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.summary-table td {
  padding: 10px 14px;
  border-bottom: 1px solid #ecf0f1;
}

.summary-table td:first-child {
  color: #7f8c8d;
  font-size: 14px;
}

.summary-table td:last-child {
  text-align: right;
  font-weight: bold;
  font-size: 16px;
  color: #2c3e50;
}

.summary-table tr:nth-child(even) {
  background-color: #f8f9fa;
}
```

**Milestone 2 Output:** A clean summary statistics card on the left side of the page with grey labels and bold values.

### Stage 3: Full Results Table

```css
/* Responsive wrapper */
.table-container {
  overflow-x: auto;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.08);
}

/* Results Table */
.results-table {
  border-collapse: collapse;
  width: 100%;
  min-width: 650px;
  background: white;
}

.results-table caption {
  text-align: left;
  font-size: 16px;
  font-weight: bold;
  padding: 14px 0 8px;
  color: #2c3e50;
}

.results-table th {
  background-color: #2980b9;
  color: white;
  padding: 12px 14px;
  text-align: center;
  font-size: 13px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  white-space: nowrap;
}

.results-table th:nth-child(2) {
  text-align: left;   /* Student name column — left aligned */
}

.results-table td {
  padding: 10px 14px;
  border-bottom: 1px solid #ecf0f1;
  text-align: center;
  font-size: 14px;
}

.results-table td:nth-child(2) {
  text-align: left;
  font-weight: bold;
}

.results-table tr:nth-child(even) td {
  background-color: #f4f6f7;
}

.results-table tbody tr:hover td {
  background-color: #d6eaf8;
}

/* Total column */
.total {
  font-weight: bold;
  font-size: 15px;
  color: #2c3e50;
}
```

**Milestone 3 Output:** A full-width results table with blue header, zebra striping, and hover highlights. Responsive scrolling is enabled.

### Stage 4: Grade Colour Coding

```css
/* Grade badge styles */
.grade-a {
  background-color: #d5f5e3;
  color: #1e8449;
  font-weight: bold;
  border-radius: 4px;
}

.grade-b {
  background-color: #d6eaf8;
  color: #1a5276;
  font-weight: bold;
  border-radius: 4px;
}

.grade-c {
  background-color: #fef9e7;
  color: #b7950b;
  font-weight: bold;
  border-radius: 4px;
}

.grade-f {
  background-color: #fadbd8;
  color: #922b21;
  font-weight: bold;
  border-radius: 4px;
}
```

**Final Output:** A complete dashboard page featuring:
- A compact summary statistics table with clean label/value layout
- A full results table with blue header, alternating stripes, hover effect, bold totals column
- Colour-coded grade badges (green A, blue B, yellow C, red F)
- Full mobile responsiveness via horizontal scrolling

**Reflection Questions:**
- How does colour coding help a teacher read this table faster?
- What would you add to the table to make it sortable by column?
- How would you add a "footer" row showing class totals/averages?

**Optional Advanced Extensions:**
- Add a `<tfoot>` row showing the class average for each subject
- Use `position: sticky; top: 0;` on `th` to make the header row freeze while scrolling
- Add a `border-left: 4px solid green` on the `grade-a` rows using `:has()` or JavaScript

---

## Common Beginner Mistakes

### Mistake 1: Forgetting `border-collapse: collapse`

❌ **Wrong (double borders everywhere):**
```css
table, th, td {
  border: 1px solid black;
}
/* Missing border-collapse! */
```

✅ **Correct:**
```css
table {
  border-collapse: collapse;  /* ALWAYS add this */
}

th, td {
  border: 1px solid black;
}
```

**Why:** Without `border-collapse: collapse`, every cell draws its own border — adjacent cells create ugly double lines.

---

### Mistake 2: Applying `width: 100%` to `th`/`td` Instead of `table`

❌ **Wrong:**
```css
td {
  width: 100%;   /* This makes EACH cell try to be 100% wide — nonsensical */
}
```

✅ **Correct:**
```css
table {
  width: 100%;   /* The WHOLE TABLE takes up 100% of the available space */
}
```

---

### Mistake 3: Confusing `text-align` and `vertical-align`

- `text-align` → horizontal (left, right, centre)
- `vertical-align` → vertical (top, middle, bottom)

❌ **Wrong:**
```css
td {
  text-align: middle;   /* 'middle' is NOT a valid text-align value! */
}
```

✅ **Correct:**
```css
td {
  text-align: center;       /* horizontal centering */
  vertical-align: middle;   /* vertical centering */
}
```

---

### Mistake 4: Forgetting the Responsive Wrapper

❌ **Wrong (table overflows off-screen on mobile):**
```html
<table>...</table>
```

✅ **Correct (table scrolls horizontally on mobile):**
```html
<div style="overflow-x: auto;">
  <table>...</table>
</div>
```

---

### Mistake 5: Using `border-spacing` When `border-collapse: collapse` Is Active

These two properties conflict with each other:

❌ **Wrong:**
```css
table {
  border-collapse: collapse;
  border-spacing: 10px;  /* This is IGNORED when collapse is active */
}
```

✅ **Use one or the other:**
```css
/* Option A: collapsed borders (no spacing between cells) */
table { border-collapse: collapse; }

/* Option B: separate borders with spacing */
table {
  border-collapse: separate;
  border-spacing: 10px;
}
```

---

### Mistake 6: Not Giving Headers Enough Visual Contrast

❌ **Hard to read:**
```css
th {
  background-color: #eee;
  color: #ccc;   /* Light grey on light grey = terrible contrast */
}
```

✅ **Clear contrast:**
```css
th {
  background-color: #2c3e50;   /* Dark background */
  color: white;                /* White text */
}
```

---

### Mistake 7: Applying `:hover` to the Entire `tr` Including the Header

❌ **Oops — the header row highlights too:**
```css
tr:hover {
  background-color: yellow;   /* The <thead> row also turns yellow! */
}
```

✅ **Target only tbody rows:**
```css
tbody tr:hover {
  background-color: #d6eaf8;  /* Only data rows highlight on hover */
}
```

---

## Reflection Questions

1. What is the visual difference between `border-collapse: collapse` and `border-collapse: separate`? When would you choose `separate` over `collapse`?

2. Why are numbers in a table typically right-aligned? Give an example of a table where right-aligning numbers makes a significant difference to readability.

3. You have a table with 8 columns and it is breaking on mobile screens. Describe two different approaches you could use to fix this, and explain the trade-offs of each.

4. What does `tr:nth-child(even)` mean? How would you change it to colour every third row instead?

5. Why might you add `white-space: nowrap` to table cells in a responsive table? What problem does it solve?

6. What is the purpose of `<caption>` in a table? Is it only visual, or does it serve another purpose as well?

7. A client asks you to highlight the entire row of any employee whose salary exceeds ₦700,000. What CSS and/or HTML approach would you take?

---

## Completion Checklist

Tick each item once you feel confident:

- [ ] Understand the HTML structure of a table: `<table>`, `<tr>`, `<th>`, `<td>`, `<thead>`, `<tbody>`, `<tfoot>`, `<caption>`
- [ ] Add borders to a table using `border` on `table, th, td`
- [ ] Use `border-collapse: collapse` to eliminate double borders
- [ ] Use `border-spacing` to control gaps between cells in separate-border mode
- [ ] Apply borders to individual sides only (e.g., `border-bottom` only)
- [ ] Set table width using `width: 100%` or a fixed pixel value
- [ ] Control row height using `height` on `<tr>` or `<td>`
- [ ] Use `text-align` for horizontal cell alignment (left, center, right)
- [ ] Use `vertical-align` for vertical cell alignment (top, middle, bottom)
- [ ] Add comfortable `padding` inside table cells
- [ ] Style the header row with contrasting background and text colour
- [ ] Implement zebra striping using `tr:nth-child(even)` and `tr:nth-child(odd)`
- [ ] Add a hover highlight using `tbody tr:hover`
- [ ] Apply background colour to individual cells for status indication
- [ ] Style the `<caption>` element using `caption-side`, `text-align`, and font properties
- [ ] Build a complete professional table combining all styling techniques
- [ ] Wrap a table in `<div style="overflow-x: auto;">` for mobile responsiveness
- [ ] Understand and use `min-width` and `white-space: nowrap` in responsive tables
- [ ] Complete the Student Scorecard Dashboard mini-project

---

## Lesson Summary

In this lesson you mastered the art of styling HTML tables with CSS. Here is a quick recap of everything covered:

**Table Borders** (`border`, `border-collapse`, `border-spacing`) — Tables need `border-collapse: collapse` to avoid the ugly "double border" problem that occurs when adjacent cells each draw their own border. You can target individual sides with `border-bottom` for a modern "lines-only" look.

**Table Size** (`width`, `height`, column widths) — Use `width: 100%` on the `<table>` to make it fill its container. Apply `height` to `<tr>` elements for consistent row heights. Target individual `<th>` elements to control column widths.

**Table Alignment** (`text-align`, `vertical-align`) — `text-align` controls horizontal content position inside cells (left/center/right). `vertical-align` controls vertical position (top/middle/bottom). Numbers and currency are conventionally right-aligned.

**Table Styling** — The core professional techniques: padding for breathing room, contrasting header colours, zebra striping with `:nth-child()`, hover highlights with `:hover`, colour-coded cells for status, and a styled `<caption>` for the table title.

**Responsive Tables** — The scroll-box pattern: wrap the `<table>` in a `<div>` with `overflow-x: auto`. Add `min-width` to the table and `white-space: nowrap` to cells so the table doesn't collapse or wrap awkwardly on small screens.

With these skills, you can build any kind of data table — from a school grade book to a corporate dashboard — and make it look professional, readable, and mobile-friendly.

---

*Next lesson: CSS Display — understanding `block`, `inline`, `inline-block`, `none`, and how elements are laid out on a page.*
