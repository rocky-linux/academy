---
marp: true
theme: gaia
_class: lead
paginate: false
markdown.marp.enableHtml: true
backgroundColor: #fff
header: Learning with Rocky Linux
footer: Rocky Linux Academy
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

![right:50% w:200](./assets/rocky_linux_logo.svg)

Learning Linux made easy.

# Welcome to the Rocky Linux Academy

---

# What you will learn :

- Learning Linux Administration with Rocky Linux (soon)
- Learning Bash with Rocky Linux (soon)
- Learning Ansible with Rocky Linux

---
# Learning Linux Administration with Rocky Linux

:heavy_check_mark: [Introduction](./admin_guide/00-toc.html)
:heavy_check_mark: [Introduction to Linux](./admin_guide/01-presentation.html)


---
# Learning Bash with Rocky Linux

soon...

---
# Learning Ansible with Rocky Linux

:heavy_check_mark: [Introduction](./ansible/Learning_Ansible_with_Rocky-0-Introduction.html)
:heavy_check_mark: [Ansible Basics](./ansible/Learning_Ansible_with_Rocky-1-Ansible_Basics.html)
:heavy_check_mark: [Ansible Intermediate](./ansible/Learning_Ansible_with_Rocky-2-Ansible_Advanced.html)
:heavy_check_mark: [ Management of Files](./ansible/Learning_Ansible_with_Rocky-3-Working_with_files.html)
:heavy_check_mark: [Ansible Galaxy](./ansible/Learning_Ansible_with_Rocky-4-Ansible_galaxy.html)
:heavy_check_mark: [Ansible deployments with Ansistrano](./ansible/Learning_Ansible_with_Rocky-5-Ansible_deployments_with_ansistrano.html)
:heavy_check_mark: [Large scale infrastructure](./ansible/Learning_Ansible_with_Rocky-6-Ansible_Large_scale_infrastructure.html)
:heavy_check_mark: [Working with filters](./ansible/Learning_Ansible_with_Rocky-7-Ansible_Working_with_filters.html)
:heavy_check_mark: [Management server optimizations](./ansible/Learning_Ansible_with_Rocky-8-Ansible_Management_server_optimizations.html)
