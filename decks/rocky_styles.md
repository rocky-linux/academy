---
marp: true
theme: gaia
style: |
  @import url('./assets/css/rocky-theme.css');
_class: lead
paginate: true
markdown.marp.enableHtml: true
header: '![w:300](./assets/rocky_logo_white.png) [Back to menu](#styles-menu)'
footer: '**Rocky Linux Academy > Style Guide**'
---



# Graphical examples

![bg opacity:.5](./assets/rocky_linux_logo.svg)

<div class="intro">

## Styles for presentations on Rocky Linux

This slide is intended to illustrate the graphic parts that can be used to create presentations in Rocky Academy.

</div>

---

## Introduction

The following tools are used in the implementation of this project:

* **Marp** a suite of tools for transforming documentation written in Markdown into presentations (HTML and PDF)
* **Awesome Fonts** set of CSS fonts and styles that allow the inclusion of characters depicting images (glyphs) for slide customization.

---

![bg opacity:.5](./assets/rocky_linux_logo.svg)

<div class="plan_header">

## Styles menu

<div class="columns plan">
<div>

<i class="fa fa-book"></i> [Introduction](#introduction)
<i class="fa fa-book"></i> [Add a background](#add-a-background-11)
<i class="fa fa-book"></i> [Add Awesome Fonts](#add-awesome-fonts-11)
<i class="fa fa-book"></i> [Unordered List](#lists-style-11)
<i class="fa fa-book"></i> [Ordered List](#lists-style-31)

</div>
<div>

<i class="fa fa-book"></i> [Add Images](#add-images-11)
<i class="fa fa-book"></i> [Admonition](#admonition)
<i class="fa fa-book"></i> [Back to Main Menu](./index.html)

</div>
</div>

---

## Add a background 1/1

**Marp** provides numerous options for background insertion and placement. The background is inserted with a common Markdown `[text](url)` tag what differentiates it is the use of the `bg` attribute in the alternative text. In Rocky Academy, the *rocky_linux_logo.svg* was used with the following settings:

```markdown
![bg opacity:.5](./assets/rocky_linux_logo.svg)
```

This sets the background as in the next slide.

---

![bg opacity:.5](./assets/rocky_linux_logo.svg)

## Add a background 2/1

The background is mainly used for the first page of the slide and for the menu.

---

## Headings Style

# Title example

---

## Heading Style h2

The `h2` title should be used for main slide titles. For all other needs, subsequent tags (h3, h4 and h5) should be used.

### Heading Style h3

This tag can be used for all topics that are nevertheless important but secondary to the title of the slide.

---

#### `Heading` Style h4

This style fits well with subtopics such as the commands described in the *03-command.md* page of the administrator's guide.

Example:

#### `apropos` command

##### h5 Title example

This style has no defined purpose and can be used as a wildcard to interrupt long text or as a title for slides where there are only examples or blocks of code.

---

###### h6 Title example

---

## Add Awesome Fonts 1/1

---

## Add Awesome Fonts 2/1

<div class="columns">
<div>

* <i class="fa-brands fa-linux"></i> Normal size
* <i class="fa-brands fa-linux fa-2x"></i> Double size
* <i class="fa-brands fa-linux fa-4x"></i> Quad size

</div>
<div>

### Sizes

```markdown
<i class="fa-brands fa-linux"></i>
<i class="fa-brands fa-linux fa-2x"></i>
<i class="fa-brands fa-linux fa-4x"></i>
```

Awesome Fonts provides through its CSS classes the insertion, sizing and styling of the glyph.

</div>

---

## Add Awesome Fonts 3/1

<div class="columns">
<div>

* <i class="fa-solid fa-lightbulb fa-2x"></i> Solid Style
* <i class="fa-regular fa-lightbulb fa-2x"></i> Regular Style
* <i class="fa-brands fa-github fa-2x"></i> Brands Style

</div>
<div>

The free classes provided by **Awesome Fonts** are three:

**fa-solid** - **fa-regular** - **fa-brands**

```markdown
<i class="fa-solid fa-lightbulb"></i>
<i class="fa-regular fa-lightbulb"></i>
<i class="fa-brands fa-github"></i>
```

</div>

---

## Add Awesome Fonts 4/1

<i class="fa-solid fa-quote-left fa-2x fa-pull-left"></i> Left positioning is set with the `fa-pull-left` class, which determines its position and the wrapping of text in the image.

```markdown
<i class="fa-solid fa-quote-left fa-2x fa-pull-left"></i>
```

<i class="fa-solid fa-quote-right fa-2x fa-pull-right"></i> Similarly, the `fa-pull-right` class places it to the right.

```markdown
<i class="fa-solid fa-quote-right fa-2x fa-pull-right"></i>
```

---

## Add Awesome Fonts 5/1

Through the `style=""` you can configure font properties such as color, border properties and margins.

<i class="fa-solid fa-arrow-right fa-pull-right" style="color: #078ad2;"> [Next Chapter](#lists-style-11)</i>

Right-hand positioning:

```markdown
<i class="fa-solid fa-arrow-right fa-pull-right" style="color: #078ad2;"> [Next Chapter](#lists-style-11)</i>
```

<i class="fa-regular fa-circle-right fa-pull-right fa-border" style="color: #ff9100; border-color: #ff9100; border-radius: .3em"> [Next Chapter](#lists-style-11)</i>

Other version:

---

## Add Awesome Fonts 6/1

<i class="fa-brands fa-linux fa-4x fa-border fa-pull-left" style="--fa-border-color: #10b981; --fa-border-radius: 50%"></i>

This image was obtained using the `fa-linux` font with the additional style properties.

**Note:** There is no property for the font background, this in some cases can be set with CSS.

```css
style="--fa-border-color: #10b981; --fa-border-radius: 50%"
```

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

### Unordered List

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

## Add images 1/1

Basic functions are provided by *Marpit* to use Markdown tags to insert images.

![w:70](./assets/rocky_linux_logo.svg)

This image was inserted with the following Markdown code:

`![w:70](./assets/rocky_linux_logo.svg)`

---

## Add images 2/1

The positioning of images within slides can be achieved by integrating CSS settings provided by [Awesome Fonts](https://fontawesome.com/docs/web/style/pull).

Awesome Fonts CSS attributes add the ability to position the image to the right, left, and to create a border between the text and the image.

In particular, it provides the classes:

`fa-border` `fa-pull-left` `fa-pull-right`

---

## Add images 3/1

Using the options provided by *Marpit* only image insertion is possible, with no control over the position and behavior of the text. This image was inserted using only the functions of *Marpit*.

![w:150](./assets/rocky_linux_logo.svg) Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

---

## Add images 4/1

Using the `fa-pull-right` attribute, it is possible to place the image right with the text wrapping the image.

<i class="fa-border fa-pull-right">![w:150](./assets/rocky_linux_logo.svg)</i> Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat. Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

---

## Add images 5/1

<style scoped>
code {
  font-size: 0.5em;
}
</style>

Multiple images can be inserted by controlling the position and size of each one.

<i class="fa-border fa-pull-right" style="--fa-border-style: none"> ![w:150](./assets/rocky_linux_logo.svg)</i> It is also possible to insert the same image in multiple positions with different sizes. <i class="fa-border fa-pull-left" style="--fa-border-style: none"> ![w:100](./assets/rocky_linux_logo.svg)</i> In this example, the image *rocky_linux_logo.svg* was inserted twice in two different positions with different sizes.

```markdown
<i class="fa-border fa-pull-right" style="--fa-border-style: none"> ![w:150](./assets/rocky_linux_logo.svg)</i>
<i class="fa-border fa-pull-left" style="--fa-border-style: none"> ![w:100](./assets/rocky_linux_logo.svg)</i>
```

---

## Admonition

---

##### Admonition - Note

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

##### Admonition - Abstract

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

##### Admonition - Info

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
