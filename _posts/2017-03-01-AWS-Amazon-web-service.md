---
layout: post
title: AWS Amazon web service
---

## Hello

### EC2

- The Amazon Linux AMI is an EBS-backed, AWS-supported image. The default image includes AWS command line tools, Python, Ruby, Perl, and Java. The repositories include Docker, PHP, MySQL, PostgreSQL, and other packages.

- [Amazon Elastic Compute Cloud](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
- [Launch a Linux Virtual Machine
with Amazon EC2](https://aws.amazon.com/getting-started/tutorials/launch-a-virtual-machine/)
- [Installing a LAMP Web Server on Amazon Linux](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-LAMP.html)
  - Apache `/etc/httpd/conf/httpd.conf` `sudo service httpd restart` `sudo a2enmod rewrite`
  - [Set up mod_rewrite / for Apache on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-set-up-mod_rewrite-for-apache-on-centos-7)

  - Install the Mbstring PHP Extension / php 7.0 `$ sudo yum install php70-mbstring`
  - Permission:
  - `sudo chmod 775 -R storage/`
  - `sudo chmod 775 -R bootstrap/cache`

- [Configure Apache Web Server on Amazon Linux to Use SSL/TLS](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/SSL-on-an-instance.html)

- `$ cd /var/www` `$ composer update`
- `$ composer install --no-dev`
- `composer install --optimize-autoloader`
- `php artisan key:generate` `php artisan storage:link`
- Make sure to turn on production mode when deploying for production. (Vue)


### RDS
- Connect to the database / Sequel Pro / Security group add rule

- Elastic beanstalk
- AWS Security Credentials
  - Root vs. IAM User Credentials
  - Access keys sign programmatic requests / CLIs

- Creating IAM users (Console)
  - Create group

- .ebextensions
  - config/container_commands

## CLI

- ssh
  - ssh -i
  - Key pairs


## Link
- [elasticbeanstalk](https://aws.amazon.com/elasticbeanstalk/)
- [Laravel / Setting up Elastic Beanstalk](https://deliciousbrains.com/scaling-laravel-using-aws-elastic-beanstalk-part-3-setting-elastic-beanstalk/)
- [Deploying Laravel applications using AWS Elastic Beanstalk](http://blog.mallow-tech.com/2016/03/deploying-laravel-applications-using-aws-elastic-beanstalk/)
- [Laravel 5 on AWS Elastic Beanstalk – Production Guide](http://blog.goforyt.com/laravel-5-aws-elastic-beanstalk-production-guide/)


- [Example Snippets: ElastiCache / Redis](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/customize-environment-resources-elasticache.html#customize-environment-resources-elasticache-targetedvpc)


## ElasiCache

- A cache cluster in ElasiCache

- Best practices and Usage patterns
- [Getting Started with Amazon ElastiCache](https://aws.amazon.com/elasticache/getting-started/)
