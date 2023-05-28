---
marp: true
theme: gaia
_class: lead
paginate: true
markdown.marp.enableHtml: true

backgroundColor: #fff

header: <img src='./assets/rocky_linux_logo.svg'>
footer: Rocky Linux Academy - Admin Guide
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

.fa-twitter { color: aqua; }
.fa-mastodon { color: purple; }
.fa-linkedin { color: blue; }
.fa-window-maximize { color: skyblue; }
.fa-circle-exclamation { color: red; }
.fa-trophy { color: #10b981; }
@import 'https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.3.0/css/all.min.css'
table {
  font-size: 10px;
}
</style>

# X - 
## Rocky Linux Admin Guide

---
# 
![right:20% w:100](./assets/rocky_linux_logo.svg)

The Administrator's Guide is a collection of educational documents focused on System Administrators. They can be used by future System Administrators trying to get up to speed, by current System Administrators who would like a refresher, or by any Linux user who'd like to learn more about the Linux environment, commands, processes, and more. Like all documents of this type, it will evolve and update over time.
<br/>

---
# 

<br/>
<br/>
<br/>

We start with Introduction to Linux, which outlines Linux, distributions, and the whole ecosystem around our operating system.

---
# 

<br/>
<br/>
<br/>

User Commands contains essential commands for getting up to speed with Linux. More experienced users should also consult the following chapter on Advanced Linux Commands.

---
# 

<br/>

The VI Text Editor deserves its own chapter. While Linux comes with many editors, VI is one of the most powerful. Other commands sometimes use identical syntax to VI (`sed` comes to mind). So, knowing something about VI, or at least demystifying its essential functions (how to open a file, save, quit or quit without saving), is very important. The user will become more comfortable with the other functions of VI as they use the editor. An alternative would be to use nano which comes installed by default in Rocky Linux. While not as versatile, it is simple to use, straightforward, and gets the job done.

---
# 

<br/>
<br/>
<br/>

We can then get into the deep functioning of Linux to discover how the system addresses:

* User Management
* File Systems
* Process Management

---
# 

<br/>
<br/>
<br/>

Backup and Restoration is essential info for the System Administrator. Linux comes with many software solutions to enhance backups (rsnapshot, lsyncd, etcetera.). It is valuable to know the essential components of the backup that exist within the operating system. We investigate two tools: `tar` and the less widespread `cpio` in this chapter.

---
# 

<br/>
<br/>
<br/>

System Startup is also an important read because management of the system during the boot process has evolved significantly in recent years since the arrival of the systemd.

---
# 

<br/>
<br/>
<br/>

Final chapters address Task Management, Implementing the Network, and Software Management including installation.

---
#

<div class="columns">
<div>



</div>
<div>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

[Next Chapter](./01-presentation.html)

</div>
</div>