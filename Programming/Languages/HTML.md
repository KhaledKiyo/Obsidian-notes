#web #programing #frontend
[[CSS]]

## structure

every html file starts with this boilerplate

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>page title</title>
  </head>
  <body>

  </body>
</html>
````

- `<!DOCTYPE html>` — tells the browser this is html5
- `<html lang="en">` — root of the page, `lang` helps screen readers and search engines
- `<head>` — invisible info about the page (title, links, meta)
- `<meta charset="UTF-8">` — lets you use any character (arabic, emoji, etc.)
- `<meta name="viewport" ...>` — makes the page not look zoomed out on mobile
- `<title>` — the text shown on the browser tab
- `<body>` — everything visible on the page goes here

---

## head extras

link a css file

```html
<link href="css/style.css" rel="stylesheet">
```

link a js file — `defer` means it runs after the html is loaded

```html
<script src="js/main.js" defer></script>
```

set a favicon (the little icon on the browser tab)

```html
<link rel="icon" href="favicon.ico">
```

---

## text

h1 is the main title of the page — use it once. h2, h3... are sub-headings

```html
<h1>main title</h1>
<h2>sub heading</h2>
<h3>smaller heading</h3>
```

a paragraph

```html
<p>some text here</p>
```

make text bold or italic

```html
<strong>bold</strong>
<em>italic</em>
```

force a line break (no closing tag)

```html
<br>
```

a horizontal line, useful as a divider

```html
<hr>
```

---

## links

clicking the text takes you to the url

```html
<a href="https://example.com">click here</a>
```

`target="_blank"` opens the link in a new tab

```html
<a href="https://example.com" target="_blank">opens in new tab</a>
```

link to a section on the same page — the href matches an id on another element

```html
<a href="#about">go to about section</a>

<h2 id="about">about</h2>
```

---

## images

`alt` is the text shown if the image fails to load — also used by screen readers

```html
<img src="image.png" alt="a description of the image">
```

---

## lists

unordered list — shows bullet points

```html
<ul>
  <li>html</li>
  <li>css</li>
  <li>javascript</li>
</ul>
```

ordered list — shows numbers

```html
<ol>
  <li>wake up</li>
  <li>open laptop</li>
  <li>code</li>
</ol>
```

---

## containers

`<div>` is a block container — takes up the full width, starts on a new line

```html
<div>i'm a block, i push things above and below me</div>
```

`<span>` is an inline container — sits inside text, doesn't break the line

```html
<p>this word is <span>highlighted</span> with css</p>
```

use `<div>` to group sections of the page. use `<span>` to style part of a text.

---

## semantic layout

these work exactly like `<div>` but their names describe their purpose. browsers, search engines, and screen readers understand them better.

```html
<header>
  <!-- logo, site title, top nav -->
</header>

<nav>
  <!-- navigation links -->
</nav>

<main>
  <!-- the main content of the page — use once -->

  <section>
    <!-- a group of related content, like "about" or "services" -->
  </section>

  <article>
    <!-- self-contained content like a blog post or news item -->
  </article>

  <aside>
    <!-- side content — related but not the main point, like a sidebar -->
  </aside>

</main>

<footer>
  <!-- bottom of the page — copyright, links, contact -->
</footer>
```

a real page usually looks like this

```
┌──────────────────────┐
│        header        │
├──────────────────────┤
│         nav          │
├───────────────┬──────┤
│               │      │
│     main      │aside │
│               │      │
├───────────────┴──────┤
│        footer        │
└──────────────────────┘
```

---

## forms

a form collects input from the user and sends it somewhere

```html
<form action="/submit" method="post">

  <!-- action = where to send the data -->
  <!-- method = how to send it (post for sensitive data, get for search) -->

  <label for="name">name</label>
  <input type="text" id="name" name="name" placeholder="your name">

  <!-- label "for" must match the input "id" — clicking the label focuses the input -->

  <button type="submit">send</button>

</form>
```

common input types — the browser changes behavior based on `type`

```html
<input type="text">       <!-- plain text -->
<input type="email">      <!-- validates email format -->
<input type="password">   <!-- hides characters -->
<input type="number">     <!-- only numbers -->
<input type="checkbox">   <!-- on/off tick box -->
<input type="radio">      <!-- pick one from a group -->
<input type="file">       <!-- upload a file -->
```

for longer text, use textarea

```html
<textarea name="message" rows="4" placeholder="write something..."></textarea>
```

for a dropdown menu

```html
<select name="color">
  <option value="red">red</option>
  <option value="blue">blue</option>
  <option value="green">green</option>
</select>
```

---

## tables

for displaying data in rows and columns

```html
<table>
  <thead>              <!-- the header row -->
    <tr>               <!-- tr = table row -->
      <th>name</th>    <!-- th = table header (bold by default) -->
      <th>age</th>
    </tr>
  </thead>
  <tbody>              <!-- the data rows -->
    <tr>
      <td>ali</td>     <!-- td = table data (a cell) -->
      <td>25</td>
    </tr>
    <tr>
      <td>sara</td>
      <td>22</td>
    </tr>
  </tbody>
</table>
```

---

## media

embed a video (controls adds play/pause buttons)

```html
<video src="video.mp4" controls></video>
```

autoplay, muted, loop

```html
<video src="video.mp4" autoplay muted loop></video>
```

embed audio

```html
<audio src="audio.mp3" controls></audio>
```

embed another website inside your page

```html
<iframe src="https://example.com" width="600" height="400"></iframe>
```

---

## misc

html comment — not visible on the page

```html
<!-- this is a comment -->
```

`&nbsp;` — a space that won't collapse (html ignores extra spaces normally)

```html
<p>hello&nbsp;&nbsp;&nbsp;world</p>
```

special characters

```
&lt;   →  <
&gt;   →  >
&amp;  →  &
&copy; →  ©
```