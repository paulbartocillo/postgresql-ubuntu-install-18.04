# How To Install and Use PostgreSQL on Ubuntu 18.04

## Prerequisites

### Install PostgreSQL

`$ sudo apt update`

`$ sudo apt install postgresql postgresql-contrib`

### PostgreSQL Roles and Databases

Postgres use ident authentication that uses System Unix/Linux account as a PostgreSQL Roles.
Postgres uses a concept called "roles" to handle in authentication and authorization to each databases.
By default, Postgres create a "postgres" role and at the same time a Unix/Linux "postgres" system account 
during installation for you to interact with the default postgres database.

Switching over a system account "postgres" to access postgres:

`$ sudo -i -u postgres`

`$ psql`

Accessing postgres w/o switching account

`$ sudo -u postgres psql`

### Creating a New Postgres Role

Switching over a system account "postgres" and create new postgres role

`$ sudo -i -u postgres`

`$ createuser --interactive`

Creating new postgres role w/o switching account

`$ sudo -u postgres createuser --interactive`
```
Output
Enter name of role to add: stark
Shall the new role be a superuser? (y/n) y
```

To create a Unix/Linux system account for the "stark" role you created previously for postgres

`$ sudo adduser stark`

You can then use stark to access postgres given you have a stark database

```
$ sudo -i -u stark
$ psql

or

$ sudo -u stark psql
```
### Creating a New Database

Create Database using stark role and without switching a system user account

`$ sudo -u stark createdb stark_db`

Accessing database with stark role given you created a stark_db using stark role

`$ sudo -u stark psql -d stark_db`

## Caveats: How to enable remote connection on postgres database

Login as postgres user

`$ sudo -i -u postgres`

Edit the file pg_hba.conf:

`$ sudo vim /var/lib/postgresql/9.5/main/pg_hba.conf`

or

`$ sudo vim /etc/postgresql/9.5/main/pg_hba.conf`

Append the following configuration lines to give access to 10.10.29.0/24 (YOUR OWN IP) network:

`host all all 10.10.29.0/24 trust`

### You need to enable TCP / IP networking for postgres

Edit the file postgresql.conf:

`$ sudo vim /var/lib/postgresql/9.5/main/postgresql.conf`

or

`$ sudo vim /etc/postgresql/9.5/main/postgresql.conf`

Find configuration line that read as follows:

`listen_addresses='localhost'`

Change the value to "*" or "SPECIFIC-IP"

`listen_addresses='*'` or `listen_addresses='10.10.29.0 10.20.0.0'`

### Restart PostgreSQL

`$ sudo service postgresql restart`

or 

`$ sudo su`

`$ /etc/init.d/postgresql restart`

# How To Install and Use PostgreSQL on Amazon Linux 2

`sudo yum update -y`

`sudo amazon-linux-extras install postgresql11`

`yum clean metadata`

`yum install postgresql`

`psql --version`


## Extras:

### How to connect remotely on rds postgres server

`psql -h companyx.ap-southeast-1.rds.amazonaws.com -U companyx -d companyx`

### How to get the size of db
`SELECT pg_size_pretty( pg_database_size('dbname'));`

### Troubleshoot
https://installvirtual.com/install-postgresql-11-on-amazon-linux-compile/

### Resources
https://www.compose.com/articles/postgresql-tips-installing-the-postgresql-client/
