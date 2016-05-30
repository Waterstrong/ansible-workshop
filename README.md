# run vagrant or setup your own vm

# test ansible connection
ansible -i inventory all -m ping

# run ansible playbook
ansible-playbook -i inventory setup_static_page.yml
