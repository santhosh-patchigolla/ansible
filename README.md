ansible
Ansible is a configuration management tool which works both on push and pull mechanisms

INVENTORY File
 Inventory is nothing but the list of machine ip or dns names that you want ansible to be managed
Ansible by default installs 2.9 as by default on AMI's we will get python2. Always go with latest version, which can be installed from tools/ansible/install.sh

all is a group which included all the entries in INVENTORY File

ANSIBLE has lot of pre-defined variables and we need to use them to supply userName and password it has to use to authenticate to the nodes.


### ansible_user     : Predefined variable for userName 
### ansible_password : Predefined variable for password  
Variables should be passed to ansible by using the flag -e


    
    Ex: ansible -i INVENTORY all  -e ansible_user=userName -e ansible_password=password 
    $ ansible -i inv all  -e ansible_user=centos -e ansible_password=xyz123 -m shell -a uptime

Ansible is a collection of modules / collections : Whatever the task that you want to perform is already predefined, all you need is just to consume them.

There 1000's of modules available : -m shell. -m yum , -m service

Ansible can be executed in 2 ways :

1) Manual Approach      : using ansible command  : With this you can execute one command at time.
2) Automated Approach   : using ansible playbook : With this we can mention all the set of tasks that needs to be executed, things will happen in the declared approach 

Automated Approach : This uses Playbook
Playbooks are written using a language called YAML.

YAML is just  markup languaga ; Markup language is nothing a presentation language

YAML is indendation specific.

What is a playbook ?
* Playbook : A Playbook is a list of plays ( and that's why it always starts with - )
* Play     : A Play is a list of tasks.
* Task     : A Task is nothing but an action that we wish to perform

How to run a playbook ?
ansible-playbook -i inventoryFileName -e ansible_user=userName -e ansible_password=password nameOfThePlaybook.yml 

Ansible Facts :
Facts are the properties of the remote nodes that you ansible is going to collect ;  Based on these facts collected ansible decides whether to perform the action or not 

How do I know, what all are the facts that are collected by ANSIBLE ?

* Ansible uses a module called as setup using that we can check the collected facts 

    $ ansible -i inventory all -m setup 

Ansible-Vault :
This is used encrypt any sort of senstitive content on your playbook

    $ ansible-vault encrypt_string pswrd1432    ( enter the password to give you the encrypted string and supply the password when you run the playook )

    $ ansible-playbook -i inv -e ansible_user=centos -e ansible_password=xyz123 13-vault.yaml --ask-vault-password
Ansible-Pull
ansible-pull -U urlName.git playbookName.yml -e COMPONENT=componentName
Block and Rescue :
Block is nothing but a group of tasks; Rescue will only be executed if any of the tasks in the block of tasks fail.

Ansible-Dryrun Command
ansible-playbook robot-dryrun.yaml -e COMPONENT=mongodb -e ansible_user=centos -e ansible_password=xyz123 -e ENV=qa
Ansible Reference Documentation :
https://docs.ansible.com/ansible/latest/index.html
YAML Reference

courses: 
    - terraform
    - kubernetes 
    - docker 
    - ansible 

name: verma


tabitha:
    name: Tabitha Bitumen
    job: Developer
    skills:
      - lisp
      - fortran
      - erlang
Ansible Roles :
Ansible roles are a way to organize your Ansible code. They are a collection of files that contain tasks, variables, and other resources that can be used to perform a specific task
Here are some of the benefits of using Ansible roles:
* Organization:  Roles can help you organize your Ansible code into logical units. This makes your code easier to understand, maintain, and reuse.

* Reusability: Roles can be reused across multiple projects. This can save you time and effort when you need to perform the same task on multiple systems.

* Modularity: Roles can be broken down into smaller, more manageable tasks. This makes your code easier to test and debug.

* Documentation: Roles can be used to document your Ansible code. This can help you and other developers understand how your systems are configured and how to manage them.

Ansible Roles Directory Structure :

roles/
    common/               # this hierarchy represents a "role"
        tasks/            #
            main.yml      #  <-- tasks file can include smaller files if warranted
        handlers/         #
            main.yml      #  <-- handlers file
        templates/        #  <-- files for use with the template resource
            ntp.conf.j2   #  <------- templates end in .j2
        files/            #
            bar.txt       #  <-- files for use with the copy resource
            foo.sh        #  <-- script files for use with the script resource
        vars/             #
            main.yml      #  <-- variables associated with this role
        defaults/         #
            main.yml      #  <-- default lower priority variables for this role
        meta/             #
            main.yml      #  <-- role dependencies
        library/          # roles can also include custom modules
        module_utils/     # roles can also include custom module_utils
        lookup_plugins/   # or other types of plugins, like lookup in this case

    webtier/              # same kind of structure as "common" was above, done for the webtier role
    monitoring/           # ""
    fooapp/               # ""

Roles Etiquitee :
By default Ansible will look in each directory within a role for a main.yml file for relevant content (also main.yaml and main):

    tasks/main.yml - the main list of tasks that the role executes.

    handlers/main.yml - handlers, which may be used within or outside this role.

    library/my_module.py - modules, which may be used within this role (see Embedding modules and plugins in roles for more information).

    defaults/main.yml - default variables for the role (see Using Variables for more information). These variables have the lowest priority of any variables available, and can be easily overridden by any other variable, including inventory variables.

    vars/main.yml - other variables for the role (see Using Variables for more information).

    files/main.yml - files that the role deploys.

    templates/main.yml - templates that the role deploys.

    meta/main.yml - metadata for the role, including role dependencies and optional Galaxy metadata such as platforms supported.

# The below command is used to create the "redis: component using ansible playboo
# gp ; ansible-playbook -i inv-dev -e ansible_user=centos -e ansible_password=DevOps321 -e COMPONENT=redis -e ENV=dev roboshop.yml    


Ansible pull and push
![image](https://github.com/santhosh-patchigolla/ansible/assets/53848645/3d8c5864-9add-4a0e-8e64-b2f7d5ec9c68)

Ansible push 
this is used if our infrastructure is dynaimic so that our inventry file is not update that time we can use the ansible push

Ansible pull
this is used if our infra is static and dont to much changes in the Inventry file (like if our infra is scales up or scales down)

####password for the user is #password for the roboshop in the ansible playbook is 
RoboSho@1

######



