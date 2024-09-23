*Note: Most of the installation steps was obtained from official documentations and guides. These include the Drupal user guide (https://www.drupal.org/docs/user_guide/en/index.html) and Tripal documentation (https://tripal.readthedocs.io/en/latest/user_guide.html).*

The hardware specifications of the system used as server to host the website were:
- OS - Ubuntu 22.04.4 LTS
- Memory - 32 GB
- Disc capacity - 514.5 GB

## LAMP stack ##
The LAMP stack (Linux, Apache, MySQL and PHP) is commonly installed for web development. However,
PostgreSQL was used here instead of MySQL since Drupal and Chado support PostgreSQL.

```
sudo apt update && sudo apt upgrade
sudo apt -y install python3
sudo apt-get -y install apache2
sudo apt-get -y install openssh-server
sudo apt-get -y install ufw
sudo ufw enable
sudo ufw allow 'OpenSSH'
sudo ufw allow 'Apache'
sudo apt-get -y install postgresql postgresql-contrib
sudo systemctl start postgresql.service
sudo apt-get -y install php8.1-fpm
sudo apt-get install -y php8.1-cli php8.1-common php8.1-mysql php8.1-zip php8.1-gd php8.1-mbstring php8.1-curl php8.1-xml php8.1-bcmath php8.1-pgsql
for module in /etc/php/8.1/mods-available/*.ini; do sudo phpenmod -v 8.1 $(basename $module .ini); done
```
## Web Root ##
The web root is the root directory of a website, which is the top-level directory of a file system on a server. This directory contains all other directories and files associated with the website, including HTML pages, images, CSS stylesheets, JavaScript files etc.
```
cd /var/www/html
sudo mkdir teak-genes-database
sudo chown -Rv www-data:www-data /var/www/html/teak-genes-database
sudo chmod -Rv 755 /var/www/html/teak-genes-database
```

It is important to note the listen ports or listen directive, because it is used to configure Apache HTTPD to use it. When using a Unix socket, the web server must be on the same machine in order to communicate with phpfpm. Here, it was present in ‘/etc/php/8.1/fpm/pool.d/www.conf’. The socket was found as
‘listen = /run/php/php8.1-fpm.sock’. This was noted for use in the next step (virtual host configuration).
```
sudo systemctl restart php8.1-fpm
sudo a2enconf php8.1-fpm
sudo a2enmod proxy proxy_fcgi
sudo systemctl restart apache2
```

For each Drupal site, a virtual host configuration file had to be created to configure the virtual host to use the appropriate PHP-FPM pool. Here it was configured in ‘/etc/apache2/sites-available/teak-genes-database.conf’
```
<VirtualHost *:80>
 ServerName teak-genes-database
 DocumentRoot /var/www/html/teak-genes-database
 <Directory /var/www/html/teak-genes-database>
 Options Indexes FollowSymLinks
 AllowOverride All
 Require all granted
 </Directory>
40
 <FilesMatch \.php$>
 SetHandler "proxy:unix:/run/php/php8.1-
fpm.sock|fcgi://localhost"
 </FilesMatch>
</VirtualHost>
```
Next, “/etc/hosts” file was edited to map the domain name to the localhost IP
`127.0.0.1 teak-genes-database`. 
The web server was now configured to use PHP 8.1. However, a dependency of Drupal called Drush requires a lower version of 7.4. Therefore that was installed as well.
```
sudo apt-get -y install php7.4
sudo apt-get install -y php7.4-cli php7.4-common php7.4-mysql php7.4-zip php7.4-gd php7.4-mbstring php7.4-curl php7.4-xml php7.4-bcmath php7.4-pgsql
for module in /etc/php/7.4/mods-available/*.ini; do sudo phpenmod -v 7.4 $(basename $module .ini); done
```
This way the version of PHP used for web server and shell were both installed so that Drupal 7 rus PHP 8.1 while Drush commands on the shell use PHP 7.4. The steps to manage them are given further.

## Other software ##
Composer, Drush, phpPgAdmin/pgAdmin4

```
php -r "copy('https://getcomposer.org/installer', 'composersetup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'; } else {echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
sudo chmod +x composer.phar
sudo mv composer.phar /usr/local/bin/composer
composer require drush/drush:^8.4 –W
alias d7drush='sudo update-alternatives --set php /usr/bin/php8.1;
/var/www/html/teak-genes-database/vendor/bin/drush'
source ~/.bashrc
sudo curl https://www.pgadmin.org/static/packages_pgadmin_org.pub |
sudo apt-key add
sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
sudo apt-get -y install pgadmin4 pgadmin4-web pgadmin4-desktop
```
