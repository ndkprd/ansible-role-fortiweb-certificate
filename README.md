# ansible-role-fortiweb-certificate

## Description

Ansible role to import and apply SSL certificate to Fortinet's FortiWeb devices.

## Usage

### Installation

```bash
ansible-galaxy install ndkprd.fortiweb_certificate
```

### Hosts Example

```ini
[fortiweb]
fwb-01 ansible_host=fwb-01.example.com ansible_user=ansible ansible_password=supersecretpassword

[fortiweb:vars]
ansible_network_os=fortinet.fortiweb.fwebos
ansible_httpapi_use_ssl="yes"
ansible_httpapi_validate_certs="no"
ansible_httpapi_port=443
```

### Playbook Example

```yaml
---

- name: Import SSL certificate.
  hosts: fortiweb
  become: false
  gather_facts: false
  connection: local
  vars:
    fortiweb_certificate_vdom: "root"
    fortiweb_certificate_file: "example.com_2024-2025.crt"
    fortiweb_certificate_private_key: "example.com_cert_private.key"
    fortiweb_certificate_intermediate: "example.com_intermediate.crt"
    fortiweb_certificate_server_policy: "example-com-server-policy"

  roles:
    - ndkprd.fortiweb_cert

```

## TODO

- [ ] Add support for multiple certificates/server-policy.

## License

[MIT](./LICENSE)
