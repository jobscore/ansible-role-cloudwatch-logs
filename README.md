[![Build Status](https://travis-ci.org/jobscore/ansible-role-cloudwatch-logs.svg?branch=master)](https://travis-ci.org/jobscore/ansible-role-cloudwatch-logs)

CloudWatch Log
=========

This role install the CloudWatch Logs agent on an Ubuntu machine

Requirements
------------

You should have your AWS credentials already configured in the machine, it works with either IAM roles or global IAM user credentials such as in the AWS CLI configuration (see https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)

Role Variables
--------------

``` yaml
aws_region: us-east-1
```
This one defines the AWS region to use

``` yaml
cw_logs_files: []
```
This is the most important variable, it defines the configuration for logs that you want to manage. It expects a list of logs to for the agent to watch. The list itself follow this format:

``` yaml
cw_logs_files:
  - name: syslog
    args:
      log_group_name: syslog
      log_stream_name: ubuntu
      datetime_format: '%b %d %H:%M:%S'
      time_zone: UTC
      file: /var/log/syslog
      file_fingerprint_lines: 1-5
      multi_line_start_pattern: '^\s+.*'
      initial_position: start_of_file
      encoding: utf_8
      buffer_duration: 5000
      batch_count: 10000
      batch_size: 1048576
  - name: auth
    args:
      log_group_name: auth.log
      log_stream_name: ubuntu
      datetime_format: '%b %d %H:%M:%S'
      time_zone: UTC
      file: /var/log/auth.log
      file_fingerprint_lines: 1-5
      multi_line_start_pattern: '^\s+.*'
      initial_position: start_of_file
      encoding: utf_8
      buffer_duration: 5000
      batch_count: 10000
      batch_size: 1048576
```
The field `name` defines the name of the log entry, that should be unique and the field `args` should contain the specifics of the log configuration as per AWS docs in here: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.htmlhtml


Dependencies
------------

None

Example Playbook
----------------

``` yaml
- hosts: all
  roles:
    - role: jobscore.cloudwatch-logs
      cw_logs_files:
        - name: syslog
          args:
            log_group_name: syslog
            log_stream_name: ubuntu
            datetime_format: '%b %d %H:%M:%S'
            time_zone: UTC
            file: /var/log/syslog
            file_fingerprint_lines: 1-5
            multi_line_start_pattern: '^\s+.*'
            initial_position: start_of_file
            encoding: utf_8
            buffer_duration: 5000
            batch_count: 10000
            batch_size: 1048576
        - name: auth
          args:
            log_group_name: auth.log
            log_stream_name: ubuntu
            datetime_format: '%b %d %H:%M:%S'
            time_zone: UTC
            file: /var/log/auth.log
            file_fingerprint_lines: 1-5
            multi_line_start_pattern: '^\s+.*'
            initial_position: start_of_file
            encoding: utf_8
            buffer_duration: 5000
            batch_count: 10000
            batch_size: 1048576

```
License
-------

[GPLv3](/LICENSE)

Author Information
------------------

This role was created by [Eric Magalhães](https://emagalha.es) while working for [JobScore Inc](https://jobscore.com).
