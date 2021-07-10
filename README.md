# PoCAcmeLocal

This a PoC of configuring two VM using Vagrant + Ansible. One VM will run NGINX + PHP and with two Prometheus exporters and the orther one, Prometheus + Grafana for monitoring.

This project is just for learning how to configure this services using Vagrant + Ansible, so I hope it will be evolving as I get more skilled.

### Prerequisites

Vagrant >= 2.2.6
Ansible >= 2.9

### Software used

VM are created the image *bento/ubuntu-20.04*
All the packages used are the included in this linux distribution.
Except:
* community.grafana plugin for ansible
* grafana oficial repository is added
* php-fpm-exporter from [bakins/php-fpm-exporter](https://github.com/bakins/php-fpm-exporter)

### Starting

Just clone the project and execute **vagrant up** in the main directory

### Update log

#### 2021-07-11 First Commit

Known issues / pending improvements
* php-fpm-exporter is working but grafana doesn't show metrics
* IP's are hardcoded on the playbook
* Passwords are in plain test on the playbook and templates
* Grafana Dashboards included are for test, I need to work on real ones
* Comments are in spanish ;-)
* I used a third VM to run the local playbook
* Retrive dashboards .json from Githubs sometimes fail, retry with "vagrant provision"
