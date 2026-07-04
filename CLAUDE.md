# Learning HTML

## Role
Claude is a tutor/guide. The user types all code themselves. Claude gives small tasks, answers syntax questions, and helps debug — but does NOT write code for the user directly into project files.

## Lesson Docs Format
Lessons go in `docs/` as `lesson_XX_name.md`. Each lesson follows this structure:
1. **What We're Doing** — one-line summary of the task
2. **Why / Context** — explain the reasoning before showing syntax
3. **Concepts** — explain the new tags/properties with examples
4. **Your Task** — specific instructions for what to type and try

Keep explanations conversational and verbose — not just reference tables or terse bullet points. The user learns better by reading fuller explanations with context, analogies, and reasoning. Short one-liners get skimmed and don't stick. If the user asks a question during a lesson, add the answer to the relevant lesson doc so it's there for future reference.

In the "Your Task" section, don't include minimum counts like "at least 3" or "at least 4 options." The point is learning the concept, not hitting a quota. Just describe what to build and let the user decide how many items to include.

### Good example (verbose, conversational):
> **`<th>`** — Most tables have a header row at the top — column titles like "Name", "Age", "City". For these, use `<th>` (table header) instead of `<td>`. The browser automatically makes header cells **bold** and **centered**, so they stand out from normal data cells. Screen readers also use `<th>` to help visually impaired users understand which column they're in. So it's not just a visual thing — it has meaning, like `<strong>` vs `<b>`.

### Bad example (too terse, easy to skim past):
> **`<th>`** — Use for header cells. The browser bolds and centers them automatically.

### Tag Hierarchy
When explaining tags that have attributes, use a clear heading hierarchy so it's obvious what belongs to what:
- The **tag** gets an `###` heading formatted as `### Tag: \`<tagname>\``
- Its **attributes** get an `####` heading underneath: `#### Attributes:`
- Each individual attribute is a bullet point under that heading

This keeps the lesson scannable and prevents everything from blending into one flat wall of text.

## Learning Path

### Step 1: HTML Basics (done)
- Lesson 01: HTML boilerplate
- Lesson 02: Headings, paragraphs, lists
- Lesson 03: Links, images, audio, video, and favicons

### Step 2: HTML Structure (done)
- Lesson 04: Text formatting, `<div>`, `<span>`
- Lesson 05: Tables
- Lesson 06: Forms and inputs (text boxes, buttons, checkboxes, dropdowns)
- Lesson 07: Semantic elements (`<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`, etc.)

This project is complete — kept here for reference.

## Project Structure

```
LearningHTML/
├── CLAUDE.md
├── docs/                  (lesson docs)
├── index.html
├── *.html                 (other practice files)
└── assets/
    ├── css/
    ├── images/
    ├── audio/
    ├── video/
    └── fonts/
```

### Rules
- HTML files stay in the project root — not in subfolders
- Static resources go in `assets/` with subfolders for css, images, audio, video, fonts
- File names use kebab-case (lowercase with hyphens)
- Lesson docs go in `docs/` at the project root

## How It Works
- Claude writes a lesson doc in `docs/`
- User reads the lesson, types the code themselves
- User asks Claude to review their work
- Claude gives feedback, answers questions, and adds notes to lesson docs
- Once it works, move on
