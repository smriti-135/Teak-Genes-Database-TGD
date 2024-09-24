A great tool for viewing and downloading Tripal data (biological data) is Mainlab’s Tripal Megasearch as detailed in its repository (https://gitlab.com/mainlabwsu/tripal_megasearch). Similar to the chado search tool, it a webform with the ability to choose the type of data (e.g., genes, markers, phenotypes) as well as additional filters. In the backend, it leverages two potential data sources:
- Materialized Views: Pre-computed summaries of the data, allowing for faster retrieval.
- Chado Base Tables: The underlying relational database tables storing the biological data on the Tripal website.

When available, Tripal MegaSearch prioritizes using materialized views to retrieve the data. This can then be simply viewed or downloaded as CSV, TSV or FASTA (for sequences) by the user. 

The module was first downloaded and enabled.
```
cd /var/www/html/teak-genes-database/sites/all/modules
sudo git clone https://gitlab.com/mainlabwsu/tripal_megasearch
d7drush pm-enable tripal_megasearch
```

The necessary fields (with prefix tripal_megasearch_) were populated at *`Home -> Administration -> Tripal -> Chado Schema -> Materialized Views`*. This generated the Download webform in the form of a ‘Download page’.
