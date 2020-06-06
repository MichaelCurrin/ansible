# Ansible Playbooks
> Manage packages and configurations on my machines using Ansible

Focused on Linux and macOS laptops.


## Requirements

- [Ansible](https://ansible.com)
- [Python 3](python.org/) - this is a dependency of Ansible which is automatically installed.
- [Git](https://git-scm.com/) - needed to run remote playbooks.


## Installation

### Install system dependencies

- Debian/Ubuntu
    ```sh
    $ sudo apt install -y ansible git
    ```

### Install project dependencies

Note `sudo` is needed otherwise the playbook can't find the roles.

```sh
$ sudo ansible-galaxy install geerlingguy.nodejs
```

Or install from locally cloned and repo and [requirements.yml](/requirements.yml).

```sh
$ sudo ansible-galaxy install -r requirements.yml
```


## Usage

### Run the playbook

#### Remote playbook

Using remote playbook. Note this stills required Python and Git to be installed.

```sh
$ sudo ansible-pull -U https://github.com/MichaelCurrin/ansible-playbooks.git local.yml
```

Ignore the warnings about localhost not being covered in all. The `hosts: localhost` line still works fine.

Add `-v` or up to `-vvvv` for more verbosity.

#### Local playbook

Use local file such as from a cloned project with overrides (might not be needed).

```sh
$ ansible-playbook --connection=local --inventory 127.0.0.1, \
--limit 127.0.0.1 local.yml -i ansible_hosts
```

Note the comma in inventory is important.

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
