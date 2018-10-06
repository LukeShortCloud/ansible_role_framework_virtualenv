# ansible_role_framework_virtualenv

An Ansible role to manage isolated Python virtual environments.

# Requirements

Ansible >= 2.5

# Dependencies

virtualenv

# Variables

* virtualenv_state
    * present = Install virtualenv and create a new virtualenv.
    * absent = Remove an existing virtualenv.
    * execute = Execute a command from `bin/` in the virtualenv.
* virtualenv_name = The name of the virtualenv.
* virtualenv_path = The path to where the virtualenv should be managed.
* virtualenv_cmd = The command to run in the virtualenv. Example: `pip install docker`.

# Example Playbook

```
---
- hosts: app_hosts
  roles:
    - name: ansible_role_framework_virtualenv
      vars:
        virtualenv_name: pygame
        virtualenv_path: /usr/local
        virtualenv_state: present
    - name: ansible_role_framework_virtualenv
      vars:
        virtualenv_name: pygame
        virtualenv_path: /usr/local
        virtualenv_state: execute
        virtualenv_cmd: pip install Pygame
```

# Molecule Tests

Execute the tests:

```
$ molecule test
```

There is only a test for creating a virtual environment. Executing a random command in a virtual environment is not idempotent. Users of this framework are expected to use their own logic for checking to see if the system's state has been changed. Alternatively, set `changed_when: false` on the task if nothing will be changed. Deleting the virtual environment creates a false-positive report by Molecule for the idempotent test.

# License

Apache v2.0
