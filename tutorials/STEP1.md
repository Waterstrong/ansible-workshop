## Step 1. Set up the environment on Mac

### Install Ansible

#### Brew Install

可以采用[Homebrew](http://brew.sh/)进行安装：
```
brew install ansible # 安装Ansible

brew install --upgrade ansible # 以后可更新版本
```

#### Pip Install

还可采用Python的[pip](https://pip.pypa.io/en/stable/installing/)包管理工具安装：
```
sudo pip install ansible # 安装Ansible

sudo pip install --upgrade ansible # 以后可更新版本
```

### Install VirtualBox if not have one
```
brew install Caskroom/cask/virtualbox
```

或在[VirtualBox官网下载](https://www.virtualbox.org/wiki/Downloads)进行安装。

### Install Vagrant if not have one
```
brew install vagrant
```

或在[Vagrant官网下载](https://www.vagrantup.com/downloads.html)进行安装。

### Vagrant up base on existing `Vagrantfile`
```
git clone https://github.com/Waterstrong/ansible-workshop.git
git checkout step1
cd ansible-workshop/vagrant
vagrant up
```

验证登录虚拟机成功后退出:
```
vagrant ssh
exit
```

### Test Ansible Connection
```
cd ..
ansible -i inventory all -m ping
```

若连接成功返回:
```
192.168.33.100 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

#### Unreachable Solution
如果连接不成功返回:
```
192.168.33.100 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh.",
    "unreachable": true
}
```

可能原因是之前已经在`~/.ssh/known_hosts`中有相同的记录，可以通过ssh命令确认:
```
ssh -i vagrant/.vagrant/machines/default/virtualbox/private_key vagrant@192.168.33.100
```

如果确实报错:
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ECDSA key sent by the remote host is
SHA256:JIdGdnPGRJcOZd1ZMiisaPesCr3I0/o00agtrOGNYYA.
Please contact your system administrator.
Add correct host key in /Users/sqlin/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /Users/sqlin/.ssh/known_hosts:50
ECDSA host key for 192.168.33.100 has changed and you have requested strict checking.
Host key verification failed.
```

可通过执行以下命令解决:
```
ssh-keygen -R 192.168.33.100
```

或者可直接修改known_hosts文件，找到该记录并删除:
```
sudo vim ~/.ssh/known_hosts # 找到192.168.33.100记录并删除行后保存
```

### The End
环境搭建完成，准备工作结束，关闭虚拟机:
```
cd vagrant
vagrant halt
```

----
References

* [Ansible](https://www.ansible.com/)
* [Vagrant](https://www.vagrantup.com/)
* [VirtualBox](https://www.virtualbox.org/)
* [Homebrew](http://brew.sh/)
* [Pip](https://pip.pypa.io/en/stable/installing/)

