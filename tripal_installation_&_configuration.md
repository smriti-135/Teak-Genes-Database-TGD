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
