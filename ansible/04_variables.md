# Variables
1. Variable unify scripts while having diverse set of actions based on the scenarios across hosts.
2. Variable names can have letters, numbers and underscore. Variables cannot begin with a number
   ```
   # Valid
   foo
   bar
   foobar1
   foo_bar2
   _foo
   
   # Invalid
   12foo
   foo&
   foo^
   12
   if # python keyword
   lambda
   ```
3. Variables can be defined in
   - Playbook
   - Vars file
   - Role
   - Inventory
   - Cmd line
   - Register run time variables created during playbook execution
4. Types of variables
   - simple 
   - boolean
   - list
   - dictionary
   - dynamic - register the output of task as a variable to be used elsewhere
```
## Playbook variables
# Define variables
# simple
package: apache2  
# boolean
is_web: true
# list 
packages:
  - apache2
  - ufw
  - python3
# dictionary
capitals:
  karnataka: bangalore
  telangana: hyderabad
  andhra: amaravati
  tn: chennai
  
  
# Use variables  
---
- name: Install package via apt
  apt:
    name: '{{ package }}'
    state: present  

- name: print
  debug: 
    msg: 
      - '{{ is_web }}'
      - '{{ packages[1] }}'
      - '{{ capitals.karnataka }}'
      - "{{ capitals['karnataka'] }}"
  register: debug_result

- name: print result
  debug:
    msg: '{{ debug_result }}'
    
## Variables set via cmdline
ansible-playbook playbook.yml --extra-vars "version=0.06.92 other_variable=works"
```

5. [Variable precedence](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html#understanding-variable-precedence)
6. Special variables
    - fact variables - variables related to the remote host
    - magic variables - variables related to the ansible, python, inventory and directories for playbooks
    - connection variables - variables related to connection to remote host - user, host, ssh and more
7. Data in the variables can be manipulated using Filters. 