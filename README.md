# Radarr
Radarr installation from public release tarball.

## Requirements
[supported platforms](https://github.com/r-pufky/ansible_radarr/blob/main/meta/main.yml)

## Role Variables
[defaults](https://github.com/r-pufky/ansible_radarr/tree/main/defaults/main)

### Ports
All ports and protocols have been defined for the role.

[defaults/ports.yml](https://github.com/r-pufky/ansible_radarr/blob/main/defaults/main/ports.yml)

## Dependencies
**galaxy-ng** roles cannot be used independently. Part of
[r_pufky.arr](https://github.com/r-pufky/ansible_collection_ar) collection.

## Example Playbook
Read defaults documentation.

Install latest release of Radarr; ensuring media files have proper permissions.
Version (and databases) will be migrated and updated on new releases. Media
permissions will be set to ensure Radarr can read files.
``` yaml
- name: 'radarr server'
  hosts: 'radarr.example.com'
  become: true
  roles:
     - 'r_pufky.arr.radarr'
  vars:
    radarr_srv_version: 'latest'
    radarr_cfg_api_key: '{{ vault_radarr_api_key }}'
    radarr_cfg_update_automatically: true
    radarr_cfg_theme: 'dark'
    radarr_srv_media_root_folders:
      - '/data/media'
    radarr_srv_media_set_perms_file_enable: true
```

### Initial Deployment with No User
New installs REQUIRE 'external' to create a login user; authentication can be
toggled on after the user exists in the database . Suggest running initial role
application temporarily disabling this option:

``` bash
ansible-playbook radarr.yml -e 'radarr_cfg_authentication_method=external'
```

### Postgres Support
Postgres is supported in the role, however, sqlite3 to postgres migrations must
be done manually. See defaults and Radarr documentation.

[defaults/database.yml](https://github.com/r-pufky/ansible_radarr/blob/main/defaults/main/database.yml)

[Radarr Postgres](https://wiki.servarr.com/radarr/postgres-setup)

## Development
Configure [environment](https://r-pufky.github.io/ansible_collection_docs/ansible/environment)

Run all unit tests:
``` bash
molecule test --all
```

### Releases
Release format: **{OS}-{SERVICE}-{ROLE}**

Each type inherits the versioning system used; defaulting to schematic
versioning.

`12-2.0.3-1.0.0`

* 12 - Debian 12 (bookworm).
* 2.0.3 - Service/app version.
* 1.0.0 - Role version.

Releases are branched on Debian releases:

* **[13.x.x](https://github.com/r-pufky/ansible_radarr)**: 13 Trixie.
* **[12.x.x](https://github.com/r-pufky/ansible_radarr/tree/12.x)**: 12 Bookworm.

## Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License](https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0)
 [(direct link)](https://github.com/r-pufky/ansible_radarr/blob/main/LICENSE)

## Author Information
PGP Fingerprint: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9](https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9)
| [github gist](https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22)
