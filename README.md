# Setup Metathesaurus  
This package runs UMLS's Metamorphosys from the R console as well as loads select UMLS Metathesaurus tables in a MySQL database:  
* MRCONSO.RRF
* MRHIER.RRF
* MRMAP.RRF
* MRSMAP.RRF
* MRSAT.RRF
* MRREL.RRF  

## Related Packages  
The metaorite R Package contains functions that query the tables in your MySQL instance.  

## MySQL v5.5 Requirement  
* MySQL version 5.5 server can be installed via MacPorts (Prerequisites are most current XCode and XCode Command Line tools). More information can be found here: https://trac.macports.org/wiki/howto/MySQL.  
* /opt/local/etc/mysql55/my.cnf is a good place to customize your mysql55 installation  
* Socket: /opt/local/var/run/mysql55/mysqld.sock  
* Example of creating a database named `umls` using `root` as user:  

         ```
         -mysql -u root -p  
         -mysql> CREATE DATABASE umls;  
         -mysql -u root -p --local-infile umls  
         -mysql> SHOW PROCESSLIST
         
         ```  
         
## Downloading UMLS Files   
* Files can be downloaded at https://www.nlm.nih.gov/research/umls/licensedcontent/umlsknowledgesources.html and requires an account.    
* Full Release is required to run Metamorphosys, at which point the user can select various specialized configurations desired in the MySQL Tables, such as a specific set of source vocabularies. The total time estimations of downloading, configuring, and processing the Metathesaurus tables in this way is approximately 2-3 hours. To save time, the Metamorphosys step may be skipped if the user does not desire this type of customizability and the `UMLS Metathesaurus Files` can be downloaded directly at the link and used as the source files in lieu of a Metamorphosys output.  

# Procedure  
## Setup and Run Metamorphosys  
* Unpack the Full Release download   
* Unzip mmys.zip in the unpacked download and move unzipped contents into a root folder  
* Run `openMetamorphysis()` with path to `run_mac.sh` as the argument  
* If not yet installed, install UMLS Metamorphosys (current configurations are all English vocabularies available). Time estimations for installation are approximately 45 minutes-1 hour, but this depends on the configurations.  

## Load Metathesaurus Tables  
* The RRF files can either be sourced from the outputs generated by running Metamorphosys, at which point a META/ folder will be generated containing all the source RRF files according to user configurations or they can be directly sourced from a `UMLS Metathesaurus Files` download.  
* The SQL used to load the RRF files was forked from the load_source_tables.sql found at https://github.com/patelm9/Vocabulary-v5.0/tree/master/UMLS and `LOAD DATA INTO` statements were added to populate the tables.  
