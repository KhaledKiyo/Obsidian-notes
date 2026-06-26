#concepts #web 
[[HTML]] [[CSS]]
## what a browser does

a browser requests a resource from a server (usually an html file) and displays it in the window. the location is specified by a uri (uniform resource identifier). the way it interprets and displays html is defined by the w3c html and css specifications.

common ui elements every browser has: address bar, back/forward buttons, bookmarks, refresh/stop, home button. none of this is in any spec — browsers just copied each other over the years.

---

## main components

- user interface — everything you see except the actual page (address bar, buttons, etc.)
- browser engine — the middleman between the ui and the rendering engine
- rendering engine — parses html and css, draws the page on screen
- networking — handles http requests
- ui backend — draws basic os-level widgets like dropdowns and windows
- javascript interpreter — parses and runs javascript
- data storage — cookies, localstorage, indexeddb, websql, filesystem

chrome runs a separate rendering engine instance per tab, each in its own process.

---

## rendering engines

each browser uses a different engine:

- firefox → gecko
- safari → webkit
- chrome / opera (v15+) → blink (a fork of webkit)
- internet explorer → trident

webkit started as a linux engine, then apple modified it for mac and windows.

---

## the rendering flow

when you load a page, the rendering engine does this:

```
html ──► parse ──► DOM tree ──┐
                              ├──► render tree ──► layout ──► paint
css  ──► parse ──► style ─────┘
```

1. parse html → build the dom tree
2. parse css → build style rules
3. combine both → build the render tree (visual elements only)
4. layout → calculate exact position and size of every element
5. paint → draw everything on screen

this is gradual — the browser doesn't wait for the full html to arrive before it starts rendering. it displays content as it comes in.

---

## parsing

parsing = turning raw text into a tree structure the code can use.

every parser works in two steps:

- lexer (tokenizer) — breaks the input into tokens (the building blocks, like words in a language)
- parser — applies grammar rules to those tokens and builds a tree

the parser asks the lexer for tokens one at a time, tries to match them to grammar rules, and builds the tree as it goes. if no rule matches, it stores the token and keeps going until a match is found. if nothing ever matches, it throws a syntax error.

there are two parser types:

- top-down — starts from the highest-level rule and works down
- bottom-up (shift-reduce) — scans the input, matches low-level rules first, builds up

webkit uses flex (for the lexer) and bison (for the parser) to auto-generate its parsers from grammar files.

---

## html parsing

html cannot be parsed with a normal parser because it's not a proper context-free grammar. it's forgiving — you can omit tags, nest things wrong, use made-up tags, and the browser still renders it.

so browsers use a custom html parser defined by the html5 spec. it has two stages:

**tokenization** — reads the html character by character using a state machine. example states:

- data state → normal text
- tag open state → just saw `<`
- tag name state → reading the tag name
- end tag state → reading a closing tag

each recognized token (start tag, end tag, attribute, text) gets passed to the tree constructor.

**tree construction** — takes tokens and builds the dom tree. also uses a state machine (called "insertion modes"). it maintains a stack of open elements to handle nesting and unclosed tags.

example: parsing `<html><body>Hello world</body></html>`

- `<html>` token → creates HTMLHtmlElement, appended to Document
- `<body>` token → head is created implicitly, then HTMLBodyElement is created
- `Hello world` → text node created and appended
- `</body>` → mode shifts to "after body"
- `</html>` → mode shifts to "after after body"
- end of file → parsing done

when parsing finishes, deferred scripts run, document state is set to "complete", and the `load` event fires.

---

## html error tolerance

browsers never show a syntax error for html — they fix bad markup silently. examples of what webkit handles:

- `</br>` instead of `<br>` → treated as `<br>`
- a table inside another table → split into two sibling tables
- a form inside a form → second form is ignored
- more than 20 of the same nested tag → extras ignored

this behavior isn't in any spec, it just grew from browsers trying to match each other's behavior.

---

## dom

dom (document object model) is the tree the browser builds from html. each element becomes a node. javascript uses the dom to read and modify the page.

```html
<html>
  <body>
    <p>hello</p>
    <div><img src="x.png"/></div>
  </body>
</html>
```

becomes:

```
Document
└── html
    └── body
        ├── p
        │   └── "hello"
        └── div
            └── img
```

the dom is specified by the w3c. it's the interface between the page and javascript.

---

## css parsing

unlike html, css is a proper context-free grammar, so it can be parsed with standard parsers.

each css file becomes a stylesheet object. each rule becomes a rule object with a selector and declarations.

to match rules efficiently, browsers store them in hash maps by id, class, and tag name. this skips ~95% of rules for any given element without even checking them.

**cascade order** (low → high priority):

1. browser default styles
2. user normal styles
3. author normal styles
4. author `!important`
5. user `!important`

**specificity** — when two rules have the same cascade level, specificity decides which wins. calculated as a 4-part score (a, b, c, d):

- a = 1 if it's an inline style, else 0
- b = number of id selectors
- c = number of class / attribute / pseudo-class selectors
- d = number of element / pseudo-element selectors

higher score wins. examples:

- `*` → 0,0,0,0
- `li` → 0,0,0,1
- `#id` → 0,1,0,0
- `style=""` → 1,0,0,0

firefox also builds a rule tree and style context tree to cache computed styles and avoid recalculating them for every element.

---

## render tree

built at the same time as the dom tree. only contains elements that will actually be painted:

- `display: none` → not in the render tree
- `visibility: hidden` → still in the render tree (takes up space)
- `<head>` → not in the render tree

each node in the render tree:

- webkit calls them render objects / renderers
- firefox/gecko calls them frames

each renderer knows how to calculate its own size and how to paint itself and its children. it corresponds to a css box — it has geometry (width, height, position).

the render tree doesn't map 1:1 to the dom. one dom element can produce multiple renderers (e.g. a `<select>` creates 3: display area, dropdown, button). floats and absolutely positioned elements are placed in a different part of the tree with a placeholder where they would have been.

---

## layout

layout (called reflow in firefox) assigns every renderer an exact position and size on screen.

html uses a flow-based model — most elements can be calculated in a single left-to-right, top-to-bottom pass. tables may need multiple passes.

**dirty bit system** — browsers don't recalculate the whole tree on every change. renderers mark themselves as "dirty" when they change. only dirty nodes get recalculated.

two types of layout:

- global layout — recalculates everything. happens on font size change, window resize, etc.
- incremental layout — only recalculates dirty nodes. runs asynchronously.

layout process for each renderer:

1. parent determines its own width
2. parent places children (sets x, y), calls their layout if needed
3. parent uses children's heights to set its own height
4. dirty bit is cleared

---

## painting

the render tree is traversed and each node's `paint()` method is called to draw it on screen.

painting order for each element:

1. background color
2. background image
3. border
4. children
5. outline

like layout, painting can be global or incremental. when a renderer changes, it marks its screen rectangle as dirty. the os fires a paint event for that region and the browser repaints it.

webkit saves the previous rectangle as a bitmap and only repaints the difference (delta).

the rendering engine is single-threaded — everything except network operations runs on one thread. network requests can run on multiple parallel threads (usually 2–6 connections).

the browser's main thread is an event loop — an infinite loop that waits for events (layout, paint, user input) and processes them.

---

## dynamic changes

| change                   | what the browser does                 |
| ------------------------ | ------------------------------------- |
| element color changes    | repaint only                          |
| element position changes | layout + repaint                      |
| dom node added           | layout + repaint                      |
| font size on `<html>`    | full relayout + repaint of everything |

---

## scripts and style sheets

**scripts** — `<script>` halts html parsing until the script is fetched and executed. this is synchronous by design.

- `defer` → script runs after parsing finishes
- `async` → script fetches and runs in a separate thread, doesn't block parsing

webkit and firefox do speculative parsing — while a script is running, another thread scans the rest of the html and preloads external resources (scripts, stylesheets, images). it doesn't modify the dom, just preloads.

**style sheets** — don't block html parsing, but they do block scripts. if a script runs before a stylesheet is loaded, it might get wrong style info. firefox blocks all scripts when a stylesheet is still loading. webkit only blocks scripts that try to access style properties that might be affected.

---

## css box model

every element generates a rectangular box:

```
┌─────────────────────────┐
│         margin          │
│  ┌───────────────────┐  │
│  │      border       │  │
│  │  ┌─────────────┐  │  │
│  │  │   padding   │  │  │
│  │  │  ┌───────┐  │  │  │
│  │  │  │content│  │  │  │
│  │  │  └───────┘  │  │  │
│  │  └─────────────┘  │  │
│  └───────────────────┘  │
└─────────────────────────┘
```

box types:

- block — gets its own rectangle, stacks vertically (`div`, `p`)
- inline — sits inside a line, flows horizontally (`span`, `a`)

block elements stack top to bottom. inline elements flow left to right inside line boxes. if the container is too narrow, inlines wrap to the next line.

---

## positioning

- static — default, normal flow
- relative — normal flow, then shifted by top/left/right/bottom
- float — placed in normal flow first, then shifted left or right. other content flows around it
- absolute — removed from normal flow, positioned relative to its containing block
- fixed — same as absolute but relative to the viewport, doesn't scroll

---

## z-index and stacking

`z-index` controls which element appears on top when elements overlap.

elements with `z-index` form stacking contexts. within a context, elements with higher z-index are painted in front. stacking contexts can be nested. the viewport is the outermost stacking context.

painting within a stacking context goes back to front — lower z-index elements get painted first.
