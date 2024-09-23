## Database Configuration ##
The default psql user was set to “postgres” with all permissions upon installation.

`sudo -u postgres psql`

An additional super user “postgres_admin_molecular” was created to manage the database linked to the
website.

*Note: ********** contains original password*
```
CREATE USER postgres_admin_molecular WITH PASSWORD ‘**********’
SUPERUSER;
ALTER USER postgres_admin_molecular CREATEDB;
CREATE DATABASE teak_genes_database_db;
ALTER DATABASE teak_wood_genes_drupal7_db OWNER TO
postgres_admin_molecular;
```
