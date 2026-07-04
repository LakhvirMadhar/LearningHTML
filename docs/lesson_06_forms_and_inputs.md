# Lesson 06: Forms and Inputs

## What We're Doing
Learn how to build forms — text boxes, buttons, checkboxes, radio buttons, dropdowns, and more.

## Why / Context
Forms are how users send data to a website. Every login page, search bar, signup form, checkout page, and comment box is a form. If you think about it, almost every meaningful interaction you have with a website beyond just reading it involves a form of some kind. When you type a search into Google — that's a form with a single text input and a submit button. When you sign up for an account somewhere — that's a form with text fields, maybe a dropdown for your country, and a submit button.

Even if your page doesn't connect to a server yet, learning the HTML for forms is the foundation. The form will look and work visually in your browser — you'll be able to type in fields, check boxes, pick from dropdowns, and click buttons. It just won't actually send the data anywhere until you eventually add a backend (server-side code) later. For now, we're focused purely on the HTML structure.

## Concepts

### The Form Tag
Before we get into the individual inputs, let's set up the container they all live in. All form elements go inside a `<form>` tag. Think of `<form>` as a wrapper, similar to how `<table>` wraps all your rows and cells, or how `<ul>` wraps a list of `<li>` items. The `<form>` tag tells the browser "everything inside here is a group of inputs that belong together."

```html
<form>
    <!-- all your inputs, labels, buttons go here -->
</form>
```

Start your page with this wrapper, and add everything else inside it as you go. You need the `<form>` tag in place for things like email validation and `required` to work — the browser only checks those when you try to submit a form.

Later, when you connect to a real server, `<form>` has two extra attributes: `action` (the URL to send data to) and `method` (how to send it — `GET` or `POST`). You don't need those right now. Live Server in VS Code serves your files so you can view them, but it doesn't process form data — that requires a real backend, which is a TypeScript thing later. For now, clicking submit will just refresh the page, but the browser validation (email checks, `required` fields) will still trigger before the refresh.

### Text Input and Labels
The most common form element is a single-line text box where the user can type freely. These always come in pairs: a label that tells the user what to type, and the input box itself. Here's what the pair looks like together:

```html
<label for="username">Username:</label>
<input type="text" id="username" name="username" placeholder="Enter your name">
```

Let's break this down by tag — first the label, then the input — and look at the **attributes** (those `key="value"` pairs inside the angle brackets) that each one uses.

### Tag: `<label>`

The `<label>` tag is the visible text next to the input — "Username:" in this example. It's not just decoration. A label is connected to its input, which means clicking the label text will automatically focus (put the cursor in) the associated input. Screen readers also use this connection to tell visually impaired users what each input is for — without a proper label, a blind user would just hear "text input" with no idea what to type. Always pair your inputs with labels.

#### Attributes:

- **`for`** — this is the attribute that creates the connection between the label and its input. The value of `for` must match the `id` attribute on the input it belongs to. In the example above, `for="username"` links to `id="username"` on the input. That's how the browser knows which input to focus when you click the label text.

### Tag: `<input>`

The `<input>` tag is a self-closing tag, meaning there's no `</input>`. It works the same way as `<img>` or `<br>` — all the information lives in its attributes rather than between opening and closing tags. Forms are where attributes really take center stage — you'll use more of them per tag here than in any lesson so far.

#### Attributes:

- **`type`** — this is the single most powerful attribute on `<input>` because changing it completely transforms what the input looks like and how it behaves. `type="text"` makes it a plain text box. We'll see many more types below (password, email, number, date, etc.) — all just different values for this one attribute.

- **`id`** — a unique identifier for this specific input on the page. This is what the `<label>`'s `for` attribute points to. Every `id` on a page must be unique — no two elements should share one.

- **`name`** — the key that gets used when data is sent to a server. Think of it like a variable name. If the user types "Bob" into this field, the server receives `username=Bob`. You won't see this in action yet since we have no server, but always include it — it's a good habit, and you'll need it eventually.

- **`placeholder`** — the grey hint text that appears inside the input when it's empty. As soon as the user starts typing, the placeholder disappears. It's meant to give the user a hint about what to enter, like "Enter your name" or "you@example.com". Don't rely on it as a replacement for a label though — placeholders vanish once you type, so if someone forgets what the field was for, they'd have to delete their text to see the hint again.

Try this one first — type it out, open it in the browser, and you should see a text label and a box you can type in. Click the label text and watch the cursor jump into the box. That's the `for`/`id` linkage in action.

### Other Input Types
The `type` attribute changes what the input looks like and how it behaves. This is one of the most interesting parts of HTML forms — you can get a surprising amount of functionality just by changing a single attribute. The browser handles all the visual differences and built-in validation for you.

**`password`** — looks identical to a text box, but everything you type is masked with dots or asterisks. This is purely a visual privacy measure so someone looking over your shoulder can't read your password. Under the hood, the actual text is still there — it's just hidden on screen.
```html
<label for="pw">Password:</label>
<input type="password" id="pw" name="password">
```

**`email`** — at first glance, this looks exactly like a regular text box. But it has a hidden superpower: when the user tries to submit the form, the browser checks whether the value looks like a valid email address (has an `@`, has something after the dot, etc.). If it doesn't, the browser shows a built-in error message and blocks the submission. On mobile phones, this type also changes the keyboard layout to show the `@` symbol more prominently, which is a nice touch.
```html
<label for="email">Email:</label>
<input type="email" id="email" name="email" placeholder="you@example.com">
```

**`number`** — restricts the input to numeric values only. The browser typically adds small up/down arrows (called a "spinner") so users can increment or decrement the value by clicking. You can also set `min` and `max` attributes to define a valid range — in this example, the age must be between 0 and 120. If someone tries to submit a number outside that range, the browser will warn them.
```html
<label for="age">Age:</label>
<input type="number" id="age" name="age" min="0" max="120">
```

**`date`** — instead of making the user type a date manually (and deal with all the different date formats people use around the world), this pops up a native date picker calendar. The exact look of the calendar depends on the browser and operating system, so it'll look different on Chrome vs. Firefox vs. Safari, but the functionality is the same. This is way more user-friendly than asking someone to type "2024-03-15" by hand. You can use `min` and `max` to restrict the selectable range — dates outside the range will be greyed out in the calendar. The format must be `YYYY-MM-DD`. You can also set a default date with `value`.
```html
<label for="bday">Birthday:</label>
<input type="date" id="bday" name="birthday" min="1900-01-01" max="2026-02-01" value="2000-01-01">
```

**`color`** — shows a small color swatch that, when clicked, opens a full color picker dialog. The value stored is a hex color code like `#ff0000` for red. This is a fun one to play with, even if you won't use it in every project. Without a `value` attribute, it defaults to black (`#000000`). You can set a default color with `value` — just make sure to include the `#`.
```html
<label for="fav">Favorite color:</label>
<input type="color" id="fav" name="favcolor" value="#ff0000">
```

**`range`** — renders as a horizontal slider instead of a text box. The user drags the slider between the `min` and `max` values. One downside: the slider doesn't show the current value by default — the user just sees a slider with no number. You'd typically use JavaScript to display the value next to it, but for now, just know the HTML for it.
```html
<label for="vol">Volume:</label>
<input type="range" id="vol" name="volume" min="0" max="100">
```

**`file`** — displays a "Choose File" or "Browse" button (the exact text depends on the browser). Clicking it opens the operating system's file picker dialog. The user selects a file, and the file name appears next to the button. Actually uploading the file to a server requires backend code, but the HTML side is just this one input type.
```html
<label for="pic">Upload a photo:</label>
<input type="file" id="pic" name="photo">
```

### Checkbox and Radio Buttons

These two are easy to confuse at first because they look somewhat similar and serve a related purpose (picking from a list of options), but they work very differently.

### Tag: `<input type="checkbox">`

Checkboxes let the user select multiple options at once, like a to-do list where you can check off as many items as you want. Each checkbox is independent — checking one has no effect on the others. Also notice the labels come *after* the inputs here — with checkboxes and radio buttons, it's conventional to put the little box/circle first and the label text second.

```html
<p>Choose your toppings:</p>
<input type="checkbox" id="cheese" name="topping" value="cheese">
<label for="cheese">Cheese</label>

<input type="checkbox" id="pepperoni" name="topping" value="pepperoni">
<label for="pepperoni">Pepperoni</label>

<input type="checkbox" id="mushroom" name="topping" value="mushroom">
<label for="mushroom">Mushrooms</label>
```

#### Attributes:

- **`type="checkbox"`** — makes the input render as a small square box that can be checked or unchecked.

- **`name`** — all checkboxes in a group share the same `name` (like `"topping"` above). When the form is submitted, the server receives all the checked values under that name.

- **`value`** — what actually gets sent to the server when this box is checked. The user sees "Cheese" (from the label), but the server receives `topping=cheese` (from the value).

- **`id`** — links to the `<label>`'s `for` attribute, same as with text inputs.

### Tag: `<input type="radio">`

Radio buttons force the user to pick exactly one option from a group. The critical difference from checkboxes: selecting one automatically deselects whichever one was previously selected.

```html
<p>Choose a size:</p>
<input type="radio" id="small" name="size" value="small">
<label for="small">Small</label>

<input type="radio" id="medium" name="size" value="medium">
<label for="medium">Medium</label>

<input type="radio" id="large" name="size" value="large">
<label for="large">Large</label>
```

#### Attributes:

- **`type="radio"`** — makes the input render as a small circle instead of a square.

- **`name`** — this is the key detail. Radio buttons **must** share the same `name` attribute to be linked together as a group. The shared `name` is what tells the browser "these radio buttons belong together — only one can be selected at a time." If you accidentally give them different names, they'll each act independently and the user could select all of them, which defeats the purpose.

- **`value`** — same as checkboxes — what gets sent to the server for the selected option.

- **`id`** — links to the `<label>`, same as always.

The key difference in summary: checkboxes let you pick as many as you want (zero, one, or all of them), while radio buttons force you to pick exactly one. The name "radio button" actually comes from old car radios that had physical preset buttons — pressing one would pop out whichever button was already pressed.

### Dropdown (Select)

A dropdown menu is a good choice when you have a list of options that's too long for radio buttons (imagine having 50 radio buttons for every US state — that would take up a lot of screen space). A dropdown keeps things compact: it shows one selected value, and the full list only appears when the user clicks on it.

```html
<label for="country">Country:</label>
<select id="country" name="country">
    <option value="">-- Select --</option>
    <option value="us">United States</option>
    <option value="uk">United Kingdom</option>
    <option value="jp">Japan</option>
</select>
```

### Tag: `<select>`

The dropdown container. It works like a wrapper — the individual choices go inside it as `<option>` tags.

#### Attributes:

- **`id`** — links to the `<label>`'s `for` attribute, same as other inputs.

- **`name`** — the key sent to the server (e.g., `country=us`).

### Tag: `<option>`

Each individual choice inside the dropdown.

#### Attributes:

- **`value`** — what gets sent to the server when this option is selected. The text between the `<option>` tags is what the user *sees* in the dropdown, but the `value` is what the server *receives*. For example, the user sees "United States" but the server gets `country=us`.

### Textarea

### Tag: `<textarea>`

A multi-line text box for longer text — comments, bios, messages, etc. Unlike `<input>`, `<textarea>` is NOT self-closing. It has an opening and closing tag.

```html
<label for="msg">Message:</label>
<br>
<textarea id="msg" name="message" rows="5" cols="40" placeholder="Type your message here..."></textarea>
```

#### Attributes:

- **`id`** — links to the `<label>`, same as always.

- **`name`** — the key sent to the server.

- **`rows`** — how many lines tall the text box appears (visible height).

- **`cols`** — how many characters wide the text box appears (visible width).

- **`placeholder`** — hint text, same as on `<input>`.

### Buttons

There are three ways to make buttons in a form:

### Tag: `<input type="submit">` and `<input type="reset">`

These are `<input>` tags that render as clickable buttons instead of text boxes.

```html
<input type="submit" value="Send">
<input type="reset" value="Clear">
```

#### Attributes:

- **`type="submit"`** — submits the form (triggers validation and sends the data).

- **`type="reset"`** — clears all inputs in the form back to their default values.

- **`value`** — the text displayed on the button face. Without it, the browser uses default text like "Submit" or "Reset."

### Tag: `<button>`

A more flexible button tag that can hold text or even HTML inside it (like an icon and text together).

```html
<button type="submit">Send Form</button>
<button type="button">Just a Button</button>
```

#### Attributes:

- **`type="submit"`** — submits the form, same as `<input type="submit">`.

- **`type="button"`** — does nothing by default. You'd add behavior with TypeScript later. This is useful when you want a button that does something custom (like showing/hiding content) without submitting the form.

### Fieldset and Legend

### Tag: `<fieldset>`

Groups related inputs together with a visible border. This is useful when you have a form with multiple sections — like "Personal Info" and "Account Info." The browser draws a border around the group automatically, which looks pretty clean without any CSS.

### Tag: `<legend>`

Goes inside `<fieldset>` as the first element. It provides a title for the group — the browser displays it right on the border line of the fieldset.

```html
<fieldset>
    <legend>Personal Info</legend>
    <label for="fn">First name:</label>
    <input type="text" id="fn" name="firstname">
    <br>
    <label for="ln">Last name:</label>
    <input type="text" id="ln" name="lastname">
</fieldset>
```

### Useful Attributes
These work on most inputs:

- **`required`** — the form won't submit unless this field is filled in. Try adding this to an input, leave it empty, and click submit — the browser will show a warning message automatically. This is built-in browser validation, no code needed.
- **`disabled`** — greys out the input so it can't be interacted with. The user can see it but can't click or type in it.
- **`readonly`** — the user can see the value but can't change it. Different from `disabled` in that `readonly` fields still get submitted with the form, while `disabled` ones don't.
- **`value`** — sets a default value that's already filled in when the page loads.
- **`maxlength`** — limits how many characters you can type. Once you hit the limit, the input just stops accepting characters.
- **`autofocus`** — automatically focuses this input when the page loads, so the cursor is already in the box and ready for typing without the user having to click.

```html
<input type="text" name="username" required maxlength="20" autofocus>
```

### Autocomplete
You know how password managers like Bitwarden can automatically fill in your username and password on a login page? And how your browser sometimes suggests your name, email, or address when you start typing in a form? That's the `autocomplete` system at work.

The `autocomplete` attribute tells the browser (and password managers) exactly what a field is for — no guessing required. Without it, the browser has to look at the `name`, `id`, and `<label>` text and try to figure it out on its own. Sometimes it guesses right, sometimes it puts your phone number in the city field.

```html
<input type="text" name="username" autocomplete="username">
<input type="password" name="password" autocomplete="current-password">
<input type="email" name="email" autocomplete="email">
<input type="text" name="street" autocomplete="street-address">
```

There are a bunch of standardized values that every browser and password manager understands:

- `username` — login username
- `current-password` — existing password (for login pages)
- `new-password` — setting a new password (the browser may offer to generate a strong one for you)
- `email`
- `given-name` — first name
- `family-name` — last name
- `street-address`
- `country`
- `postal-code`
- `tel` — phone number
- `off` — turns autocomplete off entirely for that field

You can also set `autocomplete="off"` on the whole `<form>` tag to disable it for every field inside. Some sites do this on sensitive forms where they don't want the browser caching values.

This is also why some badly-built websites don't work well with password managers — if the developer used vague names like `name="field1"` and skipped labels and `autocomplete` attributes, Bitwarden has nothing to latch onto and can't figure out which field is the username and which is the password.

You don't need to use `autocomplete` in your practice page right now, but it's good to know it exists. When you build real forms later, adding `autocomplete` attributes is a small thing that makes a big difference for usability.

## Your Task

This lesson is split across two pages.

### Page 1: `forms.html` (Text Inputs)

1. Start with a `<form>` tag — this is the wrapper everything goes inside
2. Add a text input with a label — try clicking the label to see it focus the input
3. Add a password input and an email input, each with labels
4. Add at least one other input type that interests you (number, date, color, range, file)
5. Try adding `placeholder` text to your inputs

### Page 2: `forms-02.html` (Selections & Buttons)

1. Start with the boilerplate skeleton and a `<form>` wrapper
2. Add a group of checkboxes — try checking multiple at once
3. Add a group of radio buttons — try selecting them and watch how only one stays selected
4. Add a `<select>` dropdown
5. Add a `<textarea>`
6. Add a submit button and a reset button — click reset and watch all your inputs clear
7. Wrap a group of related inputs in a `<fieldset>` with a `<legend>`
8. Try adding `required` to one of your inputs and click submit — see what happens

Save and refresh after each step. Let me know when you want a review.
