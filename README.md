# smbmount

Ansible role that manages SMB/CIFS mounts on Linux systems.

## Requirements

This role requires the ability to mount SMB shares, which may not work on Linux containers, but will work on bare metal and in virtual machines.

## Role Variables

* `smb_credentials_path`: Path to the directory containing credentials files. By default this is `/etc/smb`.
* `smb_mountpoints`: A list of SMB mountpoints.
  * `name`: Mountpoint path
  * `state`: State of the mountpoint, eg. mounted, absent
  * `src`: SMB share path
  * `smb_username`: SMB share username
  * `smb_password`: SMB share password
  * `smb_domain`: In a domain environment, the domain name, eg. `contoso.com`
  * `user`: User the mountpoint is mounted as, defaults to root
  * `group`: Group the mountpoint is mounted as, defaults to root

## Dependencies

None

## Example Playbook

```yaml
- name: SMB mountpoint
  hosts: all
  become: true
  roles:
    - cmurphy.smbmount
  vars:
    smb_mountpoints:
      - name: "/mnt/files"
        state: mounted
        src: "//fileserver.domain.tld/files"
        smb_username: "smb_username"
        smb_password: "smb_password"
        smb_domain: "domain.tld"
        user: "root"
        group: "files"
```

## License

MIT

## Author Information

Colin Murphy 
