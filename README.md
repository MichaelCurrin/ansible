# Ansible Playbooks
> Manage packages and configurations on my machines using Ansible

Focused on Linux and macOS laptops.


## Requirements

- [Ansible](https://ansible.com)
- [Python 3](python.org/) - this is a dependency of Ansible which is automatically installed.
- [Git](https://git-scm.com/) - needed to run remote playbooks.


## Installation

### Install system dependencies

### Debian/Ubuntu

```sh
$ sudo apt install -y ansible git
```

### macOS

```sh
$ brew install ansible git
```

### Clone

Clone from the public HTTPS URL.

```sh
$ git clone https://github.com/MichaelCurrin/ansible-playbooks.git
$ cd ansible-playbooks
```

_Note that while it's possible to install from a URL without cloning first, that command actually needs git to do a clone. Either way the requirements file will be needed. So it's best to do just clone anyway._

### Install project dependencies
_Note `sudo` is needed otherwise the playbook can't find the roles._

Install from [requirements.yml](/requirements.yml) file.

```sh
$ sudo ansible-galaxy install -r requirements.yml
```

Install ad hoc role.

```sh
$ sudo ansible-galaxy install ROLE
```

Check dependencies.

```sh
$ sudo ansible-galaxy list
```

## Usage

### Play

Use Ansible to run the [local.yml](/local.yml) playbook

Ansible will attempt to run `local.yml` so the playbook name does not have to be include. It will also look for a playbook based on the current machine's - e.g. `dell-lite.yml`.

#### Run remote playbook file

Note this still requires Python, Git and roles to be installed first.

```sh
$ sudo ansible-pull -U https://github.com/MichaelCurrin/ansible-playbooks.git
```

Ignore the warnings about localhost not being covered in all. The `hosts: localhost` line still works fine.

Add `-v` or up to `-vvvv` for more verbosity.

#### Run local playbook file

Use local file.

```sh
$ ansible-playbook local.yml
```

Some possible arguments - note the comma in inventory is important.

```
--connection=local --inventory 127.0.0.1, --limit 127.0.0.1 -i ansible_hosts
```

[source](https://www.middlewareinventory.com/blog/run-ansible-playbook-locally/)

### Ad hoc commands

```sh
$ ansible localhost -m ping
localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

```sh
$ ansible localhost -a "/bin/echo hello"
localhost | CHANGED | rc=0 >>
hello
```
