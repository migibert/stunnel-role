Stunnel
=========
[![Galaxy](http://img.shields.io/badge/ansible--galaxy-stunnel-blue.svg)](https://galaxy.ansible.com/list#/roles/3502)
[![License](http://img.shields.io/:license-mit-blue.svg)](http://doge.mit-license.org)


Ansible role to install stunnel in order to achieve SSL Termination on Linux machines.

Install it with `ansible-galaxy install migibert.stunnel`


Role Variables
--------------

```
stunnel_use_cert (default True) : determines if we use certificates
stunnel_use_psk (default False) : determines if we use psk
stunnel_certificate_generation (default False) : determines if this role has to generate a self signed certificate
stunnel_certificate_duration: (optional, if stunnel_certificate_generation is True, default 365) : self signed certificate validity duration
stunnel_certificate_domain: (optional, if stunnel_certificate_generation is True, default www.domain.com) : self signed certificate domain field
stunnel_certificate_country: (optional, if stunnel_certificate_generation is True, default FR) : self signed certificate country field
stunnel_certificate_organization: (optional, if stunnel_certificate_generation is True, default organization) : self signed certificate organization field
stunnel_certificate_state_name: (optional, if stunnel_certificate_generation is True, default state) : self signed certificate state field
stunnel_certificate_locality: (optional, if stunnel_certificate_generation is True, default locality) : self signed certificate locality field
stunnel_certificate_file: certificate file to generate or use, depends on stunnel_certificate_generation value. Default is /tmp/certificate.pem
stunnel_key_file: key file to generate or use, depends on stunnel_certificate_generation value. Default is /tmp/key.pem
stunnel_psks: a list of psk. This look like this:
- name: client1
  psk: AEO/WE+pBCn3+WBy3FJoyJF/HEBZqMym

stunnel_services: list of services. They look like this:
- service:
  name: https
  accept: 443
  connect: 80

```

Dependencies
------------

This role has no dependencies.

Example Playbook
----------------

```
- hosts: all

  roles:
  - role: stunnel-role
    stunnel_certificate_generation: True
    stunnel_certificate_duration: 365
    stunnel_certificate_domain: www.domain.com
    stunnel_certificate_country: FR
    stunnel_certificate_organization: Gibert
    stunnel_certificate_state_name: Paris
    stunnel_certificate_locality: Paris
    stunnel_certificate_file: /tmp/stunnel.pem
    stunnel_key_file: /tmp/key.pem
    stunnel_services:
      - service:
        name: https
        accept: 443
        connect: 80
```

you may also use [PSK (Pre Shared Keys)](https://www.stunnel.org/auth.html)
which allow faster communication
at the cost of knowing clients in advance.

```
- hosts: all

  roles:
  - role: stunnel-role
    stunnel_use_certificate: false
    stunnel_use_psk: true
    stunnel_psks:
      - name: client1
        key: ATJX7VOAMIF2nhaknNVmSqSQGrCvMyPt
      - name: client2
        key: enNezGQMkZmSyjTDjpndjrBEXhJ9ki3v
    stunnel_services:
      - service:
        name: postfix
        accept: 12221
        connect: 21
```


License
-------

MIT

Author Information
------------------

Mikaël Gibert, Developer / Devops
