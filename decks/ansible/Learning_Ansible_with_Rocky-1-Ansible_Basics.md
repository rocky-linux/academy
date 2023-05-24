---
marp: true
theme: gaia
_class: lead
paginate: true
markdown.marp.enableHtml: true

backgroundColor: #fff

header: Learning Ansible with Rocky | 1 - Ansible Basics
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

# 1 - Ansible Basics
## Learning Ansible with Rocky

---
<br/>

# <i class="fa-solid fa-trophy"></i> Objectives

In this chapter you will learn how to work with Ansible.

:heavy_check_mark: Implement Ansible;
:heavy_check_mark: Apply configuration changes on a server;
:heavy_check_mark: Create first Ansible playbooks;

---
<br/>

# Plan

* [Generalities](#4)
* [Installation](#12)
* [Ansible CLI](#20)
* [Deployment](#30)
* [The modules](#46)
* [Playbooks](#59)
---
#

Ansible centralizes and automates administration tasks. It is:

* agentless
* idempotent
* SSH Protocol (Linux), WinRM Protocol (Windows), API calls

---
#

<br/>
<br/>
<br/>

<i class="fa-solid fa-circle-exclamation"></i> The opening of SSH or WinRM flows to all clients from the Ansible server, makes it a **critical element of the architecture** that must be carefully monitored.



---
#

Ansible can manage differents OS, network equipments, and even containers!

* Linux,
* Windows,
* Docker,
* Network (junos, fortios, ...)
* ...

---
### Ansible functionalities

<div class="columns">
<div>

![right:50% w:500](./assets/chapter1/life-cycle.png)

</div>
<div>

Ansible is "push-based" (stateless).

</div>
</div>

---

### A little word about devops

<div class="columns">

<div>
Optimize the work of all the teams:

  * build
  * run
  * change
</div>
<div>

![right:20% w:250](./assets/chapter1/devops.png)
</div>

</div>
implementing continuous integration/deployment

---
#

<br/>
<br/>
<br/>

To offer a graphical interface to your daily use of Ansible, you can install some tools like Ansible Tower (RedHat), which is not free, its opensource counterpart Awx, or other projects like Jenkins and the excellent Rundeck can also be used.

---
### The Ansible vocabulary

The management machine is the server on which Ansible is installed (no software is deployed on the managed servers.).

<div class="columns">
<div>

* task
* module
* inventory
* playbook
</div>
<div>

* role
* fact
* handler
* collection

</div>
</div>

<!-- 
The management machine: the machine on which Ansible is installed. Since Ansible is agentless, no software is deployed on the managed servers.
The inventory: a file containing information about the managed servers.
The tasks: a task is a block defining a procedure to be executed (e.g., create a user or a group, install a software package, etc.).
A module: a module abstracts a task. There are many modules provided by Ansible.
The playbooks: a simple file in yaml format defining the target servers and the tasks to be performed.
A role: a role allows you to organize the playbooks and all the other necessary files (templates, scripts, etc.) to facilitate the sharing and reuse of code.
A collection: a collection includes a logical set of playbooks, roles, modules, and plugins.
The facts: these are global variables containing information about the system (machine name, system version, network interface and configuration, etc.).
The handlers: these are used to cause a service to be stopped or restarted in the event of a change.
-->


---
<br/>
<br/>
<br/>


# Questions ?

---
<br/>
<br/>
<br/>

# Installation on the management server

---
#
Ansible is available in the repositories of the main distributions.

On Rocky 9 / RHEL 9 (EPEL repo) :

```bash
sudo dnf install epel-release
sudo dnf makecache
sudo dnf install ansible 
```

On Debian (Launchpad repo) :

```bash
sudo apt-get install ansible
```

---
# Configuration files

The server configuration is located under `/etc/ansible`

The main configuration file (commands, modules, plugins, and ssh configuration):

```bash
/etc/ansible/ansible.cfg
```

The inventory file: (declaration of clients and groups):

```bash
/etc/ansible/hosts
```

---
# The main configuration file

`ansible-config` command generate a new configuration file:

```bash
usage: ansible-config [-h] [--version] [-v] {list,dump,view,init} ...

View ansible configuration.

positional arguments:
  {list,dump,view,init}
    list                Print all config options
    dump                Dump configuration
    view                View configuration file
    init                Create initial configuration
```

---
# The main configuration file

Example:

```bash
ansible-config init --disabled > /etc/ansible/ansible.cfg
```

---
# The inventory file

The inventory file can be written in different formats (including yaml):

Creation of a `Rocky9` group containing 2 targets:

```bash
[Rocky9]
172.16.1.210
172.16.1.211
```

---

# The inventory file

Creating a group of groups:

```bash
[rocky:children]
rocky8
rocky9
```


---
<br/>
<br/>
<br/>


# Questions ?

---
<br/>
<br/>
<br/>

# Ansible CLI

---
# ansible command line usage
<style scoped>
table {
  font-size: 0.5em;
}
</style>

The ansible command launches a task on one or more target hosts.

```bash
ansible <host-pattern> [-m module_name] [-a args] [options]
```

| Option | Information |
|--------|-------------|
| -m module	             | Runs the module called|
| -a 'arguments'         | The arguments to pass to the module. |
| -b -K	                 | Requests a password and runs the command with higher privileges. |
| --user=username	       | Uses this user to connect to the target host instead of the current user. | 
| --become-user=username | Executes the operation as this user (default: root). | 
| -C	                   | Simulation. Does not make any changes to the target but tests it to see what should be changed.| 

---
#

<i class="fa-solid fa-circle-exclamation"></i> Since we have not yet configured authentication on our 2 test servers, not all the following examples will work. They are given as examples to facilitate understanding, and will be fully functional later in this chapter.

---
#

List the hosts belonging to the rocky9 group:

```bash
ansible rocky9 --list-hosts
```

---
#

Ping a host group with the ping module:

```bash
ansible rocky9 -m ping
```

---
#

Display facts from a host group with the setup module:

```bash
ansible rocky9 -m setup
```

---
#

Run a command on a host group by invoking the command module with arguments:

```bash
ansible rocky9 -m command -a 'uptime'
```

---
#

Run a command with administrator privileges:

```bash
ansible rocky9 --become -m command -a 'reboot'
```

---
#

Run a command using a custom inventory file:

```bash
ansible rocky9 -i ./local-inventory -m command -a 'date'
```

> As in this example, it is sometimes simpler to separate the declaration of managed devices into several files (by cloud project for example) and provide Ansible with the path to these files, rather than to maintain a long inventory file.

---
<br/>
<br/>
<br/>


# Questions ?

---
<br/>
<br/>
<br/>

# Deployment

---
# Preparing the client

On both management machine and clients, we will create an ansible user dedicated to the operations performed by Ansible. This user will have to use sudo rights, so it will have to be added to the wheel group.

---
# Preparing the client

This user will be used:

* On the administration station side: to run ansible commands and ssh to managed clients.
* On the managed stations (here the server that serves as your administration station also serves as a client, so it is managed by itself) to execute the commands launched from the administration station: it must therefore have sudo rights.

---
# Preparing the client

On both machines, create an ansible user, dedicated to ansible:

```bash
$ sudo useradd ansible
$ sudo usermod -aG wheel ansible
```

Set a password for this user:

```bash
$ sudo passwd ansible
```

---
# Preparing the client

Modify the `sudoers` config to allow members of the `wheel` group to sudo without password:

```bash
$ sudo visudo
```

---
# Preparing the client

Our goal here is to comment out the default, and uncomment the `NOPASSWD` option so that these lines look like this when we are done:

```bash
## Allows people in group wheel to run all commands
# %wheel  ALL=(ALL)       ALL

## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL
```

---
# Test with the ping module

By default, password login is not allowed by Ansible.

Uncomment the following line from the `[defaults]` section in the `/etc/ansible/ansible.cfg` configuration file and set it to `True`:

```bash
ask_pass      = True
```

---
# Test with the ping module

When using management from this point on, start working with this new user:

```bash
$ sudo su - ansible
```

---
# Test with the ping module

Run a ping on each server of the rocky9 group:

```bash
SHELL > ansible rocky9 -m ping
SSH password:
172.16.1.10 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
172.16.1.11 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

---
#

You are asked for the ansible password of the remote servers, which is a security problem...

You can now test the commands that didn't work previously in this chapter.

---
# Key authentication

Password authentication will be replaced by a much more secure private/public key authentication.

---
# Creating an SSH key

The dual-key will be generated with the command ssh-keygen on the **management station by the ansible user**:

```bash
SHELL > ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ansible/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ansible/.ssh/id_rsa.
Your public key has been saved in /home/ansible/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:Oa1d2hYzzdO0e/K10XPad25TA1nrSVRPIuS4fnmKr9g ansible@localhost.localdomain
The key's randomart image is:
+---[RSA 3072]----+
|           .o . +|
|           o . =.|
|          . . + +|
|         o . = =.|
|        S o = B.o|
|         = + = =+|
|        . + = o+B|
|         o + o *@|
|        . Eoo .+B|
+----[SHA256]-----+
```

---
# Creating an SSH key

The public key can be copied to the servers:

```bash
# ssh-copy-id ansible@172.16.1.10
# ssh-copy-id ansible@172.16.1.11
```

Re-comment the following line from the `[defaults]` section in the `/etc/ansible/ansible.cfg` configuration file to prevent password authentication

```bash
# ask_pass      = True
```
---

# Private key authentication test

For the next test, the shell module, allowing remote command execution, is used:

```bash
# ansible rocky8 -m shell -a "uptime"
172.16.1.10 | SUCCESS | rc=0 >>
 12:36:18 up 57 min,  1 user,  load average: 0.00, 0.00, 0.00

172.16.1.11 | SUCCESS | rc=0 >>
 12:37:07 up 57 min,  1 user,  load average: 0.00, 0.00, 0.00
```
No password is required, private/public key authentication works!

---
# 

<i class="fa-solid fa-circle-exclamation"></i> In production environment, you should now remove the `ansible` passwords previously set to enforce your security (as now an authentication password is not necessary).

---
<br/>
<br/>
<br/>


# Questions ?

---
<br/>
<br/>
<br/>

# The modules

---
# The modules

The list of modules classified by category can be found [here](https://docs.ansible.com/ansible/latest/collections/index_module.html). 

Ansible offers more than 750!

The modules are now grouped into module collections, a list of which can be found [here](https://docs.ansible.com/ansible/latest/collections/index.html).

> Collections are a distribution format for Ansible content that can include playbooks, roles, modules, and plugins.

---
# The modules

A module is invoked with the `-m` option of the `ansible` command:

```
ansible <host-pattern> [-m module_name] [-a args] [options]
```

There is a module for almost every need! It is thus advised, instead of using the shell module, to look for a module adapted to the need.

---
<style scoped>
table {
  font-size: 0.7em;
}
</style>
Each category of need has its own module. Here is a non-exhaustive list:

| Type                | Examples                                                     |
|---------------------|--------------------------------------------------------------|
| System Management   | `user` (users management), `group` (groups management), etc. |
| Software management | `dnf`,`yum`, `apt`, `pip`, `npm`                             |
| File management     | `copy`, `fetch`, `lineinfile`, `template`, `archive`         |
| Database management | `mysql`, `postgresql`, `redis`                               |
| Cloud management    | `amazon S3`, `cloudstack`, `openstack`                       |
| Cluster management  | `consul`, `zookeeper`                                        |
| Send commands       |  `shell`, `script`, `expect`                                 |
| Downloads           |  `get_url`                                                   |
| Source management   |  `git`, `gitlab`                                             |

---
# Example of software installation
<style scoped>
code {
  font-size: 0.4em;
}
</style>

The `dnf` module allows for the installation of software on the targets:

```
# ansible rocky8 --become -m dnf -a name="httpd"
172.16.1.10 | SUCCESS => {
    "changed": true,
    "msg": "",
    "rc": 0,
    "results": [
      ...
      \n\nComplete!\n"
    ]
}
172.16.1.11 | SUCCESS => {
    "changed": true,
    "msg": "",
    "rc": 0,
    "results": [
      ...
    \n\nComplete!\n"
    ]
}
```

---
# Example of software installation
<style scoped>
code {
  font-size: 0.6em;
}
</style>
The installed software being a service, it is now necessary to start it with the module `systemd`:

```
# ansible rocky8 --become  -m systemd -a "name=httpd state=started"
172.16.1.10 | SUCCESS => {
    "changed": true,
    "name": "httpd",
    "state": "started"
}
172.16.1.11 | SUCCESS => {
    "changed": true,
    "name": "httpd",
    "state": "started"
}
```

---
#

Try to launch those last 2 commands twice. You will observe that the first time Ansible will take actions to reach the state set by the command. The second time, it will do nothing because it will have detected that the state is already reached!

---
<br/>
<br/>
<br/>


# Questions ?

---
# Exercises
<style scoped>
li {
  font-size: 0.7em;
}
</style>


<div class="columns">
<div>
To help discover more about Ansible and to get used to searching the Ansible documentation, here are some exercises you can do before going on:

Do not use the shell module. Look in the documentation for the appropriate modules!
</div>
<div>

* Create the groups Paris, Tokio, NewYork
* Create the user `supervisor`
* Change the user to have a uid of 10000
* Change the user so that it belongs to the Paris group
* Install the tree software
* Stop the crond service
* Create an empty file with `644` rights
* Update your client distribution
* Restart your client

</div>

</div>

---
# `setup` module: introduction to facts

The system facts are variables retrieved by Ansible via its `setup` module.

Take a look at the different facts of your clients to get an idea of the amount of information that can be easily retrieved via a simple command.

We'll see later how to use facts in our playbooks and how to create our own facts.

---
#

```
# ansible ansible_clients -m setup | less
192.168.1.11 | SUCCESS => {
    "ansible_facts": {
        "ansible_all_ipv4_addresses": [
            "192.168.1.11"
        ],
        "ansible_all_ipv6_addresses": [
            "2001:861:3dc3:fcf0:a00:27ff:fef7:28be",
            "fe80::a00:27ff:fef7:28be"
        ],
        "ansible_apparmor": {
            "status": "disabled"
        },
        "ansible_architecture": "x86_64",
        "ansible_bios_date": "12/01/2006",
        "ansible_bios_vendor": "innotek GmbH",
        "ansible_bios_version": "VirtualBox",
        "ansible_board_asset_tag": "NA",
        "ansible_board_name": "VirtualBox",
        "ansible_board_serial": "NA",
        "ansible_board_vendor": "Oracle Corporation",
        ...
```

---
#

Now that we have seen how to configure a remote server with Ansible on the command line, we will be able to introduce the notion of playbook. Playbooks are another way to use Ansible, which is not much more complex, but which will make it easier to reuse your code.

---
<br/>
<br/>
<br/>


# Questions ?

---
<br/>
<br/>
<br/>

# Playbooks

---
# Playbooks

Ansible's playbooks describe a policy to be applied to remote systems, to force their configuration.

Playbooks are written in an easily understandable text format that groups together a set of tasks: the `yaml` format.

Learn more about yaml at [https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html)

---
# Playbooks

Syntaxe:
```
ansible-playbook <file.yml> ... [options]
```

The options are identical to the `ansible` command.

---
# Example of Apache and MySQL playbook

The following playbook allows us to install Apache and MariaDB on our target servers.

---
<style scoped>
code {
  font-size: 0.5em;
}
</style>
Create a `test.yml` file with the following content:

```
---
- hosts: rocky8 <1>
  become: true <2>
  become_user: root

  tasks:

    - name: ensure apache is at the latest version
      dnf: name=httpd,php,php-mysqli state=latest

    - name: ensure httpd is started
      systemd: name=httpd state=started

    - name: ensure mariadb is at the latest version
      dnf: name=mariadb-server state=latest

    - name: ensure mariadb is started
      systemd: name=mariadb state=started
...
```

---
#

<1> The targeted group or the targeted server must exist in the inventory
<2> Once connected, the user becomes `root` (via `sudo` by default)

---
<style scoped>
code {
  font-size: 0.35em;
}
</style>
#

The execution of the playbook is done with the command `ansible-playbook`:

```
$ ansible-playbook test.yml

PLAY [rocky8] ****************************************************************

TASK [setup] ******************************************************************
ok: [172.16.1.10]
ok: [172.16.1.11]

TASK [ensure apache is at the latest version] *********************************
ok: [172.16.1.10]
ok: [172.16.1.11]

TASK [ensure httpd is started] ************************************************
changed: [172.16.1.10]
changed: [172.16.1.11]

TASK [ensure mariadb is at the latest version] **********************************
changed: [172.16.1.10]
changed: [172.16.1.11]

TASK [ensure mariadb is started] ***********************************************
changed: [172.16.1.10]
changed: [172.16.1.11]

PLAY RECAP *********************************************************************
172.16.1.10             : ok=5    changed=3    unreachable=0    failed=0
172.16.1.11             : ok=5    changed=3    unreachable=0    failed=0
```

---
#

For more readability, it is recommended to write your playbooks in full yaml format. 

In the previous example, the arguments are given on the same line as the module, the value of the argument following its name separated by an `=`. 

---
# 
<style scoped>
code {
  font-size: 0.35em;
}
</style>
Look at the same playbook in full yaml:

```
---
- hosts: rocky8
  become: true
  become_user: root

  tasks:

    - name: ensure apache is at the latest version
      dnf:
        name: httpd,php,php-mysqli
        state: latest

    - name: ensure httpd is started
      systemd:
        name: httpd
        state: started

    - name: ensure mariadb is at the latest version
      dnf:
        name: mariadb-server
        state: latest

    - name: ensure mariadb is started
      systemd:
        name: mariadb
        state: started
...
```

---
#

Note:     `dnf` is one of the modules that allow you to give it a list as argument.

```
    - name: ensure apache is at the latest version
      dnf:
        name:
          - httpd
          - php
          - php-mysqli
        state: latest
```

---
# Note about collections

Ansible now provides modules in the form of collections.

Some modules are provided by default within the `ansible.builtin` collection, others must be installed manually via the:

```
ansible-galaxy collection install [collectionname]
```

where [collectionname] is the name of the collection (the square brackets here are used to highlight the need to replace this with an actual collection name, and are NOT part of the command).

---
<style scoped>
code {
  font-size: 0.35em;
}
</style>
The previous example should be written like this:

```
---
- hosts: rocky8
  become: true
  become_user: root

  tasks:

    - name: ensure apache is at the latest version
      ansible.builtin.dnf:
        name: httpd,php,php-mysqli
        state: latest

    - name: ensure httpd is started
      ansible.builtin.systemd:
        name: httpd
        state: started

    - name: ensure mariadb is at the latest version
      ansible.builtin.dnf:
        name: mariadb-server
        state: latest

    - name: ensure mariadb is started
      ansible.builtin.systemd:
        name: mariadb
        state: started
...
```

---
<style scoped>
code {
  font-size: 0.30em;
}
</style>
A playbook is not limited to one target:

```
---
- hosts: webservers
  become: true
  become_user: root

  tasks:

    - name: ensure apache is at the latest version
      ansible.builtin.dnf:
        name: httpd,php,php-mysqli
        state: latest

    - name: ensure httpd is started
      ansible.builtin.systemd:
        name: httpd
        state: started

- hosts: databases
  become: true
  become_user: root

    - name: ensure mariadb is at the latest version
      ansible.builtin.dnf:
        name: mariadb-server
        state: latest

    - name: ensure mariadb is started
      ansible.builtin.systemd:
        name: mariadb
        state: started
...
```

---
# Code quality

You can check the syntax of your playbook:

```
$ ansible-playbook --syntax-check play.yml
```

---
# Code quality

You can also use a "linter" for yaml:

```
$ dnf install -y yamllint
```

then check the yaml syntax of your playbooks:

```
$ yamllint test.yml
test.yml
  8:1       error    syntax error: could not find expected ':' (syntax)
```

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

[Next Chapter >>](./Learning_Ansible_with_Rocky-2-Ansible_Advanced.html)

</div>
</div>
