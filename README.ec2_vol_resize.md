# ec2_vol_resize - extend an existing drive 

## Synopsis

That module permits to resize a Amazon EC2 volume (extend, not reduce) in one action, where the common Ansible action is creating a snapshot, create a extended volume from that snapshot, detach the old volume, attach the new volume and delete the snapshot and the old volume.
It also correct the "Cannot specify volume_size and either one of name or id" bug ([#7719](https://github.com/ansible/ansible/issues/7719)).

## Requirements (on host that executes module)

* python >= 2.7
* boto3

## Options

| parameter      | required    | default | choices | comments             |
|----------------|-------------|---------|---------|----------------------|
| aws_access_key | no          |         |         | <div>AWS access key. If not set then the value of the AWS_ACCESS_KEY_ID, AWS_ACCESS_KEY or EC2_ACCESS_KEY environment variable is used.</div><br/><div style="font-size:small;">aliases: access_key</div> |
| aws_secret_key | no          |         |         | <div>AWS secret key. If not set then the value of the AWS_SECRET_ACCESS_KEY, AWS_SECRET_KEY, or EC2_SECRET_KEY environment variable is used.</div><br/><div style="font-size:small;">aliases: ec2_secret_key, secret_key</div> |
| device_name    | no          |         |         | <div>name of the device to resize when it's attached to a given instance. If the 'volume_id' parameter is not specified, the fields 'instance_id' and 'device_name' are required.</div><br/><div style="font-size:small;">aliases: device</div> |
| instance_id    | no          |         |         | <div>id of the instance which the resized volume is attached on. If the 'volume_id' parameter is not specified, the fields 'instance_id' and 'device_name' are required.</div><br/><div style="font-size:small;">aliases: instance</div> |
| region         | no          |         |         | <div>The AWS region to use. If not specified then the value of the EC2_REGION environment variable, if any, is used. See http://docs.aws.amazon.com/general/latest/gr/rande.html#ec2_region</div><br/><div style="font-size:small;">aliases: aws_region, ec2_region</div> |
| size           | yes         |         |         | <div>Size (in Gigabytes) of the newly resized volume</div><br/><div style="font-size:small;">aliases: volume_size</div> |
| timeout        | no          |     300 |         | The number of seconds before the module tasks exits on error |
| volume_id      | no          |         |         | <div>id of the volume to resize. Required in case of detached volume</div><br/><div style="font-size:small;">aliases: subnet, subnet_id</div> |

## Examples

```
# Note: These examples do not set authentication details, see the AWS Guide for details.

# Extend the first drive to 40GB
- ec2_vol_resize:
    instance_id: i-000001
    size: 40
    device_name: /dev/sda1

# Increase the size of a given drive by 20GB
- hosts: localhost
  gather_facts: False
  vars:
    volume_id: vol-foobar
  tasks:
    - ec2_vol_facts:
        filters:
          volume-id: "{{ volume_id }}"
      register: aws_vol
    - set_fact: size={{ item.size + 20 }}
      with_items: "{{ aws_vol.volumes }}"
    - ec2_vol_resize:
        volume_id: "{{ volume_id }}"
        size: "{{ size }}"
```

## Notes

* If parameters are not set within the module, the following environment variables can be used in decreasing order of precedence : `AWS_ACCESS_KEY_ID` or `AWS_ACCESS_KEY` or `EC2_ACCESS_KEY`, `AWS_SECRET_ACCESS_KEY` or `AWS_SECRET_KEY` or `EC2_SECRET_KEY`, `AWS_SECURITY_TOKEN` or `EC2_SECURITY_TOKEN`, `AWS_REGION` or `EC2_REGION`
* Since the operation create a new volume from a snapshot, the returning volume id will be different from the original one.
* Or the parameter 'volume_id', or the parameters 'instance_id' and 'device_name' are required


