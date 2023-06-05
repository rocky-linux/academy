---
marp: true
theme: gaia
_class: lead
paginate: false
markdown.marp.enableHtml: true
backgroundColor: #fff
header: Translation Process - po4a experimentation
footer: Rocky documentation team
---
<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
blockquote {
  background: #ffedcc;
  border-left: 10px solid #d1bf9d;
  margin: 1.5em 10px;
  padding: 0.5em 10px;
}
blockquote:before{
  content: unset;
}
blockquote:after{
  content: unset;
}
header {
    display: grid;
    grid-template-columns: 1fr max-content;
    background-color: #10b981;
    align-content: right;
    color: white;
    font-size: 1em;
    padding: 20px;
}
footer {
    display: grid;
    grid-template-columns: 1fr max-content;
    background-color: #10b981;
    align-content: right;
    color: white;
}
.columns {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1rem;
}
.columns3 {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 1rem;
} 

</style>

<br/>

![right:50% w:200](../assets/rocky_linux_logo.svg)

po4a experimentation

# Translation process

---

# Experimentation team

<div class="columns">
  <div>

  ## Antoine (alemorvan)
  Author of the Admin Guide, Ansible book, Learning Bash

  French Translator
  </div>

  <div>

  ## Franco (Ambaradan)
  Author of NvChad book

  <br/>

  Italian Translator
  </div>
</div>

with the help of Steven Spencer of course...

---
# Typical translation workflow

1. Extract strings from source files
2. Translate strings for each language
3. Generate translated files from translated files

---
# Actual crowdin workflow

1. Directly extract strings from Mardown
2. Manage translation of the strings per language
3. Generate (try to) translated files

---

# Strong points

- WebUI for translators
- No `git` knowledge required
- Overview of translated files
- XLIFF exportation for offline translation (`poedit`)
- Easy review of translated files in github PR

---
# Problems

Lots of problems!

- Small changes mean many previously translated strings need to be revalidated (a never-ending grind for translators)
- Cannot correctly reorder translated strings in translated files
- Poor management of certain markdown tags (e.g. admonitions)

---
# `po4a` challenge

Take string extraction and file reconstruction out of the crowdin process

`po4a` is a mature and recognized tool for this task

Have to be integrated in the github actions process to be transparent for end users

---
# New workflow

- When a change is detected in the source files, github actions will launch a new extraction process and will update `pot` files
- Crowdin will sync the `pot` files

Translators have to do the job...

---
# New workflow

- When a pot file is translated, crowdin will generate the `po` file for the concerned language
- Crowdin will sync the `po` within github

...

- Once again, github action detect the changes, generate the translated markdown files thanks to `po4a` then next launch the `mkdocs` process to generate website and pdfs.

---
# Strong points

- This process works!
- `po` files exportation for offline translation (poedit)

---
# Concessions

- No more overview of translated files
- More complicated github action process (transparent for user)
- Less easy review of translated files in github PR

---
# Problems

How to retrieve previously translated strings (crowdin suggestion from older translations)?
