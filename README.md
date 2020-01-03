Metricbeat Role
=========
[![License](https://img.shields.io/badge/license-Apache-green.svg?style=flat)](https://raw.githubusercontent.com/lean-delivery/ansible-role-filebeat/master/LICENSE)
[![Build Status](https://travis-ci.org/lean-delivery/ansible-role-filebeat.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-filebeat)
[![Build Status](https://gitlab.com/lean-delivery/ansible-role-filebeat/badges/master/build.svg)](https://gitlab.com/lean-delivery/ansible-role-filebeat/pipelines)
[![Galaxy](https://img.shields.io/badge/galaxy-lean__delivery.filebeat-blue.svg)](https://galaxy.ansible.com/lean_delivery/filebeat)
![Ansible](https://img.shields.io/ansible/role/d/38385.svg)
![Ansible](https://img.shields.io/badge/dynamic/json.svg?label=min_ansible_version&url=https%3A%2F%2Fgalaxy.ansible.com%2Fapi%2Fv1%2Froles%2F38385%2F&query=$.min_ansible_version)


## Summary


This role:
  - installs metricbeat on Ubuntu, CentOS
  - copies prepared configuration file (log path, connect to elasticsearch etc.)




Role tasks
------------


- Prepare server (add elastic repo)
- [Optional] Create folder(s) for custom paths
- Install metricbeat
- Copy configuration file


Requirements
------------


- Minimal Version of the ansible for installation: 2.9
 - **Supported OS**:
   - CentOS
     - 7
   - Ubuntu
     - 16.04, 18.04
   - Debian
     - 8, 9


## Role Variables
--------------


You can override any variable below by setting "variable: value" in playbook.


- `elastic_gpg_key`
GPG-key from elasticsearch repository. Default value is `https://artifacts.elastic.co/GPG-KEY-elasticsearch`
- `elastic_gpg_key_redhat`
GPG-key from elasticsearch repository. Default value is `https://packages.elastic.co/GPG-KEY-elasticsearch`


## Output customization:

- `metricbeat_config`
Custom config for metricbeat
- `metricbeat_modules`
Specify which modules will be enabled. By default only system module enabled


## Advanced config parameters:

- `metricbeat_service_name`
Name of nssm\init script, which manages filebeat service


## Dependencies
------------


Nothing


Example Playbook
----------------


### Installing Metricbeat 7.x version:


```yaml
- name: Install metricbeat
  hosts: all
  roles:
    - role: ansible-role-metricbeat
```
### Installing Metricbeat 7.x version with custom config:


```yaml
- name: Install metricbeat
  hosts: all
  roles:
    - role: ansible-role-metricbeat
  vars:
    metricbeat_config: {
      "metricbeat.config.modules": {
        "path": '${path.config}/modules.d/*.yml',
        "reload.enabled": false
        },
       "output.elasticsearch": {
         "hosts": ["localhost:9200"],
         "#username": "elastic",
         "#password": "changeme"
       },
       "#output.logstash": {
         "#hosts": ["localhost:5044"]
       }
      }
```


License
-------
Apache


Author Information
------------------


authors:
  - Lean Delivery Team <team@lean-delivery.com>
