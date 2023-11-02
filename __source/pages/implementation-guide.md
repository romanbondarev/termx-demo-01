TermX provides the ability to prepare FHIR compatible Implementation Guide (IG).

TermX synchronizes terminology, wiki pages and models into the format suitable
for [FHIR IG Publisher](https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation).

*Read more about the IG confuguration
in [Confluece](https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation), [Mitre cource](https://fshschool.org/courses/fsh-seminar/02-creating-an-ig.html),  [FHIR IG guidance](https://build.fhir.org/ig/FHIR/ig-guidance/index.html)
and [Jose Teixeira presentation](https://www.devdays.com/wp-content/uploads/2020/12/qplgv_201119_JoseCostaTeixeira_ImplementationGuideLetsBuild.pdf).*

## Configuration

TermX Wiki uses several [MD extensions](page:extended-markdown-syntax) that are not supported by the HL7 IG template out of the box. To extend the HL7 IG template rendering capabilities, we utilize the concept of IG template extension.

*Read more about [how to extend the IG template](https://build.fhir.org/ig/FHIR/ig-guidance/template.html).*

### File structure

```
├── local-template
│   ├── content
│   |   └── assets
│   |       └── js
│   |           └── **/*.js (extensions go here)
│   └── includes
|       └── _append.fragment-feedback_form.html (manually created)
├── _genonce.sh
└── ...
```

+++ Notes about extension

The extensions could be inserted directly into the HTML, but it's advised to extract them into a JavaScript file.

### {.tabset}

#### Inline

```html
<!-- _append.fragment-feedback_form.html -->
<script type="module">
  window.addEventListener('load', () => {
    // ...
  })
</script>
```

#### Script import

```html
<!-- _append.fragment-feedback_form.html -->
<script type="module" src="assets/js/file_name.js"></script>
```

+++

## Extensions


> **The `script` type**
> If you want to view IG locally, choose the `"application/javascript"` type.
> When using the `"module"` type, CORS issues may occur, but it's fine when served from the HTTP server.
> *Each extension relies on the `import` functionality. Refer to [browser compatibility](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/import#browser_compatibility).*
> {.is-info}

### Mermaid

Create `mermaid.js` file in `/content/assets/js` folder and import it in the `_append.fragment-feedback_form.html`.

#### {.tabset}

##### type="application/javascript"

```js
window.addEventListener('load', ev => {
  import('https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs').then(({default: mermaid}) => {
    document.querySelectorAll('pre.language-mermaid').forEach(el => {
      el.outerHTML = `<figure class="mermaid">${el.firstChild.innerText}</figure>`;
    })
    mermaid.run({nodes: document.getElementsByClassName('mermaid')});
  })
})
```

##### type="module"

```js
import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs';

window.addEventListener('load', () => {
  document.querySelectorAll('pre.language-mermaid').forEach(el => {
    el.outerHTML = `<figure class="mermaid">${el.firstChild.innerText}</figure>`;
  })
  mermaid.run({nodes: document.getElementsByClassName('mermaid')});
})
```

### PlantUML

Create `plantuml.js` file in `/content/assets/js` folder and import it in the `_append.fragment-feedback_form.html`. **Don't forget to copy the utils!**

#### {.tabset}

##### type="application/javascript"

```js
window.addEventListener('load', () => {
  import('https://cdn.jsdelivr.net/npm/pako@2.1.0/+esm').then(({default: pako}) => {
    document.querySelectorAll('pre.language-plantuml').forEach((el, idx) => {
      const codeElement = el.firstChild;
      const umlCode = codeElement.innerText;
      const imgUrl = composePlantUmlUrl(umlCode);
      fetch(imgUrl).then(r => r.text()).then(svg => el.outerHTML = `<figure class="plantuml">${svg}</figure>`)
    })

    // paste utils here
  })
});
```

##### type="module"

```js
import pako from 'https://cdn.jsdelivr.net/npm/pako@2.1.0/+esm'

window.addEventListener('load', () => {
  document.querySelectorAll('pre.language-plantuml').forEach((el, idx) => {
    const codeElement = el.firstChild;
    const umlCode = codeElement.innerText;
    const imgUrl = composePlantUmlUrl(umlCode);
    fetch(imgUrl).then(r => r.text()).then(svg => el.outerHTML = `<figure class="plantuml">${svg}</figure>`)
  })
});

// paste utils here
```

##### utils

```js
function composePlantUmlUrl(umlCode) {
  const server = 'https://www.plantuml.com/plantuml';
  const zippedCode = encode64(pako.deflate('@startuml' + '\n' + umlCode + '\n@enduml'));
  return `${server}/svg/~1${zippedCode}`;
}

function encode64(data) {
  let r = "";
  for (let i = 0; i < data.length; i += 3) {
    if (i + 2 === data.length) {
      r += append3bytes(data[i], data[i + 1], 0);
    } else if (i + 1 === data.length) {
      r += append3bytes(data[i], 0, 0);
    } else {
      r += append3bytes(data[i], data[i + 1],
        data[i + 2]);
    }
  }
  return r;
}

function append3bytes(b1, b2, b3) {
  let c1 = b1 >> 2;
  let c2 = ((b1 & 0x3) << 4) | (b2 >> 4);
  let c3 = ((b2 & 0xF) << 2) | (b3 >> 6);
  let c4 = b3 & 0x3F;
  let r = "";
  r += encode6bit(c1 & 0x3F);
  r += encode6bit(c2 & 0x3F);
  r += encode6bit(c3 & 0x3F);
  r += encode6bit(c4 & 0x3F);
  return r;
}

function encode6bit(b) {
  if (b < 10) {
    return String.fromCharCode(48 + b);
  }
  b -= 10;
  if (b < 26) {
    return String.fromCharCode(65 + b);
  }
  b -= 26;
  if (b < 26) {
    return String.fromCharCode(97 + b);
  }
  b -= 26;
  if (b === 0) {
    return '-';
  }
  if (b === 1) {
    return '_';
  }
  return '?';
}
```

### Draw.<span>io

Create `drawio.js` file in `/content/assets/js` folder and import it in the `_append.fragment-feedback_form.html`.

```js
window.addEventListener('load', () => {
  document.querySelectorAll('pre.language-drawio').forEach(el => {
    el.outerHTML = `<figure class="drawio"><img src="data:image/svg+xml;base64, ${el.innerText}"></figure>`
  })
})
```

## Result

The file structure should resemble the one displayed below:

```
├── local-template
│   ├── content
│   |   └── assets
│   |       └── js
│   |           ├── drawio.js
│   |           ├── mermaid.js
│   |           └── plantuml.js
│   └── includes
|       └── _append.fragment-feedback_form.html
└── ...
```

The `_append.fragment-feedback_form.html` should contain three imports:

### {.tabset}

#### type="application/javascript"

```html
<script type="application/javascript" src="assets/js/mermaid.js"></script>
<script type="application/javascript" src="assets/js/drawio.js"></script>
<script type="application/javascript" src="assets/js/plantuml.js"></script>
```

#### type="module"

```html
<script type="module" src="assets/js/mermaid.js"></script>
<script type="module" src="assets/js/drawio.js"></script>
<script type="module" src="assets/js/plantuml.js"></script>
```
