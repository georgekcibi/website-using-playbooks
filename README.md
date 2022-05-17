# Installing LAMP stack using Ansible roles and deploying index.php page

I have written a Ansible playbook using Ansible roles for installing a LAMP stack on a server and loading a index.php file from the server

The MYSQL password is also reset and the new password is defined as a variable in the file "roles/mysql/vars/main.yaml" which has been encrypted using the password provided in the file password-file


### Clone the application and run the playbook as below

```
git clone https://github.com/georgekcibi/website-using-playbooks.git
```

```
ansible-playbook --vault-password-file password-file playbook.yaml
```
