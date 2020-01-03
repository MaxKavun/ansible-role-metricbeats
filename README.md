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


- `filebeat_version`
Is used to select main Filebeat branch to be installed (5.x or 6.x current stable versions). Default value is `6`.
- `filebeat_last_version`
Is used to select specific Filebeat version to be installed. Default value is `6.6.0`
- `elastic_gpg_key`
GPG-key from elasticsearch repository. Default value is `https://artifacts.elastic.co/GPG-KEY-elasticsearch`
- `elastic_gpg_key_redhat`
GPG-key from elasticsearch repository. Default value is `https://packages.elastic.co/GPG-KEY-elasticsearch`
- `filebeat_node_name`
Name of the filebeat node. Default value is `{{ inventory_hostname }}`. If this options is not defined, the hostname is used.
- `filebeat_ssl_enabled`


## Output customization:

- `elasticsearch.host`
Array of hosts to connect to. Default value is `localhost`
- `elasticsearch.port`
Value for setting custom port. Default value is `9200`


- `logstash.host`
Array of hosts to connect to. Default value is `localhost`
- `logstash.port`
Value for setting custom port. Default value is `5044`


## Advanced config parameters:


The `filebeat(systemd)\initd` section of the configuration  options defines which init script will be used to manage filebeat service depending on the *nix OS. Custom paths will be taken into account (if configured).
- `filebeat_service_name`
Name of nssm\init script, which manages filebeat service


- `filebeat_bulk_max_size`
Maximum number of events to bulk in a single Logstash request. Default value is `500`
- `filebeat_worker`
Number of workers per Elasticsearch host. Default value is `1`
- `filebeat_logging_to_syslog`
Send all logging output to syslog. Default value is `false`
- `filebeat_logging_to_files`
Send all logging output to rotating files. Default value is `true`
- `filebeat_rotateeverybytes`
Defines log file size limit. Defalt value is `104857600` = `100MB`
- `filebeat_keepfiles`
Number of log files to keep. Default value is `30`
- `filebeat_ignore_older`
Value (any time strings like 2h, 5m can be used) above which files will be ignored. Default value is `0` (disabled)
- `filebeat_scan_frequency`
Defines how often filebeat checks file updates. Default value is `15s`
- `filebeat_harvester_buffer_size`
Defines the buffer size. Default value is `65535`
- `filebeat_logname`
Name of the logging files. Default value is `"filebeat.log"`


## Dependencies
------------


Nothing


Example Playbook
----------------


### Installing Filebeat 6.x version:


```yaml
- name: Install filebeat
  hosts: all
  roles:
    - role: ansible-role-filebeat
```
### Installing Filebeat 6.x version with custom path to log files and elasticsearch output:


```yaml
- name: Install filebeat
  hosts: all
  roles:
    - role: ansible-role-filebeat
  vars:
    input_logpath: "/var/log/messages"
    elasticsearch:
      host: elasticsearch.example.com
      port: 9200
```


License
-------
Apache


Author Information
------------------


authors:
  - Lean Delivery Team <team@lean-delivery.com>
