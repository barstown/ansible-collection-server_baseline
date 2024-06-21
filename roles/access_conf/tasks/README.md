<!-- BEGIN_ANSIBLE_DOCS -->
# Ansible Role: barstown.server_baseline.access_conf
---
Version: 1.0.0

Access is used to deploy the /etc/security/access.conf file which is used
to control who can access the endpoint and from which origins.


Tags: access, security, pam

## Requirements
---
| Platform | Versions |
| -------- | -------- |
| EL | 8, 9 |
| Debian | bookworm |

## Role Arguments
---
### Entrypoint: main
---
The main entrypoint for the access_conf role v7

|Option|Description|Type|Required|Default|
|---|---|---|---|---|
| access_conf_entry_common | List of common access control entries | list of dicts of 'access_conf_entry_common' options | no |  |
| access_conf_entry_extra | List of extra access control entries | list of dicts of 'access_conf_entry_extra' options | no |  |

#### Options for main > access_conf_entry_common
---
|Option|Description|Type|Required|Default|
|---|---|---|---|---|
| name | Name of the access entry, likely a user or group | str | yes |  |
| origins | List of origins | list of 'str' | yes |  |
| permission | Permission type | str | no | + |

#### Options for main > access_conf_entry_extra
---
|Option|Description|Type|Required|Default|
|---|---|---|---|---|
| name | Name of the access entry, likely a user or group | str | yes |  |
| origins | List of origins | list of 'str' | yes |  |
| permission | Permission type | str | no | + |

#### Choices for main > access_conf_entry_common > permission
---
|Choice|
|---|
| + |
| - |

#### Choices for main > access_conf_entry_extra > permission
---
|Choice|
|---|
| + |
| - |

### Entrypoint: bool
---
The bool entry point for the access_conf role.

|Option|Description|Type|Required|Default|
|---|---|---|---|---|
| access_conf_enabled | Used to enable or disable this entire role. The access task deployes a template file that controls users or groups that are able to SSH to a server. Each of the three variables below do the same thing, but exist so that you may define different options globally (common), in a group var, or in a host var. The task will render the template on the server with a section dedicated to each variable. These should be defined as a list of dictionaries. | bool | yes | true |
| access_conf_manage_pam | Description: Used to enable or disable the pam_access.so module. `Disabled by default because faulty PAM` configuration can lock you out of your system. Make backups and test in lower environments thoroughly before enabling in production! | bool | yes | false |
| access_conf_allow_root | Permit root from all origins. | bool | yes | true |
| access_conf_default_deny | Deny all others from all origins. | bool | yes | true |


## Dependencies
---
None.

## Example Playbook
---
```
- hosts: all
  tasks:
    - name: Importing role: barstown.server_baseline.access_conf
      ansible.builtin.import_role:
        name: barstown.server_baseline.access_conf
      vars:
        
```

## License
---
MIT

## Author and Project Information
---
Kyle Barstow

<!-- END_ANSIBLE_DOCS -->
