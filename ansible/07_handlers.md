# Handlers
- handlers run a task only when a change/s is made to the dependent tasks.
- Uses 
  - `notify` section is added to the depedent task
  - `handlers` block has all the tasks that has to run with change
- Handlers must be named in a ordered way so that the notify can identify a unique handler. All matching handlers will be run.
- Handlers are run once at the end of a particular play
```
---
- name: Set up apache
  tasks:
    - name: install apache
      apt:
        name: apache2
        state: present
    - name: set config
      template:
        src: template/apache2.conf
        dest: /etc/apache2/apache2.conf
      notify: 
        - Restart apache
        - Restart tomcat
  handlers:
    - name: Restart apache
      service:
        name: apache2
        state: restarted
    - name: Restart tomcat
      service:
        name: tomcat
        state: restarted
```

```
---
- name: Set up apache
  tasks:
    - name: install apache
      apt:
        name: apache2
        state: present
    - name: set config
      template:
        src: template/apache2.conf
        dest: /etc/apache2/apache2.conf
      notify: Restart "{{item}}"
      loop:
        - apache
        - tomcat
  handlers:
    - name: Restart apache
      service:
        name: apache2
        state: restarted
    - name: Restart tomcat
      service:
        name: tomcat
        state: restarted
```

```
---
- name: Set up apache
  tasks:
    - name: install apache
      apt:
        name: apache2
        state: present
    - name: set config
      template:
        src: template/apache2.conf
        dest: /etc/apache2/apache2.conf
      notify: "restart stack"
  handlers:
    - name: Restart apache
      service:
        name: apache2
        state: restarted
      listen: "restart stack"
    - name: Restart tomcat
      service:
        name: tomcat
        state: restarted
      listen: "restart stack"
```

