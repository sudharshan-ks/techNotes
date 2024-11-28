# Loops
- Loops can be achieved via
  - `until` - run infinitely until a condition is met
  - `loop` block - runs for all items specified
  - `with_x` block - runs for all items specified where x can be a list, sequence, dict and other lookups
- Use `loop` block as it is simple and straight forward
```
# Loop with list
- name: Install packages
  apt:
    name: "{{ item }}"
    state: present
  loop:
    - apache2
    - ufw
    - libcurl
    
# Loop with dict
- name: Install packages
  apt:
    name: "{{ item.name }}"
    state: "{{ item.state }}"
  loop:
    - { name: "apache2", state: "present"}
    - { name: "ufw", state: "absent"}
    - { name: "libcurl", state: "present"}
    
# Until
- name: Run script until successful
  shell: "bash serious_changes.sh"
  register: result
  until: result.rc == 0
  retries: 20 # retry 20 times
  delay: 2 # with a delay of 2s between retries
  
```

# Conditionals
- Execute certain tasks when a certain condition is met using the `when` section
```
- name: Run script 
  shell: "bash serious_changes.sh"
  register: result
- name: Print if failed
  debug:
    msg: Script failed
  when: result.rc != 0
```

# Blocks
- Blocks are logical group of tasks which offers ways to handle errors

### Handling errors
- Handle errors in tasks using
  - `rescue` - runs when the earlier task block failed
  - `always` - runs irrespetive of success or failure of previous tasks
- If the rescue block execution succeeds, it is considered as if the original task was successful and the execution continues
```
- name: 'I'm a Block'
  block:
    - name: Run script 
      shell: "bash serious_changes.sh"
    - name: "run command"
      command: /bin/true
  rescue:
  - name: print in case of failure
    debug:
      msg: failed
  always:
    - name: run always
      debug:
        msg: I'm always invited

```