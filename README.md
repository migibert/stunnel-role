Stunnel
=========
[![Galaxy](http://img.shields.io/badge/ansible--galaxy-stunnel-blue.svg)](https://galaxy.ansible.com/list#/roles/3502)
[![License](http://img.shields.io/:license-mit-blue.svg)](http://doge.mit-license.org)  


Ansible role to install stunnel in order to achieve SSL Termination on Linux machines.

Install it with `ansible-galaxy install migibert.stunnel`


Role Variables
--------------

```
stunnel_certificate_generation (default False) : determines if this role has to generate a self signed certificate
stunnel_certificate_duration: (optional, if stunnel_certificate_generation is True, default 365) : self signed certificate validity duration
stunnel_certificate_domain: (optional, if stunnel_certificate_generation is True, default www.domain.com) : self signed certificate domain field
stunnel_certificate_country: (optional, if stunnel_certificate_generation is True, default FR) : self signed certificate country field
stunnel_certificate_organization: (optional, if stunnel_certificate_generation is True, default organization) : self signed certificate organization field
stunnel_certificate_state_name: (optional, if stunnel_certificate_generation is True, default state) : self signed certificate state field
stunnel_certificate_locality: (optional, if stunnel_certificate_generation is True, default locality) : self signed certificate locality field
stunnel_certificate_file: certificate file to generate or use, depends on stunnel_certificate_generation value. Default is /tmp/certificate.pem
stunnel_key_file: key file to generate or use, depends on stunnel_certificate_generation value. Default is /tmp/key.pem
stunnel_services: list of services. They look like this:
- service:
    name: https
    accept: 443
    connect: 80
    client: "yes"  # defaults to "no"
```

(beware, set client to string "yes", not to yes alone, which, in yaml, is boolean value true)

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

License
-------

MIT

Author Information
------------------

Mikaël Gibert, Developer / Devops
