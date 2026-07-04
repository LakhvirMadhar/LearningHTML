# Lesson 05: Tables

## What We're Doing
Learn how to display data in rows and columns using HTML tables.

## Why / Context
Tables are for displaying structured data — think schedules, pricing pages, stats, spreadsheets, leaderboards, anything where information makes sense in rows and columns. You see them everywhere: Amazon product comparisons, sports standings, your bank transaction history.

Back in the early days of the web, people actually used tables to build entire page layouts (like putting your sidebar in one column and your content in another). That's considered bad practice now — CSS handles layout much better. Today, tables are strictly for tabular data.

Even though frameworks like React can generate tables dynamically from data, the underlying HTML is still `<table>`, `<tr>`, `<td>`. Knowing how tables work means you can build them, style them with CSS, and debug them when something looks off.

## Concepts

### Basic Table Structure
A table is built with three main tags, nested inside each other like Russian dolls:

- **`<table>`** — the outer container that wraps everything. Think of it as the spreadsheet itself.
- **`<tr>`** — stands for **t**able **r**ow. Each `<tr>` is one horizontal row in your table.
- **`<td>`** — stands for **t**able **d**ata. Each `<td>` is one individual cell inside a row.

Here's a simple 2-row, 3-column table:

```html
<table border="1">
    <tr>
        <td>Row 1, Cell 1</td>
        <td>Row 1, Cell 2</td>
        <td>Row 1, Cell 3</td>
    </tr>
    <tr>
        <td>Row 2, Cell 1</td>
        <td>Row 2, Cell 2</td>
        <td>Row 2, Cell 3</td>
    </tr>
</table>
```

**Important:** Notice the `border="1"` on the `<table>` tag — that's an **attribute**, one of those `key="value"` pairs inside the tag that you've been using since Lesson 03 (like `href` on links and `src` on images). This particular attribute tells the browser to draw visible borders around the cells. By default tables have no visible borders, so you'd just see text floating with no grid lines — very confusing. Always add `border="1"` while learning so you can see the cell boundaries. VS Code might show a red squiggle warning because this is an older attribute that's been replaced by CSS — ignore it, it works fine. We'll replace it with CSS later.

The nesting goes: `<table>` contains `<tr>` rows, and each `<tr>` contains `<td>` cells. Every row should have the same number of cells, otherwise your table will look lopsided (the browser won't crash, it'll just look weird).

When you first type this out and open it in the browser, you might be confused — it'll look like plain text with no grid lines. That's because tables have no visible borders by default. We'll fix that below.

### Table Headers
Most tables have a header row at the top — column titles like "Name", "Age", "City". For these, use **`<th>`** (table header) instead of `<td>`. The browser automatically makes header cells **bold** and **centered**, so they stand out from normal data cells.

```html
<table>
    <tr>
        <th>Name</th>
        <th>Age</th>
        <th>City</th>
    </tr>
    <tr>
        <td>Alice</td>
        <td>25</td>
        <td>London</td>
    </tr>
    <tr>
        <td>Bob</td>
        <td>30</td>
        <td>Tokyo</td>
    </tr>
</table>
```

Screen readers also use `<th>` to help visually impaired users understand which column they're in. So it's not just a visual thing — it has meaning, like `<strong>` vs `<b>`.

### Table Sections
For bigger tables, you can organize your rows into three logical sections. These are optional, but they're good practice and become useful when you start styling with CSS:

- **`<thead>`** — wraps the header row(s) at the top. This is where your `<th>` cells live.
- **`<tbody>`** — wraps all the data rows in the middle. This is the main content of the table.
- **`<tfoot>`** — wraps the footer row(s) at the bottom. Typically used for totals, summaries, or notes.

```html
<table>
    <thead>
        <tr>
            <th>Item</th>
            <th>Price</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Coffee</td>
            <td>$3</td>
        </tr>
        <tr>
            <td>Donut</td>
            <td>$2</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>Total</td>
            <td>$5</td>
        </tr>
    </tfoot>
</table>
```

Visually it looks the same as before — you won't see any difference in the browser. The benefit is under the hood: screen readers understand the structure better, CSS can target each section separately (like giving the header a different background color), and if you print a long table, the browser can repeat the header on every page.

### Spanning Rows and Columns
Sometimes you need a cell to stretch across multiple columns or multiple rows. This is like merging cells in Excel.

**`colspan`** — makes a cell span across multiple columns. The number tells it how many columns to take up:

```html
<table border="1">
    <tr>
        <td colspan="3">This cell stretches across all 3 columns</td>
    </tr>
    <tr>
        <td>Cell 1</td>
        <td>Cell 2</td>
        <td>Cell 3</td>
    </tr>
</table>
```

**`rowspan`** — makes a cell span across multiple rows. The cell "reaches down" into the row(s) below it:

```html
<table border="1">
    <tr>
        <td rowspan="2">This cell takes up 2 rows</td>
        <td>Normal cell</td>
    </tr>
    <tr>
        <td>Normal cell (first column is already filled by the rowspan above)</td>
    </tr>
</table>
```

These are tricky at first, especially `rowspan`. Let's walk through more concrete examples.

#### colspan example — a totals row

Think of a table as a grid on paper. Say you have a 3-column table with names, ages, and cities, and you want a "TOTAL" row at the bottom that stretches across the whole table:

```
| Name    | Age | City   |
| Alice   | 25  | London |
| Bob     | 30  | Tokyo  |
| TOTAL: 2 people        |
```

That last row — "TOTAL: 2 people" — takes up all 3 column slots. In HTML, you write ONE `<td>` instead of three, because that single cell is occupying all three spots:

```html
<tr>
    <td colspan="3">TOTAL: 2 people</td>
</tr>
```

If you wrote `colspan="2"` instead, the cell would take up two columns and you'd still need a second `<td>` for the third column.

#### rowspan example — a class schedule

This is the trickier one. Imagine a school schedule:

```
| Day     | Morning | Afternoon |
| Monday  | Math    | English   |
| Tuesday | Math    | Science   |
```

Monday and Tuesday both have Math in the morning. You want to merge those two "Math" cells into one tall cell that spans both rows:

```
| Day     | Morning | Afternoon |
| Monday  |         | English   |
|         |  Math   |           |
| Tuesday |         | Science   |
```

In HTML:

```html
<tr>
    <td>Monday</td>
    <td rowspan="2">Math</td>
    <td>English</td>
</tr>
<tr>
    <td>Tuesday</td>
    <!-- NO morning cell here — the rowspan above is already occupying this spot -->
    <td>Science</td>
</tr>
```

The critical thing to notice: the second `<tr>` only has TWO `<td>` tags instead of three. That's because the "Math" cell from the first row is reaching down and occupying the morning slot in the second row. If you accidentally put three `<td>` tags in the second row, the table would get an extra column and look broken.

The rule: when a `rowspan` from a previous row is occupying a slot, you skip that `<td>` in the current row. Count the columns carefully — the total number of columns should stay consistent across all rows, but some of those columns are being filled by spanning cells from above.

Try building that schedule table yourself. Add `border="1"` so you can see the grid — it makes everything much clearer. It clicks once you see it render in the browser.

### Table Caption
You can give your table a title using `<caption>`. It goes right after the opening `<table>` tag, before any rows. The browser displays it above the table by default.

```html
<table>
    <caption>Monthly Expenses</caption>
    <tr>
        <th>Item</th>
        <th>Cost</th>
    </tr>
</table>
```

This is also useful for accessibility — screen readers announce the caption so users know what the table is about before they start navigating it.

### Borders
By default, tables have no visible borders, which makes them hard to work with while learning. You can add a quick border to see the grid lines:

```html
<table border="1">
```

This is an old HTML attribute from the early web — the proper way to add borders is with CSS, which we'll learn later. But for now, `border="1"` is a handy shortcut so you can actually see what your table looks like. Feel free to use it on every table in this lesson.

## Your Task

Create a new file called `tables.html` (with the full boilerplate skeleton from lesson 01), and build the following:

1. Add an `<h2>` for "Tables"
2. Create a basic table with at least 3 columns and 3 rows of data — pick any topic you want (favorite games, groceries, work schedule, whatever)
3. Add a header row using `<th>` tags so the columns have titles
4. Add `border="1"` to your `<table>` so you can actually see the grid
5. Wrap your table in `<thead>`, `<tbody>`, and `<tfoot>` sections — put a total or summary in the footer
6. Add a `<caption>` to give your table a title
7. Try `colspan` — make one cell in the footer span across all columns (like a "Total" row)
8. If you're feeling adventurous, try `rowspan` — make one cell stretch across two rows

Save and refresh after each step. Add `border="1"` first so you can see the grid while you work. Let me know when you want a review.
