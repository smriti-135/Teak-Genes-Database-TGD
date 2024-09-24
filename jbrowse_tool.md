The main steps for installation and configuration are detailed in Tripal Jbrowse User Guide (https://tripaljbrowse.readthedocs.io/en/latest/).

Firstly, the dependencies for Jbrowse were installed.
```
sudo apt-get install libgd-dev zlib1g-dev libpng-dev
find /usr/lib -name “libgd.so*” # For GD
find /usr/lib -name “libz.so*” # For Zlib
find /usr/lib -name “libpng.so*” # For libpng
```

Next, the standalone version of Jbrowse was installed in the tools directory and given permissions.
```
sudo curl -L -O https://github.com/GMOD/jbrowse/releases/download/1.16.11-release/Jbrowse-1.16.11.zip
unzip Jbrowse-1.16.11.zip
cd /var/www/html/tools
sudo cp /home/molecular/Downloads/Jbrowse-1.16.11 .
sudo chown `whoami` Jbrowse-1.16.11
cd Jbrowse-1.16.11
sudo ./setup.sh
sudo mkdir data
sudo chown -R www-data:www-data /var/www/html/tools/Jbrowse-1.16.11
sudo chmod -R 755 /var/www/html/tools/Jbrowse-1.16.11/data
```

Optionally, symbolic links (symlinks) from the web root to the tools directory was created so that the tool can be accessed from outside web root.
```
cd /var/www/html/teak-genes-database
sudo mkdir tools
sudo ln -s /var/www/html/tools/Jbrowse-1.16.11 /var/www/html/teakgenes-database/tools/Jbrowse-1.16.11
```

The Tripal Jbrowse management module was downloaded and installed. Its setting were configured via *`Administration -> Tripal -> Extensions -> Tripal Jbrowse Management -> Settings`*.

Following this, a directory for the JBrowse files was created where the name of the link matches the organism it is for: genus_species__common_name. Here it was named as ‘tectona_grandis__teak’.
```
cd /var/www/html/tools/JBrowse-1.16.11/data
sudo mkdir tectona_grandis__teak
cd tectona_grandis__teak
sudo mkdir data
sudo chown -R www-data:www-data /var/www/html/tools/JBrowse1.16.11/data
sudo chmod -R 755 /var/www/html/tools/JBrowse-1.16.11/data
```
The reference sequence to be added as reference track was manually prepared. This was done using `preparerefseqs.pl`. After loading feature data, to let users find features by typing feature names or IDs in the autocompleting search box, a special index of feature names was generated using `generate-names.pl`. All of these are present in JBrowse’s bin.
```
cd /var/www/html/teak-genes-database/tools/JBrowse1.16.11/data/tectona_grandis__teak
sudo /var/www/html/tools/JBrowse-1.16.11/bin/prepare-refseqs.pl --fasta /var/www/html/teak-genesdatabase/sites/default/files/teak_tectona_grandis_26Jun2018_7GlFM_fmt_tp.fa
sudo /var/www/html/tools JBrowse-1.16.11/bin/generate-names.pl -v
```
Finally, this was set up for display as an instance of JBrowse via *`Home -> Administration -> Tripal -> Extensions -> Tripal JBrowse Management -> Create new instance`*.
