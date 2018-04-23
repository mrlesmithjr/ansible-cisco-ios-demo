<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [ansible-cisco-ios-demo](#ansible-cisco-ios-demo)
  - [Requirements](#requirements)
    - [Variables](#variables)
    - [Inventory](#inventory)
  - [Open Issues](#open-issues)
  - [Usage](#usage)
    - [Defining Additional Interface Settings](#defining-additional-interface-settings)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# ansible-cisco-ios-demo

## Requirements

### Variables

Create `group_vars/all/accounts.yml`:

```yaml
ansible_user:          admin
ansible_ssh_pass:      adminpass
ansible_become_pass:   enablepass
```

### Inventory

Update [inventory](hosts.yml) based on your needs.

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
