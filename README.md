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
- Fedora 36
- Fedora 37

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# password-store version
passwordstore_version: '1.7.4'

# archive url
passwordstore_url: https://git.zx2c4.com/password-store/snapshot/password-store-{{ passwordstore_version }}.tar.xz

# Installation method (package or archive)
passwordstore_source: 'package'

# Define default user + group (defaults to user on control node)
passwordstore_user_name: "{{ lookup('pipe', 'id -un') }}"
passwordstore_group_name: "{{ lookup('pipe', 'id -gn') }}"
passwordstore_user_home: "{{ ('~' + passwordstore_user_name) | expanduser }}"

# Package dependencies
passwordstore_dependencies:
  - tree
  - gpg

# Package dependencies for archive installation
passwordstore_dependencies_archive:
  - make
  - tar
  - xz

# Package
passwordstore_packages:
  - pass
</pre></code>

### defaults/family-Debian.yml
<pre><code>
# Package dependencies for archive installation
passwordstore_dependencies_archive:
  - make
  - tar
  - xz-utils
</pre></code>

### defaults/family-RedHat.yml
<pre><code>
# Installation method (package or archive)
passwordstore_source: 'archive'
</pre></code>

### defaults/Fedora.yml
<pre><code>
# Installation method (package or archive)
passwordstore_source: 'package'
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
    passwordstore_group_name: root
    passwordstore_user_email: root@localhost
  roles:
    - deitkrachten.gpg
  tasks:
    - name: Include role 'passwordstore'
      ansible.builtin.include_role:
        name: passwordstore
</pre></code>
