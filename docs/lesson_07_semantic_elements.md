# Lesson 07: Semantic Elements

## What We're Doing
Giving your page real structure using semantic HTML tags.

## Why / Context
Right now your page is just headings, paragraphs, lists, links, and images all dumped into `<body>`. It works, but it's like writing an essay with no chapters or sections — the browser and screen readers have no idea which part is the navigation, which part is the main content, or where the footer is.

Think of it this way: if you printed out a webpage and handed it to someone, they could probably figure out that the links at the top are navigation and the small text at the bottom is a footer. But a browser can't "look" at a page the way a person can. It just sees a flat list of elements. Semantic elements are how you give the browser (and assistive technologies like screen readers) the same understanding a human would get at a glance.

Semantic elements fix that. They work exactly like `<div>` (a generic container) but they have **meaning**. A `<nav>` tells the browser "this is navigation." A `<footer>` says "this is the bottom stuff." The page looks the same visually, but the structure underneath is proper. Search engines also use this structure to understand your page better, which is why semantic HTML matters for SEO (search engine optimization) too.

## Concepts

### The Page Structure Tags
These are the big ones that define the layout of almost every website:

**`<header>`** — This is the introductory area at the top of a page (or at the top of a section). On most websites, the header is where you'll find the site logo, the site title, and the main navigation links. It's the first thing visitors see and it sets the tone for the whole page. You can actually have more than one `<header>` on a page — for instance, each `<article>` could have its own `<header>` — but the most common use is a single one at the top of `<body>` that acts as the page-wide header.
```html
<header>
    <h1>My Website</h1>
</header>
```

**`<nav>`** — This tells the browser "everything inside here is a group of navigation links." You typically put it inside the `<header>`, but it doesn't have to live there — some sites have a sidebar nav or a footer nav. The important thing is that `<nav>` signals intent: these aren't just random links scattered in a paragraph, these are the links that help people move around your site. Screen readers can use this to let users jump straight to the navigation, which is a big deal for accessibility. You don't need to wrap every single link on the page in a `<nav>` — just the main navigation blocks.
```html
<nav>
    <a href="#about">About</a>
    <a href="#projects">Projects</a>
    <a href="#contact">Contact</a>
</nav>
```

**`<main>`** — This wraps the primary content of the page — the reason the page exists. Everything that's unique to this particular page goes in `<main>`. The header, footer, and sidebar are usually shared across all pages of a site, so they stay outside `<main>`. There should only be **one** `<main>` per page, because a page only has one primary purpose. Think of `<main>` as saying "skip past the navigation and boilerplate — HERE is what this page is actually about."
```html
<main>
    <p>This is the important stuff.</p>
</main>
```

**`<section>`** — A thematic chunk of content, usually with its own heading. If your page has an "About Me" area and a "Projects" area, each of those is a `<section>`. The key idea is that a `<section>` groups related content together under a common theme. A good rule of thumb: if the content would get its own heading in an outline, it probably deserves a `<section>`. Don't use `<section>` as a generic wrapper the way you'd use `<div>` — it should always represent a meaningful grouping.
```html
<section>
    <h2>About Me</h2>
    <p>I like cats and HTML.</p>
</section>
```

**`<article>`** — Self-contained content that could stand on its own, even if you ripped it out of the page and put it somewhere else. A blog post is the classic example — it has a title, an author, a date, and a body, and it makes sense all by itself. News stories, forum posts, user comments, and product cards are all good candidates for `<article>`. The difference between `<article>` and `<section>` can feel blurry at first: think of `<article>` as "this is a complete, independent piece of content" and `<section>` as "this is a chunk of a larger whole." An `<article>` can contain `<section>`s inside it, and a `<section>` can contain multiple `<article>`s — they nest however makes sense for your content.
```html
<article>
    <h2>Why Cats Are Great</h2>
    <p>They just are.</p>
</article>
```

**`<aside>`** — Content that is related to the stuff around it but isn't part of the main flow. Think of it like a sidebar in a magazine article, or a "Did you know?" box. It might contain related links, a glossary term, a fun fact, or an author bio. If you removed the `<aside>`, the main content would still make complete sense on its own — the aside is supplementary. On many websites, `<aside>` is styled as a literal sidebar, but it doesn't have to be. It's about the relationship of the content, not the visual position.
```html
<aside>
    <p>Fun fact: cats sleep 16 hours a day.</p>
</aside>
```

**`<footer>`** — The bottom of a page or section. This is where you put the stuff that wraps things up: copyright notices, "built by" credits, links to privacy policies, contact information, or social media icons. Just like `<header>`, you can have more than one `<footer>` — each `<article>` or `<section>` could technically have its own footer — but the most common pattern is a single page-wide footer at the bottom of `<body>`. It's the "fine print" area of your site.
```html
<footer>
    <p>Made by me, 2026</p>
</footer>
```

### Content Tags You'll Use Often

**`<figure>` and `<figcaption>`** — When you put an image on a page, it's just floating there — the browser doesn't know if there's a caption that goes with it or what the image is illustrating. `<figure>` solves that by creating a self-contained unit that groups an image (or a diagram, a code snippet, or even a video) with its caption. The `<figcaption>` inside it is the caption text. This pairing tells the browser "this image and this caption belong together." It's similar to how figures work in textbooks or research papers — the figure is a labeled, referenced unit, not just a picture dropped into a paragraph. Screen readers benefit from this too, because they can announce the caption alongside the image.
```html
<figure>
    <img src="cat.png" alt="A cat" height="300">
    <figcaption>My cat being adorable</figcaption>
</figure>
```

**`<blockquote>`** — A block-level quote from another source. If you're quoting someone or citing a passage from another website, `<blockquote>` is the right tag. Browsers typically indent it by default, which gives it that "quoted" look, but the real purpose is semantic: you're telling the browser "these aren't my words, I'm quoting something." This matters for accessibility and for tools that analyze page content. For short inline quotes within a sentence, there's also `<q>`, but `<blockquote>` is for the bigger standalone quotes.
```html
<blockquote>
    <p>The only way to learn HTML is to type it yourself.</p>
</blockquote>
```

**`<code>` and `<pre>`** — These two often work together. `<code>` marks a piece of text as computer code — it's an inline element, so you can use it inside a paragraph to highlight a tag name or a variable. Browsers typically render it in a monospace font (like Courier) so it looks like code. `<pre>` stands for "preformatted text" — it preserves all your whitespace, indentation, and line breaks exactly as you typed them, instead of collapsing them the way HTML normally does. When you want to show a multi-line code block, you wrap the code in both: `<pre>` handles the formatting, and `<code>` communicates that it's code. Used separately, `<code>` is great for inline mentions like "use the `<img>` tag," while `<pre>` is useful anytime you need whitespace preserved, even for non-code content like ASCII art.
```html
<p>Use the <code>&lt;img&gt;</code> tag for images.</p>

<pre><code>&lt;img src="cat.png" alt="A cat"&gt;</code></pre>
```

**`<details>` and `<summary>`** — A collapsible section, and one of the coolest things in HTML because it gives you interactivity with zero CSS or JavaScript. The `<summary>` is the clickable label that's always visible, and everything else inside `<details>` is hidden until the user clicks to expand it. It's perfect for FAQs, spoiler text, optional extra info, or anything where you want to keep the page clean but still make content available. Try this one out in your browser — click the summary line, and the hidden content slides open. It's genuinely fun to see HTML do something interactive all on its own.
```html
<details>
    <summary>Click to reveal a secret</summary>
    <p>Cats are actually tiny lions.</p>
</details>
```

**`<strong>`** — This makes text **bold**, but it's not just about appearance — it carries meaning. Using `<strong>` tells the browser and screen readers "this text is important, it has strong significance." Screen readers may even change their tone of voice for `<strong>` text. You might have seen `<b>` used for bold text — that's purely visual. `<b>` says "make this look bold" but doesn't signal any importance. It's the same distinction as wearing a bright red sign that says "DANGER" versus just painting something red because it looks nice. In practice, they look identical on screen, but `<strong>` is the right choice when the text actually matters more than the text around it.

**`<em>`** — This makes text *italic*, and like `<strong>`, it carries meaning — specifically, emphasis. When you `<em>`phasize a word, you're telling the browser "if someone were reading this out loud, they'd stress this word." Screen readers actually do change their inflection for `<em>` text. Compare that to `<i>`, which is visual-only italic with no implied emphasis. Use `<em>` when you mean "this word matters in this sentence" and `<i>` for things like book titles or foreign words where italic is just a typographic convention, not a cue to stress the word.

```html
<p>This is <strong>very important</strong> and this is <em>emphasized</em>.</p>
```

**`<time>`** — This wraps a date or time and gives it a machine-readable format via the `datetime` attribute. To a human, "February 1, 2026" and "2/1/26" and "1st of Feb '26" all mean the same thing, but computers can't reliably parse all those formats. The `datetime` attribute uses a standardized format (like `2026-02-01`) so that browsers, search engines, and other tools can reliably understand the date. You might see this used on blog posts for the publish date, on event pages for event times, or anywhere a date appears. The text between the tags can be whatever human-friendly format you prefer — it's the `datetime` attribute that matters for machines.
```html
<p>Published on <time datetime="2026-02-01">February 1, 2026</time></p>
```

### How a Typical Page Looks

Here's how all these structural elements come together on a real page. Notice the pattern: `<header>` at the top with the site title and `<nav>`, then `<main>` wrapping the actual content (broken into `<section>`s), and `<footer>` at the bottom. This is the skeleton of almost every website you visit — once you start looking for this pattern, you'll see it everywhere.

```html
<body>
    <header>
        <h1>My Site</h1>
        <nav>
            <a href="#about">About</a>
            <a href="#contact">Contact</a>
        </nav>
    </header>

    <main>
        <section>
            <h2>About</h2>
            <p>Hello world.</p>
        </section>

        <section>
            <h2>Contact</h2>
            <p>Email me.</p>
        </section>
    </main>

    <footer>
        <p>Copyright 2026</p>
    </footer>
</body>
```

## Your Task

Restructure your `index.html` using semantic elements:

1. Wrap your `<h1>` in a `<header>` tag
2. Wrap everything between the header and the end in a `<main>` tag
3. Turn each `<h2>` section (Headers, Paragraphs, Lists, Links, Images) into a `<section>`
4. Add a `<footer>` at the bottom with your name and the year
5. Pick at least one image and wrap it in a `<figure>` with a `<figcaption>`
6. Add a `<details>`/`<summary>` somewhere — it's fun, try it
7. Try using `<strong>` and `<em>` in one of your paragraphs

Don't worry about making it look different — it'll look almost the same. The point is the structure underneath. Open your page in the browser after each change to make sure nothing breaks.
