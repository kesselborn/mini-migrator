Mini Migrator
=============

What is it
----------

This is a collection of a few bash scripts to mimic Rails-like migrations for
your not-Rails project.

What is it not
--------------

You will have to write pure mysql code -- no Rails-like ORM syntax

Installation & usage
--------------------

### Installation: 

Clone this repo:

    git clone git://github.com/kesselborn/mini-migrator.git

create a directory (i.e. `migrations`) in your project where you want to use
`mini-migrator` and copy the files from this repository to this directory.

### Setup database / creating config files

In order to setup your database you should create a dedicated user and several
databases (one for production, one for development and one for testing). For
this use the `setup` script:

    setup -U <admin_user> [-P <admin_password>] -u <user> -p <password> -d <database_name>

this will create the mysql user `<user>` with password `<password>` and the
three databases

    <database_name>
    <database_name>_development
    <database_name>_test

### Create a migration

Now you are ready to create your first migration: Call

    ./create_migration <migration_name>

and fill in the mysql code into the file that opens. Read the comments at the 
bottom of the file for some examples.

### Execute migration

In order to apply your migrations, call

    ./migrate

if you want to migrate to a specific migration, call

    ./migrate <num>

where `<num>` is the number of the migration you want to migrate to.

By default, the `<database_name>_development` database is used. Call

    ENV=production ./migrate

or 

    ENV=test ./migrate

to migrate your `production` or `test` database respectivly.

### Teardown

If you want to delete the databases and the users that were created with the 
`setup` command call 

    ./teardown
