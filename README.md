# Master-Project-Thesis An approach to link the datasets metadata of ODISSEI to Microsoft Publication citations

The below are the methods followed for linking the dataset metadata to the Microsoft Publication
1) Step1: Data Extraction:
* The datasets metadata (title, and DOI) is the first source that needs to be extract for the linking there are three ways to extract the Metadata
  * If there is an adminstrator access to Dataverse, this can be done using CURL command as recommanded in Dataverse user guide
  * If there are RDF files available from the dataset repository, this can be extracted using RDFLIB using python
  * If the metadata to be extract directly from the site, web scraper tool called "PARSE HUB" can be used
 * The publication data from Microsoft Academic scholar needs to be extracted, there are two files available in a datasets produced by "Microsoft Academic Scholar"
    * Paper.txt : This has PaperID, DOI, Title, +19 attributes
    * Paperreferences.txt : This has Paper ID and Paper reference ID
    
2) Step 2: Preprocessing of Input files
* The datasets metadata input file for the linking should have the following format for the linking:
  * Datasets metadata: This should be in a separate file, DOI should be present separately in a .txt fle and same with Title
  * This can be easily copy pasted in a separate .txt file.
 * The publication data input file for the linking should have the following format for the linking:
    * Publication DOI file : This should have Paper ID, Paper Reference ID, and DOI
    * Publication Title file : This should have Paper ID, Paper Reference ID, and Title
    * Publication DOI file : In order to get the appropriate fields for the input file, we need to join both extracted files Papers.txt and Paper References.txt and there are three ways to do it
    * SQL : 1) The data needs to be loaded in two different table by indexing 2) SQL Left Join query should be executed to join these two files to get the output. If there is adequate internal memory the output files can be easily retrived.
    * Power Query : 1) The two files can be loaded in power query (in Excel or Power BI) 2) Relationship between these two can be established wth PaperID field of Papers.txt and PaperreferenceID field of Paperreeference.txt 3) New dataset will be populated 4) This method will be successful if the output rows is less than 1 million rows.
    * AWK : Using Git bash by using AWK command the large files can be linked and desired input files can be retrived
    
3) Step 3: Linking Process
* The linking process is performed using KeywordProcessor of FlashText library. There are two output files retrived through the linking
  * Citation count for the matched dataset title and DOI
  * Details of the matched records: Input dataset title/DOI, MAG Paper reference ID, MAG Paper ID
  * Using Paper ID, AWK command can be run to get the Paper Title. This is useful while performing the evaluation and to define precision and recall of the output result
