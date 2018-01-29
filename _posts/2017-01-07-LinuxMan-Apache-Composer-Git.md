---
layout: post
title: LinuxMan Apache Composer Redis Git
---

### Linux Unix Command

- [My gist - Linux Unix Command](https://gist.github.com/ambuilding/3ba2567c2b40f3aeb786988e42201b51)



### A Chat Application with Redis / socket.io

### PubSub
- PubSub, where a message is sent to a centralized topic channel.
- Interested parties can subscribe to this channel to be notified of updates.
- This pattern decouples the publisher and subscribers, so that the set of subscribers can grow or shrink without the knowledge of the publisher.

- PubSub is implemented on a backend server, to which clients communicate using WebSockets.
- WebSockets is a persistent TCP connection that provides a channel for data to be streamed bidirectionally between the client and server.

- Single-Server PubSub Architecture / Multiserver architecture


- A production system would likely modularize the UI components using external .vue files and transpiling using webpack on build.

### Link

- [nstalling Node.js via package manager](https://nodejs.org/en/download/package-manager/)
- [PM2](http://pm2.keymetrics.io/docs/usage/quick-start/)
- [How to Build a Chat Application with Amazon ElastiCache for Redis](https://aws.amazon.com/blogs/database/how-to-build-a-chat-application-with-amazon-elasticache-for-redis/)


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

### [How to open a port in the firewall on CentOS or RHEL](http://ask.xmodulo.com/open-port-firewall-centos-rhel.html)

```
`# iptables -L`
`# firewall-cmd --zone=public --add-port=80/tcp --permanent`
`# firewall-cmd --reload`
`# firewall-cmd --list-all`
```

### [How To Set Up a Firewall Using FirewallD on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-centos-7)


### Git

- [Install Git on Linux](https://git-scm.com/download/linux) `sudo yum install git`
- `git clone -b <name> repo`
