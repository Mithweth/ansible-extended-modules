# ansible-extended-modules
Modules I've developed to make actions that Ansible doesn't permit (yet)

Example :
```
 - ec2_modify:
     instance_id: i-000001
     region: eu-west-1
     instance_type: t2.nano
     zone: eu-west-1a
```
