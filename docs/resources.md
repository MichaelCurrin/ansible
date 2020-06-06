# Resources


## Ansible sites

- https://ansible.com
- https://docs.ansible.com
    - [Getting Started](https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html)
- https://galaxy.ansible.com

## Installation

- https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html	
- https://linuxhandbook.com/install-ansible-linux/


## Configuration tutorials

- https://opensource.com/article/18/3/manage-workstation-ansible
    - https://gitlab.com/jsherman82/ansible_article
- https://opensource.com/article/18/3/manage-your-workstation-configuration-ansible-part-2
- [Managing apt packages](https://docs.ansible.com/ansible/latest/modules/apt_module.html)


## Deb packages

- [Managing apt packages](https://docs.ansible.com/ansible/latest/modules/apt_module.html)
    ```yaml
    - name: Install a .deb package from the internet.
      apt:
        deb: https://example.com/python-ppq_0.1-1_all.deb
    ```
- [Install deb packages in ansible](https://chaosmail.github.io/programming/2015/03/04/install-deb-packages-in-ansible/)
- [Add and remove apt repos](https://docs.ansible.com/ansible/latest/modules/apt_repository_module.html)
    ```yaml
    # Add specified repository into sources list.
    - apt_repository:
        repo: deb http://archive.canonical.com/ubuntu hardy partner
        state: present
    ```
    ```yaml
    # Add nginx stable repository from PPA and install its signing key.
    # On Ubuntu target:
    - apt_repository:
        repo: ppa:nginx/stable
    ```

## Template repos

- https://github.com/pbulteel/ansible-laptop
- https://github.com/acch/ansible-boilerplate
- https://github.com/dmahler/ansible-template


## Roles

- [Playbooks reuse roles](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html) in the docs
- [Ansible Role Ruby](https://github.com/geerlingguy/ansible-role-ruby) by `geerlingguy`
- [Ansible Role Node.js](https://github.com/geerlingguy/ansible-role-nodejs) by `geerlingguy`
    - [defaults/main.yml](https://github.com/geerlingguy/ansible-role-nodejs/blob/master/defaults/main.yml)
- [Ansible Node.js Role](https://github.com/nodesource/ansible-nodejs-role) by `nodesource`

Note that `import_role` does a check at the start of the run so is safer than `include_role`.

### Project structure

[source](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html#id5)

- tasks - contains the main list of tasks to be executed by the role.
- handlers - contains handlers, which may be used by this role or even anywhere outside this role.
- defaults - default variables for the role (see Using Variables for more information).
- vars - other variables for the role (see Using Variables for more information).
- files - contains files which can be deployed via this role.
- templates - contains templates which can be deployed via this role.
- meta - defines some meta data for this role. See below for more details
