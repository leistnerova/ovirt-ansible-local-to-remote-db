oVirt Engine Local DB to Remote
===============================

This role moves engine and dwh local database to remote machine.

- dump engine/dwh database on engine
- create databases/users on remote server and import dump files, install postgres if neccessary
- set engine from local db to remote

Target systems
--------------

* engine
* database

Requirements
------------

Preinstalled engine with local DB.
Preinstalled clean el7/linux based operating system on remote server.

Role Variables
--------------

```yaml
---
ovirt_engine_to_remote_db: [True, False] Change from local to remote engine database (default: True)
ovirt_engine_dwh_to_remote_db: [True, False] Change from local to remote DWH database (default: False)

ovirt_engine_reset: [True, False] True - set back engine to local db (default: False)
ovirt_engine_drop_local_db: [True, False] Drop local databases after engine is set to remote db, dump will be stored (default: True)
ovirt_engine_version: oVirt engine X.Y version
```

Dependencies
------------

* ansible-role-ovirt-dump-db
* ansible-role-ovirt-remote-db

Example Playbook
----------------

```yaml
---
# in inventory file engine has ovirt_type=engine, database has ovirt_type=remote_db
- hosts: engine database
  vars:
    ovirt_engine_dwh_to_remote_db: True
    ovirt_engine_version: "4.2"
    ovirt_engine_drop_local_db: False
  roles:
    - ovirt-engine-local-to-remote-db
```

Example Inventory
----------------

```yaml
---
[engine]
engine1.example.com
[engine:vars]
ovirt_type=engine

[database]
db1.example.com
[database:vars]
ovirt_type=remote_db
```

Author Information
------------------

Lucie Leistnerova
lucie.leistnerova@gmail.com
