Requirements: **Virtual Box**, **Vagrant** v2 and **Ansible** v2.

1) Generate RSA public/private files (if needed):
    ```
    bash# ssh-keygen
    ```
2) Start environment:

    All machines (HDP, Kerberos):
    ```
    bash# vagrant up
    ```
    
    Only HDP server:
    ```
    bash# vagrant up hdp
    ```
    Only Kerberos (KDC) server:
    ```
    bash# vagrant up krb
    ```
3) Run Ansible playbooks:
    ```
    bash# ansible-playbook -i production site.yml
    ```
4) Access [Ambari](http://127.0.0.1:8080/), create/setup your cluster and enjoy it!