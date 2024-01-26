---
marp: true
theme: gaia
style: |
  @import url('../assets/css/rocky-theme.css');
_class: lead
paginate: true
markdown.marp.enableHtml: true
header: '![w:300](../assets/rocky_logo_white.png) [Back to menu](./index.html)'
footer: '**Rocky Linux Academy > Ansible courses > 6 - Large scale infrastructure**'
---

# 6 - Large scale infrastructure

![bg opacity:.5](../assets/rocky_linux_logo.svg)

<div class="intro">

## Learning Ansible with Rocky

</div>

---

## Objectives

<i class="fa-pull-right fa-4x">![w:200 opacity:50%](../assets/images/objectives.png)</i>

In this chapter you will learn how to scale your configuration management system.

<i class="fa fa-check"></i> Organize your code for large infrastructure;   
<i class="fa fa-check"></i> Apply all or part of your configuration management to a group of nodes;   

---
<div class="plan_header">

## Plan

<div class="plan columns">

<i class="fa fa-book"></i> [Variables storage](#10)
<i class="fa fa-book"></i> [About Ansible tags](#18)
<i class="fa fa-book"></i> [About the directory layout](#24)
<i class="fa fa-book"></i> [Tests](#34)
<i class="fa fa-book"></i> [Benefits](#43)

</div>
</div>

---
#
<br/>
<br/>
<br/>

We have seen in the previous chapters how to organize our code in the form of roles but also how to use some roles for the management of updates (patch management) or the deployment of code.

What about configuration management? How to manage the configuration of tens, hundreds, or even thousands of virtual machines with Ansible?

---
#
<br/>
<br/>
<br/>

The advent of the cloud has changed the traditional methods a bit. The VM is configured at deployment. If its configuration is no longer compliant, it is destroyed and replaced by a new one.

---
#
<br/>
<br/>
<br/>

The organization of the configuration management system presented in this chapter will respond to these two ways of consuming IT: "one-shot" use or regular "re-configuration" of a fleet.

---
#
<br/>
<br/>
<br/>

However, be careful: using Ansible to ensure park compliance requires changing work habits. It is no longer possible to manually modify the configuration of a service manager without seeing these modifications overwritten the next time Ansible is run.

---
#
<br/>
<br/>
<br/>

> What we are going to set up below is not Ansible's favorite terrain. Technologies like Puppet or Salt will do much better. Let's remember that Ansible is a Swiss army knife of automation and is agentless, which explains the differences in performance.

---
#
<br/>
<br/>
<br/>

> More information can be found at https://docs.ansible.com/ansible/latest/user_guide/sample_setup.html

---
<br/>
<br/>
<br/>

# Variables storage

---
# Variables storage

The first thing we have to discuss is the separation between data and Ansible code.

As the code gets larger and more complex, it will be more and more complicated to modify the variables it contains.

To ensure the maintenance of your site, the most important thing is correctly separating the variables from the Ansible code.

---
# Variables storage

We haven't discussed it here yet, but you should know that Ansible can automatically load the variables it finds in specific folders depending on the inventory name of the managed node, or its member groups.

---
# Variables storage

The Ansible documentation suggests that we organize our code as below:

```
inventories/
   production/
      hosts               # inventory file for production servers
      group_vars/
         group1.yml       # here we assign variables to particular groups
         group2.yml
      host_vars/
         hostname1.yml    # here we assign variables to particular systems
         hostname2.yml
```

---
# Variables storage

If the targeted node is `hostname1` of `group1`, the variables contained in the `hostname1.yml` and `group1.yml` files will be automatically loaded. It's a nice way to store all the data for all your roles in the same place.

---
# Variables storage

> In this way, the inventory file of your server becomes its identity card. It contains all the variables that differ from the default variables for your server.

---
# Variables storage

From the point of view of centralization of variables, it becomes essential to organize the naming of its variables in the roles by prefixing them, for example, with the name of the role. It is also recommended to use flat variable names rather than dictionaries.

For example, if you want to make the `PermitRootLogin` value in the `sshd_config` file a variable, a good variable name could be `sshd_config_permitrootlogin` (instead of `sshd.config.permitrootlogin` which could also be a good variable name).

---
<br/>
<br/>
<br/>


# Questions ?

---
<br/>
<br/>
<br/>

# About Ansible tags

---
# About Ansible tags

The use of Ansible tags allows you to execute or skip a part of the tasks in your code.

---
# About Ansible tags
<style scoped>
code {
  font-size: 0.6em;
}
</style>

For example, let's modify our users creation task:

```
- name: add users
  user:
    name: "{{ item }}"
    state: present
    groups: "users"
  loop:
     - antoine
     - patrick
     - steven
     - xavier
  tags: users
```

---
# About Ansible tags

You can now play only the tasks with the tag `users` with the `ansible-playbook` option `--tags`:

```
ansible-playbook -i inventories/production/hosts --tags users site.yml
```

You can also use the `--skip-tags` option.

```
ansible-playbook -i inventories/production/hosts --skip-tags groups --tags users site.yml
```

---
# About Ansible tags

> More information can be found at https://docs.ansible.com/ansible/latest/user_guide/playbooks_tags.html

---
<br/>
<br/>
<br/>


# Questions ?

---
<br/>
<br/>
<br/>

# About the directory layout

---
# About the directory layout

Let's focus on a proposal for the organization of files and directories necessary for the proper functioning of a CMS (Content Management System).

---
# About the directory layout
<style scoped>
code {
  font-size: 0.6em;
}
</style>
Our starting point will be the `site.yml` file. This file is a bit like the orchestra conductor of the CMS since it will only include the necessary roles for the target nodes if needed:

```
---
- name: "Config Management for {{ target }}"
  hosts: "{{ target }}"

  roles:

    - role: roles/functionality1

    - role: roles/functionality2
```

---
# About the directory layout

Of course, those roles must be created under the `roles` directory at the same level as the `site.yml` file.

---
<style scoped>
code {
  font-size: 0.5em;
}
</style>
# About the directory layout

I like to manage my global vars inside a `vars/global_vars.yml`, even if I could store them inside a file located at `inventories/production/group_vars/all.yml`

```
---
- name: "Config Management for {{ target }}"
  hosts: "{{ target }}"
  vars_files:
    - vars/global_vars.yml
  roles:

    - role: roles/functionality1

    - role: roles/functionality2
```

---
<style scoped>
code {
  font-size: 0.6em;
}
</style>

I also like to keep the possibility of disabling a functionality. So I include my roles with a condition and a default value like this:

```
---
- name: "Config Management for {{ target }}"
  hosts: "{{ target }}"
  vars_files:
    - vars/global_vars.yml
  roles:

    - role: roles/functionality1
      when:
        - enable_functionality1|default(true)

    - role: roles/functionality2
      when:
        - enable_functionality2|default(false)
```

---
<style scoped>
code {
  font-size: 0.5em;
}
</style>

Don't forget to use the tags:


```
- name: "Config Management for {{ target }}"
  hosts: "{{ target }}"
  vars_files:
    - vars/global_vars.yml
  roles:

    - role: roles/functionality1
      when:
        - enable_functionality1|default(true)
      tags:
        - functionality1

    - role: roles/functionality2
      when:
        - enable_functionality2|default(false)
      tags:
        - functionality2
```

---
<style scoped>
code {
  font-size: 0.4em;
}
</style>

You should get something like this:

```
$ tree cms
cms
├── inventories
│   └── production
│       ├── group_vars
│       │   └── plateform.yml
│       ├── hosts
│       └── host_vars
│           ├── client1.yml
│           └── client2.yml
├── roles
│   ├── functionality1
│   │   ├── defaults
│   │   │   └── main.yml
│   │   └── tasks
│   │       └── main.yml
│   └── functionality2
│       ├── defaults
│       │   └── main.yml
│       └── tasks
│           └── main.yml
├── site.yml
└── vars
    └── global_vars.yml
```

---
#

<br/>
<br/>
<br/>

> You are free to develop your roles within a collection


---
<br/>
<br/>
<br/>


# Questions ?

---
<br/>
<br/>
<br/>

# Tests

---
<style scoped>
code {
  font-size: 0.4em;
}
</style>
# Tests

Let's launch the playbook and run some tests:

```
$ ansible-playbook -i inventories/production/hosts -e "target=client1" site.yml

PLAY [Config Management for client1] ****************************************************************************

TASK [Gathering Facts] ******************************************************************************************
ok: [client1]

TASK [roles/functionality1 : Task in functionality 1] *********************************************************
ok: [client1] => {
    "msg": "You are in functionality 1"
}

TASK [roles/functionality2 : Task in functionality 2] *********************************************************
skipping: [client1]

PLAY RECAP ******************************************************************************************************
client1                    : ok=2    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0   
```

---

As you can see, by default, only the tasks of the `functionality1` role are played.

---
Let's activate in the inventory the `functionality2` for our targeted node and rerun the playbook:

```
$ vim inventories/production/host_vars/client1.yml
---
enable_functionality2: true
```

---
<style scoped>
code {
  font-size: 0.4em;
}
</style>
#

```
$ ansible-playbook -i inventories/production/hosts -e "target=client1" site.yml

PLAY [Config Management for client1] ****************************************************************************

TASK [Gathering Facts] ******************************************************************************************
ok: [client1]

TASK [roles/functionality1 : Task in functionality 1] *********************************************************
ok: [client1] => {
    "msg": "You are in functionality 1"
}

TASK [roles/functionality2 : Task in functionality 2] *********************************************************
ok: [client1] => {
    "msg": "You are in functionality 2"
}

PLAY RECAP ******************************************************************************************************
client1                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

---
#

Try to apply only `functionality2`:

```
$ ansible-playbook -i inventories/production/hosts -e "target=client1" --tags functionality2 site.yml

PLAY [Config Management for client1] ****************************************************************************

TASK [Gathering Facts] ******************************************************************************************
ok: [client1]

TASK [roles/functionality2 : Task in functionality 2] *********************************************************
ok: [client1] => {
    "msg": "You are in functionality 2"
}

PLAY RECAP ******************************************************************************************************
client1                    : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

---
<style scoped>
code {
  font-size: 0.4em;
}
</style>
Let's run on the whole inventory:

```
$ ansible-playbook -i inventories/production/hosts -e "target=plateform" site.yml

PLAY [Config Management for plateform] **************************************************************************

TASK [Gathering Facts] ******************************************************************************************
ok: [client1]
ok: [client2]

TASK [roles/functionality1 : Task in functionality 1] *********************************************************
ok: [client1] => {
    "msg": "You are in functionality 1"
}
ok: [client2] => {
    "msg": "You are in functionality 1"
}

TASK [roles/functionality2 : Task in functionality 2] *********************************************************
ok: [client1] => {
    "msg": "You are in functionality 2"
}
skipping: [client2]

PLAY RECAP ******************************************************************************************************
client1                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
client2                    : ok=2    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0   
```

---
#

As you can see, `functionality2` is only played on the `client1`.

---
<br/>
<br/>
<br/>


# Questions ?

---
<br/>
<br/>
<br/>

# Benefits

---
<style scoped>
li {
  font-size: 0.9em;
}
</style>
# Benefits

By following the advice given in the Ansible documentation, you will quickly obtain a:

* easily maintainable source code even if it contains a large number of roles
* a relatively fast, repeatable compliance system that you can apply partially or completely
* can be adapted on a case-by-case basis and by servers
* the specifics of your information system are separated from the code, easily audit-able, and centralized in the inventory files of your configuration management.


---
<br/>
<br/>
<br/>


# Questions ?

---
#

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

<i class="button">[Next Chapter >>](./Learning_Ansible_with_Rocky-7-Ansible_Working_with_filters.html)</i>
