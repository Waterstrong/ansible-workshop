## Step 5. Ansible Galaxy Practice
通过Ansible Galaxy快速安装Jenkins。在[Ansible Galaxy](https://galaxy.ansible.com/list#/roles)上搜索找到Jenkins对应的Role，比如选择[geerlingguy.jenkins](https://galaxy.ansible.com/geerlingguy/jenkins/)。

#### 下载Jenkins的role到本地
首先下载role到本地：
```
ansible-galaxy install geerlingguy.jenkins
```

下载role安装成功后得到以下信息：
```
- downloading role 'jenkins', owned by geerlingguy
- downloading role from https://github.com/geerlingguy/ansible-role-jenkins/archive/2.1.1.tar.gz
- extracting geerlingguy.jenkins to /usr/local/etc/ansible/roles/geerlingguy.jenkins
- geerlingguy.jenkins was installed successfully
- adding dependency: geerlingguy.java
- downloading role 'java', owned by geerlingguy
- downloading role from https://github.com/geerlingguy/ansible-role-java/archive/1.4.0.tar.gz
- extracting geerlingguy.java to /usr/local/etc/ansible/roles/geerlingguy.java
- geerlingguy.java was installed successfully
```

特别注意其中的路径`/usr/local/etc/ansible/roles/geerlingguy.jenkins`，会在接下来的role中用到。 

#### 创建安装Jenkins的playbook
在`ansible-workshop`目录创建一个安装jenkins的playbook `setup_jenkins.yml`，目前只把第一台虚拟机作为CI服务器:
```
---
- hosts: ubuntu
  become_method: sudo
  become: yes
  roles:
    - /usr/local/etc/ansible/roles/geerlingguy.jenkins
```

其中的role为之前安装的文件路径。

#### 运行命令执行安装
```
ansible-playbook -i inventory setup_jenkins.yml
```

可能会花较长的时间，请耐心等待。安装成功后可以访问Jenkins Home页面[http://192.168.33.100:8080](http://192.168.33.100:8080)或Jenkins CLI页面[http://192.168.33.100:8080/cli](http://192.168.33.100:8080/cli)，然后可以开始使用Jenkins了。
用户名: `admin`   密码: `admin`

#### Workshop结束语
Thanks everyone! You can halt your virtual machines and destroy them to reduce your computer resoures.
Make sure your are in `ansible-workshop` directory and execute the below commands:
```
cd vagrant
vagrant halt
vagrant destroy

cd ../vagrant2
vagrant halt
vagrant destroy
```

----
References

* [Ansible Galaxy Docs](http://docs.ansible.com/ansible/galaxy.html)
* [Ansible Galaxy Home](https://galaxy.ansible.com/)
* [geerlingguy.jenkins README](https://galaxy.ansible.com/geerlingguy/jenkins/)
