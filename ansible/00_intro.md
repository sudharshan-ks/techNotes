# Ansible

1. Configuration Management tool
2. Simple, Human readable
3. Agent-less
4. Idempotence
5. Ansible scripts aka Playbooks are written in YAML
6. Declarative -- desired state
7. Parallel execution
7. Has 3 components
   a. Control node - System where ansible is installed
   b. Inventory - List of managed nodes present on the control node
   c. managed node - Remote node that ansible controls
8. The ansible running on control node connects to manages node/s via SSH and runs python scripts to reach desired state
   mentioned in the playbook.