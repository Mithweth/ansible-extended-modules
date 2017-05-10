# vmware_module - Manages disks in vcenter

## Synopsis
* Creates VMDK disks to an existing instance (hotplug)
* Lists existing VMDK attached to an instance
* Removes from inventory and deletes from disks VMDK disks (hotplug)

## Requirements (on host that executes module)

* python >= 2.7
* python2-pyvmomi

## Options

| parameter      | required    | default | choices | comments             |
|----------------|-------------|---------|---------|----------------------|
| hostname       | yes         |         |         | The hostname or IP address of the vSphere vCenter. |
| name           | yes         |         |         | Name of the VM to work with<br/><div style="font-size:small;">aliases: guest</div>
| password       | yes         |         |         | The password of the vSphere vCenter.<br/><div style="font-size:small;">aliases: pass, pwd</div> |
| size           | no          |         |         | Disk size (in GB) (mandatory if state=present) |
| state          | no          | present | <ul><li>present</li><li>absent</li><li>list</li></ul> | <ul><li>if state=present, create the disk if the (optional) UUID doesn't exist</li><li>if state=absent, destroy the disk if the UUID corresponds</li><li>if state=list, display details about VM disks</li></ul> |
| username       | yes         |         |         | The username of the vSphere vCenter.<br/><div style="font-size:small;">aliases: user, admin</div> |
| uuid           | no         |         |         | Relevant disk UUID (mandatory if state=absent) |

## Examples

```
# Note: These examples do not set authentication details, see the PyVMomi Guide for details.

# Create of check existance for disk whose UUID is 00001
 - vmware_volume:
     guest: vmtoto
     uuid: 000001
     size: 10

# Create a disk on each iteration
 - vmware_volume:
     guest: vmtoto
     size: 10

# Delete the disk whose UUID is 00001
 - vmware_volume:
     guest: vmtoto
     uuid: 000001
     state: absent
```

## Return values

| name      | description    | returned | type | sample             |
|-----------|----------------|----------|------|--------------------|
| volumes   | metadata about VM guest disks | state=list | dict | None |




