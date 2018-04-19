# ansible-cisco-ios-demo

## Requirements

Create `group_vars/all/accounts.yml`:

```yaml
ansible_user:          admin
ansible_ssh_pass:      adminpass
ansible_become_pass:   enablepass
```

## Open Issues

-   [ ] <https://github.com/ansible/ansible/issues/38989>
-   [ ] <https://github.com/ansible/ansible/issues/39011>

## Usage

### Defining Additional Interface Settings

In order to define additional interface settings which are not covered via
an existing Ansible module you can define the lines which should be executed
against the interface.

Interface settings can be found in [group_vars/all/interfaces.yml](group_vars/all/interfaces.yml)

Example:

```yaml
---
ios_interfaces:
  GigabitEthernet1/0/4:
    description:         unconfigured
    enabled:             true
    l2:
      access_vlan:       1
      mode:              access
      state:             unconfigured
    l3:
      ipv4:              []
      state:             absent
    lines:
      - no spanning-tree portfast
    speed:               auto
    state:               present
  Vlan10:
    description:         OSPF_Uplink_To_Router
    enabled:             true
    l3:
      ipv4:              10.10.10.3/24
      state:             present
    lines:
      - ip ospf cost 10
    speed:               auto
    state:               present
```
