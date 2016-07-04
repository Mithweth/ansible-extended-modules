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
| aws_secret_key | no          |         |         | <div>AWS secret key. If not set then the value of the AWS_SECRET_ACCESS_KEY, AWS_SECRET_KEY, or EC2_SECRET_KEY environment variable is used.</div><br/><div style="font-size:small;">aliases: ec2_secret_key, secret_key</div> |
| group_id       | no          |         |         | <div>security group id (or list of ids) to use with the instance</div><br/><div style="font-size:small;">aliases: security_group_id, security_group_ids, security_group, security_groups</div> |
| instance_id    | yes         |         |         | <div>id of the instance which changes are applied on</div><br/><div style="font-size:small;">aliases: instance</div> |
| instance_tags  | no          |         |         | <div>a hash/dictionary of tags to add to the instance; '{"key":"value"}' and '{"key":"value","key":"value"}'</div><br/><div style="font-size:small;">aliases: tags</div> |
| instance_type  | no          |         |         | new instance type to use for the instance, see http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html |
| key_name       | no          |         |         | <div>new key pair to use on the instance</div><br/><div style="font-size:small;">aliases: keypair, ssh_key</div> |
| region         | no          |         |         | <div>The AWS region to use. If not specified then the value of the EC2_REGION environment variable, if any, is used. See http://docs.aws.amazon.com/general/latest/gr/rande.html#ec2_region</div><br/><div style="font-size:small;">aliases: aws_region, ec2_region</div> |
| state          | no          | running | <ul><li>running</li><li>stopped</li></ul> | instance state after changes |
| timeout        | no          |     300 |         | The number of seconds before the module tasks exits on error |
| vpc_subnet_id  | no          |         |         | <div>the new subnet ID in which to launch the instance</div><br/><div style="font-size:small;">aliases: subnet, subnet_id</div> |
| wait           | no          |     no  | <ul><li>yes</li><li>no</li></ul> | wait for the instance to be in the desired state before returning |
| zone           | no          |         |         | <div>AWS availability zone in which to launch the instance</div><br/><div style="font-size:small;">aliases: availability_zone, placement, aws_zone, ec2_zone</div> |


