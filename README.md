Requirements: **Virtual Box**, **Vagrant** v2 and **Ansible** v2.

0) Generate RSA public/private files (if needed):
```
bash# ssh-keygen
```
1)
```
bash# vagrant up
```
2)
```
bash# ansible-playbook -i production site.yml
```
3) [Ambari](http://127.0.0.1:8080/), create/setup your cluster and enjoy it!
