# Ruby

## StackOverflow

Suggestions for install Ruby and Bundler:

```yaml
- name: Install Bundler
  shell: gem install bundler
```

```yaml
  - name: Install Ruby
    apt:
      name:
        - ruby
        - ruby-dev
        - make
        
  - name: Install gems
    gem:
      name: xyz
      user_install: yes
```

[source](https://stackoverflow.com/questions/22115936/install-bundler-gem-using-ansible)

## Role

The Ruby role does this in [tasks/main.yml](https://github.com/geerlingguy/ansible-role-ruby/blob/master/tasks/main.yml).

```yaml
# ...

# Install Bundler and configured gems.
- name: Install Bundler.
  gem: name=bundler state=present user_install=no
  when: ruby_install_bundler

- name: Install configured gems.
  gem:
    name: "{{ item }}"
    state: present
  become: true
  become_user: "{{ ruby_install_gems_user }}"
  with_items: "{{ ruby_install_gems }}"
```

It also makes changes around the path.
