# Ansible模块Module


## 什么是Ansible Module？

bash无论在命令行上执行，还是bash脚本中，都需要调用cd、ls、copy、yum等命令；
module就是Ansible的“命令”，module是ansible命令行和脚本中都需要调用的。

在bash，调用命令时可以跟不同的参数，每个命令的参数都是该命令自定义的；
同样，ansible中调用module也可以跟不同的参数，每个module的参数也都是由module自定义的，每个module的用法可以查阅文档。http://docs.ansible.com/ansible/modules_by_category.html



## Module在命令里使用Module

```
$ ansible all -m copy -a "src=/etc/hosts dest=/tmp/hosts"
$ ansible web -m yum -a "name=httpd state=present"

```


## Ansilbe在Playbook使用Module


```
---
  tasks:
  - name: ensure apache is at the latest version
    yum: pkg=httpd state=latest
  - name: write the apache config file
    template: src=templates/httpd.conf.j2 dest=/etc/httpd/conf/httpd.conf
  - name: ensure apache is running
    service: name=httpd state=started

```

## Module的特性
* Module是通过命令或者Playbook可以执行的task的插件

* Module是用Python写的。

* Ansible提供一些常用的Module http://docs.ansible.com/ansible/modules_by_category.html

* 通过命令ansible-doc可以查看module的用法

* Ansible提供API，用户可以自己写Module