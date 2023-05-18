---
marp: true
theme: gaia
_class: lead
paginate: true
markdown.marp.enableHtml: true

backgroundColor: #fff

header: Learning Ansible with Rocky | 3 - Management of Files
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

# 3 - Management of Files
## Learning Ansible with Rocky


---
<br/>

# <i class="fa-solid fa-trophy"></i> Objectives

In this chapter you will learn how to manage files with Ansible.

:heavy_check_mark: modify the content of file;
:heavy_check_mark: upload files to the targeted servers;
:heavy_check_mark: retrieve files from the targeted servers.

---
<br/>

# Plan

* [ini_file module](#5)
* [lineinfile module](#11)
* [copy module](#16)
* [fetch module](#21)
* [template module](#26)
* [get_url module](#32)


---
#
<br/>
<br/>
<br/>

Depending on your needs, you will have to use different Ansible modules to modify the system configuration files.

---
<br/>
<br/>
<br/>

# `ini_file` module

---
# `ini_file` module

When you want to modify an INI file eg:

```
[section]
key=value
```

the easiest way is to use the `ini_file` module.

---
# `ini_file` module

The module requires:

* The value of the section
* The name of the option
* The new value

---
# `ini_file` module

Example of use:

```
- name: change value on inifile
  community.general.ini_file:
    dest: /path/to/file.ini
    section: SECTIONNAME
    option: OPTIONNAME
    value: NEWVALUE
```

---
# `ini_file` module

> More information can be found at https://docs.ansible.com/ansible/latest/collections/community/general/ini_file_module.html.

---
<br/>
<br/>
<br/>


# Questions ?

---
<br/>
<br/>
<br/>

# `lineinfile` module

---
# `lineinfile` module

To ensure that a line is present in a file, or when a single line in a file needs to be added or modified, use the `linefile` module.

In this case, the line to be modified in a file will be found using a regexp.

---
# `lineinfile` module

For example, to ensure that the line starting with `SELINUX=` in the `/etc/selinux/config` file contains the value `enforcing`:

```
- ansible.builtin.lineinfile:
    path: /etc/selinux/config
    regexp: '^SELINUX='
    line: 'SELINUX=enforcing'
```

---
# `lineinfile` module

> More information can be found at https://docs.ansible.com/ansible/latest/collections/ansible/builtin/lineinfile_module.html.
---
<br/>
<br/>
<br/>


# Questions ?

---

<br/>
<br/>
<br/>

# `copy` module

---
# `copy` module

When a file has to be copied from the Ansible server to one or more hosts, it is better to use the `copy` module.

---
# `copy` module

Here we are copying `myflile.conf` from one location to another:

```
- ansible.builtin.copy:
    src: /data/ansible/sources/myfile.conf
    dest: /etc/myfile.conf
    owner: root
    group: root
    mode: 0644
```

---
#  `copy` module

> More information can be found at https://docs.ansible.com/ansible/latest/collections/ansible/builtin/copy_module.html.

---
<br/>
<br/>
<br/>


# Questions ?

---

<br/>
<br/>
<br/>

# `fetch` module

---
# `fetch` module

When a file has to be copied from a remote server to the local server, it is best to use the `fetch` module.

---
# `fetch` module

This module does the opposite of the `copy` module:

```
- ansible.builtin.fetch:
    src: /etc/myfile.conf
    dest: /data/ansible/backup/myfile-{{ inventory_hostname }}.conf
    flat: yes
```

---
# `fetch` module

> More information can be found at https://docs.ansible.com/ansible/latest/collections/ansible/builtin/fetch_module.html.

---
<br/>
<br/>
<br/>


# Questions ?

---
<br/>
<br/>
<br/>

# `template` module

---
# `template` module

Ansible and its `template` module use the **Jinja2** template system (http://jinja.pocoo.org/docs/) to generate files on target hosts.

---
# `template` module

For example:

```
- ansible.builtin.template:
    src: /data/ansible/templates/monfichier.j2
    dest: /etc/myfile.conf
    owner: root
    group: root
    mode: 0644
```

---
# `template` module

It is possible to add a validation step if the targeted service allows it (for example apache with the command `apachectl -t`):

```
- template:
    src: /data/ansible/templates/vhost.j2
    dest: /etc/httpd/sites-available/vhost.conf
    owner: root
    group: root
    mode: 0644
    validate: '/usr/sbin/apachectl -t'
```

---
# `template` module

> More information can be found at https://docs.ansible.com/ansible/latest/collections/ansible/builtin/template_module.html.

---
<br/>
<br/>
<br/>


# Questions ?

---
<br/>
<br/>
<br/>

# `get_url` module

---
# `get_url` module

To upload files from a web site or ftp to one or more hosts, use the `get_url` module:

```
- get_url:
    url: http://site.com/archive.zip
    dest: /tmp/archive.zip
    mode: 0640
    checksum: sha256:f772bd36185515581aa9a2e4b38fb97940ff28764900ba708e68286121770e9a
```

---
# `get_url` module

By providing a checksum of the file, the file will not be re-downloaded if it is already present at the destination location and its checksum matches the value provided.

---
<br/>
<br/>
<br/>


# Questions ?

---
#

<div class="columns">
<div>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

[Index](./Learning_Ansible_with_Rocky-0-Introduction.html)


</div>
<div>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

[Next Chapter >>](./Learning_Ansible_with_Rocky-4-Ansible_galaxy.html)

</div>
</div>
