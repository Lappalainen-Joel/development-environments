# Vagrant virtual machines for development and testing environments.

### Requirements
* Ansible => 2.x
* Vagrant => 1.9.3

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
  to this git directory's folder shared_folders.


### debian-dev01:
  Set-up development environment for Laravel, or Set-up developing/testing
  machine for existing PHP-project.

### Variables to begin with:
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

## How to setup:
After cloning repo execute following command in cloned repo's folder:
```
 $ ansible-galaxy -r install requirements.yml
```
And after that, check your virtualbox version and replace your version number to
group_vars/debian-dev-servers.yml
```
virtualbox_version: 5.1.18
```
Fire up virtual-machine:
```
$ vagrant up <machine_name> # eg. debian-dev01 
```
At first, this will return an error about not being able to mount shared folders.
This is because virtualbox guest-additions are missing from machine. Just
provision machine with:
```
$ vagrant provision
```
After this another occurs with message "Now you should run 'vagrant reload <machine_name> --provision'".
Just follow instructions:
```
$ vagrant reload <machine_name> --provision' eg. debian-dev01
```
Now everything should be set-up. Try to connect to 192.168.33.10 via browser. If just a blank page comes up
then just reboot virtual-machine. 

## Currently used external roles in this repository:
* ajsalminen.apt_source
* ANXS.mysql
* geerlingguy.git
* geerlingguy.composer
* geerlingguy.php

## Other github repositories mentioned/used in this repository:
* https://github.com/laravel/laravel - Laravel PHP-framework.
