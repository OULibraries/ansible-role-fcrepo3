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

The following variables and defaults are used by this role:

```yaml
# DBMS Settings for Islandora Fedora
fedora_db_host: "{{ mariadb_host }}"
fedora_db_port: "{{ mariadb_port }}"
fedora_db_pass: root
fedora_db_user: root
fedora_db: fcrepo3_repository_resdev

# Admin credentials
fedora_pass: fedoraAdmin

# Install destination
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