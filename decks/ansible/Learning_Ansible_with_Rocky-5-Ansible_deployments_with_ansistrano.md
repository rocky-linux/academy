---
marp: true
theme: gaia
_class: lead
paginate: true
markdown.marp.enableHtml: true

backgroundColor: #fff

header: Learning Ansible with Rocky | 5 - Ansible deployments with Ansistrano
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

# 5 - Ansible deployments with Ansistrano
## Learning Ansible with Rocky

---
<br/>

# <i class="fa-solid fa-trophy"></i> Objectives

In this chapter you will learn how to deploy applications with the Ansible role Ansistrano (https://ansistrano.com).

:heavy_check_mark: Implement Ansistrano;
:heavy_check_mark: Configure Ansistrano;       
:heavy_check_mark: Use shared folders and files between deployed versions;       
:heavy_check_mark: Deploying different versions of a site from git;        
:heavy_check_mark: React between deployment steps.  

---
<br/>

# Plan

* [Introduction](./Learning_Ansible_with_Rocky-5-Ansible_deployments_with_ansistrano.html#5)
* [Demo](./Learning_Ansible_with_Rocky-5-Ansible_deployments_with_ansistrano.html#10)

---
#
<br/>
<br/>
<br/>

Ansistrano is an Ansible role to easily deploy PHP, Python, etc. applications.

It is based on the functionality of Capistrano (http://capistranorb.com/).

---
<br/>
<br/>
<br/>

# Introduction

---
# Introduction

Ansistrano requires the following to run:

* Ansible on the deployment machine,
* `rsync` or `git` on the client machine.

It can download source code from `rsync`, `git`, `scp`, `http`, `S3`, ...

---
<style scoped>
li {
  font-size: 0.7em;
}
</style>
# Introduction

Ansistrano deploys applications by following these 5 steps:

<div class="columns">
<div>

![right:50% w:500](./assets/chapter5/ansistrano-001.png)

</div>
<div>

* **Setup**: create the directory structure to host the releases;
* **Update Code**: downloading the new release to the targets;
* **Symlink Shared** and **Symlink**: after deploying the new release, the `current` symbolic link is modified to point to this new release;
* **Clean Up**: to do some clean up (remove old versions).
</div>
</div>

---
<style scoped>
code {
  font-size: 0.6em;
}
</style>
# Introduction

The skeleton of a deployment with Ansistrano looks like this:

```
/var/www/site/
├── current -> ./releases/20210718100000Z
├── releases
│   └── 20210718100000Z
│       ├── css -> ../../shared/css/
│       ├── img -> ../../shared/img/
│       └── REVISION
├── repo
└── shared
    ├── css/
    └── img/
```

---
#

<br/>
<br/>
<br/>

You can find all the Ansistrano documentation on its Github repository (https://github.com/ansistrano/deploy).

---
# Deploying the software

For this, we will use the `ansistrano.deploy` role in a playbook dedicated to application deployment.

---
# Demo

Install the `ansistrano.deploy` role:

```
$ ansible-galaxy role install ansistrano.deploy
Starting galaxy role install process
- downloading role 'deploy', owned by ansistrano
- downloading role from https://github.com/ansistrano/deploy/archive/3.10.0.tar.gz
- extracting ansistrano.deploy to /home/ansible/.ansible/roles/ansistrano.deploy
- ansistrano.deploy (3.10.0) was installed successfully

```

---
<style scoped>
code {
  font-size: 0.6em;
}
</style>
# Demo

Create a playbook `playbook-deploy.yml` to manage deployments:

```
---
- hosts: ansible_clients
  become: yes
  become_user: root
  vars:
    dest: "/var/www/site/"
    ansistrano_deploy_via: "git"
    ansistrano_git_repo: https://github.com/alemorvan/demo-ansible.git
    ansistrano_deploy_to: "{{ dest }}"

  roles:
     - { role: ansistrano.deploy }
```

---
#
```
$ ansible-playbook playbook-deploy.yml

PLAY [ansible_clients] *********************************************************

TASK [ansistrano.deploy : ANSISTRANO | Ensure deployment base path exists] *****
TASK [ansistrano.deploy : ANSISTRANO | Ensure releases folder exists]
TASK [ansistrano.deploy : ANSISTRANO | Ensure shared elements folder exists]
TASK [ansistrano.deploy : ANSISTRANO | Ensure shared paths exists]
TASK [ansistrano.deploy : ANSISTRANO | Ensure basedir shared files exists]
TASK [ansistrano.deploy : ANSISTRANO | Get release version] ********************
TASK [ansistrano.deploy : ANSISTRANO | Get release path]
TASK [ansistrano.deploy : ANSISTRANO | GIT | Register ansistrano_git_result variable]
TASK [ansistrano.deploy : ANSISTRANO | GIT | Set git_real_repo_tree]
TASK [ansistrano.deploy : ANSISTRANO | GIT | Create release folder]
TASK [ansistrano.deploy : ANSISTRANO | GIT | Sync repo subtree[""] to release path]
TASK [ansistrano.deploy : ANSISTRANO | Copy git released version into REVISION file]
TASK [ansistrano.deploy : ANSISTRANO | Ensure shared paths targets are absent]
TASK [ansistrano.deploy : ANSISTRANO | Create softlinks for shared paths and files]
TASK [ansistrano.deploy : ANSISTRANO | Ensure .rsync-filter is absent]
TASK [ansistrano.deploy : ANSISTRANO | Setup .rsync-filter with shared-folders]
TASK [ansistrano.deploy : ANSISTRANO | Get current folder]
TASK [ansistrano.deploy : ANSISTRANO | Remove current folder if it's a directory]
TASK [ansistrano.deploy : ANSISTRANO | Change softlink to new release]
TASK [ansistrano.deploy : ANSISTRANO | Clean up releases]

PLAY RECAP *******************************************************************************************************
192.168.1.11               : ok=25   changed=8    unreachable=0    failed=0    skipped=14   rescued=0    ignored=0   
```

---
# Demo

So many things done with only 11 lines of code!

```
$ curl http://192.168.1.11
<html>
<head>
<title>Demo Ansible</title>
</head>
<body>
<h1>Version Master</h1>
</body>
<html>
```

---
<style scoped>
li {
  font-size: 0.8em;
}
</style>
# Demo

Checking on the remote server:

<div class="columns">
<div>

```
$ tree /var/www/site/
/var/www/site
├── current -> ./releases/20210722155312Z
├── releases
│   └── 20210722155312Z
│       ├── REVISION
│       └── html
│           └── index.htm
├── repo
│   └── html
│       └── index.htm
└── shared
```

</div>
<div>

Please note:

* the `current` symlink to the release `./releases/20210722155312Z`
* the presence of a directory `shared`
* the presence of the git repos in `./repo/`

</div>
</div>

---
# Demo
<style scoped>
code {
  font-size: 0.4em;
}
</style>
Restart the deployment **3** times, then check on the client.

<div class="columns">
<div>

```
$ tree /var/www/site/
var/www/site
├── current -> ./releases/20210722160048Z
├── releases
│   ├── 20210722155312Z
│   │   ├── REVISION
│   │   └── html
│   │       └── index.htm
│   ├── 20210722160032Z
│   │   ├── REVISION
│   │   └── html
│   │       └── index.htm
│   ├── 20210722160040Z
│   │   ├── REVISION
│   │   └── html
│   │       └── index.htm
│   └── 20210722160048Z
│       ├── REVISION
│       └── html
│           └── index.htm
├── repo
│   └── html
│       └── index.htm
└── shared
```

</div>
<div>

Please note:

* `ansistrano` kept the 4 last releases,
* the `current` link linked now to the lastest release

</div>
</div>

---
# Limit the number of releases

The `ansistrano_keep_releases` variable is used to specify the number of releases to keep.

---
<style scoped>
code {
  font-size: 0.65em;
}
</style>
Using the `ansistrano_keep_releases` variable, keep only 3 releases of the project. Check.

```
---
- hosts: ansible_clients
  become: yes
  become_user: root
  vars:
    dest: "/var/www/site/"
    ansistrano_deploy_via: "git"
    ansistrano_git_repo: https://github.com/alemorvan/demo-ansible.git
    ansistrano_deploy_to: "{{ dest }}"
    ansistrano_keep_releases: 3

  roles:
     - { role: ansistrano.deploy }
```

---
<style scoped>
code {
  font-size: 0.4em;
}
</style>
#
On the remote server:

```
$ tree /var/www/site/
/var/www/site
├── current -> ./releases/20210722160318Z
├── releases
│   ├── 20210722160040Z
│   │   ├── REVISION
│   │   └── html
│   │       └── index.htm
│   ├── 20210722160048Z
│   │   ├── REVISION
│   │   └── html
│   │       └── index.htm
│   └── 20210722160318Z
│       ├── REVISION
│       └── html
│           └── index.htm
├── repo
│   └── html
│       └── index.htm
└── shared
```

---
<style scoped>
code {
  font-size: 0.5em;
}
</style>
# Using shared_paths and shared_files

```
---
- hosts: ansible_clients
  become: yes
  become_user: root
  vars:
    dest: "/var/www/site/"
    ansistrano_deploy_via: "git"
    ansistrano_git_repo: https://github.com/alemorvan/demo-ansible.git
    ansistrano_deploy_to: "{{ dest }}"
    ansistrano_keep_releases: 3
    ansistrano_shared_paths:
      - "img"
      - "css"
    ansistrano_shared_files:
      - "logs"

  roles:
     - { role: ansistrano.deploy }
```

---

On the remote server, create the file `logs` in the `shared` directory:

```
sudo touch /var/www/site/shared/logs
```

Then execute the playbook:

```
TASK [ansistrano.deploy : ANSISTRANO | Ensure shared paths targets are absent] *******************************************************
ok: [192.168.10.11] => (item=img)
ok: [192.168.10.11] => (item=css)
ok: [192.168.10.11] => (item=logs/log)

TASK [ansistrano.deploy : ANSISTRANO | Create softlinks for shared paths and files] **************************************************
changed: [192.168.10.11] => (item=img)
changed: [192.168.10.11] => (item=css)
changed: [192.168.10.11] => (item=logs)
```

---
<style scoped>
code {
  font-size: 0.4em;
}
li {
  font-size: 1em;
}
</style>
On the remote server:

<div class="columns">
<div>

```
$  tree -F /var/www/site/
/var/www/site/
├── current -> ./releases/20210722160631Z/
├── releases/
│   ├── 20210722160048Z/
│   │   ├── REVISION
│   │   └── html/
│   │       └── index.htm
│   ├── 20210722160318Z/
│   │   ├── REVISION
│   │   └── html/
│   │       └── index.htm
│   └── 20210722160631Z/
│       ├── REVISION
│       ├── css -> ../../shared/css/
│       ├── html/
│       │   └── index.htm
│       ├── img -> ../../shared/img/
│       └── logs -> ../../shared/logs
├── repo/
│   └── html/
│       └── index.htm
└── shared/
    ├── css/
    ├── img/
    └── logs
```

</div>
<div>

Please note that the last release contains 3 links:  `css`, `img`, and `logs`

from `/var/www/site/releases/css` to the `../../shared/css/` directory.
from `/var/www/site/releases/img` to the `../../shared/img/` directory.
from `/var/www/site/releases/logs` to the `../../shared/logs` file.
  
</div>
</div>

---
#

Therefore, the files contained in these 2 folders and the `logs` file are always accessible via the following paths:

* `/var/www/site/current/css/`,
* `/var/www/site/current/img/`,
* `/var/www/site/current/logs`,

but above all they will be kept from one release to the next.

---
# Managing git branch or tags

The `ansistrano_git_branch` variable is used to specify a `branch` or `tag` to deploy.

---
<style scoped>
code {
  font-size: 0.6em;
}
</style>
Deploy the `releases/v1.1.0` branch:

```
---
- hosts: ansible_clients
  become: yes
  become_user: root
  vars:
    dest: "/var/www/site/"
    ansistrano_deploy_via: "git"
    ansistrano_git_repo: https://github.com/alemorvan/demo-ansible.git
    ansistrano_deploy_to: "{{ dest }}"
    ansistrano_keep_releases: 3
    ...
    ansistrano_git_branch: 'releases/v1.1.0'

  roles:
     - { role: ansistrano.deploy }
```

---
#

> You can have fun, during the deployment, refreshing your browser, to see in 'live' the change.

```
$ curl http://192.168.1.11
<html>
<head>
<title>Demo Ansible</title>
</head>
<body>
<h1>Version 1.0.1</h1>
</body>
<html>
```

---
<style scoped>
code {
  font-size: 0.6em;
}
</style>
* Deploy the `v2.0.0` tag:

```
---
- hosts: ansible_clients
  become: yes
  become_user: root
  vars:
    dest: "/var/www/site/"
    ansistrano_deploy_via: "git"
    ansistrano_git_repo: https://github.com/alemorvan/demo-ansible.git
    ansistrano_deploy_to: "{{ dest }}"
    ansistrano_keep_releases: 3
    ...
    ansistrano_git_branch: 'v2.0.0'

  roles:
     - { role: ansistrano.deploy }
```

---
#

```
$ curl http://192.168.1.11
<html>
<head>
<title>Demo Ansible</title>
</head>
<body>
<h1>Version 2.0.0</h1>
</body>
<html>
```

---
# Actions between deployment steps

A deployment with Ansistrano respects the following steps:

<div class="columns">
<div>

* `Setup`
* `Update Code`
* `Symlink Shared`
* `Symlink`
* `Clean Up`

</div>
<div>

![right:50% w:500](./assets/chapter5/ansistrano-001.png)

</div>
</div>

---
# 

It is possible to intervene before and after each of these steps.

A tasks file can be included through the variables provided for this purpose:

* `ansistrano_before_<task>_tasks_file`
* or `ansistrano_after_<task>_tasks_file`

---
<style scoped>
code {
  font-size: 0.6em;
}
</style>
Easy example: send an email (or whatever you want like Slack or Mattermost notification) at the beginning of the deployment:

```
---
- hosts: ansible_clients
  become: yes
  become_user: root
  vars:
    dest: "/var/www/site/"
    ...
    ansistrano_git_branch: 'v2.0.0'
    ansistrano_before_setup_tasks_file: "{{ playbook_dir }}/deploy/before-setup-tasks.yml"

  roles:
     - { role: ansistrano.deploy }
```
---
# 
Create the file `deploy/before-setup-tasks.yml`:

```
---
- name: Send a mail
  mail:
    subject: Starting deployment on {{ ansible_hostname }}.
  delegate_to: localhost
```

```
TASK [ansistrano.deploy : include] *************************************************************************************
included: /home/ansible/deploy/before-setup-tasks.yml for 192.168.10.11

TASK [ansistrano.deploy : Send a mail] *************************************************************************************
ok: [192.168.10.11 -> localhost]
```

---
<style scoped>
code {
  font-size: 0.6em;
}
</style>
#

You will probably have to restart some services at the end of the deployment, to flush caches for example. Let's restart Apache at the end of the deployment:

```
---
- hosts: ansible_clients
  become: yes
  become_user: root
  vars:
    dest: "/var/www/site/"
    ... 
    ansistrano_git_branch: 'v2.0.0'
    ansistrano_before_setup_tasks_file: "{{ playbook_dir }}/deploy/before-setup-tasks.yml"
    ansistrano_after_symlink_tasks_file: "{{ playbook_dir }}/deploy/after-symlink-tasks.yml"

  roles:
     - { role: ansistrano.deploy }
```

---
# 

Create the file `deploy/after-symlink-tasks.yml`:

```
---
- name: restart apache
  systemd:
    name: httpd
    state: restarted
```

```
TASK [ansistrano.deploy : include] *************************************************************************************
included: /home/ansible/deploy/after-symlink-tasks.yml for 192.168.10.11

TASK [ansistrano.deploy : restart apache] **************************************************************************************
changed: [192.168.10.11]
```

---
#

As you have seen during this chapter, Ansible can greatly improve the life of the system administrator. Very intelligent roles like Ansistrano are "must haves" that quickly become indispensable.

Using Ansistrano, ensures that good deployment practices are respected, reduces the time needed to put a system into production, and avoids the risk of potential human errors. The machine works fast, well, and rarely makes mistakes!


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

[Next Chapter >>](./Learning_Ansible_with_Rocky-6-Ansible_Large_scale_infrastructure.html)

</div>
</div>