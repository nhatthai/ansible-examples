#Ansible Django

Ansible Playbook designed for environments running a Django app. It can install and configure these applications that are commonly used in production Django deployments:

+ Nginx
+ Gunicorn
+ Supervisor
+ Virtualenv
+ MySQL
+ Django

Default settings are stored in roles/role_name/vars/main.yml. Environment-specific settings are in the vars directory.

Tested with OS: Ubuntu 14.04 LTS x64


#Getting Started
===============
A quick way to get started is with Vagrant and VirtualBox.

Requirements:
============
+ [Ansible](http://docs.ansible.com/ansible/intro_installation.html)
+ [Vagrant](https://www.vagrantup.com/downloads.html)
+ [VirtualBox](https://www.virtualbox.org/wiki/Downloads)


Note that the default values in the playbooks assume that your project structure looks something like this:
```
myapp
├── myapp
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── manage.py
└── requirements
     |-- base.txt
     |-- development.txt
```

Run the playbook:
=================
Please make sure that you added id_rsa.pub into vagrant machine
```
$cd ansible-django-stack
ansible-django-stack$ ansible-playbook -i hosts deploy.yml
```

Notes:
======

+ fatal: [22.22.22.22]: FAILED! => {"changed": false, "cmd": "./manage.py syncdb --noinput --settings=myapp.settings --pythonpath=/home/vagrant/sources/myapp/venv/bin/python", "failed": true, "msg": "[Errno 13] Permission denied", "rc": 13}

	- Fixed:
	```
	sudo chmod u+x manage.py
	```

+ fatal: [22.22.22.22]: FAILED! => {"changed": false, "cmd": "/usr/bin/supervisorctl update", "failed": true, "msg": "", "rc": 2, "stderr": "", "stdout": "error: <class 'socket.error'>, [Errno 2] No such file or directory: file: /usr/lib/python2.7/socket.py line: 224\n", "stdout_lines": ["error: <class 'socket.error'>, [Errno 2] No such file or directory: file: /usr/lib/python2.7/socket.py line: 224"]}
+ error: <class 'socket.error'>, [Errno 2] No such file or directory: file: /usr/lib/python2.7/socket.py line: 224

	- Fixed:
	```
		sudo touch /var/run/supervisor.sock
		sudo chmod 777 /var/run/supervisor.sock
		sudo service supervisor restart
	```

+ If a django isn't running.
	- Please stop supervisor
		```
		sudo supervisorctl stop myapp
		```
	- Start Django App
		```
		venv/bin/python ./manage.py runserver 0.0.0.0:8000 --settings=myapp.settings
		```
	- Start supervisor:
		```
		sudo supervisorctl start myapp
		```


Useful Links
============
+ [Ansible Django Stack](https://github.com/jcalazan/ansible-django-stack/)
+ http://technivore.org/posts/2015/10/09/easy-django-deployments-with-ansible.html
+ https://www.stavros.io/posts/example-provisioning-and-deployment-ansible/
+ https://danielgroves.net/notebook/2014/05/development-environments/
+ http://michal.karzynski.pl/blog/2013/06/09/django-nginx-gunicorn-virtualenv-supervisor/
