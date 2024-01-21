# Guidelines for writing good decks

If you are reading this document, it means that you have decided to take part in writing our presentation materials.
Thank you very much.

By following these guidelines, we aim to :

* keep the source code readable and maintainable,
* keep our presentations consistent,
* generate good-looking, high-quality documents.

To achieve this, we recommend that you install a linter such as markdownlinter (available under vscode) and follow good practice in resolving any problems that the linter brings to your attention. Normally, the necessary exceptions will already have been added to the configuration file (`.markdownlint.yml`).

In this document, we will not be dwelling on the syntax of markdown code itself, but on how to build successful slides.

## Managing the header

Each deck should start with a header in yaml format.

This header is used to specify that we will be using **marp** and to define its main options (theme, pagination, etc.).

You will also need to specify any additional css styles for the entire deck. Putting the styles in the header avoids overloading the first slide and avoids using html code in the markdown.

```yaml
marp: true
theme: gaia
style: |
  @import url('../assets/css/rocky-theme.css');
_class: lead
paginate: true
markdown.marp.enableHtml: true
header: '![w:300](../assets/rocky_logo_white.png) [Back to menu](../)'
footer: '**Rocky Linux Academy > DECK TITLE > SUBTITLE**'
---
```

In the style tag, we take care to incorporate the css of the Rocky theme. This same theme takes care of including the necessary style sheets and fonts.

The header and footer tags have to be customized. The header contains a link to the top menu, allowing our users to return to the menu from any slide and easily navigate through our presentations.

## Creating the first page

Once the header has been defined, it is time to create the first page of our presentation. This may not be the most important page, but it is the one that will be visible to users for the longest: we might as well make it as pretty as possible.

The first page must begin with a level 1 heading (`#`), and this will be the only level one heading in your entire document.

As with any title, a blank line must be placed after it.

```markdown
# Title of the deck

![bg opacity:.5](../assets/rocky_linux_logo.svg)

<div class="intro">

## Title of the chapter

**Text to introduce the chapter.**

</div>
```

Next, we define a background image with the Rocky logo.

* The level 1 title corresponds to the title of our presentation.
* the level 2 title corresponds to the title of the presentation group. For example, for the ansible introduction deck, title 1 is `# Introduction`, while title 2 will be identical to all the presentations in the chapter and will be `## Learning Ansible with Rocky`.

If you can, complete this first slide with an introductory text to the chapter (optional).

Remember to add `---` at the end of your diapositive to start a new one (with one blank line before and after the `---`).

## Talking about objectives

In terms of pedagogy, it is important to define the objectives to be achieved with the learner. These objectives must be quantifiable and measurable (with a quiz at the end to check that the objectives have been achieved). Believe me, it is not that easy to define these kinds of objectives.

```markdown

---

## Objectives

In this chapter, future Linux administrators will learn how to:

:heavy_check_mark: **Move** within the system tree.   
:heavy_check_mark: **Create** a text file, **display** its contents and **modify** it.   
:heavy_check_mark: **Use** the most useful Linux commands.
```

Note that the title of this slide is level 2! There is a blank line before and after the title.

Please do not skip this important step for our learners.

## Adding a plan

A plan is important so that the user can project himself into the chapter he is about to follow, and allows the trainer to introduce each topic.

This is the example plan used in the *01-presentation.md* file:

```markdown

![bg opacity:.5](../assets/rocky_linux_logo.svg)

<div class="plan_header">

## Presentation menu

</div>

<div class="columns plan">
<div>

[What is an operating system?](#what-is-an-operating-system)
[Generalities UNIX - GNU/Linux](#generalities-unix---gnulinux)
[Market Share](#market-share)
[Architectural design](#architectural-design)
[Multi-task](#multi-task)
[The GNU/Linux philosopy](#the-unixlinux-philosophy)
[The GNU/Linux distributions](#the-gnulinux-distributions)

</div>
<div>

[Desktop environments](#desktop-environments)
[Free / Open Source](#free--open-source)
[GNU GPL](#gnu-gpl)
[Areas of use](#areas-of-use)
[Shell](#shell)
[Check your Knowledge](#check-your-knowledge)
[Back to Main Menu](../)

</div>
</div>
```

## Last slide

Let us talk about the last slide right away: this slide should enable the trainer to take stock of the chapter before moving on to the next chapter or returning to the main menu. A button is therefore created to go directly to the next chapter.

```markdown
---

## <i class="fa-regular fa-square-check"></i> Next steps

<i class="button">[Next Chapter](./name_of_the_markdown_file_without_extension.html)</i>
```

## How to deal with multiple same titles

In order to have a smoother display of the slides, it is sometimes necessary to repeat the initial title in the subsequent slides, so that the course user when the content changes always has the reference on what the main topic of the slide is.

Its repetition does not produce any Markdown syntax problems in the resulting file since *marp* takes care of numbering any equal titles to have a unique `id` for all anchors.

NOTE: Headings with the same content are classified as syntax errors in Markdown but since they are necessary for better display they should be muted if a linter is used (by default in this project *markdownlint* is used).

The inline tag can be used for the purpose.

```markdown
<!-- markdownlint-disable MD024 -->
```

## Making columns

You can process columns using a specific class, as shown below:

```markdown
<div class="columns">
<div>

First column

</div>
<div>

Second column

</div>
</div>
```

Do not forget to leave a blank line before and after the `div` HTML tags.

## Questions pages

At the end of each chapter, you should introduce a special slide allowing the trainer to pause and take stock of the situation before continuing with the next chapter, and the learners to ask any questions they may have to clarify certain points.

```markdown
---

## Questions ?

```

Next chapter is introduced with a blank slide like bellow:

```markdown
---

## Installation on the management server

```

## Code snippets

Code snippets must specify with language is used. If there are no specific language, please use the `text` attribute.

```markdown
    ```bash
    sudo dnf install epel-release
    sudo dnf makecache
    sudo dnf install ansible 
    ```
```

## How to deal with big table or scripts

If your table or script are a little bit too long, you can use a scoped style to reduce the size:

```markdown

---

## My title

<style scoped>
table {
  font-size: 0.5em;
}
</style>
```

Then, the size of the table will be reduce and easily adjusted.

Same thing for a script:

```markdwon
<style scoped>
code {
  font-size: 0.4em;
}
</style>
```

## Admonitions

To represent admonitions in the documentation, corresponding CSS classes (notes,info,tip,...) were created in the file `rocky-theme.css`. In particular, a common part was created for all admonitions:

```css
.note,
.abstract,
.info,
.tip,
.question,
.warning,
.danger {
  border-radius: 0.5em;
  border-style: solid;
  border-width: 0.1em;
  padding: 0em 0.6em 0.6em 0.6em;
  margin: 0.5em;
  color: #111827;
}
```

And a custom part for each admonition that sets the background and border color according to the type of admonition:

```css
.note {
  background-color: #d9e7ff;
  border-color: #c5dbff;
}
```

A separate class was also created for the admonition icon to set its color:

```css
.note-icon {
  color: #448aff;
}
```

### Conversion of admonition

To correctly represent the admonition in the slide, the original code in the document must be changed. An admonition will have the following code in the original document:

```markdown
!!! note "Title of the note"

    Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.
```

which should be changed to:

```markdown
<div class="note">

<i class="fa note-icon fa-book-open fa-pull-left fa-2x"></a>

**Title of the note**

Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.

</div>
```

In this way, the admonition is inserted into a *div* to which the corresponding class of the admonition is assigned which determines its background and border color. The admonition icon with the following classes is also inserted:

* `fa` activate Awesome Fonts font loading without any customization
* `note-icon` sets the color of the icon
* `fa-book-open` corresponds to the selected icon
* `fa-pull-left` this property fixes the icon on the left side of the box and allows the text to wrap around the icon
* `fa-2x` doubles the size of the icon

NOTE: If the text is too short the display is not optimal, to remedy this you can insert a `</br>` tag after the sentence.

## Checking knowledge

Feel free to add questions to your presentations. You can add them at the end of a chapter or the end of the presentation. This allows you to go back over specific notions, get the class talking, and make the presentation more interactive.

```markdown
---

## <i class="fa fa-user-check"></i> Check your Knowledge

:heavy_check_mark: An operating system is a set of programs for managing the available resources of a computer:

[ ] True
[ ] False

```

## A few final recommendations

* Simplify your slides. An image is preferable to a long presentation. Remove as much text as possible.
* Make your presentations fun. Add questions, games, and images.
* Put yourself in the trainer's shoes and allow him/her the opportunity to interact with the class and the students.
* Strongly prefer Markdown to HTML.
