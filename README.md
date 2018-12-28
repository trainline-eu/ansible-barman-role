## Barman Ansible role [![Build Status](https://travis-ci.org/trainline-eu/ansible-barman-role.svg?branch=master)](https://travis-ci.org/trainline-eu/ansible-barman-role)

Ansible role which installs and configures Barman, a backup manager for Postgresql.

#### Installation

This role has been tested on Ansible 2.3.0 and higher.

To install:

```
ansible-galaxy install trainline-eu.ansible_barman_role
```

#### Dependencies

No dependencies

Recommended related roles:
- trainline-eu.ansible_postgresql_role

#### Compatibility matrix

This table lists the tested version of OS/Barman couples.

| Distribution / PostgreSQL | 2.x |
| ------------------------- |:---:|
| Debian 8.x |  :white_check_mark:|
| Debian 9.x |  :white_check_mark:|

- :white_check_mark: - tested, works fine

#### Variables

```yaml
# Basic settings
barman_databases:                                 # Mandatory
  - name: 'app1'                                     # Mandatory
    description: 'Database of App1'                  # Mandatory
    primary_host: 10.0.0.1                           # Mandatory
    postgres_barman_password: 'super_secure_vaulted' # Mandatory
    backup_method: rsync                             # Optional (default value)
    ansible_group: "db-app1"                         # Optional (used to authorize SSH access)
    retention_policy: 'RECOVERY WINDOW OF 7 DAYS'    # Optional (default value)

barman_restore_directory: "/home/restore-$server"

barman_rsync_daemon_enabled: true (default to false)
# If Rsync daemon is enabled
barman_rsync_allowed_hosts: 10.0.0.0/24
barman_rsync_password: "vaulted_secret_password"

# Barman configuration
# See http://docs.pgbarman.org/release/2.4/barman.5.html#configuration-file-syntax
# to understand the following settings
barman_config:                        # Optional
  reuse_backup: "None|link|copy"
  bandwith_limit: 0
  parallel_jobs: 2
  network_compression: true|false
```

#### Testing

There are currently no tests written in this project.

However the role is tested together with the [postgresql role](https://github.com/trainline-eu/ansible-postgresql-role) in a set of automatic integration tests.

#### License

Licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.

#### Thanks

Creators:
- [Gaëtan Duchaussois](https://twitter.com/gduchaussois)
- [Théophile Helleboid](https://twitter.com/chtitux)
- [Paul Bonaud](https://twitter.com/paulRb_r)

Maintainers:
- [Théophile Helleboid](https://twitter.com/chtitux)
- [Paul Bonaud](https://twitter.com/paulRb_r)

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/trainline-eu/ansible-barman-role/issues)!
