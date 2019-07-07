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
