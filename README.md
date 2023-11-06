# MySQL Backup Role
=========

This Ansible role is used for creating MySQL/MariaDB database backups, managing the backup directory, and optionally transferring the latest backup to the Ansible controller machine.

Requirements
------------

- Ansible 2.9 or higher
- `community.mysql` collection

Role Variables
--------------


The role uses the following variables which you can also override:

- `db_type`: The type of the database, `mysql` or `mariadb`.
- `mysql_package_name`: The package name for MySQL client utilities.
- `mariadb_package_name`: The package name for MariaDB client utilities.
- `mysql_backup_path`: The path where backups should be stored on the target machine.
- `mysql_user`: The user for connecting to the database.
- `mysql_group`: The group for file permissions in the backup directory.
- `mysql_database`: The name of the database to backup.
- `cron_minute`: The minute when the cron job should run.
- `cron_hour`: The hour when the cron job should run.
- `dump_execute_now`: Whether to execute a database dump immediately.
- `local_backup`: Whether to fetch the latest dump to the local machine.
- `local_backup_path`: The local path where the backup should be stored.


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

- hosts: debian11-test
  gather_facts: yes
  become: yes
  vars_files:
    - ../secrets-infra-lm.yml
  vars:
    local_backup: true
    dump_execute_now: true
    cron_minute: '0'
    cron_hour: '2'
    mysql_user: zabbix
    mysql_database: "zabbix-server"
    mysql_password: "{{ zabbix_server_dbpassword }}"

  roles:
    - mysql-dump

License
-------

BSD

Author Information
------------------

This role was created in 2023 by Karim BAIDI.
