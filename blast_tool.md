BLAST+ Standalone is a suite of programs designed for performing sequence similarity searches. It is an upgraded version of BLAST legacy version. The main steps for installation and configuration are detailed in Tripal BLAST User Guide (https://tripal-blast-ui.readthedocs.io/en/latest/user_guide.html).
The standalone version of BLAST was downloaded and installed in a new directory *‘tools’*. It was also added to the path.
```
cd /var/www/html
sudo mkdir tools
cd tools
sudo cp /home/molecular/Downloads/ncbi-blast-2.15.0+-x64-linux.tar.gz .
sudo tar zxvpf ncbi-blast-2.15.0+-x64-linux.tar.gz
export PATH=$PATH:/var/www/html/tools/ncbi-blast-2.15.0+/bin
source ~/.bashrc
echo $PATH
```

The Tripal Blast module was also installed and configured with the path of the BLAST bin:
```
d7drush pm-download tripal_analysis_blast
d7 drush pm-enable -y tripal_analysis_blast
```

With the program loaded, the file to be used as reference/target database was also formatted accordingly. Here, the chromosome-scale genome assembly FASTA was used as target by converting into a database format. This was done using NCBI+ BLAST tool `formatdb` or `makeblastdb`.
```
cd /var/www/html/teak-genes-database/sites/default/files
sudo mkdir blast_db
cd blast_db
sudo /var/www/html/tools/ncbi-blast-2.15.0+/bin/makeblastdb -in ../teak_tectona_grandis_26Jun2018_7GlFM_fmt_tp.fa -dbtype nucl -out teak_chromosomal_scale_genome_assembly_2018
sudo chown -R www-data:www-data /var/www/html/teak-genesdatabase/sites/default/files/blast_db
sudo chmod -R 755 /var/www/html/teak-genesdatabase/sites/default/files/blast_db
```
<br>
Finally, the details about the reference database were added at *`Home -> Administration -> Tripal -> Data Storage -> Chado -> Databases -> Add Database`*. The path included full path along with files name until the extension type i.e, *‘/var/www/html/teak-genesdatabase/sites/default/files/blast_db/teak_chromosomal_scale_genome_assembly_2018’*. This created a new BLAST page that contained the four basic types of BLAST with all the basic features.
