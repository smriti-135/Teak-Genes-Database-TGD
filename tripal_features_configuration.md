Before integrating the tools, some features and pages related to Tripal need to be setup.

### Organism Page
Organism (*Tectona grandis*) details were added at *`Content > Tripal content > Add > Organism`*. Additional fields for other organism details other than provided by default were added at *`Tripal > Data Loaders > Chado NCBI Taxonomy Loader`*.

### Analysis
Tripal’s Chado loader for importing genomic data requires that an analysis be associated with all imported features. This is useful because it contains the details of how the features were created, source of features (sequences) can be traced and all of the features can be associated together. The analysis details were input via *`Home -> Add Tripal Content -> Analysis`*.

### Gene Ontology (Controlled Vocabularies)
Gene Ontology (GO) provides a standardized, controlled vocabulary for describing gene products in terms of their location, role and molecular function. Some commonly used GO include gene, mRNA etc. Since the website and its use case mandated the upload of whole genome, genes and transcripts with annotations, selecting a GO was important for standardisation. This was done via *`Tripal → Data Loaders → Chado Vocabularies → OBO Vocabulary Loader → Ontology OBO File Reference → Gene Ontology`*.
