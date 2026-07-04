# Lesson 04: Text Formatting, Div, and Span

## What We're Doing
Learn how to format text (bold, italic, highlight, etc.) and use the two most common generic containers: `<div>` and `<span>`.

## Why / Context
So far all your text has been plain. In real pages, you need to bold important words, italicize titles, show deleted text, display code snippets, and more. HTML has tags for all of this.

You'll also meet `<div>` and `<span>` -- two tags that do *nothing* visually on their own. They're generic boxes you can wrap around things. They become useful later when you add CSS, because they give you something to target and style. Almost every website is full of them. If you right-click any webpage and inspect it, you'll see `<div>` tags everywhere -- they're basically the bricks that websites are built out of. But on their own, they're invisible. You'll see why they matter once we get to CSS.

## Concepts

### Bold and Italic
There are two ways to bold and two ways to italicize. They look the same in the browser but mean different things under the hood, and the difference matters more than you might think:

**`<strong>`** -- Bold with meaning. When you wrap text in `<strong>`, you're telling the browser (and screen readers, and search engines) "this text is important." It's not just a visual thing -- a screen reader will actually change its tone of voice when it reads `<strong>` text, so a visually impaired user can hear the emphasis. Think of it like raising your voice when you say something important in conversation.

**`<b>`** -- Bold with no special meaning. The text looks bold, but you're not saying it's important -- you just want the visual style. This is more rare in practice. You might use it for a product name or a lead-in word at the start of a paragraph, where you want a bold look but there's no actual importance or urgency behind it.

**`<em>`** -- Italic with meaning. "Em" stands for "emphasis." When you wrap text in `<em>`, you're saying "stress this word" -- like how you'd lean on a word in speech. "I didn't say *he* stole it" vs. "I didn't say he *stole* it." Screen readers shift their intonation for `<em>` text, which changes the meaning for listeners just like it does for readers.

**`<i>`** -- Italic with no special meaning. Just visually italic. You might use this for a book title, a foreign word, a technical term -- cases where italic is a typographic convention, but you're not actually emphasizing the word.

```html
<p>This is <strong>very important</strong> information.</p>
<p>This is <em>emphasized</em> text.</p>
<p>This is <b>bold but not important</b> text.</p>
<p>This is <i>italic but not emphasized</i> text.</p>
```

In practice, use `<strong>` and `<em>` most of the time. The rule of thumb: if you'd stress the word out loud, use the semantic tag. If it's purely a visual/typographic choice, use `<b>` or `<i>`. When in doubt, go with `<strong>` and `<em>` -- you almost never go wrong picking the meaningful version.

### Other Text Formatting Tags

**`<mark>`** -- Highlighted text. The browser gives it a yellow background by default, like someone took a highlighter to it. This is meant for text that's relevant in context -- for example, if someone searched for "HTML" on your page, you might `<mark>` every occurrence of "HTML" in the results to show what matched. It's not meant for general decoration, but for drawing attention to something contextually important.
```html
<p>Don't forget to <mark>bring your laptop</mark> tomorrow.</p>
```

**`<small>`** -- Smaller text. This is meant for "side comments" and fine print -- things like disclaimers, copyright notices, legal text, or attribution lines. The browser renders it in a smaller font size. You might wonder: is there a `<big>` tag? There was, but it was removed in HTML5 because "big" doesn't have a clear semantic meaning the way "small/fine print" does. If you want to make text bigger, you'll use CSS later with `font-size` -- that gives you precise control over exactly how big you want it.
```html
<p><small>Terms and conditions apply.</small></p>
```

**`<u>`** -- Underlined text. This one is tricky and worth being careful with. Technically, the HTML spec says `<u>` is for "unarticulated annotation" -- things like marking a misspelled word in a text, or proper names in Chinese text. The reason to be cautious is that on the web, underlined text almost universally looks like a clickable link. If you underline a random word, users will try to click it and get confused when nothing happens. In most real projects, developers avoid `<u>` and use CSS (`text-decoration: underline`) when they actually need an underline, because they can control exactly when and where it appears. But it works fine for learning purposes right now.
```html
<p>This is <u>underlined</u> text.</p>
```

**`<del>`** -- Deleted or struck-through text. The browser draws a line through the middle of the text, like crossing something out on paper. This tells the reader "this content used to be here but has been removed or is no longer accurate."

**`<ins>`** -- Inserted text. The browser underlines it by default, signaling "this content was added." It's the counterpart to `<del>`, and they're often used together -- for example, to show a price change where the old price is crossed out and the new price is shown as an insertion. Think of it like track changes in a Word document.
```html
<p>The price is <del>$50</del> <ins>$30</ins></p>
```

**`<sub>`** -- Subscript. The text shrinks and drops below the normal line of text. This is mainly used for chemical formulas (like H2O) and mathematical notation. Without `<sub>`, you'd just have "H2O" which doesn't look right -- with it, you get the "2" sitting below the H and O where it belongs.

**`<sup>`** -- Superscript. The opposite of subscript -- the text shrinks and floats above the normal line. You see this in exponents (like E = mc2 or x2), footnote markers, and ordinal numbers (like 1st, 2nd, 3rd). It's one of those tags that seems small but makes a big difference in how professional your text looks.
```html
<p>Water is H<sub>2</sub>O</p>
<p>E = mc<sup>2</sup></p>
```

**`<code>`** -- Inline code. The browser renders this in a monospace font (a font where every character is the same width, like what you see in a code editor). Use it when you're mentioning a snippet of code, a tag name, a function name, a variable, or a terminal command inside a regular sentence. It visually sets the code apart from the surrounding prose so the reader immediately knows "this is code, not regular English." You've already seen this exact pattern in this lesson doc -- every time you see something like `<strong>` rendered in that little code-style box, that's what `<code>` does in HTML.
```html
<p>Use the <code>&lt;img&gt;</code> tag for images.</p>
```

**`<pre>`** -- Preformatted text. Normally, HTML collapses all whitespace. If you type five spaces in your HTML, the browser shows one. If you press Enter three times, the browser ignores all of them. `<pre>` turns that off -- it preserves every space, tab, and line break exactly as you typed them. This is essential for displaying code blocks, ASCII art, or anything where the spacing matters. You almost always see `<pre>` and `<code>` used together: `<pre>` preserves the formatting, and `<code>` tells the browser "this is code" and applies the monospace font.
```html
<pre><code>function hello() {
    console.log("hi");
}</code></pre>
```

**`<blockquote>`** -- A block-level quote. When you want to quote someone or pull a passage from another source, you wrap it in `<blockquote>`. The browser indents the entire block from the left margin, which visually sets it apart from your own writing -- like how a quoted passage looks in a book or an article. It's a block-level element, meaning it takes up its own space (it doesn't sit inline with a sentence). If you need a short inline quote within a sentence, there's also a `<q>` tag, but `<blockquote>` is far more common.
```html
<blockquote>
    <p>The best way to learn is to do.</p>
</blockquote>
```

Up to this point in the lesson, you've been using tags that stand on their own with no extra configuration — `<strong>`, `<em>`, `<mark>`, etc. But `<abbr>` brings back something you first learned in Lesson 03: **attributes**. Quick refresher: attributes are the `key="value"` pairs you write inside a tag's angle brackets that give the browser extra instructions about how the element should behave. You've already used `href` on links and `src` on images — those were attributes too. Now you'll see a new one: `title`.

**`<abbr>`** -- Abbreviation. This one is neat. You wrap an abbreviation in `<abbr>` and give it a `title` **attribute** with the full expanded text. When a user hovers over the abbreviation, they see the full text as a tooltip. But it's more than a tooltip -- it's semantic. Screen readers can announce "HTML, abbreviation, HyperText Markup Language," which helps visually impaired users understand what the abbreviation means without having to guess. A generic tooltip is just visual; `<abbr>` carries actual meaning, like the difference between `<strong>` and `<b>`.
```html
<p>I love writing <abbr title="HyperText Markup Language">HTML</abbr>.</p>
```

You can actually add a tooltip to *any* element using the `title` attribute:
```html
<p title="This is a tooltip">Hover over me</p>
```
This works on any tag, but it's not considered truly accessible -- screen readers handle the `title` attribute inconsistently, and on touchscreens there's no "hover" at all, so mobile users never see it. Real tooltips on production websites are usually built with CSS and JavaScript for better control and accessibility. But for learning purposes, `title` is a quick way to see how attributes can add behavior to elements.

### Div and Span

These two tags are generic containers. They have **no visual effect** on their own -- if you add a `<div>` or `<span>` to your page and refresh, you won't see any change. Their purpose is grouping, and they only become visually meaningful when you attach CSS styles to them.

Think of it this way: semantic tags like `<header>`, `<nav>`, and `<section>` are like labeled boxes -- "this box is a header," "this box is navigation." But sometimes you need a plain, unlabeled box just to group things together or to give CSS something to target. That's what `<div>` and `<span>` are -- generic, unlabeled boxes.

**`<div>`** -- A block-level container. "Block-level" means it takes up the full width of its parent and starts on a new line, like how paragraphs and headings behave. You use `<div>` to group sections of content together -- maybe you want a blue background behind three paragraphs, or you want to center a whole chunk of the page. You wrap those elements in a `<div>`, and then later in CSS you style that `<div>`. Without `<div>`, you'd have no way to say "treat these five elements as one group." It's the most-used HTML tag on the internet by a huge margin.
```html
<div>
    <h2>A Section</h2>
    <p>Some content inside a div.</p>
</div>

<div>
    <h2>Another Section</h2>
    <p>More content in a separate div.</p>
</div>
```

**`<span>`** -- An inline container. "Inline" means it stays within the flow of text, like `<strong>` or `<em>`. It doesn't start a new line or take up extra width -- it wraps snugly around whatever text is inside it. You use `<span>` when you want to target a specific word or phrase within a paragraph. For example, if you want to make one word in a sentence red, you can't wrap it in a `<div>` (that would break it onto its own line). Instead, you wrap it in a `<span>` and style the span.
```html
<p>My favorite color is <span>blue</span>.</p>
```

Right now these look pointless -- the page looks exactly the same with or without them. But when you learn CSS, you'll do things like:
```html
<div style="background-color: lightblue;">
    <p>This whole box has a blue background.</p>
</div>

<p>My favorite color is <span style="color: blue;">blue</span>.</p>
```

The key difference:
- **`<div>`** = block (takes full width, starts a new line) -- use it to group chunks of content
- **`<span>`** = inline (stays in the flow of text) -- use it to target a piece of text within a line

A good analogy: `<div>` is like a cardboard box you put things in. `<span>` is like a highlighter -- it wraps around text without moving it anywhere.

### Anchor Links (id attribute)
You asked about the `#` links in your nav -- here's how they work. Any element can have an `id` attribute, which gives it a unique name on the page. Think of it like putting a flag or a bookmark on that element so you can point to it from somewhere else.

```html
<h2 id="about">About</h2>
```

Then you can link to it with `#`:
```html
<a href="#about">Jump to About</a>
```

Clicking that link scrolls the page down (or up) to the element with `id="about"`. The `#` symbol means "look on this page" instead of going to a different URL. So `href="about.html"` would navigate to a different file, but `href="#about"` stays on the current page and just jumps to the element with that id. This is how "table of contents" links work on long pages -- each section has an `id`, and the links at the top use `#` to jump to them.

One important rule: every `id` on a page must be unique. You can't have two elements with `id="about"` -- the browser wouldn't know which one to jump to. If you need to label multiple elements the same way, that's what CSS classes are for (we'll get to those later).

## Your Task

Use your `index.html` (the fresh one). Inside the `<body>`:

1. Add a heading and a paragraph that uses `<strong>` and `<em>`
2. Try `<mark>` to highlight a word
3. Write a fake price using `<del>` and `<ins>` (like a sale)
4. Write "H2O" properly using `<sub>`, and "x squared" using `<sup>`
5. Show an inline code example with `<code>`
6. Add a `<blockquote>` with a quote you like
7. Create two `<div>` blocks, each with a heading and paragraph inside
8. Use `<span>` inside a paragraph to wrap a word (it won't look different yet -- that's expected)
9. Add `id` attributes to your sections and create anchor links that jump to them

Save and refresh after each one. Let me know when you want a review.
