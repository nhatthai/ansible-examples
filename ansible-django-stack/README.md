#Ansible Django Stack

Ansible Playbook designed for environments running a Django app. It can install and configure these applications that are commonly used in production Django deployments:

+ Nginx
+ Gunicorn
+ Supervisor
+ Virtualenv
+ MySQL
+ Django

Tested with EC2: Ubuntu 14.04 LTS x64

Requirements:
============
+ [Ansible](http://docs.ansible.com/ansible/intro_installation.html)
+ [Vagrant](https://www.vagrantup.com/downloads.html)
+ [VirtualBox](https://www.virtualbox.org/wiki/Downloads)


Vagrant
========
+Ubuntu: My SQL Server & Web App


Staging
========
+ EC2: My SQL Server & Web App


Production
===========
+ RDS MySQL: My SQL Server
+ EC2: Web App


Run the playbook:
=================
Please make sure that you added id_rsa.pub into your machine as well as the repository(github or bitbucket)


+ Run on vagrant:
	```
	$cd ansible-django-stack
	$ansible-django-stack$ ansible-playbook -i vagrant deploy.yml
	```

+ Run on staging:
	```
	$cd ansible-django-stack
	$ansible-django-stack$ ansible-playbook -i staging deploy.yml
	```

+ Run on production:
	```
	$cd ansible-django-stack
	$ansible-django-stack$ ansible-playbook -i production deploy_production.yml
	```

Notes
=====
+ Change server ip in inventory file
+ All variables contain in group_vars dir


Useful Links
============
+ [Ansible Django Stack](https://github.com/jcalazan/ansible-django-stack/)
+ [Ansible - Best Practices](http://docs.ansible.com/playbooks_best_practices.html)
+ [Setting up Django with Nginx, Gunicorn, virtualenv, supervisor and PostgreSQL](http://michal.karzynski.pl/blog/2013/06/09/django-nginx-gunicorn-virtualenv-supervisor/)
+ https://www.stavros.io/posts/example-provisioning-and-deployment-ansible/


