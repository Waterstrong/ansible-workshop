## Step 4. Install Apache2 Server Practice

#### 安装Apache2
修改文件`roles/install_tools/vars/main.yml`并添加一行安装Apache2的条目：
```
---
packages:
  - { name: 'Git', value: git }
  - { name: 'Apache2', value: apache2 }
```

#### Git下载代码
通过git clone下载静态页面代码测试服务器，首先创建一个role的task文件`roles/git_clone_file/tasks/main.yml`并写以下内容：
```
---
- name: Ensure repo clone and update to apache directory
  git:
    repo: "https://github.com/Waterstrong/waterstrong.github.com.git" 
    dest: "/var/www/html/home"
    update: yes
```

#### 配置重启Apache服务
创建一个role的task文件`roles/start_apache2/tasks/main.yml`并配置：
```
---
- name: enabled mod_rewrite
  apache2_module:
    name: rewrite
    state: present

- name: restart apache2
  service:
    name: apache2
    state: restarted
```

当前目录树结构为：
```
.
├── inventory
├── roles
│   ├── git_clone_file
│   │   └── tasks
│   │       └── main.yml
│   ├── install_tools
│   │   ├── tasks
│   │   │   └── main.yml
│   │   └── vars
│   │       └── main.yml
│   └── start_apache2
│       └── tasks
│           └── main.yml
└── setup_server.yml
```

#### 运行playbook并测试服务器
在目录`ansible-workshop`目录下运行命令测试：
```
ansible-playbook -i inventory setup_server.yml
```

成功执行完成后可访问[http://192.168.33.100/page](http://192.168.33.100/page)和[http://192.168.33.101/page](http://192.168.33.101/page)测试是否部署页面成功。

----
References

*[配置和重启apache服务器](https://yaowenjie.gitbooks.io/ansible-workshop/content/pei_zhi_he_zhong_qi_apache_fu_wu_qi.html)
