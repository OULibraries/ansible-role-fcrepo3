fcrepo3
=========

Installs Fedora Commons Repository 3.8.1

Requirements
------------

This role needs the following on the target host:
* python-mysqldb
* mysql
* mysqldump 

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

Probably depends on OUlibraries.centos7

Doesn't actually depend on OULibraries.mariadb, but a compatible DB needs to go somewhere. 


Example Playbook
----------------
TBD


License
-------
TBD

Author Information
------------------

Written for the University of Oklahoma Libraries. 