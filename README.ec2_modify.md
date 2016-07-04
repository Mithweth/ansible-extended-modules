# ec2_modify - modify or migrate an existing instance in ec2

## Synopsis

The ansible [ec2 module](http://docs.ansible.com/ansible/ec2_module.html) has great features to create and destroy ec2 instances but does not allow to modify an existing instance.
An existing instance cannot change subnet, instance type or even availability zone and need to be terminated to be recreated, losing all the data during the process.
This module permits those changes without any data losses.

## Requirements (on host that executes module)

* python >= 2.7
* boto3

## Options

| parameter      | required    | default | choices | comments             |
|----------------|-------------|---------|---------|----------------------|
| aws_access_key | no          |         |         | <div>AWS access key. If not set then the value of the AWS_ACCESS_KEY_ID, AWS_ACCESS_KEY or EC2_ACCESS_KEY environment variable is used.</div><br/><div style="font-size:small;">aliases: access_key</div> |


