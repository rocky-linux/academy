---
marp: true
theme: gaia
style: |
  :root {
    --color-background: #fff !important;
    --color-foreground: #6b7280 !important;
    --color-highlight: #f96 !important;
    --color-dimmed: #10b981 !important;
  }
_class: lead
paginate: true
markdown.marp.enableHtml: true
header: <img src='./assets/rocky_linux_logo.svg'>
footer: Rocky Linux Academy - Admin Guide
---
<style>
header,footer
{
    color: #111827;
}
@import url('../../css/rocky-theme.css');
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.3.0/css/all.min.css');
</style>

# Introduction
## Rocky Linux Admin Guide

---
<br/>

# ![right:20% w:50](./assets/rocky_linux_logo.svg) Introduction

We start with Introduction to Linux, which outlines Linux, distributions, and the whole ecosystem around our operating system.

User Commands contains essential commands for getting up to speed with Linux. More experienced users should also consult the following chapter on Advanced Linux Commands.

---
<br/>

# ![right:20% w:50](./assets/rocky_linux_logo.svg) Introduction

The VI Text Editor deserves its own chapter. While Linux comes with many editors, VI is one of the most powerful. Other commands sometimes use identical syntax to VI (`sed` comes to mind). So, knowing something about VI, or at least demystifying its essential functions (how to open a file, save, quit or quit without saving), is very important.

---
<br/>

# ![right:20% w:50](./assets/rocky_linux_logo.svg) Introduction

The user will become more comfortable with the other functions of VI as they use the editor. An alternative would be to use nano which comes installed by default in Rocky Linux. While not as versatile, it is simple to use, straightforward, and gets the job done.

---
<br/>

# ![right:20% w:50](./assets/rocky_linux_logo.svg) Introduction

We can then get into the deep functioning of Linux to discover how the system addresses:

* User Management
* File Systems
* Process Management

---
<br/>

# ![right:20% w:50](./assets/rocky_linux_logo.svg) Introduction

Backup and Restoration is essential info for the System Administrator. Linux comes with many software solutions to enhance backups (rsnapshot, lsyncd, etcetera.). It is valuable to know the essential components of the backup that exist within the operating system. We investigate two tools: `tar` and the less widespread `cpio` in this chapter.

---
<br/>

# ![right:20% w:50](./assets/rocky_linux_logo.svg) Introduction

System Startup is also an important read because management of the system during the boot process has evolved significantly in recent years since the arrival of the systemd.

---
<br/>

# ![right:20% w:50](./assets/rocky_linux_logo.svg) Introduction

Final chapters address Task Management, Implementing the Network, and Software Management including installation.

<br/>
<br/>

[Next Chapter](./01-presentation.html)