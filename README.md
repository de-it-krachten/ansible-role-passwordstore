[![CI](https://github.com/de-it-krachten/ansible-role-passwordstore/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-passwordstore/actions?query=workflow%3ACI)


# ansible-role-passwordstore

Installs passwordstore 



## Dependencies

#### Roles
None

#### Collections
- community.general

## Platforms

Supported platforms

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- CentOS 7
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- OracleLinux 9
- AlmaLinux 8
- AlmaLinux 9
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 35
- Fedora 36

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# password-store version
password_store_version: '1.7.4'

# Installtion method (package or archive)
passwordstore_source: 'package'

# Package dependencies
passwordstore_dependencies:
  - tree
  - gpg

# Package
passwordstore_packages:
  - pass
</pre></code>

### defaults/family-RedHat-8.yml
<pre><code>
# Installtion method (package or archive)
passwordstore_source: 'archive'
</pre></code>

### defaults/family-RedHat-7.yml
<pre><code>
# Installtion method (package or archive)
passwordstore_source: 'archive'
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'passwordstore'
  hosts: all
  become: "yes"
  vars:
    gpg_user_name: root
    gpg_user_realname: root
    gpg_user_comment: test key
    gpg_user_email: root@localhost
    gpg_user_passphrase: Abcd1234
    passwordstore_user_name: root
    passwordstore_user_email: root@localhost
  pre_tasks:
    - name: Create 'remote_tmp'
      ansible.builtin.file:
        path: /root/.ansible/tmp
        state: directory
        mode: "0700"
  roles:
    - gpg
  tasks:
    - name: Include role 'passwordstore'
      ansible.builtin.include_role:
        name: passwordstore
</pre></code>
