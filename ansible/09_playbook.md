# Playbook
1. Module - the actual logic/code/binary that ansible copies to managed nodes to do an action. Each module performs predetermined actions.   
2. Task - reference to a single module defining ansible operation. It executes a module with specific arguments. 
3. Play - Ordered list of tasks
4. Playbook - Ordered list of plays
5. Playbooks are written in YAML and are executed top to bottom. 
6. A task is executed in parallel across all machines and post successful completion it moves to the execution of next task.
7. Before a task is run, ansible first check the current state on the machine and if it matches the desired state in the playbook. The changes are performed in the machines only when they dont match. 


```
ansible-playbook -i inventory playbook/setup.yml
ansible-playbook -i inventory --check playbook/setup.yml # Only check the state in the managed node and dont apply any changes
```