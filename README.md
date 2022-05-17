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


### Output of the deployed playbook

```
root@ansible-server:~/ansible-git/website-using-playbooks# ansible-playbook --vault-password-file password-file playbook.yaml 
Vault password: 

PLAY [Installing LAMP stack and deploying test website] **********************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************
ok: [aws]

TASK [apache : Installing Apache] ********************************************************************************************************************
included: /root/ansible-lamp-task-roles/roles/apache/tasks/apache.yaml for aws

TASK [apache : Installing Apache] ********************************************************************************************************************
changed: [aws]

TASK [apache : Installing HTTPD] *********************************************************************************************************************
skipping: [aws]

TASK [apache : Copying apache config] ****************************************************************************************************************
included: /root/ansible-lamp-task-roles/roles/apache/tasks/config.yaml for aws

TASK [apache : Copying website apache config via rendering] ******************************************************************************************
changed: [aws]

TASK [apache : Copying index file] *******************************************************************************************************************
included: /root/ansible-lamp-task-roles/roles/apache/tasks/index.yaml for aws

TASK [apache : Copying website index.php file via rendering] *****************************************************************************************
changed: [aws]

TASK [php : Installing PHP packages] *****************************************************************************************************************
included: /root/ansible-lamp-task-roles/roles/php/tasks/php.yaml for aws

TASK [php : Installing PHP and its dependicies] ******************************************************************************************************
changed: [aws] => (item={'name': 'php'})
changed: [aws] => (item={'name': 'php-mysql'})
changed: [aws] => (item={'name': 'php-curl'})
changed: [aws] => (item={'name': 'php-gd'})
ok: [aws] => (item={'name': 'php-exif'})
ok: [aws] => (item={'name': 'php-mysqli'})
ok: [aws] => (item={'name': 'php-opcache'})
changed: [aws] => (item={'name': 'php-zip'})
changed: [aws] => (item={'name': 'php-pear'})
changed: [aws] => (item={'name': 'php-mbstring'})

TASK [mysql : Installing MYSQL] **********************************************************************************************************************
included: /root/ansible-lamp-task-roles/roles/mysql/tasks/mysql.yaml for aws

TASK [mysql : Installing MYSQL] **********************************************************************************************************************
changed: [aws]

TASK [mysql : Resetting MYSQL root password and changing MYSQL plugin] *******************************************************************************
changed: [aws]

TASK [user_creation : Creating user Bob and adding my.cnf file] **************************************************************************************
included: /root/ansible-lamp-task-roles/roles/user_creation/tasks/user.yaml for aws

TASK [user_creation : Creating user Bob] *************************************************************************************************************
changed: [aws]

TASK [user_creation : Copying .my.cnf file to user home directory via Jinja templating] **************************************************************
changed: [aws]

RUNNING HANDLER [apache : Restart Apache] ************************************************************************************************************
changed: [aws]

RUNNING HANDLER [mysql : Restart MYSQL] **************************************************************************************************************
changed: [aws]

PLAY RECAP *******************************************************************************************************************************************
aws                        : ok=17   changed=10   unreachable=0    failed=0    skipped=1    rescued=0    ignored=0 
```

From the output you can see Apache, PHP, MYSQL are installed and apache custom configuration file and index.php file being copied to the remote server using Ansible template.


### Load the remote server IP and you can see index.php file loading
