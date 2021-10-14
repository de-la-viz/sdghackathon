# SDG Hackathon 2021
## _The Swiss hackathon on Sustainable Development Goals visualisation_

## Overview
This Hackathon aims at creating visualisations that provide insights on the amount and quality of research in the direction of achieveng the Sustainable Development Goals established by the United Nations.

The data that is provided for this sutdy is the P3 database containing the projects that have been approved for funding by the Swiss National Science Foundation (SNSF) between 1980(?) and Aug-2021, downloaded from https://p3.snf.ch/Pages/DataAndDocumentation.aspx.

## Description of the datasets
### 1) SNSF_Projects.csv
The dataset contains the following columns:

_[Dan] I suggest removing from the dataset the columns whose description is N/A_

|Column #|Name|Type|Description|Type of entry|
| ------ | ------ | ------ | ------ | ------ |
|1| Project Number | numeric |Project identifier.||
|2| Project Number String | text |Full-text project identifier.||
|3| Project Title | text |Short description of the project.||
|4| Funding Instrument | text |Research funding scheme as defined by https://www.snf.ch/en/9o5ezhuSlHENVQxr/page/overview-of-funding-schemes||
|5| Funding Instrument Hierarchy | text |Top level hierarchy of the research funding scheme.||
|6| Institution | text |Institution where the project will largely be carried out.|Free text|
|7| Institution Country | text |The country of the institution. Most international locations are related to mobility fellowships.|List|
|8| University | text |Institution where the project will largely be carried out, based on a list to pick at the moment of the application.|List|
|9| Discipline Number | numeric |Discipline ID defined by the SNSF. Defined for the main discipline.|List|
|10| Discipline Name | text |Discipline name defined by the SNSF. Defined for the main discipline.|List|
|11| Discipline Name Hierarchy | text |The hierarchy of the main discipline.||
|12| All disciplines | text |List of all the discipline IDs involved in the project.||
|13| Start Date | text |Date at which the project starts (dd.mm.yyyy).|Free text|
|14| End Date | text |Actual date at which the project ends. Updated if necessary (dd.mm.yyyy).|Free text|
|15| Approved Amount | text |Approved funding amount. Updated if modified. Format is text because not always a number is stored. Ex: it may say "not included in P3".||
|16| Keywordstext | text |Keywords related to the project.|Free text|
|17| Abstracttext | text |The scientific abstract of the research project. May be edited by the applicants online. The researchers are responsible for the contents.|Free text|
|18| abstract_translated| text |Abstract translated to English for the abstracts that were translated.|Free text|
|19| abstract_translated_yes_no| text |Flag indicating whether the abstract has been translated to English.|Free text|
|20| abstract_english| text |Abstract in English, either the original one or the translated one.|Free text|
|21| sdg | text | SDG that has been detected, NA if no SDG has been detected in this document by the given system ||
|22| system | text | Query system used to detect SDG (see "How the SDGs were detected in the text" below) ||
|23| hits | numeric | How many hits were produced for a given SDG for the given document by the given system ||



### 2) SNSF_Projects_SDGS.csv
The dataset contains the following columns:

TBD

### 3) Changes made to the original P3 databse
The following variables have been deleted:
* Project Title English | text 
* Responsible Applicant | text 
* Lay Summary Lead (English) | logical 
* Lay Summary (English) | text 
* Lay Summary  Lead (German) | logical 
* Lay Summary (German) | text 
* Lay Summary Lead (French) | logical 
* Lay Summary (French) | text 
* Lay Summary Lead (Italian) | logical 
* Lay Summary (Italian) | text 

## How the SDGs were detected in the text
The ['text2sdg'](https://github.com/dwulff/text2sdg) R package was used to detect SDGs in the project abstracts. 'text2sdg' implements several query based systems to detect SDGs in text. Those systems are shortly described in the following:
* Aurora: These queries were developed by the [Aurora Universities Network](https://aurora-network.global/activity/sustainability/). The Aurora queries were designed to be precise rather than sensitive. To achieve this the queries make use complex keyword-combinations using several different logical search operators. All SDGs (1-17) are covered. [Version 5.0](https://github.com/Aurora-Network-Global/sdg-queries) is used in the 'text2sdg' package. All SDGs (1-17) are covered.
* Siris: These queries were developed by [SIRIS Academic](http://www.sirislab.com/lab/sdg-research-mapping/). The queries are available fromZenodo.org. The SIRIS queries were developed by extracting key terms from the UN official list of goals, targets and indicators as well from relevant literature around SDGs. The query system has subsequently been expanded with a pre-trained word2vec model and an algorithm that selects related words from Wikipedia. There are no queries for SDG-17.
* Elsevier: A dataset containing the SDG queries of [Elsevier](https://www.elsevier.com/connect/sdg-report) (version 1). The queries are available from [data.mendeley.com](https://data.mendeley.com/datasets/87txkw7khs/1). The Elsevier queries were developed to maximize SDG hits on the Scopus database. A detailed description of how each SDG query was developed can be found [here](https://elsevier.digitalcommonsdata.com/datasets/87txkw7khs/1). There are no queries for SDG-17.
* Ontology: A dataset containing the SDG queries based on the keyword ontology of Bautista-Puig and Mauleón (2019). The queries are available from [figshare.com](https://figshare.com/articles/dataset/SDG_ontology/11106113/1). The authors of these queries first created an ontology from central keywords in the SDG UN description and expanded these keywords with keywords they identified in SDG related research output. All SDGs (1-17) are covered.
* SDSN: A dataset containing SDG-specific keywords compiled from several universities from the Sustainable Development Solutions Network (SDSN) Australia, New Zealand & Pacific Network. The authors used UN documents, Google searches and personal communications as sources for the keywords. All SDGs (1-17) are covered.
