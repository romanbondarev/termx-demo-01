This page gives an overview of the basic markdown syntax supported by almost all Markdown applications. There are minor variations and discrepancies between Markdown processors. 
TermX markdown based on [MarkdownIT implementation](https://github.com/markdown-it/markdown-it). The non-standard features described on the [extended syntax](page:extended-markdown-syntax) page.


## Headers

# Header 1 
## Header 2
### Header 3
#### Header 4
##### Header 5
###### Header 6

+++ Code
```
# Header 1
## Header 2
### Header 3
#### Header 4
##### Header 5
###### Header 6
```
+++
 
## Styling
| Style         | Output                    |
|---------------|---------------------------|
| Bold          | **This is bold text**     |
| Italic        | *This text is italicized* |
| Strikethrough | ~~This was mistaken text~~ |
| Subscript     | H~2~O                     |
| Superscript   | E = mc^2^                 |

+++ Code
```
| Style         | Output                    |
|---------------|---------------------------|
| Bold          | **This is bold text**     |
| Italic        | *This text is italicized* |
| Strikethrough | ~~This was mistaken text~~ |
| Subscript     | H~2~O                     |
| Superscript   | E = mc^2^                 |
```
+++


## Blockquotes
> This is a default blockquote.

> This is a {.is-success} blockquote. {.is-success}

> This is a {.is-info} blockquote. {.is-info}

> This is a {.is-warning} blockquote. {.is-warning}

> This is a {.is-error} blockquote. {.is-error}

+++ Code
```
> This is a default blockquote.

> This is a {.is-success} blockquote. {.is-success}

> This is a {.is-info} blockquote. {.is-info}

> This is a {.is-warning} blockquote. {.is-warning}

> This is a {.is-error} blockquote. {.is-error}
+++


## Content Tabs
## {.tabset}
### First Tab

Any content here will go into the first tab...

### Second Tab

Any content here will go into the second tab...

### Third Tab

Any content here will go into the third tab...
##

Pure CSS tabs. No additional JavaScript is run.

+++ Code
```
## Content Tabs
## {.tabset}
### First Tab

Any content here will go into the first tab...

### Second Tab

Any content here will go into the second tab...

### Third Tab

Any content here will go into the third tab...
##
```
+++



## Emojis
:apple:

Can be also be used :fire: inline
+++ Code
```
:apple:

Can be also be used :fire: inline
```
+++

*See the [Emoji Cheat Sheet](https://www.webfx.com/tools/emoji-cheat-sheet/) for the full list of possible options.*


## Horizontal Line
Lorem ipsum dolor

---

Consectetur adipiscing elit

+++ Code
```
Lorem ipsum dolor

---

Consectetur adipiscing elit
```
+++


## Images
![External image](https://www.wikipedia.org/portal/wikipedia.org/assets/img/Wikipedia-logo-v2.png){width=250 title=Wikipedia align=right}
![nternal page attachment](files/64/pm.png){width=300 title="Kodality webpage background"}

+++ Code
```
![External image](https://www.wikipedia.org/portal/wikipedia.org/assets/img/Wikipedia-logo-v2.png){width=250 title=Wikipedia align=right}
![nternal page attachment](files/64/pm.png){width=300 title="Kodality webpage background"}
```
+++
Check [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img) specification for additional parameters.


## HTML
:bookmark_tabs: HTML tags are **enabled** in the source.

The inserted HTML is sanitized using Angular's DOM sanitizer, and the HTML in the code blocks is escaped using the `escape-html` library.

*The code below should not be propagetad to real input element:*
```html
<input type="text" id="name" name="name" required>
```

+++ Code
~~~
```html
<input type="text" id="name" name="name" required>
```
~~~
+++

## Inline Code
Lorem `ipsum` dolor

+++ Code
```
Lorem `ipsum` dolor
```
+++

## Code Blocks
```javascript
function lorem (ipsum) {
    const languages = 'Supported languages are javascript, json, xml, html, bash, mermaid, plantuml, fsh, ...'
}
```
Supported languages are javascript, json, xml, html, bash, mermaid, plantuml, fsh, ...

+++ Code
~~~
```javascript
function lorem (ipsum) {
    const languages = 'Supported languages are javascript, json, xml, html, bash, mermaid, plantuml, fsh, ...'
}
```
~~~
+++


## Keyboard Keys
Lorem ipsum dolor CTRL + C

+++ Code
```
Lorem ipsum dolor CTRL + C
```
+++

## Links
[Absolute link to external page](https://wikipedia.org)

[Relative link to internal page](/wiki/termx-tutorial/extended-syntax)

+++ Code
```
[Absolute link to external page](https://wikipedia.org)

[Relative link to internal page](/wiki/termx-tutorial/extended-syntax)
```
+++

## Lists
### Ordered
1. Lorem ipsum dolor sit amet
1. Consectetur adipiscing elit
1. Morbi vehicula aliquam

+++ Code
```
1. Lorem ipsum dolor sit amet
1. Consectetur adipiscing elit
1. Morbi vehicula aliquam
```
+++

### Unordered
- Lorem ipsum dolor sit amet
- Consectetur adipiscing elit
- Morbi vehicula aliquam

+++ Code
```
- Lorem ipsum dolor sit amet
- Consectetur adipiscing elit
- Morbi vehicula aliquam
```
+++

### .grid-list
- Lorem ipsum dolor sit amet
- Consectetur adipiscing elit
- Morbi vehicula aliquam
{.grid-list}

+++ Code
```
- Lorem ipsum dolor sit amet
- Consectetur adipiscing elit
- Morbi vehicula aliquam
{.grid-list}
```
+++

### .links-list
- [Lorem ipsum dolor sit amet *Subtitle description here*](https://www.google.com)
- [Consectetur adipiscing elit](https://www.google.com)
- Morbi vehicula aliquam
{.links-list}

+++ Code
```
### .links-list
- [Lorem ipsum dolor sit amet *Subtitle description here*](https://www.google.com)
- [Consectetur adipiscing elit](https://www.google.com)
- Morbi vehicula aliquam
{.links-list}
```
+++


## Table
| Header 1 (aligned left) | Header 2 (centered) | Header 3 (aligned right) |
|:---------|:----------:|---------:|
| Foo      | Bar        | Xyz      |
| Abc      | Def        | 123      |

+++ Code
```
| Header 1 (aligned left) | Header 2 (centered) | Header 3 (aligned right) |
|:---------|:----------:|---------:|
| Foo      | Bar        | Xyz      |
| Abc      | Def        | 123      |
```
+++
 

Stage | Direct Products | ATP Yields
----: | --------------: | ---------:
Glycolysis | 2 ATP ||
^^ | 2 NADH | 3--5 ATP |
Pyruvaye oxidation | 2 NADH | 5 ATP |
Citric acid cycle | 2 ATP ||
^^ | 6 NADH | 15 ATP |
^^ | 2 FADH2 | 3 ATP |
**30--32** ATP |||
{.dense}

+++ Code
```
Stage | Direct Products | ATP Yields
----: | --------------: | ---------:
Glycolysis | 2 ATP ||
^^ | 2 NADH | 3--5 ATP |
Pyruvaye oxidation | 2 NADH | 5 ATP |
Citric acid cycle | 2 ATP ||
^^ | 6 NADH | 15 ATP |
^^ | 2 FADH2 | 3 ATP |
**30--32** ATP |||
{.dense}
```
+++

## Task Lists
- [x] Checked task item
- [x] Another checked task item
- [ ] Unchecked task item

+++ Code
```
- [x] Checked task item
- [x] Another checked task item
- [ ] Unchecked task item
```
+++

## Collapsible
+++ Visible text
Hidden text
+++

```
+++ Visible text
Hidden text
+++
```

## Footnotes
This sentence[^1] needs a few footnotes.[^2]

[^1]: A string of syntactic words.
[^2]: A useful example sentence.

+++ Code
```
This sentence[^1] needs a few footnotes.[^2]

[^1]: A string of syntactic words.
[^2]: A useful example sentence.
```
+++

