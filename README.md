# NGLP Ansible

## Installation

You'll need some Python packages installed system-wide:

Fedora:

```bash
$ sudo dnf install python3-cryptography python3-passlib
```

Debian or Ubuntu:

```bash
$ sudo apt install python3-cryptography python3-passlib
```

And then set up locally with Ansible:

```bash
$ ansible-galaxy collection install -r requirements.yml
$ ansible-playbook nglp-local.yml
```
