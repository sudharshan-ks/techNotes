# Roles
- Roles automatically load all the vars, files,  templates, handlers, tasks based on a known file structure.
- Eases reusing and sharing
- Directory structure
```
roles/
    web-tier/                                   # Role name
        tasks/                                  #
            main.yml                            # Task files
        handlers/                               #    
            main.yml                            # handler files
        templates/                              #
            apache2.conf.j2                     # Template files
        files/                                  #
            serious_changes.sh                  # files that are to be copied
        vars/                                   #
            main.yml                            # Higher priority variables    
        defaults/                               #
            main.yml                            # default low priority variables
        meta/                                   #
            main.yml                            # Role dependencies
    app-tier/
playbook
```

```
$ cat playbook
---
- hosts: all
  roles:
    - role: web-tier
    - role: app-tier
```