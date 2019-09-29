
# vagrant-ansible-postgresql

Example of PostgreSQL replication with two servers: master and standby


## Prerequisites:

Download and install the following tools:

- [VirtualBox & Extension Pack](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant](https://www.vagrantup.com/downloads.html)
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) 2.8+

## Running the code

- Status:
  ```bash
  -:$ vagrant status
  ```
- Instantiate servers:
   ```bash
   -:$ vagrant up postgresql01 postgresql02
   ```
- Connect to the master server
   ```bash
   -:$ vagrant ssh postgresql01 -- -t "sudo -i -u postgres psql"
   postgres=# \l                         # DATABASES LISTED           (1)
   postgres=# create database test;      # 'test' DATABASE CREATED    (4)
   postgres=# \l                         # DATABASES LISTED           (6)
   postgres=# drop database test;        # 'test' DATABASE DROPPED    (7)
   postgres=# \l                         # DATABASES LISTED           (9)
   ```
- Connect to the standby server
   ```bash
   -:$ vagrant ssh postgresql02 -- -t "sudo -i -u postgres psql"
   postgres=# \l                         # DATABASES LISTED           (2)
   postgres=# create database test;      # ERROR: READONLY TRANSACION (3)
   postgres=# \l                         # DATABASES LISTED           (5)
   postgres=# \l                         # DATABASES LISTED           (8)
   ```

