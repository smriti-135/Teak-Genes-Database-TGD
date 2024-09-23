## Drupal ##
```
cd /var/www/html/teak-genes-database
sudo wget https://ftp.drupal.org/files/projects/drupal-7.100.tar.gz
sudo tar -zxvf drupal-7.100.tar.gz
sudo mv drupal-7.100/* ./
sudo mv drupal-7.100/.htaccess ./
sudo mkdir -p /var/www/html/teak-genes-database/sites/default
sudo chgrp www-data /var/www/html/teak-genes-database/sites/default
cd /var/www/html/teak-genes-database/sites/default/
sudo cp default.settings.php settings.php
sudo gedit settings.php
```

The settings.php file stores essential configuration details such as database connection information, site name,
and URL.

*Note: ********** contains original password*
```
$databases['default']['default'] = array(
 'driver' => 'pgsql',
 'database' => 'teak_genes_database_db',
 'username' => 'postgres_admin_molecular',
 'password' => '**********',
 'host' => 'localhost',
 'prefix' => '',
);
```
Finally, the site alias or url of the website was added to the end of the sites.php file at *‘/var/www/html/teak-genes-database/sites’*.
`$sites['teak-genes-database'] = 'teak-genes-database';`
