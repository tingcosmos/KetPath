## KetPath
This repository provides the code for the KetPath (Ketamine Pathway Knowledge Graph), a biomedical pathway knowledge graph designed for exploring the pathways of the antidepressant Ketamine, and Ketamine's effects on brain mneurotransmitters and gut microbiota. This project is done by [IBIVU](https://www.vubioinformatics.com/) and [L&R](https://lr.cs.vu.nl/) group, Verije Universteit Amsterdam. Please refer to our paper "A biomedical literature derived ketamine pathway knowledge graph" for more detail which published on xxx.

## Authors
Ting Liu (t.liu@vu.nl), K. Anton Feenstra (k.a.feenstra@vu.nl), Zhisheng Huang (z.huang@vu.nl) and Jaap Heringa (j.heringa@vu.nl)

## SPARQL
We provide four SPARQL query cases with the code and their results. Users can perform their own queries by changing parameters in templates that we designed.

## Downloading databases
SPARQL protocols are presented in sparql-codes.txt
All databases are available at [KetPath Release Page](https://github.com/tingcosmos/KetPath/releases/).

## Downloading GraphDB
Download GraphDB free edition from https://www.ontotext.com/products/graphdb/graphdb-free/.
GraphDB is a Java application and requires Java 8. Make sure you have an up-to-date Java 8 installation.
You can download Java from https://java.com/en/download/help/download_options.xml.

## Starting GraphDB
Run the graphdb script in the bin directory. To access the Workbench, open http://localhost:7200 in a browser.

## Creating repositories
By default, the GraphDB will initialise a location but not create any repositories.
You can create a new repository from the menu Setup -> Repositories page in the GraphDB Workbench.
To create a new repository in the location, click on "Create new repository".
Fill in KetPath at the Repository ID*, and then click on "creat".

## Importing databases
You can import databases from the menu Import -> RDF page -> User data.
Click on "Upload RDF files" and select files to upload.
Click on "Import", and fill the Target graphs with an URL as Named graphs.
If the database is too large to upload from the User data page, you can store the datababase in the local 'graphdb-import' file and then import the datababase from the menu Import -> RDF page -> Server files.

## Accessing and reasoning data
The data in GraphDB can be accessed and reasoned by SPARQL query language.
You can start your query from the menu SPARQL.
You can find several query templates in [sparql-codes](https://github.com/tingcosmos/KetPath/blob/main/sparql-codes).

## More information
Please contact Ting Liu (t.liu@vu.nl) if you have any questions about the databases and query cases.
Here also a GraphDB quick start guide: http://graphdb.ontotext.com/documentation/free/quick-start-guide.html for more information.

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
