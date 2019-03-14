Ansible Role Backupninja
=========

[![Build Status](https://travis-ci.com/cloudweeb/cloudweeb.backupninja.svg?branch=master)](https://travis-ci.com/cloudweeb/cloudweeb.backupninja)

Ansible role to install and configure Backupninja, based on [sigio.backupninja](https://github.com/sigio/ansible-role-backupninja) role

Requirements
------------

None

Role Variables
--------------

Backupninja main config

```YAML
backupninja_main_backupdir: /var/backups
backupninja_reportemail: root
backupninja_reportsuccess: "yes"
backupninja_reportinfo: "yes"
backupninja_reportwarning: "yes"
backupninja_reportspace: "yes"
backupninja_reporthost: ""
backupninja_reportuser: ninja
backupninja_reportdirectory: /var/lib/backupninja/reports
backupninja_admingroup: adm
backupninja_logfile: /var/log/backupninja.log
backupninja_configdirectory: /etc/backup.d
backupninja_scriptdirectory: /usr/share/backupninja
backupninja_usecolors: "yes"
backupninja_default_when: everyday at 02:00
backupninja_vservers: "no"
```

Backupninja job that you want to activate

```YAML
backupninja_enable_job:
  - 20.cloudweeb-mysql
  - 90.cloudweeb-tar
```

Backupninja tar backup options

```YAML
backupninja_tar_when: everyday at 01
backupninja_tar_backupname: "{{ ansible_fqdn }}"
backupninja_tar_backupdir: "{{ backupninja_main_backupdir }}/tar/{{ ansible_fqdn }}"
backupninja_tar_compression: bzip
backupninja_tar_rotate: 7
backupninja_tar_includes:
  - /home
backupninja_tar_excludes:
  - /tmp
  - /proc
  - /sys
  - /dev
  - /srv
  - /media
  - /misc
  - /net
  - /selinux
```

Backupninja mysql backup options

```YAML
backupninja_mysql_sqldump: "yes"
backupninja_mysql_compress: "yes"
backupninja_mysql_backupdir: "{{ backupninja_main_backupdir }}/mysql"
backupninja_mysql_configfile: "{{ backupninja_main_backupdir }}.my.cnf"
backupninja_mysql_databases: ['all']
backupninja_mysql_rotate: 7
backupninja_mysql_sqldumpoptions: >
  --single-transaction
  --complete-insert
  --add-drop-table
  --quick
  --quote-names
```

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: cloudweeb.backupninja }

License
-------

MIT / BSD

Author Information
------------------

Agnesius Santo Naibaho
