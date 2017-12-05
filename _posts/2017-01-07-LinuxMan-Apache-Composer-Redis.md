---
layout: post
title: LinuxMan Apache Composer Redis
---

### Redis

- [Install redis on EC2 Amazon linux AMI / The latest stable Redis version](https://gist.github.com/ambuilding/1fd59869f8944f2eb834eb42cb5e470c)
- [Redis Quick Start](https://redis.io/topics/quickstart)
- [Install Redis v3.2 on AWS EC2 Instance](https://medium.com/@andrewcbass/install-redis-v3-2-on-aws-ec2-instance-93259d40a3ce)

### Composer

- [Install composer on Amazon EC2 Linux](https://gist.github.com/ambuilding/ad26e36ecc14a20dcb625554620e3689)

### Apache

```
Apache:
Apachectl: $ sudo apachectl start / stop / restart
Php.ini: /usr/local/php5/lib/php.ini

Hosts: $ vi /etc/hosts

A. $ cd /etc/apache2/
B. $ vi httpd.conf
# uncomment the following lines:
LoadModule deflate_module libexec/apache2/mod_deflate.so
LoadModule expires_module libexec/apache2/mod_expires.so
LoadModule rewrite_module libexec/apache2/mod_rewrite.so

/Library/WebServer/Documents
```

### [Install net-tools command in CentOS 7 / RHEL 7](https://www.ostechnix.com/linux-troubleshooting-netstat-command-not-found-in-centos-7-rhel-7/)

First, we should find out which package provides ‘netstat’ command.

```
`# yum provides */netstat`
`# yum whatprovides */netstat`

`# yum install net-tools`

`# netstat`
```

## [How to open a port in the firewall on CentOS or RHEL](http://ask.xmodulo.com/open-port-firewall-centos-rhel.html)

```
`# iptables -L`
`# firewall-cmd --zone=public --add-port=80/tcp --permanent`
`# firewall-cmd --reload`
`# firewall-cmd --list-all`
```

## [How To Set Up a Firewall Using FirewallD on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-centos-7)
