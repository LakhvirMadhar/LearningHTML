# Lesson 01: HTML Boilerplate

## What We're Doing
Create a file called `index.html` and write the basic HTML skeleton that every web page needs.

## What is HTML?
HTML stands for HyperText Markup Language. It's the language you use to structure a web page — to tell the browser what each piece of content *is*. Is this chunk of text a heading? A paragraph? A link? A list of items? HTML is how you answer those questions.

The key word here is **markup**. You're not programming logic or calculations — you're *marking up* content with meaning. Think of it like an editor going through a manuscript with a red pen: "this is a title," "this is a footnote," "this is a quote." HTML does the same thing, except instead of a red pen, you use **tags** (more on those in a moment).

The browser reads your HTML and uses it to decide how to display things. A heading gets big bold text. A paragraph gets normal-sized text with some spacing. A list gets bullet points. You're not telling the browser *how* things should look (that's CSS's job, which we'll get to later) — you're telling it *what* things are, and the browser applies its default styling from there.

## Why `index.html`?
`index.html` is a naming convention from web servers. When you visit a website like `example.com/about/`, the server automatically looks for a file called `index.html` inside that folder and serves it. It's the **default page** of any directory.

- `example.com/` serves `index.html` from the root folder
- `example.com/about/` serves `about/index.html`

For what you're doing right now (opening files locally in a browser), the name doesn't matter — you could call it `banana.html` and it would work fine. But `index.html` is the standard name for a site's main/home page, so it's a good habit.

## Tags
Tags are the fundamental building blocks of HTML. They're how you wrap content to give it meaning. A tag is a keyword surrounded by angle brackets, like `<body>` or `<title>`.

Most tags come in pairs — an **opening tag** and a **closing tag** — and your content goes in between:
- **Opening tag:** `<body>`
- **Closing tag:** `</body>` (note the forward slash `/` before the name — that's what makes it a closing tag)

So if you write `<p>Hello there</p>`, you're saying: "Everything between `<p>` and `</p>` is a paragraph." The browser sees that and knows to treat "Hello there" as a paragraph — it'll put some vertical spacing around it, display it as a block of text, and so on.

The opening and closing tags act like bookends. The opening tag says "this type of content starts here," and the closing tag says "it ends here." Forgetting the closing tag is like leaving a parenthesis open in a sentence — things can get confusing fast, and the browser has to guess where you meant to stop. Sometimes it guesses right. Sometimes it doesn't.

There are a few tags that don't have a closing pair (called **void elements** or **self-closing tags**) — things like `<br>` for a line break or `<img>` for an image. You'll meet those later. For now, just remember: most tags come in pairs, and you need to close what you open.

## The Skeleton
Every HTML page needs this basic structure. Think of it like the frame of a house — before you start adding rooms and furniture, you need the foundation, walls, and roof. This skeleton is the foundation. Type this into your `index.html`:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First Page</title>
  </head>
  <body>

  </body>
</html>
```

## What Each Piece Does

### `<!DOCTYPE html>`
This isn't actually an HTML tag — it's a declaration. It tells the browser "this document is HTML5." Without it, browsers may fall back to older, quirkier rendering modes (called "quirks mode") where they try to be backwards-compatible with web pages from the late 1990s. That can cause subtle and confusing differences in how your page looks and behaves. Always put it on the very first line. It's one of those things you type once, never think about again, but it matters.

### `<html>`
This wraps your entire page. Everything else goes inside it. Think of it as the outer container that says "HTML starts here, HTML ends here." Every other tag in your document will be nested somewhere inside `<html>`. It's the root of the tree — if your page were a family tree, `<html>` would be the ancestor at the very top.

### `<head>`
The invisible section. Nothing inside `<head>` shows up on the page itself — your visitors will never see it directly. This is the behind-the-scenes area where you put information *about* the page rather than information *on* the page. That includes things like:
- The page title (the text in the browser tab)
- Links to CSS stylesheets (we'll do this later — this is how you make things look nice)
- Metadata (character encoding, a description for search engines, viewport settings for mobile, etc.)

Think of `<head>` as the backstage area of a theater. The audience (your visitors) never sees it, but it's essential for the show to work properly.

### `<meta charset="UTF-8">`
This tells the browser what **character encoding** to use when reading your HTML file. Character encoding is how text is stored as bytes — different encodings represent characters differently, so the browser needs to know which one you used.

UTF-8 is the universal standard that supports virtually every character you'd ever need: letters from any language (English, Chinese, Arabic, Russian — all of them), accented characters (é, ñ, ü, ø), symbols (©, ™, →, ÷), and even emojis (🎉, 😊, 🚀). It's become so dominant that there's really no reason to use anything else.

Without this tag, the browser has to guess the encoding. Sometimes it guesses right, sometimes it doesn't. When it guesses wrong, you get garbled text — things like `Ã©` showing up instead of `é`, or question marks where special characters should be. This is especially common when someone writes a page on one operating system and opens it on another, or when you copy text from other sources. Always include this tag and always put it near the top of your `<head>` — it should come before any text content (including `<title>`) so the browser knows the encoding before it tries to read anything else.

### `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
This tag is critical for **mobile devices** and becomes especially important once you start writing CSS.

Here's the problem it solves: back in the early days of smartphones, most websites were designed only for desktop computers — big screens, around 1000 pixels wide. When phones first got web browsers, they had tiny screens (maybe 320 pixels wide), and these desktop-only sites looked terrible. So mobile browsers came up with a workaround: they'd pretend the screen was ~980 pixels wide, render the whole desktop site at that width, and then shrink it down to fit the phone screen. The result was a tiny, zoomed-out version of the page that you'd have to pinch-to-zoom to actually read.

This was a decent workaround for old sites, but it's a disaster for sites that are actually *designed* for mobile. If you're trying to make a responsive layout that adapts to different screen sizes, you need the browser to tell you the *real* screen width, not a fake 980px.

That's what this viewport tag does:
- **`width=device-width`** — tells the browser to use the actual screen width (e.g., 375px on an iPhone, 412px on a Pixel) instead of pretending it's 980px
- **`initial-scale=1.0`** — sets the initial zoom level to 100% (no zooming in or out)

Without this tag, your CSS media queries won't work properly on mobile, percentage-based widths will behave unexpectedly, and your carefully designed mobile layouts will get squished into a zoomed-out mess. Always include it.

### `<title>`
Goes inside `<head>`. This sets the text that appears in the browser tab — you know, that tiny label at the top of each tab that helps you tell your tabs apart. It's also what shows up when you bookmark the page, and what search engines display as the clickable blue link in search results. So even though it doesn't appear on the page itself, it's one of the most important things for users to find and recognize your page.

### `<body>`
The visible section — this is where everything the user actually sees goes. Text, images, buttons, links, lists, forms, videos — all of it lives inside `<body>`. If you put something outside of `<body>`, it won't show up on the page. When you think "I want to add something to my web page," you're thinking about adding it inside `<body>`.

## Your Task
1. Type the skeleton above into `index.html`
2. Save the file
3. Open it in your browser (double-click the file, or drag it into a browser window)
4. You should see a blank page, but the browser tab should say "My First Page"
5. Once that works, move on to Lesson 02

## Indentation
The browser doesn't care about whitespace — your page will look the same with or without indentation. You could write your entire HTML file on a single line and the browser would render it identically. But **you** should care about indentation, because it makes your code readable to *humans* — including future-you, who will come back to this code in a week and wonder what's going on.

The rule is straightforward: every time you nest a tag inside another tag, indent one level deeper. This way, you can visually see which tags belong inside which other tags, like an outline.

```html
<body>
    <h1>Title</h1>
    <p>Content</p>
</body>
```

Here, `<h1>` and `<p>` are inside `<body>`, so they get one indent. When `<body>` closes, it comes back to the original level. You can immediately see at a glance: "these two elements live inside the body." As nesting gets deeper, keep adding levels:

```html
<body>
    <main>
        <section>
            <h2>Title</h2>
            <p>Content</p>
        </section>
    </main>
</body>
```

Notice how every layer of nesting adds another indent. You can trace the indentation to see the structure: `<h2>` and `<p>` are inside `<section>`, which is inside `<main>`, which is inside `<body>`. It reads like an outline, and when you start building pages with 50+ lines, that visual structure becomes essential for not getting lost.

Whether you use tabs or spaces is personal preference — developers have been arguing about this for decades and will never stop. Just be consistent within a project. Pick one and stick with it.

## Every Page Needs the Skeleton
Every HTML file is its own standalone document. The browser doesn't carry anything over from one page to another — it only reads what's in the file you opened. So every new `.html` file you create needs the full boilerplate (`<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`) all over again.

This might feel repetitive, and it is — but that's by design. Each page is self-contained. The browser doesn't know or care that you have other HTML files in the same folder. It loads one file, reads it top to bottom, and renders what it finds. If the skeleton is missing, the browser will try its best to figure things out, but you're relying on guesswork at that point, and different browsers may guess differently. Always start with the full skeleton.

## Tips
- **Forgetting a closing tag is the #1 beginner mistake.** It's easy to do — you write the opening tag, then you write your content, and then you move on to the next thing and forget to close what you opened. The browser will often try to compensate, but it might close the tag in the wrong place or not at all, leading to layout problems that can be really hard to track down. Build the habit early: as soon as you type an opening tag, immediately type the closing tag, then move your cursor back between them to fill in the content. That way you never forget.
- **View your page source.** Right-click anywhere on your page in the browser and choose "View Page Source" (or press `Ctrl+U`). This shows you the raw HTML exactly as the browser received it. It's a great way to verify that what you typed is what the browser is actually reading. You can also do this on *any* website to see how real sites are built — it's like being able to peek behind the curtain.
