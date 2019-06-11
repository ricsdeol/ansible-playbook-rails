# ansible-playbook-rails
An initial setup rvm-ruby and Nginx-Passenger config with ansible playbook

Server Target: Ubuntu 18.04 LTS

Adjustment variables and servers


run:

```
ansible-galaxy install -r requirements.yml
ansible-playbook -i servers rails.yml
```



Remove lines below at `~/.ansible/roles/zzet.rbenv/tasks/user_install.yml`:
```yml
- name: add rbenv initialization to profile system-wide
  template:
    src: rbenv_user.sh.j2
    dest: /etc/profile.d/rbenv.sh
    owner: root
    group: root
    mode: 0755
  become: yes
  when:
    - (ansible_os_family != 'OpenBSD' and ansible_os_family != 'Darwin') and rbenv_user_profile

- name: add rbenv initialization to profile system-wide
  blockinfile:
    block: "{{ lookup('template', 'rbenv_user.sh.j2') }}"
    dest: /etc/profile
  become: yes
  when:
    - ansible_os_family == 'Darwin' and rbenv_user_profile
```

https://github.com/zzet/ansible-rbenv-role/issues/137


