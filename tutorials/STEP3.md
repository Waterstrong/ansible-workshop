## Step 3. Playbooks, Roles and Tasks Practice

#### 创建playbooks
写一个Playbook,命名为`setup_server.yml`：
```
---
- hosts: myserver
  become_method: sudo
  become: yes

  roles:
    - install_tools
```

#### 创建roles和tasks
在ansible-workshop目录下创建文件`roles/install_tools/tasks/main.yml`
```
---
- name: Ensure update cache
  run_once: no
  apt:
    update_cache: yes
- name: Ensure serveral components installed
  apt:
    name: "{{item.value}}"
    state: installed
  with_items: "{{packages}}"
```

在ansible-workshop目录下创建文件`roles/install_tools/vars/main.yml`
```
---
packages:
  - { name: 'Git', value: git }
```

当前目录结构如下：
```
.
├── hosts
├── roles
│   └── install_tools
│       ├── tasks
│       │   └── main.yml
│       └── vars
│           └── main.yml
└── setup_server.yml
```

#### 运行playbooks安装Git
运行Playbooks命令如下:
```
ansible-playbook -i hosts setup_server.yml
```

最后执行完成显示：
```
PLAY [myserver] ****************************************************************

TASK [setup] *******************************************************************
ok: [192.168.33.100]
ok: [192.168.33.101]

TASK [install_tools : Ensure update cache] *************************************
ok: [192.168.33.100]

TASK [install_tools : Ensure serveral components installed] ********************
ok: [192.168.33.100] => (item={u'name': u'Git', u'value': u'git'})
ok: [192.168.33.101] => (item={u'name': u'Git', u'value': u'git'})

PLAY RECAP *********************************************************************
192.168.33.100             : ok=3    changed=0    unreachable=0    failed=0
192.168.33.101             : ok=2    changed=0    unreachable=0    failed=0
```

----
References

* [Ansible Playbooks](http://docs.ansible.com/ansible/playbooks_intro.html)
