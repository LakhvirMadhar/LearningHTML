# Lesson 02: Headings, Paragraphs, and Lists

## What We're Doing
Add visible content to your page — headings, paragraphs, and lists.

## Where Does This Go?
Everything in this lesson goes inside the `<body>` tags. Now, the browser *will* display plain text even without tags — if you just type "Hello world" inside the body, it shows up. So you might wonder why we bother with tags at all. The reason is that tags tell the browser **what** the content actually is: a heading, a paragraph, a list item. Think of it like this — if you handed someone a printed page with no formatting, no bold titles, no bullet points, just a wall of text, they'd have a hard time figuring out the structure. Tags are how you give that structure to the browser.

This matters even more once you start adding CSS later on. When you want to style your headings differently from your paragraphs, you need the browser to *know* which text is a heading and which is a paragraph. If everything is just plain text floating in the body, you have nothing to grab onto — no way to say "make all the headings blue" or "put extra space between paragraphs." The tags are your handles.

```html
<body>
    <!-- All the stuff below goes in here -->
</body>
```

## Headings
HTML gives you 6 levels of headings, from biggest to smallest:

```html
<h1>Biggest Heading</h1>
<h2>Second Biggest</h2>
<h3>Third</h3>
<h4>Fourth</h4>
<h5>Fifth</h5>
<h6>Smallest Heading</h6>
```

Think of these like an outline for a research paper or a book. The `<h1>` is the title of the whole thing. The `<h2>`s are your major chapters or sections. The `<h3>`s are sub-sections within those chapters, and so on. You probably won't use `<h5>` or `<h6>` very often — most pages don't go that deep — but they're there if you need them.

The convention is **one `<h1>` per page**. After that, use `<h2>` for sections, `<h3>` for sub-sections, and so on. This isn't a hard rule — the browser won't break or throw an error if you use five `<h1>` tags. But it's a strong convention, and here's why:

- **SEO** — Search engines like Google treat `<h1>` as a signal for what the page is *about*. If you have multiple `<h1>` tags, you're essentially telling Google "this page is about five different things equally," which dilutes the signal. One clear `<h1>` helps your page rank for the right topic.
- **Accessibility** — People who use screen readers (software that reads web pages aloud for visually impaired users) rely heavily on headings to navigate. The screen reader can list all the headings on a page like a table of contents, letting the user jump to the section they want. If your heading hierarchy is jumbled — like jumping from `<h1>` straight to `<h4>` — it's like a book where the chapter numbering skips around randomly. One clear `<h1>` followed by logically nested `<h2>`s and `<h3>`s makes the page easy to navigate.
- **Convention** — Most developers structure headings this way, so when someone else reads your code (or when *you* read it six months from now), the structure will be immediately familiar and easy to follow.

One more thing worth knowing: the heading level controls the *semantic meaning*, not just the size. Yes, `<h1>` is visually bigger than `<h2>` by default, but you can change the size of anything with CSS later. The real point is that `<h1>` tells the browser "this is the most important heading on the page." Don't pick a heading level just because you like how big or small it looks — pick it based on where it falls in your content hierarchy, and style it later.

## Paragraphs
The `<p>` tag wraps a paragraph of text. Whenever you have a block of text that represents a distinct thought or section of writing, put it in `<p>` tags:

```html
<p>This is a paragraph. The browser adds spacing above and below it automatically.</p>
<p>This is a second paragraph. Notice they don't smush together.</p>
```

That automatic spacing is important. The browser puts a visible gap between paragraphs so readers can tell where one thought ends and the next begins — just like you'd expect in a book or article. You don't need to add blank lines or extra spaces yourself; the `<p>` tag handles that for you.

Here's something that trips up a lot of beginners: without `<p>` tags, **the browser completely ignores your line breaks**. You might type this in your HTML file:

```
This is line one.
This is line two.
This is line three.
```

And expect three separate lines, right? But the browser will smash it all into one continuous line: "This is line one. This is line two. This is line three." That's because HTML treats any amount of whitespace — line breaks, multiple spaces, tabs — as a single space. The browser doesn't care about how you formatted your source code. It only cares about the tags. So if you want text to appear as separate paragraphs on the page, you *must* wrap each one in `<p>` tags. The tags are the instruction; the whitespace in your source file is just for your own readability.

## Lists
Lists come up all the time in web content — navigation menus, feature lists, recipe steps, to-do items. HTML gives you two main kinds of lists, and they work almost identically except for how the items are marked.

**Unordered list** (bullet points) — Use this when the order doesn't matter. A list of your favorite foods, a set of features, a group of links. The browser will put a bullet point (a small dot by default) next to each item:

```html
<ul>
  <li>First item</li>
  <li>Second item</li>
  <li>Third item</li>
</ul>
```

**Ordered list** (numbered) — Use this when the sequence matters. Step-by-step instructions, a ranking, a top-10 list. The browser will automatically number each item for you — you don't type the numbers yourself, which is nice because if you rearrange items or add one in the middle, the numbers update on their own:

```html
<ol>
  <li>First item</li>
  <li>Second item</li>
  <li>Third item</li>
</ol>
```

Notice the pattern: the outer tag (`<ul>` or `<ol>`) is the *container* that says "this is a list," and the `<li>` tags are the individual items *inside* it. You always need both — an `<li>` floating outside of a `<ul>` or `<ol>` doesn't make sense, and a `<ul>` without any `<li>` items inside is just an empty list.

The tag names are abbreviations, which makes them easier to remember:
- **`<ul>`** = **u**nordered **l**ist — bullets, no particular sequence
- **`<ol>`** = **o**rdered **l**ist — numbered, sequence matters
- **`<li>`** = **l**ist **i**tem — used inside *both* `<ul>` and `<ol>`. The `<li>` tag is the same regardless of which kind of list it's in; it's the outer container that determines whether you get bullets or numbers.

## Your Task
Inside the `<body>` of your `index.html`, replace what you have with:
1. An `<h1>` with your page title
2. A `<p>` with a sentence or two about anything
3. An `<h2>` that says something like "Things I Like"
4. A `<ul>` with at least 3 `<li>` items
5. An `<h2>` that says something like "My Top 3"
6. An `<ol>` with 3 items

Save, refresh your browser, and check it out. Let me know when you're done.
