### KetPath
This repository provides the process of the construction of the Ketamine Pathway (KetPath) knowledge graphs wlong with all the datasets and query protocols used in the work. KetPath is a biomedical pathway knowledge graph designed for exploring the pathway relations of the antidepressant ketamine, and ketamine's effects on brain neurotransmitters and gut microbiota. This project is done by IBIVU and L&R group, Verije Universteit Amsterdam. 

### Authors
Ting Liu (t.liu@vu.nl), K. Anton Feenstra (k.a.feenstra@vu.nl), Zhisheng Huang (z.huang@vu.nl) and Jaap Heringa (j.heringa@vu.nl)

### Datasets

The weights of the dataset used to construct the KetPath knowledge graph are as follows:
    KetFact (28 KB) - created by manual fact curation
    KetCept (14 MB) - generated by the XMedlan tool
    KetRela (0.9 MB) - derived by the BioKetBERT model
    MiKG (0.1 MB) - created by manual fact curation, results in the MiKG paper
    PPKG (0.3 MB) - created by combining manual fact curation and the XMedlan tool, results in the PPKG paper
    WikiPathway (18 MB) - only includes biological pathways of homo sapiens
    Gene Ontology (7 MB) - contains gene and gene product attributes of homo sapiens
    KEGG Pathways (0.7 MB) - includes data profiles of pathways related to neurotransmitters
    DrugBank (180 MB) - includes basic information on drug targets, pharmacology and metabolism
    UMLS (31 MB) - consists of named biomedical vocabularies and defined relationships between terms
    SNOMED CT (48 MB) - consists of named biomedical vocabularies and defined relationships between terms
    BioBERT-Base v1.1 (+ PubMed 1M) - based on BERT-base-Cased, see the BioBERT page

### Workflow

## 1. Retrieving articles: 

Retrieve PubMed IDs (PMIDs) for relevant articles by using the following query: https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&term="Ketamine+Depression"&RetMax=10000. Save the retrieved list of PIMDs locally in text format under the pmid2html-->data-->pmidlist file directory.

2. Downloading articles: 

Right-click and edit the 'run-PubmedDownload.bat' file located in the 'pmid2html' directory. Updated the name of the PMID list file as needed, save changes, and then double-click the 'run-PubmedDownload.bat' file to initiate the download of articles in HTML format.

3. Manual fact curation from pathway images

(1) Manually collect hand-drawn images and free-text descriptions of the ketamine pathway from relevant publications. (2) Manually extract entities and relations of interest from those images and texts. (3) Define entities and their relations using KetFact as a domain name. (4) Map entities to the KEGG and UMLS databases by matching their URIs with the owl:sameAs statement. The generated dataset is stored in the 'KetFact.ttl' file.

4. Named entity recognition and semantic annotation with XMedlan

Use XMedlan, a Xerox natural language processing (NLP) tool, for named entity recognition and semantic annotation of biomedical text with terminologies UMLS and SNOMED CT. The dataset generated by XMedlan is stored in the 'KetCept.zip' file.

5. Knowledge graph construction in the GraphDB

5.1 Downloading and starting the GraphDB

Download GraphDB free edition from https://www.ontotext.com/products/graphdb/graphdb-free/. GraphDB is a Java application and requires Java 8. Make sure you have an up-to-date Java 8 installation. Please download Java from https://java.com/en/download/help/download_options.xml. Run the GraphDB script in the bin directory. To access the Workbench, open http://localhost:7200 in a browser. Please get more information on GraphDB for a quick start guide.

5.2 Creating repositories in GraphDB

By default, the GraphDB will initialize a location but not create any repositories. Create a new repository from the menu `Setup` -> `Repositories` page in the GraphDB Workbench. To create a new repository in the location, click `Create new repository`. Fill in KetPath at the `Repository ID*`, then click `creat`.

5.3 Importing databases in GraphDB

Import all databases from the menu `Import` -> `RDF page` -> `User data`. Click on `Upload RDF files` and select files to upload. Click on `Import`, and fill the Target graphs with a URL as Named graphs. If the database is too large to upload from the User data page, you can store the database in the local `graphdb-import` file and then import the database from the menu `Import` -> `RDF page` -> `Server files`.

5.4 Accessing and reasoning data in GraphDB

The data in GraphDB can be accessed and reasoned by SPARQL query language. Start query from the menu `SPARQL`. Please find query templates in the 'sparql-codes.txt' file. Use the SPARQL query endpoint of UniProt to retrieve its data without downloading the data stack.

6. Relation extraction with BioKetBERT

6.1 Preparing training and testing datasets for relation extraction

Run the query protocol for case 1 from the 'sparql-codes.txt' file in GraphDB to retrieve sentences where 'ketamine' and 'neurotransmitter' co-occurrence. The target-named entities need to be tagged with the pre-defined tags such as @entity$ for further relation extraction tasks. For the training set, a label needs to be added indicating whether the two entities in a sentence are related: 1 for a relation, 0 otherwise. 

6.2 Fine-tuning the BioBERT model and performing relation extraction

Fine-tune the BioBERT model and dubber the resulting model BioKetBERT. Perform relation extraction tasks withBioKetBERT according the process provided by Lee et al. at https://github.com/dmis-lab/biobert. More details can be find in their paper BioBERT: a pre-trained biomedical language representation model for biomedical text mining for more details. 

The performance of the relation extraction task needs to be evaluated using five-fold cross-validation, where the dataset containing 2,143 sentences is randomly partitioned into five stratified subsets of equal size: for each round, one data block (428 sentences) is used for training and the remaining (1,715 sentences) four are for testing.

The relational dataset generated by the BioKetBERT model is stored in the 'KetRela.ttl' file, which also need to be added to the KetPath repository in GraphDB.

More information

Please contact Ting Liu (t.liu@vu.nl; tingliu0909@gmail.com) if you have any questions about the constructing process, datasets and query protocols.

## SPARQL
SPARQL protocols are presented in [sparql-codes](https://github.com/tingcosmos/KetPath/blob/main/sparql-codes) and the query results are available at [NEED FURTHER UPDATED](). Users can perform their own queries by changing the parameters in the templates that we designed.

## Downloading databases
All databases are available at [KetPath Release Page](https://github.com/tingcosmos/KetPath/releases/).

## Downloading GraphDB
Download GraphDB free edition from https://www.ontotext.com/products/graphdb/graphdb-free/.
GraphDB is a Java application and requires Java 8. Make sure you have an up-to-date Java 8 installation.
Please download Java from https://java.com/en/download/help/download_options.xml.

## Starting GraphDB
Run the GraphDB script in the bin directory. To access the Workbench, open http://localhost:7200 in a browser.

## Creating repositories in GraphDB
By default, the GraphDB will initialise a location but not create any repositories.
You can create a new repository from the menu `Setup` -> `Repositories` page in the GraphDB Workbench.
To create a new repository in the location, click `Create new repository`.
Fill in KetPath at the `Repository ID*`, then click `creat`.

## Importing databases in GraphDB
You can import databases from the menu `Import` -> `RDF page` -> `User data`.
Click on `Upload RDF files` and select files to upload.
Click on `Import`, and fill the Target graphs with a URL as Named graphs.
If the database is too large to upload from the User data page, you can store the database in the local `graphdb-import` file and then import the database from the menu `Import` -> `RDF page` -> `Server files`.

## Accessing and reasoning data in GraphDB
The data in GraphDB can be accessed and reasoned by SPARQL query language.
Start query from the menu `SPARQL`.
Please find query templates in [sparql-codes](https://github.com/tingcosmos/KetPath/blob/main/sparql-codes).

## More information
Please contact Ting Liu (t.liu@vu.nl) if you have any questions about the databases and query cases.
Please get more information on GraphDB for a [quick start guide](http://graphdb.ontotext.com/documentation/free/quick-start-guide.html).

## Citation
`@article{liu2020ketpath,
    author = {Liu, Ting and Feenstra, K Anton and Huang, Zhisheng and Heringa, Jaap},
    title = "{Mining literature, microbiome and pathway data to explore the relations of ketamine with neurotransmitters and gut microbiota using a knowledge-graph}",
    journal = {},
    year = {2023},
    volume = {},
    number = {},
    pages = {},
    publisher = {},
    doi = {},
}`
