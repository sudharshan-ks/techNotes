# Inventory

1. File having a list of Managed nodes. aka `hostfile`
2. Can be written in
    - `ini` - Simple and straight-forward
    - `yaml` - Use when the inventory list is huge - 1000s of hosts
3. Types
    - Static
    - Dynamic - fetched dynamically via scripts
4. Nodes/hosts can be grouped logically for ansible to run on all the nodes in a group at once.
5. Nodes can be grouped based on
    - `what they do` - Eg. web, app, db
    - `where they are` - Eg. in, sg, dc1
    - `when are they used` - Eg. dev, uat, prod
6. Groups of groups can be created
7. There are 2 default groups
    - `all` - all hosts
    - `ungrouped` - all hosts that aren't a part of any other group 
8. A single host can belong to more than one group.
9. Multiple inventory files can be organised in a directory and the entire directory can be read by ansible. The inventory files are loaded in the ASCII order. 
10. Variables can be added at both host and group level
11. Variables can be managed out of inventory files as stand-alone yml variable files.
    - If the inventory file is at `/home/buzz/ansible/inventory`
    - `/home/buzz/ansible/group_vars/<group-name>/vars-file.yml`
    - `/home/buzz/ansible/host_vars/<host-name>/vars-file.yml`
12. [Behavioural inventory parameters](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html#connecting-to-hosts-behavioral-inventory-parameters) decide how Ansible interacts with the machines. 
```
# list of nodes
sun
moon
europa
titan
mercury
venus
earth

# Group the nodes
[stars]
sun

[planets]
mercury
venus
earth

[satellites]
moon
europa
titan

[solarsystem]
sun
mercury
venus
earth
mars
asteroids

[galaxies]
milkyway
andromeda

[life]
earth

# Group of groups
[celestial:children]
stars
planets
satellites

# Range of hosts [start:stop:stride]
earth-[01:05:2]  # earth-01, earth-03, earth-05 
earth-[a:f:3]  #earth-a, earth-d

# host variables
mars color=red habitable="gotta die to try"

# group variables
[planets:vars]
planet=true
rotates=true
luminous=false

# alias
xae191 ansible_port=22 ansible_host=192.168.0.128

# Test the inventory file
$ ansible-inventory -i path/to/inventory --list
$ ansible-inventory -i path/to/inventory --graph
```