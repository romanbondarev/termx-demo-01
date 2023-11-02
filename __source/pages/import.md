KTS provides a list of adapters to import different terminologies. The solution architecture offers the ability to add your own custom adapter.

# FHIR
### Source

You can perform import of the FHIR artifacts using artifacts directly from the HL7 FHIR standard page.  
When you use [HL7 Terminology (THO)](https://terminology.hl7.org/index.html) or terminology related to the [HL7 FHIR resources](http://hl7.org/fhir/resourcelist.html) you should open the tab with JSON presentation and select the link to the raw JSON content (as in the picture below).  

![code-system-json-raw.png](files/71/code-system-json-raw-2.png){width=500}

## CodeSystem
-   Select from menu "Management" -> "Integration" -> "Code system" -> "$sync" ("1"). 
![fhir-import-code-system.png](files/71/fhir-import-code-system.png){width=500}
-   Provide link to JSON file ("2") and press plus button ("3").
> For example for code system [arrivalMode](https://terminology.hl7.org/CodeSystem-v2-0430.html) use `https://terminology.hl7.org/3.1.0/CodeSystem-v2-0430.json`.
{.is-info}
-   Press "Send request" ("4") to initialize import.

## ValueSet, ConceptMap
The import is identical to the code system import.


# ICD10
## WHO Edition
### Source
-   ICD10 official page: [https://www.who.int/standards/classifications/classification-of-diseases](https://www.who.int/standards/classifications/classification-of-diseases)
-   ICD10 official browser: [https://icd.who.int/browse10/2019/en#/](https://icd.who.int/browse10/2019/en#/)
-   ICD10 official download site (you should have an account in WHO): [https://apps.who.int/classifications/apps/icd/ClassificationDownload/DLArea/Download.aspx](https://apps.who.int/classifications/apps/icd/ClassificationDownload/DLArea/Download.aspx)
-   Mirror for the latest ICD10 version: [https://kexus.kodality.com/repository/store-public/terminology/int-icd10en.zip](https://kexus.kodality.com/repository/store-public/terminology/int-icd10en.zip)

### Import
-   Select from menu "Management" -> "Integration" -> "ICD10 WHO import".
-   Press the "Set default data" button.  
![icd10-who-default.png](files/71/icd10-who-default.png){width=500}

> We recomment to use default settings for ICD10 import.
{.is-info}
-   Press "Send request".

## Estonian Edition
### Source
-   Official site of Estonian ICD10 (RHK10 in Estonian): [https://rhk.sm.ee/](https://rhk.sm.ee/)
-   Official download site: [https://pub.e-tervis.ee/classifications/RHK-10](https://pub.e-tervis.ee/classifications/RHK-10)
-   Mirror for latest RHK10: [https://kexus.kodality.com/repository/store-public/terminology/icd10\_v8.zip](https://kexus.kodality.com/repository/store-public/terminology/icd10_v8.zip)

> Please use mirror instead of the official download site. There are was removed `&gt;` tags in V01-Y99.xml file from RHK10v8.zip archive in order to prevent parser from crash.
{.is-warning}

### Import
-   Select from menu "Management" -> "Integration" -> "ICD10 Est import".
-   Press the "Set default data" button.

> We recommend to use default settings for ICD10 import.
{.is-info}
-   Press "Send request".

> We recommend to import WHO Edition of ICD10 first.
{.is-info}

> We recommend to use "icd10..." in the code of code system. In this case concepts of WHO Edition and Estonian Edition will be shared. In other case there will be two independent classification.
{.is-success}

# ATC
## WHO Edition
### Source
-   WHO official site: [https://www.who.int/tools/atc-ddd-toolkit/atc-classification](https://www.who.int/tools/atc-ddd-toolkit/atc-classification)
-   ATC data: [https://www.whocc.no/atc\_ddd\_index/](https://www.whocc.no/atc_ddd_index/)
-   Upcoming registry of European Medicines Agency (required signup and access): [https://spor.ema.europa.eu/rmswi/#/lists/100000093533/terms](https://spor.ema.europa.eu/rmswi/#/lists/100000093533/terms)

### Import
-   Select from menu "Management" -> "Integration" -> "ATC WHO import".
-   Press the "Set default data" button.
> We recommend to use default settings for ATC import.
{.is-info}
-   Press "Send request".

## Estonian Edition
### Source
-   Estonian official registry available from Ravimiamet x-Road services
-   Plain text available through [http://ravimiamet.ee](http://ravimiamet.ee) website -> "e-teenused" → "Andmete allaadimine" → "ATC puu" → "ATC.csv" will be generated without hierarchy.
-   The mirror of ATC.csv is available on [https://kexus.kodality.com/repository/store-public/terminology/est-atc.csv](https://kexus.kodality.com/repository/store-public/terminology/est-atc.csv)

### Import
-   Select from menu "Management" -> "Integration" -> "ATC Est import".
-   Press the "Set default data" button.
> We recomment to use default settings for ATC import.
{.is-info}
-   Press "Send request".
> We recommend to import WHO Edition of ATC first.
{.is-info}

> We recommend to use "atc..." in the code of code system. In this case concepts of WHO Edition and Estonian Edition will be shared. In other case there will be two independent classifications.
{.is-success}

# File importer
The plain text file importers may be used for the import of terminology from comma-separated files (CSV) or tab-separated files (TSV).
-   Your data should be in UTF-8 format.
-   The first line of the file (header) should contain column names.
-   The supported date formats are YYYY-MM-DD, YY-MM-DD, DD.MM.YYYY, DD.MM.YY, DD/MM/YYYY, MM/DD/YYYY, or MM/DD/YY.

## CodeSystem
### Destination
You can import new (select link "*new*") or update existing (search for existing) code systems.  
![file-import-cs-main.png](files/71/file-import-cs-main.png){width=500}
When you create a new code system you should specify also the *title* and *URI*. 
![file-import-cs-new.png](files/71/file-import-cs-new.png){width=500}
With a selection "*Generate ValueSet too*" you can manage when an application will create a new value set with a rule that includes all concepts from created code system.

### Source
Before the import of the code system please read the information about the [code system structure](/terminology-server/guide/resources#relations).  
You can specify the source as a link to the file or upload the file to the server.
![file-import-upload-link.png](files/71/file-import-upload-link.png){width=500}
> When you use a link to the file you should ensure that terminology server (not your computer) have access to the link. It means link should be accessible witout VPN or IP limitation.
{.is-warning}

![file-import-upload-file.png](files/71/file-import-upload-file.png){width=500}

### File content
Pressing the "Analyze" button KTS will validate the file, compose the list of columns, detect their types and formats and scan for empty columns. The results will be presented in a table format:
![file-import-structure-initial.png](files/71/file-import-structure-initial.png){width=500}
For every column from the CSV file, you can (re)define the name of the property in the code system, the data type, format (in the case of date datatype), and language (in the case of text datatype). Checkbox "import" to indicate when to import a column or to skip it.  
By default we propose 4 predefined properties: *concept-code* - should be used as a unique key; *display* - official name; *definition* - the long name of the concept; *description* - additional description (typically represents rules on how to use concept). You can define new properties by choosing "ADD NEW". If you don't specify the KTS property then the CSV column name will be used as property.  
If you have many files with similar structures you can also use the predefined templates with mappings to KTS properties, datatypes, format, and languages. In this case, you should describe only columns that are missing in the template (on the picture below template "[pub.e-tervis.ee](http://pub.e-tervis.ee)" used).  

![file-import-structure-with-template.png](files/71/file-import-structure-with-template.png){width=500}

### Processing
As a result of processing the definition of the code system (button "Process")
-   the new code system will be created (or updated)
-   the new code system properties will be created
-   the new code system version will be created
-   the new value set will be created within the rule referring to the created code system version

For every line in the text file
-   the new concept will be created (if it wasn't created before)
-   the new version of the concept will be added (if data in files differ from the previous version)
-   every imported column will be linked as property or designation to the concept version
-   the concept version will be mapped to the code system version.

### File import through API
You can use API call for code system import. The examples of call is:
~~~
curl -X 'POST' \
  'https://termx.kodality.dev/api/file-importer/code-system/process' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=' \
  -F 'request={parameters}'
~~~

The parameters of import are
|Parameter | Content | Is required? | Description |
|---|---|---|---|
| codeSystem | object | Yes | The reference to the code system. |
| codeSystem.id | string | Yes | Resource unique identifier. Any combination of upper- or lower-case ASCII letters ('A'..'Z', and 'a'..'z', numerals ('0'..'9'), '-' and '.', with a length limit of 64 characters. |
| codeSystem.uri | string | Yes (for first import) | Canonical identifier for this code system, represented as a URI (globally unique). |
| codeSystem.title.$lang | string | Yes (for first import)  | Localized human friendly name. |
| codeSystem.description.$lang | string | No | Localized natural language description of the code system. |
| codeSystem.name | string | No | Machine name. If not specified it calculated from uri (where every word is capitalized and hyphens removed). |
| codeSystem.oid | string | No | Legacy OID identifier. |
| version | object | Yes | The version of code system. |
| version.number | string | Yes | The version number. |
| version.status | code | No | Value from the list: draft, active, retired. Default _draft_. |
| version.releaseDate | date | No | Release date or date expected use since. Default _today()_. |
| type | code | No* | Value from list: _csv_; _tsv_; _json_; _fsh_. (*) Required if file provided. |
| link | url | No* | (*) File or link should be provided |
| importClass | string | No | The name of import class. Default _CS-FILE-IMPORT_. |
| generateValueSet | boolean | No | Should it create value set automatically? Default _false_. |
| valueSetProperties | string array | No | List of value set (generated from code system) properties. |
| dryRun | boolean | Yes | Perform validations only without data changes? Default _true_. |
| cleanVersion | boolean | No | Delete all concepts before import from version? _true_ - Delete, _false_ - Hold. Default _false_. |
| replaceConcept | boolean | No | Behavior on the overlap of concepts? _true_ - Replace, _false_ - Merge. Default _false_. |
| properties | object | Yes | The description of the file to be imported. |
| properties.columnName | string | Yes | The name of column in the import file. |
| properties.propertyName | string | Yes | The name of property in the code system. The name 'concept-code' should be specified for unique identifier, 'hierarchical-concept' same as 'concept-code' with automatical hierarchy detection. The [defined properties](/resources/defined-properties) is recommended. At least one and only one from 'concept-code' and 'hierarchical-concept' should be specified.  |
| properties.propertyType | code | Yes | The value _designation_ and FHIR [concept property types](http://hl7.org/fhir/ValueSet/concept-property-type) are supported. If _designation_ specified it will be imported as concept designation, in other case as property. |
| properties.preferred | string | No | If both 'concept-code' and 'hierarchical-concept' are specified which should be used as concept code. |
| properties.propertyTypeFormat | string | No | Applicable for _datetime_ datatype only to specify the date format. |
| properties.propertyDelimiter | string | No | The separator inside one field. If specified several values of the same property may be created. Applicable for _string_ and _Coding_ only.|
| properties.language | string | No | The language of designation from [AllLanguages](http://hl7.org/fhir/ValueSet/all-languages). Applicable for datatype _designation_ only. |

+++ Example of CodeSystem 12345
```json
{
   "codeSystem":{
      "id":"test12345",
      "uri":"http://example.org/CodeSystem/test12345",
      "title":{
         "en":"Test12345"
      },
      "description":{
         "en":"Test 12345",
         "et":"Test 1 2 3 4 5"
      },
      "name":"test-12345",
      "oid":"1.2.3.4.5.6.7"
   },
   "version":{
      "number":"1.0.0",
      "status":"draft",
      "releaseDate":"2023-09-18T13:02:32.888Z"
   },   
   "link":"C:\\fakepath\\2-8.csv",
   "type":"csv",
   "importClass": "import-class",
   "generateValueSet":false,
   "dryRun":true,
   "cleanVersion":false,
   "replaceConcept":false,   
   "properties":[
      {
         "columnName":"Kood",
         "propertyType":"string",
         "propertyName":"concept-code"
      },
      {
         "columnName":"Nimetus",
         "propertyType":"designation",
         "propertyName":"display",
         "language":"et"
      },
      {
         "columnName":"Pikk_nimetus (SNOMED CT FSN)",
         "propertyType":"designation",
         "propertyName":"display",
         "language":"en"
      },
      {
         "columnName":"Kehtivuse_alguse_kpv",
         "propertyType":"dateTime",
         "propertyTypeFormat":"dd.MM.yyyy",
         "propertyName":"effectiveDate"
      },
      {
         "columnName":"Selgitus",
         "propertyType":"string",
         "propertyName":"comment"
      }
   ]
}
```
+++

## ValueSet
### Destination
You can import new (select link "*Create new*") or update existing (search for existing) value set.  
![file-import-vs-main.png](files/71/file-import-vs-main.png)
When you create a new value set you should specify also the *name* and *URI*. 
![file-import-vs-new.png](files/71/file-import-vs-new.png)

### Source
You can specify the source as a link to the file or upload the file to the server.
![file-import-upload-link.png](files/71/file-import-upload-link.png)
> When you use a link to the file you should ensure that terminology server (not your computer) have access to the link. It means link should be accessible witout VPN or IP limitation.
{.is-warning}

![file-import-upload-file.png](files/71/file-import-upload-file.png)

### File content
Pressing the "Analyze" button KTS will validate the file, compose the list of columns.
From proccesed columns you can select only 2 columns to import - one is concept code and another display. Display is optional.
![file-import-vs-mapping.png](files/71/file-import-vs-mapping.png)

### Processing
As a result of processing the definition of the code system (button "Process")
-   the new value set will be created (or updated)
-   the new value set version will be created
-   the new value set will be created within the existing rule or a rule referring to the selected code system

For every line in the text file
-   the new concept will be added to rule defintion 
-   the concept code will be taken from referred column and also same for display (if referred column was selected)


### File import through API
You can use API call for value set import. The examples of call is:
~~~
curl -X 'POST' \
  'https://termx.kodality.dev/api/file-importer/value-set/process' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=' \
  -F 'request={parameters}'
~~~

The parameters of import are
|Parameter | Content | Is required? | Description |
|---|---|---|---|
| valueSet | object | Yes | The reference to the value set. |
| valueSet.id | string | Yes | Resource unique identifier. Any combination of upper- or lower-case ASCII letters ('A'..'Z', and 'a'..'z', numerals ('0'..'9'), '-' and '.', with a length limit of 64 characters. |
| valueSet.uri | string | Yes (for first import) | Canonical identifier for this value set, represented as a URI (globally unique). |
| valueSet.title.$lang | string | Yes (for first import)  | Localized human friendly name. |
| valueSet.description.$lang | string | No | Localized natural language description of the value set. |
| valueSet.name | string | No | Machine name. If not specified it calculated from uri (where every word is capitalized and hyphens removed). |
| valueSet.oid | string | No | Legacy OID identifier. |
| version | object | Yes | The version of value set. |
| version.number | string | Yes | The version number. |
| version.status | code | No | Value from the list: draft, active, retired. Default _draft_. |
| version.releaseDate | date | No | Release date or date expected use since. Default _today()_. |
| type | code | No* | Value from list: _csv_; _tsv_; _json_; _fsh_. (*) Required if file provided. |
| link | url | No* | (*) File or link should be provided |
| importClass | string | No | The name of import class. Default _VS-FILE-IMPORT_. |
| dryRun | boolean | Yes | Perform validations only without data changes? Default _true_. |
| mapping | object | Yes | The description of the file to be imported. |
| mapping.code | string | Yes | The name of column referred to the concept code in the import file. |
| mapping.display | string | No | The name of column referred to the concept display in the import file.  |
| mapping.retirementDate | string | No | The name of column referred to the concept retirementDate in the import file. Used for validation.  |
| mapping.status | string | No | The name of column referred to the concept status in the import file. Used for validation.  |

+++ Example of ValueSet 12345
```json
{
   "valueSet":{
      "id":"test12345",
      "uri":"http://example.org/ValueSet/test12345",
      "title":{
         "en":"Test12345"
      },
      "description":{
         "en":"Test 12345",
         "et":"Test 1 2 3 4 5"
      },
      "name":"test-12345",
      "oid":"1.2.3.4.5.6.7"
   },
   "version":{
      "number":"1.0.0",
      "status":"draft",
      "releaseDate":"2023-09-18T13:02:32.888Z"
   },   
   "link":"C:\\fakepath\\2-8.csv",
   "type":"csv",
   "importClass": "import-class",
   "dryRun":true,
   "mapping":{
         "code":"Kood",
         "display":"Nimetus"
    }
}
```
+++

## ConceptMap
### Destination
You can import a new (select link "new") or update an existing (search for existing) concept map.
![concept-map-import.png](files/71/concept-map-import.png){width=500}
The source and destination value sets should be created beforehand.

### Source
The CSV file with the predefined structure should be used for the import.
The file should contain next columns:
|Column | Description | Is required? |
|---|---|---|
| sourceCodeSystem | The code system belongs to the source value set. | Optional| 
| sourceVersion | A version of the source code system. | Optional| 
| sourceCode | Code of the concept in the source code system (if specified) or any code system that belongs to the source value set.| Mandatory| 
| targetCodeSystem | Code system belongs to the destination value set. | Optional| 
| targetVersion | A version of the destination code system. | Optional| 
| targetCode | Code of the concept in the destination code system (if specified) or any code system that belongs to the destination value set. | Mandatory| 
| equivalence | Value from the FHIR [concept-map-equivalence](http://hl7.org/fhir/valueset-concept-map-equivalence.html) value set. 'equal' is used if empty. | Optional | 
| comment |  | Optional |  
| dependsOnProperty | Reference to the additional property required for this mapping. | Optional |
| dependsOnSystem | Code system of the property. | Optional| 
| dependsOnValue | Value of the property. | Optional| 

Example of empty [file](/terminology-server/concept-map.csv).

# LOINC
### Source 
-   Official site: [http://loing.org](http://loing.org)
-   The LOINC database: [https://loinc.org/downloads/](https://loinc.org/downloads/)

### Import
-   Select from menu "Management" -> "Integration" -> "LOINC" -> "LOINC import"
-   Specify version you are importing
-   From downloaded zip choose proper files for import ("Parts" and "Loinc terminology" required for minimal import)

File locations in downloaded zip file:
-   Parts - AccessoryFiles/PartFile/Part.csv
-   Loinc terminology - AccessoryFiles/PartFile/LoincPartLink_Primary.csv
-   Supplementary properties - AccessoryFiles/PartFile/LoincPartLink_Supplementary.csv
-   Panels - AccessoryFiles/PanelsAndForms/PanelsAndForms.csv
-   Answer list - AccessoryFiles/AnswerFile/AnswerList.csv
-   Answer list link - AccessoryFiles/AnswerFile/LoincAnswerListLink.csv
-   Translations - AccessoryFiles/LinguisticVariant/...
-   Order observation - AccessoryFiles/LoincUniversalLabOrdersValueSet/LoincUniversalLabOrdersValueSet.csv

![loinc_import.png](files/71/loinc_import.png){width=500}


# SNOMED
### Source
-   Official site: [https://www.snomed.org](https://www.snomed.org)
-   Official SNOMED browser: [https://browser.ihtsdotools.org](https://browser.ihtsdotools.org)
-   Download releases (required account): [https://mlds.ihtsdotools.org](https://mlds.ihtsdotools.org)

### Import
-   Read about RF2 import on the [Snowstorm page](/terminology-server/snowstorm).

# WHO ICF

### Source
-   Official site: [https://www.who.int/standards/classifications/international-classification-of-functioning-disability-and-health](https://www.who.int/standards/classifications/international-classification-of-functioning-disability-and-health)
-   ICF browser: [https://icd.who.int/dev11/proposals/f/icf/en](https://icd.who.int/dev11/proposals/f/icf/en)
-   Official download (required WHO account): [https://icd.who.int/dev11/downloads](https://icd.who.int/dev11/downloads)
-   ICF CSV file [icf.csv](/terminology-server/icf.csv)
-   The example segment from the ICF LinearizationMiniOutput-ICHI-en file  
![icf-example.png](files/71/icf-example.png){width=500}
-   You can use the predefined template with mappings to KTS properties, datatypes, format, and languages. (on the picture below template "icf" used).
![icf-file-import-template.png](files/71/icf-file-import-template.png){width=500}


### Import
-   Use File Importer for ICF file upload
    -   Specify file type as tab-separated (TSV)
    -   *Linearization URI* is the only mandatory field in the file and should be used as an internal id
    -   Please define the data type of the import file according to the picture below  

![icf-mappings.png](files/71/icf-mappings.png){width=500}

# Orphanet
## Rare diseases
### Source
-   Scientific database: [https://www.orphadata.com/orphanet-scientific-knowledge-files/](https://www.orphadata.com/orphanet-scientific-knowledge-files/)
-   Classification of the rare diseases: [https://www.orphadata.com/classifications/](https://www.orphadata.com/classifications/)

### Import
-   Select from menu "Management" -> "Integration" -> "Orphanet" -> "Rare diseases".
-   Press the "Set default data" button.  
![orphanet-rare-deaseses-default.png](files/71/orphanet-rare-deaseses-default.png){width=500}

> Please verify data! Check file name, uri, code system code and name twice.
{.is-warning}
-   Press "Send request".

