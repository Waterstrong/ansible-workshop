# run vagrant or setup your own vm
```
cd ubuntu
vagrant up
```

# test ansible connection
`ansible -i inventory all -m ping`

# run ansible playbook
`ansible-playbook -i inventory setup_static_page.yml`

# test page
http://192.168.56.104/home
http://192.168.33.10/home