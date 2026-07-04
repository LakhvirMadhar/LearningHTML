# Lesson 03: Links, Images, Audio, Video, and Favicons

## What We're Doing
Add links, images, audio, video, and a favicon to your page.

## Why This Matters
So far your page is just text — headings, paragraphs, and lists. It works, but it's like a book with no pictures, no references, and no connections to anything else. Links are what make the web a *web* — they're the threads that connect pages together, letting users jump from one place to another. Without links, every page would be a dead end. Images make pages visual and engaging — try to think of a single website you use that doesn't have at least one image on it. These two elements, along with media like audio and video, are foundational to almost everything you see on the internet.

## What Are Attributes?
This lesson introduces a bunch of new tags, and almost all of them use **attributes** — so it's worth pausing here because they'll come up constantly from now on. Think of attributes like extra instructions you're giving to a tag. The tag itself says *what* the element is, and the attribute adds details about *how* it should behave or what it should contain.

The general pattern looks like this:

```html
<tag attribute="value">content</tag>
```

It always goes inside the opening tag (never the closing tag), and it's always in the format `name="value"`. Some tags have required attributes (like `href` on a link — a link without an `href` doesn't go anywhere), while others are optional. You'll see attributes on almost every tag from here on out. `href` is just the first of many.

## Links

### Tag: `<a>`

Links use the `<a>` tag (short for "anchor"). The name comes from the early days of the web — the idea was that a link "anchors" one document to another, creating a connection between them. The text between `<a>` and `</a>` is what the user actually sees and clicks on. The browser will style it as blue underlined text by default, signaling to the user "hey, this is clickable."

```html
<a href="https://www.google.com" target="_blank">Click here to go to Google</a>
```

#### Attributes:

- **`href`** — stands for "hypertext reference," which is a fancy way of saying "the address this link points to." The browser knows you want a link (because you used `<a>`), but it has no idea *where* to send the user unless you tell it — that's what `href` does. The URL goes inside the quotes after `href=`. This can be a full web address like `https://www.google.com`, or it can be a relative path to another file in your project (more on that later).

- **`target`** — controls where the link opens. By default, clicking a link replaces your current page — the user navigates away and your page is gone. Sometimes that's fine, but other times (especially when linking to an external website), you'd rather keep your page open and let the link open in a new tab. Setting `target="_blank"` tells the browser "open this in a blank, new tab." The underscore is just part of the syntax — don't worry about why it's there, just know that `target="_blank"` is the magic phrase for "new tab." You'll see this used all the time on real websites, especially for external links where the site doesn't want you to leave entirely.

## Images

### Tag: `<img>`

Images use the `<img>` tag. This tag works differently from what you've seen so far — it has no closing tag. It's one of the few "self-closing" or "void" tags in HTML. There's no `</img>`. Why? Because there's no "content" to put between an opening and closing tag. A paragraph wraps around text. A link wraps around clickable text. But an image doesn't wrap around anything — it *is* the content. So HTML just uses a single tag.

```html
<img src="cat.jpg" alt="A photo of a cat" width="300">
```

#### Attributes:

- **`src`** — the source attribute. It tells the browser where to find the image file. This can be a filename in your project folder (like `"cat.jpg"`) or a full URL to an image on the internet (like `"https://example.com/photo.jpg"`). Think of it like giving someone directions to a photo — you're saying "go here to get the picture." The name `src` is short for **s**ou**rc**e.

- **`alt`** — the alternative text. This serves two important purposes. First, if the image fails to load for any reason (broken link, slow internet, the file got deleted), the browser will display this text instead so the user at least knows what was supposed to be there. Second, and arguably more importantly, screen readers (software used by visually impaired users) read this text out loud to describe the image. Writing good `alt` text is a real skill — you want to describe what the image actually shows, not just say "image" or "photo." For example, `alt="A tabby cat sleeping on a red couch"` is much more helpful than `alt="cat"`.

- **`width`** / **`height`** — control the display size in pixels. A pixel is a single dot on your screen — 300 pixels wide is roughly a third of a typical laptop screen, though it varies by screen size and resolution. Images display at their full, original size by default, which can be a problem — a photo from your phone might be 4000 pixels wide, which is way wider than your browser window. You can set just `width` and let the browser figure out the height automatically to keep the image's original proportions (so it doesn't look stretched or squished) — that's usually the better approach. Later when you learn CSS, you'll have even more control over image sizing, but these HTML attributes work perfectly fine for now.

### Where Do I Get an Image?
You have three options:
1. **Save a file locally** — find any image online or on your computer, save it into your `LearningHTML` folder (the same folder where `index.html` lives), and reference it by its filename: `src="myimage.jpg"`. This is the most reliable approach because the image is right there with your code — no internet connection needed, no risk of the image disappearing from some other website.
2. **Copy an image URL** — right-click any image on the web, choose "Copy image address" (the exact wording varies by browser), and paste that full URL as your `src`: `src="https://example.com/photo.jpg"`. This is quick and easy, but the image could disappear if the website takes it down or changes the URL.
3. **Use a placeholder service** — `src="https://placehold.co/300x200"` gives you a simple grey box with the dimensions written on it. This is useful when you're working on layout and you just need *something* in the image spot without caring what it looks like. Developers use placeholder images all the time during development.

Option 1 (local file) is the most reliable since it doesn't depend on an external website staying online or keeping the image at the same URL.

### Local vs Online Images
This is a distinction that trips people up at first, so let's be clear about it:

- **Online:** `src="https://some-website.com/photo.jpg"` — the browser goes out to the internet and fetches the image from that web address every time someone loads your page. If the website is down or the image is removed, your page shows a broken image icon.
- **Local:** `src="photo.jpg"` — the browser looks for a file called `photo.jpg` in the same folder as your HTML file. No internet needed. The file just has to be there.

The browser decides which one you mean based on whether the `src` starts with `http://` or `https://`. If it does, the browser treats it as a web address. If it doesn't, the browser assumes it's a local file path relative to your HTML file.

## Audio

### Tag: `<audio>`

Audio uses the `<audio>` tag. The concept is similar to `<img>` — you point it at a file — but there are some differences because audio is interactive. The user needs to be able to play, pause, and adjust the volume, so you need to tell the browser to show those controls.

```html
<audio controls>
    <source src="song.mp3" type="audio/mp3">
    Your browser does not support the audio element.
</audio>
```

The text "Your browser does not support the audio element." is a fallback message that only shows up if the browser is so old it doesn't understand the `<audio>` tag at all. This is pretty rare these days (all modern browsers support it), but it's good practice to include it just in case. Common audio formats: `.mp3` (the most universally supported), `.wav` (uncompressed, high quality but large files), and `.ogg` (open-source format, well-supported in most browsers).

#### Attributes:

- **`controls`** — this is an attribute with no value, which is new. Unlike `href="..."` or `src="..."` where you assign a value, `controls` works just by being present. Its mere existence on the tag tells the browser "show the play/pause button, volume slider, and progress bar." If you leave out `controls`, the audio element is completely invisible on the page — the audio is technically there, but the user has no way to interact with it. These are sometimes called "boolean attributes" because they're either there or they're not, like a light switch.

- **`autoplay`** — starts playing automatically. Browsers often block this unless `muted` is also set, to prevent websites from blasting sound at you the moment the page loads.

- **`loop`** — repeats the audio when it reaches the end.

- **`muted`** — starts the audio muted.

```html
<audio controls autoplay loop muted>
    <source src="song.mp3" type="audio/mp3">
</audio>
```

### Tag: `<source>`

You might wonder why the audio file isn't just an attribute on `<audio>` itself (like `src` on `<img>`). The reason is that `<source>` is its own tag that goes *inside* `<audio>`, and you can include multiple `<source>` tags with different file formats as fallbacks — if the browser can't play `.mp3`, it'll try the next `<source>`, and so on.

```html
<source src="song.mp3" type="audio/mp3">
```

#### Attributes:

- **`src`** — the path to the audio file, just like `src` on an image.

- **`type`** — tells the browser what format the file is (like `audio/mp3` or `audio/ogg`). This helps the browser quickly figure out which format each source is without having to download the file first.

### Where to get an audio file?
Save any `.mp3` file into your project folder, same as you did with images. Or search for "free mp3 samples" online.

## Video

### Tag: `<video>`

Video works almost exactly like audio, just with `<video>` instead. It has the same `controls`, `autoplay`, `loop`, and `muted` attributes, plus a few extras. Common video formats: `.mp4`, `.webm`, `.ogg`. You can also use a URL instead of a local file for the `src`.

```html
<video controls width="400">
    <source src="clip.mp4" type="video/mp4">
    Your browser does not support the video element.
</video>
```

#### Attributes:

- **`controls`** / **`autoplay`** / **`loop`** / **`muted`** — same behavior as on `<audio>`.

- **`width`** — you'll want to set this (like images) so the video doesn't take over the whole page.

- **`poster`** — shows a preview image before the video plays. Set it to the path of an image file:

```html
<video controls width="400" poster="thumbnail.jpg">
    <source src="clip.mp4" type="video/mp4">
</video>
```

### Tag: `<track>`

You can add subtitles to a video using the `<track>` tag inside `<video>`:

```html
<video controls width="400">
    <source src="clip.mp4" type="video/mp4">
    <track src="subtitles.vtt" kind="subtitles" srclang="en" label="English">
</video>
```

#### Attributes:

- **`src`** — the path to the subtitle file (a `.vtt` WebVTT file).

- **`kind`** — what type of text track this is (usually `"subtitles"`).

- **`srclang`** — the language of the subtitles (like `"en"` for English).

- **`label`** — the name shown to the user in the subtitle menu (like `"English"`).

The subtitle file is a `.vtt` (WebVTT) file — just a plain text file with timestamps. Create one in your text editor and save it as `.vtt`:

```
WEBVTT

00:00:01.000 --> 00:00:04.000
Hello, welcome to my video.

00:00:05.000 --> 00:00:08.000
This is the second subtitle.
```

The timestamps tell the browser when to show each line. The user can toggle subtitles on/off using the CC button in the video player.

### Embedding YouTube videos
Instead of hosting your own video file, you can embed a YouTube video using `<iframe>`. On any YouTube video, click **Share** → **Embed**, and you'll get code like this:

```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/VIDEO_ID" frameborder="0" allowfullscreen></iframe>
```

Replace `VIDEO_ID` with the part after `v=` in the YouTube URL. For example, if the URL is `https://www.youtube.com/watch?v=dQw4w9WgXcQ`, the embed URL is `https://www.youtube.com/embed/dQw4w9WgXcQ`.

### Tag: `<iframe>`

An `<iframe>` is basically a window into another webpage, inside your webpage. Think of it as a picture frame on your wall, but instead of a photo, it's showing a live website. Your page literally loads that URL inside the box. The user can scroll, click links, and interact with it — all within that rectangle on your page.

```html
<iframe src="https://www.example.com" width="600" height="400"></iframe>
```

Common uses:
- **YouTube embeds** — the video player you see on other sites is YouTube's page in an iframe
- **Google Maps** — when a website shows an embedded map, that's usually an iframe
- **Payment forms** — sites like Stripe load their credit card form in an iframe for security
- **Any external widget** — comment sections, booking tools, etc.

#### Attributes:

- **`src`** — the URL of the page to load.

- **`width`** / **`height`** — size of the frame.

- **`allowfullscreen`** — lets embedded content (like video) go fullscreen.

- **`frameborder`** — `frameborder="0"` removes the border around the frame. This is an old attribute — CSS is better for this now.

Note: some websites block being loaded in iframes for security reasons, so not every URL will work. Services like YouTube specifically provide embed URLs that are designed to work in iframes.

## Favicons

A favicon is the small icon that appears in the browser tab next to your page title. You've seen them everywhere — Google's "G", YouTube's play button, etc.

### Tag: `<link>`

To add a favicon, put an image file (`.ico`, `.png`, or `.svg`) in your project folder and add a `<link>` tag inside your `<head>` (not `<body>`). The `<link>` tag is a self-closing tag that connects your page to an external resource.

```html
<head>
    <title>My Page</title>
    <link rel="icon" href="favicon.ico" type="image/x-icon">
</head>
```

#### Attributes:

- **`rel`** — stands for "relationship." It tells the browser what this linked resource is for. `rel="icon"` means it's a favicon.

- **`href`** — points to the image file, just like `href` on a link.

- **`type`** — the file format. Use `image/x-icon` for `.ico` files, or `image/png` for `.png`:

```html
<link rel="icon" href="favicon.png" type="image/png">
```

### Where to get a favicon?
Search for "favicon generator" — there are free sites where you upload any image and it converts it to the right size (16x16 or 32x32 pixels). Or just use any small `.png` file you have.

## Your Task
You've already done links and images in your `practice.html`. Now add audio, video, and a favicon to your `index.html`:

1. Find or download an `.mp3` file and save it in your project folder
2. Add an `<audio>` tag with `controls` to your page
3. Find or download a short `.mp4` file and save it in your project folder
4. Add a `<video>` tag with `controls` and a `width`
5. Find or create a small image for a favicon
6. Add a `<link rel="icon">` inside your `<head>`
7. Check the browser tab — you should see your favicon next to the page title

Save and refresh after each step. Let me know when you want a review.
