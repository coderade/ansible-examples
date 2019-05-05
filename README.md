# ansible-examples

Project with some examples of how to use [Ansible](https://www.ansible.com/).

To run these examples will need to have the ansible tool installed. To install please follow the official [doc](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).


## Examples

- [Simple Ansible playbooks](#simple-ansible-playbooks)
    - [Playbook file](playbooks/playbook-demo.yml)
    - [Inventory](inventories/hosts)


## Simple Ansible playbooks

Ansible example of how to works with Ansible playbooks.
This example shows how to:

- Work with hosts and variables
- Work with a simple playbook
- Add conditional tasks on playbooks

This example the project has two files:

- a [inventory](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html) file called [`hosts`](inventories/hosts).

- a playbook example file called [`playbook-demo.yml`](playbooks/playbook-demo.yml).

##### Inventory file: [`hosts`](inventories/hosts)

The inventory file on this project will just be a set of hosts in a couple of groups. Each host is uniquely named so that we can distinguish it in the output. 

To run this example is defined too a variable for all the hosts that instructs Ansible to connect to these fake hosts locally.

    [all:vars]
    ansible_connection=local

This file is needed in order to play the ansible playbook example.


##### Playbook example file: [`playbook-demo.yml`](playbooks/playbook-demo.yml)

Simple example of an Ansible playbook with some debug tasks that only print some debug messages. 
This playbook uses the inventory file [`playbook-demo.yml`](playbooks/playbook-demo.yml)


### Running the example

To run the ansible is needed to tell Ansible playbook the inventory file to use and the playbook file to parse that in this case the  [`hosts`](inventories/hosts) file.

The Inventory is provided with the -i argument.


To run this example, on the root of this project run:

     ansible-playbook -i inventories/hosts playbooks/playbook-demo.yml


If everything works properly each play is displayed on screen and as each host completes each task, the result is displayed on screen like the following result:

    ➜  ansible-examples git:(master) ✗  ansible-playbook -i  invetories/hosts playbooks/playbook-demo.yml 

    PLAY [Do a demo 1] **************************************************************************************

    TASK [Gathering Facts] **********************************************************************************
    ok: [host3]
    ok: [host2]
    ok: [host1]

    TASK [demo task 1] **************************************************************************************
    ok: [host1] => {
        "msg": "this is task 1"
    }
    ok: [host2] => {
        "msg": "this is task 1"
    }
    ok: [host3] => {
        "msg": "this is task 1"
    }

    TASK [demo task 2] **************************************************************************************
    ok: [host1] => {
        "msg": "this is task 2"
    }
    ok: [host2] => {
        "msg": "this is task 2"
    }
    ok: [host3] => {
        "msg": "this is task 2"
    }

    PLAY [Do another demo 1] ********************************************************************************

    TASK [Gathering Facts] **********************************************************************************
    ok: [host4]
    ok: [host6]
    ok: [host5]

    TASK [demo task 3] **************************************************************************************
    ok: [host4] => {
        "msg": "this is task 3"
    }
    ok: [host5] => {
        "msg": "this is task 3"
    }
    ok: [host6] => {
        "msg": "this is task 3"
    }

    TASK [demo task 4] **************************************************************************************
    ok: [host4] => {
        "msg": "this is task 4"
    }
    ok: [host5] => {
        "msg": "this is task 4"
    }
    ok: [host6] => {
        "msg": "this is task 4"
    }

    PLAY [Do another demo 2] ********************************************************************************

    TASK [Gathering Facts] **********************************************************************************
    ok: [host8]
    ok: [host9]
    ok: [host7]

    TASK [demo task 5] **************************************************************************************
    fatal: [host7]: FAILED! => {"changed": false, "msg": "this is task 5"}
    skipping: [host8]
    skipping: [host9]

    TASK [demo task 6] **************************************************************************************
    ok: [host8] => {
        "msg": "this is task 6"
    }
    ok: [host9] => {
        "msg": "this is task 6"
    }

    PLAY [Do another demo 3] ********************************************************************************

    TASK [Gathering Facts] **********************************************************************************
    ok: [host10]

    TASK [demo task 7] **************************************************************************************
    skipping: [host10]

    TASK [demo task 8] **************************************************************************************
    ok: [host10] => {
        "msg": "this is task 8"
    }

    PLAY [Do another demo 3] ********************************************************************************

    TASK [Gathering Facts] **********************************************************************************
    ok: [host11]

    TASK [demo task 7] **************************************************************************************
    fatal: [host11]: FAILED! => {"changed": false, "msg": "this is task 7"}
    	to retry, use: --limit @/home/coderade/repo/personal/ansible-examples/playbooks/playbook-demo.retry

    PLAY RECAP **********************************************************************************************
    host1                      : ok=3    changed=0    unreachable=0    failed=0   
    host10                     : ok=2    changed=0    unreachable=0    failed=0   
    host11                     : ok=1    changed=0    unreachable=0    failed=1   
    host2                      : ok=3    changed=0    unreachable=0    failed=0   
    host3                      : ok=3    changed=0    unreachable=0    failed=0   
    host4                      : ok=3    changed=0    unreachable=0    failed=0   
    host5                      : ok=3    changed=0    unreachable=0    failed=0   
    host6                      : ok=3    changed=0    unreachable=0    failed=0   
    host7                      : ok=1    changed=0    unreachable=0    failed=1   
    host8                      : ok=2    changed=0    unreachable=0    failed=0   
    host9                      : ok=2    changed=0    unreachable=0    failed=0   

