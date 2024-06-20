# Access

The access role can explicitly grant users or groups access to a server by
adding content to /etc/security/access.conf to enhance server security posture.

Two default, but optional, variables ensures that the root user retains access
and denies all others. A common variable defines a access for system
administrators or service accounts. An extra variable is available to
define others that can access a server in a group_var or host_var.

## Requirements

None.

## Role variables

- `access_conf_enabled`
  - Default: `true`
  - Description: Used to enable or disable this entire role. Disabling the role
    doesn't clear the access.conf file.
  - Type: bool
  - Required: yes
- `access_conf_manage_pam`
  - Default: `false`
  - Description: Used to enable or disable the pam_access.so module. Disabled
    by default because faulty PAM configuration can lock you out of your
    system. Make backups and test in lower environments thoroughly before
    enabling in production!
  - Type: bool
  - Required: yes
- `access_conf_allow_root`
  - Default: `true`
  - Description: Permit root from all origins.
  - Type: bool
  - Required: yes
- `access_conf_default_deny`
  - Default: `true`
  - Description: Deny all others from all origins.
  - Type: bool
  - Required: yes
- `access_conf_common_entries`
  - Default: ``
  - Description: List of dictionaries used to define access for all managed
    endpoints, intended for system administrators and service accounts. Accepts
    name for the list item, origins, and permissions. See `man access.conf` for
    more details.
  - Type: list
  - Required: no
- `access_conf_extra_entries`
  - Default: ``
  - Description: List of dictionaries used to define access for group or host
    vars.
  - Type: list
  - Required: no

## Dependencies

None.

## Example playbook

```yml
    - hosts: servers
      vars:
        access_conf_enabled: true
        access_conf_allow_root: true
        access_conf_default_deny: true
        access_conf_common_entries:
          - name: 'admins'
            origins:
              - ALL
            permissions: '+' # optional, defaults to `+`

      roles:
         - barstown.server_baseline.access
```
