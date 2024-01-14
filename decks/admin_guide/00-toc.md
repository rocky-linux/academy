---
marp: true
theme: gaia
style: |
  @import url('../assets/css/rocky-theme.css');
_class: lead
paginate: true
markdown.marp.enableHtml: true
header: '![w:300](../assets/rocky_logo_white.png) [Back to menu](#presentation-menu)'
footer: '**Rocky Linux Academy > Admin Guide > Introduction**'
---

# Introduction
<!-- markdownlint-disable MD024 -->
![bg opacity:.5](../assets/rocky_linux_logo.svg)

<div class="intro">

## Rocky Linux Admin Guide

</div>

---

### Introduction

<i class="fa-pull-right">![w:350](../assets/rocky_linux_logo.svg)</i>

We start with Introduction to Linux, which outlines Linux, distributions, and the whole ecosystem around our operating system.

---

### User Commands

<i class="fa-pull-right">![w:350](./images/user-commands.png)</i>

**User Commands** contains essential commands for getting up to speed with Linux. More experienced users should also consult the following chapter on Advanced Linux Commands.

---

### VI Text Editor

<i class="fa-pull-right">![w:300 opacity:50%](./images/vi-text-editor.png)</i>

The **VI Text Editor** deserves its own chapter. While Linux comes with many editors, VI is one of the most powerful. Other commands sometimes use identical syntax to VI (`sed` comes to mind). So, knowing something about VI, or at least demystifying its essential functions (how to open a file, save, quit or quit without saving), is very important.

---

### VI Text Editor

<i class="fa-pull-right">![w:300 opacity:50%](./images/vi-text-editor.png)</i>

The user will become more comfortable with the other functions of VI as they use the editor. An alternative would be to use nano which comes installed by default in Rocky Linux. While not as versatile, it is simple to use, straightforward, and gets the job done.

---

### System

<div class="columns">
<div>

We can then get into the deep functioning of Linux to discover how the system addresses:

<i class="fa-pull-left">![w:200 opacity:50%](./images/system.png)</i>

</div>
<div>

* **User Management**
* **File Systems**
* **Process Management**

</div>
</div>

---

### Backup and Restoration

<i class="fa-pull-right">![w:300 opacity:50%](./images/backup.png)</i>

**Backup and Restoration** is essential info for the System Administrator. Linux comes with many software solutions to enhance backups (rsnapshot, lsyncd, etcetera.). It is valuable to know the essential components of the backup that exist within the operating system. We investigate two tools: `tar` and the less widespread `cpio` in this chapter.

---

### System Startup

<i class="fa-pull-right">![w:300 opacity:50%](./images/start-system.png)</i>

**System Startup** is also an important read because management of the system during the boot process has evolved significantly in recent years since the arrival of the systemd.

---

### Task Management

<i class="fa-pull-right fa-border">![w:200 opacity:50%](./images/task-management.png)</i>

Final chapters address **Task Management**, Implementing the Network, and Software Management including installation.

</br>
</br>
</br>
</br>

<i class="button">[Next Chapter](./01-presentation.html)</i>
