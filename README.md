# Vagrant virtual machines as for development and testing environments.

## Machines:
  debian-dev01 - apache, mysql, php

## Description
Idea of these virtual machines is to easily deploy testing environment for projects.
I've tried to leave all role-variables as much default as possible.

- Listed all used roles variables in group_vars/<machine_name>, so that
  they can be managed from a single place easily.

- Ideal situation is that you just input project git-url, deploy machine and
  everything works.
  (Surely we can agree that this is not going to be the case most of the times.)

- To keep developing simple, virtual machines' /srv/sites -folder is shared
  to this git directory's folder shared_folders. This requires guest-additions
  for virtual machine. debian/jessie64 -box does not have this by default,
  and need to be installed for shared folder to work.

  Installation guide:
  https://www.vagrantup.com/docs/virtualbox/boxes.html#virtualbox-guest-additions

### debian-dev01:
  Set-up development environment for Laravel, or Set-up developing/testing
  machine for existing PHP-project.
  
# Variables to begin with:
```
  project_laravel_template: True
  project_database_in_use: True
  project_database_use_dump: False
  project_git_url: https://github.com/laravel/laravel.git
  project_git_destination: /srv/sites/laravel
  project_git_version: master
  project_local_folder_path: files/debian.dev01
  project_database_dump_file: "{{ project_local_folder_path }}/mysql_dump.sql"
  project_git_url: https://github/laravel/laravel
  project_git_destination: /srv/sites/
  project_git_version: master

  apache_document_root: /srv/sites/laravel/public
  apache_default_port: 80
  
  mysql_port: 3306
  mysql_users: []
  mysql_databases: []
```

## Currently used roles in this repository:
* ajsalminen.apt_source
* ANXS.mysql
* geerlingguy.git
* geerlingguy.composer
* geerlingguy.php

## Other github repositories mentioned/used in this repository:
* https://github.com/laravel/laravel - Laravel PHP-framework.
