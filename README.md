[![Build Status](https://travis-ci.org/jobscore/ansible-role-elasticsearch.svg?branch=master)](https://travis-ci.org/jobscore/ansible-role-elasticsearch)

ElasticSearch
=========

This Ansible role for installing ElasticSearch on Ubuntu

Requirements
------------

Ansible > 1.4

Role Variables
--------------

`es_ver: 6.x`
It defines the ElasticSearch version to use, default to **'6.x'**.

`es-config: {}`
It defines the configuration keys to be set in the `elasticsearch.yml` file. The defaults are the following:
``` yaml
es_config:
  cluster_name: default
  node.name: master
  path.data: /var/lib/elasticsearch
  path.logs: /var/log/elasticsearch
  http.port: 9200
```

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - role: jobscore.elasticsearch

License
-------

GPL v3

Author Information
------------------

This role was created by [Eric Magalhães](https://emagalha.es).
