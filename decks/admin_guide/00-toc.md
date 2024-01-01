---
marp: true
theme: gaia
paginate: true
_class: lead
markdown.marp.enableHtml: true
header: '![w:300](../assets/rocky_logo_white.png) [Back to menu](../index.html)'
footer: '**Rocky Linux Academy > Admin Guide > Introduction**'
---

<style>
header,footer
{
    color: #fff;
}
section header a {
  color: inherit;
}
section a,a:link,a:visited {
    color: inherit;
}
section {
  padding-top: 90px;
}
@import url('../assets/css/rocky-theme.css');
</style>

![bg opacity:.5](../assets/rocky_linux_logo.svg)

<div class="h1lead">

# Introduction

</div>

## Rocky Linux Admin Guide

---

# ![right:20% w:50](../assets/rocky_linux_logo.svg) Introduction

We start with Introduction to Linux, which outlines Linux, distributions, and the whole ecosystem around our operating system.

---

# <i class="fa-regular fa-user"></i> User Commands

**User Commands** contains essential commands for getting up to speed with Linux. More experienced users should also consult the following chapter on Advanced Linux Commands.

---

# <i class="fa-regular fa-pen-to-square"></i> VI Text Editor

The **VI Text Editor** deserves its own chapter. While Linux comes with many editors, VI is one of the most powerful. Other commands sometimes use identical syntax to VI (`sed` comes to mind). So, knowing something about VI, or at least demystifying its essential functions (how to open a file, save, quit or quit without saving), is very important.

---

# <i class="fa-regular fa-pen-to-square"></i> VI Text Editor

The user will become more comfortable with the other functions of VI as they use the editor. An alternative would be to use nano which comes installed by default in Rocky Linux. While not as versatile, it is simple to use, straightforward, and gets the job done.

---

# ![right:20% w:50](../assets/rocky_linux_logo.svg) Introduction

We can then get into the deep functioning of Linux to discover how the system addresses:

* **User Management**
* **File Systems**
* **Process Management**

---

# <i class="fa-regular fa-window-restore"></i> Backup and Restoration

**Backup and Restoration** is essential info for the System Administrator. Linux comes with many software solutions to enhance backups (rsnapshot, lsyncd, etcetera.). It is valuable to know the essential components of the backup that exist within the operating system. We investigate two tools: `tar` and the less widespread `cpio` in this chapter.


---

# <i class="fa-regular fa-square-caret-right"></i> System Startup

**System Startup** is also an important read because management of the system during the boot process has evolved significantly in recent years since the arrival of the systemd.

---

# <i class="fa-regular fa-square-check"></i> Task Management

Final chapters address **Task Management**, Implementing the Network, and Software Management including installation.

</br>
</br>
</br>
</br>

<i class="button">[Next Chapter](./01-presentation.html)</i>
