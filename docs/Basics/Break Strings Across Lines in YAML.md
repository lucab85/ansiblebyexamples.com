---
title: "Break Strings Across Lines in YAML and Ansible"
summary: 'Learn to use YAML "|" and ">" operators for breaking strings into multiple lines in Ansible. Explore practical examples and playbook implementations.'
authors:
    - luca
date: 2022-01-18
---

# How to Break a string over multiple lines with Ansible? And in general with YAML language.

I'm going to show you a live Playbook with some simple Ansible code.
I'm Luca Berton and welcome to today's episode of Ansible Pilot.

<iframe width="560" height="315"
src="https://www.youtube.com/embed/w5RwmYN8PBo"
frameborder="0" allowfullscreen>
</iframe>

## Ansible Break a string over multiple lines

Today we're talking about Ansible Break a string over multiple lines:
Basically, there are two different operators:
- the "|" - Literal Block Scalar"
- the ">" Folded Block Scalar"

It's easy for me to show you the behavior by example.
To break a string over multiple lines in Ansible, you can use the following operators:

- Literal Block Scalar (|): This operator tells Ansible to treat the string as a literal block scalar. This means that Ansible will preserve the newlines in the string. For example, the following code will create a variable called `my_variable` that contains the following string:

```yaml
my_variable = |
This is a
multiline string
```
- Folded Block Scalar (>): This operator tells Ansible to treat the string as a folded block scalar. This means that Ansible will collapse all of the newlines in the string into a single space. For example, the following code will create a variable called `my_variable` that contains the following string:

```yaml
my_variable = >
This is a
multiline string
```

The main difference between the Literal Block Scalar and the Folded Block Scalar operators is that the Literal Block Scalar operator will preserve the newlines in the string, while the Folded Block Scalar operator will collapse all of the newlines in the string into a single space.

## Examples

#### variable1 code

```yaml
variable1: |
 exactly as you see
 will appear these three
 lines of poetry

```

#### variable1 output

```yaml
 exactly as you see
 will appear these three
 lines of poetry\n

```

#### variable2 code

```yaml
variable2: >
 this is really a
 single line of text
 despite appearances

```

#### variable2 output

```yaml
variable2: this is really a single line of text despite appearances\n

```

Welcome to the examples sections.
Let's assume we have two multi-line variables "variable1" and "variable2".
These are both multi-line variable but variable1 use the "|" - Literal Block Scalar" operator and variable 2 use the ">" Folded Block Scalar" operator.
The result of this is that variable1 remains multiline but variable2 has literally collapsed in a single line and substitutes newlines with spaces.
Please note that both variables have a newline at the end of the string.
Do you want to remove the newline at the end of the strings? Simply add a "-", a minus, after the "|" or ">" operator!

{{< promote-video-book >}}
 ## Playbook

Break a string over multiple lines with Ansible by examples.

### code1

```yaml
---
- name: debug module Playbook
  hosts: all
  vars:
    variable1: |
      exactly as you see
      will appear these three
      lines of poetry
    variable2: >
      this is really a
      single line of text
      despite appearances
  tasks:
    - name: print variable1
      ansible.builtin.debug:
        var: variable1
- name: print variable2
      ansible.builtin.debug:
        var: variable2

```

### execution1

```bash

$ ansible-playbook -i virtualmachines/demo/inventory print\ text\ variable\ during\ execution/multi-line.yml
PLAY [debug module Playbook] **************************************************************************
TASK [Gathering Facts] ****************************************************************************
ok: [demo.example.com]
TASK [print variable1] ****************************************************************************
ok: [demo.example.com] => {
    "variable1": "exactly as you see\nwill appear these three\nlines of poetry\n"
}
TASK [print variable2] ****************************************************************************
ok: [demo.example.com] => {
    "variable2": "this is really a single line of text despite appearances\n"
}
PLAY RECAP ****************************************************************************************
demo.example.com           : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ansible-pilot $

```


### code2

```yaml

---
- name: debug module Playbook
  hosts: all
  vars:
    variable1: |-
      exactly as you see
      will appear these three
      lines of poetry
    variable2: >-
      this is really a
      single line of text
      despite appearances
  tasks:
    - name: print variable1
      ansible.builtin.debug:
        var: variable1
- name: print variable2
      ansible.builtin.debug:
        var: variable2

```

### execution2

```bash

$ ansible-playbook -i virtualmachines/demo/inventory print\ text\ variable\ during\ execution/multi-line.yml
PLAY [debug module Playbook] **************************************************************************
TASK [Gathering Facts] ****************************************************************************
ok: [demo.example.com]
TASK [print variable1] ****************************************************************************
ok: [demo.example.com] => {
    "variable1": "exactly as you see\nwill appear these three\nlines of poetry"
}
TASK [print variable2] ****************************************************************************
ok: [demo.example.com] => {
    "variable2": "this is really a single line of text despite appearances"
}
PLAY RECAP ****************************************************************************************
demo.example.com           : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ansible-pilot $

```

### code3

```yaml

---
- name: debug module Playbook
  hosts: all
  vars:
    variable1: |-
      exactly as you see
      will appear these three
      lines of poetry
    variable2: >-
      this is really a
      single line of text
      despite appearances
  tasks:
    - name: print variable1
      ansible.builtin.debug:
        msg: "{{ variable1.split('\n') }}"
- name: print variable2
      ansible.builtin.debug:
        var: variable2

```

### execution3

```bash

$ ansible-playbook -i virtualmachines/demo/inventory print\ text\ variable\ during\ execution/multi-line.yml
PLAY [debug module Playbook] **************************************************************************
TASK [Gathering Facts] ****************************************************************************
ok: [demo.example.com]
TASK [print variable1] ****************************************************************************
ok: [demo.example.com] => {
    "msg": [
        "exactly as you see",
        "will appear these three",
        "lines of poetry"
    ]
}
TASK [print variable2] ****************************************************************************
ok: [demo.example.com] => {
    "variable2": "this is really a single line of text despite appearances"
}
PLAY RECAP ****************************************************************************************
demo.example.com           : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ansible-pilot $

```

[code with ❤️ in GitHub](https://github.com/lucab85/ansible-pilot/tree/master/copy%20files%20to%20remote%20hosts)

## Conclusion
Now you know how to use Ansible ">" and "|" operators to break a string over multiple lines.