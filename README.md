fcrepo3
=========

This role installs Fedora Commons Repository 3.8.1

Requirements
------------

Requres:
* python-mysqldb
* mysql


Role Variables
--------------

The following variables are used by this role:

```yaml
# Database settings for the Fedora repository
fedora_db_pass: root
fedora_db_user: root
fedora_db: fcrepo3_repository_resdev
fedora_db_host: localhost

# Password for the fedoraAdmin user
fedora_pass: fedoraAdmin

# Fedora install path
fedora_home: /usr/local/fedora
```


Dependencies
------------

Probably depends on:

* OUlibraries.centos7



Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

TBD

Author Information
------------------

Written for the University of Oklahoma Libraries. 