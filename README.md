# role-linux-config-backup
Role contains tasks that SIMULATE configs backups on Linux devices.

This is just a test role

# Requirements
- Minimum ansible 2.11

# Role Variables

- Variables are fed into the role during the play.
- Varibles are set in playbooks/vars/all.yml file

# Dependencies
- Playbook with variables.

# How to use

1. If running as ansible core : 
- Install the role : $ ansible-galaxy install -r collections/requirements.yml
  ** The collections/requirements.yml file will be in your tool's repo**

2. If running on AAP :
- AAP has an automated job( Which one??) that will pull down and install the mentioned roles before running the job. 

# Example Use :
## === roles/requirements.yml 

roles:
  - src: https://github.com/254In61/ansible-role-rhel-test.git
    scm: git
    version: main

## == playbooks/scripts/site.yml

--- 
- name: CHECK LINUX ENV
  hosts: "{{ target_host }}"
  gather_facts: false

  vars:
    vars needed here
 
  pre_tasks:
    - Pre-tasks here

  tasks:
    - name: Set traffic_redirect variables
      ansible.builtin.set_fact:
        traffic_movement: true   # Couldn't set a bool on the AAP as extra variable. AAP takes in a string.
      when: traffic_redirect | lower == "yes"
      delegate_to: localhost
    
    - name: Apply traffic isolation tasks
      ansible.builtin.include_role:
        name: ansible-role-rhel-test
      vars:
        _date_: true
        _tmp-file_: "{{ tmp_store_file }}"


# License
BSD

# Author Information
Name : Allan Maseghe

Company: Red Hat

Role: Consultant - Ansible
