---
marp: true
theme: gaia
style: |
  @import url('../assets/css/rocky-theme.css');
  header,footer{
    color: #fff;
  }
  section header a {
    color: inherit;
  }
  section {
    padding-top: 90px;
  }
_class: lead
paginate: true
markdown.marp.enableHtml: true
header: '![w:300](../assets/rocky_logo_white.png) [Back to menu](./index.html)'
footer: '**Rocky Linux Academy > Ansible courses > 2 - Ansible Intermediate**'
---
# ![right:20% w:50](../assets/rocky_linux_logo.svg) 2 - Ansible Intermediate

![bg opacity:.5](../assets/rocky_linux_logo.svg)

## Learning Ansible with Rocky

---
<br/>

# <i class="fa-solid fa-trophy"></i> Objectives

In this chapter you will continue to learn how to work with Ansible.

<i class="fa fa-check"></i> work with variables;  
<i class="fa fa-check"></i> use loops;  
<i class="fa fa-check"></i> manage state changes and react to them;  
<i class="fa fa-check"></i> manage asynchronous tasks.

---
<br/>

# Plan

<i class="fa fa-book"></i> [The variables](#the-variables)
<i class="fa fa-book"></i> [Loop management](#loop-management)
<i class="fa fa-book"></i> [Conditionnals](#conditionals)
<i class="fa fa-book"></i> [Managing changes: the `handlers`](#36)
<i class="fa fa-book"></i> [Asynchronous tasks](#43)

---

#

In the previous chapter, you learned how to install Ansible, use it on the command line, or how to write playbooks to promote the re-usability of your code.

In this chapter, we can start to discover some more advanced notions of how to use Ansible, and discover some interesting tasks that you will use very regularly.

---
<br/>
<br/>
<br/>

# The variables

---

# The variables

Under Ansible, there are different types of primitive variables:

* strings,
* integers,
* booleans.

> More information can be found at https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html.

---
# The variables

These variables can be organized as:

* dictionaries,
* lists.

---
<style scoped>
code {
  font-size: 0.6em;
}
</style>
# The variables

A variable can be defined in different places, like in a playbook, in a role or from the command line for example.

For example, from a playbook:

```yml
---
- hosts: apache
  vars:
    port_http: 80
    service:
      debian: apache2
      rhel: httpd
```

---
# The variables

or from the command line:

```bash
ansible-playbook deploy-http.yml --extra-vars "service=httpd"
```

---
<style scoped>
code {
  font-size: 0.8em;
}
</style>
# The variables

Once defined, a variable can be used by calling it between double braces:

<div class="columns">
<div>

* `{{ port_http }}` for a simple value,
* `{{ service['rhel'] }}` or `{{ service.rhel }}` for a dictionary.

</div>
<div>
For example:

```yml
- name: make sure apache is started
  ansible.builtin.systemd:
    name: "{{ service['rhel'] }}"
    state: started
```

</div>
</div>

---

# The variables

Of course, it is also possible to access the global variables (the **facts**) of Ansible (OS type, IP addresses, VM name, etc.).

---

# Outsourcing variables

Variables can be included in a file external to the playbook, in which case this file must be defined in the playbook with the `vars_files` directive:

<div class="columns">
<div>

```yml
---
- hosts: apache
  vars_files:
    - myvariables.yml
```

</div>
<div>

The `myvariables.yml` file:

```yml
---
port_http: 80
service:
  debian: apache2
  rhel: httpd
```

</div>
</div>

---
#

It can also be added dynamically with the use of the module `include_vars`:

```yml
- name: Include secrets.
  ansible.builtin.include_vars:
    file: vault.yml
```

---

# Display a variable

To display a variable, you have to activate the `debug` module as follows:

```yml
- ansible.builtin.debug:
    var: service['debian']
```

You can also use the variable inside a text:

```yml
- ansible.builtin.debug:
    msg: "Print a variable in a message : {{ service['debian'] }}"
```

---

# Save the return of a task

<div class="columns">
<div>

To save the return of a task and to be able to access it later, you have to use the keyword `register` inside the task itself.

</div>
<div>
Use of a stored variable:

```yml
- name: /home content
  shell: ls /home
  register: homes

- name: Print the first directory name
  ansible.builtin.debug:
    var: homes.stdout_lines[0]

- name: Print the first directory name
  ansible.builtin.debug:
    var: homes.stdout_lines[1]
```

</div>
</div>

---
<br/>
<br/>
<br/>

# Questions ?

---
<br/>
<br/>
<br/>

# Loop management

---

# Loop management

With the help of loop, you can iterate a task over a list, a hash, or dictionary for example.

More information can be at https://docs.ansible.com/ansible/latest/user_guide/playbooks_loops.html

---

# Loop management

Simple example of use, creation of 4 users:

```yml
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
```

---

# Loop management

At each iteration of the loop, the value of the list used is stored in the `item` variable, accessible in the loop code.

---

# Loop management

Of course, a list can be defined in an external file and be used inside the task like this (after having include the vars file):

<div class="columns">
<div>

```yml
users:
  - antoine
  - patrick
  - steven
  - xavier
```

</div>
<div>

```yml
- name: add users
  user:
    name: "{{ item }}"
    state: present
    groups: "users"
  loop: "{{ users }}"
```

</div>
</div>

---

#

We can use the example seen during the study of stored variables to improve it. Use of a stored variable:

```yml
- name: /home content
  shell: ls /home
  register: homes

- name: Print the directories name
  ansible.builtin.debug:
    msg: "Directory => {{ item }}"
  loop: "{{ homes.stdout_lines }}"
```

---

#

A dictionary can also be used in a loop.

In this case, you will have to transform the dictionary into an item with what is called a **jinja filter** (jinja is the templating engine used by Ansible): `| dict2items`.

In the loop, it becomes possible to use `item.key` which corresponds to the dictionary key, and `item.value` which corresponds to the values of the key.

---

<style scoped>
code {
  font-size: 0.45em;
}
</style>
Let's see this through a concrete example:

```yml
---
- hosts: rocky8
  become: true
  become_user: root
  vars:
    users:
      antoine:
        group: users
        state: present
      steven:
        group: users
        state: absent

  tasks:

  - name: Manage users
    user:
      name: "{{ item.key }}"
      group: "{{ item.value.group }}"
      state: "{{ item.value.state }}"
    loop: "{{ users | dict2items }}"
```

---

#

Many things can be done with the loops. You will discover the possibilities offered by loops when your use of Ansible pushes you to use them in a more complex way.

---
<br/>
<br/>
<br/>

# Questions ?

---
<br/>
<br/>
<br/>

# Conditionals

---

# Conditionals

The `when` statement is very useful in many cases: not performing certain actions on certain types of servers, if a file or a user does not exist, etc.

> More information can be at https://docs.ansible.com/ansible/latest/user_guide/playbooks_conditionals.html.

---

# Conditionals

Behind the `when` statement the variables do not need double braces (they are in fact Jinja2 expressions...).

```yml
- name: "Reboot only Debian servers"
  reboot:
  when: ansible_os_family == "Debian"
```

---

# Conditionals

Conditions can be grouped with parentheses:

```yml
- name: "Reboot only CentOS version 6 and Debian version 7"
  reboot:
  when: (ansible_distribution == "CentOS" and ansible_distribution_major_version == "6") or
        (ansible_distribution == "Debian" and ansible_distribution_major_version == "7")
```

---

# Conditionals

The conditions corresponding to a logical AND can be provided as a list:

```yml
- name: "Reboot only CentOS version 6"
  reboot:
  when:
    - ansible_distribution == "CentOS"
    - ansible_distribution_major_version == "6"
```

---

# Conditionals

<style scoped>
code {
  font-size: 0.55em;
}
</style>
You can test the value of a boolean and verify that it is true:

```yml
- name: check if directory exists
  stat:
    path: /home/ansible
  register: directory

- ansible.builtin.debug:
    var: directory

- ansible.builtin.debug:
    msg: The directory exists
  when:
    - directory.stat.exists
    - directory.stat.isdir
```

---

# Conditionals

You can also test that it is not true:

```yml
  when:
    - file.stat.exists
    - not file.stat.isdir
```

---

# Conditionals

You will probably have to test that a variable exists to avoid execution errors:

```yml
  when: myboolean is defined and myboolean
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

# Managing changes: the `handlers`

---

# Managing changes: the `handlers`

Handlers allow to launch operations, like restarting a service, when changes occur.

> More information can be at https://docs.ansible.com/ansible/latest/user_guide/playbooks_handlers.html.

---

A module, being idempotent, a playbook can detect that there has been a significant change on a remote system, and thus trigger an operation in reaction to this change.

<center>

![w:600](./assets/chapter2/handlers.png)

</center>

A notification is sent at the end of a playbook task block, and the reaction operation will be triggered only once even if several tasks send the same notification.

---
#

For example, several tasks may indicate that the `httpd` service needs to be restarted due to a change in its configuration files. But the service will only be restarted once to avoid multiple unnecessary starts.

```yml
- name: template configuration file
  template:
    src: template-site.j2
    dest: /etc/httpd/sites-availables/test-site.conf
  notify:
     - restart memcached
     - restart httpd
```

---

#

A handler is a kind of task referenced by a unique global name:

* It is activated by one or more notifiers.
* It does not start immediately, but waits until all tasks are complete to run.

---

#

Example of handlers:

```yml
handlers:

  - name: restart memcached
    systemd:
      name: memcached
      state: restarted

  - name: restart httpd
    systemd:
      name: httpd
      state: restarted
```

---

#

<style scoped>
code {
  font-size: 0.5em;
}
</style>
Since version 2.2 of Ansible, handlers can listen directly as well:

```yml
handlers:

  - name: restart memcached
    systemd:
      name: memcached
      state: restarted
    listen: "web services restart"

  - name: restart apache
    systemd:
      name: httpd
      state: restarted
    listen: "web services restart"

tasks:
    - name: restart everything
      command: echo "this task will restart the web services"
      notify: "web services restart"
```

---

# Asynchronous tasks

By default, SSH connections to hosts remain open during the execution of various playbook tasks on all nodes.

This can cause some problems, especially:

* if the execution time of the task is longer than the SSH connection timeout
* if the connection is interrupted during the action (server reboot for example)

---

# Asynchronous tasks

In this case, you will have to switch to asynchronous mode and specify a maximum execution time as well as the frequency (by default 10s) with which you will check the host status.

---

# Asynchronous tasks

By specifying a poll value of 0, Ansible will execute the task and continue without worrying about the result.

---
<style scoped>
code {
  font-size: 0.5em;
}
</style>
Here's an example using asynchronous tasks, which allows you to restart a server and wait for port 22 to be reachable again:

```yml
# Wait 2s and launch the reboot
- name: Reboot system
  shell: sleep 2 && shutdown -r now "Ansible reboot triggered"
  async: 1
  poll: 0
  ignore_errors: true
  become: true
  changed_when: False

  # Wait the server is available
  - name: Waiting for server to restart (10 mins max)
    wait_for:
      host: "{{ inventory_hostname }}"
      port: 22
      delay: 30
      state: started
      timeout: 600
    delegate_to: localhost
```

---

# Asynchronous tasks

You can also decide to launch a long-running task and forget it (fire and forget) because the execution does not matter in the playbook.

---

# Asynchronous tasks

> More information can be at https://docs.ansible.com/ansible/latest/user_guide/playbooks_async.html.

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

<i class="button">[Next Chapter >>](./Learning_Ansible_with_Rocky-3-Working_with_files.html)</i>
