## Tripal ##
```
cd /var/www/html/teak-genes-database/sites/all/modules/
sudo drush pm-download entity views ctools ds field_group field_group_table field_formatter_class field_formatter_settings jquery_update
d7drush pm-enable -y entity views ctools ds field_group field_group_table field_formatter_class field_formatter_settings jquery_update
cd /var/www/html/teak-genes-database/
d7drush pm-download tripal
```

The patches for a couple of bugs, provided by the developers, were also applied
```
sudo wget --no-check-certificate https://drupal.org/files/drupal.pgsql-bytea.27.patch
sudo patch -p1 < drupal.pgsql-bytea.27.patch
sudo patch -p1 < ../tripal/tripal_chado_views/views-sql-compliantthree-tier-naming-1971160-30.patch
d7drush pm-enable -y tripal tripal_chado tripal_ds tripal_ws
```
### Chado
Chado is a relational database schema for storing molecular biological and ancillary data. It is used by Tripal and integrates with Drupal's default PostgreSQL. 
It was installed via `Home -> Administration -> Tripal -> Data Storage -> Chado -> Install Chado`. 
Following this, it was prepared via `Home -> Administration -> Tripal -> Data Storage -> Chado -> Prepare this site`.

In Drupal, these settings do not take effect immediately. Instead, they are saved as ‘Jobs’ for the background processes to finish. This way, the website does not take up unnecessary resources continuously. But this also leads to the jobs staying in queue until the Tripal jobs system wakes and runs. 
This limitation was overcome by manually starting the jobs at the CLI.
```
drush trp-run-jobs --username=admin_molecular --root=/var/www/html/teak-genes-database
```

### Daemon and Cron
Jobs can be run manually as described above or automated using tripal_daemon. Drupal cron is used to automatically execute necessary Drupal housekeeping tasks.
```
cd /var/www/html/teak-genes-database/sites/all/libraries
sudo wget https://github.com/shaneharter/PHPDaemon/archive/v2.0.tar.gz
sudo tar -zxvf v2.0.tar.gz
sudo mv PHP-Daemon-2.0 PHP-Daemon
sudo drush en libraries -y
sudo drush pm-download drushd
sudo drush pm-enable -y drushd
sudo drush pm-enable -y tripal_daemon
```
