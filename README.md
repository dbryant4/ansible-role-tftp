# TFTP Role

[![Build
Status](https://travis-ci.org/dbryant4/ansible-role-tftp.svg?branch=master)](https://travis-ci.org/dbryant4/ansible-role-tftp)

## Description

This role manages the installation of TFTP on a Raspberry Pi, although it
should be able to manage any other Debian based system. This role also
sets up a basic PXE boot environment by downloading some files from a
Centos 7 mirror and also pointing newly booted nodes to that mirror for
the installation media.

When this role completes successfuly and assuming you update your DHCP
server's `next-server` option to point to the Ansible node, you will be
able to boot a machine over the network using PXE and will be presented
with a menu with the option to install CentOS 7. When you select CentOS
7, it should start the installer to ask the user what packages to
install, timezone, root password, etc.

## Provides

1. An TFTP server
2. Basic PXE boot environment (note: you still need to setup the
   next-server on your DHCP server)

## Requires

1. Ansible 1.7 or higher
2. Raspberry Pi (possibly other Debian based systems)

## Variables
- tftp_centos_mirror - the http URL for a CentOS server near you. This
  can be over the internet or a local node on your network.
- tftp_tftpboot_dir - the directory where to place all of the PXE boot
  files.
- tftp_ks_method - URL of the installation media for CentOS 7. Usually
  the same as the `tftp_centos_mirror`.

### Changing Variable Values

To Change the value of variables, create a file in `host_vars/` or `group_vars/` or define variables in the playbook.

There are other options for changing variable values. See [Ansible
Variable
Documentation](http://docs.ansible.com/playbooks_variables.html) for
more ideas.

## Usage

Include this role in your plays and set varaibles as desired.

```yaml
---
  name: tftp-servers
  hosts: tftp-servers
  vars:
    tftp_centos_mirror: 'http://mymirror.local/centos/7/x86_64'
    tftp_ks_method:     'http://mymirror.local/centos/7/x86_64'
  roles:
    - tftp
```

## Tests
This role includes Travis CI tests.
