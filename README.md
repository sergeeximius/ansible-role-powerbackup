Ansible role for powerbackup script
=========

This code is used to set up a backup system using Ansible. It copies two scripts (powerbackup and powerbackup_rotate) to the /usr/local/sbin directory and sets the owner and group to root. It then creates a config directory at /etc/powerbackup, as well as tasks directories for each item in the powerbackup_tasks list. It also creates an include file and an exclude file for each item in the powerbackup_tasks list, if one is defined. Finally, it creates two cronjobs - one to run backup files every day at 1:05am, and another to run a full backup periodically (weekly by default). It also creates a destination directory for the backups at powerbackup_destination_dir.

![Ansible Lint](https://github.com/sergeeximius/ansible-role-powerbackup/workflows/Ansible%20Lint/badge.svg)

Requirements
------------

None

Role Variables
--------------
powerbackup_tasks [_list_] - directories list for backup tasks
- &ndash; name [_string_] - task name
- include_dir [_string_] - directory for backup in the task

powerbackup_destination_dir [_string_] - destination directory for the backups
powerbackup_fullbackup_periodically [_daily|weekly(default)|monthly_] - Crontab special time specification nickname

Dependencies
------------

None

Example
----------------

requirements.yml
```
    roles:
      - src: https://github.com/sergeeximius/ansible-role-powerbackup.git
          scm: git
          name: sergeeximius.powerbackup
```
playbook.yml
```
    - hosts: servers
      vars:
        powerbackup_destination_dir: "/mnt/s3fs/files"
        powerbackup_tasks:
          - name: site1
            include_dir: "/home/site1/data/www/"
          - name: site2
            include_dir: "/home/site2/data/www/"
        powerbackup_fullbackup_periodically: "weekly"
      roles:
         - role: sergeeximius.powerbackup
```
License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
