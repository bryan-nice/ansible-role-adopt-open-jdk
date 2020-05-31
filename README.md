Adopt Open JDK
=========

This role install's java from a JFrog artifactory called [AdoptOpenJDK](https://adoptopenjdk.net/installation.html#linux-pkg). It will install java for both Debian based and Red Hat based systems.

Role Variables
----------------

Ansible variable is listed below, along with defualt value (see defaults/main.yml):

```ansible
adopt_open_jdk_version: ""
```

Set this variable with the target version to install. See references below to go to Adopt Open JDK to find desired version name.

Dependencies
----------------

None.

Example Playbook
----------------

Including an example of how to use the role in a playbook:

```ansible
- hosts: all
  vars:
    adopt_open_jdk_version: adoptopenjdk-11-hotspot
  pre_tasks:
    - name: Gather package facts
      package_facts:
        manager: auto
  roles:
  - role: adopt-open-jdk
    when: "'{ adopt_open_jdk_version }' not in ansible_facts.packages"
```

Testing Role
----------------

```ansible
docker run --rm -it \
    -v "$(pwd)":/tmp/$(basename "${PWD}"):ro \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -w /tmp/$(basename "${PWD}") \
    quay.io/ansible/molecule:3.0.4 \
    molecule test
```

References
-------

* [AdoptOpenJDK Installation](https://adoptopenjdk.net/installation.html)
* [anssible/molecule images](https://quay.io/repository/ansible/molecule?tab=tags)
* [ansible_os_family](https://github.com/ansible/ansible/blob/794d269a4d7b02ff0a5d44353d22c86bea1e8d26/lib/ansible/module_utils/facts/system/distribution.py#L468)

License
-------

[Apache 2](LICENSE)
