# Patterns with inventory

Each execution of playbook needs the list of hosts(pattern) to be specified

1. inline
   ```
   - name: play
     hosts: <pattern>
     <...snip...>
   ```
2. cmd line
   ```
   ansible -i inventory --limit <pattern> path/to/playbook.yml
   ```

##### Patterns

| Pattern                                 | Description                                                     |
|-----------------------------------------|-----------------------------------------------------------------|
| all/ *                                  | All hosts                                                       |
| earth01.example.com                     | one host                                                        |
| earth01.example.com,earth02.example.com | two hosts                                                       |
| earth01.example.com:earth02.example.com | two hosts(same as above)                                        |
| planets                                 | all hosts in planets group                                      |
| planets:stars                           | Union, all hosts in planets and stars groups                    |
| celestial:!stars                        | Difference, all hosts in celestial group and not in stars group |
| celestial:&stars                        | Intersection, all hosts in both celestial and stars group       |

```
# Complex patterns
planets:stars:satellites:&life # All hosts in both (planets+stars+satellites) and life
solarsystem:celestial:!stars:&life # # All hosts in both ((solarsystem+celestial) and host not in stars)  and life

# Test
$ ansible -i inventory.ini 'solarsystem:celestial:&planets' --list-hosts
```