---
marp: true
theme: gaia
_class: lead
paginate: false
markdown.marp.enableHtml: true

backgroundColor: #fff

header: <img src='./assets/rocky_linux_logo.svg'> Learning Ansible with Rocky | Introduction
footer: Rocky Linux Academy - Ansible courses
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

![right:20% w:100](./assets/rocky_linux_logo.svg)

Ansible is a simple, yet powerful, automation engine for Linux.
<br/>

<div class="columns">
<div>
This tutorial will guide you through the concepts of using Ansible to automate your IT tasks in a way that is (hopefully) fun and informative. 
</div>
<div>
Using the exercises throughout these chapters, will help you gain a comfort level with Ansible in real-world applications.

</div>
</div>

---

# Table of contents

:heavy_check_mark: [Introduction](./Learning_Ansible_with_Rocky-0-Introduction.html)
:heavy_check_mark: [Ansible Basics](./Learning_Ansible_with_Rocky-1-Ansible_Basics.html)
:heavy_check_mark: [Ansible Intermediate](./Learning_Ansible_with_Rocky-2-Ansible_Advanced.html)
:heavy_check_mark: [Management of Files](./Learning_Ansible_with_Rocky-3-Working_with_files.html)
:heavy_check_mark: [Ansible Galaxy](./Learning_Ansible_with_Rocky-4-Ansible_galaxy.html)
:heavy_check_mark: [Ansible deployments with Ansistrano](./Learning_Ansible_with_Rocky-5-Ansible_deployments_with_ansistrano.html)