---
marp: true
theme: gaia
style: |
  @import url('./assets/css/rocky-theme.css');
  section {
    padding-top: 90px;
  }
_class: lead
paginate: true
markdown.marp.enableHtml: true
header: '![w:300](./assets/rocky_logo_white.png) <i class="top_link">[Back to menu](#2)</i>'
footer: '<i class="footer_text">**Rocky Linux Academy > Style Guide**</i>'
---

# Graphical examples

![bg opacity:.5](./assets/rocky_linux_logo.svg)

## Styles for presentations on Rocky Linux

---

![bg opacity:.5](./assets/rocky_linux_logo.svg)

## Plan menu

<div class="columns plan">
<div>

<i class="fa fa-book"></i> [What is an operating system?](#4)
<i class="fa fa-book"></i> [Generalities UNIX - GNU/Linux](#8)
<i class="fa fa-book"></i> [The GNU/Linux distributions](#33)

</div>
<div>

<i class="fa fa-book"></i> [Areas of use](#48)
<i class="fa fa-book"></i> [Shell](#50)
<i class="fa fa-book"></i> [Check your Knowledge](#56)

</div>
</div>

---

## Lists Style 1/1

<div class="columns">
<div>

* first
  * sub item 1
    * sub item 1.2
* second
  * sub item 2
* third

</div>
<div>

## Unordered List

Unordered lists offer a dynamic display of list items. With each advance, the next item is displayed.

</div>
</div>

---

## Lists Style 2/1

In unordered lists containing long phrases, it is possible to take advantage of the default behavior to liven up the slides by working on the colors of the various attributes ( *ul*, *li*, *ul* *li* ).  

* Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.
  * Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

---

## Lists Style 3/1

<div class="columns">
<div>

### Ordered List

Items in ordered lists are all displayed at the same time.

</div>
<div>

1. first
2. second
3. third
4. fourth

</div>
</div>

---

## Add images to slides 1/1

Basic functions are provided by *Marpit* to use Markdown tags to insert images.

![w:70](./assets/rocky_linux_logo.svg)

This image was inserted with the following Markdown code:

`![w:70](./assets/rocky_linux_logo.svg)`

---

## Add images to slides 2/1

The positioning of images within slides can be achieved by integrating CSS settings provided by [Awesome Fonts](https://fontawesome.com/docs/web/style/pull).

Awesome Fonts CSS attributes add the ability to position the image to the right, left, and to create a border between the text and the image.

In particular, it provides the classes:

`fa-border` `fa-pull-left` `fa-pull-right`

---

## Add images to slides 3/1

Using the options provided by *Marpit* only image insertion is possible, with no control over the position and behavior of the text. This image was inserted using only the functions of *Marpit*.

![w:150](./assets/rocky_linux_logo.svg) Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

---

## Add images to slides 4/1

Using the `fa-border` and `fa-pull-right` attributes, it is possible to place the image right with the text wrapping the image.

<i class="fa-border fa-pull-right">![w:150](./assets/rocky_linux_logo.svg)</i> Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat. Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

---

## Add images to slides 5/1

Multiple images can be inserted by controlling the position and size of each one.

<i class="fa-border fa-pull-right">![w:150](./assets/rocky_linux_logo.svg)</i> Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat. <i class="fa-border fa-pull-left">![w:100](./assets/rocky_linux_logo.svg)</i> Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat. Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

---

## Admonition - Note

<div class="note">

<i class="fa note-icon fa-book-open fa-pull-left fa-2x"></i>

**Note Title:** Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

</div>

Code:

```markdown
<div class="note">

<i class="fa note-icon fa-book-open fa-pull-left fa-2x"></i>

**Note Title:** Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

</div>
```

---

## Admonition - Abstract

<div class="abstract">

<i class="fa abstract-icon fa-arrows-to-circle fa-pull-left fa-2x"></i>

**Abstract:** Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

</div>

Code:

```markdown
<div class="abstract">

<i class="fa abstract-icon fa-arrows-to-circle fa-pull-left fa-2x"></i>

**Abstract:** Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

</div>
```

---

## Admonition - Info

<div class="info">

<i class="fa info-icon fa-circle-info fa-pull-left fa-2x"></i>

**Info:** Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

</div>

Code:

```markdown
<div class="info">

<i class="fa info-icon fa-circle-info fa-pull-left fa-2x"></i>

**Info:** Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

</div>
```

---

<div class="tip">

<i class="fa tip-icon fa-comments fa-pull-left fa-2x"></i>

Tip: Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

</div>

<div class="question">

<i class="fa question-icon fa-circle-question fa-pull-left fa-2x"></i>

Question: Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

</div>

<div class="warning">

<i class="fa warning-icon fa-circle-exclamation fa-pull-left fa-2x"></i>

Warning: Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

</div>

---

<div class="danger">

<i class="fa danger-icon fa-triangle-exclamation fa-pull-left fa-2x"></i>

Danger: Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

</div>

---
