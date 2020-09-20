### MySQL Master-Slave Cluster

Installation Document:-
https://dev.mysql.com/doc/refman/8.0/en/linux-installation-yum-repo.html

Replication Document:
https://dev.mysql.com/doc/refman/8.0/en/replication-setup-slaves.html

Resetting root password Document:-
https://dev.mysql.com/doc/refman/8.0/en/resetting-permissions.html  

NOTE: Reset root password in MySQL need a bash shell script to process it as there is no ansible module to do so.

This ansible playbook has been tested and can be clone from my "linh5847" GitHub account. https://github.com/linh5847/ 

PreRequisites:-

Need a Linux or Mac machine/Laptop

Install VirtualBox

Install Vagrant

Install python

Install Ansible

or

vi requirements.txt

cryptography
PyYAML
tabulate
colorama
launchpadlib
molecule
ansible
ansible-lint
flake8
flake8-docstrings
yamllint
testinfra
jmespath

/usr/bin/python3 -m pip install -r requirements.txt

Method:-

git clone https://github.com/linh5847/mysql.git

or

git clone git@github.com:linh5847/mysql.git

cd mysql

vagrant status

vagrant up