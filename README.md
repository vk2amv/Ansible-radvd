
# Ansible Role: RADVD Daemon

## Description

Ansible role to install and configure Linux IPv6 Router Advertisement Daemon [RADVD](https://radvd.litech.org/).

https://linux.die.net/man/8/radvd

https://linux.die.net/man/5/radvd.conf

https://manpages.debian.org/testing/radvd/radvd.conf.5.en.html

## Example Vars for minimal RADVD instance

```yml
---
radvd_daemon_run: true

radvd_daemon_interfaces:
  - interface: "eth0"
    options:
        advsendadvert: "on"
        minrtradvinterval: "3"
        maxrtradvinterval: "10"
    prefixes:
      - prefix: "2001:0db8:0100:f101::/64"
        advonlink: "on"
        advautonomous: "on"
        advrouteraddr: "on"
```

## Example Vars for configuring RADVD on two interfaces

```yml
---
radvd_daemon_run: true

radvd_daemon_interfaces:
  - interface: "eth0"
    options:
        advsendadvert: "on"
        minrtradvinterval: "3"
        maxrtradvinterval: "10"
    prefixes:
      - prefix: "2001:0db8:0100:f101::/64"
        advonlink: "on"
        advautonomous: "on"
        advrouteraddr: "on"
  - interface: "eth1"
    options:
        advsendadvert: "on"
        minrtradvinterval: "3"
        maxrtradvinterval: "10"
    prefixes:
      - prefix: "2001:0db8:0100:e101::/64"
        advonlink: "on"
        advautonomous: "on"
        advrouteraddr: "on"        
```

## Example Vars for configuring RADVD with multiple prefixes on single interface and also advertising a DNS server to use

```yml
---
radvd_daemon_run: true

radvd_daemon_interfaces:
  - interface: "eth0"
    options:
        advsendadvert: "on"
        minrtradvinterval: "3"
        maxrtradvinterval: "10"
    prefixes:
      - prefix: "2001:0db8:0100:f101::/64"
        advonlink: "on"
        advautonomous: "on"
        advrouteraddr: "on"
      - prefix: "2001:0db8:0100:e101::/64"
        advonlink: "on"
        advautonomous: "on"
        advrouteraddr: "on"
    nameservers:
      - rdnss: "2606:4700:4700::1111"           
```


## Example Playbook

```yml
- hosts: all
  roles:
     - radvd-daemon
```


### v1.0.0

- Initial git push to Github




## Author
* Lindsay Harvey

## License

This project is under the MIT License. See the LICENSE file for the full license text.

## Copyright

- Copyright (c) 2022 Lindsay Harvey
