---
layout: post
title:  "Ansible: print role name inside template"
tags: ansible
---
Ansible guys suppose to use `{% raw %}{{ ansible_managed }}{% endraw %}` inside templates to indicate where it came from. Unfortunately, this variable contains date and time, so it is changed on every playbook run. That breaks `--check` mode.

I prefer to include role name in template, so you can see where it came from. If you hard-code it, after refactoring that will become broken. Here is how you can generate it dynamicaly:

```
{% raw %}
# Generated by ansible role: {{ role_path | regex_replace('^.*/([^/]+)$', '\\1') }}
{% endraw %}
```
It's a bit clumsy, but it will never break.