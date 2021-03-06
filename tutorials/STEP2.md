## Step 2. Inventory Practice
当前工作目录为`ansible-workshop`，演示使用Inventory文件来指定受控资源列表。

#### 配置虚拟机Host2
现在可以再加入一台虚拟机，随后会在inventory中进行配置
```
mkdir vagrant2
cd vagrant2
vagrant init ubuntu/trusty64
```

修改Vagrantfile并加入以下配置：
```
config.vm.network "private_network", ip: "192.168.33.101"

config.vm.provider "virtualbox" do |vb|
    vb.name = "ansible-workshop-host2"
end
```

启动第二台虚拟机后再回到上一级目录：
```
vagrant up

cd ..
```

#### 配置Inventory加入新Host2
创建名为`hosts`的文件，配置虚拟机的Host和Group：
```
[ubuntu]
192.168.33.100 ansible_ssh_user=vagrant ansible_ssh_private_key_file=vagrant/.vagrant/machines/default/virtualbox/private_key

[ubuntu2]
192.168.33.101 ansible_ssh_user=vagrant ansible_ssh_private_key_file=vagrant2/.vagrant/machines/default/virtualbox/private_key

[myserver:children]
ubuntu
ubunt2
```

#### 测试是否ping得通
测试一下应该两台都可以正常访问：
```
ansible -i hosts myserver -m ping
```

可能需要多次输入`yes`回车确认加入key fingerprint，当然也可在ansible.cfg中配置参数关闭提示。当连接成功结果为：
```
192.168.33.100 | SUCCESS => {
        "changed": false,
            "ping": "pong"
}
192.168.33.101 | SUCCESS => {
        "changed": false,
            "ping": "pong"
}
```

也可以单独ping某台虚拟机：
```
ansible -i hosts ubuntu2 -m ping
```

----
> * Goto Prev [Step 1](STEP1.md).
> * Goto Next [Step 3](STEP3.md).

----
References

* [Ansible Inventory](http://docs.ansible.com/ansible/intro_inventory.html)

