# Install ansible

Ansible has to be installed only in the Control node. It has two packages available

1. `ansible-core`- Minimal package containing limited Ansible Builtin modules
1. `ansible` - larger batteries included package

```
pip3 install ansible
or
pip3 install ansible-core

ansible --version
```

**Prerequisites**
- Python
- User account in managed nodes to which ansible running in the control node can connect to via SSH
