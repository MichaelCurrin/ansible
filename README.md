# Ansible Playbooks
> Manage packages and configurations on my machines using Ansible

This guide is focused on managing a Linux laptop and includes setup and run steps. This was my first time using Ansible and these instructions are aimed at other beginners or myself when I need a reference.


## Requirements

- [Ansible](https://ansible.com)
- [Python 3](https://python.org/) - this is a dependency of Ansible which is automatically installed.
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

Check installed dependencies.

```sh
$ sudo ansible-galaxy list
```


## Usage

### Play

Use Ansible to run the [local.yml](/local.yml) playbook.

Ansible will attempt to run `local.yml` so the playbook name does not have to be include. It will also look for a playbook based on the current machine's configured hostname.

#### Run local playbook file

Use `ansible-playbook` command.

```sh
$ sudo ansible-playbook local.yml
```

To avoid warning, you can pass inventory as one of:

```
-i ansible_hosts
-i inventory
```

[source](https://www.middlewareinventory.com/blog/run-ansible-playbook-locally/)

#### Run remote playbook file

Use `ansible-pull` command.

Note this still requires Python, git and roles to be installed first. Also, the color output is not supported like with the local install.

```sh
$ sudo ansible-pull -U https://github.com/MichaelCurrin/ansible-playbooks.git
```

Ignore the warnings about localhost not being covered in all. The `hosts: localhost` line still works fine.

Add `-v` or up to `-vvvv` for more verbosity.


### Checks

```sh
$ ansible-playbook local.yml --checks
```

```sh
$ ansible-lint local.yml
```


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


## Notes

This is project works but is **not maintained**.

Ansible was to heavy understand and debug for what I need to do on **one** machine - so I went with a plain Bash scripting approach instead - [os-genesis](https://github.com/MichaelCurrin/os-genesis).

Ansible is modern and the docs are good. So it was easy enough to get going - the Roles and the YAML syntax was the hardest part. It's just overkill for managing a single laptop. It abstracts way logic especially if you use Roles (extensions), making it harder to debug and reverse any changes.

I did this Ansible project as an experiment to improve my configuration of my laptops in order to save time and effort and to learn about Ansible. I am going with a traditional approach and am discontinuing for the following reasons:

- Having a script to add `apt` install/upgrade commands is easy to setup (download and run with bash) and so has fewer dependencies and no Ansible Roles needed.
- The traditional approach is more transparent to debug - I keep a record of what I installed and there are plenty of resources out there. When going into the Ansible way of doing it, there will be fewer online resources and its hard to imagine what it will do and to risk running it. For example, there are two Node.js roles that I found and they are intended to work for many operating systems. And they might be targeted at a root user or a remote server setup rather than a home laptop setup. There is a ton of code in a role and it was hard to see what is actually does.
- Some things like setting up deb repo for Node.js or VS Code have to be done just once and afterwards you can update with apt or the application's updater. Using an entire Node.js role didn't make sense to me.
- It's not simple to run an arbitrary command from the playbook - it becomes abstracted but harder to use just a piece.
- The setup only works so far for apt on Linux. Setup on macOS is possible but it must probably not be with sudo and I would worry about unintended automated actions on macOS for work. Also I'll have to write instructions for both Linux and macOS so there's no Ansible gain here.
- I don't need to run an initial setup that often. My choice of operating system and number of machines is limited and easy to manage by hand and through local use - I don't need orchestration of many machines that are remote or have services on.
- I don't want to be tied to Ansible in the long run.
- If I want to try something out without Ansible and then keep it, I have to learn both ways of doing it anyway which is extra work.
- Changes to config files such as PATH and hosts are better done with more control
- Ansible is too heavy of features for my usecase. It can handle managing multiple operating systems, managing a group of machines and checking if a web server or database is online. I didn't need these features.


## License

Released under [MIT](/LICENSE).
