# Role: configure_timesync

## Description
This role configures time synchronization on RHEL servers using the certified RHEL system roles collection (`redhat.rhel_system_roles.timesync`). It allows you to set custom NTP servers and a timezone, and can optionally restart the `chronyd` service to apply changes.

## Requirements
- Ansible version >= 2.9
- Collections: `redhat.rhel_system_roles`

## Role Variables
### Default Variables

- `restart_chronyd_service` (default: `true`):
  - Specifies whether the `chronyd` service should be restarted after configuration changes are made.
  - **Type**: Boolean
  - **Example**: `false`

- `user_ntp_servers` (default: `['0.rhel.pool.ntp.org', '1.rhel.pool.ntp.org', '2.rhel.pool.ntp.org', '3.rhel.pool.ntp.org']`):
  - A list of NTP server addresses to use for time synchronization. Custom NTP servers can be specified if desired.
  - **Type**: List of strings
  - **Example**:
    ```yaml
    user_ntp_servers:
      - 'time.example.com'
      - 'ntp.example.org'
    ```

- `user_timezone` (default: `"UTC"`):
  - Specifies the timezone to set on the server.
  - **Type**: String
  - **Example**: `"America/New_York"`

## Dependencies
This role depends on the following collection:
- `redhat.rhel_system_roles` for managing timesync configuration.

## Example Playbook Usage
Here is an example of how to use the `configure_timesync` role:

```yaml
- hosts: all
  become: true
  roles:
    - role: configure_timesync
      vars:
        user_ntp_servers:
          - "time.example.com"
        user_timezone: "America/New_York"
```
