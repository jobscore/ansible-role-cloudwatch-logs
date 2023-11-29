CloudWatch Log
=========

This role installs the CloudWatch Logs agent on an Ubuntu machine

Requirements
------------

You should have your AWS credentials already configured in the machine, it works with either IAM roles or global IAM user credentials such as in the AWS CLI configuration (see https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)

Role Variables
--------------

```yaml
cw_server_type: <ec2 | onPremise>
```
This variable defines if the agent is being installed within an EC2 instance or an on-premise server. The default is `ec2`.

``` yaml
aws_region: us-east-1
```
This one defines the AWS region to use when the instance mode is not EC2.

``` yaml
cw_logs_files: []
```
This is the most important variable, it defines the configuration for logs that you want to manage. It expects a list of logs for the agent to watch. The list itself follows this format:

``` yaml
cw_logs_files:
  - log_group_name: /var/log/syslog
    log_stream_name: '{hostname}-{instance_id}'
    timestamp_format: '%b %d %H:%M:%S'
    file_path: /var/log/syslog
    encoding: utf-8
  - log_group_name: /var/log/auth.log
    log_stream_name: '{hostname}-{instance_id}'
    timestamp_format: '%b %d %H:%M:%S'
    file_path: /var/log/auth.log
    encoding: utf-8
```
The field `name` defines the name of the log entry, which should be unique and the field `args` should contain the specifics of the log configuration as per AWS docs here: [https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AgentReference.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.html)


Dependencies
------------

None

Example Playbook
----------------

``` yaml
- hosts: all
  roles:
    - role: jobscore.cloudwatch-logs
      cw_server_type: onPremise
      aws_region: us-east-1
      cw_logs_files:
        - log_group_name: /var/log/syslog
          log_stream_name: '{hostname}-{instance_id}'
          timestamp_format: '%b %d %H:%M:%S'
          file_path: /var/log/syslog
          encoding: utf-8
        - log_group_name: /var/log/auth.log
          log_stream_name: '{hostname}-{instance_id}'
          timestamp_format: '%b %d %H:%M:%S'
          file_path: /var/log/auth.log
          encoding: utf-8
```
License
-------

[GPLv3](/LICENSE)

Author Information
------------------

This role was created by [Eric Magalhães](https://emagalha.es) and [Glauber Batista](https://glauberrbatista.dev) while working for [JobScore Inc](https://jobscore.com).
