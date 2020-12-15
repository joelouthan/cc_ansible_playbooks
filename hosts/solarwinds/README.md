# swinds-ansible-inv

Give credit where credit is due: [cbabs/solarwinds-ansible-inv](https://github.com/cbabs/solarwinds-ansible-inv)

---

## Requirements

Update your swinds.ini with the following:

```ini
npm_server = 10.10.10.10
npm_user = ansible
npm_password = **password**
```

## Changes from the original swinds.py

```python
#use_groups = True
use_groups = False

# Field for groups
#groupField = 'GroupName'
groupField = 'Location'

# payload = "query=SELECT C.Name as GroupName, N.SysName FROM Orion.Nodes as N JOIN Orion.ContainerMemberSnapshots as CM on N.NodeID = CM.EntityID JOIN Orion.Container as C on CM.ContainerID=C.ContainerID WHERE CM.EntityDisplayName = 'Node' AND N.Vendor = 'Cisco'"
payload="query=SELECT NodeID, SysName,IPAddress, Vendor, Location FROM Orion.Nodes WHERE Status=1"
```

---

## To test

`./swinds.py --list`

## To test with Ansible

`ansible -i solarwinds/swinds.py all -m ansible.builtin.ping`

## To install within Ansible Tower

1\. Log into Tower

2\. Click on Inventory Scripts

3\. Click on the green plus + button on the right side

4\. Name your script: Solarwinds

5\. Copy the contents of `swinds.py`

6\. Go back to Tower and paste within the CUSTOM SCRIPT typebox

7\. Save

8\. Click on Inventory and then green plus button for new Inventory 

9\. Name your inventory: Solarwinds Dynamic Inventory

10\. Save

11\. Click on Source and then click on green plus button to add a source

12\. Name your Source: Solarwinds source

13\. Source: Custom Script

14\. Under Custom Inventory Script, hit the Search button to find your script

15\. Save

16\. Click on Sources again and then the Sync button to pull your hosts

17\. Click on Hosts to verify