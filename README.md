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
[fortiwebs]
fwb-01 ansible_host=fwb-01.example.com ansible_user=ansible ansible_password=supersecretpassword

[fortiwebs:vars]
ansible_network_os=fortinet.fortiweb.fwebos
ansible_httpapi_use_ssl="yes"
ansible_httpapi_validate_certs="no"
ansible_httpapi_port=443
```

### Playbook Example

```yaml
---

- name: Import SSL certificate.
  hosts: fortiwebs
  become: false
  gather_facts: false
  vars:
    fortiweb_certificate_vdom: root
    fortiweb_certificates:
      - domain: dev.example.com
        private_key: /tmp/dev.example.com_cert_private.key
        certificate_file: /tmp/dev.example.com.crt
        certificate_intermediate: /tmp/dev.example.com_intermediate.crt
        server_policy: server-policy_dev.example.com
      - domain: example.com
        private_key: /tmp/example.com_cert_private.key
        certificate_file: /tmp/example.com.crt
        certificate_intermediate: /tmp/example.com_intermediate.crt
        server_policy: server-policy_example.com
  roles:
    - ndkprd.fortiweb_cert

```

## TODO

- [x] Add support for multiple certificates/server-policy.

## License

[MIT](./LICENSE)
