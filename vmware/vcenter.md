---
layout: default
title: VMware vCenter
parent: VMware
---

# VMware vCenter

VMware vCenter is the virtualization solution for enterprise environments.

用于管理多个 ESXi 实例

### FAQ

***Changing your vCenter Server’s FQDN***

> [400] An error occurred while sending an authentication request to the vCenter Single Sign-On server - An error occurred when processing metadata during vCenter Single Sign-On setup: the service provider validation failed. Verify that the server URL is correct and is in FQDN format, or that the hostname is a trusted service provider alias.

Process to workaround the issue:
To enable short name access to vCenter, add the desired shortname in webclient.properties file.
Note: Ensure you have a backup of vCenter Server Appliance (vcsa) before making any changes

Log in to the vCenter Server via SSH/PuTTY session as root, and enable shell
Stop the vSphere client service using below command

```sh
service-control --stop vsphere-ui
```

Navigate to the vsphere-ui location to edit `webclient.properties`, Add the desired shortname under the `sso.serviceprovider.alias.whitelist`

```shell
~$ vim /etc/vmware/vsphere-ui/webclient.properties
```

```ini
sso.serviceprovider.alias.whitelist=vcsa70
```

Start the vSphere client service.

```sh
service-control --start vsphere-ui
```

+ https://kb.vmware.com/s/article/71387
+ https://blogs.vmware.com/vsphere/2019/08/changing-your-vcenter-servers-fqdn.html


***Update 8.0.2.00100 for component vlcm is not found***

[Patching vCenter to 8.0U2 using Update Planner fails with error "Update 8.0.2.00000 for component vlcm is not found" (94779)](https://kb.vmware.com/s/article/94779)

```sh
#!/bin/bash

# Define the file name and replacement strings
echo "Starting to fix the vCenter Server Reduced Downtime feature"
file_name="/usr/lib/applmgmt/update/py/vmware/appliance/update/update_b2b.py"
file_name_bak="/usr/lib/applmgmt/update/py/vmware/appliance/update/update_b2b.py.bak"
old_string='wgetWrapper(url + "/", tempFolder, "\*" + RPM_MANIFEST_FILE)'
new_string='wgetWrapper(url + "/" + "vlcm-rpm-manifest.json", tempFolder)'

echo "Backing up the file where changes will go in"
cp $file_name $file_name_bak

# Use sed to replace the old string with the new string in the file
echo "Patching the file"
sed -i "s|$old_string|$new_string|g" "$file_name"

# Restart applmgmt service to pick up changes.
echo "Restarting Appliance Management Service"
service-control --restart applmgmt

echo "Fixed the vCenter Server Reduced downtime upgrade"
```

To resolve the issue, run the script `fix_rdu.sh` attached to this KB.

```shell
root@vmware-vcenter [ ~ ]# ./fix_rdu.sh
Starting to fix the vCenter Server Reduced Downtime feature
Backing up the file where changes will go in
Patching the file
Restarting Appliance Management Service
Successfully restarted service applmgmt
Fixed the vCenter Server Reduced downtime upgrade
```
