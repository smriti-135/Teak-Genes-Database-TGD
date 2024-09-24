Many useful Tripal modules have been developed by Mainlab Bioinformatics. To use these, the mainlab tripal and mainlab chado loader modules were first installed as detailed in their repository (https://gitlab.com/mainlabwsu/mainlab_tripal, https://github.com/tripal/mainlab_chado_loader).

For the search functionality, manilab chado search was used as detailed in its repository (https://gitlab.com/mainlabwsu/chado_search). This creates an interface with a webform for the user. This connects with the chado dataase to query the content required by the user and display it back as a web page.

The module was first downloaded and enabled.

```
cd /var/www/html/teak-genes-database/sites/all/modules
sudo git clone https://gitlab.com/mainlabwsu/chado_search
cd /var/www/html/teak-genesdatabase/sites/all/modules/chado_search/file
sudo cp default.settings.txt settings.conf
d7drush csreload
d7drush pm-enable chado_search
```

To make it available for viewing and searching, necessary fields (with prefix chado_search_) were populated via *`Home -> Administration -> Tripal -> Data Storage -> Chado Schema -> Materialized Views`*. Now different types of search could be made such as gene search, feature search etc. To access them in a single place, a new ‘Search page’ page was created with links to the search function.
```
<button><a href="http://teak-genes-database/find/features/" class="btn">Sequence Search</a></button><br>
<button><a href="http://teak-genes-database/data_search/mrna" class="btn">mRNA Search</a></button><br>
<button><a href="http://teak-genes-database/search/node" class="btn">Content Search</a></button>
```
